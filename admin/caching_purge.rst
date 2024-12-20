.. _caching-purge:

5장. Caching 무효화
******************

이 장에서는 Caching된 콘텐츠를 무효화하는 방법에 대해 설명한다.
업계용어로 Purge로 통칭하지만 다양한 상황과 환경으로 인해 세분화된 API가 필요하다.


.. note::

   - `[동영상 강좌] 해보자! STON Edge Server - Chapter 8. 컨텐츠 제어 <https://www.youtube.com/watch?v=bo-AItkIk-w&index=8&list=PLqvIfHb2IlKeZ-Eym_UPsp6hbpeF-a2gE>`_


원본으로부터 캐싱된 콘텐츠는 :ref:`caching-policy-ttl` 에 기반한 갱신주기를 가진다.
하지만 명백히 콘텐츠가 변경되었고 관리자가 이를 즉시 반영하고 싶을 경우 :ref:`caching-policy-ttl` 이 만료될 때까지 기다릴 필요는 없다.
`Purge`_ / `Expire`_ / `HardPurge`_ 등을 사용하면 즉시 콘텐츠를 무효화시킬 수 있다.

무효화 API는 단순히 브라우저에 의해 호출되는 경우도 있지만 자동화되어 있는 경우가 많다.
가령 FTP를 통한 파일 업로드가 끝나면 즉시 `Purge`_ 를 호출하는 식이다.
관리자는 다음과 같이 몇가지 동작방식에 대해 설정할 수 있다. ::

   # server.xml - <Server><VHostDefault><Options>
   # vhosts.xml - <Vhosts><Vhost><Options>
   
   <Purge2Expire>NONE</Purge2Expire>
   <RootPurgeExpire>ON</RootPurgeExpire>
   <RootHardPurge>ON</RootHardPurge>
   <ResCodeNoCtrlTarget>200</ResCodeNoCtrlTarget>
   <ResCodeDenyCtrlTarget>200</ResCodeDenyCtrlTarget>

