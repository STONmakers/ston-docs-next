.. _release:

Appendix A: 릴리스 이력
***********************


v2.0.x
====================================

2.0.4 (2015.2.27)
----------------------------

**기능개선/정책변경**

   - :ref:`origin-balancemode` 의 ``Hash`` 알고리즘 변경
   
     | **Before.** hash(URL) / 서버대수
     | **After.** `Consistent Hashing <http://en.wikipedia.org/wiki/Consistent_hashing>`_
     |     
   - :ref:`access-control-vhost` 를 통해 Redirect 할 때 클라이언트가 요청한 URI을 파라미터로 입력할 수 있다.
   
**버그 수정**

   - 캐싱된 파일이 삭제되지 않아 디스크가 꽉 차던 증상
   
   

2.0.3 (2015.2.9)
----------------------------

**기능개선/정책변경**

   - DIMS 내재화 및 고도화
   - WM - 트래픽 관련 안내 메세지 추가
   
**버그 수정**

   - WM - 신규 가상호스트 생성이 실패 하는 버그 수정


2.0.2 (2015.1.28)
----------------------------

- 원본서버에 캐싱요청할 때 클라이언트가 보낸 User-Agent헤더 값을 보낼 수 있다.

**버그 수정**

   - MDAT 길이가 1인 MP4파일의 Trimming이 되지 않던 증상
   - WM - 클러스터 내의 다른 서버 그래프가 표시되지 않던 증상
   - WM - 클러스터 내의 다른 서버들이 현재 서버로 보여지던 증상


2.0.1 (2014.12.30)
----------------------------

**버그 수정**

   - HitRatio그래프가 0으로 표시되던 증상


2.0.0 (2014.12.17)
----------------------------

- 원본에서 다운로드된 크기만큼만 디스크 공간사용. ( :ref:`origin_partsize` 참조)
- :ref:`env-cache-resource` 기능추가.
- TLS 1.1 지원.
- AES-NI를 통해 :ref:`https-aes-ni` 지원.
- ECDHE 계열의 CipherSuite를 지원. ( :ref:`https-ciphersuite` 참조)
- :ref:`admin-log-dns` 추가
- 원본서버가 Domain일 경우 각 IP별 TTL을 사용하도록 정책변경.
- 원본 :ref:`origin_exclusion_and_recovery` 추가
- 원본 :ref:`origin-health-checker` 추가
- :ref:`adv_topics_sys_free_mem` 추가
- 기타

  - 최소 실행환경 변경. (Cent 6.2이상, Ubuntu 10.01 이상)
  - 설치 패키지에 NSCD데몬이 탑재.
  - :ref:`media-dims` 기본 탑재.
  - :ref:`getting-started-reset` 후 STON 재시작하도록 변경.
  - ``<DNSBackup>`` 기능 삭제
  - ``<MaxFileCount>`` 기능 삭제.
  - ``<Distribution>`` 기능 삭제. :ref:`origin-balancemode` 기능에 통합.


v1.4.x
====================================

1.4.4 (2014.12.15)
----------------------------

**버그 수정**

   - DIMS 처리시 404 Not Found로 응답되던 증상


1.4.3 (2014.12.10)
----------------------------

**버그 수정**

   - FTP 클라이언트에서 업로드 경로가 길면 오동작하는 증상


1.4.2 (2014.12.8)
----------------------------

- Purge(자동 복구) API가 HardPurge(복구 불가)로 동작하도록 설정할 수 있다.
- 로그 롤링시 압축하도록 설정할 수 있다.
- FTP 클라이언트 기능강화 - 전송시간, 경로, 삭제, 백업 기능 추가

**버그 수정**

   - SSL/TLS Handshake과정 중 비정상 종료되던 증상


1.4.1 (2014.11.25)
----------------------------

- 클라이언트가 보낸 URI를 가공없이 원본서버에 보내도록 설정할 수 있다.

**버그 수정**

   - MP4영상에 SPS/PPS가 없을 때 비정상 종료되던 증상
   - FTP 클라이언트가 Active모드로 동작하지 않던 증상
   - WM - SNMP의 VhostMin, ViewMin을 0부터 설정가능하도록 수정 (기존 1부터)


1.4.0 (2014.11.12)
----------------------------

- License 도입
- WM - 클러스터 전용 포트분리 추가


v1.3.x
====================================

1.3.20 (2014.11.5)
----------------------------

- [전역] MaxSockets 기능 추가. 설정된 최대 클라이언트(소켓) 수를 넘어가는 접근이 발생할 경우 클라이언트 접속 즉시 연결을 끊는다. 이는 솔루션과 플랫폼을 보호하기 위한 가장 강력한 조치이다. 전체 소켓이 일정비율 이하로 내려가면 다시 클라이언트 접근을 허용한다.
- Https 프로토콜(SSL3.0 또는 TLS1.0) 선택가능

**기능개선/정책변경**

   - File System 에서 파일시간 제공방식 설정가능
   
     | **Before.** 로컬에 캐싱된 시간
     | **After.** 원본의 Last-Modified 시간
     |     
   - 원본헤더 인식 ON 설정시 동작변경
   
     | **Before.** cookie 헤더를 제거한다.
     | **After.** cookie, set-cookie, set-cookie2 헤더를 제거한다. WM에서 경고메시지 강화
     |     
   - WM - 가상호스트 삭제시 삭제 될 가상호스트 이름 명시
   - WM - 설치시 cgi-bin경로에 어떤 파일도 설치하지 않도록 수정
   - WM - RRD 메모리 그래프의 Scale을 1000에서 1024로 변경
   
**버그 수정**

   - File System에서 파일접근에 실패했을 경우 비정상종료될 수 있던 증상
   - WM - 원본 복구에서 Cycle과 값이 서로 바뀌어서 저장되던 증상

1.3.19 (2014.10.21)
----------------------------

**기능개선/정책변경**

   - MP4/M4A Trimming 정책변경
   
     | **Before.** 모든 트랙을 Trimming한다.
     | **After.** Audio/Video 트랙만을 Trimming한다. AllTracks속성을 통해 기존처럼 모든 트랙을 Trimming할 수 있다.
     |

1.3.18 (2014.10.15)
----------------------------

**버그 수정**

   - DIMS 처리에서 클라이언트가 보낸 QueryString이 반영되지 않던 증상
   - 원본서버가 모두 배제되었을 때 특정조건에서 캐싱파일이 초기화되지 않던 증상
   - WM - 보안정책 강화 및 가상호스트 이름에 공백이 없도록 Trim.
   - WM - Unmount된 디스크의 상태를 올바르게 인식하지 못하던 증상

1.3.17 (2014.9.22)
----------------------------

**버그 수정**

   - SNMPWalk를 통해 FileSystem통계가 제공되지 않던 증상
   - WM을 통해 DIMS설정 시 해당 가상호스트의 Alias가 초기화되던 증상

1.3.16 (2014.8.27)
----------------------------

**버그 수정**

   - FileSystem 에서 getattr함수가 많이 호출되면 메모리가 정리되지 않던 증상 및 관련 통계 수정

1.3.15 (2014.8.25)
----------------------------

**버그 수정**

   - 잘못된 SNMP 접근으로 인해 비정상 종료되던 증상

1.3.14 (2014.8.13)
----------------------------

- 최대 사용 메모리를 제한하도록 설정할 수 있다.
- SNMP - 허가된 Community외엔 접근이 불가능하도록 설정할 수 있다.
- WM - 서비스 Listen포트를 멀티로 설정할 수 있다. 클러스터 전용포트를 설정할 수 있다.

