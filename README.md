# AWS

### EC2 (Elastic Compute Cloud)

Amazon Elastic Compute Cloud (EC2) 는 안전하고 크기 조정이 가능한 컴퓨팅 파워를 클라우드에서 제공하는 웹 서비스입니다. 개발자가 더 쉽게 웹 규모의 클라우드 컴퓨팅 작업을 할 수 있도록 설계되었습니다.

Amazon EC2 의 간단한 웹 서비스 인터페이스를 통해 `간편하게 필요한 용량`을 얻고 구성할 수 있습니다. 컴퓨팅 리소스에 대한 포괄적인 제어권을 제공하며, Amazon 의 컴증된 컴퓨팅 인프라에서 실행할 수 있습니다.
 
Amazon EC2 는 새로운 인스턴스를 획득하고 부팅하는데 `필요한 시간을 단 몇 분` 으로 단축하므로 컴퓨팅 요구 사항의 변화에 따라 `신속하게 용량을 확장하거나 축소` 할 수 있습니다. 또한 `실제 사용한 만큼만 요금을 지불`하면 되므로, 컴퓨팅 비용이 절감됩니다. Amazon EC2는 개발자가 `장애에 대한 복원력이 뛰어나고` 일반적인 오류 상황에 영향을 받지 않는 애플리케이션을 구축할 수 있도록 도구를 제공합니다.

- On-Demand : 실행하는 인스턴스에 따라 시간 또는 초당 컴퓨팅 파워로 측정된 가격을 지불
    - 약정은 필요 없음
    - 장기적인 수요 예측이 힘들거나 유연하게 EC2를 사용하고 싶을 때
    - 한번 써보고 싶을 때
- Spot Instance : 경매 형식으로 시장에 남는 인스턴스를 저렴하게 구매해서 쓰는 방식
    - 최대 90% 정도 저렴
    - 단 언제 도로 내주어야 할지 모름
    - 시작 종료가 자유롭고나 추가적인 컴퓨팅 파워가 필요한 경우
- 예약 인스턴스 (Reserved Instance - RI) : 미리 일정 기간 (1년 ~ 3년) 약정해서 쓰는 방식
    - 최대 75% 정도 저렴
    - 수요 예측이 확실할 때
    - 총 비용을 절감하기 위해 어느정도 기간의 약정이 가능한 사용자
- 전용 호스트 (Dedicated) : 실제 물리적인 서버를 임대하는 방식
    - 라이선스 이슈 (Window Server등)
    - 규정에 따라 필요한 경우

<br>

---
<br>

### EBS (Elastic Block Store)

Amazon Elastic Block Store (EBS)는 AWS 클라우드의 Amazon EC2 인스턴스에 사용할 영구블록 스토리지 볼륨을 제공합니다. 각 Amazon EBS 볼륨은 가용 영역 내에 자동으로 복제되어 구성요소 장애로부터 보호해주고, 고가용성 및 내구성을 제공합니다. Amazon EBS 볼룸은 워크로드 실행에 필요한 지연 시간이 짧고 일관된 성능을 제공합니다. Amazon EBS 를 사용하면 단 몇 분 내에 사용량을 많게 또는 적게 확장할 수 있으며, 프로비저닝한 부분에 대해서만 저렴한 비용을 지불합니다.

- EBS Based : 반 영구적인 파일의 저장 가능
    - Snapshot 가능
    - 인스턴스 업그레이드 가능
    - STOP 이 가능함
- Instance Sroage : 휘방성이나 빠른 방식
    - 빠르지만 저장이 필요 없는 경우
    - STOP 이 불가능함

### AMI (Amazon Machine Image)

Amazon 머신 이미지 (AMI)는 인스턴스를 시작하는 데 필요한 정보를 제공합니다. 인스턴스를 시작할 때 AMI 를 지정해야 합니다. 동일한 구성의 인스턴스가 여러 개 필요할 때는 한 AMI에서 여러 인스턴스를 시작할 수 있습니다. 서로 다른 구성의 인스턴스가 필요할 때는 다양한 AMI를 사용하여 인스턴스를 시작하면 됩니다.

- AMI 는 다음을 포함합니다.
    - 1개 이상의 EBS 스냅샨 또는, 인스턴스 저장 지원 AMI 의 경우, 인스턴스의 루트 볼륨에 대한 템플릿 (예: 운영 체제, 애플리케이션 서버, 애플리케이션)
    - AMI 를 사용하여 인스턴스를 시작할 수 있는 AWS 계정을 제어하는 시작 권한
    - 시작될 때 인스턴스에 연결한 볼륨을 지정하는 블록 디바이스 매핑