-  ``<Purge2Expire> (기본: NONE)``

   `Purge`_ 요청을 설정에 따라 `Expire`_ 로 처리한다.
   예를 들어 특정 패턴(*.jpg)를 `Purge`_ 하는 경우 의도하지 않게 많은 컨텐츠가 
   삭제되어 원본에 과도한 부하를 발생시킬 수 있다.
   이런 경우 `Expire`_ 로 처리하도록 설정하면 과도한 원본부하를 방지할 수 있다.
   
   - ``NONE`` `Expire`_ 로 처리하지 않는다.
   - ``ROOT`` 도메인 전체(/*)에 대한 `Purge`_ 를 `Expire`_ 로 처리한다.
   - ``PATTERN`` 모든 패턴 `Purge`_ 를 `Expire`_ 로 처리한다.
   - ``ALL`` 모든 `Purge`_ 를 `Expire`_ 로 처리한다.

-  ``<RootPurgeExpire> (기본: ON)``
   
   전체 콘텐츠에 대한 의도하지 않은 `Purge`_ / `Expire`_ 는 과도한 원본서버 부하를 발생시킬 수 있다. 
   이 설정을 통하여 전체 콘텐츠에 대한 `Purge`_ / `Expire`_ 를 차단할 수 있다. 
   이 설정은 ``<Purge2Expire>`` 보다 우선한다.
   
   - ``ON`` `Purge`_ / `Expire`_ 를 허용한다.
   - ``PURGE`` `Purge`_ 만 허용한다.
   - ``EXPIRE`` `Expire`_ 만 허용한다.
   - ``OFF`` 모든 `Purge`_ / `Expire`_ 를 금지한다.

-  ``<RootHardPurge> (기본: ON)``
   
   전체 콘텐츠( ``/*`` ) 에 대한 `HardPurge`_ 는 모든 캐싱을 삭제하기 때문에 매우 위험하다.

   - ``ON`` 전체 콘텐츠의 `HardPurge`_ 를 허용한다.
   - ``OFF`` 전체 콘텐츠의 `HardPurge`_ 를 금지한다.


-  ``<ResCodeNoCtrlTarget> (기본: 200)``

   `Purge`_ , `Expire`_ , `HardPurge`_ , `ExpireAfter`_ 의 대상객체가 없을 때의 HTTP 응답코드를 설정한다.

-  ``<ResCodeDenyCtrlTarget> (기본: 200)``
   
   ``<RootPurgeExpire>`` , ``<RootHardPurge>`` 설정에 의해서 Control API 호출이 거부 될 경우 설정된 응답코드로 응답 한다.



대상 지정은 URL, 패턴 2가지로 표현한다. ::

   example.com/logo.jpg      // URL
   example.com/img/          // URL
   example.com/img/*.jpg     // 패턴
   example.com/img/*         // 패턴
   
명확한 URL 외에 패턴(*.jpg)으로 무효화가 가능하다.
하지만 작업을 수행하기 전까지 대상개수를 명확히 알 수 없다.
이는 자칫 관리자의 의도와 다르게 너무 많은 대상을 지정할 수 있다.
이는 실제로 CPU자원을 너무 많이 소모하게 되어 시스템 전체에 부담을 줄 수 있다.
   
그러므로 실 서비스 중에는 명확한 URL만을 사용할 것을 강력히 권장한다.
패턴표현은 서비스에서 배제된 상태에서 관리용도로 사용하기 위함이다.


.. note::

   보안적인 이유로 example.com/files/ 같은 특정 디렉토리에 대한 접근은 403 FORBIDDEN등으로 차단된다. 
   하지만 루트 디렉토리는 예외를 가진다. 
   예를 들어 사용자가 example.com에 접근하면 브라우저는 루트 디렉토리(/)를 요청한다. ::
   
      GET / HTTP/1.1
      Host: example.com
   
   이에 대해 웹서버는 관리자가 설정한 기본 페이지(아마도 index.html 또는 index.htm)로 응답한다.
   분명 웹 서비스 구성에서 루트 디렉토리(/)는 디렉토리가 아닌 페이지로 동작한다.
   
   하지만 Cache서버는 루트 디렉토리(/)에 접근했더니 200 OK 페이지가 왔다고 이해한다.
   심지어 원본서버가 어떤 페이지를 응답했는지 알지 못한다.
   간단히 정리하면 Cache서버의 관점에서는 디렉토리 표현도 URL의 한 종류일 뿐이다. ::
   
      example.com/img/          // example.com 가상호스트의 /img/ 에 접근한 결과 페이지
      example.com/              // example.com 가상호스트의 기본 페이지(/)
      example.com/img/*         // example.com 가상호스트의 /img 디렉토리와 그 하위 페이지
      example.com/*             // example.com 가상호스트의 모든 콘텐츠
         


.. toctree::
   :maxdepth: 2


.. _api-cmd-purge:

Purge
====================================

타겟 컨텐츠를 무효화시켜 원본서버로부터 컨텐츠를 다시 다운로드 받도록 한다. 
Purge후 최초 접근 시점에 원본서버로부터 컨텐츠를 다시 캐싱한다. 
만약 원본서버에 장애가 발생하여 컨텐츠를 가져올 수 없다면 무효화된 컨텐츠를 다시 복원시켜 
서비스에 장애가 없도록 처리한다. 
이렇게 복원된 컨텐츠는 해당 시점으로부터 ConnectTimeout설정만큼 뒤에 갱신한다. ::

    http://127.0.0.1:10040/command/purge?url=...
    
타겟 컨텐츠는 URL, 패턴으로 지정할 수 있을 뿐만 아니라 "|"(Vertical Bar)를 
구분자를 사용하여 복수의 도메인에 복수의 타겟을 지정할 수 있다. 
만약 도메인 이름이 생략되었다면 최근 사용된 도메인을 사용한다. ::

    http://127.0.0.1:10040/command/purge?url=http://www.site1.com/image.jpg
    http://127.0.0.1:10040/command/purge?url=www.site1.com/image.jpg
    http://127.0.0.1:10040/command/purge?url=www.site1.com/image/bmp/
    http://127.0.0.1:10040/command/purge?url=www.site1.com/image/*.bmp
    http://127.0.0.1:10040/command/purge?url=www.site1.com/image1.jpg|/css/style.css|/script.js
    http://127.0.0.1:10040/command/purge?url=www.site1.com/image1.jpg|www.site2.com/page/*.html
    
결과는 JSON형식으로 제공된다. 
타겟 컨텐츠 개수/용량 및 처리시간(단위: ms)이 명시된다. 
이미 Purge 된 컨텐츠는 다시 Purge되지 않는다. ::

    {
        "version": "2.0.0",
        "method": "purge",
        "status": "OK",
        "result": { "Count": 24, "Size": 3747491, "Time": 12 }
    }
    
``<Purge2Expire>`` 를 통해 특정조건의 Purge를 Expire로 동작하도록 설정할 수 있다.
결과없는 응답에 대해서는 ``<ResCodeNoCtrlTarget>`` 로 HTTP 응답코드를 설정할 수 있다.


.. note::
   
   원본서버가 장애로 인해 모두 배제되었다면 컨텐츠를 갱신할 수 없기 때문에 Purge가 동작하지 않는다.
   

.. _api-cmd-expire:
   
Expire
====================================

타겟 컨텐츠의 TTL을 즉시 만료시킨다. 
Expire후 최초 접근 시점에 원본서버로부터 변경여부를 확인한다. 
변경되지 않았다면 TTL연장만 있을 뿐 컨텐츠 다운로드는 발생하지 않는다. ::

    http://127.0.0.1:10040/command/expire?url=...
    
그 외의 모든 동작은 `Purge`_ 와 동일하다.


.. _api-cmd-expireafter:
   
ExpireAfter
====================================

타겟 컨텐츠의 TTL만료 시간을 현재(API호출시점)로부터 입력된 시간(초)만큼 뒤에 설정한다. 
ExpireAfter로 만료시간을 앞당겨 컨텐츠를 더 빨리 갱신하거나, 
반대로 만료시간을 늘려 원본서버 부하를 줄일 수 있다. ::

   http://127.0.0.1:10040/command/expireafter?sec=86400&url=...

함수 호출규격은 `Purge`_ / `Expire`_ 와 유사하지만 sec파라미터(단위: 초)를 통해 
TTL만료 시간을 지정할 수 있다. 
sec가 생략된다면 기본 값은 1일(86400초)로 설정되며 0을 입력할 경우 실패한다. 
결과는 `Purge`_ / `Expire`_ 와 동일하지만 원본서버 장애여부와 상관없이 동작한다. 
결과없는 응답에 대해서는 ``<ResCodeNoCtrlTarget>`` 로 HTTP 응답코드를 설정할 수 있다.

.. note::
   ExpireAfter는 캐싱되어있는 컨텐츠의 현재 만료시간만을 설정할 뿐 커스텀TTL이나 
   설정된 기본 TTL을 변경시키는 API가 아니다. 
   ExpireAfter 호출뒤에 캐싱된 컨텐츠들은 영향을 받지 않는다.
   
   
   url파라미터를 먼저 입력하는 경우 sec파라미터가 url파라미터의 QueryString으로 인식될 수 있다. 
   그러므로 sec파라미터가 먼저 입력되는 것이 안전하다.
   
   

.. _api-cmd-hardpurge:
   
HardPurge
====================================

`Purge`_ / `Expire`_ / `ExpireAfter`_ 이상의 API는 원본서버 장애상황에서도 컨텐츠가 
사라지지 않고 정상적으로 동작한다. 
하지만 HardPurge는 컨텐츠의 완전한 삭제를 의미한다. 
HardPurge는 가장 강력한 삭제방법이지만 삭제한 컨텐츠는 원본서버에 장애가 발생해도 되살릴 수 없다. 
결과없는 응답에 대해서는 ``<ResCodeNoCtrlTarget>`` 로 HTTP 응답코드를 설정할 수 있다. ::

    http://127.0.0.1:10040/command/hardpurge?url=...



Purge 기본동작
====================================

Purge API가 호출될 때 컨텐츠 복구 여부를 선택한다. ::

   # server.xml - <Server><Cache>
   
   <Purge>Normal</Purge>
      
-  ``<Purge>`` 
   
   - ``Normal (기본)`` `Purge`_ 로 동작한다. (원본장애 시 복구 함)
   
   - ``Hard`` `HardPurge`_ 로 동작한다. (원본장애 시 복구하지 않음)



.. _caching-purge-http-method:

HTTP Method
====================================

무효화 API를 확장 HTTP Method로 호출할 수 있다. ::

    PURGE /sample.dat HTTP/1.1
    host: ston.winesoft.co.kr
    
HTTP Method는 기본적으로 Manager포트와 서비스(80)포트에서 동작한다. 
서비스포트로 요청되는 HTTP Method의 :ref:`env-host` 에서 설정한다.


비동기 모드를 사용하는 경우 다음과 같이 HTTP Method가 변경된다. ::

   // 비동기 expire
   ASYNCEXPIRE /index.html HTTP/1.1
   Host: foo.com:10040

   // 비동기 purge
   ASYNCPURGE /* HTTP/1.1
   Host: foo.com:10040

   // 비동기 hardpurge
   ASYNCHARDPURGE /*.html HTTP/1.1
   Host: foo.com:10040


.. _api-etc-post:

POST 규격
====================================

무효화 API를 다음과 같이 POST로 호출할 수 있다. ::

   POST /command/purge HTTP/1.1
   Content-Length: 37
 
   url=http://ston.winesoft.co.kr/sample.dat
    


.. _caching-purge-async:

동기/비동기 무효화
====================================

무효화 API의 기본동작은 동기방식이다. 
설정을 통해 비동기로 동작하도록 설정할 수 있다. ::

   #server.xml

   <Cache>
      <ControlAPI>sync</ControlAPI>
      <AsyncControlTarget>PATTERN</AsyncControlTarget>
   </Cache>


-  ``<ControlAPI>`` 
   
   - ``sync (기본)`` 무효화 API가 동기로 동작한다.
   
   - ``async`` 무효화 API가 비동기로 동작한다.


-  ``<AsyncControlTarget>`` 비동기 무효화로 구성된 상태라도, 요청된 URL에 따라 선별적으로 비동기 처리한다.
   
   - ``pattern (기본)`` 패턴(*) 요청에 대해서만 비동기 처리한다.
   
   - ``all`` 모든 요청을 비동기 처리한다.


비동기로 동작하는 경우 무효화 요청은 큐에 저장되며 백그라운드로 수행된다.

.. note::

   -  백그라운드 수행 이전이라도 접근되는 콘텐츠가 무효화 대상이라면 즉시 만료된다.

   -  비동기 API를 호출했으나 동기로 처리되었다면 ``201 Created`` 로 응답한다.


호출 규격은 아래과 같다. ::

  /command/async/expire?url=foo.com/index.html
  /command/async/purge?url=foo.com/*
  /command/async/hardpurge?url=foo.com/*.jpg


비동기 무효화 동작의 세부 설정은 다음과 같다. ::

   # server.xml - <Server><Cache>

   <Performance>
      <MaxAsyncCacheCtrl>100000</MaxAsyncCacheCtrl>
      <PreCacheControl Max="5000" FirstOnly="OFF">ON</PreCacheControl>
   </Performance>


-  ``<MaxAsyncCacheCtrl> (기본: 100000)`` 비동기 무효화 최대 저장개수

-  ``<PreCacheControl> (기본: ON)`` 접근되는 콘텐츠에 대해 저장된 비동기 무효화를 매칭한다.

   -  ``Max (기본: 5000)`` 가상호스트별로 매칭할 비동기 무효화 최대 개수
   
   -  ``FirstOnly (기본: OFF)`` ON인 경우 첫번째 미칭에 대해서 반영하며, OFF인 경우 전체 무효화를 검사해 가장 강한 표현을 반영한다.
   



.. _caching-purge-async-idbase:

``Id`` 체계와 응답
-----------------------------------

API를 통해 비동기 무효화가 등록되면 고유한 ``Id`` 가 자동 발급된다. ::

   {
     "version": "2.10.3",
     "method": "async/purge",
     "status": "OK",
     "result": { "Count": 0, "Size": 0, "Time": 4, "Id": "20241022114432345", "Merge": "N" }
   }

``Id`` 는 ``YYYY:MM:DD hh:mm:ss.SSS`` 형식으로 발급되며 충돌이 발생할 경우 문자열 끝에 ``_{n}`` 을 순차적으로 추가한다.

``Id`` 를 임의로 지정하여 호출이 가능하다. ::

   # my_sample_id로 Id를 명시적 지정
   /command/async/purge?id=my_sample_id&url=foo.com/*

   # 응답
   {
     "version": "22.2.0",
     "method": "async/purge",
     "status": "OK",
     "result": { "Count": 0, "Size": 0, "Time": 4, "Id": "my_sample_id", "Merge": "N" }
  }


에러 상황시 응답코드로 구분한다.

================================= ==================================================
응답코드                            설명
================================= ==================================================
``400 Bad Request``               쿼리스트링 URL 이 없음
``503 Service Unavailable``       비동기 무효화 삽입 실패
``409 Conflict``                  중복 ID 생성 시도
================================= ==================================================



.. _caching-purge-async-getter:

조회 API
-----------------------------------

비동기 무효화로 관리되는 아이템을 조회한다.

::

    # 전체 비동기 무효화 정보
    http://127.0.0.1:10040/monitoring/asynctrl/info

    # 특정 ID의 비동기 무효화 정보
    http://127.0.0.1:10040/monitoring/asynctrl/info?id=20241022171032554

    # 특정 가상호스트들의 비동기 무효화 정보
    http://127.0.0.1:10040/monitoring/asynctrl/info?vhosts=foo.com,bar.com

    # 특정 URL의 비동기 무효화 정보
    http://127.0.0.1:10040/monitoring/asynctrl/info?url=foo.com/*

    # 특정 type의 비동기 무효화 정보
    http://127.0.0.1:10040/monitoring/asynctrl/info?type=purge


-  ``type`` 쿼리스트링은 가상호스트, URL 쿼리스트링과 함께 사용하여 type 별로 조회할 수 있다.
-  ``vhosts`` 쿼리스트링이 없다면 전체 가상호스트를 조회한다. 콤마로 멀티 가상호스트 입력이 가능하며 해당 가상호스트만 조회한다.


::

   {
      "map": {
        "used": 1424,
        "wait": 1324,
        "max": 100000
      },
      "ids": [
        {
            "id": "202410221646113b",
            "command": "purge",
            "timestamp": "2024-10-22T16:46:11Z",
            "url": "bar.com/*.jpg",
            "cancel": "N",
            "done": "N"
        },
        {
            "id": "2024102216461111",
            "command": "purge",
            "timestamp": "2024-10-22T16:46:11Z",
            "url": "bar.com/*.bmp",
            "cancel": "N",
            "done": "N"
         }
      ]
   }


.. _caching-purge-async-cancelreset:

취소/초기화 API
-----------------------------------

특정 ``Id`` 의 작업을 취소하거나 등록된 전체 API를 초기화할 수 있다. ::

   # 특정 id를 가진 비동기 무효화를 취소한다.
   http://127.0.0.1:10040/command/async/asynctrl/cancel?id=202410221646113b

   # 특정 가상호스트를 가진 비동기 무효화를 모두 취소한다.
   http://127.0.0.1:10040/command/async/asynctrl/cancel?vhost=foo.com

   # 특정 URL를 가진 비동기 무효화를 모두 취소한다.
   http://127.0.0.1:10040/command/async/asynctrl/cancel?url=foo.com/*.jpg

   # 특정 가상호스트를 가진 비동기 무효화중 type에 해당하는 비동기 무효화를 취소한다.
   http://127.0.0.1:10040/command/async/asynctrl/cancel?type=purge&vhost=foo.com

   # 모든 비동기 무효화 정보를 초기화한다.
   http://127.0.0.1:10040/command/async/asynctrl/reset

   # 특정 가상호스트의 prectrl만 초기화한다.
   # 단, 비동기 무효화 항목은 삭제되지 않고 수행된다.
   http://127.0.0.1:10040/command/async/asynctrl/prectrl/reset?vhost=foo.com


``type`` 쿼리스트링은 가상호스트, URL과 함께 사용하여 ``type`` 별로 취소를 진행한다.
