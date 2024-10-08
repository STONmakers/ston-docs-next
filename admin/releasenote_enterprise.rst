.. _release_enterprise:

Appendix F: 릴리스 노트  ``[Enterprise]``
********************************************

.. note::

   ``deprecated`` 2021년부터 `M2 <https://doc.m2live.co.kr>`_ 로 통합됨을 알려 드립니다.



v24.x
====================================

.. _release-enterprise-24-08-21:

24.08.1 (2024.08.21)
----------------------------

-  ( ``v24.08.0`` 버그) 멀티 ``RSA`` 인증서 등록시 인증서가 정상선택되지 않던 증상 수정


.. _release-enterprise-24-07-29:

24.08.0 (2024.07.29)
----------------------------

-  :ref:`origin-balancemode` ``Hash`` 맵 구성 성능 개선
-  :ref:`media-hls` 비정상 MP4 예외처리 강화
-  :ref:`media-mp3-hls` – 낮은 확률의 메모리누수 문제 수정
-  ``DSA`` , ``RSA`` 하이브리드 인증서 지원


.. _release-enterprise-24-03-18:

24.03.1 (2024.03.18)
----------------------------

-  원본과 클라이언트의 HTTP 응답코드별 개수 통계를 제공한다. ( :ref:`monitoring_stats_conf` 설정)
-  HTTP 비정상 ``Range`` 요청에 처리 정책 변경

   | **Before**. 세션 종료
   | **After**. ``Range`` 헤더 무시


.. _release-enterprise-24-03-14:

24.03.0 (2024.03.14)
----------------------------

-  :ref:`media-hls` - :ref:`media-mp4-hls-enc` 기능 사용시 미디어가 간헐적으로 튀는 증상 개선


.. _release-enterprise-24-03-05:

24.02.0 (2024.03.05)
----------------------------

-  :ref:`media-hls` 변환시 모노 오디오가 스테레오로 한쪽만 재생되던 증상 수정
-  ``Amazon Linux 2023`` , ``Amazon Linux 2`` 지원 ( :ref:`getting-started-os` )


.. _release-enterprise-24-01-0:

24.01.0 (2024.02.05)
----------------------------

-  ``Ubuntu v22.04`` 지원 ( :ref:`getting-started-os` )
-  :ref:`https-conf` - 잘못된 인증서가 설정되더라도 해당 인증서만 제외하고 정상 인증서를 로딩
-  :ref:`env-vhost-defaultvhost` 선택시 서비스 포트를 검사하지 않도록 개선
-  ImageTool(DIMS), 압축등 콘텐츠 가공 과정 중 발생한 원본요청에 대해 ``X-Forwarded-For`` 헤더를 전달하도록 개선
-  원본서버가 ``Content-Type`` 헤더를 응답하지 않을 때 ``Content-Type`` 헤더는 빈 값으로 명시하던 증상 개선
-  가상 호스트가 삭제될 때 Alias를 반납하여 다른 가상호스트로 양도하도록 개선


v23.x
====================================

.. _release-enterprise-23-12-0:

23.12.0 (2023.12.22)
----------------------------

.. warning::

   Cent OS 6 지원 종료
   

-  `HTTP/2 Rapid Reset <https://blog.cloudflare.com/ko-kr/technical-breakdown-http2-rapid-reset-ddos-attack-ko-kr/>`_ 패치
-  :ref:`https-conf` 과 :ref:`handling_http_requests_http2` 설정이 통합되었으며, :ref:`handling_http_requests_http2` 설정은 :ref:`https-conf` 보다 우선한다.
   
   .. note::
      
      :ref:`handling_http_requests_http2` 활성화시 :ref:`https-conf` 의 개별 설정은 무시된다.


.. _release-enterprise-23-03-0:

23.03.0 (2023.03.03)
----------------------------

-  CDN 에디션 추가기능 통합
-  DIMS 안정성 강화, 성능개선



v22.x
====================================


.. _release-enterprise-22-08-0:

22.08.0 (2022.09.01)
----------------------------

