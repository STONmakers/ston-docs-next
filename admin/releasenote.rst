.. _release:

Appendix E: 릴리스 노트
***********************

v2.12.x
====================================

.. _release-cdn-2-12-1:

2.12.1 (2025.07.17)
----------------------------

-  :ref:`adv_topics_maxsockets` - ``<MaxSockets>`` 설정 임계치 변경 (기존 10만 -> 20만)
-  :ref:`admin-log-access` - ``x-sc-ssl-cipher`` 필드 추가
-  :ref:`https-conf` - 중복된 인증서 로딩시 예외 처리 및 로그 강화
-  :ref:`caching-purge-async` - ``PreCacheControl`` 에 의해서 Purege가 되지 않는 문제 개선
-  ``HTTP/2`` 다수 인증서(20개) 로딩 문제 개선
-  WM - Apache HTTP Server 버전 업데이트(v2.4.64) 및 보안 패치

.. _release-cdn-2-12-0:

2.12.0 (2025.06.24)
----------------------------

-  ``HTTP/3`` 지원
-  :ref:`https-ocsp-stapling` 기능 추가
-  `HTTP/2 continuation flood <https://nowotarski.info/http2-continuation-flood/>`_ 취약점 대응
-  ``/monitoring/realtime`` , ``/monitoring/average`` 가상호스트 통계분리 지원


v2.11.x
====================================

.. _release-cdn-2-11-6:

2.11.6 (2025.06.10)
----------------------------

-  캐싱 디스크가 배제될 경우 낮은 확률로 비정상 종료되는 문제수정 및 로그보강
-  WM - ``HTTP/2`` 의 ``TLS Ciphers`` 가 설정 값이 반영 되지 않는 문제 수정
-  :ref:`media-trimming` - ``M4A`` 포맷 음원파일에 대한 Trimming 예외처리 강화
-  ``AES-NI`` 가속 기능 안내 문구 삭제


.. _release-cdn-2-11-5:

2.11.5 (2025.05.08)
----------------------------

-  메모리관리자 동작개선

   | **Before**. 메모리 사용량의 일괄 10%를 정리
   | **After**. :ref:`adv_topics_mem_secure` 추가 (관련로그 개선)

-  :ref:`caching-policy-vary-header` 설정이 활성화된 경우 ``TCP_MISS`` 상황에서 요청카운트가 2번 집계되던 증상 수정
-  고용량 메모리 환경에서 :ref:`api-conf-reload` 수행시간이 증가하던 증상 수정
-  일부 환경에서 디스크 정리가 되지 않던 증상 수정 (관련로그 개선)


.. _release-cdn-2-11-4:

2.11.4 (2025.03.26)
----------------------------

-  :ref:`api-conf-vhostapi` 추가
-  :ref:`로그 통합기록<admin-log>` 기능 추가
-  :ref:`handling_http_requests_compression` - 클라이언트의 ``Accept-Encoding`` 헤더와 원본의 ``Content-Encoding`` 헤더가 호환성되지 않을 경우 예외처리 강화
-  하이브리드 인증서( ``ECDSA / RSA`` ) 지원 개선
-  DNS 리졸빙 실패시 예외처리 강화



.. _release-cdn-2-11-3:

2.11.3 (2025.03.06)
----------------------------

-  ``STONU`` 업데이트 명령어 OS 호환성 개선


.. _release-cdn-2-11-2:

2.11.2 (2025.02.25)
----------------------------

-  :ref:`origin-health-checker` - :ref:`origin-health-checker-validation` , :ref:`origin-health-checker-header` 기능 추가
-  :ref:`admin-log-access-custom` - 특정 응답헤더 기록설정 ``%l`` , ``%o`` 추가 
-  :ref:`env-vhost-standbyorigin` - 원본서버 완전 정상화상태에서 일부 보조주소가 사용되던 증상 개선
-  :ref:`handling_http_requests_compression` - 원본 서버가 비압축 콘텐츠 요청에 대해 ``Content-Encoding`` 헤더를 명시했을 때 압축하던 증상 수정. 원본의 응답을 그대로 전송하도록 개선.
-  클러스터 Purge 요청시 ``&`` 문자열 이후는 전달 되지 않는 문제 수정




.. _release-cdn-2-11-1:

2.11.1 (2025.01.07)
----------------------------

-  여러 가상호스트가 동일한 도메인을 리졸빙할 때 중복호출 제거
-  :ref:`admin-log-access-custom` - 제품버전을 기록하는 ``%v`` 필드 추가
-  :ref:`caching-policy-custom-cachingkey` - 헤더의 지시자를 정교하게 인식하도록 개선


.. _release-cdn-2-11-0:

2.11.0 (2024.12.16)
----------------------------

-  Ubuntu 24.04 지원
-  :ref:`handling_http_requests_modify_client` , :ref:`origin_modify_client` - ``#CLIENTIP`` 예약어 추가
-  SNMPWalk가 종료되지않던 증상 수정



v2.10.x
====================================

.. _release-cdn-2-10-4:

2.10.4 (2024.11.05)
----------------------------

-  :ref:`origin_dynamic` 에 대한 :ref:`monitoring_stats_vhost_origin` 지원
-  :ref:`caching-purge-async` 기능을 :ref:`caching-purge-async-idbase` 으로 개선 및 :ref:`caching-purge-async-cancelreset` 보강



.. _release-cdn-2-10-3:

2.10.3 (2024.10.22)
----------------------------

-  원본 ``Transfer-Encoding: chunked`` 응답 콘텐츠 캐싱성능 향상



.. _release-cdn-2-10-2:

2.10.2 (2024.09.25)
----------------------------

-  :ref:`origin_dynamic` 기능 추가
-  원본 ``Cache-Control`` 헤더의 ``s-maxage`` 지시자 지원 ( :ref:`caching-policy-priority` 참고)
-  :ref:`handling_http_requests_http_to_https` 기능 추가
-  :ref:`admin-log-origin` 의 ``cs-acceptencoding`` 필드가 기록되지 않던 문제 수정


.. _release-cdn-2-10-1:

2.10.1 (2024.08.21)
----------------------------

-  ( ``v2.10.0`` 버그) 멀티 ``RSA`` 인증서 등록시 인증서가 정상선택되지 않던 증상 수정
-  10GB이상 대용량 파일 캐싱시에도 메모리가 안정적으로 관리될 수 있도록 정책 보강 ( :ref:`adv_topics_perf_cleanup-condition` )
-  서비스 재기동시 디스크 인덱싱 로딩 메커니즘 개선 및 로딩상태를 10초마다 로그에 기록하도록 개선



.. _release-cdn-2-10-0:

2.10.0 (2024.07.24) 
----------------------------

-  ``DSA`` , ``RSA`` 하이브리드 인증서 지원
-  :ref:`handling_http_requests_compression` 우선 알고리즘 지원
-  :ref:`media-mp3-hls` – 낮은 확률의 메모리누수 문제 수정



v2.9.x
====================================


.. _release-cdn-2-9-15:

2.9.15 (2024.07.16) 
----------------------------

-  :ref:`origin-balancemode` ``Hash`` 맵 구성 성능 개선
-  :ref:`media-hls` 비정상 MP4 예외처리 강화
-  디스크 ``Quota`` 설정이 지정된 경우 잔여 공간정책보다 ``Quota`` 설정을 우선하도록 정책 변경
-  ``Rocky Linux 9`` 지원



.. _release-cdn-2-9-14:

2.9.14 (2024.07.08) 
----------------------------

-  WM - httpd 보안 취약점 개선을 위한 버전 업데이트 ( ``v2.4.57`` → ``v2.4.59`` )
-  ``brotli`` :ref:`handling_http_requests_compression` 알고리즘의 ``BrotliQuality`` 기본값 변경 ( ``11`` → ``6`` )



.. _release-cdn-2-9-13:

2.9.13 (2024.06.27) 
----------------------------

-  :ref:`caching-policy-post-method-caching` 시 :ref:`caching-policy-customttl` 이 반영되지 않던 증상 수정
-  최초 객체 초기화 과정 중 원본이 비정상적으로 연결종료하였을 때 데이터 참조 오류로 간헐적으로 비정상 종료 되는 문제 수정
-  :ref:`api-graph` 생성를 응답하는 과정에서 호출 클라이언트가 연결을 종료할 경우 간헐적으로 비정상 종료 되는 문제 수정
-  ``v2.9.11 ~ v2.9.12`` :ref:`caching-policy-vary-header` 가 활성화되어 있지 않은 상태에서 Purge성능이 저하되는 문제 수정


.. _release-cdn-2-9-12:

2.9.12 (2024.06.21) 
----------------------------

-  :ref:`origin-balancemode-on-counter` 동작 중 비정상 종료 되는 문제 수정



.. _release-cdn-2-9-11:

2.9.11 (2024.06.04) 
----------------------------

-  :ref:`monitoring_counter` 기능 추가
-  :ref:`origin-balancemode-on-counter` 기능 추가
-  원본서버 선택이유를 알 수 있도록 :ref:`admin-log-origin` 에 ``cs-balance`` 필드 추가
-  :ref:`caching-policy-vary-header` 로 파생된 객체가 Purge되지 않던 증상 수정



.. _release-cdn-2-9-10:

2.9.10 (2024.05.16) 
----------------------------

-  이미지 툴 - 이미지 라이브러리 업데이트
-  WM - :ref:`adv-vhost-facadevhost` 설정이 구성되지 않던 증상 수정



.. _release-cdn-2-9-9:

2.9.9 (2024.04.09) 
----------------------------

-  :ref:`https-conf` - SNI(Server Name Indication) 필드가 없는 ClientHello에 대해 최상위에 설정된 인증서가 제공되도록 정책 변경
-  :ref:`origin-retry` 동작시 ``Host`` 헤더의 값으로 IP가 설정되던 증상 수정


.. _release-cdn-2-9-8:

2.9.8 (2024.03.18) 
----------------------------

-  원본과 클라이언트의 HTTP 응답코드별 개수 통계를 제공한다. ( :ref:`monitoring_stats_conf` 설정)
-  :ref:`adv-vhost-sharevhost` 를 :ref:`adv_topics_volatile` 로 지정할 수 있다.
-  :ref:`adv_topics_req_hit_ratio` 판정에 ``TCP_RT_HIT`` 상태 추가
-  WM - 가상호스트 목록에서 :ref:`adv-vhost-sharevhost` 가 :ref:`adv-vhost-facadevhost` 로 표기 되는 문제 수정
-  HTTP 비정상 ``Range`` 요청에 처리 정책 변경

   | **Before**. 세션 종료
   | **After**. ``Range`` 헤더 무시



.. _release-cdn-2-9-7:

2.9.7 (2024.03.05) 
----------------------------

-  :ref:`media-hls` 변환시 모노 오디오가 스테레오로 한쪽만 재생되던 증상 수정
-  ``Amazon Linux 2023`` , ``Amazon Linux 2`` 지원 ( :ref:`getting-started-os` )


.. _release-cdn-2-9-6:

2.9.6 (2024.02.05)
----------------------------

-  ``Ubuntu v22.04`` 지원 ( :ref:`getting-started-os` )
-  :ref:`https-conf` - 잘못된 인증서가 설정되더라도 해당 인증서만 제외하고 정상 인증서를 로딩
-  :ref:`env-vhost-defaultvhost` 선택시 서비스 포트를 검사하지 않도록 개선
-  ImageTool(DIMS), 압축등 콘텐츠 가공 과정 중 발생한 원본요청에 대해 ``X-Forwarded-For`` 헤더를 전달하도록 개선
-  원본서버가 ``Content-Type`` 헤더를 응답하지 않을 때 ``Content-Type`` 헤더는 빈 값으로 명시하던 증상 개선



.. _release-cdn-2-9-5:

2.9.5
----------------------------

-  가상 호스트가 삭제될 때 Alias를 반납하여 다른 가상호스트로 양도하도록 개선


.. _release-cdn-2-9-4:

2.9.4 (2023.12.22)
----------------------------

.. warning::

   Cent OS 6 지원 종료
   

-  `HTTP/2 Rapid Reset <https://blog.cloudflare.com/ko-kr/technical-breakdown-http2-rapid-reset-ddos-attack-ko-kr/>`_ 패치
-  :ref:`https-conf` 과 :ref:`handling_http_requests_http2` 설정이 통합되었으며, :ref:`handling_http_requests_http2` 설정은 :ref:`https-conf` 보다 우선한다.
   
   .. note::
      
      :ref:`handling_http_requests_http2` 활성화시 :ref:`https-conf` 의 개별 설정은 무시된다.



.. _release-cdn-2-9-3:

2.9.3 (2023.11.24)
----------------------------

-  ``v2.9.0 ~ v2.9.2`` 에서 원본부하시 비정상 종료될 수 있던 문제 수정
-  :ref:`caching-policy-custom-cachingkey` 사용 시 :ref:`caching-policy-accept-encoding` 설정이 반영되지 않는 문제 수정
-  :ref:`caching-purge-async` - 비동기 무효화 큐가 꽉 차지 않은 상태에서 ``412 Precondition Failed`` 응답 증상 수정


.. _release-cdn-2-9-2:

2.9.2 (2023.11.08)
----------------------------

-  ``v2.9.1`` 에서 :ref:`handling_http_requests_cache_control_etag` 설정이 비활성화되지 않던 문제 수정


.. _release-cdn-2-9-1:

2.9.1 (2023.11.02)
----------------------------

-  :ref:`adv-vhost-sharevhost` 기능 추가
-  ``308 Permanent Redirect`` 응답코드 지원
-  ``Shared`` 모드로 :ref:`api-conf-reload` 동작시 삭제된 가상호스트가 재배포되던 문제 수정
-  캐싱 디스크 삭제 동작시점을 여유공간의 20% 이하로 변경
-  캐싱 디스크를 가용할 수 없는 상황에서 ``Content-Length`` 가 없는 콘텐츠를 캐싱할 때 간헐적으로 비정상 종료 되는 문제 수정



.. _release-cdn-2-9-0:

2.9.0 (2023.08.11)
----------------------------

-  :ref:`caching-policy-custom-cachingkey` 기능 추가
-  `RFC 9111 Age (Session 5.1) <https://www.rfc-editor.org/rfc/rfc9111.html#section-5.1>`_ 스펙 지원
-  설정파일을 콘솔에서 불완전하게 수정하는 중, WM으로 접근할 경우 기존 인증서 설정이 모두 초기화 되는 증상 수정
-  디스크 삭제 프로세스와 비동기 파일 쓰기 시 간헐적 간섭 현상 수정



v2.8.x
====================================

.. _release-cdn-2-8-5:

2.8.5 (2023.07.06)
----------------------------

-  원본 통신 장애로 컨텐츠를 갱신 할 수 없을 경우에 대한 :ref:`caching-policy-invalid-refresh` 동작 설정 기능 추가
-  :ref:`adv-vhost-link` 동작 시나리오 강화
-  :ref:`https_sni` 필드에서 서버 Port를 제거 하도록 수정



.. _release-cdn-2-8-4:

2.8.4 (2023.06.12)
----------------------------

-  :ref:`caching-policy-applyquerystring-match` 기능 추가
-  :ref:`origin-retry` 기능 추가


.. _release-cdn-2-8-3:

2.8.3 (2023.05.02)
----------------------------

-  더 큰 디스크 공간지원을 위한 :ref:`adv_topics_perf_securedisk` 고도화

