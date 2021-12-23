Client와 Server의 개념

### 2 TIER

서비스를 제공하는 서버와 데이터베이스 서버를 동시에 운영

1. 소규모 네트워크에 적합
2. 응답이 빠름
3. 구조가 간단
4. 관리의 편리
5. 보안이 취약할 수 있음

### 3 TIER

서비스 서버와 데이터베이스 서버 분리한 구조

1. 오류 발생에 대한 대응 용이
2. 부하의 분산
3. 웹서버와 DB의 다른 보안 적용 가능

실제로는 외부에서 접근가능한 DMZ 영역과(Web server; https 443) 내부영역(database server; mysql 3306 or mariadb)로 분리하여 보안을 강화한다.

### Port 

- 서비스를 구분하는 식별자
  1) System port(Well known port): 공통적으로 서버에 할당하는 포트
     ex) 80(HTTP), 443(HTTPS), 22(SSH), 53(DNS) 용도가 미리지정되어있음
  2) Aplication Port: 개별 회사들이 사용하는 port(1024~49151)
     ex) 3306(MySQL), 5432(PostgreSQL), 3389(RDP: MS의 원격접속)
  3) Dynamic Port: 클라이언트들이 사용하는 포트(49151~65536)
     Ex) Web Browser들이 사용하는 구간 (여러 탭을 사용할 경우 탭마다 할당)
- Packet filtering 방화벽 : IP주소와 Port를 기반으로 차단 또는 허용
- Screened Subnet(가려진 서브넷 = Internal Network)
  1. DMZ가 인터넷과 내부망의 사이에 배치되는 방식
  2. 금융권에서 주로 사용함.
- 네트워크 방화벽 : 네트워크의 중간에 배치해서 네트워크를 분하고 접근 통제 ex) 공유기
- 시스템 방화벽 : OS에 설치되어 있거나, Application 형태로 설치하는 방식

#### Quiz) HTML, Image 등을 전송하기 위한 프로토콜은? HTTP



### 서버 운영 방식

- Active-Standby : High-Availability => Active 상태의 서버가 죽으면 Standby 상태에 있던 서버가 Active로 전환된다.
- Load-Balancing(부하분산) : 여러 대의 서버에 부하를 분산 모든 서버가 요청 분산처리
- Auto Scaling : 활성화된 서버의 개수를 유지하거나, 트래픽이 증가하면 서버를 늘리고 트래픽이 감소하면 서버의 개수를 줄이는 방식, Cloud와 크게 관련이 있음.

### Master와 Slave

- Master와 Slave는 모두 동작하며
- 모든 정보는 Master로 들어온다(읽기/쓰기)
- Slave는 Master의 정보를 동기화, 읽기만 할 수 있다.

### MariaDB

- 오픈 소스 관계형 데이터 베이스 
- MySQL과 명령어와 Port 번호가 같다.
- 성능이 최고 70%로 정도 향상됨

### 문자

1) ASCII(American Standard Code ~~~)

   - 대문자, 소문자, 숫자, 특수문자
   - 128개 이하로 표현 가능 2의7승 = 7bit

2) EUC-kr 

   - Microsoft에서 만든 한글표현 문자셋(완성형에 기반)

3) UTF-8 로도 한글 표시 가능

   - Web, Linux, MySQL 등에서 사용하는 한글 표현 문자셋

   