-  Access.log의 ``sc-bytes`` 정밀도 개선
-  `CVE-2022-2274 <https://nvd.nist.gov/vuln/detail/CVE-2022-2274>`_ 취약점 대응
-  `CVE-2022-2097 <https://nvd.nist.gov/vuln/detail/CVE-2022-2097>`_ 취약점 대응



.. _release-enterprise-22-07-0:

22.07.0 (2022.07.14)
----------------------------

-  ``RHEL/CentOS Stream 8`` 지원
-  ``RHEL/CentOS Stream 9`` 지원
-  ``Ubuntu 20.04`` 지원
-  ``Rocky Linux 8`` 지원 ( ``RHEL/CentOS`` 패키지 사용)



.. _release-enterprise-22-06-1:

22.06.1 (2022.06.28)
----------------------------

**버그수정**

-  HTTP/2가 활성화 되어 있는 경우 원본이 ``204 No Content`` 을 하는 경우 낮은 확률로 ``502 Bad Gateway`` 를 응답 하는 문제 수정 


.. _release-enterprise-22-06-0:

22.06.0 (2022.06.16)
----------------------------

-  :ref:`handling_http_requests_header_contentfreshness` 설정 기능

-  캐싱관리 - Root Purge/HardPurge를 허용하지 않는 경우 Purge API 응답 코드 설정 기능

-  :ref:`admin-log-origin` - 원본 요청시간 필드 ``time-request`` 추가


**버그수정**

-  HTTP/2가 활성화 되어 있는 경우 ``X-Forwarded-For`` 헤더의 값에 ``127.0.0.1`` 이 추가 되는 버그 수정



.. _release-enterprise-22-04-0:

22.04.0 (2022.04.12)
----------------------------

**기능개선/정책변경**

-  `CVECVE-2022-0778 <https://nvd.nist.gov/vuln/detail/CVE-2022-0778>`_ 취약점 대응



.. _release-enterprise-22-02-0:

22.02.0 (2022.03.15)
----------------------------


**버그수정**

-  바이패스 - POST 요청이 바이패스 되는 경우 간헐적으로 트랜잭션이 완료 되지 않는 문제 수정
-  ImageTool - ``PreoptimizeJpeg`` 기능 사용 시 이미지 색상이 반전 되는 문제 수정
-  인스턴트 모드 사용시 간헐적으로 500 Error가 응답 되는 문제 수정


.. _release-enterprise-22-01-0:

22.01.0 (2022.01.19)
----------------------------


**버그수정**

-  캐싱관리 - 비동기 무효화 API에서 잘못 된 응답 코드가 리턴 되는 문제 수정



v21.x
====================================


.. _release-enterprise-21-12-1:

21.12.1 (2022.01.12)
----------------------------

**기능개선/정책변경**

-  캐싱 - :ref:`caching-policy-base` 설정 기능
-  캐싱 - 원본 ``304 Not Modified`` 응답 코드 TTL 별도 설정 기능
-  캐싱관리 - :ref:`caching-purge-async` 기능추가
-  이미지툴 - cropc 명령어 추가
-  WM - httpd 보안 취약점 개선을 위한 버전 업데이트 ``v2.4.41`` → ``v2.4.51``


**버그수정**

-  설정 변경 시 서비스 응답이 지연 될 수 있는 문제 수정
-  낮은 확률로 ``500 Internal Error`` 가 응답 될 수 있는 문제 수정
-  MP4HLS - 캐싱 되지 않은 ts 파일을 요청 할 경우 ``415 Unsupported Media Type`` 에러가 응답되는 문제 수정




21.12.0 (2021.12.03)
----------------------------

**버그수정**

-  ByClient 기능이 활성화된 상태에서 M2core가 요청을 재정의할 경우 원본요청이 오동작하던 증상 수정



21.10.0 (2021.11.04)
----------------------------

**기능개선/정책변경**

-  ImageTool(DIMS) - ``Strip`` 수행시 ``Exif profile`` 유지 하도록 정책 변경


**버그수정**

-  간헐적으로 500 에러가 응답 되는 문제 수정
-  캐싱된 콘텐츠 메모리 정리 중 낮은 확률로 비정상 종료 되는 문제 수정