---

### Security Group

보안 그룹은 인스턴스에 대한 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽 역활을 합니다.
VPC 에서 인스턴스를 시작할 때 `최대 5개의 보안 그룹` 에 인스턴스를 할당할 수 있습니다. 
보안그룹은 `서브넷 수준이 아니라 인스턴스 수준에서 작동`하므로 VPC 에 있는 서브넷의 각 인스턴스를 서로 다른 보안그룹 세트에 할당할 수 있습니다. 시작할 때 특정 그룹을 지정하지 않으면 인스턴스가 자동으로 VPC 의 기본 보안 그룹에 할당됩니다. 

- 보안장치
    - Network Access List (NACL) 와 함께 방화벽의 역활을 하는 서비스
- PORT 허용
    - 트래픽이 지나갈 수 있는 `Port` 와 `Source` 를 설정 가능
    - Deny 는 불가능  ->  `NACL` 로 가능함
- 인스턴스 단위
    - 하나의 인스턴스에 하나 이상의 SG설정 가능
    - NACL 의 경우 서브넷 단위
    - 설정된 Instance 는 설정한 모든 SG의 룰을 적용 받음
- 설정된 모든 룰을 사용해서 필터링
    - NACL의 경우 적용된 룰의 순서대로 필터링
- Stateful
    - Inbound 로 들어온 트래픽이 별 다른 Outbound 설정 없이 나갈 수 있음
    - NACL 은 Stateless
- Stateless / Stateful 
    - Stateless : client 와 server 의 동작, `상태정보를 저장하지 않는 형태`, server의 응답이 client와의 세션 상태와 독립적임
        - 장점 : 서버가 client정보를 저장관리 하지 않으므로 Scaling이 자유로움
    - Stateful : client와 server의 동작, `상태정보를 저장하는 형태`, 세션 상태에 기반하여 server의 응답이 달라짐

---

### ELB (Elastic Load Balancer)

Elastic Load Balancing 은 들어오는 애플리케이션 트래픽을 Amazon EC2 인스턴스, 컨테이너, IP주소, Lambda 함수와 같은 여러 대상에 자동으로 `분산` 시킵니다. Elastic Load Balancing 은 단일 가용 영역 또는 여러 가용 영역에서 다양한 애플리케이션 부하를 처리할 수 있습니다. Elastic Load Balancing 이 제공하는 세 가지 로드 밸런서는 모두 애플리케이션의 내결함성에 필요한 `고가용성, 자동확장/축소, 강력한 보안` 을 갖추고 있습니다. 

- ELB 의 특징
    - IP 가 지속적으로 바뀜
        - 지속적으로 IP주소가 바뀜
        - 따라서 도메인 기반으로 사용해야 함
    - Health Check
        - 직접 트래픽을 발생시켜 Instance 가 살아있는지를 체크함
        - InService, OutoService 두가지 상태로 나누어 짐
    - 3가지 종류가 존재함
        - Application Load Balancer
        - Network Load Balancer
        - Classic Load Balancer
- ELB 의 종류
    - Application Load Balancer
        - Application Level
        - "똑똑한 놈"
    - Network Load Balancer
        - "빠른 놈"
        - Elastic IP 할당 기능
    - Classic Load Balancer
        - "옜날 놈"
- Sticky Session
    - 첫 request에 대한 응답을 준 서버에 껌딱지처럼 붙어있는 것!
    - 특정 세션의 요청을 처음 처리한 서버로만 보내는 것
    

#### Vertical Scale

수직 확장 은 요청 시 서버에 더 많은 리소스(CPU/RAM/DISK)를 추가하는 것을 의미한다. (데이터베이스 또는 애플리케이션 서버는 여전히 하나임). 

Vertical Scaling 은 중소기업은 물론 중견기업의 애플리케이션 및 제품에서 가장 일반적으로 사용됩니다. Virtual Scaling 의 가장 일반적인 예 중 하나는 값비싼 하드웨어를 구입하여 VMWare ESX(가상 머신 하이퍼바이저)로 사용하는 것입니다.

수직적 확장 은 일반적으로 서버 하드웨어의 업그레이드를 의미합니다. 수직으로 확장해야 하는 몇 가지 이유에는 IOPS(입력/출력 작업) 증가, CPU/RAM 용량 및 디스크 용량 확장이 포함됩니다.

