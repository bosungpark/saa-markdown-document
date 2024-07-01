
AWS 예산설정
-
- Root User에서 권한설정


Amazon EC2
-
- Elastic Compute Cloud = Infrastructure as a Service
  - options
    - Rentinf virtual machines (EC2)
    - Storing data on virtual drives (EBS)
    - Distributing load across machines (ELB)
    - Scaling the services using an auto-scaling group (ASG)
- sizing and config options
  - OS
  - CPU
  - RAM
  - storge space
    - network (EBS, EFS)
    - hardware (EC2 instance store)
  - network card; speed, Pubic IP address
  - Firewall rules: security group
  - Bootstrap script: EC2 user data
    - EC2 user data is used for bootstrap
    - runs with rootuser (runs with cmd: $ sudo)

Amazon EC2 생성
- watch the video

EC2 인스턴스 유형 기본사항
- name convnetion: {instance_type}{genration}.{sizr within the instance class}
- ex: r2.micro
- type
  - Gerneral Purpose
  - Compute Optimized
  - Memory Optimized
  - storage Optimized
  - ...

보안 그룹 및 클래식 포트 개요
- 보안그룹
  - Security Groups control how thraffic is allowed into or out of EC2
  - only contains allow rules
  - rules can reference by IP or by security group
  - 인바운드 트래픽(디폴트: 블럭)이 가능하면 아웃바운드(디폴트: 논블럭) 역시 가능해지는 매커니즘
  - 여러 인스턴스에 접근할 수 있고, 지역과 VPC 결합으로 통제되어 있으며, EC2 외부에 있다.
  - SSH 그룹을 위한 분리된 보안그룹을 관리하는 것이 좋다
- 클래식 포트
  - SSH, FTP, SFTP, HTTP, RDP ...

SSH 개요
- Linux 시큐어 셸
- 커맨드라인 인터페이스 유틸리티

SSH 실행
- watch the video

SSH 문제 해결
-
- 연결 시간 초과가 발생하는 경우 : 보안 그룹에 문제가 있는 경우 발생합니다. 모든 유형의 시간 초과(SSH뿐만 아니라)는 보안 그룹 또는 방화벽과 관련 있습니다. 보안 그룹이 다음과 같이 설정되었는지 확인하고, EC2 인스턴스에 올바르게 할당되었는지 확인해주세요.
- 연결 시간 초과 문제가 계속해서 발생할 경우: 위와 같이 보안 그룹이 올바르게 설정되었으나 여전히 연결 시간 초과 문제가 발생하는 경우, 회사 방화벽 또는 개인 방화벽이 연결을 차단한다는 뜻입니다. 다음 강의에서 설명하는 대로 EC2 Instance Connect를 사용하세요.
- 연결이 거부될 경우: 이는 인스턴스에는 도달할 수 있지만 해당 인스턴스에서 SSH 유틸리티가 실행되고 있지 않다는 뜻입니다.
  - 인스턴스를 재시작하세요.
  - 여전히 동작하지 않는다면, 인스턴스를 종료하고 새 인스턴스를 만드세요. 반드시 Amazon Linux 2를 사용하세요.
- 권한 거부(publickey,gssapi-keyex,gssapi-with-mic): 이는 다음의 두 상황에서 발생합니다.
  - 보안 키가 틀렸거나 보안 키를 사용하지 않는 경우입니다. EC2 인스턴스 구성을 확인하여 올바른 키를 할당했는지 확인하세요.
  - 잘못된 사용자를 사용할 경우에도 발생합니다. Amazon Linux 2 EC2 인스턴스에서 실행했는지 확인하고, ec2-user 사용자를 사용하고 있는지 확인하세요. SSH 명령어 또는 PuTTY 구성에서 ec2-user@<public-ip> (ex:ec2-user@35.180.242.162) 코드를 실행할 때 지정해야하는 사항입니다.
- 어제는 연결이 가능했는데 오늘은 되지 않습니다.
  - EC2 인스턴스를 중단했다가 오늘 다시 시작했을 경우, 이런 일이 발생할 수 있습니다. 이 경우, EC2 인스턴스의 퍼블릭 IP가 변경됩니다. 따라서 명령어 또는 PuTTY 구성에서 새 퍼블릭 IP로 업데이트하여 저장하세요.

EC2 인스턴스 연결
- watch the video

EC2 인스턴스 역할 데모
- watch the video

EC2 인스턴스 시작
- 
- EC2: 클라우드 안의 가상서버
- 옵션
  - 온디맨드: 짧은 기간, 정가, 비용 예상이 쉽다.
  - 예약: 1년이상 사용시 가능, 비용절감 가능
  - 스팟: 저렴한 단기 워크로드, 신뢰성이 비교적 낮음. 중요한 또는 DB관련 작업은 절대 하면 안됨.
  - 전용 호스트: 실제 서버를 가지고, 큰 통제를 가짐.

EC2 스팟 인스턴스
-
- 지불할 의향이 있는 최고가에 대해 정의하고,인스턴스 비용이 최고가보다 낮다면 계속 사용, 높다면 높은 기한 동안 중단, 큰 비용절감 가능.
- 종료를 원할 시, 스팟을 먼저 취소하고 인스턴스를 종료해야한다.
- spot-fleet: spot + (Optional) on+demand