21.09.0 (2021.09.09)
----------------------------

**버그수정**

-   원본 S3인증 사용시 요청 URL에 “~” 있는 경우 인증을 실패 하는 버그 수정



21.07.0 (2021.07.13)
----------------------------

**버그수정**

-   [v21.04.1 ~ v21.06.1] POST캐싱 기능 사용시 원본 요청이 GET으로 바뀌는 문제 수정



21.06.1 (2021.06.22)
----------------------------

**기능개선/정책변경**

-  :ref:`caching-policy-nocacherequestexpire` 기능 사용시 이미지툴 원본 파일도 Expire 되도록 정책 변경



21.05.1 (2021.05.31)
----------------------------

**기능개선/정책변경**

-  :ref:`env-cache-storage` - Disk Quota를 비율로 설정하는 기능 추가


**버그수정**

-  4GB 넘는 구간을 :ref:`media-trimming` 할 경우 재생오류 수정


21.05.0 (2021.05.24)
----------------------------

**버그수정**

-  바이패스  - 원본 HTTPS 통신 시에 간헐적으로 비정상 종료 되는 문제
-  WM – 클러스터 적용을 통한 설정 배포 시 설정이 누락 되는 문제 수정



21.04.1 (2021.04.22)
----------------------------

**기능개선/정책변경**

-  원본 :ref:`origin-busysessioncount` 기능 비활성화
-  WM에서 가상호스트 생성시 불필요한 설정 정리




21.04.0 (2021.04.07)
----------------------------

**기능개선/정책변경**

-  `CVE-2021-3449 <https://www.openssl.org/news/secadv/20210325.txt>`_ 취약점 대응
-  `CVE-2021-3450 <https://www.openssl.org/news/secadv/20210325.txt>`_ 취약점 대응




21.03.2 (2021.3.31)
----------------------------

**기능개선/정책변경**

-  ImageTools – 이미지 :ref:`media-dims-resize-stretch-out` 기능 추가
-  WM을 통한 M2 로그 다운로드 기능


**버그수정**

-  HTTP/2가 활성화 되어 있는 경우 요청 URL의 ``//`` 가 ``/`` 로 변환 되는 문제
-  WM에서 CustomTTL에서 OnTime 설정을 하지 않는 경우 TTL이 반영 되지 않는 문제



21.03.1 (2021.3.11)
----------------------------

**기능개선/정책변경**

-  미디어 – 비정상 적으로 인코딩 된 MP4 파일 호환성 강화


21.03.0 (2021.3.4)
----------------------------

**기능개선/정책변경**

-  가상호스트 :ref:`adv_topics_instant` 지원
-  HTTP/2에서 IPv6를 사용하지 않도록 수정 


**버그수정**

-  가상호스트 추가 시 간헐적으로 SNMP 통계가 보이지 않는 문제 수정



21.01.0 (2021.2.1)
----------------------------

**버그수정**

-  원본 HTTPS 통신 시 낮은 확률로 비정상 종료 되는 문제 수정



v20.x
====================================

20.12.0 (2021.1.28)
----------------------------

**기능개선/정책변경**

-  SSL Library(OpenSSL) 버전 업데이트
-  :ref:`caching-policy-customttl-cron` 기능 추가
-  :ref:`admin-log-origin` 에 ``time-sock-creation`` , ``x-cs-retry`` 필드 추가
-  :ref:`handling_http_requests_modify_client` , :ref:`origin_modify_client` - ``#HOSTNAME``  예약어 추가
-  :ref:`handling_http_requests_cache_control_expires` - 남은 TTL 정보를 알려주는 ``#TTL_LEFT`` 예약어 추가
-  [WM] 가상호스트 삭제 시 가상호스트 이름 표시
 

**버그수정**

-  :ref:`adv-vhost-redirection-trace` 과 :ref:`origin_modify_client` 을 함께 사용 할 경우 비정상 종료 되는 문제 수정



20.11.0 (2020.11.24)
----------------------------

**기능개선/정책변경**