-  :ref:`caching-policy-ttl-basic` 개선

   -  ``<NoCache Expire="OFF" />`` 속성 추가
   -  ``<NoStore>`` 설정 추가


-  :ref:`origin_exclusion_and_recovery` 시 원본 전체 장애상황이라도 마지막 IP는 배제하지 않는 설정 추가 ::

      <Exclusion All="OFF">3</Exclusion>


-  소스 이미지 ``quality`` 보다 높은 ``quality`` 변환을 요청할 때 변환하지 않는 설정 추가 ::

      <Dims UpscalingQuality="OFF">


-  솔루션 재구동시 파일삭제 대상이 존재한다면 삭제를 진행한다.


.. _release-cdn-2-8-2:

2.8.2 (2023.03.14)
----------------------------

-  :ref:`admin-log-access` 에 빈 문자열이 기록될 수 있는 문제 수정



.. _release-cdn-2-8-1:

2.8.1 (2023.02.16) 
----------------------------

-  :ref:`media-hls` 로 오디오만 존재하는 ``MP4`` 파일을 서비스할 때 ``Content-Type: audio/MP2T`` 로 응답하는 기능 추가



.. _release-cdn-2-8-0:

2.8.0 (2023.01.31)
----------------------------

-  ``brotli`` :ref:`handling_http_requests_compression` 알고리즘 지원
-  :ref:`api-conf-reload-mode` - 변경된 가상호스트만을 로딩하는 ``Shared`` 모드 추가
-  :ref:`handling_http_requests_http2` 가 활성화된 상태에서 ``ECDSA`` 인증서가 로딩되지 않던 문제 수정
-  `dlsym <https://man7.org/linux/man-pages/man3/dlsym.3.html>`_ 함수로 참조되는 외부 라이브러리 로딩속도 개선


v2.7.x
====================================

.. _release-cdn-2-7-42:

2.7.42 (2023.01.19)
----------------------------

-  :ref:`caching-purge-async-management-api` 추가
-  비동기 무효화 동작 중 낮은 확률로 비정상 종료 되는 문제 수정


.. _release-cdn-2-7-41:

2.7.41 (2022.11.11)
----------------------------

-  DNS resolving 시스템 콜이 잠기고 복구되는 시점의 ``sys.log`` 메시지 강화 ::

      [qDnsCache] dns-resolver timeout (domain: google.com, elapsed: 10010 ms)
      [qDnsCache] dns-resolver created (2)
      [qDnsCache] dns-resolver terminated (1)



.. _release-cdn-2-7-40:

2.7.40 (2022.10.20)
----------------------------

-  캐싱객체 :ref:`origin-fullrangeinit-head` 지원
-  DNS resolving 시스템 콜이 잠길 때 원본서버 IP목록이 갱신되지 않던 문제 수정



.. _release-cdn-2-7-39:

2.7.39 (2022.09.15)
----------------------------

-  MP4HLS – ``Dolby (AC-3, EAC-3)`` 지원
-  MP4HLS – 미디어 호환성 강화


.. _release-cdn-2-7-38:

2.7.38 (2022.09.01)
----------------------------

-  Access.log의 ``sc-bytes`` 정밀도 개선
-  `CVE-2022-2274 <https://nvd.nist.gov/vuln/detail/CVE-2022-2274>`_ 취약점 대응
-  `CVE-2022-2097 <https://nvd.nist.gov/vuln/detail/CVE-2022-2097>`_ 취약점 대응


.. _release-cdn-2-7-37:

2.7.37 (2022.07.14)
----------------------------

-  ``RHEL/CentOS Stream 8`` 지원
-  ``RHEL/CentOS Stream 9`` 지원
-  ``Ubuntu 20.04`` 지원
-  ``Rocky Linux 8`` 지원 ( ``RHEL/CentOS`` 패키지 사용)


.. _release-cdn-2-7-36:

2.7.36 (2022.06.28)
----------------------------

**버그수정**

-  HTTP/2가 활성화 되어 있는 경우 원본이 ``204 No Content`` 을 하는 경우 낮은 확률로 ``502 Bad Gateway`` 를 응답 하는 문제 수정 



.. _release-cdn-2-7-35:

2.7.35 (2022.06.16)
----------------------------

-  :ref:`handling_http_requests_header_contentfreshness` 설정 기능

-  캐싱관리 - Root Purge/HardPurge를 허용하지 않는 경우 Purge API 응답 코드 설정 기능

-  :ref:`admin-log-origin` - 원본 요청시간 필드 ``time-request`` 추가


**버그수정**

-  HTTP/2가 활성화 되어 있는 경우 ``X-Forwarded-For`` 헤더의 값에 ``127.0.0.1`` 이 추가 되는 버그 수정



.. _release-cdn-2-7-34:

2.7.34 (2022.05.19)
----------------------------

-  WM - :ref:`caching-purge-async` 구성 중 ``<AsyncControlTarget>`` 설정 기능 누락 수정



.. _release-cdn-2-7-33:

2.7.33 (2022.04.12)
----------------------------

-  `CVECVE-2022-0778 <https://nvd.nist.gov/vuln/detail/CVE-2022-0778>`_ 취약점 대응



.. _release-cdn-2-7-32:

2.7.32 (2022.03.15)
----------------------------

-  :ref:`caching-purge-async` 수행시 요청된 URL에 따라 선별적으로 동기로 처리할 수 있는 ``<AsyncControlTarget>`` 설정 추가
-  바이패스 - POST 요청이 바이패스 되는 경우 간헐적으로 트랜잭션이 완료 되지 않는 문제



.. _release-cdn-2-7-31:

2.7.31 (2022.01.19)
----------------------------


**버그수정**

-  캐싱관리 - 비동기 무효화 API에서 잘못 된 응답 코드가 리턴 되는 문제 수정


.. _release-cdn-2-7-30:

2.7.30 (2022.01.12)
----------------------------

**기능개선/정책변경**

-  캐싱 - :ref:`caching-policy-base` 설정 기능
-  캐싱 - 원본 ``304 Not Modified`` 응답 코드 TTL 별도 설정 기능
-  캐싱관리 - :ref:`caching-purge-async` 기능추가
-  WM - httpd 보안 취약점 개선을 위한 버전 업데이트 ``v2.4.41`` → ``v2.4.51``


**버그수정**

-  설정 변경 시 서비스 응답이 지연 될 수 있는 문제 수정
-  낮은 확률로 ``500 Internal Error`` 가 응답 될 수 있는 문제 수정



2.7.27 (2021.11.04)
----------------------------

**버그수정**

-  간헐적으로 500 에러가 응답 되는 문제 수정
-  캐싱된 콘텐츠 메모리 정리 중 낮은 확률로 비정상 종료 되는 문제 수정



2.7.26 (2021.09.09)
----------------------------

**버그수정**

-   원본 S3인증 사용시 요청 URL에 “~” 있는 경우 인증을 실패 하는 버그 수정



2.7.25 (2021.07.26)
----------------------------

**기능개선/정책변경**

-  MP4HLS – 비정상 인코딩 MP4 파일 호환성 강화
-  :ref:`handling_http_requests_headers_originalheader` - 캐싱 정책과 무관한 원본헤더 값 추가 가능



2.7.24 (2021.06.22)
----------------------------

**기능개선/정책변경**

-  :ref:`caching-policy-nocacherequestexpire` 기능 사용시 이미지툴 원본 파일도 Expire 되도록 정책 변경



2.7.23 (2021.05.31)
----------------------------

**기능개선/정책변경**

-  :ref:`env-cache-storage` - Disk Quota를 비율로 설정하는 기능 추가


**버그수정**

-  4GB 넘는 구간을 :ref:`media-trimming` 할 경우 재생오류 수정
-  이미지 :ref:`media-dims-composite` - 투명도 설정이 미동작 증상 수정



2.7.22 (2021.05.24)
----------------------------

**버그수정**

-  바이패스  - 원본 HTTPS 통신 시에 간헐적으로 비정상 종료 되는 문제
-  WM – 클러스터 적용을 통한 설정 배포 시 설정이 누락 되는 문제 수정


2.7.21 (2021.04.22)
----------------------------

**기능개선/정책변경**

-  ImageTools – 이미지 :ref:`media-dims-resize-stretch-out` 기능 추가
-  원본 :ref:`origin-busysessioncount` 기능 비활성화
-  WM에서 가상호스트 생성시 불필요한 설정 정리



2.7.20 (2021.04.07)
----------------------------

**기능개선/정책변경**

-  `CVE-2021-3449 <https://www.openssl.org/news/secadv/20210325.txt>`_ 취약점 대응
-  `CVE-2021-3450 <https://www.openssl.org/news/secadv/20210325.txt>`_ 취약점 대응




2.7.18 (2021.03.11)
----------------------------

**기능개선/정책변경**

-  미디어 – 비정상 적으로 인코딩 된 MP4 파일 호환성 강화
-  ``HTTP/2`` 에서 ``IPv6`` 를 사용하지 않도록 수정



2.7.17 (2021.02.24)
----------------------------

**기능개선/정책변경**

-  SSL Library(OpenSSL) 버전 업데이트
-  Origin 로그 에 ``time-sock-creation`` , ``x-cs-retry`` 필드 추가


**버그수정**

-  :ref:`adv-vhost-redirection-trace` 과 :ref:`origin_modify_client` 을 함께 사용 할 경우 비정상 종료 되는 문제 수정
-  가상호스트 추가 시 간헐적으로 SNMP 통계가 보이지 않는 문제 수정



2.7.16 (2021.02.01)
----------------------------

**버그수정**

-  원본 HTTPS 통신 시 낮은 확률로 비정상 종료 되는 문제 수정



2.7.15 (2021.1.28)
----------------------------

**기능개선/정책변경**

-  :ref:`caching-policy-customttl-cron` 기능 추가
-  :ref:`handling_http_requests_modify_client` , :ref:`origin_modify_client` - ``#HOSTNAME``  예약어 추가
-  :ref:`handling_http_requests_cache_control_expires` - 남은 TTL 정보를 알려주는 ``#TTL_LEFT`` 예약어 추가
-  [WM] 가상호스트 삭제 시 가상호스트 이름 표시
 


2.7.14 (2020.12.29)
----------------------------

**기능개선/정책변경**

-  MP4HLS – 오디오 포멧 호환성 강화
-  [WM] 가상호스트 삭제시 이름 표시



2.7.13 (2020.11.24)
----------------------------

**기능개선/정책변경**

-  Fatal 로그 기록 방식 개선
-  :ref:`monitoring-stats-vhost` , :ref:`monitoring-stats-host` - 시간 정밀도 개선
 

**버그수정**

-  :ref:`admin-log-access-custom` - ``%H`` 예약어가 동작하지 않는 문제 수정



2.7.12 (2020.10.22)
----------------------------

**기능개선/정책변경**

- :ref:`adv-vhost-url-rewrite` – :ref:`adv-vhost-url-rewrite-protocol` 추가
- :ref:`origin-balancemode-url-suffix-ignore` 추가
 

**버그수정**

- ``ByClient`` 기능 사용시 Purge API가 수행 되지 않는 문제
- 바이패스 동작 중 비정상 종료 되는 문제
- HardPurge 수행 중 낮은 확률로 비정상 종료 되는 문제 수정



2.7.11 (2020.9.4)
----------------------------

**기능개선/정책변경**

- [원본] :ref:`adv-vhost-redirection-trace` - ``<URL>`` 조건 추가
- [원본] :ref:`origin-cache-control` 변경
- [MP4] :ref:`media-trimming` 호환성 강화
 
**버그수정**

- [클라이언트] CentOS 7에서 낮은 확률로 응답이 누락 될 수 있는 문제 수정
- [바이패스] 낮은 확률로 비정상 종료 되는 문제 수정
- [ :ref:`adv-vhost-link` ] 링크가 2번 동작 할 수 있는 문제 수정
- [WM] 삭제 된 가상호스트가 가상호스트 목록에 남아 있는 문제 수정



2.7.10 (2020.8.13)
----------------------------

**기능개선/정책변경**

- 일부 고객사 커스터마이징 기능 강화



2.7.9 (2020.7.23)
----------------------------

**기능개선/정책변경**

- :ref:`handling_http_requests_modify_client` - ``#SESSIONID`` 예약어 추가


**버그수정**

- MPxHLS – PCR 계산식 호환성 강화
- HTTPS 절대 경로로 요청이 올 경우 낮은 확률로 비정상 종료 되는 문제 수정



2.7.8 (2020.7.15)
----------------------------

**버그수정**

- 파일을 삭제 하는 중에 낮은 확률로 종료 되는 문제 수정 (보완)


2.7.7 (2020.7.13)
----------------------------

**기능개선/정책변경**

 - HardPurge를 이용한 전체 콘텐츠 삭제 금지기능 ``<RootHardPurge>`` 추가 
 - :ref:`access-control-vhost` - HTTP 요청의 Host헤더를 참조하는 ``#HOST`` 예약어 추가
 - :ref:`adv_topics_volatile` 기능 추가
 - 대량의 가상호스트 설정변경 성능 개선
 - 원본서버 – 최소 DNS TTL 설정 기능 추가
 

**버그수정**

- 파일을 삭제 하는 중에 낮은 확률로 종료 되는 문제 수정
- :ref:`caching-policy-vary-header` 사용시 HTTPS요청에 대해 가상호스트를 찾지 못하는 문제 수정


2.7.6 (2020.6.10)
----------------------------

**버그수정**

-  HTTPS - SSLv3.0 이 활성화 되지 않는 문제 수정(2.7.0 ~ 2.7.5)
-  HTTPS - SNI가 활성화 되어 있는 경우 인증서가 잘못 선택 되는 문제 수정

   .. note::
   
      *.winesoft.co.kr, *.image.winesoft.co.kr과 같이 동일한 도메인에 대해서 각각 발급 받은 인증서를 함께 설정할 경우에만 문제가 발생합니다.



2.7.5 (2020.5.14)
----------------------------

**버그수정**

 - MP4 비정상 예외처리 (Timescale 필드 값이 0인 경우)



2.7.4 (2020.4.21)
----------------------------

**기능개선/정책변경**

 - :ref:`admin-log-originerror` - 원본서버 Port 필드 ``s-port`` 추가
 - 원본서버가 ``If-Range`` 에 대한 응답으로 200 OK를 줄 경우 파일을 갱신 하도록 정책 변경
 - :ref:`handling_http_requests_header_if_range` -  클라이언트가 보낸 If-Range의 값이 더 최신이라면 캐싱 컨텐츠를 Purge 하는 속성 추가

**버그수정**

 - :ref:`media-mp4-upfront-header` - 일부 파일의 CPU 과점유 현상 개선



2.7.3 (2020.3.12)
----------------------------

:ref:`handling_http_requests_custom_error_page` 기능 추가



2.7.2 (2020.2.18)
----------------------------

**기능개선/정책변경**

 - 바이패스/ :ref:`bypass-affinity-sticky` - Sticky 속성 추가


**버그수정**

 - HTTPS - [2.6.17 ~ 2.7.1] SSL 전송이 미완료 되는 문제 수정



2.7.1 (2020.1.20)
----------------------------

**버그수정**

 - :ref:`handling_http_requests_http2` - HEAD 요청이 처리 되지 않는 문제 수정
 - :ref:`handling_http_requests_http2` - 인증서 파일이 백업되지 않는 문제 수정
 - 원본 S3 인증이 실패 하는 문제 수정



2.7.0 (2019.12.27)
----------------------------

- :ref:`handling_http_requests_http2` 지원