**기능개선/정책변경**

   - 파일 인덱싱 정책 변경
   
     | **Before.** 완료된 파일만 인덱싱한다.
     | **After.** 다운로드 중인 파일도 인덱싱한다.
     |
   - Emergency 기본 값 OFF로 변경
   - 기본 Access로그에 sc-content-length필드 추가

1.3.13 (2014.7.21)
----------------------------

- WM - 파일캐싱 모니터링에서 조회한 파일을 다운로드 할 수 있다.

**버그 수정**

   - FileSystem 메모리 누수버그 수정

1.3.12 (2014.7.10)
----------------------------

**기능개선/정책변경**

   - 서비스 허용/거부/Redirect 조건, 바이패스 조건, Bandwidth-Throttling 조건 - 복합조건을 설정할 때 결합(AND) 키워드를 "&"에서 " & "로 변경.
   
     | **Before.** $IP[AP]&!HEADER[referer] 표현가능
     | **After.** $IP[AP] & !HEADER[referer] 처럼 결합조건 사이에 반드시 공백필요
     |
   - SNMP - bytesHitRatio 타입이 음수를 표현할 수 있도록 gauge32에서 integer로 변경
   - WM - 비대칭키 인증정책으로 변경
   
**버그 수정**

   - 1MB보다 작은 MP4파일을 Media 기능으로 서비스할 때 오동작하거나 비정상 종료되던 문제
   - 비정상 HTTP요청에 대한 예외처리 강화

1.3.11 (2014.6.19)
----------------------------

- 마지막(=현재) 설정상태 확인(/conf/lastest) API 추가

**기능개선/정책변경**

   - Bypass-Control 개선
   
     | **Before.** 명시적인 URL 또는 Cookie등으로 바이패스(또는 예외) 설정 
     | **After.** IP, Header, URL 또는 이를 결합한 복합조건으로 바이패스 가능. Cookie바이패스 삭제.
     |
   - 클라이언트 트래픽 - 디렉토리 별 requestHitRaio 추가
   - WM - hostname과 IP가 로그인하지 않은 상태에서 표시되지 않도록 수정
   
**버그 수정**

   - DNS가 Resolving응답을 정상적으로 주지만 주소가 없을 때 죽는 버그.
   - origin.log, filesystem.log 롤링할 때 파일명이 GMT시간으로 생성되던 증상. 로컬시간으로 생성되도록 수정.
   - /monitoring/hwinfo API에서 디스크 사용량이 표시되지 않던 증상
   - WM - 마지막 접근시간이 올바르게 표시되지 않던 증상

1.3.10 (2014.6.3)
----------------------------

- 모든 Disk가 장애로 배제되었을 때 동작방식(재투입, Bypass, 종료)을 설정할 수 있습니다.
- 원본 HTTP요청의 Host헤더를 클라이언트가 보낸 값을 사용하도록 설정할 수 있습니다.

**기능개선/정책변경**

   - 파일캐싱 모니터링에서 QueryString 특수문자을 포함하는 URL도 모니터링할 수 있습니다.
   - 5분평균 통계(XML, JSON)에서 5분간 총 양이 함께 표기됩니다.
   - HTTP POST요청캐싱과 Bypass정책이 동시에 설정된 경우, 서비스 정책이 재정립되었습니다
   - Trimming정책 변경
   | **Before.** Trimming의 끝(end) 시간에 가장 인접하도록 분할
   | **After.** Trimming의 끝(end) 시간의 이전 Key-Frame으로 분할
   
**버그 수정**

   - MP4파일이 서비스되지 않고 CPU를 점유하던 증상

1.3.9 (2014.5.21)
----------------------------

**기능개선/정책변경**

   - 서비스 거부 조건에서 응답코드를 설정할 수 있습니다.
   | **Before.** 에러 페이지에 "401 Access Denied"라고 명시
   | **After.** 별도의 페이지 없이 설정된 응답코드로만 응답

**버그 수정**

   - 잘못된 MP4영상 Trimming 중 비정상 종료되던 증상.
   - FileSystem에서 (최초 PartSize가 설정된 상태에서 캐싱되는 파일에 대해) 간헐적으로 잘못된 데이터를 서비스하던 증상.
   - WM - Port바이패스 설정이 반영되지 않던 증상

1.3.8 (2014.4.30)
----------------------------

- 로그가 롤링될 때 FTP로 전송하도록 설정할 수 있습니다.
- Emergency모드가 발동하지 않도록 설정할 수 있습니다.
- 원본서버의 ETag를 인식하도록 설정할 수 있습니다.
- SNMP Community를 설정할 수 있습니다.
- TTL적용 우선순위를 설정할 수 있습니다.
- HTTP의 POST Method요청의 Body를 캐싱키로 인식/무시하도록 설정할 수 있습니다.

**버그 수정**

   - MP4HLS 변환 중 비디오가 깨지던 증상.
   - 강제로 TTL을 만료시킨 컨텐츠가 304 Not Modified로 인해 TTL이 다시 정해질 때 설정상 가장 큰 값이 할당되던 증상. 설정상 가장 작은 값이 할당되도록 수정.

1.3.7 (2014.4.11)
----------------------------

**버그 수정**

   - domain.com:80 처럼 Port가 명시된 HTTP요청에 대해 가상호스트를 찾지 못하던 증상 (v1.3.4~1.3.6)
   - 잘못된 MP4영상분석 중 비정상 종료되던 증상

1.3.6 (2014.4.9)
----------------------------

사용자정의 접근로그를 설정할 수 있습니다.
View를 통해 가상호스트를 통합하여 모니터링 할 수 있습니다.
컨트롤 API(Purge, Expire, HardPurge, ExpireAfter)의 대상이 없을 때 HTTP 응답코드를 설정할 수 있습니다.
FAQ에 "Wowza는 어떻게 연동하나요?"가 추가 되었습니다.

**기능개선/정책변경**

   - Log 롤링 조건
   | **Before.** 시간 또는 크기 중 택1
   | **After.** 시간과 크기 동시설정 가능
   |
   - WM - 페이지 상단에 서버의 호스트명과 IP를 보여줍니다.

**버그 수정**

   - WM - 설정파일 중 CDATA로 저장된 문자열이 Plain Text로 바뀌던 증상

1.3.5 (2014.4.2)
----------------------------

**버그 수정**

   - 변경된 설정 적용 중 CPU사용량이 높아지며 서비스가 정상동작하지 않던 증상
   - WM - 설정파일에 동일한 설정이 중복되어 표시되던 증상

1.3.4 (2014.3.26)
----------------------------

   - FileSystem 업그레이드 - 파일확장(Trimming, HLS, DIMS등)이 HTTP와 동일하게 동작합니다. - 전용 로그(filesystem.log)가 추가되었습니다. - Hit율, Outbound, Session, XML/JSON, SNMP, 상세통계 가 추가 되었습니다.
   - 정규표현식을 사용한 URL전처리가 가능합니다.
   - 시스템(OS)의 TCP 소켓상태를 실시간으로 모니터링 합니다. SNMP, XML/JSON, RRD Graph로 제공됩니다.
   - 가상호스트가 포트를 Listen하지 않도록 설정할 수 있습니다.

**버그 수정**

   - (FileSystem이 Mount되어 있을 때) STON의 정상종료가 오래 걸리던 증상
   - WM - (FileSystem을 사용하지 않는 환경에서) 신규 가상호스트 추가시 FileSystem페이지 활성화되던 증상
   - WM - 클러스터링 구성 중 대상 WM이 한번도 실행되지 않았었다면 설정이 적용되지 않던 증상

1.3.3 (2014.3.19)
----------------------------