-  Fatal 로그 기록 방식 개선
-  :ref:`monitoring-stats-vhost` , :ref:`monitoring-stats-host` - 시간 정밀도 개선
 

**버그수정**

-  :ref:`admin-log-access-custom` - ``%H`` 예약어가 동작하지 않는 문제 수정



20.10.0 (2020.10.22)
----------------------------

**기능개선/정책변경**

-  :ref:`adv-vhost-url-rewrite` – :ref:`adv-vhost-url-rewrite-protocol` 추가
-  ImageTools – 변환을 위한 원본 최소 크기 제한 기능

 
**버그수정**

-  MP4 :ref:`media-trimming` 기능 사용 시 비정상 종료 되는 문제 수정 ``v20.08.0 ~ v20.09.0``
-  ``ByClient`` 기능 사용시 Purge API가 수행 되지 않는 문제
-  바이패스 동작 중 비정상 종료 되는 문제



20.09.0 (2020.10.12)
----------------------------

**기능개선/정책변경**

- ImageTools – :ref:`media-dims-anigif` :ref:`media-dims-anigif-exceptiongif` 기능 추가
- :ref:`media-hls` 변경 - 호환되지 않는 파일에 대한 응답코드를 ``415 Unsupported Media Type`` 으로 수정 (기존 ``404 Not Found`` )

 
**버그수정**

- HardPurge 수행 중 낮은 확률로 비정상 종료 되는 문제 수정
- 바이패스 – 낮은 확률로 클라이언트에게 응답을 전송하는 중에 비정상 종료 되는 문제 수정



20.08.0 (2020.9.4)
----------------------------

**기능개선/정책변경**

- [원본] :ref:`adv-vhost-redirection-trace` - ``<URL>`` 조건 추가
- [원본] :ref:`origin-cache-control` 변경
- [미디어] MP4 Trimming 호환성 및 안정성 강화

 
**버그수정**

- [클라이언트] CentOS 7에서 낮은 확률로 응답이 누락 될 수 있는 문제 수정
- [바이패스] 낮은 확률로 비정상 종료 되는 문제 수정
- [ :ref:`adv-vhost-link` ] 링크가 2번 동작 할 수 있는 문제 수정
- [WM] 삭제 된 가상호스트가 가상호스트 목록에 남아 있는 문제 수정



20.07.2 (2020.7.23)
----------------------------
**기능개선/정책변경**

- :ref:`handling_http_requests_modify_client` - ``#SESSIONID`` 예약어 추가


**버그수정**

- MPxHLS – PCR 계산식 호환성 강화
- HTTPS 절대 경로로 요청이 올 경우 낮은 확률로 비정상 종료 되는 문제 수정


20.07.1 (2020.7.16)
----------------------------

**버그수정**

- 파일을 삭제 하는 중에 낮은 확률로 종료 되는 문제 수정 (보완)



20.07.0 (2020.7.13)
----------------------------

**기능개선/정책변경**

 - HardPurge를 이용한 전체 콘텐츠 삭제 금지기능 ``<RootHardPurge>`` 추가 
 - :ref:`access-control-vhost` - HTTP 요청의 Host헤더를 참조하는 ``#HOST`` 예약어 추가
 - 대량의 가상호스트 설정변경 성능 개선
 - 원본서버 – 최소 DNS TTL 설정 기능 추가
 

**버그수정**

- 파일을 삭제 하는 중에 낮은 확률로 종료 되는 문제 수정
- :ref:`caching-policy-vary-header` 사용시 HTTPS요청에 대해 가상호스트를 찾지 못하는 문제 수정


20.06.0 (2020.6.10)
----------------------------

-  :ref:`adv_topics_volatile` 기능 추가
-  원본서버 :ref:`origin-balancemode-url-suffix-ignore` 기능 추가


**버그수정**

-  HTTPS - SSLv3.0 이 활성화 되지 않는 문제 수정(19.12.0 ~ 20.05.0)
-  HTTPS - SNI가 활성화 되어 있는 경우 인증서가 잘못 선택 되는 문제 수정

   .. note::
   
      *.winesoft.co.kr, *.image.winesoft.co.kr과 같이 동일한 도메인에 대해서 각각 발급 받은 인증서를 함께 설정할 경우에만 문제가 발생합니다.