그러나 가상화를 사용한 후에도 성능 향상을 목표로 할 때마다 수평 확장을 사용하는 것보다 가동 중지 시간의 위험이 훨씬 더 큽니다.

#### Horizontal Scale

수평적 확장 은 (서버) 서비스의 고가용성이 필요할 때마다 반드시 사용해야 하는 기술입니다.

수평 확장 에는 서버나 데이터베이스에 처리 장치나 물리적 시스템을 더 추가하는 작업이 포함됩니다. 여기에는 클러스터의 노드 수를 늘리고 키 공간을 더 넓게 확장하고 클라이언트 연결을 위한 추가 끝점을 제공하여 각 구성원 노드의 책임을 줄이는 것이 포함됩니다. 수평적 확장은 역사적으로 높은 수준의 컴퓨팅과 애플리케이션 및 서비스에 훨씬 더 많이 사용되었습니다.

이는 개별 노드의 용량에 영향을 미치지는 않지만 개별 서버 노드 간의 분산으로 인해 부하가 감소합니다.

---

### Auto Scaling

`AWS Auto Scaling` 은 애플리케이션을 모니터링하고 용량을 자동으로 조정하여, `최대한 저렴한 비용`으로 `안정적`이고 예측 가능한 성능을 유지합니다. AWS Auto Scaling 을 사용하면 몇분 만에 손쉽게 여러 서비스 전체에서 여러 리소스에 대해 애플리케이션 규모 조정을 설정 할 수 있습니다.

#### EC2 Auto Scaling 의 목표
- 최소한의 인스턴스 사용 (비용)
- 원하는 만큼의 인스턴스 개수를 목표로 유지 (안정성)
- 최대 인스턴스 개수 이하로 인스턴스를 유지 (돈)
- Availability Zone 에 골고루 분산될 수 있도록 인스턴스를 분배 (안정성)
- 항상 서비스가 유지될 수 있는 인스턴스를 확보 (안정성)

#### EC2 Auto Scaling 의 구성
- Launch Configuration : `무었을` `어떻게` 실행시킬 것인가?
    - EC2 의 타입, 사이즈
    - AMI
    - Security Group, Key, IAM
    - User Data
- Monitoring : `언제` 실행시킬 것인가? + 상태확인
    - Ex) : CPU 점유율이 일정 % 을 넘어섰을 때 추가로 실행 or 2개 이상이 필요한 스택에서 EC2 하나가 죽었을때
    - Cloud Watch (And/Or) ELB 와 연계
- Desired Capacity : `얼만큼` 실행 시킬 것인가?
    - Ex) : 최소 1개 ~ 최대 3개
- Lifecyle Hook : 인스턴스 시작/종료시 Callback
    - 다흔 서비스와 연계하여 전/후 처리 가능 -> CloudWatch Event/SNS/SOS
    - Teminating : wait/Terminating : Proceed 상태로 전환
    - 기본 3600초 동안 기다림

---
<br>

### IAM (Identity and Access Management)

IAM 을 사용하면 AWS 서비스와 리소스에 대한 엑세스를 안전하게 `관리` 할 수 있습니다. 또한, AWS 사용자 및 그룹을 만들고 관리하며 AWS 리소스에 대한 엑세스를 `허용 및 거부` 할 수 있습니다.

- AWS 어카운트 관리 및 리소스 / 유저 / 서비스 의 관한 제어
    - 임시 권한 부여
    - 서비스 사용을 위한 인증 정보 부여
- 유저의 생성 및 관리 및 계정의 보완
    - Multi-factor Authentication
    - 유저의 패스워드 정책 관리
- 다른 계정과의 리소스 공유
- Identify Federation (Facebook 로그인, 구글 로그인 등)

#### IAM 의 구성
1. 유저 : 실제 AWS 를 사용하는 사람
    - Access Key / Secret Access Key : 유저가 AWS 의 서비스를 사용하기 위한 인증정보
    - 유조명 / 패스워드 : 유저가 AWS 콘솔을 사용하기 위한 인증정보
2. 그룹 : 유저의 집합. 그룹에 속한 유저는 그룹에 부여된 권한을 행사할 수 있다.
3. 정책(policy) : JSON 형싱으로 정의되며 유저와 그룹, 자격이 무었을 할 수 있는지에 관한 문서
4. 자격(Role) : AWS 리소스에 부여하여 AWS 리소스가 무었을 할 수 있는지를 정의
    - 다른 자격에 대해서 신뢰관계를 구축 가능
    - 역활을 바꾸어 가며 서비스를 사용 가능

