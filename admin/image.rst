.. _media-dims:

17장. 이미지 툴
******************

이 장에서는 이미지를 전송시점에 on-the-fly로 변환/전송하는 이미지 툴(Tool)에 대해 다룬다.
이미지 툴은 DIMS(Dynamic Image Management System)를 포함하여 원본이미지를 다양한 형태로 가공하는 기능이다. 
이미지 가공에 대한 기록은 :ref:`admin-log-image` 에 기록된다.


.. note::

   `실시간 이미지 가공 패턴 <https://csp-kr.readthedocs.io/ko/latest/patterns/pattern_image.html#pattern-image-tool>`_  을 구현한다.
   
   - `[동영상 강좌] 해보자! STON Edge Server - Chapter 4. 실시간 이미지 가공 <https://youtu.be/Pdfe-HbtXVs?list=PLqvIfHb2IlKeZ-Eym_UPsp6hbpeF-a2gE>`_


.. figure:: img/dims.png
   :align: center

   다양한 동적 이미지 가공

이미지는 동적으로 생성되며 원본 이미지 URL뒤에 약속된 키워드와 가공옵션을 붙여서 호출한다.
가공된 이미지는 캐싱되어 원본서버 이미지가 바뀌지 않는 이상 다시 가공되지 않는다.

예를 들어 원본 파일이 /img.jpg라면 다음과 같은 형식으로 이미지를 가공할 수 있다.
("12AB"는 약속된 Keyword이다.) ::

   http://image.example.com/img.jpg    // 원본 이미지
   http://image.example.com/img.jpg/12AB/optimize
   http://image.example.com/img.jpg/12AB/resize/500x500/
   http://image.example.com/img.jpg/12AB/crop/400x400/
   http://image.example.com/img.jpg/12AB/composite/watermark1/

``<Dims>`` 는 별도로 설정하지 않으면 모두 비활성화되어 있다. ::

   # server.xml - <Server><VHostDefault><Options>
   # vhosts.xml - <Vhosts><Vhost><Options>

   <Dims Status="Active" Keyword="dims" MaxSourceSize="10" MinSourceSize="0" />

-  ``<Dims>``

   - ``Status`` DIMS활성화 ( ``Active`` 또는 ``Inactive`` )
   - ``Keyword`` 원본과 DIMS를 구분하는 키워드
   - ``MaxSourceSize (기본: 10MB)`` 변환을 허용할 최대 원본 이미지 크기 (단위: MB)
   - ``MinSourceSize (기본: 0KB)`` 변환을 허용할 최소 원본 이미지 크기 (단위: KB)
 

.. note::

   변환 과정 중 오류가 발생할 경우 원본 이미지를 전송한다.



.. toctree::
   :maxdepth: 2




리사이즈
====================================

이미지 크기를 변경한다.
크기는 **width x height** 로 표현한다.
이미지는 변경되어도 비율은 유지된다.
다음은 원본 이미지를 width=200, height=200크기로 변경하는 예제다. ::

   http://image.example.com/img.jpg/dims/resize/200x200/

그 외 명령어는 다음과 같다.

-  **resizec** - 축소하면 resize와 동일하지만, 확대하면 이미지는 유지되고 캔버스 크기만 확대된다.
-  **extent** - 캔버스만 조절하는 명령어. 축소하면 crop과 동일한 효과를 내지만, 확대하면 resizec와 동일하게 확대된다.
-  **trim** - 상하좌우 흰색배경을 제거한다.





잘라내기
====================================

좌상단을 기준으로 원하는 영역만큼 이미지를 잘라낸다.
영역은 **width x height{+-}x{+-}y{%}** 로 표현한다.
다음은 좌상단 x=20, y=30을 기준으로 width=100, height=200만큼 잘라내는 예제다. ::

   http://image.example.com/img.jpg/dims/crop/100x200+20+30/


이미지 중앙을 기준으로 하고 싶은 경우 cropcenter명령어를 사용한다. ::

   http://image.example.com/img.jpg/dims/cropcenter/100x200+20+30/




Format 변경
====================================

이미지 포맷을 변경한다.
``png`` , ``jpg`` , ``gif`` 를 지원한다.