20.05.0 (2020.5.7)
----------------------------

**버그수정**

 - [v20.02.0 ~ v20.04.0] ImageTool – WebP 이미지 변환 관련 기능이 동작하지 않는 문제 수정



20.04.0 (2020.4.21)
----------------------------

**기능개선/정책변경**

 - :ref:`admin-log-originerror` - 원본서버 Port 필드 ``s-port`` 추가
 - 원본서버가 ``If-Range`` 에 대한 응답으로 200 OK를 줄 경우 파일을 갱신 하도록 정책 변경
 - :ref:`handling_http_requests_header_if_range` -  클라이언트가 보낸 If-Range의 값이 더 최신이라면 캐싱 컨텐츠를 Purge 하는 속성 추가

**버그수정**

 - :ref:`media-mp4-upfront-header` - 일부 파일의 CPU 과점유 현상 개선


20.03.0 (2020.3.12)
----------------------------

:ref:`handling_http_requests_custom_error_page` 기능 추가



20.02.0 (2020.2.18)
----------------------------

**기능개선/정책변경**

 - 바이패스/ :ref:`bypass-affinity-sticky` - Sticky 속성 추가


**버그수정**

 - HTTPS - [19.10.1 ~ 20.01.0] SSL 전송이 미완료 되는 문제 수정


20.01.0 (2020.01.20)
----------------------------

**기능개선/정책변경**

 - ImageTool - TIFF포맷 변환기능 추가

**버그수정**

 - :ref:`handling_http_requests_http2` - HEAD 요청이 처리 되지 않는 문제 수정
 - :ref:`handling_http_requests_http2` - 인증서 파일이 백업되지 않는 문제 수정
 - 원본 S3 인증이 실패 하는 문제 수정


v19.x
====================================


19.12.0 (2019.12.27)
----------------------------

- :ref:`handling_http_requests_http2` 지원

**기능개선/정책변경**

 - :ref:`media-mp3-hls` – TS 변환 시 PCR을 추가 하는 기능

   .. note::

      PCR 추가 기능이 활성화되면 이전에 생성된(PCR 필드가 없는) TS파일과 호환이 되지 않습니다.



19.11.0 (2019.11.28)
----------------------------

**기능개선/정책변경**

 - ImageTool – 비정상 변환 파라미터 안정성 강화
 - 헤더변조 – 요청 PORT를 추가 할 수 있는 ``#PORT`` 예약어 추가

**버그수정**

 - WM – 설정 된 HTTPS 인증서가 50개 이상인 경우 클러스터 적용이 오동작 하는 문제 수정
 - RRD 통계 프로세스가 비정상 종료 되는 문제 수정



19.10.1 (2019.10.29)
----------------------------

**기능개선/정책변경**

 -  LTE 환경에서 대용량 파일 전송 최적화



19.10.0 (2019.10.10)
----------------------------

**버그수정**

 - HTTPS – POST Bypass 요청이 간헐적으로 처리 되지 않는 문제 수정
 - 원본 서버가 1초 안에 모두 배제/복구 될 경우 비정상 종료 될 수 있는 문제 수정



19.09.0 (2019.9.26)
----------------------------

**기능개선/정책변경**

 - 원본서버 - :ref:`origin_aws_s3_authentication` 지원
 - WM - Apache 업데이트 (v2.4.41)
 


19.08.0 (2019.8.14)
----------------------------

**기능개선/정책변경**

 - HTTPS - ECDSA Key 파일 호환성 강화
 - 1분 평균 통계 API 지원

**버그수정**

 -  WM - GeoIP 데이터베이스 파일이 업로드 되지 않는 문제
 -  WM - CustomTTL을 편집 할 수 없는 문제
 -  HTTPS - DSA 인증서에서 RSA인증서로 교체 할 경우 비정상 종료 되는 문제



19.07.0 (2019.7.4)
----------------------------

