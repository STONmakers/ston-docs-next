.. _adv-vhost:

14장. 가상호스트 고급기법
******************

이 장에서는 가상호스트를 활용하여 서비스를 유연하게 구성하는 여러 기법에 대해 설명한다.


.. note::

   - `[동영상 강좌] 해보자! STON Edge Server - Chapter 7. 가상호스트 고급기법 <https://www.youtube.com/watch?v=HFFVcBw0F7c&list=PLqvIfHb2IlKeZ-Eym_UPsp6hbpeF-a2gE&index=7>`_


가상호스트는 보통 원본(Domain 또는 IP목록)과 1:1로 구성되는 것이 기본이다.
하지만 상황에 따라 대표 가상호스트를 여러 하위 가상호스트로 분기하거나,
반대로 독립적인 여러 가상호스트를 하나의 서비스로 포장해야 하는 경우도 발생한다.
각 기능에 따라 :ref:`monitoring_stats_vhost_client` / :ref:`admin-log-access` 의 정책이 다를 수 있음을 유의해야 한다.


.. toctree::
   :maxdepth: 2


.. _adv-vhost-viewpoint:

처리 시점
====================================

실서비스에서는 다양한 방식으로 HTTP 요청을 라우팅하는 경우가 발생한다. 
각 모듈이 동작하는 시점을 명확히 이해해야 안정적인 운영이 가능하다.

먼저 간단한 HTTP 요청부터 시작하자. ::

   http://foo.com/


이 요청은 아래 그림과 같은 흐름으로 처리된다. 

.. figure:: img/avdhostpoint0.png
   :align: center


``HTTP 트랜잭션`` 은 HTTP 요청을 어플리케이션이 처리하는 단위이다.
따라서 가상호스트에 진입하면서 시작되고, 떠나면서 종료된다.


.. note::

   흔히 HTTP 트랜잭션의 시작을 HTTP Layer로 생각하는데 이는 잘못된 이해이다. 
   HTTP Layer의 책임은 HTTP 프로토콜 구현(Parsing & Reponse)에 한정된다.
   파싱된 HTTP 요청이 가상호스트 ``[foo.com]`` 로 분기되어야 비로소 ``HTTP 트랜잭션`` 이 시작되는 것이다.



`URL 전처리`_ 는 ``HTTP Layer`` 와 가상호스트 ``[foo.com]`` 사이에 위치한다. 
`URL 전처리`_ 를 이용하면 ``[foo.com]`` 의 요청을 ``[bar.com]`` 으로 분기시킬 수 있다.


.. figure:: img/avdhostpoint1.png
   :align: center

`URL 전처리`_ 는 ``HTTP 트랜잭션`` 에 영향을 주지 않는다. 
``[bar.com]`` 으로 요청이 진입할 때 ``HTTP 트랜잭션`` 이 시작된다. 
``[foo.com]`` 에는 아무런 액션도 발생하지 않는다.


`Facade 가상호스트`_ 는 통계와 로그를 분리하기 위해 사용한다. 
``[foo.com]`` 이 ``[bar.com]`` 의 facade라면 다음과 같이 동작한다.

.. figure:: img/avdhostpoint2.png
   :align: center

그림에서 알 수 있듯이 ``HTTP 트랜잭션`` 이 2개의 가상호스트에서 발생한다. 
이렇게 중첩된 경우 상위 ``HTTP 트랜잭션`` 이 모든 책임을 위임받는다.
따라서 손쉽게 통계와 로그의 분리가 가능하다.


`Sub-Path 지정`_ 은 분기조건만을 참조한다.

.. figure:: img/avdhostpoint3.png
   :align: center

`Sub-Path 지정`_ 조건에 해당된면 ``[foo.com]`` 은 ``HTTP 트랜잭션`` 을 시작하지 않고 ``[bar.com]`` 으로 재분기한다.


`가상호스트 링크`_ 는 `URL 전처리`_ 와 가상호스트 사이에 존재한다. 

.. figure:: img/avdhostpoint4.png
   :align: center


``HTTP 트랜잭션`` 은 개별 가상호스트에서 독립적으로 이루어진다. 
`가상호스트 링크`_ 는 HTTP 응답을 가로채 재분기 시키는 메카니즘이다.