**기능개선/정책변경**

 - :ref:`media-mp3-hls` – TS 변환 시 PCR을 추가 하는 기능

   .. note::

      PCR 추가 기능이 활성화되면 이전에 생성된(PCR 필드가 없는) TS파일과 호환이 되지 않습니다.




v2.6.x
====================================

2.6.18 (2019.11.28)
----------------------------

**기능개선/정책변경**

 - ImageTool – 비정상 변환 파라미터 안정성 강화
 - 헤더변조 – 요청 PORT를 추가 할 수 있는 ``#PORT`` 예약어 추가

**버그수정**

 - WM – 설정 된 HTTPS 인증서가 50개 이상인 경우 클러스터 적용이 오동작 하는 문제 수정
 - RRD 통계 프로세스가 비정상 종료 되는 문제 수정



2.6.17 (2019.10.29)
----------------------------

**기능개선/정책변경**

 -  LTE 환경에서 대용량 파일 전송 최적화



2.6.16 (2019.10.10)
----------------------------

**버그수정**

 - HTTPS – POST Bypass 요청이 간헐적으로 처리 되지 않는 문제 수정
 - 원본 서버가 1초 안에 모두 배제/복구 될 경우 비정상 종료 될 수 있는 문제 수정



2.6.15 (2019.9.26)
----------------------------

**기능개선/정책변경**

 - 원본서버 - :ref:`origin_aws_s3_authentication` 지원
 - ImageTool(DIMS) - 이미지 포맷이 변경되면, 변경된 포맷의 표준 Content-Type 헤더를 제공
 - WM - Apache 업데이트 (v2.4.41)



2.6.14 (2019.8.14)
----------------------------

**기능개선/정책변경**

 - ImageTool(DIMS) - :ref:`media-dims-autorotate` 기능 추가
 - HTTPS - ECDSA Key 파일 호환성 강화
 - 1분 평균 통계 API 지원

**버그수정**

 -  WM - GeoIP 데이터베이스 파일이 업로드 되지 않는 문제
 -  WM - CustomTTL을 편집 할 수 없는 문제
 -  HTTPS - DSA 인증서에서 RSA인증서로 교체 할 경우 비정상 종료 되는 문제


2.6.13 (2019.7.4)
----------------------------

**기능개선/정책변경**

 - :ref:`adv_topics_rrd_inactive` - 기능 추가
 - :ref:`caching-policy-customttl` – 원본 응답 조건 추가
 - :ref:`origin_exclusion_and_recovery` - 원본 서버를 배제 하지 않는 기능 추가 

**버그수정**

 -  WM – 시스템 설정 중 디스크 설정이 초기화 될 수 있는 문제 수정
 -  Hardware Info API를 호출 할 경우 CPU 사용량이 증가하는 문제 수정


2.6.12 (2019.5.9)
----------------------------

**기능개선/정책변경**

 - ImageTool(DIMS) - 원본이미지 조건판단 기능 개선

**버그수정**

 - GeoIP2를 사용 할 경우 낮은 확률로 비정상 종료 될 수 있는 문제 수정

   .. note::

      GeoIP2는 Database 파일을 덮어쓰기로 업데이트 하는 것을 지원하지 않습니다.




2.6.11 (2019.4.12)
----------------------------

**버그수정**

 -  HTTPS – ``[v2.6.9 ~ v2.6.10]`` SNI 기능이 활성화 되어 있는 경우 낮은 확률로 일부 클라이언트가 보낸 ServerName 을 찾지 못하고 Alert를 응답하는 문제 수정
 
    .. note::

       SNI 기능을 사용하지 않으시면 문제가 발생하지 않습니다.



2.6.10 (2019.4.11)
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



2.6.9 (2019.3.13)
----------------------------

**기능개선/정책변경**

 - HTTPS - TLS v1.3 지원

**버그수정**

 -  WM - 헤더 변조 기능에 빈 값을 넣을 수 없는 문제
 -  HTTPS - SNI 기능 사용시 인증서마다 프로토콜 설정을 할 수 없는 문제



2.6.8 (2019.2.11)
----------------------------

**기능개선/정책변경**

- :ref:`handling_http_requests_modify_client` - 클라이언트 요청 헤더의 값을 원본 요청 헤더에 추가하는 기능

**버그수정**

 -  원본 서버를 50개 이상 설정 했을 경우 낮은 확률로 비정상 종료 되는 문제
 -  WM - HTTPS 인증서 클러스터 적용 시 SNI 설정이 초기화 되는 문제



2.6.7 (2019.1.16)
----------------------------

**기능개선/정책변경**

- GeoIP2 지원



2.6.6 (2018.12.19)
----------------------------

**기능개선/정책변경**

- ImageTool(Dims) - 이미지 Color Profile 정책 변경
- Access 로그 롤링 파일명을 초 단위까지 명시하도록 변경. 기존 버전과의 호환성을 위해서 로그 타입을 TIME을 설정 했을 경우에는 기존 파일명 정책을 유지합니다.



2.6.5 (2018.11.15)
----------------------------

**기능개선/정책변경**

- 디스크 인덱싱 기능 제거


**버그수정**

 -  설정 값 Reload API가 동시에 요청 될 경우 비정상 종료 되는 문제
 -  메모리 모드에서 파일 분포 통계가 맞지 않는 문제
 -  HTTPS – 낮은 확률로 비정상 종료 되는 문제


2.6.4 (2018.10.15)
----------------------------

**버그수정**

 -  [2.6.0 ~ 2.6.3] URL 바이패스 기능 동작 시 낮은 확률로 비정상 종료 되는 문제 수정



2.6.3 (2018.9.18)
----------------------------

**버그수정**

 - HTTPS – Multi NIC로 인증서를 설정 할 경우 *:443 설정과 STATIC-IP:443 설정이 혼합되어 있으면 인증서를 찾지 못하는 문제


2.6.2 (2018.9.12)
----------------------------

**버그수정**

 - 간헐적으로 HTTPS 세션이 끊어지는 문제 수정


2.6.1 (2018.9.7)
----------------------------

**버그수정**

 - 일부 시스템 환경에서 전송 완료 시간이 늘어나는 증상


2.6.0 (2018.9.3)
----------------------------

- :ref:`env-vhost-activeorigin` - HTTPS 통신 지원

**기능개선/정책변경**

- HTTPS - 성능개선 및 ECDSA 인증서 지원
- :ref:`handling_http_requests_cache_control_expires` – 원본 Max-Age 값을 사용하는 기능 추가


v2.5.x
====================================

2.5.18 (2018.8.8)
----------------------------

**기능개선/정책변경**

- :ref:`handling_http_requests_modify_client` - 요청 헤더의 값을 응답 헤더에 추가한다.
- :ref:`media-dims` - 이미지 포맷이 변경되면 해당 포맷의 Content-Type으로 응답하도록 정책 수정


2.5.17 (2018.7.10)
----------------------------

**기능개선/정책변경**

- 바이패스 응답에도 :ref:`handling_http_requests_basic_via` 추가하도록 정책변경


**버그수정**

 - :ref:`media-dims` - :ref:`media-dims-byoriginal` 에서 :ref:`media-dims-optimize` 가 동작하지 않던 증상
 - WM - 클러스터 복제시 설정이 누락되던 증상
 - Indexing과 파일 삭제가 동시에 동작할 경우 낮은 확률도 비정상 종료되던 증상


2.5.16 (2018.5.29)
----------------------------

**기능개선/정책변경**

- :ref:`media-hls` - 키프레임의 간격이 불규칙한 영상에 대한 호환성 강화

.. warning::

   이전 버전과 :ref:`media-hls` 의 MPEG2-TS가 호환되지 않습니다.



2.5.15 (2018.5.21)
----------------------------

**버그수정**

 -  :ref:`handling_http_requests_header_lastmodifiedcheck` - ``orlater`` 로 설정 할 경우 최초 캐싱 시 304 응답을 할 수 있는 문제 수정


2.5.14 (2018.4.26)
----------------------------

-  클라이언트 요청 :ref:`handling_http_requests_header_if_range` 헤더 지원 
-  원본 요청 시 :ref:`origin_header_if_range` 헤더 지원
-  :ref:`handling_http_requests_header_lastmodifiedcheck` 설정기능 추가


2.5.13 (2018.3.27)
----------------------------

**기능개선/정책변경**

- :ref:`handling_http_requests_modify_client` - CACHE-HIT 결과를 응답 헤더에 추가한다.
- WM - CI 변경


**버그수정**

 - TTL을 0으로 설정 하고 빠르게 컨텐츠가 갱신되면 i-node가 증가하는 증상
 - 특정 환경에서 Index 파일이 계속 커지는 증상



2.5.12 (2018.2.26)
----------------------------

**기능개선/정책변경**

- :ref:`media-hls` - 미디어정보와 실제 파일의 크기가 다른 경우 예외처리 강화



2.5.11 (2018.1.25)
----------------------------

**기능개선/정책변경**

 - SSL/TLS - :ref:`https-ciphersuite` SHA384 지원
 - SSL/TLS - `The ROBOT Attack <https://robotattack.org/>`_ 대응
 - :ref:`handling_http_requests_modify_client` - HTTP 요청 Method 조건 추가
 - :ref:`access-control-vhost` - POST 요청도 접근 제한이 가능하도록 개선
 - WM - 캐싱상태 확인 페이지에 HTTPS 다운로드 기능 추가



2.5.10 (2017.12.18)
----------------------------

**기능개선/정책변경**

 - :ref:`media-dims` - Round(이미지 모서리를 둥글게 처리) 명령어 추가
 - :ref:`handling_http_requests_modify_client` , :ref:`origin_modify_client` - #PROTOCOL 키워드 추가
 - :ref:`env-etc` - 빈 디렉토리 삭제정책 추가
 - :ref:`api-conf-upload-xml` 추가


**버그수정**

 - 일부 API 호출결과 JSON 문법오류 수정



2.5.9 (2017.11.30)
----------------------------

**버그수정**

 - :ref:`media-dims` - 세로 길이만 입력 할 경우 Resize 되지 않는 문제 수정
 - :ref:`media-hls` - 일부 iOS에서 낮은 확률로 재생되지 않는 증상



2.5.8 (2017.11.9)
----------------------------

- :ref:`origin-use-policy` - DNS에서 Resolving된 IP의 최대 사용시간을 설정한다.

**기능개선/정책변경**

 - :ref:`media-dims` - ``ResizeCrop`` 명령어 추가
 - :ref:`media-dims` - :ref:`media-dims-anigif` 변환시 프레임 수 제한 명령어 ``limit`` 추가
 - :ref:`access-control-vhost` - :ref:`access-control-vhost_redirect` 조건에 ``PROTOCOL`` 조건 추가

**버그수정**

 - :ref:`origin-use-policy` - DNS에서 Resolving된 IP의 누적개수가 많아질 경우 통계집계가 지연되던 증상
 - [WM] :ref:`access-control-vhost` UI가 깨지는 증상
 - [WM] :ref:`handling_http_requests_modify_client` 설정이 초기화되는 증상



2.5.7 (2017.10.13)
----------------------------

**버그수정**

 - [v2.5.5 ~ v2.5.6] Transfer-Encoding 콘텐츠의 메모리가 정리되지 않던 문제 수정
 - [v2.4.6 ~ v2.5.6] :ref:`media-mp3-hls` - 캐싱된 콘텐츠가 갱신될 경우 비정상 종료되는 문제 수정




2.5.6 (2017.9.28)
----------------------------

- HTTP OPTIONS Method 지원

**버그수정**

 - 설정이 정상적으로 백업되지 않을 때 SNMP 관련 설정이 반영되지 않던 문제 수정
 - :ref:`handling_http_requests_compression` - TTL이 초기화되던 문제 수정



2.5.5 (2017.8.30)
----------------------------

- 콘텐츠 :ref:`handling_http_requests_drm` 을 지원한다.
- :ref:`caching-policy-unvalidatable` 을 설정할 수 있다.

**기능개선/정책변경**

- :ref:`adv_topics_memory_only` 안정성 강화
- 클러스터 정보 조회 :ref:`wm_cluster_list_api` 추가
- [WM] Apache 보안 권고사항 반영


**버그수정**

 - :ref:`media-dims` , :ref:`handling_http_requests_compression` 된 파일에 대한 I/O가 실패 한 경우 변환 요청이 Bypass 되는 문제
 


2.5.4 (2017.8.10)
----------------------------

**버그수정**

 - [v2.5.0 ~ v2.5.3] Byte Hit Ratio가 떨어지는 문제 수정


2.5.3 (2017.7.10)
----------------------------

**버그수정**

 - [v2.5.0 ~ v2.5.2] SSL 정상 동작하지 않는 문제 수정



2.5.2 (2017.7.6)
----------------------------

**기능개선/정책변경**

 - :ref:`media-dims` Trim과 Crop Center기능 추가
 - :ref:`media-dims` Geometric 정보가 잘못 된 요청에 대한 예외처리 강화
 
**버그수정**

 - :ref:`adv_topics_memory_only` 에서 Disk 정리 로직이 수행되는 증상 수정
 - :ref:`adv-vhost-link` 에서 간헐적으로 다음 가상호스트로 넘어가지 않는 문제 수정



2.5.1 (2017.6.8)
----------------------------

**기능개선/정책변경**

 -  POST 요청을 캐싱 할 경우 원본 서버에 클라이언트가 보낸 Content-Type을 보내도록 변경
 
**버그수정**

 - [v2.5.0] :ref:`origin_partsize` 기능이 활성화 되어 있는 경우 캐싱 되어 있던 파일이 초기화 되는 문제
 - [v2.5.0] :ref:`origin_partsize` 기능이 활성화 되어 있는 Write 통계가 수집되지 않는 문제
 - WM – HTTP 헤더 변경시 따옴표(“)가 입력되지 않는 문제



2.5.0 (2017.5.25)
----------------------------

- HTTPS - :ref:`https_sni` 를 지원한다.
- :ref:`adv_topics_memory_only` 를 지원한다.



v2.4.x
====================================


2.4.11 (2017.5.18)
----------------------------

**버그수정**

 - MP4 헤더가 뒤에 있고 크기가 4G 이상인 파일이 Pseudo-Streaming이 되지 않는 문제 수정




2.4.10 (2017.5.11)
----------------------------

**버그수정**

 - :ref:`media-hls` - 헤더가 큰 MP4 파일을 HLS로 서비스 할 경우 낮은 확률로 경우 영상과 음성이 맞지 않는 문제 수정



2.4.9 (2017.4.24)
----------------------------

**기능개선/정책변경**

 - :ref:`media-hls` - 인코딩 정보가 모든 키프레임에 들어 있는 영상에 대한 호환성 강화
 - 고사양 서버의 메모리 사용정책 최적화 (Disk I/O가 느려질 경우 메모리 정리가 지연되던 증상 개선)

**버그수정**

 - STON Edge Server가 실행 중에 시스템 시간이 변경되면 1시간 동안 통계가 누락되는 문제
 - :ref:`origin-health-checker` 세션이 활성화 되어 있는 경우 아주 낮은 확률로 비정상 종료 될 수 있는 문제
 - Bypass 세션이 활성화 되어 있는 상태에서 Disk가 배제 될 경우 낮은 확률로 비정상 종료 될 수 있는 문제
 - (로그 압축 기능 사용 시) 로그가 압축 되는 시점에 로그가 일부 누락 될 수 있는 문제
 - :ref:`origin_partsize` 기능이 활성화된 상태에서 헤더가 큰 미디어 파일을 서비스 할 때 최초 요청이 간헐적으로 끊어질 수 있는 문제