#### IAM 팁
- IAM 은 글로벌 서비스 ( -> Region 별 서비스가 아님)
    - STS (Session Token Service) 의 경우 Region 별 활성 / 비활성 처리 가능
- 계정에 별명 부여 가능 -> 로그인 주소 생성 가능
- 유저의 경우 루트 유저와 생성된 유저로 구분
    - 루트 유저의 경우 보안에 신경쓰기 (Multi-factor Authentication 등)
- 유저의 패스워드 보안 정책 변경 가능 (일정 시간마다 패스워드 변경 등)
- 최소한의 권한만을 허용하는 습관을 들이기 (Principle of least privilege)

---

### Simple Storage Service 
Simple Storage Service (Amaazon `S3`) 는 업계 최고의 확장성과 데이터 가용성 및 보안과 성능을 제공하는 `객체 스토리지` 서비스입니다. 즉, 어떤 규모 어떤 산업의 고객이든 이 서비스를 사용하여 웹 사이트, 모바일 애플리케이션, 백업 및 복원, 아카이브, 엔터프라이즈 애플리케이션, IOT디바이스, 빅 데이터 분석 등과 같은 다양한 사용 사례에서 원하는 만큼의 데이터를 저장하고 보호 할 수 있습니다. Amazone S3 는 사용하기 쉬운 관리 기능을 제공하므로 특정 비지니스, 조직 및 규정 준수 요구 사항에 따라 데이터를 조직화하고 `세부적인 엑세스 제어를 구성` 할 수 있습니다. Amazone S3 는 `99.99999%` 의 내구성을 제공하도록 설계되었으며, 전 세계 기업의 수백만 애플리케이션을 위한 데이터를 저장합니다.

#### S3 살펴보기
- 객체 스토리지 서비스
- 무제한 용량
- Bucket 이라는 단위로 구분
- 버전 관리 가능
- 99.999999% 내구성
- Static Web 호스팅 가능
- 업로드와 업데이트 / 삭제의 데이터 일관성 모델이 다름
- 여러 티어로 구성됨
- 암호화 기능
- 보안 설정 가능
- 다른 유저 / 다른 계정과 공유 가능
- 다른 Region 으로 복제 가능
- 수명 주기 설정 가능
- 삭제 방지 기능 (MFA) 
- 파일 전송 Transfer Acceleration 가능
- Athena / Macie 등의 서비스로 Query 및 검증 가능

<br>

##### 객체 스토리지 서비스
- 객체 스토리지 서비스 : 파일 만 가능 <-> Block Storage Service (EBS,EFS 등)
    - 파일 설치 불가
- 무제한 용량
    - 단 하나의 객체는 0byte 에서 5TB 의 용량
- Bucket 이라는 단위로 구분
    - 디렉토리의 개념
    - Bucket 이름은 Global Unique
    - 즉 전세계에 어디에도 중복된 이름이 존재 할 수 없음
    - Web Hosting 시 도메인과 Bucket 명이 같아야 함
- 99.999999999% 내구성
    - 0.000000001% 확률로 파일을 잃어버릴 수 있음
    - 로또 당첨확률 0.00000012277% (S3 로 파일을 잃어버릴 확률보다 많음 약 122배)
- 99.9% SLA 가용성 (티어에 따라 다름)

##### S3 API
- 파일 관련 API (업로드, 업데이트, 삭제 등)
    - 업로드 성공시 HTTP 200 코드 반환
    - 큰 용량의 파일의 경우 Multipart Upload 가능 (개당 5gb)
    - 다운로드는 Torrent 지원
- Bucket 관련 API (조화, 생성, 삭제 등)
- 기타 기능 (Lifecycle, Replication 등)

##### S3 객체의 구성
- key : 파일의 이름
- Value : 파일의 데이터
- Version Id : 파일의 버전 아이디
- Metaadata : 파일의 정보를 담은 데이터
- ACL : 파일의 권한을 담은 데이터
- Torrents : 토렌트 공유를 위한 데이터

##### S3 버저닝
- 모든 버전을 관리 (삭제 포함)
- 활성화 해야 함 (기본적으로 비활성화)
    - 한번 활성화시 비활성화 불가능