.. note::

   `URL 전처리`_ 와 `가상호스트 링크`_ 가 같이 사용되는 경우가 종종 있다.
   
   .. figure:: img/avdhostpoint5.png
      :align: center
   
   `가상호스트 링크`_ 는 `URL 전처리`_ 후 분기지점에 위치한다. 
   따라서 URL은 더 이상 변조되지 않으며, 모든 가상호스트는 변조된 경로를 사용한다.



.. _adv-vhost-url-rewrite:

URL 전처리
====================================

`정규표현식 <http://en.wikipedia.org/wiki/Regular_expression>`_ 을 사용하여 요청된 URL을 변경한다.
URL전처리가 설정되어 있다면 모든 클라이언 요청(HTTP 또는 File I/O)은 반드시 URL Rewriter를 거친다.

.. figure:: img/urlrewrite1.png
   :align: center

   URL Rewriter를 통과해야 가상호스트에 갈 수 있다.

만약 URL Rewriter에 의해 접근하려는 Host이름이 변경되었다면 클라이언트 HTTP요청의 Host헤더가 변경된 것으로 간주한다.
URL 전처리는 가상호스트 설정(vhosts.xml)에 설정한다.
대부분의 설정이 가상호스트에 종속되지만, URL전처리의 경우 클라이언트가 요청한 Host의 이름을 변경할 수 있으므로 가상호스트와 같은 레벨로 설정한다. ::

   # vhosts.xml

   <Vhosts>
      <Vhost ...> ... </Vhost>
      <Vhost ...> ... </Vhost>
      <URLRewrite ...> ... </URLRewrite>
      <URLRewrite ...> ... </URLRewrite>
   </Vhosts>

멀티로 설정할 수 있으며 순차적으로 정규표현식 일치 여부를 비교한다. ::

   # vhosts.xml - <Vhosts>

   <URLRewrite AccessLog="Replace">
       <Pattern>www.exmaple.com/([^/]+)/(.*)</Pattern>
       <Replace>#1.exmaple.com/#2</Replace>
   </URLRewrite>