**기능개선/정책변경**

 - :ref:`adv_topics_rrd_inactive` - 기능 추가
 - :ref:`caching-policy-customttl` – 원본 응답 조건 추가
 - :ref:`origin_exclusion_and_recovery` - 원본 서버를 배제 하지 않는 기능 추가
 - ImageTool(DIMS) - :ref:`media-dims-autorotate` 기능 추가 


**버그수정**

 -  WM – 시스템 설정 중 디스크 설정이 초기화 될 수 있는 문제 수정
 -  Hardware Info API를 호출 할 경우 CPU 사용량이 증가하는 문제 수정



19.06.0 (2019.6.4)
----------------------------

**버그수정**

 -  ImageTool(DIMS) - Byoriginal의 Orientation 설정이 중복해서 들어가는 문제 수정
 -  WM - 가상호스트 복제 기능을 이용 할 경우 ByOriginal 설정이 복제 되지 않고 설정 할 수 없는 문제 수정



19.05.0 (2019.5.9)
----------------------------

**기능개선/정책변경**

 - ImageTool(DIMS) - 원본이미지 조건판단 기능 개선

**버그수정**

 - GeoIP2를 사용 할 경우 낮은 확률로 비정상 종료 될 수 있는 문제 수정

   .. note::

      GeoIP2는 Database 파일을 덮어쓰기로 업데이트 하는 것을 지원하지 않습니다.



19.04.1 (2019.4.12)
----------------------------

**버그수정**

 -  HTTPS – ``[v2.6.9 ~ v2.6.10]`` SNI 기능이 활성화 되어 있는 경우 낮은 확률로 일부 클라이언트가 보낸 ServerName 을 찾지 못하고 Alert를 응답하는 문제 수정
 
    .. note::

       SNI 기능을 사용하지 않으시면 문제가 발생하지 않습니다.



19.04.0 (2019.4.11)
----------------------------

**기능개선/정책변경**

 - :ref:`adv_topics_storage_cleanupsize` 추가
 - :ref:`adv_topics_perf_cleanupfilecount` 추가
 - 설정 리로드 API 응답 개선
 - HTTPS – 인증서 설정이 잘못된 경우 관련 로그 보강

**버그수정**

 -  WM - 영문 페이지에서 시스템 설정을 할 수 없는 문제 수정
 -  WM - 영문 페이지에서 메모리 값이 음수로 표현되는 문제 수정
 -  WM - 디스크 설정화면이 깨지는 문제 수정
 -  HTTPS - 인증서 키 파일 설정에 지원하지 않는 키 파일을 설정할 경우 비정상 종료 되는 문제 수정



19.03.0 (2019.3.13)
----------------------------

**기능개선/정책변경**

 - HTTPS - TLS v1.3 지원

**버그수정**

 -  WM - 헤더 변조 기능에 빈 값을 넣을 수 없는 문제
 -  HTTPS - SNI 기능 사용시 인증서마다 프로토콜 설정을 할 수 없는 문제



19.02.0 (2019.2.11)
----------------------------

**기능개선/정책변경**

 - ImageTool(DIMS) - Format 변환 시 기본 Quality 설정 기능
 - ImageTool(DIMS) - 최대 Quality 설정 기능
 - :ref:`admin-log-image` 추가
 - :ref:`handling_http_requests_modify_client` - 클라이언트 요청 헤더의 값을 원본 요청 헤더에 추가하는 기능

**버그수정**

 -  원본 서버를 50개 이상 설정 했을 경우 낮은 확률로 비정상 종료 되는 문제
 -  WM - HTTPS 인증서 클러스터 적용 시 SNI 설정이 초기화 되는 문제



19.01.0 (2019.1.16)
----------------------------

**기능개선/정책변경**

- GeoIP2 지원

**버그수정**

 - ImageTool(Dims) - webp로 포맷을 변경할 경우 화질이 변경되는 문제 수정



v18.x
====================================

18.12.1 (2018.12.19)
----------------------------

**기능개선/정책변경**

- Access 로그 롤링 파일명을 초 단위까지 명시하도록 변경. 기존 버전과의 호환성을 위해서 로그 타입을 TIME을 설정 했을 경우에는 기존 파일명 정책을 유지합니다.