**버그 수정**

   - 갱신중인 파일을 MP4 Trimming으로 서비스 할 때 간헐적으로 비정상 종료되던 증상

1.3.2 (2014.3.5)
----------------------------

   - WM을 통해 최신버전으로 업그레이드 할 수 있습니다.
   - STON의 설치/업그레이드 시 진행상황을 install.log에 기록합니다.
   
**버그 수정**

   - 불완전한(=실시간으로 변환 중인) MP4 파일 캐싱 중 서비스가 멈추던 증상.
   - WM에서 클러스터 전체 적용 시 가상호스트 파일이 초기화되던 증상

1.3.1 (2014.2.24)
----------------------------

**버그 수정**

   - MP4 파일 서비스 중 비정상 종료될 수 있던 증상.
   - 설정백업 기간 이외의 설정이 삭제되지 않던 증상.

1.3.0 (2014.2.20)
----------------------------

   - FileSystem 추가 - STON을 Linux VFS(Virtual File System)에 Mount합니다. 원본서버의 모든 파일을 로컬 파일 I/O로 사용할 수 있습니다.
   - 설정백업관리 추가 - 설정이 변경될 때마다 전체설정을 기록합니다. API(목록, 롤백, 다운로드, 업로드)와 SNMP를 통해 열람, 다운로드, 업로드, 복원이 가능합니다.
   - MP4HLS 추가 - 단일 MP4파일을 HLS(Http Live Streaming)으로 전송할 수 있습니다.
   - 통계 추가 - 전송 중 원본서버에서 먼저 소켓을 종료시킨 횟수

**기능개선/정책변경**

   - SNMP [vhostIndex] 관리 정책변경
   | **Before.** 가상호스트가 삭제되거나 순서가 변경될 경우 [vhostIndex]가 재조정된다. 예를 들어 A(1), B(2), C(3)에서 B가 삭제된 경우 A(1), C(2)로 재조정된다.
   | **After.** [vhostIndex]를 기억한다. 예를 들어 A(1), B(2), C(3)에서 B가 삭제되더라도 A(1), C(3)을 유지한다. 신규 가상호스트가 추가되면 비어있는 [vhostIndex]를 가진다. 예를 들어 가상호스트 D가 추가되면 A(1), D(2), C(3)로 재조정된다.
   |
   - 설정 리로드 API 변경
   | **Before.** /conf/reloadall, /conf/reloadserver, /conf/reloadvhosts가 별도로 존재하며 기능을 달리한다.
   | **After.** /conf/reload로 일괄통일한다. 하위 호환성을 위해 기존 API를 유지한다.


v1.2.x
====================================

1.2.14 (2014.2.6)
----------------------------

**기능개선/정책변경**

   - 원본주소 DNS 정책 변경
   | **Before.** 다른 가상호스트지만 원본주소로 같은 Domain을 사용한다면 Domain Resolving결과를 공유한다.
   | **After.** 모든 가상호스트는 독립적으로 Domain Resolving을 수행하며 공유하지 않는다.

**버그 수정**

   - WM을 통한 Disk Hot-Swap 오동작 수정.

1.2.13 (2014.1.22)
----------------------------

**버그 수정**

   - 특정 설정(NoCacheRequestExpire=ON, RefreshExpired=ON, VaryHeader 존재)에서 응답이 지연되거나 전송되지 않던 동작 수정.

1.2.12 (2014.1.2)
----------------------------

