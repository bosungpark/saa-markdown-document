IAM 소개: 사용자, 그룹, 정책 
-
- Concepts
  - IAM = Identity And Access Management, Global service
  - Root account -> 기본적으로 생성되며, 계정에 대한 모든 권한을 가져, 직접 사용되거나 공유되어서는 안된다.
    - 한 유저가 한 개 혹은 여러 그룹에 속할 수 있다. IAM은 이러한 그룹의 정의이다.
  - Permission
    - Users or Group can be assigned JSON docs called policy
    - the policy define the permission of users
    - In AWS least privileg principle is applyed; means users get minimum permissions they need

IAM 사용자 및 그룹 실습 
-
- watch the video
  - point
    - IAM User의 Account Id에는 alias를 붙일 수 있다.

IAM 정책
-
- watch the video
  - 상속
    - 그룹의 소속과 상관없이 인라인 정책을 적용할 수 있다.

IAM 정책 실습 
-
- watch the video

IAM MFA 개요
-
- Factors use in Securing Authentication
  - Password Policy
    - setup options
      - minimum pw lenth 
      - specfic char type
      - allow iam user change pw
      - set pw expiration
      - prevent reuse
      - ...
  - Muti Factor Authentication(MFA)
    - 비밀번호와 기기의 보안 장치의 결합
      - Virtual MFA device
      - Universal 2nd Factor(U2f) Security Key
      - Hardware Key Fob MFA device
      - Hardware Key Fob MFA device for AWS GovCloud (US)

AWS 엑세스 키, CLI 및 SDK
-
- How to accrss AWS
  - options
    - AWS Manangement Console (protected by pw + MFA)
    - AWS Command Line Interface (CLI : protected by access key)
    - AWS Software Developer Kit (SDK: for code, protected by access key)
  - Access Keys are through AWS Console -> **Do Not Share**

Window에서 AWS CLI 설정
-
- watch the video

Mac OS에서 AWS CLI 설정
-
- watch the video

Linux에서 AWS CLI 설정
-
- watch the video

AWS CLI 실습
-
- watch the video


AWS CloudShell Region 가용성
-
- watch the video
  - AWS CloudShell은 제공을 하지 않는 리전이 있다.

AWS CloudShell
-
- watch the video
  - AWS에서 제공하는 일종의 무료 터미널

AWS 서비스에 대한 IAM Role
-
- AWS 서비스가 사용하는 IAM Role
  - EC2와 같은 서비스를 우리의 기기에서 사용하기 위해 권한을 부여한다.

IAM Role 실습
-
- watch the video

IAM 보안도구
-
- watch the video
  - IAM Credential Report (account-level)
  - IAM Access Advisor (user-level)

IAM 보안도구 실습
-
- watch the video

IAM 모범 사례
-
- 루트 계정은 AWS를 설정할 때 외에는 사용하지 않는다
- 계정을 빌려주는 대신 User를 하나 만들어 권한을 주는 것이 좋다
- 강한 비밀번호 정책을 가진 그리고, MFA를 사용하는 것이 좋다
- AWS 서비스에 대한 역할과 권한을 설정하는 것이 좋다 (Role, Permission)
- CLI, SDK 등 프로그래밍적 접근을 할 때에는 Access Key를 반드시 사용하라 
- IAM Credential Report 를 통해 계정의 권한을 조회 및 수정할 수 있다
- 절대 IAM User와 Access Key는 공유해서는 안된다