18.12.0 (2018.12.12)
----------------------------

**기능개선/정책변경**

- ImageTool(Dims) - 이미지 Color Profile 정책 변경


18.11.0 (2018.11.15)
----------------------------

**기능개선/정책변경**

- 디스크 인덱싱 기능 제거


**버그수정**

 -  설정 값 Reload API가 동시에 요청 될 경우 비정상 종료 되는 문제
 -  메모리 모드에서 파일 분포 통계가 맞지 않는 문제
 -  HTTPS – 낮은 확률로 비정상 종료 되는 문제


18.10.0 (2018.10.15)
----------------------------

**버그수정**

 -  [18.09.0 ~ 18.09.3] URL 바이패스 기능 동작 시 낮은 확률로 비정상 종료 되는 문제 수정



18.09.3 (2018.9.18)
----------------------------

**버그수정**

 - HTTPS – Multi NIC로 인증서를 설정 할 경우 *:443 설정과 STATIC-IP:443 설정이 혼합되어 있으면 인증서를 찾지 못하는 문제



18.09.2 (2018.9.12)
----------------------------

**버그수정**

 - 간헐적으로 HTTPS 세션이 끊어지는 문제 수정



18.09.1 (2018.9.7)
----------------------------

**버그수정**

 - 일부 시스템 환경에서 전송 완료 시간이 늘어나는 증상


18.09.0 (2018.9.3)
----------------------------

- :ref:`env-vhost-activeorigin` HTTPS 통신 지원

**기능개선/정책변경**

- HTTPS - 성능개선 및 ECDSA 인증서 지원
- :ref:`handling_http_requests_cache_control_expires` – 원본 Max-Age 값을 사용하는 기능 추가


18.08.0 (2018.8.8)
----------------------------

**기능개선/정책변경**

- :ref:`handling_http_requests_modify_client` - 요청 헤더의 값을 응답 헤더에 추가한다.
- :ref:`media-dims` - 이미지 포맷이 변경되면 해당 포맷의 Content-Type으로 응답하도록 정책 수정


18.07.0 (2018.7.10)
----------------------------

**기능개선/정책변경**

- :ref:`media-dims` - WebP 포맷 지원
- 바이패스 응답에도 :ref:`handling_http_requests_basic_via` 추가하도록 정책변경


**버그수정**

 - :ref:`media-dims` - :ref:`media-dims-byoriginal` 에서 :ref:`media-dims-optimize` 가 동작하지 않던 증상
 - WM - 클러스터 복제시 설정이 누락되던 증상
 - Indexing과 파일 삭제가 동시에 동작할 경우 낮은 확률도 비정상 종료되던 증상



18.05.1 (2018.5.29)
----------------------------

**기능개선/정책변경**

- :ref:`media-hls` - 키프레임의 간격이 불규칙한 영상에 대한 호환성 강화

.. warning::

   이전 버전과 :ref:`media-hls` 의 MPEG2-TS가 호환되지 않습니다.


**버그수정**

 -  :ref:`handling_http_requests_header_lastmodifiedcheck` - ``orlater`` 로 설정 할 경우 최초 캐싱 시 304 응답을 할 수 있는 문제 수정


18.05.0 (2018.5.15)
----------------------------

-  클라이언트 요청 :ref:`handling_http_requests_header_if_range` 헤더 지원 
-  원본 요청 시 :ref:`origin_header_if_range` 헤더 지원
-  :ref:`handling_http_requests_header_lastmodifiedcheck` 설정기능 추가
-  :ref:`bypass-put` 기능 추가



18.04.0 (2018.4.26)
----------------------------

**기능개선/정책변경**

- :ref:`media-dims` - :ref:`media-dims-annotation` 기능 추가


.. note::

   v2.5.13 이후부터 새로운 Versioning으로 제공됩니다.

   -  ``CDN`` - v2.5.14와 같은 기존 Versioning
   -  ``Enterprise`` - v.18.04.0과 같은 연도.월 형태의 새로운 Versioning