- 수명 주기 관리와 연동 가능

##### S3 Static Hosting
- 기본적으로 파일은 두가지 웹 URL 을 가지고 있음
    - https://`bucket-name`.s3.`Region`.amazonaws.com/`keyname`
    - https://s3.`Region`.amazonaws.com/`bucket-name`/`keyname`
- Static Web 호스팅 기능
    - Html / Javascript 등으로 구성된 Static (데이터가 변하지 않는) 사이트만 가능 -> React 등
    - 호스팅 비용이 (비교적) 저렴함
    - Serverless 구성의 기초
    - 동적인 데이터는 AJAX 등으로 해결 가능

##### S3 일관성 모델
- PUT (새로 생성) : 읽기 후 쓰기 (Read After Write)
    - 파일을 올리고 성공한 즉시 읽기 가능
    - 먼저 Put 한 요청이 우선권
- UPDATE / DELETE : 최종 일관성 ( Eventual Consistency)
    - 파일을 삭제하거나 업데이트 후 일정 시간 후에 결과가 반영됨 (1초 미만)
    - 원자성 확보 불가능

##### S3 티어
- S3 Standard
    - 99.99% 가용성
    - 99.999999999% 내구성
    - 여러 장소에 분산 보관
- S3 - IA (Infrequently Accessed)
    - 자주 사용되지 않는 데이터를 저렴한 가격에 보관
    - 데이터를 불러올 때마다 비용 지불
- S3 - One Zone IA 
    - IA 와 같으나 하나의 AZ 에만 저장됨
    - 덜 중요하고 자주 사용되지 않는 데이터
- S3 Intelligent Tiering
    - 머신 러닝을 사용해 자동으로 티어 변경
    - 퍼포먼스 손해 / 오버헤드 없음
- S3 - Glacier
    - 아카이브용 저장소
    - 저렴한 가격
    - 데이터를 가져오는데 (분 ~ 시간) 단위의 시간이 소요
- S3 - Glacier Deep Archive
    - 매우 쌈
    - 데이터를 가져오는데 12시간 정도 필요함

##### S3 보안 설정
- Bucket Policy
    - 버킷 단위
    - JSON 형식
- ACL (Access Control List)   
    - 파일 단위
- Access Log 전송 가능
    - 다른 버킷 혹은 다른 계정으로 전송 가능
- MFA 를 활용해 삭제 방지 가능

##### S3 암호화
- S3 의 데이터의 암호화는 3가지 암호화로 구성
    - On Transit : SSL / TLS (HTTPS)
    - At Rest
        - SSE S3 : S3 에서 알아서 암호화
        - SSE KMS : KMS 서비스를 이용해 암호화
        - SSE C : 클라이언트에서 제공한 암호를 통해 암호화
    - 클라이언트가 직접 암호화

##### S3 공유
- S3 의 공유는 3가지 방법으로 가능
- Bucket Policy / IAM 
    - 프로그램 엑세스만 가능
    - 버킷 단위
- ACL 
    - 프로그램 엑세스만 가능
    - 파일 단위
- IAM 크로스 어카운트
    - 콘솔 / 프로그램 엑세스 가능

##### S3 Cross Region Replication
- 다른 Region 으로 복제 가능
- 버저닝이 활성화 되어 있어야 함 (원본, 대상 모두)
- 동일한 Refion 으로 복제 불가능
- 복제 기능 활성화 전의 데이터는 복제 되지 않음
- 버전 삭제 혹은 파일 삭제는 복제되지 않음

##### S3 수명주기
- "~~시간이 지난후 ~~을 해라" 라는 명령
    - ex) : 30일이 지난후 삭제
    - ex) : 30일이 지난후 Glacier 로 옮기기
- 버전과 연동 가능
- 예전 버전과 현재 버전에 대해 설정 가능
- 파일이 업로드 / 삭제 / 업데이트 되었을때 Lamdba 호출 가능

##### S3 Transfer Acceleration
- AWS 의 네트워크를 활용해 각 Edge Location 에서 더욱 빠른 업로드 가능

##### S3 Athena
- S3 를 SQL 언어로 조화할 수 있는 서비스
    - SQL 쿼리 사용
    - Serverless
    - 로그를 조회하거나 분석하는데 주로 사용