**버그 수정**

   - 최신 NEXUS 기기에서 Trimming된 MP4/M4A가 재생되지 않던 증상 수정. (에러 메세지: The player doesn't support this type of audio file.)

1.2.11 (2013.12.20)
----------------------------

**기능개선/정책변경**

   - 원본서버 Cach-Control 헤더 인식정책 변경
   | **Before.** no-cache 또는 max-age만을 인식한다.
   | **After.** no-cache, no-store, no-transform, muset-revalidate, proxy-revalidate, private, max-age를 구분하여 인식한다. custom은 무시한다.
   |
   - 5분 평균 Request Hit율 계산방식 변경
   | **Before.** 각 TCP_XXX의 (단위 시간에 대한)평균을 구한 뒤 Hit율 계산한다. 각 평균 값이 단위 시간보다 작을 때 누락될 수 있다.
   | **After.** (평균을 내지 않고) 비율로만 계산하여 값이 누락되지 않는다.
   

1.2.10 (2013.12.13)
----------------------------

**기능개선/정책변경**

   - HTTPS 통신에서 Access로그 범위 변경
   | **Before.** 클라이언트가 SSL Server Finished 패킷을 온전히 수신한 HTTPS 트랜잭션만을 Access로그에 기록한다.
   | **After.** 클라이언트가 SSL Server Finished 패킷을 온전히 수신하지 못했더라도 HTTP Request 패킷을 보냈다면 Access로그에 기록한다.

**버그 수정**

   - 비정상 종료(물리적 세션 손실)된 HTTPS세션이 재사용될 때 이전에 요청되었던 컨텐츠와 현재 요청된 컨텐츠를 동시에 처리하던 증상. 2개의 HTTP 요청이 동시에 처리될 수 있었으며 이를 항상 현재 요청한 요청만이 유효하도록 수정.

1.2.9 (2013.12.9)
----------------------------

**기능개선/정책변경**

   - Bandwidth-Throttling 정책 변경
   | **Before.** Boost 시간동안 미디어를 전송할 때 헤더를 포함한다. 헤더가 클 경우 미디어 데이터가 전송되지 않아 버퍼링이 발생할 수 있다.
   | **After.** 미디어 헤더는 대역폭 제한없이 전송한다. 헤더 전송이 완료된 후 Boost 시간이 시작된다.

**버그 수정**

   - WM 포트 변경 후 STON 업데이트 시 변경된 포트가 유지되지 않던 증상

1.2.8 (2013.11.14)
----------------------------

**기능개선/정책변경**

   - 접속하는 HTTP 클라이언트마다 고유번호(session-id)를 부여합니다. session-id는 Access로그와 Origin로그에 추가되어 연관성을 유추할 수 있습니다.
   - API호출의 파라미터로 https://... 형식을 인식합니다.
   
**버그 수정**

   - OriginalHeader가 ON으로 설정되어 있을 때 Content-Disposition헤더가 HTTP 응답에 2번 표시되던 증상
   - Bandwidth-Throttling설정이 OFF일 때 Trimming이 동작하지 않던 증상
   - WM계정에 특수문자(&)사용시 로그인 안되던 증상

1.2.7 (2013.10.17)
----------------------------

   - HTTP Connection헤더를 설정할 수 있습니다.
   - HTTP Keep-Alive헤더를 설정할 수 있습니다.
   - FAQ에 "HTTP 연결관리 정책은?" 이 추가되었습니다.

**기능개선/정책변경**

   - HTTP 응답에 Connection헤더와 Keep-Alive헤더를 기본으로 설정합니다.

1.2.6 (2013.10.14)
----------------------------

   - 원본서버의 "Server" 헤더를 클라이언트에게 전달하도록 설정할 수 있습니다.
   
1.2.5 (2013.10.10)
----------------------------

**기능개선/정책변경**

   - 인식할 수 있는 미디어파일에 대해 동적으로 Bandwidth-Throttling의 Bandwidth를 설정할 수 있습니다. v1.2.4까지 존재했던 Media.Pacing은 이 기능에 포함되면서 삭제되었습니다.

**버그 수정**

   - 극히 드물게 잘못된 문자열 참조 오류로 인해 비정상종료되던 증상

1.2.4 (2013.9.27)
----------------------------


   - Bandwidth-Throttling을 통해 전송 대역폭을 다양하게 설정할 수 있습니다. 
   
   .. Warning:: 다음 버전에서 Media.Pacing은 Bandwidth-Throttling에 통합될 것입니다. 미디어 파일(현재 MP3, MP4, M4A 지원)의 Bitrate를 Bandwidth-Throttling에서 인식할 수 있는 형태가 될 것입니다. 현재는 기존 기능인 Media.Pacing이 더 우선하도록 개발되어 있습니다. 

   - 가상호스트별로 클라이언트 최대 Bandwidth를 제한하도록 설정할 수 있습니다.
   - 헤더가 뒤에 있는 M4A파일을 헤더를 앞으로 옮겨서 서비스하도록 설정할 수 있습니다.
   - M4A파일을 원하는 구간만큼 잘라내어 서비스하도록 설정할 수 있습니다.

**기능개선/정책변경**

   - 가상호스트 AccessControl 조건에 해당하는 클라이언트 요청에 대해 Redirect(302 moved temporarily)로 응답하도록 설정할 수 있습니다. HIT율은 TCP_REDIRECT_HIT로 별도로 수집됩니다.
   - TCP_REDIRECT_HIT가 모든 통계에 추가되었습니다.
   - 가상호스트 AccessControl 조건을 AND로 결합하도록 설정할 수 있습니다.

**버그 수정**

   - 클러스터가 구성되지 않던 증상 - IP를 추출할 때 Loopback이 추출되던 증상

1.2.3 (2013.9.5)
----------------------------


   - DIMS(Dynamic Image Management System) - 원본서버의 이미지를 가공(잘라내기, 썸네일생성, 크기변경, 포맷변경, 품질조절, 합성)하도록 설정할 수 있습니다.
   - MP3파일을 원하는 구간만큼 잘라내어 서비스하도록 설정할 수 있습니다.
   - 특정 IP만 Listen하도록 설정할 수 있습니다.
   - [WM] 신규 가상호스트를 생성할 때 기존 가상호스트를 선택해 복사할 수 있습니다.
   - [WM] 가상호스트에서 DIMS를 설정할 수 있습니다.

**기능개선/정책변경**

   - 원본세션을 재사용하지 않도록 설정할 수 있습니다.
   
**버그 수정**

   - MP4 Trimming 중 비정상 종료되던 증상
   - 콘솔에서 수정한 가상호스트 설정이 WM의 클러스터에 반영되지 않던 증상

1.2.2 (2013.8.16)
----------------------------


   - HTTP Post 요청을 캐싱하도록 설정할 수 있습니다.
   - STON이 서비스를 감당할 수 없는 상태에 Emergency모드로 전환된다.
   
**기능개선/정책변경**

   - 서비스 허용/차단 조건에 부정(!IP, !HEADER, !URL)조건이 추가되었습니다.
   - WM과 콘솔에서 동시에 설정을 변경할 때 WM에서 콘솔에서 변경한 내용을 인식하도록 변경되었습니다.
   - WM에서 IE의 "호환성 보기" 메뉴를 숨기도록 변경되었습니다.

**버그 수정**

   - CPU 과부하 상태에서 바이패스 세션이 정상적으로 정리되지 않아 비정상 종료되던 증상
   - (Vary헤더 설정환경에서) 원본서버에서 200 OK로 응답하지 않는 컨텐츠 서비스 중 비정상 종료되던 증상
   - 가상호스트명과 Alias가 같은 경우 Alias를 제거했을 때 가상호스트를 찾을 수 없던 증상
   - WM 클러스터에 설정이 반영되지 않던 증상

1.2.1 (2013.7.26)
----------------------------


   - MP4파일을 원하는 구간만큼 잘라내어 서비스하도록 설정할 수 있습니다.
   - 원본서버에서 컨텐츠를 최초로 캐싱하거나 갱신할 때 Range요청을 하도록 설정할 수 있습니다.
   
**버그 수정**

   - WM에서 클러스터가 구성되지 않던 증상
   - 로그설정 변경 후 "/conf/reloadserver" API를 호출했을 때 반영되지 않던 증상
   - SNMP에서 Host평균 통계가 평균이 아닌 합으로 계산되던 증상
   - 특정 상황에서 클라이언트 트래픽 통계수치가 비정상적으로 높게 계산되던 증상

1.2.0 (2013.7.1)
----------------------------


   - WM(Web Management)이 추가되었습니다. 모든 설정이 WM을 통해 가능하며 MRTG(5종류 - 대쉬보드/5분/30분/2시간/1일)가 최대 18개월치 제공됩니다. WM을 통해 STON을 클러스터로 묶어서 쉽게 관리할 수 있습니다.
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

1.1.17 (2013.5.27)
----------------------------

   - Origin By Client를 설정할 수 있습니다.

**기능개선/정책변경**

   - Transfer-Encoding으로 전송된 컨텐츠를 (전송지연 등의 이유로) 온전하게 캐싱하지 못한 경우 클라이언트 서비스정책 변경
   | **Before.** 캐싱에 실패한 현재 컨텐츠를 서비스
   | **After.** 이전에 온전하게 캐싱된 컨텐츠가 있다면 이전 컨텐츠로 서비스. 없다면 500 Internal Error.

**버그 수정**

   - RefreshExpired가 OFF인 상태에서 PartSize가 0보다 크게 설정된 경우 컨텐츠 갱신이 안되는 증상

1.1.16 (2013.5.15)
----------------------------


**기능개선/정책변경**

   - 리눅스 최대 파일개수 제한으로 File I/O가 실패하지 않도록 파일저장방식 변경
   - 정상동작을 위해 필요한 서브파일 점검 로그 추가

**버그 수정**

   - 갱신중인 파일이 HardPurge될 때 비정상 종료되던 증상
   - 가상호스트별로 미디어 설정이 되지 않던 증상
   - syslog 설정이 리로드되지 않던 증상
   - OriginError로그에 syslog설정시 Info로그에 Inactive로 표시되던 증상

1.1.15 (2013.4.29)
----------------------------

   - CPU 성능지표(Nice, IOWait, IRQ, SoftIRQ, Steal) 통계 추가 - Stats, SNMP(System.27 ~ 36)

**버그 수정**

   - Track정보가 많은 MP4파일 분석 중 비정상 종료되던 증상
   - HTTP Transfer-Encoding된 컨텐츠를 전송할 때 지연되던 증상
   
1.1.14 (2013.4.10)
----------------------------

   - SNMP에 Host통계(=전체 가상호스트의 합)가 추가되었습니다.
   
**기능개선/정책변경**

   - (파일이 없을 때) GeoIP파일목록 조회 결과 변경
   | **Before.** 404 NOT FOUND
   | **After.** 200 OK ("files": [] 응답)
   - 
**버그 수정**

   - SSLv3에서 RSA_WITH_3DES_EDE_CBC_SHA로 Handshake가 되지 않던 증상 수정
   - CipherSuite속성에 빈 문자열 입력 시 오동작하던 증상

1.1.13 (2013.3.29)
----------------------------

**버그 수정**

   - 디렉토리별 통계가 설정된 상태에서 누적통계가 OFF인 경우 비정상 종료되던 증상
   - 처음 접근되는 컨텐츠가 원본서버로부터 응답을 받기 전에 Purge되는 경우 클라이언트에게 응답을 주지 않던 증상
   - HTTP 요청의 URI가 상대주소가 아니라 절대주소일 경우 서비스 안되던 증상

1.1.12 (2013.3.27)
----------------------------

   - No-Cache요청이 올 경우 요청된 컨텐츠를 즉시 만료시키도록 설정할 수 있습니다.
   - CentOS 패키지로 openSUSE에서 설치할 수 있습니다.

**기능개선/정책변경**

   - No-Cache요청 인식조건 변경
   | **Before.** "pragma: no-cache" 또는 "cache-control: no-cache"
   | **After.** 기존 조건에 "cache-control: max-age=0" 추가

**버그 수정**

   - DNS갱신시 비정상 종료되던 증상
   - 최대 파일개수를 넘어갈 때 URL에 Vertical Bar(|)가 있는 파일들이 삭제되지 않던 증상
   - HTTP 요청이 바이패스 될 때 HttpReqBodySize와 ClientInbound 값이 정확하지 않던 증상

1.1.11 (2013.3.21)
----------------------------

   - Disk장애 조건을 설정할 수 있습니다. 장애로 판단된 디스크는 자동배제됩니다.
   - Disk HotSwap용(실행 중 디스크 교체) API가 추가되었습니다.
   - 로그를 syslog로 전송하도록 설정할 수 있습니다.
   - 원본서버에서 한번에 다운로드 받는 컨텐츠 크기를 설정할 수 있습니다.
   - GeoIP 파일목록 조회 API가 추가되었습니다.
   - FAQ에 "멀티 도메인에 대한 SSL구성은?" 이 추가되었습니다.

**기능개선/정책변경**

   - 원본서버 장애코드 변경
   | **Before.** 숫자로 표시
   | **After.** 읽기 쉬운 형식으로 표시(Connect-Timeout, Receive-Timeout, Server-Close)
   - 원본서버 장애로그 기록시 주석으로 에러상황을 기록하던 것 제거. OriginErrorLog로 통합.

**버그 수정**

   - Manager Port변경 후 Reload할 때 비정상 종료되던 버그 수정


1.1.10 (2013.3.7)
----------------------------


   - 가상호스트마다 접근/차단조건(IP, GeoIP, URI, Header)을 설정할 수 있습니다. 관련 통계가 추가되었습니다.
   - 도메인 Resolving이 실패할 경우 최근 사용된 IP들을 모두 사용하여 원본서버 부하를 분산하도록 설정할 수 있습니다.
   - 모니터링 API가 추가되었습니다.
   - 가상호스트 목록 조회
   - 하드웨어 정보 조회
   - HTTPS CipherSuite 조회
   - 접근차단 조건(acl.txt) 조회
   - Expires헤더 조건(expires.txt) 조회
   
**기능개선/정책변경**

   - 로그 디스크 여유공간이 부족해질 경우 정책 변경
   | **Before.** 개입하지 않음. 관리자가 명시적으로 삭제해야 함.
   | **After.** Access로그만을 삭제. 만약 현재 사용 중인 로그를 지워야하는 상황이라면 새로운 로그 생성 후 삭제함.
   |
   - STON 종료 후 (vhosts.xml에서)삭제된 가상호스트 파일들에 대한 정책 변경
   | **Before.** 개입하지 않음. 관리자가 명시적으로 삭제해야 함.
   | **After.** 디스크 여유공간이 부족해지면 우선적으로 삭제.
   | 
   - (가상호스트 별) 재구동 시 정상적으로 로딩되지 않은 디스크의 파일들에 대한 정책 변경
   | **Before.** 서비스 중 자연히 덮어씌워지도록 남겨둠
   | **After.** 해당 디스크를 신뢰할 수 없다고 판단하여 모두 무효화. 클린업 시간 또는 디스크 여유공간 부족 시점에 모두 삭제.
   | 
   - 도메인 Resolving결과 조회 API 변경.
   | **Before.** /dns/list
   | **After.** /monitoring/dnslist
   | 
   - 로그 트레이스 API 변경
   | **Before.** /logtrace/...
   | **After.** /monitoring/logtrace/...
   | 
   - 도메인 Resolving결과에 백업된 IP목록 추가

1.1.9 (2013.2.27)
----------------------------

   - Apache의 mod_expires와 같이 Expires헤더를 재설정할 수 있습니다.
   - HTTPS의 CipherSuite를 설정할 수 있습니다.
   - 파일을 관리(Purge/Expire/HardPurge/ExpireAfter)할 때 단일 URL만 입력하여도 QueryString까지 모두 관리하도록 설정할 수 있습니다.
   - ETag헤더 표시여부를 설정할 수 있습니다.
   - Age헤더 표시여부를 설정할 수 있습니다.

**기능개선/정책변경**

   - HTTPS CipherSuite가 추가되었습니다.
   - RSA_WITH_RC4_MD5
   - TLS_RSA_WITH_3DES_EDE_CBC_SHA
   |
   - 숫자(초=sec)로만 하던 표현을 인식하기 쉬운 문자형식으로 표현가능
   | **Before.** /image/ad.jpg, 1800
   | **After.** /image/ad.jpg, 6 hours
   |
   - SNMP에서 평균으로만 제공하던 수치를 누적으로 제공 (클라이언트/원본)
   - 기존에 Count라는 표현을 Average로 변경. Average는 시간으로 나눈 평균을 의미
   - 시간동안 집계된 전체 수는 Count로 표현
   - 전체 요청/응답 개수 추가
   - 응답코드별 응답/완료 개수 추가
   - Request Hit Count 추가
   
   - 재시작/종료/캐시초기화 API를 호출할 때 "확인" 과정없이 호출할 수 있습니다.
   - 시스템 Load Average - 1분/5분/15분 통계추가
   - 모든 가상호스트의 원본서버를 초기화 할 수 있습니다.

**버그 수정**

   - Domain Resolving결과가 변경되었을 때 여러 가상호스트에 동시에 반영이 안되던 버그 수정

   - Purge/Expire에서 QueryString이 붙어있는 URL이 처리안되던 버그 수정


1.1.8 (2013.2.21)
----------------------------


   - 클라이언트의 요청이 항상 같은 원본서버로 바이패스되도록 설정할 수 있습니다.
   - 도메인 Resolving결과를 모니터링 할 수 있습니다.
   - 도메인 Resolving결과가 업데이트되었을 때 Info로그에 기록하도록 설정할 수 있습니다.
   - 원본서버 사용 및 배제/복구 상황을 초기화 할 수 있습니다.
   - Clean-up 시간에 일정 기간동안 접근되지 않은 컨텐츠들을 삭제하도록 설정할 수 있습니다.
   - Clean-up을 수행하는 API가 추가되었습니다.

**기능개선/정책변경**

   - Origin 로그강화
   - 접속한 포트 기록
   - Bypass와 PrivateBypass구분 가능
   - 원본서버가 보낸 Content-Encoding 헤더 기록
   
   - Access 로그강화
   - 클라이언트가 보낸 Accept-Encoding헤더 기록
   - Bypass와 PrivateBypass구분 가능
   
   - 원본서버가 도메인명으로 설정되어 있을 때 기능개선
   - Resolving결과가 즉시 반영.
   - IP들에 대하여 개별로 배제/복구.
   - Purge/Expire/HardPurge/ExpireAfter 호출결과 응답코드 수정
   - 정상. 200 OK
   - 가상호스트 없음. 502 BAD GATEWAY
   - 잘못된 규격. 400 BAD REQUEST
    
   - FAQ페이지 업데이트
   - 원본서버 사용/배제/복구 정책은?
   - 디스크 여유공간은 어떻게 보장되나요?
    
**버그 수정**

   - 디스크 공간이 부족해도 공간확보가 되지 않던 버그 수정


1.1.7 (2013.2.16)
----------------------------

**기능개선/정책변경**

   - Cent OS 5.5이상과 Ubuntu 10이상에서 동시접속 소켓이 10만을 넘으면 시스템 성능이 저하되며 소켓처리가 실패되는 증상을 확인하였습니다. 그러므로 최대 소켓을 10만으로 제한합니다.

**버그 수정**

   - 사용 중인 소켓이 설정된 최대 소켓수를 넘어갔을 때 증설되지 않던 버그 수정

   - Byte Hit Ratio결과가 부정확하게 표시되던 버그 수정

   - 누적통계 XML에서 ClientSession이 2번 나오던 버그 수정 (ClientActiveSession으로 변경)
   - "abc*"로 패턴 설정했을 경우 "abc"처럼 패턴부분이 빈 문자열에 대해 인식하지 못하던 버그 수정


1.1.6 (2013.1.30)
----------------------------


   - 원본서버가 멀티로 구성되어 있을 때 항상 서버마다 동일하게 요청하도록 설정한다.

**기능개선/정책변경**

   - 원본서버 부하분산 정책이 Session에서 RoundRobin으로 변경되었습니다.
   - 전역로그(Info, Deny, OriginError)를 시간으로 롤링시킨다.
   | **Before.** 크기로만 롤링가능(Size속성만 존재)
   | **After.** 시간/크기로 롤링가능 (Size속성 제거. Type, Unit속성 추가)
   |
   - 잘못된 형식 또는 존재하지 않는 가상호스트를 대상으로 Purge/Expire/ExpireAfter/HardPurge 호출시 응답코드 변경
   | **Before.** 200 OK
   | **After.** 400 BAD REQUEST 또는 404 NOT FOUND
   
**버그 수정**

   - v1.1.5에서 원본서버 주소목록을 변경하고 리로드하였을 때 간헐적으로 비정상종료되던 증상
   - 원본서버에서 트랜잭션 완료 횟수를 수집할 때 Content-Length가 0인 응답이 누락되던 증상

1.1.5 (2013.1.28)
----------------------------

   - 클라이언트마다 바이패스 전용세션을 사용하도록 설정합니다. GET요청과 POST요청을 별도로 설정할 수 있습니다.
   - 클라이언트 Cookie헤더에 따라 바이패스하도록 설정합니다.

**기능개선/정책변경**

   - 원본서버 주소가 빠졌을 때 동작방식 변경
   | **Before.** 이미 연결되어 있다면 재사용한다.
   | **After.** 즉시 재사용하지 않는다.
   |
   - ApplyQueryString이 ON일 때 Purge/Expire동작방식 변경.
   | **Before.** 입력된 URL과 해당 URL에 QueryString이 붙은 컨텐츠 Purge/Expire
   | **After.** 입력된 URL만 Purge/Expire
   |
   - Active세션 산출방식 변경
   | **Before.** 통계를 뽑는 시점에 데이터 전송이 이루어지고 있는 세션
   | **After.** 데이터 전송이 발생한 Unique한 세션
   |
   - 통계/성능 데이터가 추가/삭제되었습니다.
   - 접속 허용(Allow)/차단(Deny) 통계 추가
   - 종합통계에 요청회수, Active세션 통계 추가
   - SSL클라이언트 세션 수 삭제
   

1.1.4 (2013.1.17)
----------------------------

   - HTTPS를 IP와 Port로 다르게 바인딩할 수 있습니다.

**기능개선/정책변경**

   - 64GB장비에서 Free메모리 정책이 16GB로 변경되었습니다. (이전: 8GB)
   - HTTP Method를 서비스 포트(80)로 호출할 수 있으며 Manager접근제어가 적용되도록 설정할 수 있습니다.
   - 전역설정(server.xml)의 HTTPS설정이 변경되지 않았어도 리로드할 때 인증서파일이 변경되었다면 반영합니다.

1.1.3 (2013.1.15)
----------------------------

**기능개선/정책변경**

   - 한번에 기록할 수 있는 로그의 최대 크기를 10MB로 확장(이전: 2KB)
   - POST로 보낼 수 있는 URL크기를 최대 1MB로 확장(이전: 10KB)

**버그 수정**

   - 로그가 시간기준으로 롤링될 때 파일명(날짜)이 정확하지 않던 증상

1.1.2 (2013.1.14)
----------------------------

   - GeoIP를 인식합니다. 클라이언트가 접속할 때 국가코드로 접속을 차단할 수 있습니다.
   - 접근차단된 IP를 Deny로그에 기록합니다.
   - 로그를 동적으로 변경할 수 있습니다.
   - Access로그에 캐시 HIT결과(TCP_HIT, TCP_MISS, ...) 추가
   - 관리용 HTTP Method가 추가되었습니다.
   - POST를 사용하여 PURGE, HARDPURGE, EXPIRE, EXPIREAFTER할 수 있습니다.
   - stonapi를 통해 전체/일부 도메인을 초기화할 수 있습니다.
   - API목록을 열람하는 Help 명령어 추가

**기능개선/정책변경**

   - ETag헤더를 제공할 때 따옴표("...")로 묶어서 표기
   - HIT율 계산식 변경
   | **Before.** 즉시응답 / 모든응답
   | **After.** (TCP_HIT + TCP_IMS_HIT + TCP_REFRESH_HIT + TCP_REF_FAIL_HIT + TCP_NEGATIVE_HIT) / 모든 응답
   |
   - 통계/성능 데이터가 추가/삭제되었습니다.
   - 캐시 HIT결과(TCP_*) 추가
   - 평균통계에 통계를 생성한 날짜/시간 추가
   - 클라이언트에서 STON으로 접속/종료하는 소켓 수 추가
   - STON이 원본서버로 접속/종료하는 소켓 수 추가
   - 이벤트 큐, 참조 큐 추가
   - 쓰기 대기중인 파일개수 추가
   - "Cached" 통계 제거
   
   - 정규표현식 성능향상 (X 20)
   - fileinfo에서 미캐싱파일인 경우 status를 "OK"에서 "NOT_CACHED"로 변경"

**버그 수정**

   - SNMP에서 디스크정보(diskInfoPath, diskInfoStatus)를 얻을 때 Disk개수보다 큰 값이 diskIndex로 입력되면 비정상 종료되던 증상
   - 디스크가 꽉 차기전에 삭제되지 않던 증상. 디스크 Available공간을 남은공간으로 이해하도록 수정
   - stonapi가 관리포트를 인지하지 못하던 증상
   - Info로그에 "Download-Range" 메시지 제거

1.1.1 (2012.12.24)
----------------------------

   - 모든 가상호스트의 원본서버 이상동작을 하나의 파일(OriginError.log)로 기록한다.
   - HTTP Multi-Range요청을 처리할 수 있습니다.
   - 원본서버에서 no-cache로 응답하더라도 클라이언트에게는 max-age를 주도록 설정할 수 있습니다.
   
**기능개선/정책변경**

   - Accept-Encoding처리 정책변경.
   | **Before.** 클라이언트와 원본서버의 압축이 호환되지 않으면 500에러로 응답한다.
   | **After.** 클라이언트와 원본서버의 압축이 호환되지 않더라도 원본서버의 응답을 보낸다.
   |
   - 다음과 같이 통계/성능 데이터가 추가되었습니다.
   - 원본/클라이언트 Active세션수가 추가되었습니다.
   - STON이 사용하는 CPU(Kernel, User) 성능수치가 추가되었습니다.
   
**버그 수정**

   - (설정: TTL=0, RefreshExpired=ON) 원본파일이 변경되었을 때 변경된 파일의 첫 응답코드를 500으로 보내던 증상

1.1.0 (2012.12.17)
----------------------------

가상호스트별로 최대 Outbound를 제한하도록 설정할 수 있습니다.
헤더가 뒤에 있는 MP4파일을 헤더를 앞으로 옮겨서 서비스하도록 설정할 수 있습니다.
MP4를 BiteRate만큼 낮은 대역폭으로 전송하도록 설정할 수 있습니다.
최대 서비스 파일개수를 설정할 수 있습니다.
최대 HTTP 세션 수를 설정할 수 있습니다.
API의 모든 함수를 리눅스 콘솔에서 호출할 수 있습니다.
로그Trace API를 통해 기록되는 로그를 실시간으로 받아볼 수 있습니다.
쉘에서 STON을 업데이트할 수 있습니다.

**기능개선/정책변경**

   - 메모리 정책이 수정되었습니다. 최대 파일개수와 최대 소켓개수를 설정하여 컨텐츠 메모리크기를 조절할 수 있습니다. 자세한 내용은 Performance페이지를 참고하시기 바랍니다.
   - 도메인을 리졸빙(Resolving)한 결과를 캐싱합니다. 최소 1초, 최대 10초동안 캐싱됩니다.
   - OriginOptions의 일부설정(User-Agent, Host, WL-Proxy-Client-IP, XFFClientIPOnly)을 바이패스되는 HTTP요청에 선택적으로 적용할 수 있습니다.
   - 원본서버로부터 5xx계열의 응답코드가 캐싱된 경우 TTL이 만료되면 RefreshExpired가 OFF라도 항상 원본서버에서 갱신여부를 확인하고 서비스합니다.
   - 원본서버에 example.com/dir1 처럼 디렉토리명을 같이 지정할 수 있습니다. 클라이언트가 /test.jpg로 요청한다면 원본서버로 요청하는 주소는 example.com/dir1/test.jpg가 됩니다.
   - RefreshExpired 설정의 기본 값이 OFF에서 ON으로 변경되었습니다.
   - 파일캐싱 모니터링 항목이 강화되었습니다.
   - 원본서버 주소가 도메인명이라면 별도로 <Host>를 설정하지 않아도 도메인 명으로 Host헤더를 보내도록 수정하였습니다.
   - 다음과 같이 통계/성능 데이터가 추가되었습니다.
   - 원본/클라이언트 HTTP요청 개수가 통계에 추가되었습니다.
   - 정상적으로 완료된 원본/클라이언트 HTTP 트랜잭션의 통계가 추가되었습니다.
   - CPU와 Memory에 대한 통계가 추가되었습니다.
   - Disk별 성능지표가 추가되었습니다.
   - 원본로그에 cs-acceptencoding, sc-cachecontrol필드가 추가되었습니다.
   
**버그 수정**

   - 원본서버 배제/복구 과정(주소 3개 이상)에서 후순위의 원본서버가 우선 복구됐을 때 비정상 종료되던 증상
   - HTTP 요청에서 헤더가 키와 값 사이에 공백이 없으면 해석하지 못하던 증상
   - 로그를 "Size"로 설정했을 때 중간파일이 먼저 롤링되어 삭제되던 증상
   - 다음 상황에서 응답을 주지 않던 증상
   - A파일을 원본서버에 요청하였으나 404 Not Found가 발생
   - Memory Swap과정 중 A파일의 Body를 Memory에서 삭제 (A파일은 Meta만 존재하는 상태가 됨)
   - 원본서버 장애 판단으로 배제됨
   - A파일 서비스 요청이 들어옴
   - A파일이 서비스를 위해 Body를 Load하려고 하였으나 실패함. 파일 초기화 수행
   - A파일이 원본서버로 다운로드를 진행하려고 하였으나 원본서버 배제로 실패함
   - 이후 A파일은 초기화 시점을 잃어버리고 초기화 상태로 존재함
   - 다음 상황에서 Expire/Purge가 성공된 것처럼 나오고 갱신되지 않던 증상
   - A파일을 백그라운드로 갱신 시도함
   - 원본서버에서 HTTP응답을 받았으나 전송지연이 발생함
   - 전송지연으로 연결이 종료되거나 세션이 비정상 종료됐을 때 갱신실패가 제대로 정리되지 않는 상황이 발생함
   

v1.0.x
====================================

1.0.17 (2012.11.29)
----------------------------


   - HardPurge가 API로 추가되었습니다. HardPurge한 컨텐츠는 완전삭제를 의미하며 복구가 불가능합니다.
   - 가상호스트별로 클라이언트 Keep-Alive시간을 설정할 수 있습니다.

1.0.16 (2012.11.28)
----------------------------


   - SNMPWalk가 동작하도록 SNMP의 기능이 전체적으로 수정되었습니다.
   - SNMP의 [min]변수의 기본 값을 설정할 수 있습니다. SNMPWalk는 설정 값을 참조하여 [min]변수를 설정합니다.
   - 전체 가상 호스트이름을 붙여서 제공하던 설정(VHostList)이 삭제되었습니다.
   - 일부 OID값이 확장가능하도록 재조정되었습니다.
   
   - 루트(/) 디렉토리에 대한 Purge/Expire를 막도록 설정할 수 있습니다. 이 설정은 Purge2Expire보다 우선합니다.

1.0.15 (2012.11.22)
----------------------------


   - 정상적으로 캐싱(200 OK)되어 있는 파일을 갱신하는 과정에서 원본서버로부터 4xx응답을 받았을 때 마치 304 not modified를 받은 것처럼 동작하도록 설정합니다. 이를 통해 서버의 일시적인 장애로부터 컨텐츠를 갱신하는 행위를 방지할 수 있습니다.
   - 컨텐츠의 만료시간을 강제로 지정하는 ExpireAfter가 추가되었습니다.
   - 원본서버 주소에 포트가 같이 선언되어 있는 경우 포트바이패스가 되지 않던 문제가 수정되었습니다.
   - 누적통계가 ON인 상황에서 포트바이패스 통계를 집계하면 비정상 종료되던 문제가 수정되었습니다.

1.0.14 (2012.11.15)
----------------------------


   - 디렉토리별 통계를 설정했을 때 통계 모니터링 중 비정상종료 될 수 있는 문제가 수정되었습니다.
   - 커스텀 TTL 변경이 적용되지않던 증상이 수정되었습니다. 커스텀 TTL은 즉각적으로 반영되지 않고 TTL이 만료되는 시점에 재적용됩니다.

1.0.13 (2012.11.12)
----------------------------


   - 캐싱된 파일을 최초에 변경확인(If-Modified-Since)으로 접근할 경우 파일이 정상적으로 초기화되지 않던 버그가 수정되었습니다. 이 버그로 인하여 최초 응답시점에 500 Internal Error를 보내거나 TTL이 아주 짧게 설정되어 있는 경우 파일의 유효성이 문제가 될 수 있습니다.
   - RefreshExpired옵션이 ON인 경우 원본서버에서 컨텐츠가 변경되지 않았더라도(304 Not Modified) 최초 접근하는 클라이언트를 무조건 200 OK로 처리하던 증상이 수정되었습니다.
   - 정상적으로 캐싱(200 OK)되어 있는 파일을 갱신하는 과정에서 원본서버로부터 5xx응답을 받았을 때 마치 304 not modified를 받은 것처럼 동작하도록 설정합니다. 이를 통해 서버의 임시적인 장애때문에 컨텐츠를 무효화하여 원본 서버 트래픽을 가중시키는 행위를 방지할 수 있습니다.
   - SNMP에서 응답 받을 가상호스트의 최대 개수를 설정할 수 있습니다.

1.0.12 (2012.11.5)
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

1.0.5 (2012.10.8)
----------------------------


   - 원본서버 요청 시에 값이 존재하지 않는 QueryString항목이 누락되던 증상이 수정되었습니다.

1.0.4 (2012.10.4)
----------------------------


   - 원본서버 로그에 QueryString을 기록하지 않던 증상이 수정되었습니다.

1.0.3 (2012.9.28)
----------------------------


   - 설정파일을 리로드하여도 OriginOptions의 Host설정이 반영되지 않던 증상이 수정되었습니다.

1.0.2 (2012.9.27)
----------------------------

   - 설정파일을 리로드한 후 Custom TTL설정이 적용되지 않던 증상이 수정되었습니다.

1.0.1 (2012.9.20)
----------------------------

   - ApplyQueryString 설정이 ON인 경우 Purge/Expire가 과도하게 CPU를 점유하던 문제가 개선되었습니다.

1.0.0 (2012.9.18)
----------------------------

   - 설정파일을 동적으로 Reload할 수 있습니다. 서비스 중단 없이 가상호스트 추가, 삭제, 변경이 가능합니다.
   - 하드디스크의 최대사용량을 설정할 수 있습니다. 설정하지 않아도 언제나 디스크가 꽉차지 않도록 관리됩니다.
   - 가상호스트의 순서가 변경되더라도 항상 동일한 SNMP의 OID로 통계를 수집할 수 있도록 가상호스트의 OID를 고정할 수 있습니다.
   - Access 로그를 Apache와 Microsoft IIS형식으로 설정할 수 있습니다.
   - HTTP응답에 Via헤더 삽입을 설정할 수 있습니다.
   - 클라이언트의 Accept-Encoding을 무시하도록 설정할 수 있습니다.
   - 콘솔 또는 API를 통해 STON 버전확인이 가능합니다.
   - API를 통해 설정파일 열람이 가능합니다.
   - 원본서버 로그에 QueryString을 기록합니다.
   - SSL을 통한 HTTP Post요청 바이패스가 오동작하던 버그가 수정되었습니다.
   - 가상호스트 서비스 포트설정이 <Address>에서 <Listen>으로 변경되었습니다.
   - 가상호스트별로 디스크 설정을 별도로 할 수 없습니다. 모든 가상호스트는 <Storage>를 통해 디스크를 공유하도록 변경되었습니다.
   - Info로그가 보기 쉬운 형식으로 변경되었습니다.
   - fileinfo응답의 시간표현이 "2012.09.03 14:29:50" 같이 읽기쉬운 형태로 변경되었습니다.


v0.9.x
====================================

0.9.6.7 (2012.8.23)
----------------------------

   - 바이패스 중 원본과 클라이언트 세션이 동시에 끊어질 때 STON이 비정상 종료되던 버그 수정

   - 원본서버가 "Transfer-Encoding: chunked"로 응답을 줄 때 Receive Timeout이 짧게 지정되던 버그 수정

   - API응답의 MIME 타입을 application/json에서 text/plain으로 변경

0.9.6.6 (2012.8.1)
----------------------------

   - 특정 IP의 서비스(가상호스트) 접근을 차단 또는 허가하도록 설정할 수 있습니다.
   - 원본서버가 과부하 상태라고 판단되면 만료된 컨텐츠의 TTL을 원본서버에게 물어보지 않고 자동연장합니다.
   - GET요청의 기본동작을 원본서버로 바이패스하도록 설정할 수 있습니다.
   - Origin로그에 바이패스 된 요청인지 기록합니다.
   - 바이패스 세션의 접속실패, 전송실패 시간을 설정할 수 있습니다.

0.9.6.5 (2012.7.17)
----------------------------

   - 원본서버를 Active/Standby로 설정할 수 있습니다.
   - Access로그에 클라이언트의 Range필드(cs-range)추가
   - HTTP요청이 Invalid Range를 요청하는 경우 동작방식을 변경하였습니다. 기존에는 파일 크기를 벗어난 Range요청은 무조건 416 Requested Range Not Satisfiable으로 처리됐습니다. 이번 버전부터는 끝 오프셋이 파일 크기보다 클 경우 206 Partial Content로 처리됩니다. 시작 오프셋이 파일 크기보다 큰 경우는 기존과 동일하게 처리됩니다.

0.9.6.4 (2012.7.12)
----------------------------

   - HTTP POST요청 처리시 비정상 종료되던 문제를 수정하였습니다.
   - HTTP POST요청의 원본서버 바이패스 여부를 설정할 수 있습니다.
   - 원본서버 HTTP 응답에 Content-Type헤더가 명시되어 있지 않은 경우 클라이언트에게도 Content-Type헤더를 주지 않습니다. (기존에는 text/html로 설정)

0.9.6.3 (2012.7.11)
----------------------------

   - HTTPS 요청을 원본서버로 바이패스할 때 잘못된 메모리 참조로 인하여 오동작/비정상 종료되던 문제가 수정되었습니다.
   - 투명(Transparent) 모드를 지원합니다. STON과 원본서버 네트워크 구간 사이에 원본서버의 응답을 STON으로 포워딩하는 설정이 필요합니다.
   - Expired된 컨텐츠를 서비스하기 전에 반드시 원본 갱신여부를 확인하도록 할 수 있습니다.
   - 더 이상 URLBypass통계를 별도로 수집하지 않습니다. 원본/클라이언트 트래픽 통계로 통합되었습니다.
   - IBM WebLogic에서 클라이언트 Access로그를 남길 수 있도록 WL-Proxy-Client-IP 헤더를 추가할 수 있습니다.
   - 원본서버로 보내는 HTTP요청의 X-Forwarded-For헤더의 클라이언트 IP이후를 삭제할 수 있습니다.
   - 에러 페이지(500 Internal Error)에서 에러이유를 표시합니다.
   - 설정에서 문자열의 공백을 제거하지 않던 문제가 수정되었습니다. 모든 문자열의 좌우공백은 제거됩니다.

0.9.6.2 (2012.6.19)
----------------------------

   - 캐싱되어 있지 않은 파일의 가장 마지막 부분을 Range Request했을 때(Range의 범위가 1024 Bytes미만) 데이터가 전송되지 않던 버그 수정

0.9.6.1 (2012.6.14)
----------------------------

   - CacheClear 기능 추가 - 로 설정된 모든 디스크를 삭제합니다. STON의 모든 서비스는 중단되며 작업이 완료된 뒤 자동으로 재개됩니다. 
     ``http://127.0.0.1:10040/command/cacheclear`` 
   - 로그 파일의 OriginOptions의 Host설정 누락이 수정되었습니다.
   - 로그 파일의 Options설정표현이 "TTL"에서 "Options"로 변경되었습니다.

0.9.6 (2012.6.12)
----------------------------

   - SNMP(Simple Network Monitoring Protocol)가 지원됩니다. STON은 항상 실행경로에 MIB(Management Information Base)파일을 생성합니다. STON의 SNMP는 가상호스트별, 실시간, 최근 1~60분까지의 통계를 제공합니다. 최초 실행시 비활성화되어 있으며 server.xml을 편집해 활성화 시킬 수 있습니다::

      <Server>
         <Host>
            <SNMP Port="161" Status="Active">
               <Allow>211.104.97.150</Allow>
            </SNMP>
         </Host>
      </Server>


   - 원본서버에서 Content Length없는 응답이 올 경우, Origin로그에 원본서버 에러로 기록하지 않도록 변경되었습니다. 원본서버에서 일방적으로 연결을 종료한 경우, 만약 해당 세션이 Content Length가 없는 HTTP 트랜잭션을 수행 중이었다면 원본에러로 기록되지 않습니다.