.. note::

   ``Enterprise`` v18.06.0 부터 WebP를 지원한다.


다음은 JPG를 PNG로 변환하는 예제다. ::

   http://image.example.com/img.jpg/dims/format/png/


.. note::

   ``Enterprise`` 변경된 Format의 기본 Quality를 설정할 수 있다. ::

      # server.xml - <Server><VHostDefault><Options>
      # vhosts.xml - <Vhosts><Vhost><Options>

      <Dims>
         <FormatQuality>100</FormatQuality>
      </Dims>

   
   -  ``FormatQuality (기본: 100)`` 변경된 Format의 기본 Quality (1~100).




이펙트
====================================

이미지에 다양한 이펙트를 줄 수 있다.

================ ===================== =================
설명              명령어                  변수
================ ===================== =================
반전               invert                true 또는 false
그레이 스케일        grayscale            true 또는 false
대칭이동            flipflop             vertical 또는 horizontal
밝기조절            bright                0 ~ 100
회전               rotate                0 ~ 360 (도)
세피아              sepia                 0 ~ 1
모서리 라운드        round                 0 ~ 90
================ ===================== =================



합성
====================================

두 이미지를 합성한다.
앞서 설명한 기능과는 다르게 합성조건은 미리 설정되어 있어야 한다.
주로 워터마크 효과를 내기 위해 사용된다. ::

   # server.xml - <Server><VHostDefault><Options>
   # vhosts.xml - <Vhosts><Vhost><Options>

   <Dims Status="Active" Keyword="dims">
      <Composite Name="water1" File="/img/small.jpg" />
      <Composite Name="water2" File="/img/medium.jpg" Gravity="se" Geometry="+0+0" Dissolve="50" />
      <Composite Name="water_ratio" File="/img/wmark_s.png" Gravity="s" Geometry="+0+15%" Dissolve="100" />
   </Dims>

-  ``<Composite>``

    이미지 합성조건을 설정한다. 속성에 의해 정해지며 별도의 값을 가지지 않는다.

    -  ``Name`` 호출될 이름을 지정한다.
       '/'문자는 입력할 수 없다.
       URL의 "/composite/" 뒤에 위치한다.

    -  ``File`` 합성할 이미지파일 경로를 지정한다.

    -  ``Gravity (기본: c)`` 합성할 위치는 좌측상단부터 9가지의 포인트(nw, n, ne, w, c, e, sw, s, se)가 존재한다.

       .. figure:: img/conf_dims2.png
          :align: center

          Gavity 기준점

    -  ``Geometry (기본: +0+0)`` ``Gravity`` 기준으로 합성할 이미지 위치를 설정한다.
       {+-}x{+-}y. 붉은색 원은 Gravity속성에 따라 +0+0이 의미하는 기준점으로 +x+y의
       값이 커질수록 이미지 안쪽으로 배치된다.
       초록색 화살표는 +x, 보라색 화살표는 +y가 증가하는 방향이다.
       -x-y를 사용하면 대상 이미지의 바깥에 위치하게 되어 결과 이미지에서는 보여지지 않는다.
       이 속성은 다소 복잡해 보이지만 이미지 크기를 자동으로 계산하여 배치하므로
       일관된 결과물을 얻을 수 있어서 효과적이다.
       또한 +x%+y% 처럼 %옵션을 주어 비율로 배치할 수도 있다.

    -  ``Dissolve (기본: 50)`` 합성할 이미지의 투명도(0~100).

``<Composite>`` 을 설정했다면 ``Name`` 속성을 사용하여 이미지를 합성할 수 있다. ::

    http://image.example.com/img.jpg/dims/composite/water1/




고급 기능
====================================

더욱 다양한 이미지 서비스 패턴은 ``M2`` 파이프라인 플랫폼에서 구현된다.

-  Contents Service Patterns - `이미지 서비스 패턴 <https://csp-kr.readthedocs.io/ko/latest/patterns/pattern_image.html>`_
-  ``M2`` 파이프라인 플랫폼 - `이미지 엔진 <https://m2-kr.readthedocs.io/ko/latest/guide/imagetool.html>`_ 