### Storage Gateway
AWS Storage Gateway 는 사실상 무제한의 클라우드 스토리지에 대한 온프레미스 엑세스 권한을 제공하는 하이브리드 클라우드 스토리지 서비스입니다.  Storage Gateway 를 사용하는 고객은 하이브리드 클라우드 스토리지의 주요 사례인 스토리지 고나리 간소화 및 비용 절감 효과를 얻을 수 있습니다. 여기에는 테이프 백업을 클라우드로 이동하고, 클라우드 백업 파일 공유를 통해 온프레미스 스토리지를 최소화 하고, 온프레미스 애플리케이션의 AWS 데이터에 대한 짧은 지연 시간의 엑세스 권한을 제공하는 기능과 함께 다양한 마이그레이션, 아카이빙, 프로세싱, 재해 복구 사용 사례가 포함됩니다.
이러한 사용 사례를 지원하기 위해 `테이프 게이트웨이, 파일 게이트웨이 및 볼륨 게이트웨이` 와 같은 3가지 유형의 게이트웨이를 제공합니다. 애플리케이션은 `NFS, SMB 및 ISCCSI` 와 같은 표즌 스토리지 프로토콜을 사용하는 가상 머신 또느 하드웨어 게이트웨이 어플라이언스를 통해 이 서비스에 연결됩니다. 

- File Gateway (NFS, SMB)
    - NFS : Network File System (Linux)
    - SMB : Server Message Block (Window)
- Volume Gateway(iSCSI)
    - Stored Volumes
    - Cached Volumes
- Tape Gateway (VTL)

##### File Gateway
- NFS 마운트포이트로 전송받은 데이터를 S3 에 저장
    - 소유권, 퍼미션, 파일 생성 시간등은 S3 의 메타데이터로 저장
- S3 에 저장 후에는 S3 의 모든 기능 활용 가능
    - 이벤트 트리거를 통한 다른 서비스 (분석 서비스 등) 사용
    - 버저닝
    - 수명 주기 등등

##### Volume Gateway
- iSCSI 프로토콜을 통해 전달받은 데이터를 비동기적으로 EBS 스냅샷 형식으로 저장
    - 스냅샷은 Incremental -> 이전 스냅샷에서 바뀐 부분만 저장함
- Stored Volume : `모든 데이터를 로컬`에 저장하고 비동기적으로 AWS 에 백업
    - 1GB ~ 16TB
- Cached Volume : `자주 사용되는 데이터만 로컬`에 남겨두고 나머지는 모두 AWS 에 백업
    - 1GB ~ 32TB

##### Tape Geteway
- 이미 존재하는 Tape 기반 백업 어플리케이션을 위한 서비스
- iSCSI 디바이스로 백업
- NetBackup, Backup Exec 등등 기존의 백업 어플리케이션 사용 가능


---
<br>

### Auto Scaling

AWS Auto Scaling 은 애플리케이션을 모니터링하고 용량을 자동으로 조정하여, `최대한 저렴한 비용`으로 `안정적`이고 예측 가능한 성능을 유지합니다. AWS Auto Scaling 을 사용하면 몇분만에 손쉽게 여러 서비스 전체에서 여러 리소스에 대해 애플리케이션 규모 조정을 설정 할 수 있습니다.

#### EC2 Auto Scaling
- 최소한의 인스턴스 사용
- 원하는 만틈의 인스턴스 개수를 목표로 유지
- 최대 인스턴스 개수 이하로 인스턴스 유지
- Availablity Zone 에 골고루 분산될 수 있도록 인스턴스를 분배
- 항상 서비스가 유지될 수 있는 인스턴스를 확보

#### EC2 Auto Scaling 의 구성
- Launch Configuration : `무었을` `어떻게` 실행시킬 것인가
    - EC2의 타입, 사이즈
    - AMI
    - Security Group, Key, IAM
    - User Data
- Monitoring : `언제` 실행시킬 것인가? + 상태 확인
    - ex) : CPU 점유율이 일정 %을 넘어섰을 때 추가로 실행 or 2개 이상이 필요한 스택에서 EC2 하나가 죽었을때
    - Cloud Watch (And/Or) ELB 와 연계
- Desired Capacity : 얼만큼 실행 시킬 것인가?
    - ex : 최소 1개 ~ 최대 3개
- Lifecycle Hook : 인스턴스 시작 / 종료 시 Callback
    - 다른 서비스와 연계하여 전 / 후 처리 가능 -> CloudWatch Event / SNS / SQS
    - Terminationg : wait / terminating : Proceed 상태로 전환
    - 기본 3600초 (1시간) 동안 기다림