-  ``<URLRewrite>``

   URL전처리를 설정한다.
   ``AccessLog (기본: Replace)`` 속성은  Access로그에 기록될 URL을 설정한다.
   ``Replace`` 인 경우 변환 후 URL(/logo.jpg)을, ``Pattern`` 인 경우 변환 전
   URL(/baseball/logo.jpg)을 Access로그에 기록한다.

   -  ``<Pattern>`` 매칭시킬 패턴을 설정한다.
      한개의 패턴은 ( ) 괄호를 사용하여 표현된다.

   -  ``<Replace>`` 변환형식을 설정한다.
      일치된 패턴에 대해서는 #1, #2와 같이 사용할 수 있다. #0는 요청 URL전체를 의미한다.
      패턴은 최대 9개(#9)까지 지정할 수 있다.

처리량은 :ref:`monitoring_stats` 로 제공되며 :ref:`api-graph-urlrewrite` 으로도 확인할 수 있다.
URL전처리는 :ref:`media-trimming` , :ref:`media-hls` 등 다른 기능들과 결합하여 표현을 간결하게 만든다. ::

   # vhosts.xml - <Vhosts>

   <URLRewrite>
       <Pattern>example.com/([^/]+)/(.*)</Pattern>
       <Replace>example.com/#1.php?id=#2</Replace>
   </URLRewrite>
   // Pattern : example.com/releasenotes/1.3.4
   // Replace : example.com/releasenotes.php?id=1.3.4

   <URLRewrite>
       <Pattern>example.com/download/(.*)</Pattern>
       <Replace>download.example.com/#1</Replace>
   </URLRewrite>
   // Pattern : example.com/download/1.3.4
   // Replace : download.example.com/1.3.4

   <URLRewrite>
       <Pattern>example.com/img/(.*\.(jpg|png).*)</Pattern>
       <Replace>example.com/#1/STON/composite/watermark1</Replace>
   </URLRewrite>
   // Pattern : example.com/img/image.jpg?date=20140326
   // Replace : example.com/image.jpg?date=20140326/STON/composite/watermark1

   <URLRewrite>
       <Pattern>example.com/preview/(.*)\.(mp3|mp4|m4a)$</Pattern>
       <Replace><![CDATA[example.com/#1.#2?&end=30&boost=10&bandwidth=2000&ratio=100]]></Replace>
   </URLRewrite>
   // Pattern : example.com/preview/audio.m4a
   // Replace : example.com/audio.m4a?end=30&boost=10&bandwidth=2000&ratio=100

   <URLRewrite>
       <Pattern>example.com/(.*)\.mp4\.m3u8$</Pattern>
       <Replace>example.com/#1.mp4/mp4hls/index.m3u8</Replace>
   </URLRewrite>
   // Pattern : example.com/video.mp4.m3u8
   // Replace : example.com/video.mp4/mp4hls/index.m3u8

   <URLRewrite>
       <Pattern>example.com/(.*)_(.*)_(.*)</Pattern>
       <Replace>example.com/#0/#1/#2/#3</Replace>
   </URLRewrite>
   // Pattern : example.com/video.mp4_10_20
   // Replace : example.com/example.com/video.mp4_10_20/video.mp4/10/20

.. note::

   다음처럼 유사한 서브도메인이 있는 경우 주의해야 한다. ::
   
      image.example.com
      myimage.example.com
      
   정규표현식에서는 image.exampe.com으로 패턴을 생성한 경우 myimage.example.com도 패턴과 일치하는 것으로 간주된다. 
   이를 방지하기 위해 맨 앞에 글자없음을 ``^`` 로 표기해주어야 image.example.com만 매칭시킬 수 있다. ::

      <URLRewrite>
         <Pattern>^image.example.com/img/(.*\.(jpg|png).*)</Pattern>
         <Replace>image.example.com/#1/STON/composite/watermark1</Replace>
      </URLRewrite>


패턴표현에 XML의 5가지 특수문자( " & ' < > )가 들어갈 경우 반드시 <![CDATA[ ... ]]>로 묶어주어야 올바르게 설정된다.
:ref:`wm` 을 통해 설정할 때 모든 패턴은 CDATA로 처리된다.



.. _adv-vhost-url-rewrite-protocol:

프로토콜 분기
---------------------

URL 전처리 시 프로토콜 조건을 설정한다. ::

   <URLRewrite AccessLog="Replace" Protocol="ALL">
      <Pattern>www.exmaple.com/([^/]+)/(.*)</Pattern>
      <Replace>#1.exmaple.com/#2</Replace>
   </URLRewrite>


-  ``Protocol (기본: ALL)`` 속성

   -  ``ALL`` 모든 프로토콜 매칭
   -  ``HTTP`` HTTP에 대해서만 패턴 매칭
   -  ``HTTPS`` HTTPS 에 대해서만 패턴 매칭
   -  ``HTTP2`` HTTP2 에 대해서만 패턴 매칭


이 기능을 이용해 프로토콜에 따라 서로 다른 가상호스트를 운영할 수 있다.




.. _adv-vhost-facadevhost:

Facade 가상호스트
====================================

``<Alias>`` 는 가상호스트의 별명만을 추가하는 것이므로 통계와 로그가 분리되지 않는다.
가상호스트는 공유하지만 도메인에 따라 :ref:`monitoring_stats_vhost_client` 와 :ref:`admin-log-access` 를 분리하고 싶은 경우 Facade가상호스트를 설정한다.

.. figure:: img/adv_vhost_facade.png
   :align: center

   facade는 통계와 로그만 수집한다.

::

    # vhosts.xml - <Vhosts>

    <Vhost Name="example.com">
       ...
    </Vhost>

    <Vhost Name="another.com" Status="facade:example.com">
       ...
    </Vhost>

``Status`` 속성의 값을 ``facade:`` + ``가상호스트`` 로 설정한다.
예제의 경우 :ref:`monitoring_stats_vhost_client` 와 :ref:`admin-log-access` 는 example.com이 아닌 클라이언트가 요청한 도메인인 another.com으로 수집된다.



.. _adv-vhost-sharevhost:

Share 가상호스트
====================================

가상호스트를 구성하는 3요소는 다음과 같다.

-  설정
-  캐싱객체
-  원본


이는 가상호스트 안에 격리되어 있으며 상호 공유되지 않는다.

.. figure:: img/adv_vhost_share1.png
   :align: center


STON은 ``share`` 가상호스트라는 개념으로 캐싱객체를 공유하는 기능을 제공한다.

.. figure:: img/adv_vhost_share2.png
   :align: center


``share`` 로 지정된 가상호스트는 자신의 캐싱객체 대신 공유영역에 있는 캐싱객체를 사용하여 상호 공유가 가능하다.
예를 들어 ``foo.com`` 가상호스트에서 캐싱한 객체를 ``bar.com`` 에서 공유하고 싶다면 다음 순서를 따른다.

1.  ``foo.com`` 을 ``share`` 가상호스트로 만든다. ::

         # vhosts.xml - <Vhosts>

         <Vhost Name="example.com" Status="share">
            ...
         </Vhost>


2.  ``bar.com`` 을 ``share`` 가상호스트로 만들며 ``foo.com`` 을 참조하도록 한다. ::

         # vhosts.xml - <Vhosts>

         <Vhost Name="bar.com" Status="share:foo.com">
            ...
         </Vhost>



위와 같이 구성하면 ``foo.com`` 과 ``bar.com`` 은 같은 URL에 대해서는 캐싱 객체를 공유한다.
다시 말해 ``foo.com`` 에 의해 캐싱된 객체는 ``bar.com`` 으로 접근해도 재캐싱하지 않고 ``TCP_HIT`` 로 서비스 된다.
``bar.com`` 에 의해 먼저 캐싱된 객체도 동일하게 동작한다.

``share`` 모드에는 가상호스트 이름이 캐싱키로 붙는다. 
따라서 아래와 같이 선언만 하는 것으로는 아무 것도 공유되지 않는다. ::

   <Vhost Name="foo.com" Status="share"> ... </Vhost>
   <Vhost Name="bar.com" Status="share"> ... </Vhost>
   <Vhost Name="que.com" Status="share"> ... </Vhost>


상호 캐싱객체를 공유하려면 캐싱키에 사용될 적절한 공유이름을 지정해주어야 한다. ::

   <Vhost Name="foo.com" Status="share:temp"> ... </Vhost>
   <Vhost Name="bar.com" Status="share:temp"> ... </Vhost>
   <Vhost Name="que.com" Status="share:temp"> ... </Vhost>
   <Vhost Name="football.com" Status="share:sports"> ... </Vhost>
   <Vhost Name="soccer.com" Status="share:sports"> ... </Vhost>


공유 그룹 개수에 제약은 없으며, ``share`` 가상호스트는 실시간으로 적용/해제가 가능하다.


.. warning::

   ``share`` 가상호스트는 객체만 공유할 뿐 설정/원본을 독립적으로 유지하기 때문에 관리가 매우 어렵다.

   1.  무결성이 보장되지 않는다. 멀티 가상호스트로 동시에 유입된 공유객체는 각자 다른 설정과 다른 원본으로부터 분할 캐싱된다.
   2.  캐싱개수가 많아져 패턴 Purge 등 객체 관리기능의 성능이 저하된다.
   3.  객체 유입과 서비스 경로가 명확하지 않아 서비스 추적이 어렵다.




고급 기능 ``powered by M2``
====================================

이외에 실서비스에서 즉시 활용 가능한 다양한 `인프라 구성 패턴 <https://csp-kr.readthedocs.io/ko/latest/patterns/pattern_infra.html>`_ 이 존재한다. 
`인프라 구성 패턴 <https://csp-kr.readthedocs.io/ko/latest/patterns/pattern_infra.html>`_ 은 `M2 파이프라인 플랫폼 <https://m2-kr-next.readthedocs.io/>`_ 의 `위치 투명성 <https://m2-kr.readthedocs.io/ko/latest/guide/caching.html#engine-caching-transparency>`_ 에 기반하여 구현된다.


.. _adv-vhost-link:

가상호스트 링크
-------------------------------------------

콘텐츠가 여러 원본에 분산되어 있다면, 가상호스트 링크를 활용하여 콘텐츠가 통합되어 있는 것처럼 서비스가 가능하다.


.. note::

   - 이 기능을 활용하면 `인프라 구성 패턴 <https://csp-kr.readthedocs.io/ko/latest/patterns/pattern_infra.html>`_ 의 위치 투명성을 손쉽게 구현할 수 있다.



특히 On-Premise에서 클라우드로 스토리지를 마이그레이션하거나, 스토리지의 용량, 비용 등의 이유로 콘텐츠가 분산되어 있는 환경에서 유용하다.

.. figure:: img/adv_vhost_link.png
   :align: center

   cloud.com에 없는 콘텐츠는 nas.com이 처리한다.

::

   # vhosts.xml - <Vhosts><Vhost>

   <VhostLink Condition="...">...</VhostLink>

-  ``<VhostLink>`` 요청을 위임할 가상호스트 이름. 콘텐츠에 대한 원본 응답이 ``Condition`` 을 만족하면 지정된 가상호스트로 요청을 위임한다. 단 하나만 설정할 수 있다.

   - ``Condition`` HTTP 응답코드/패턴(1xx, 2xx, 3xx, 4xx, 5xx), fail(원본에서 캐싱하지 못한 경우)

클라이언트 요청이 다른 가상호스트로 위임되더라도 :ref:`monitoring_stats_vhost_client` 와 :ref:`admin-log-access` 는 클라이언트가 접근한 가상호스트에 기록된다.

.. note::

   링크 관계에 있는 가상호스트 설정이 다를 경우 의도치 않게 동작할 수 있음을 주의한다.
   가상호스트 링크가 A(단순 캐싱) -> B(이미지 압축)로 맺어져 있다면,
   A에서 처리된 이미지는 압축되지 않지만 B에서 처리된 이미지는 압축된다.

예를 들어 nas.com의 콘텐츠를 cloud.com으로 이전 중일 경우, cloud.com에 없는(=404 Not Found) 콘텐츠에 대해서만 nas.com으로 요청을 보낼 수 있다.
아래의 경우 요청이 nas.com에 의해 처리되더라도 :ref:`monitoring_stats_vhost_client` 와 :ref:`admin-log-access` 는 cloud.com에 기록된다.

::

   # vhosts.xml - <Vhosts>

   // cloud.com에 없는(=404 Not Found) 콘텐츠는 nas.com에서 서비스한다.
   <Vhost Name="cloud.com">
     <VhostLink Condition="404">nas.com</VhostLink>
   </Vhost>

   <Vhost Name="nas.com">
   </Vhost>


:ref:`admin-log-access` 의 vhostlink 필드를 통해 클라이언트 요청이 어느 가상호스트에서 처리되었는지 알 수 있다.
"-" 는 요청이 링크되지 않았음을 의미하며 "nas.com" 은 해당 요청이 링크되어 nas.com에서 처리되었음을 의미한다. ::

    #Fields: date time s-ip cs-method cs-uri-stem ...(중략)... vhostlink
    2016.11.24 16:52:24 220.134.10.5 GET /web/h.gif ...(중략)... -
    2016.11.24 16:52:26 220.134.10.5 GET /favicon.ico ...(중략)... nas.com

링크가 여러 번 발생했다면 "+"를 구분자로 링크된 모든 가상호스트가 명시된다.
이 경우 가장 마지막에 위치한 가상호스트가 최종 요청을 처리한 가상호스트이다.

다음과 같이 여러 가상호스트를 다른 조건으로 링크할 수 있다.

::

   # vhosts.xml - <Vhosts>

   // 원본서버가 5xx로 응답했거나 캐싱하지 못했을 때(=fail) 해당 요청을 bar.com에게 위임한다.
   <Vhost Name="foo.com">
     <VhostLink Condition="5xx,fail">bar.com</VhostLink>
   </Vhost>

   // 원본서버가 4xx로 응답했을 때 해당 요청을 helloworld.com에게 위임한다.
   <Vhost Name="bar.com">
     <VhostLink Condition="4xx">helloworld.com</VhostLink>
   </Vhost>

   // 원본서버에서 403, 404 또는 5xx로 응답했을 때 해당 요청을 example.com에게 위임한다.
   <Vhost Name="helloworld.com">
     <VhostLink Condition="403,404,5xx">example.com</VhostLink>
   </Vhost>

   // 더 이상 위임하지 않는다.
   <Vhost Name="example.com">
   </Vhost>

.. figure:: img/adv_vhost_link_worst.png
   :align: center

   억지스럽지만 가능하다.

위 예제의 경우 foo.com의 :ref:`admin-log-access` 는 다음과 같다. ::

   #Fields: date time s-ip cs-method cs-uri-stem ...(중략)... vhostlink
   2016.11.24 16:52:24 220.134.10.5 GET /test.jpg ...(중략)... bar.com+helloworld.com+example.com

다음의 경우 링크는 즉시 중단된다.

* 대상 가상호스트가 존재하지 않는 경우 (foo.com -> ?)
* 자기 자신을 대상 가상호스트로 지정한 경우 (foo.com -> foo.com)
* 재귀링크(Recursive Link)가 발생한 경우 (foo.com -> bar.com -> foo.com)



.. _adv-vhost-redirection-trace:

Redirect 추적
-------------------------------------------

원본서버에서 Redirect계열( ``301`` , ``302`` , ``303`` , ``307`` , ``308`` )로 응답하는 경우 ``Location`` 헤더를 추적하여 콘텐츠를 요청한다.

   .. figure:: img/conf_redirectiontrace.png
      :align: center

      클라이언트는 Redirect여부를 모른다.

::

   # server.xml - <Server><VHostDefault><OriginOptions>
   # vhosts.xml - <Vhosts><Vhost><OriginOptions>

   <RedirectionTrace>OFF</RedirectionTrace>

-  ``<RedirectionTrace>``

   - ``OFF (기본)`` 3xx 응답으로 저장된다.

   - ``ON`` Location헤더에 명시된 주소에서 콘텐츠를 다운로드 한다.
     형식에 맞지 않거나 Location헤더가 없는 경우에는 동작하지 않는다.
     무한히 Redirect되는 경우를 방지하기 위하여 1회만 추적한다.


특정 URL 패턴에 대해서만 동작시킬 수 있다. ::

   # server.xml - <Server><VHostDefault><OriginOptions>
   # vhosts.xml - <Vhosts><Vhost><OriginOptions>

   <RedirectionTrace ResCode="302,307">ON
      <URL>*.ts</URL>
      <URL>*.mp4</URL>
   </RedirectionTrace>


``<RedirectionTrace>`` 하위에 ``<URL>`` 들을 열거하면 ``Location`` 헤더 값의 특정 패턴에 대해서만 추적한다.


.. _adv-vhost-sub-path:

Sub-Path 지정
-------------------------------------------

한 가상호스트에서 경로에 따라 다른 가상호스트가 처리하도록 설정할 수 있다.

.. figure:: img/adv_vhost_subpath.png
   :align: center

   통계/로그는 요청을 최종처리한 각각의 가상호스트에 기록된다.


::

   # vhosts.xml - <Vhosts>

   <Vhost Name="sports.com">
     <Sub Status="Active">
       <Path Vhost="baseball.com">/baseball/<Path>
       <Path Vhost="football.com">/football/<Path>
       <Path Vhost="photo.com">/*.jpg<Path>
     </Sub>
   </Vhost>

   <Vhost Name="baseball.com" />
   <Vhost Name="football.com" />
   <Vhost Name="photo.com" />

-  ``<Sub>`` 경로나 패턴이 일치하면 해당 요청을 다른 가상호스트로 보낸다.
   일치하지 않는 경우만 현재 가상호스트가 처리한다.

   - ``Status (기본: Active)`` Inactive인 경우 무시한다.

   -  ``<Path>`` 클라이언트가 요청한 URI와 경로가 일치하면 ``Vhost`` 로 해당 요청을 보낸다.
      값은 경로 또는 패턴만 가능하다. ::

         <Path Vhost="baseball.com">baseball<Path>
         <Path Vhost="photo.com">*.jpg<Path>

      위와 같이 입력해도 각각 /baseball/과 /*.jpg로 인식된다.

예를 들어 클라이언트가 다음과 같이 요청했다면 해당 요청은 가상호스트 football.com이 처리한다. ::

   GET /football/rank.html HTTP/1.1
   Host: sports.com