2.4.8 (2017.4.17)
----------------------------
**버그수정**

 - 하나의 가상호스트에서 약 20억개 이상의 파일이 신규로 생성되면 비정상 종료 되는 증상



2.4.7 (2017.4.11)
----------------------------
**버그수정**

 - [2.4.5 ~ 2.4.6] SSL 통신 시 CPU 사용량 및 시스템 부하가 높아지는 증상


2.4.6 (2017.3.29)
----------------------------

- :ref:`media-mp3-hls` MP3형태로 Segementation이 가능하다.

**기능개선/정책변경**

 - :ref:`media-mp3-hls` - 분석과정 오류가 발생할 경우 정책 수정

     | **Before**. 404 Not Found 응답
     | **After**. 분석된 지점까지 HLS로 서비스

 - :ref:`media-hls` - 시간값(PCR, PTS, DTS) 계산식 변경을 통한 플레이어 호환성 강화

**버그수정**

 - 낮은 확률로 404 응답이 메모리에서 Swap 될 때 비정상 종료 되는 문제


.. warning::

   이전 버전과 :ref:`media-hls` 의 MPEG2-TS가 호환되지 않습니다.


2.4.5 (2017.2.16)
----------------------------
**버그수정**

 - :ref:`media-dims` 처리시 원본 서버가 Transfer-Encoding: chunked로 응답 할 경우 비정상 종료되는 증상
 - SSL CipherSuite를 ECDHE 만 선택하도록 설정 할 경우 크롬 브라우저에서 연결이 종료되는 증상
 - 매우 낮은 확률로 로그 정리시 비정상 종료 되는 증상



2.4.4 (2017.2.8)
----------------------------
**버그수정**

 - 원본 서버 장애 시 간헐적으로 :ref:`media-dims` 변환 요청이 Bypass 되는 증상


2.4.3 (2017.1.20)
----------------------------
**버그수정**

 - 압축 기능 사용시 간헐적으로 Content-Encoding 헤더가 누락되는 증상

2.4.2 (2017.1.18)
----------------------------

   - :ref:`adv-vhost-link` 추가

**버그수정**

 - 원본 서버가 Content-Length헤더에 음수 값을 줄 경우 비정상 종료 되는 증상
 - :ref:`media-mp3-hls` - 원본 서버와의 통신이 불안정 할 경우 간헐적으로 비정상 종료 되는 증상

2.4.1 (2016.11.24)
----------------------------
**기능개선/정책변경**

 - 원본 HTTP 응답에서 reason phrases가 없는 경우에도 처리 할 수 있도록 정책 변경
 -	:ref:`media-dims` – 이미지 확대 시 캔버스만 키우는 기능 추가

**버그수정**

 - 압축 기능 사용 시 아주 낮은 확률로 압축 된 파일이 깨지는 증상 수정
 -	VLC 플레이어에서 M4A HLS가 재생되지 않는 문제 수정
 - :ref:`media-dims` 를 이용해서 이미지 변환시 변환 크기를 입력하지 않을 경우 비정상 종료되는 증상

2.4.0 (2016.11.7)
----------------------------
**기능개선/정책변경**

 - 원본요청 URL변경 기능 추가
 - M4A를 m4a-hls 로 전송한다

**버그수정**

 - Invalid mp4 헤더의 강화된 처리

v2.3.x
====================================

2.3.9 (2016.10.28)
----------------------------


**버그수정**

 - 일부 환경에서 낮은 확률로 수 초간 컨텐츠가 갱신되지 않던 증상


2.3.8 (2016.10.13)
----------------------------


**버그수정**

 - Invalid mp4 헤더의 강화된 처리


2.3.7 (2016.09.26)
----------------------------

**기능개선/정책변경**

 - :ref:`media-dims` 기능을 이용해서 이미지 변환시 시스템 자원 사용량을 제한하도록 정책 변경
 - Health-Checker 기능 사용시 Standby 원본 서버도 검사하도록 정책 변경

**버그수정**

 - :ref:`handling-http-requests-compression` 기능의 ON/OFF 설정이 반영되지 않던 버그 수정


2.3.6 (2016.08.16)
----------------------------

**기능개선/정책변경**

 - 일부 투명 PNG를 JPG로 포멧 변환시 배경이 검은색으로 변경되는 문제 수정
 - 비정상적인 클라이언트 소켓 처리 정책 강화

**버그수정**

 - DIMS변환 중 Hardpurge API를 호출 할 경우 간헐적으로 비정상 종료 되던 증상


2.3.5 (2016.07.01)
----------------------------

**기능개선/정책변경**

 - Native HLS 모듈을 사용하는 플레이어와의 호환성 강화
 - DIMS의 Crop 기능은 비율을 유지 하지 않고 입력한 크기로 Crop 하도록 정책 변경

**버그수정**

 - Health-Checker 기능이 활성화 되어 있는 상태에서 원본상태 초기화 API 호출시 간헐적으로 비정상 종료되는 문제 수정


2.3.4 (2016.06.03)
----------------------------

**기능개선/정책변경**

   - 32bit atom으로 인코딩된 4기가 이상의 MP4 파일 지원
   - unknown access 로그에 Host 헤더 값 추가
   - WM - 보안권고 사항으로 STON 최초 설치 시 Apache manual 폴더 삭제
   - WM - STON 최초 설치 시 Apache 구동 계정인 winesoft 계정을 nologin 권한으로 생성하도록 변경

**버그수정**

   - HLS - 일부 영상에서 CPU를 과점유 하던 증상
   - HTTP 요청이 바이패스 될 때 낮은 확률로 비정상 종료 되던 증상
   - Access 로그에 클라이언트 IP가 0.0.0.0 으로 기록 되던 증상
   - 가상호스트가 260개 이상일 경우 설정 파일이 백업되지 않던 증상

2.3.3 (2016.04.26)
----------------------------

**버그수정**

   - [2.3.0 ~ 2.3.2] 원본서버 Host 설정과 Dims, 압축 설정이 함께 되어 있는 경우 404 에러 코드를 응답하는 증상
   - SNMP View 생성 후 삭제시 CPU 과점유 증상
   - WM - SNMP GlobalMin 값을 0으로 설정 할 수 없던 증상


2.3.2 (2016.03.22)
----------------------------

**기능개선/정책변경**

   - :ref:`mp3-hls` 인덱스 파일 호환성 강화

**버그수정**

   - 정상적인 Handshake없이 암/복호화가 진행되면 비정상 종료되던 증상
   - ACL이 활성화된 상태에서 간헐적으로 비정상 종료되던 증상


2.3.1 (2016.02.25)
----------------------------

   - MP3를 :ref:`mp3-hls` 로 전송한다.

**기능개선/정책변경**

   - :ref:`admin-log-access-custom` 추가
     | %y 요청 HTTP 헤더 크기
     | %z 응답 HTTP 헤더 크기

**버그수정**

   - WM - Dest 포트를 입력하지 않으면 설정되지 않던 증상


2.3.0 (2016.02.03)
----------------------------

   - 컨텐츠를 :ref:`handling-http-requests-compression` 하여 전송한다.

**버그수정**

   - :ref:`expires` 헤더 시간을 Modification으로 설정한 경우 max-age 값이 잘못 계산되던 증상
   - :ref:`media-dims` - 평균 통계 산출할 때 분모를 “성공” 횟수만 사용하던 증상


v2.2.x
====================================

2.2.5 (2016.01.12)
----------------------------

**기능개선/정책변경**

   - HTTP <451 Unavailable For Legal Reasons> 응답코드 추가

**버그수정**

   - TLS - 공격성 패킷에 비정상 종료되던 증상 (예외처리 강화)


2.2.4 (2015.12.11)
----------------------------

**버그수정**

   - HLS - 일부 영상에서 Segmentation정책때문에 재생되지 않던 증상


2.2.3 (2015.12.04)
----------------------------

**버그수정**

   - v2.2.2에서 WM을 통해 가상호스트가 생성되지 않던 증상


2.2.2 (2015.12.04)
----------------------------

   - 원본으로 보내는 HTTP요청의 헤더를 변조한다.

**기능개선/정책변경**

   - :ref:`handling-http-requests-modify-client` - put액션 추가. 같은 이름의 헤더를 멀티라인으로 삽입한다.


2.2.1 (2015.11.19)
----------------------------

**버그수정**

   - TLS - Handshake과정 중 클라이언트가 ChangeCipherSpec과 ClientFinished을 따로 보낼 때, 서버가 ChangeCipherSpec을 중복해서 보내던 증상
   - DIMS - Animated GIF를 리사이즈할 때 비율이 유지되지 않던 증상


2.2.0 (2015.11.04)
----------------------------

   - TLS 1.2를 지원한다. (+Forward Secrecy등 세세한 보안정책 강화)

**버그수정**

   - 디스크 정보를 얻지 못한 경우 비정상 종료되던 증상
   - TLS - Handshake과정에서 Max버전을 선택하지 않던 증상

     | **Before**. TLSPlaintext.version 사용
     | **After**. ClientHello.client_version 사용


v2.1.x
====================================

2.1.9 (2015.10.15)
----------------------------

**버그수정**

   - :ref:`media-hls` - v2.1.7 업데이트 이후 일부 영상이 정상적으로 재생되지 않던 증상


2.1.8 (2015.10.14)
----------------------------

**버그수정**

   - [v2.1.6 ~ 2.1.7] 허용되지 않은 IP에서 매니저 포트로 접근시 비정상 종료되던 증상


2.1.7 (2015.10.07)
----------------------------

   - :ref:`multi-trimming` - 시간 값을 기준으로 복수로 지정된 구간을 하나의 영상으로 추출한다.

**기능개선/정책변경**

   - :ref:`access` - X-Forwarded-For헤더 기록옵션에 TrimCIP추가

**버그수정**

   - HLS - 일부 profile에서의 화면떨림 증상
   - :ref:`media-dims` - TTL이 0으로 설정되어 있을 때 간헐적으로 500 Internal Error로 응답하던 증상
   - X-Forwarded-For 헤더를 로그에 c-ip필드로 기록할 때 공백 문자가 포함되던 증상


2.1.6 (2015.09.10)
----------------------------

**기능개선/정책변경**

   - :ref:`media-dims` - Animated GIF 에 대해 첫 장면만 변환할 수 있다.

**버그수정**

   - ACL - IP허용/차단이 정상동작하지 않던 증상
   - :ref:`media-dims` - Crop등에서 + 기호를 이용한 좌표지정이 되지 않던 증상


2.1.5 (2015.08.18)
----------------------------

   - :ref:`sub-path` - 접근 경로에 따라 다른 가상호스트로 분기한다.
   - :ref:`facade` - 접근 도메인에 따라 클라이언트 트래픽 통계와 Access로그를 분리한다.


2.1.4 (2015.07.31)
----------------------------

**기능개선/정책변경**

   - CPU사용량 개선
   - :ref:`multi-nic` - NIC이름으로 Listen한다.
   - 접근제어 시점 변경

     | **Before**. 클라이언트가 요청한 URI에서 키워드(DIMS나 MP4HLS등) 제거 후 검사
     | **After**. 클라이언트가 요청한 URI 그대로 검사

**버그수정**

   - :ref:`media-dims` - 인코딩된 변환 문자열을 인식하지 못하던 증상
   - :ref:`hardpurge` 가 :ref:`caching-policy-casesensitive` 정책을 따르지 않던 증상
   - 설정백업할 때 :ref:`post` 이 누락되던 증상


2.1.3 (2015.06.25)
----------------------------

**기능개선/정책변경**

   - :ref:`syncstale` - 관리(:ref:`purge`, :ref:`expire`, :ref:`hardpurge`) API호출이 인덱싱에 반영되지 않는 경우가 없도록 로그로 기록하여 서비스 재가동시 다시 반영한다.
   - :ref:`admin-log-access-custom` 에 %u표현 추가. 클라이언트가 요청한 Full URI를 기록한다.

**버그수정**

   - :ref:`media-dims` - 원본서버에서 Last-Modified헤더를 주지 않을 때 이미지가 갱신되지 않던 증상
   - :ref:`trimming` 된 MP4의 크기가 4GB를 넘어갈 때 CPU를 과점유하던 증상
   - 에러 페이지를 응답할 때 :ref:`via` 헤더 설정이 반영되지 않던 증상


2.1.2 (2015.05.29)
----------------------------

   - WM - 영문버전 지원

**기능개선/정책변경**

   - Single Core 장비 지원

**버그수정**

   - :ref:`adv-topics-indexing` 모드에서 커스터마이징 모듈이 오동작하던 증상


2.1.1 (2015.05.07)
----------------------------

   - HLS - Stream Alternates형식을 통해 Bandwidth, Resolution 정보를 제공한다.

**버그수정**

   - 헤더가 깨진 MP4영상 분석 중 비정상 종료되던 증상


2.1.0 (2015.04.15)
----------------------------

   - :ref:`media-dims` 에서 Animated GIF포맷을 지원한다.
   - :ref:`media-dims` 변환 통계추가

**기능개선/정책변경**

   - :ref:`caching-purge` API에서 디렉토리 표현 제거

     | 디렉토리 표현(example.com/img/)은 해당 URL에 해당하는 (원본서버가 응답한)파일 하나만을 의미한다.
     | 기존의 디렉토리 표현(example.com/img/)은 패턴(example.com/img/*)으로 통합한다.

   - API표현 추가

     | /monitoring/average.xml
     | /monitoring/average.json
     | /monitoring/realtime.xml
     | /monitoring/realtime.json
     | /monitoring/fileinfo.json
     | /monitoring/hwinfo.json
     | /monitoring/cpuinfo.json
     | /monitoring/vhostslist.json
     | /monitoring/geoiplist.json
     | /monitoring/ssl.json
     | /monitoring/cacheresource.json
     | /monitoring/origin.json
     | /monitoring/coldfiledist.json

   - WM - resolv.conf 편집기능 삭제


v2.0.x
====================================

2.0.8 (2015.08.06)
----------------------------

**기능개선/정책변경**

   - CPU사용량 개선

**버그수정**

   - 설정백업할 때 POST 요청 예외조건이 누락되던 증상


2.0.7 (2015.06.25)
----------------------------

**버그수정**

   - :ref:`media_dims` - 원본서버에서 Last-Modified헤더를 주지 않을 때 이미지가 갱신되지 않던 증상
   - :ref:`trimming` 된 MP4의 크기가 4GB를 넘어갈 때 CPU를 과점유하던 증상
   - 에러 페이지를 응답할 때 :ref:`via` 헤더 설정이 반영되지 않던 증상


2.0.6 (2015.04.28)
----------------------------

**기능개선/정책변경**

   - WM - resolv.conf 편집기능 삭제

**버그수정**

   - 헤더가 깨진 MP4영상 분석 중 비정상 종료되던 증상


2.0.5 (2014.04.01)
----------------------------

**기능개선/정책변경**

   - Trimming 된 영상을 HLS 로 서비스할 수 있다.
     다음은 원본영상(/vod.mp4)의 0~60초 구간을 Trimming한 뒤 HLS 로 서비스하는 표현이다.

       | /vod.mp4?start=0&end=60/**mp4hls/index.m3u8**
       | /vod.mp4**/mp4hls/index.m3u8**?start=0&end=60
       | /vod.mp4?start=0/**mp4hls/index.m3u8**?end=60

   - HLS 인덱스 파일(.m3u8) 버전 개선

       | **Before**. 버전 1
       | **After**. 버전 3 (버전 1로 변경 가능)

**버그수정**

   - HLS 변환 중 HTTP인코딩되는 특수문자가 있을 때 비정상 종료되던 증상
   - 헤더가 깨진 MP4영상 분석 중 CPU가 과도하게 점유되던 증상
   - Audio의 KeyFrame이 균일하지 않은 MP4영상을 HLS 로 서비스할 때 Audio와 Video의 동기가 안맞는 증상
   - RRD - 통계수집이 되지 않던 증상, 응답시간이 평균이 아니라 합으로 표시되던 증상
   - WM - 신규 디스크 투입시 포맷을 강제하던 조건 제거


2.0.4 (2015.02.27)
----------------------------

**기능개선/정책변경**

   - :ref:`origin-balancemode` 의 Hash 알고리즘 변경

       | **Before**. hash(URL) / 서버대수
       | **After**. `Consistent Hashing <http://en.wikipedia.org/wiki/Consistent_hashing>`

   - :ref:`access-control-vhost` 를 통해 Redirect 할 때 클라이언트가 요청한 URI을 파라미터로 입력할 수 있다.

**버그수정**

   - 캐싱된 파일이 삭제되지 않아 디스크가 꽉 차던 증상


2.0.3 (2015.02.09)
----------------------------

**기능개선/정책변경**

   - DIMS 내재화 및 고도화
   - WM - 트래픽 관련 안내 메세지 추가

**버그수정**

   - WM - 신규 가상호스트 생성이 실패 하는 버그 수정


2.0.2 (2015.01.28)
----------------------------

   - 원본서버에 캐싱요청할 때 클라이언트가 보낸 User-Agent헤더 값을 보낼 수 있다.

**버그수정**

   - MDAT 길이가 1인 MP4파일의 Trimming이 되지 않던 증상
   - WM - 클러스터 내의 다른 서버 그래프가 표시되지 않던 증상
   - WM - 클러스터 내의 다른 서버들이 현재 서버로 보여지던 증상


2.0.1 (2014.12.30)
----------------------------

   - HitRatio그래프가 0으로 표시되던 증상


2.0.0 (2014.12.17)
----------------------------

   - 원본에서 다운로드된 크기만큼만 디스크 공간사용. (:ref:`origin-partsize` 참조)
   - :ref:`env-cache-resource` 기능추가
   - TLS 1.1 지원
   - AES-NI를 통해 :ref:`https-aes-ni` 지원
   - ECDHE 계열의 CipherSuite를 지원. (:ref:`https-ciphersuite` 참조)
   - :ref:`admin-log-dns` 추가
   - 원본서버가 Domain일 경우 각 IP별 TTL을 사용하도록 정책변경
   - 원본 :ref:`origin_exclusion_and_recovery` 추가
   - 원본 :ref:`origin-health-checker` 추가
   - :ref:`adv_topics_sys_free_mem` 추가
   - 기타

       | 최소 실행환경 변경. (Cent 6.2이상, Ubuntu 10.01 이상)
       | 설치 패키지에 NSCD데몬이 탑재
       | :ref:`media-dims` 기본 탑재
       | :ref:`getting-started-reset` 후 STON 재시작하도록 변경
       | <DNSBackup> 기능 삭제
       | <MaxFileCount> 기능 삭제
       | <Distribution> 기능 삭제. :ref:`origin-balancemode` 기능에 통합


v1.4.x
====================================

1.4.5 (2015.03.06)
----------------------------

**버그수정**

   - 캐싱된 파일이 삭제되지 않아 디스크가 꽉 차던 증상
   - STONR 이 간헐적으로 비정상 종료되는 증상


1.4.4 (2014.12.15)
----------------------------

**버그수정**

   - :ref:`media-dims` 처리시 404 Not Found로 응답되던 증상


1.4.3 (2014.12.10)
----------------------------

**버그수정**

   - FTP 클라이언트에서 업로드 경로가 길면 오동작하는 증상


1.4.2 (2014.12.08)
----------------------------

   - Purge(자동 복구) API가 HardPurge(복구 불가)로 동작하도록 :ref:`purge` 할 수 있다.
   - 로그 롤링시 압축하도록 설정 할 수 있다.
   - FTP 클라이언트 기능강화 - 전송시간, 경로, 삭제, 백업 기능 추가

**버그수정**

   - SSL/TLS Handshake과정 중 비정상 종료되던 증상


1.4.1 (2014.11.25)
----------------------------

   - 클라이언트가 보낸 URI를 가공없이 원본서버에 보내도록 :ref:`origin-wholeclientrequest` 할 수 있다.

**버그수정**

   - MP4영상에 SPS/PPS가 없을 때 비정상 종료되던 증상
   - FTP 클라이언트가 Active모드로 동작하지 않던 증상
   - WM - SNMP의 VhostMin, ViewMin을 0부터 설정가능하도록 수정 (기존 1부터)


1.4.0 (2014.11.12)
----------------------------

   - :ref:`getting-started-license` 도입
   - WM - 전용 포트분리 추가


v1.3.x
====================================

1.3.20 (2014.11.05)
----------------------------

   - [전역] 과부하관리 기능 추가. 설정된 최대 클라이언트(소켓) 수를 넘어가는 접근이 발생할 경우 클라이언트 접속 즉시 연결을 끊는다. 이는 솔루션과 플랫폼을 보호하기 위한 가장 강력한 조치이다. 전체 소켓이 일정비율 이하로 내려가면 다시 클라이언트 접근을 허용한다.
   - :ref:`https` 프로토콜(SSL3.0 또는 TLS1.0) 선택가능

**기능개선/정책변경**

   - :ref:`file-system` 에서 파일시간 제공방식 설정가능

     | **Before**. 로컬에 캐싱된 시간
     | **After**. 원본의 Last-Modified 시간

   - 쿠키관련 정책변경

     | **Before**. cookie 헤더를 제거한다.
     | **After**. cookie, set-cookie, set-cookie2 헤더를 제거한다. WM에서 경고메시지 강화

   - WM - 가상호스트 삭제시 삭제 될 가상호스트 이름 명시
   - WM - 설치시 cgi-bin경로에 어떤 파일도 설치하지 않도록 수정
   - WM - RRD 메모리 그래프의 Scale을 1000에서 1024로 변경

**버그수정**

   - :ref:`file-system` 에서 파일접근에 실패했을 경우 비정상종료될 수 있던 증상
   - WM - :ref:`origin-exclusion-and-recovery` 에서 Cycle과 값이 서로 바뀌어서 저장되던 증상


1.3.19 (2014.10.21)
----------------------------

**기능개선/정책변경**

   - :ref:`trimming` 정책변경

     | **Before**. 모든 트랙을 Trimming한다.
     | **After**. Audio/Video 트랙만을 Trimming한다. AllTracks속성을 통해 기존처럼 모든 트랙을 Trimming할 수 있다.


1.3.18 (2014.10.15)
----------------------------

**버그수정**

   - :ref:`media-dims` 처리에서 클라이언트가 보낸 QueryString이 반영되지 않던 증상
   - 원본서버가 모두 배제되었을 때 특정조건에서 캐싱파일이 초기화되지 않던 증상
   - WM - 보안정책 강화 및 가상호스트 이름에 공백이 들어가지 않도록 예외처리
   - WM - Unmount된 디스크의 상태를 올바르게 인식하지 못하던 증상


1.3.17 (2014.09.22)
----------------------------

**버그수정**

   - SNMPWalk를 통해 :ref:`cache-host-traffic-filesystem` 통계가 제공되지 않던 증상
   - WM을 통해 DIMS설정 시 해당 가상호스트의 :ref:`env-vhost-find` 가 초기화되던 증상


1.3.16 (2014.08.27)
----------------------------

**버그수정**

   - :ref:`file-system` 에서 getattr함수가 많이 호출되면 메모리가 정리되지 않던 증상 및 관련 통계 수정


1.3.15 (2014.08.25)
----------------------------

**버그수정**

   - 잘못된 SNMP 접근으로 인해 비정상 종료되던 증상


1.3.14 (2014.08.13)
----------------------------

   - 최대 사용 메모리를 제한하도록 :ref:`env-cache-resource` 할 수 있다.
   - SNMP - 허가된 Community외엔 접근이 불가능하도록 :ref:`community` 할 수 있다.
   - WM - 서비스 Listen포트를 멀티로 설정할 수 있다. 클러스터 전용포트를 설정할 수 있다.

**기능개선/정책변경**

   - 파일 인덱싱 정책 변경

     | **Before**. 완료된 파일만 인덱싱한다.
     | **After**. 다운로드 중인 파일도 인덱싱한다.

   - :ref:`emergency` 기본 값 OFF로 변경
   - 기본 Access로그에 sc-content-length필드 추가


1.3.13 (2014.07.21)
----------------------------

   - WM - "컨텐츠제어"에서 조회한 파일을 다운로드 할 수 있다.

**버그수정**

   - :ref:`file-system` 메모리 누수버그 수정


1.3.12 (2014.07.10)
----------------------------

**기능개선/정책변경**

   - :ref:`acl`, :ref:`bypass` - 복합조건을 설정할 때 결합(AND) 키워드를 "&"에서 " & "로 변경.

     | **Before**. $IP[AP]&!HEADER[referer] 표현가능
     | **After**. $IP[AP] & !HEADER[referer] 처럼 결합조건 사이에 반드시 공백필요

   - SNMP - bytesHitRatio 타입이 음수를 표현할 수 있도록 gauge32에서 integer로 변경
   - WM - 비대칭키 인증정책으로 변경

**버그수정**

   - 1MB보다 작은 MP4파일을 :ref:`media` 기능으로 서비스할 때 오동작하거나 비정상 종료되던 문제
   - 비정상 HTTP요청에 대한 예외처리 강화


1.3.11 (2014.06.19)
----------------------------

   - 마지막(=현재) 설정상태 확인(/conf/lastest) API 추가

**기능개선/정책변경**

   - :ref:`bypass` 개선

     | **Before**. 명시적인 URL 또는 Cookie등으로 바이패스(또는 예외) 설정
     | **After**. IP, Header, URL 또는 이를 결합한 복합조건으로 바이패스 가능. Cookie바이패스 삭제.

   - 클라이언트 트래픽 - 디렉토리 별 requestHitRaio 추가
   - WM - hostname과 IP가 로그인하지 않은 상태에서 표시되지 않도록 수정

**버그수정**

   - DNS가 Resolving응답을 정상적으로 주지만 주소가 없을 때 죽는 버그.
   - origin.log, filesystem.log 롤링할 때 파일명이 GMT시간으로 생성되던 증상. 로컬시간으로 생성되도록 수정.
   - /monitoring/hwinfo API에서 디스크 사용량이 표시되지 않던 증상
   - WM - 마지막 접근시간이 올바르게 표시되지 않던 증상


1.3.10 (2014.06.03)
----------------------------

   - 모든 Disk가 장애로 배제되었을 때 동작방식(재투입, Bypass, 종료)을 :ref:`storage` 할 수 있습니다.
   - 원본 HTTP요청의 Host헤더를 클라이언트가 보낸 값을 사용하도록 설정할 수 있습니다.

**기능개선/정책변경**

   - 파일캐싱 모니터링에서 QueryString 특수문자를 포함하는 URL도 모니터링할 수 있습니다.
   - :ref:`monitoring_stats` 에서 5분간 총 양이 함께 표기됩니다.
   - HTTP POST요청캐싱과 Bypass정책이 동시에 설정된 경우, 서비스 정책이 재정립되었습니다
   - Trimming정책 변경

     | **Before**. Trimming의 끝(end) 시간에 가장 인접하도록 분할
     | **After**. Trimming의 끝(end) 시간의 이전 Key-Frame으로 분할

**버그수정**

   - MP4파일이 서비스되지 않고 CPU를 점유하던 증상


1.3.9 (2014.05.21)
----------------------------

**기능개선/정책변경**

   - 서비스 거부 조건에서 응답코드를 설정할 수 있습니다.

     | **Before**. 에러 페이지에 "401 Access Denied"라고 명시
     | **After**. 별도의 페이지 없이 설정된 응답코드로만 응답

**버그수정**

   - 잘못된 MP4영상 :ref:`trimming` 중 비정상 종료되던 증상.
   - WM - Port바이패스 설정이 반영되지 않던 증상


1.3.8 (2014.04.30)
----------------------------

   - 로그가 롤링될 때 FTP로 전송하도록 설정할 수 있습니다.
   - Emergency모드가 발동하지 않도록 설정할 수 있습니다.
   - 원본서버의 ETag를 인식하도록 설정할 수 있습니다.
   - SNMP Community를 설정할 수 있습니다.
   - TTL적용 우선순위를 선택할 수 있습니다.
   - HTTP의 POST Method요청의 Body를 캐싱키로 인식/무시하도록 설정할 수 있습니다.

**버그수정**

   - HLS 변환 중 비디오가 깨지던 증상.
   - 강제로 TTL을 만료시킨 컨텐츠가 304 Not Modified로 인해 TTL이 다시 정해질 때 설정상 가장 큰 값이 할당되던 증상. 설정상 가장 작은 값이 할당되도록 수정.


1.3.7 (2014.04.11)
----------------------------

**버그수정**

   - domain.com:80 처럼 Port가 명시된 HTTP요청에 대해 가상호스트를 찾지 못하던 증상 (v1.3.4 ~ 1.3.6)
   - 잘못된 MP4영상분석 중 비정상 종료되던 증상


1.3.6 (2014.04.09)
----------------------------

   - Access.log를 Custom하게 설정할 수 있습니다.
   - View를 통해 가상호스트를 통합하여 모니터링 할 수 있습니다.
   - 컨트롤 API(Purge, Expire, HardPurge, ExpireAfter)의 대상이 없을 때 HTTP 응답코드를 설정할 수 있습니다.

**기능개선/정책변경**

   - 로그 롤링조건

     | **Before**. 시간 또는 크기 중 택1
     | **After**. 시간과 크기 동시설정 가능

   - WM - 페이지 상단에 서버의 호스트명과 IP를 보여줍니다.

**버그수정**

   - WM - 설정파일 중 CDATA로 저장된 문자열이 Plain Text로 바뀌던 증상


1.3.5 (2014.04.02)
----------------------------

**버그수정**

   - 변경된 설정 적용 중 CPU사용량이 높아지며 서비스가 정상동작하지 않던 증상
   - WM - 설정파일에 동일한 설정이 중복되어 표시되던 증상


1.3.4 (2014.03.26)
----------------------------

   - FileSystem 업그레이드

     | 미디어 기능(Trimming, HLS, DIMS등)이 HTTP와 동일하게 동작합니다.
     | XML/JSON, SNMP 상세통계가 추가 되었습니다.

   - 정규표현식을 사용한 URL전처리가 가능합니다.
   - 시스템(OS)의 TCP 소켓상태를 실시간으로 모니터링 합니다. 지표는 모두 RRD Graph로 제공됩니다.
   - 가상호스트가 포트를 Listen하지 않도록 설정할 수 있습니다.

**버그수정**

   - (FileSystem이 Mount되어 있을 때) STON의 정상종료가 오래 걸리던 증상
   - WM - (FileSystem을 사용하지 않는 환경에서) 신규 가상호스트 추가시 FileSystem페이지 활성화되던 증상
   - WM - 클러스터링 구성 중 대상 WM이 한번도 실행되지 않았었다면 설정이 적용되지 않던 증상


1.3.3 (2014.03.19)
----------------------------

**버그수정**

   - 갱신중인 파일을 MP4 Trimming으로 서비스 할 때 간헐적으로 비정상 종료되던 증상


1.3.2 (2014.03.05)
----------------------------

   - WM을 통해 최신버전으로 업데이트 할 수 있습니다.
   - STON의 설치/업그레이드 시 진행상황을 install.log에 기록합니다.

**버그수정**

   - 불완전한(=실시간으로 변환 중인) MP4 파일 캐싱 중 서비스가 멈추던 증상
   - WM에서 클러스터 전체 적용 시 가상호스트 파일이 초기화되던 증상


1.3.1 (2014.02.24)
----------------------------

**버그수정**

   - MP4 파일 서비스 중 비정상 종료될 수 있던 증상
   - :ref:`caching` 기간 이외의 설정이 삭제되지 않던 증상


1.3.0 (2014.02.20)
----------------------------

   - :ref:`filesystem` 추가 - STON을 Linux VFS(Virtual File System)에 Mount합니다. 원본서버의 모든 파일을 로컬 파일 I/O로 사용할 수 있습니다.
   - :ref:`caching` 추가 - 설정이 변경될 때마다 전체설정을 기록합니다. API(목록, 롤백, 다운로드, 업로드)와 SNMP를 통해 열람, 다운로드, 업로드, 복원이 가능합니다.
   - MP4HLS 추가 - 단일 MP4파일을 HLS(Http Live Streaming)으로 전송할 수 있습니다.
   - 통계 추가 - 전송 중 원본서버에서 먼저 소켓을 종료시킨 횟수

**기능개선/정책변경**

   - :ref:`snmp-var`

     | **Before**. 가상호스트가 삭제되거나 순서가 변경될 경우 [vhostIndex]가 재조정된다. 예를 들어 A(1), B(2), C(3)에서 B가 삭제된 경우 A(1), C(2)로 재조정된다.
     | **After**. [vhostIndex]를 기억한다. 예를 들어 A(1), B(2), C(3)에서 B가 삭제되더라도 A(1), C(3)을 유지한다. 신규 가상호스트가 추가되면 비어있는 [vhostIndex]를 가진다. 예를 들어 가상호스트 D가 추가되면 A(1), D(2), C(3)로 재조정된다.

   - 설정 리로드 API 변경

     | **Before**. /conf/reloadall, /conf/reloadserver, /conf/reloadvhosts가 별도로 존재하며 기능을 달리한다.
     | **After**. /conf/reload로 일괄통일한다. 하위 호환성을 위해 기존 API를 유지한다.


v1.2.x
====================================

1.2.14 (2014.02.06)
----------------------------

**기능개선/정책변경**

   - 원본주소 DNS 정책 변경

     | **Before**. 다른 가상호스트지만 원본주소로 같은 Domain을 사용한다면 Domain Resolving결과를 공유한다.
     | **After**. 모든 가상호스트는 독립적으로 Domain Resolving을 수행하며 공유하지 않는다.

**버그수정**

   - WM을 통한 Disk Hot-Swap 오동작 수정.


1.2.13 (2014.01.22)
----------------------------

**버그수정**

   - 간헐적으로 응답이 지연되거나 전송되지 않던 동작 수정.


1.2.12 (2014.01.02)
----------------------------

**버그수정**

   - 최신 NEXUS 기기에서 Trimming된 MP4/M4A가 재생되지 않던 증상 수정. (에러 메세지: The player doesn't support this type of audio file.)


1.2.11 (2013.12.20)
----------------------------

**기능개선/정책변경**

   - 원본서버 Cache-Control 헤더 인식정책 변경

     | **Before**. no-cache 또는 max-age만을 인식한다.
     | **After**. no-cache, no-store, no-transform, must-revalidate, proxy-revalidate, private, max-age를 구분하여 인식한다. custom은 무시한다.

   - 5분 평균 Request Hit율 계산방식 변경

     | **Before**. 각 TCP_XXX의 (단위 시간에 대한)평균을 구한 뒤 Hit율 계산한다. 각 평균 값이 단위 시간보다 작을 때 누락될 수 있다.
     | **After**. (평균을 내지 않고) 비율로만 계산하여 값이 누락되지 않는다.


1.2.10 (2013.12.13)
----------------------------

**기능개선/정책변경**

   - HTTPS 통신에서 Access로그 범위 변경

     | **Before**. 클라이언트가 SSL Server Finished 패킷을 온전히 수신한 HTTPS 트랜잭션만을 Access로그에 기록한다.
     | **After**. 클라이언트가 SSL Server Finished 패킷을 온전히 수신하지 못했더라도 HTTP Request 패킷을 보냈다면 Access로그에 기록한다.

**버그수정**

   - 비정상 종료(물리적 세션 손실)된 HTTPS세션이 재사용될 때 이전에 요청되었던 컨텐츠와 현재 요청된 컨텐츠를 동시에 처리하던 증상. 2개의 HTTP 요청이 동시에 처리될 수 있으며 이를 항상 현재 요청한 요청만이 유효하도록 수정.


1.2.9 (2013.12.09)
----------------------------

**기능개선/정책변경**

   - Bandwidth-Throttling

     | **Before**. Boost 시간동안 미디어를 전송할 때 헤더를 포함한다. 헤더가 클 경우 미디어 데이터가 전송되지 않아 버퍼링이 발생할 수 있다.
     | **After**. 미디어 헤더는 대역폭 제한없이 전송한다. 헤더 전송이 완료된 후 Boost 시간이 시작된다.

**버그수정**

   - WM 포트 변경 후 STON 업데이트 시 변경된 포트가 유지되지 않던 증상


1.2.8 (2013.11.14)
----------------------------

**기능개선/정책변경**

   - 접속하는 HTTP 클라이언트마다 고유번호(session-id)를 부여합니다. session-id는 Access로그와 Origin로그에 추가되어 연관성을 유추할 수 있습니다.
   - API호출의 파라미터로 https://... 형식을 인식합니다.

**버그수정**

   - Content-Disposition헤더가 HTTP 응답에 2번 표시되던 증상
   - Bandwidth-Throttling설정이 OFF일 때 Trimming이 동작하지 않던 증상
   - WM계정에 특수문자(&)사용시 로그인 안되던 증상


1.2.7 (2013.10.17)
----------------------------

   - HTTP Connection헤더를 설정할 수 있습니다.
   - HTTP Keep-Alive헤더를 설정할 수 있습니다.

**기능개선/정책변경**

   - HTTP 응답에 Connection헤더와 Keep-Alive헤더를 기본으로 설정합니다.


1.2.6 (2013.10.14)
----------------------------

   - 원본서버의 "Server" 헤더를 클라이언트에게 전달하도록 설정할 수 있습니다.


1.2.5 (2013.10.10)
----------------------------

   - Origin By Client를 설정할 수 있습니다.

**기능개선/정책변경**

   - 인식할 수 있는 미디어파일에 대해 동적으로 Bandwidth-Throttling의 Bandwidth를 설정할 수 있습니다. v1.2.4까지 존재했던 Media.Pacing은 이 기능에 포함되면서 삭제되었습니다.

**버그수정**

   - 극히 드물게 잘못된 문자열 참조 오류로 인해 비정상종료되던 증상


1.2.4 (2013.09.27)
----------------------------

   - Bandwidth-Throttling을 통해 전송 대역폭을 다양하게 설정할 수 있습니다.

     | Warning: 다음 버전에서 Media.Pacing은 Bandwidth-Throttling에 통합될 것입니다. 미디어 파일(현재 MP3, MP4, M4A 지원)의 Bitrate를 Bandwidth-Throttling에서 인식할 수 있는 형태가 될 것입니다. 현재는 기존 기능인 Media.Pacing이 더 우선하도록 개발되어 있습니다.

   - 가상호스트별로 클라이언트 최대 Bandwidth를 제한하도록 설정할 수 있습니다.
   - 헤더가 뒤에 있는 M4A파일을 헤더를 앞으로 옮겨서 서비스하도록 설정할 수 있습니다.
   - M4A파일을 원하는 구간만큼 잘라내어 서비스하도록 설정할 수 있습니다.

**기능개선/정책변경**

   - 가상호스트 AccessControl 조건에 해당하는 클라이언트 요청에 대해 Redirect(302 moved temporarily)로 응답하도록 접근을 제어할 수 있습니다. HIT율은 TCP_REDIRECT_HIT로 별도로 수집됩니다.
   - TCP_REDIRECT_HIT가 모든 통계에 추가되었습니다.
   - 가상호스트 AccessControl 조건을 AND로 결합하도록 설정할 수 있습니다.

**버그수정**

   - 클러스터가 구성되지 않던 증상 - IP를 추출할 때 Loopback이 추출되던 증상


1.2.3 (2013.09.05)
----------------------------

   - DIMS(Dynamic Image Management System) - 원본서버의 이미지를 가공(잘라내기, 썸네일생성, 크기변경, 포맷변경, 품질조절, 합성)하도록 설정할 수 있습니다.
   - MP3파일을 원하는 구간만큼 잘라내어 서비스하도록 설정할 수 있습니다.
   - 특정 IP만 Listen하도록 설정할 수 있습니다.
   - [WM] 신규 가상호스트를 생성할 때 기존 가상호스트를 선택해 복사할 수 있습니다.
   - [WM] 가상호스트에서 DIMS를 설정할 수 있습니다.

**기능개선/정책변경**

   - 원본세션을 재사용하지 않도록 설정할 수 있습니다.

**버그수정**

   - MP4 Trimming 중 비정상 종료되던 증상
   - 콘솔에서 수정한 가상호스트 설정이 WM의 클러스터에 반영되지 않던 증상


1.2.2 (2013.08.16)
----------------------------

   - HTTP Post 요청을 캐싱하도록 설정할 수 있습니다.
   - STON이 서비스를 감당할 수 없는 상태에 Emergency로 전환된다.

**기능개선/정책변경**

   - 서비스 허용/차단 조건에 부정(!IP, !HEADER, !URL)조건이 추가되었습니다.
   - WM과 콘솔에서 동시에 설정을 변경할 때 WM에서 콘솔에서 변경한 내용을 인식하도록 변경되었습니다.
   - WM에서 IE의 "호환성 보기" 메뉴를 숨기도록 변경되었습니다.

**버그수정**

   - CPU 과부하 상태에서 바이패스 세션이 정상적으로 정리되지 않아 비정상 종료되던 증상
   - (vary 설정에서) 원본서버에서 200 OK로 응답하지 않는 컨텐츠 서비스 중 비정상 종료되던 증상
   - 가상호스트명과 Alias가 같은 경우 Alias를 제거했을 때 가상호스트를 찾을 수 없던 증상
   - WM 클러스터에 설정이 반영되지 않던 증상


1.2.1 (2013.07.26)
----------------------------

   - MP4파일을 원하는 구간만큼 잘라내어 서비스하도록 설정할 수 있습니다.
   - 원본서버에서 컨텐츠를 최초로 캐싱하거나 갱신할 때 Range요청을 하도록 설정할 수 있습니다.

**버그수정**

   - WM에서 클러스터가 구성되지 않던 증상
   - 로그설정 변경 후 "/conf/reloadserver" API를 호출했을 때 반영되지 않던 증상
   - SNMP에서 Host평균 통계가 평균이 아닌 합으로 계산되던 증상
   - 특정 상황에서 클라이언트 트래픽 통계수치가 비정상적으로 높게 계산되던 증상


1.2.0 (2013.07.01)
----------------------------

   - WM이 추가되었습니다. 모든 설정이 WM을 통해 가능하며 MRTG(5종류 - 대쉬보드/5분/30분/2시간/1일)가 최대 18개월치 제공됩니다. WM을 통해 STON을 클러스터로 묶어서 쉽게 관리할 수 있습니다.
   - Graph API가 추가되었습니다.
   - 원본서버의 Vary헤더를 인식하도록 설정할 수 있습니다.
   - 클라이언트와 통신하는 HTTP 요청/응답 헤더를 변경하도록 설정할 수 있습니다.
   - 원본서버의 모든 헤더를 클라이언트에게 전달하도록 설정할 수 있습니다.
   - 원본서버에서 Redirect된 컨텐츠를 추적하여 캐싱하도록 설정할 수 있습니다.
   - 특정 URL에 대해서만 QueryString을 인식 또는 무시 하도록 설정할 수 있습니다.
   - 매니저 포트 ACL마다 접근권한을 설정할 수 있습니다.
   - 로그를 ON/OFF하도록 설정할 수 있습니다.
   - 로컬통신의 로그를 기록하지 않도록 설정할 수 있습니다.
   - 로컬통신의 통계를 수집하지 않도록 설정할 수 있습니다.

**기능개선/정책변경**

   - 로그 Trace접근이 있을 때 로그에 기록합니다.
   - 하드웨어 정보를 조회할 때 CPU를 높게 사용하던 증상이 개선되었습니다.


v1.1.x
====================================

1.1.17 (2013.05.27)
----------------------------

   - Origin By Client를 설정할 수 있습니다.

**기능개선/정책변경**

   - Transfer-Encoding으로 전송된 컨텐츠를 (전송지연 등의 이유로) 온전하게 캐싱하지 못한 경우 클라이언트 서비스정책 변경

     | **Before**. 캐싱에 실패한 현재 컨텐츠를 서비스
     | **After**. 이전에 온전하게 캐싱된 컨텐츠가 있다면 이전 컨텐츠로 서비스. 없다면 500 Internal Error.

**버그수정**

   - RefreshExpired가 OFF인 상태에서 PartSize가 0보다 크게 설정된 경우 컨텐츠 갱신이 안되는 증상


1.1.16 (2013.05.15)
----------------------------

**기능개선/정책변경**

   - 리눅스 최대 파일개수 제한으로 File I/O가 실패하지 않도록 파일저장방식 변경
   - 정상동작을 위해 필요한 서브파일 점검 로그 추가

**버그수정**

   - 갱신중인 파일이 HardPurge될 때 비정상 종료되던 증상
   - 가상호스트별로 미디어 설정이 되지 않던 증상
   - syslog 설정이 리로드되지 않던 증상
   - OriginError로그에 syslog설정시 Info로그에 Inactive로 표시되던 증상


1.1.15 (2013.04.29)
----------------------------

   - CPU 성능지표(Nice, IOWait, IRQ, SoftIRQ, Steal) 통계 추가

**버그수정**

   - Track정보가 많은 MP4파일 분석 중 비정상 종료되던 증상
   - HTTP Transfer-Encoding된 컨텐츠를 전송할 때 지연되던 증상


1.1.14 (2013.04.10)
----------------------------

   - SNMP에 전체 "가상호스트의 합"이 추가되었습니다.

**기능개선/정책변경**

   - (파일이 없을 때) GeoIP파일목록 조회 결과 변경

     | **Before**. 404 NOT FOUND
     | **After**. 200 OK ("files": [] 응답)

**버그수정**

   - SSLv3에서 RSA_WITH_3DES_EDE_CBC_SHA로 Handshake가 되지 않던 증상 수정
   - Https에 빈 문자열 입력 시 오동작하던 증상


1.1.13 (2013.03.29)
----------------------------

**버그수정**

   - 디렉토리별 통계가 설정된 상태에서 누적통계가 OFF인 경우 비정상 종료되던 증상
   - 처음 접근되는 컨텐츠가 원본서버로부터 응답을 받기 전에 Purge되는 경우 클라이언트에게 응답을 주지 않던 증상
   - HTTP 요청의 URI가 상대주소가 아니라 절대주소일 경우 서비스 안되던 증상


1.1.12 (2013.03.27)
----------------------------

   - No-Cache요청이 올 경우 요청된 컨텐츠를 즉시 만료시키도록 설정할 수 있습니다.
   - CentOS 패키지로 openSUSE에서 설치할 수 있습니다.

**기능개선/정책변경**

   - No-Cache요청 인식조건 변경

     | **Before**. "pragma: no-cache" 또는 "cache-control: no-cache"
     | **After**. 기존 조건에 "cache-control: max-age=0" 추가

**버그수정**

   - DNS갱신시 비정상 종료되던 증상
   - 최대 파일개수를 넘어갈 때 URL에 Vertical Bar(|)가 있는 파일들이 삭제되지 않던 증상
   - HTTP 요청이 바이패스 될 때 HttpReqBodySize와 ClientInbound 값이 정확하지 않던 증상


1.1.11 (2013.03.21)
----------------------------

   - Disk 장애조건을 설정할 수 있습니다. 장애로 판단된 디스크는 자동배제됩니다.
   - Disk HotSwap용(실행 중 디스크 교체) API가 추가되었습니다.
   - 로그를 syslog로 전송하도록 설정할 수 있습니다.
   - 원본서버에서 한번에 다운로드 받는 컨텐츠 크기를 설정할 수 있습니다.
   - GeoIP 파일목록 조회 API가 추가되었습니다.
   - FAQ에 "멀티 도메인에 대한 SSL구성은?" 이 추가되었습니다.

**기능개선/정책변경**

   - 원본서버 장애코드 변경

     | **Before**. 숫자로 표시
     | **After**. 읽기 쉬운 형식으로 표시(Connect-Timeout, Receive-Timeout, Server-Close)

   - 원본서버 장애로그 기록시 주석으로 에러상황을 기록하던 것 제거. OriginErrorLog로 통합.

**버그수정**

   - Manager Port변경 후 Reload할 때 비정상 종료되던 버그 수정


1.1.10 (2013.03.07)
----------------------------

   - 가상호스트마다 접근/차단조건(IP, GeoIP, URI, Header)을 설정할 수 있습니다. 관련 통계가 추가되었습니다.
   - 도메인 Resolving이 실패할 경우 최근 사용된 IP들을 모두 사용하여 원본서버 부하를 분산하도록 설정할 수 있습니다.
   - 모니터링 API가 추가되었습니다.

     | 가상호스트 목록 조회
     | 하드웨어 정보 조회
     | HTTPS CipherSuite 조회
     | 접근차단 조건(acl.txt) 조회
     | Expires헤더 조건(expires.txt) 조회

**기능개선/정책변경**

   - 로그 디스크 여유공간이 부족해질 경우 정책 변경

     | **Before**. 개입하지 않음. 관리자가 명시적으로 삭제해야 함.
     | **After**. Access로그만을 삭제. 만약 현재 사용 중인 로그를 지워야하는 상황이라면 새로운 로그 생성 후 삭제함.

   - STON 종료 후 (vhosts.xml에서)삭제된 가상호스트 파일들에 대한 정책 변경

     | **Before**. 개입하지 않음. 관리자가 명시적으로 삭제해야 함.
     | **After**. 디스크 여유공간이 부족해지면 우선적으로 삭제.

   - (가상호스트 별) 재구동 시 정상적으로 로딩되지 않은 디스크의 파일들에 대한 정책 변경

     | **Before**. 서비스 중 자연히 덮어씌워지도록 남겨둠
     | **After**. 해당 디스크를 신뢰할 수 없다고 판단하여 모두 무효화. 클린업 시간 또는 디스크 여유공간 부족 시점에 모두 삭제.

   - 도메인 Resolving결과 조회 API 변경.

     | **Before**. /dns/list
     | **After**. /monitoring/dnslist

   - 로그 트레이스 API 변경

     | **Before**. /logtrace/...
     | **After**. /monitoring/logtrace/...

   - 도메인 Resolving결과에 백업된 IP목록 추가


1.1.9 (2013.02.27)
----------------------------

   - mod_expires와 같이 Expires헤더를 설정할 수 있습니다.
   - HTTPS의 CipherSuite를 설정할 수 있습니다.
   - 파일을 관리(Purge/Expire/HardPurge/ExpireAfter)할 때 단일 URL만 입력하여도 QueryString까지 모두 관리하도록 설정할 수 있습니다.
   - ETag헤더 표시여부를 설정할 수 있습니다.
   - Age헤더 표시여부를 설정할 수 있습니다.

**기능개선/정책변경**

   - HTTPS CipherSuite가 추가되었습니다.

     | RSA_WITH_RC4_MD5
     | TLS_RSA_WITH_3DES_EDE_CBC_SHA

   - 숫자(초=sec)로만 하던 표현을 인식하기 쉬운 문자형식으로 표현가능

     | **Before**. /image/ad.jpg, 1800
     | **After**. /image/ad.jpg, 6 hours

   - SNMP에서 평균으로만 제공하던 수치를 누적으로 제공 (클라이언트/원본)

     | 기존에 Count라는 표현을 Average로 변경. Average는 시간으로 나눈 평균을 의미
     | 시간동안 집계된 전체 수는 Count로 표현
     | 전체 요청/응답 개수 추가
     | 응답코드별 응답/완료 개수 추가
     | Request Hit Count 추가

   - 재시작/종료/캐시초기화 API를 호출할 때 "확인" 과정없이 호출할 수 있습니다.
   - 시스템 Load Average - 1분/5분/15분 통계추가
   - 모든 가상호스트의 원본서버를 초기화 할 수 있습니다.

**버그수정**

   - Domain Resolving결과가 변경되었을 때 여러 가상호스트에 동시에 반영이 안되던 버그 수정
   - Purge/Expire에서 QueryString이 붙어있는 URL이 처리안되던 버그 수정


1.1.8 (2013.02.21)
----------------------------

   - 클라이언트의 요청이 항상 같은 원본서버로 바이패스되도록 설정할 수 있습니다.
   - 도메인 Resolving결과를 모니터링 할 수 있습니다.
   - 도메인 Resolving결과가 업데이트되었을 때 Info로그에 기록하도록 설정할 수 있습니다.
   - 원본서버 사용 및 배제/복구 상황을 초기화 할 수 있습니다.
   - Clean-up 시간에 일정 기간동안 접근되지 않은 컨텐츠들을 삭제하도록 설정할 수 있습니다.
   - Clean-up을 수행하는 API가 추가되었습니다.

**기능개선/정책변경**

   - Origin 로그강화

     | 접속한 포트 기록
     | Bypass와 PrivateBypass구분 가능
     | 원본서버가 보낸 Content-Encoding 헤더 기록

   - Access 로그강화

     | 클라이언트가 보낸 Accept-Encoding헤더 기록
     | Bypass와 PrivateBypass구분 가능

   - 원본서버가 도메인명으로 설정되어 있을 때 기능개선

     | Resolving결과가 즉시 반영.
     | IP들에 대하여 개별로 배제/복구.

   - Purge/Expire/HardPurge/ExpireAfter 호출결과 응답코드 수정

     | 정상. 200 OK
     | 가상호스트 없음. 502 BAD GATEWAY
     | 잘못된 규격. 400 BAD REQUEST

   - FAQ페이지 업데이트

     | 원본서버 사용/배제/복구 정책은?
     | 디스크 여유공간은 어떻게 보장되나요?

**버그수정**

   - 디스크 공간이 부족해도 공간확보가 되지 않던 버그 수정


1.1.7 (2013.02.16)
----------------------------

**기능개선/정책변경**

   - Cent OS 5.5이상과 Ubuntu 10이상에서 동시접속 소켓이 10만을 넘으면 시스템 성능이 저하되며 소켓처리가 실패되는 증상을 확인하였습니다. 그러므로 최대 소켓을 10만으로 제한합니다.

**버그수정**

   - 사용 중인 소켓이 설정된 최대 소켓수를 넘어갔을 때 증설되지 않던 버그 수정
   - Byte Hit Ratio결과가 부정확하게 표시되던 버그 수정
   - 누적통계 XML에서 ClientSession이 2번 나오던 버그 수정. (ClientActiveSession으로 변경)
   - "abc*"로 패턴 설정했을 경우 "abc"처럼 패턴부분이 빈 문자열에 대해 인식하지 못하던 버그 수정


1.1.6 (2013.01.30)
----------------------------

   - 원본서버가 멀티로 구성되어 있을 때 항상 서버마다 동일하게 요청하도록 설정한다.

**기능개선/정책변경**

   - 원본서버 부하분산 정책이 Session에서 RoundRobin으로 변경되었습니다.
   - 전역로그(Info, Deny, OriginError)를 시간으로 롤링시킨다.

     | **Before**. 크기로만 롤링가능(Size속성만 존재)
     | **After**. 시간/크기로 롤링가능 (Size속성 제거. Type, Unit속성 추가)

   - 잘못된 형식 또는 존재하지 않는 가상호스트를 대상으로 Purge/Expire/ExpireAfter/HardPurge 호출시 응답코드 변경

     | **Before**. 200 OK
     | **After**. 400 BAD REQUEST 또는 404 NOT FOUND


**버그수정**

   - v1.1.5에서 원본서버 주소목록을 변경하고 리로드하였을 때 간헐적으로 비정상종료되던 증상
   - 원본서버에서 트랜잭션 완료 횟수를 수집할 때 Content-Length가 0인 응답이 누락되던 증상


1.1.5 (2013.01.28)
----------------------------

   - 클라이언트마다 바이패스 전용세션을 사용하도록 설정합니다. GET요청과 POST요청을 별도로 설정할 수 있습니다.
   - 클라이언트 Cookie헤더에 따라 바이패스하도록 설정합니다.

**기능개선/정책변경**

   - 원본서버 주소가 빠졌을 때 동작방식 변경

     | **Before**. 이미 연결되어 있다면 재사용한다.
     | **After**. 즉시 재사용하지 않는다.

   - QueryString을 구분하도록 설정되었을 때 Purge/Expire동작방식 변경.

     | **Before**. 입력된 URL과 해당 URL에 QueryString이 붙은 컨텐츠 Purge/Expire
     | **After**. 입력된 URL만 Purge/Expire

   - Active세션 산출방식 변경

     | **Before**. 통계를 뽑는 시점에 데이터 전송이 이루어지고 있는 세션
     | **After**. 데이터 전송이 발생한 Unique한 세션

   - 통계/성능 데이터가 추가/삭제되었습니다.

     | System 통계 추가
     | 종합통계에 요청회수, Active세션 통계 추가
     | SSL클라이언트 세션 수 삭제


1.1.4 (2013.01.17)
----------------------------

   - HTTPS를 IP와 Port로 다르게 바인딩할 수 있습니다.

**기능개선/정책변경**

   - 64GB장비에서 Free메모리 정책이 16GB로 변경되었습니다. (이전: 8GB)
   - HTTP Method를 서비스 포트(80)로 호출할 수 있습니다.
   - 전역설정(server.xml)의 HTTPS설정이 변경되지 않았어도 리로드할 때 인증서파일이 변경되었다면 반영합니다


1.1.3 (2013.01.15)
----------------------------

**기능개선/정책변경**

   - 한번에 기록할 수 있는 로그의 최대 크기를 10MB로 확장(이전: 2KB)
   - POST로 보낼 수 있는 URL크기를 최대 1MB로 확장(이전: 10KB)

**버그수정**

   - 로그가 시간기준으로 롤링될 때 파일명(날짜)이 정확하지 않던 증상


1.1.2 (2013.01.14)
----------------------------

   - GeoIP로 접근제어가 가능합니다. 클라이언트가 접속할 때 국가코드로 접속을 차단할 수 있습니다.
   - 접근차단된 IP를 deny.log에 기록합니다.
   - 로그를 동적으로 변경할 수 있습니다.
   - Access로그에 캐시 HIT결과(TCP_HIT, TCP_MISS, ...) 추가
   - 관리용 HTTP Method가 추가되었습니다.
   - POST를 사용하여 PURGE, HARDPURGE, EXPIRE, EXPIREAFTER할 수 있습니다.
   - stonapi를 통해 전체/일부 도메인을 초기화할 수 있습니다.
   - API목록을 열람하는 Help 명령어 추가

**기능개선/정책변경**

   - ETag헤더를 제공할 때 따옴표("...")로 묶어서 표기
   - HIT율 계산식 변경

     | **Before**. 즉시응답 / 모든응답
     | **After**. (TCP_HIT + TCP_IMS_HIT + TCP_REFRESH_HIT + TCP_REF_FAIL_HIT + TCP_NEGATIVE_HIT) / 모든 응답

   - 통계/성능 데이터가 추가/삭제되었습니다.

     | 평균통계에 통계를 생성한 날짜/시간 추가
     | 클라이언트에서 STON으로 접속/종료하는 통계 추가
     | STON이 원본서버로 접속/종료하는 통계 추가
     | System 추가
     | "Cached" 통계 제거

   - 정규표현식 성능향상 (X 20)
   - fileinfo에서 미캐싱파일인 경우 status를 "OK"에서 "NOT_CACHED"로 변경"

**버그수정**

   - SNMP에서 디스크정보(diskInfoPath, diskInfoStatus)를 얻을 때 Disk개수보다 큰 값이 diskIndex로 입력되면 비정상 종료되던 증상
   - 디스크가 꽉 차기전에 삭제되지 않던 증상. 디스크 Available공간을 남은공간으로 이해하도록 수정
   - stonapi가 관리포트를 인지하지 못하던 증상
   - Info로그에 "Download-Range" 메시지 제거


1.1.1 (2012.12.24)
----------------------------

   - 모든 가상호스트의 원본서버 이상동작을 하나의 파일(originerror.log)로 기록한다.
   - HTTP Multi-Range요청을 처리할 수 있습니다.
   - 원본서버에서 no-cache로 응답하더라도 클라이언트에게는 max-age를 주도록 TTL을 설정할 수 있습니다.

**기능개선/정책변경**

   - Accept-Encoding처리 정책변경.

     | **Before**. 클라이언트와 원본서버의 압축이 호환되지 않으면 500에러로 응답한다.
     | **After**. 클라이언트와 원본서버의 압축이 호환되지 않더라도 원본서버의 응답을 보낸다.

   - 다음과 같이 통계/성능 데이터가 추가되었습니다.

     | 원본/클라이언트 Active세션수가 추가되었습니다.
     | STON이 사용하는 CPU(Kernel, User) 성능수치가 추가되었습니다.

**버그수정**

   - (설정: TTL=0, RefreshExpired=ON) 원본파일이 변경되었을 때 변경된 파일의 첫 응답코드를 500으로 보내던 증상


1.1.0 (2012.12.17)
----------------------------

   - 가상호스트별로 최대 Outbound를 제한하도록 설정할 수 있습니다.
   - 헤더가 뒤에 있는 MP4파일을 헤더를 앞으로 옮겨서 서비스하도록 설정할 수 있습니다.
   - MP4를 Bitrate 만큼 낮은 대역폭으로 전송하도록 설정할 수 있습니다.
   - 최대 서비스 파일개수를 설정할 수 있습니다.
   - 최대 HTTP 세션 수를 설정할 수 있습니다.
   - API의 모든 함수를 리눅스 콘솔에서 호출할 수 있습니다.
   - Log-Trace API를 통해 기록되는 로그를 실시간으로 받아볼 수 있습니다.
   - 쉘에서 STON을 업데이트할 수 있습니다.

**기능개선/정책변경**

   - 메모리 정책이 수정되었습니다. 최대 파일개수와 최대 소켓개수를 설정하여 컨텐츠 메모리크기를 조절할 수 있습니다.
   - 도메인을 리졸빙(Resolving)한 결과를 캐싱합니다. 최소 1초, 최대 10초동안 캐싱됩니다.
   - OriginOptions의 일부설정(user-agent, host, WL-Proxy-Client-IP, xff-x-forwarded-for)을 바이패스되는 HTTP요청에 선택적으로 적용할 수 있습니다.
   - 원본서버로부터 5xx계열의 응답코드가 캐싱된 경우 TTL이 만료되면 RefreshExpired가 OFF라도 항상 원본서버에서 갱신여부를 확인하고 서비스합니다.
   - 원본서버에 example.com/dir1 처럼 디렉토리명을 같이 지정할 수 있습니다. 클라이언트가 /test.jpg로 요청한다면 원본서버로 요청하는 주소는 example.com/dir1/test.jpg가 됩니다.
   - 파일캐싱 모니터링 항목이 강화되었습니다.
   - 원본서버 주소가 도메인명이라면 별도로 <Host>를 설정하지 않아도 도메인 명으로 Host헤더를 보내도록 수정하였습니다.
   - 다음과 같이 통계/성능 데이터가 추가되었습니다.

     | 원본/클라이언트 HTTP요청 개수가 통계에 추가되었습니다.
     | 정상적으로 완료된 원본/클라이언트 HTTP 트랜잭션의 통계가 추가되었습니다.
     | CPU와 Memory에 대한 통계가 추가되었습니다.
     | Disk별 성능지표가 추가되었습니다.
     | 원본로그에 cs-acceptencoding, sc-cachecontrol필드가 추가되었습니다.

**버그수정**

   - 원본서버 배제/복구 과정(주소 3개 이상)에서 후순위의 원본서버가 우선 복구됐을 때 비정상 종료되던 증상
   - HTTP 요청에서 헤더가 키와 값 사이에 공백이 없으면 해석하지 못하던 증상
   - 로그를 "Size"로 설정했을 때 중간파일이 먼저 롤링되어 삭제되던 증상
   - 다음 상황에서 응답을 주지 않던 증상

     | A파일을 원본서버에 요청하였으나 404 Not Found가 발생
     | Memory Swap과정 중 A파일의 Body를 Memory에서 삭제 (A파일은 Meta만 존재하는 상태가 됨)
     | A파일 서비스 요청이 들어옴
     | A파일이 서비스를 위해 Body를 Load하려고 하였으나 실패함. 파일 초기화 수행
     | A파일이 원본서버로 다운로드를 진행하려고 하였으나 원본서버 배제로 실패함
     | 이후 A파일은 초기화 시점을 잃어버리고 초기화 상태로 존재함

   - 다음 상황에서 Expire/Purge가 성공된 것처럼 나오고 갱신되지 않던 증상

     | A파일을 백그라운드로 갱신 시도함
     | 원본서버에서 HTTP응답을 받았으나 전송지연이 발생함
     | 전송지연으로 연결이 종료되거나 세션이 비정상 종료됐을 때 갱신실패가 제대로 정리되지 않는 상황이 발생함


v1.0.x
====================================

1.0.17 (2012.11.29)
----------------------------

   - HardPurge API가 신규로 추가되었습니다. HardPurge한 컨텐츠는 완전삭제를 의미하며 복구가 불가능합니다.
   - 가상호스트별로 클라이언트 Keep-Alive시간을 설정할 수 있습니다.



1.0.16 (2012.11.28)
----------------------------

   - SNMPWalk가 동작하도록 SNMP의 기능이 전체적으로 수정되었습니다.

     | SNMP의 [min]변수의 기본 값을 설정할 수 있습니다. SNMPWalk는 설정 값을 참조하여 [min]변수를 설정합니다.
     | 전체 가상 호스트이름을 붙여서 제공하던 설정(VHostList)이 삭제되었습니다.
     | 일부 OID값이 확장가능하도록 재조정되었습니다.

   - 루트(/) 디렉토리에 대한 Purge/Expire를 막도록 설정할 수 있습니다.


1.0.15 (2012.11.22)
----------------------------

   - 정상적으로 캐싱(200 OK)되어 있는 파일을 갱신하는 과정에서 원본서버로부터 4xx응답을 받았을 때 마치 304 not modified를 받은 것처럼 동작하도록 설정합니다. 이를 통해 서버의 일시적인 장애로부터 컨텐츠를 갱신하는 행위를 방지할 수 있습니다.
   - 컨텐츠의 만료시간을 강제로 지정하는 ExpireAfter API가 추가되었습니다.
   - 원본서버 주소에 포트가 같이 선언되어 있는 경우 포트바이패스가 되지 않던 문제가 수정되었습니다.
   - 누적통계가 ON인 상황에서 포트바이패스 통계를 집계하면 비정상 종료되던 문제가 수정되었습니다.


1.0.14 (2012.11.15)
----------------------------

   - 디렉토리별 통계를 설정했을 때 통계 모니터링 중 비정상종료 될 수 있는 문제가 수정되었습니다.
   - 커스텀 TTL 변경이 적용되지않던 증상이 수정되었습니다. 커스텀 TTL은 즉각적으로 반영되지 않고 TTL이 만료되는 시점에 재적용됩니다.


1.0.13 (2012.11.12)
----------------------------

   - 캐싱된 파일을 최초에 변경확인(If-Modified-Since)으로 접근할 경우 파일이 정상적으로 초기화되지 않던 버그가 수정되었습니다. 이 버그로 인하여 최초 응답시점에 500 Internal Error를 보내거나 TTL이 아주 짧게 설정되어 있는 경우 파일의 유효성이 문제가 될 수 있습니다.
   - 간헐적으로 원본서버에서 컨텐츠가 변경되지 않았더라도(304 Not Modified) 최초 접근하는 클라이언트를 무조건 200 OK로 처리하던 증상이 수정되었습니다.
   - 정상적으로 캐싱(200 OK)되어 있는 파일을 갱신하는 과정에서 원본서버로부터 5xx응답을 받았을 때 마치 304 not modified를 받은 것처럼 동작하도록 설정합니다. 이를 통해 서버의 임시적인 장애때문에 컨텐츠를 무효화하여 원본 서버 트래픽을 가중시키는 행위를 방지할 수 있습니다.
   - SNMP에서 응답 받을 가상호스트의 최대 개수를 설정할 수 있습니다.


1.0.12 (2012.11.05)
----------------------------

   - 요약통계의 수치(원본 트래픽, 세션)가 맞지 않던 증상이 수정되었습니다.


1.0.11 (2012.10.31)
----------------------------

   - 원본서버가 모두 배제된 상황에서는 Purge/Expire가 동작하지 않습니다.
   - 특정 Purge명령이 Expire로 동작하도록 설정할 수 있습니다.


1.0.10 (2012.10.29)
----------------------------

   - 원본서버가 모두 배제된 상황에서 POST 요청이 클라이언트 세션 수에서 누락되던 증상이 수정되었습니다.
   - 원본서버 장애로 인해 Purge된 컨텐츠를 되살리는 과정에서 아직 디스크에 저장되지 않은 컨텐츠를 초기화하던 증상이 수정되었습니다.


1.0.9 (2012.10.22)
----------------------------

   - 원본서버 HTTP응답의 Content-Disposition헤더를 인지하도록 수정되었습니다.


1.0.8 (2012.10.19)
----------------------------

   - 원본서버에서 Transfer-Encoding: chunked옵션으로 응답을 줄 때 클라이언트에 Content-Length를 주지 않도록 수정하였습니다.
   - 클라이언트의 If-Range헤더를 인지하도록 수정하였습니다.


1.0.7 (2012.10.18)
----------------------------

   - HTTP요청의 Host필드로 가상호스트를 찾을 때 대소문자 구분하지 않도록 수정되었습니다.


1.0.6 (2012.10.12)
----------------------------

   - SSLv2 ClientHello를 인식하도록 개선되었습니다.
   - 바이패스 중 원본서버가 먼저 연결을 종료하였을 때 오동작하던 증상이 수정되었습니다.


1.0.5 (2012.10.08)
----------------------------

   - 원본서버 요청 시에 값이 존재하지 않는 QueryString항목이 누락되던 증상이 수정되었습니다.


1.0.4 (2012.10.04)
----------------------------

   - 원본서버 로그에 QueryString을 기록하지 않던 증상이 수정되었습니다.


1.0.3 (2012.09.28)
----------------------------

   - 설정파일을 리로드하여도 OriginOptions의 Host설정이 반영되지 않던 증상이 수정되었습니다.


1.0.2 (2012.09.27)
----------------------------

   - 설정파일을 리로드한 후 Custom TTL설정이 적용되지 않던 증상이 수정되었습니다.


1.0.1 (2012.09.20)
----------------------------

   - QueryString설정이 ON인 경우 Purge/Expire가 과도하게 CPU를 점유하던 문제가 개선되었습니다.


1.0.0 (2012.09.18)
----------------------------

   - 설정파일을 동적으로 Reload할 수 있습니다. 서비스 중단 없이 가상호스트 추가, 삭제, 변경이 가능합니다.
   - 하드디스크의 최대사용량을 설정할 수 있습니다. 설정하지 않아도 언제나 디스크가 꽉차지 않도록 관리됩니다.
   - 가상호스트의 순서가 변경되더라도 항상 동일한 SNMP의 OID로 통계를 수집할 수 있도록 가상호스트의 OID를 설정할 수 있습니다.
   - Access 로그를 Apache와 Microsoft IIS형식으로 설정할 수 있습니다.
   - HTTP응답에 Via헤더 삽입을 설정할 수 있습니다.
   - 클라이언트의 Accept-Encoding을 무시하도록 설정할 수 있습니다.
   - 콘솔 또는 API를 통해 STON 버전확인이 가능합니다.
   - API를 통해 설정파일 열람이 가능합니다.
   - 원본서버 로그에 QueryString을 기록합니다.
   - SSL을 통한 HTTP Post요청 바이패스가 오동작하던 버그가 수정되었습니다.
   - 가상호스트 서비스 포트설정이 <Address>에서 <Listen>으로 설정되었습니다.
   - 가상호스트별로 디스크 설정을 별도로 할 수 없습니다. 모든 가상호스트는 <Storage>를 통해 디스크를 공유하도록 설정되었습니다.
   - Info로그가 보기 쉬운 형식으로 변경되었습니다.
   - fileinfo응답의 시간표현이 "2012.09.03 14:29:50" 같이 읽기쉬운 형태로 변경되었습니다.


v0.9.x
====================================

0.9.6.7 (2012.08.23)
----------------------------

   - 바이패스 중 원본과 클라이언트 세션이 동시에 끊어질 때 STON이 비정상 종료되던 버그 수정
   - 원본서버가 "Transfer-Encoding: chunked"로 응답을 줄 때 Receive Timeout이 짧게 지정되던 버그 수정
   - API응답의 MIME 타입을 application/json에서 text/plain으로 변경


0.9.6.6 (2012.08.01)
----------------------------

   - 특정 IP의 서비스(가상호스트) 접근을 차단 또는 허가하도록 설정할 수 있습니다.
   - 원본서버가 과부하 상태라고 판단되면 만료된 컨텐츠의 TTL을 원본서버에게 물어보지 않고 갱신합니다.
   - GET요청의 기본동작을 원본서버로 바이패스하도록 설정할 수 있습니다.
   - Origin로그에 바이패스 된 요청인지 기록합니다.
   - 바이패스 세션의 Timeout 시간을 설정할 수 있습니다.


0.9.6.5 (2012.07.17)
----------------------------

   - 원본서버를 Active/Standby로 설정할 수 있습니다.
   - Access로그에 클라이언트의 Range필드(cs-range)추가
   - HTTP요청이 Invalid Range를 요청하는 경우 동작방식을 변경하였습니다. 기존에는 파일 크기를 벗어난 Range요청은 무조건 416 Requested Range Not Satisfiable으로 처리됐습니다. 이번 버전부터는 끝 오프셋이 파일 크기보다 클 경우 206 Partial Content로 처리됩니다. 시작 오프셋이 파일 크기보다 큰 경우는 기존과 동일하게 처리됩니다.


0.9.6.4 (2012.07.12)
----------------------------

   - HTTP POST요청 처리시 비정상 종료되던 문제를 수정하였습니다.
   - HTTP POST요청의 원본서버 바이패스 여부를 설정할 수 있습니다.
   - 원본서버 HTTP 응답에 Content-Type헤더가 명시되어 있지 않은 경우 클라이언트에게도 Content-Type헤더를 주지 않습니다. (기존에는 text/html로 설정)


0.9.6.3 (2012.07.11)
----------------------------

   - HTTPS 요청을 원본서버로 바이패스할 때 잘못된 메모리 참조로 인하여 오동작/비정상 종료되던 문제가 수정되었습니다.
   - 투명(Transparent) 모드를 지원합니다. STON과 원본서버 네트워크 구간 사이에 원본서버의 응답을 STON으로 포워딩하는 설정이 필요합니다.
   - Expired된 컨텐츠를 서비스하기 전에 반드시 원본서버에서 확인하도록 할 수 있습니다.
   - 더 이상 URLBypass통계를 별도로 수집하지 않습니다. 원본/클라이언트 트래픽 통계로 통합되었습니다.
   - IBM WebLogic에서 클라이언트 Access로그를 남길 수 있도록 WL-Proxy-Client-IP 헤더를 추가할 수 있습니다.
   - 원본서버로 보내는 HTTP요청의 X-Forwarded-For헤더의 클라이언트 IP이후를 설정할 수 있습니다.
   - 에러 페이지(500 Internal Error)에서 에러이유를 표시합니다.
   - 설정에서 문자열의 공백을 제거하지 않던 문제가 수정되었습니다. 모든 문자열의 좌우공백은 제거됩니다.


0.9.6.2 (2012.06.19)
----------------------------

   - 캐싱되어 있지 않은 파일의 가장 마지막 부분을 Range Request했을 때(Range의 범위가 1024 Bytes미만) 데이터가 전송되지 않던 버그 수정


0.9.6.1 (2012.06.14)
----------------------------

   - CacheClear 기능 추가 - 로 설정된 모든 디스크를 삭제합니다. STON의 모든 서비스는 중단되며 작업이 완료된 뒤 자동으로 재개됩니다.

     | http://127.0.0.1:10040/command/cacheclear

   - 로그 파일의 OriginOptions의 Host설정 누락이 수정되었습니다.
   - 로그 파일의 Options설정표현이 "TTL"에서 "Options"로 변경되었습니다.


0.9.6 (2012.06.12)
----------------------------

   - SNMP(Simple Network Monitoring Protocol)가 지원됩니다. STON은 항상 실행경로에 MIB(Management Information Base)파일을 생성합니다. STON의 SNMP는 가상호스트별, 실시간, 최근 1~60분까지의 통계를 제공합니다. 최초 실행시 비활성화되어 있으며 server.xml을 편집해 활성화 시킬 수 잇습니다.
   - 원본서버에서 Content Length없는 응답이 올 경우, Origin로그에 원본서버 에러로 기록하지 않도록 변경되었습니다. 원본서버에서 일방적으로 연결을 종료한 경우, 만약 해당 세션이 Content Length가 없는 HTTP 트랜잭션을 수행 중이었다면 원본에러로 기록되지 않습니다.
