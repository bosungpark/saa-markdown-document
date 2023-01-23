프라이빗, 퍼블릭, 탄력적 IP
-
- IPv4 : 온라인에서 대중적인 IP 형태
- IPv6 : IoT에서 많이 이용되는 형태


- 프라이빗 IP: 
  - 사설 네트워크 안에서만 작동하며, IP는 사설 네트워크 안에서만 유일하면 된다. 기기가 재부팅되면 변할 수 있다.
- 퍼블릭 IP: 
  - 인터넷에서 식별자로써 작동하고, 전체 웹 생태계에서 유일해야한다.
- 탄력적 IP: 
  - EC2 인스턴스를 시작하고, 중지할 때 공용 IP를 바꿀 수 있다. 
  - 어떤 이유에서건 공용 IP를 사용하면 탄력적 IP가 필요하게 된다. 
  - 한 번에 한 인스턴스에만 첨부할 수 있고, 삭제하지않으면 유지된다.
  - 한 인스턴스에서 다른 인스턴스로 주소를 옮김으로써, 실패를 마스킹할 수 있다.
  - 개정당 5개까지 가능하다.

EC2 배치그룹
-
- Placement Group
  - EC2 인스턴스가 AWS 인프라에 배치되는 방식을 제어하고자 할 때 사용 
  - 전략
    - Cluster: low latency group in a single Availablility Zone.
      - 모든 인스턴스가 같은 하드웨어, 가용영역, 렉에 존재.
      - 랙 즉, 하드웨어서 FAIL하면 모든 인스턴스가 실패한다.
      - 빠른 처리 속도와 처리량으로 BIG DATA 처리 가능.
    - Spread: spread instances across underlying hardware (max 7 instance per group per AZ) - critical application
      - 모든 EC2 인스턴스는 다른 하드웨어에 위치한다.
      - 동시적 실패의 위험을 줄일 수 있다.
      - 배치그룹의 AZ마다 7개의 인스턴스로 제한된다.
      - 가용성을 극대화하고, 위험을 줄일 필요가 있는, 어플리케이션의 실패가 반드시 격리되어 관리되어야하는 어플리케이이션에서 사용한다.
    - Partiion: spread instances across many different partition with in an AZ, Scales to 100 of EC2 per group (Hadoop, Cassandre, Kafka)
      - 각각의 파티션은 렉을 의미한다, 파티션이 많으 인스턴스가 많은 하드웨어로 분리되어 렉실패의 리스크가 분산된다
      - 가용영역 최대 7개의 인스턴스가 가능하고, 동일한 리전의 여러 가용영역에 걸쳐있을 수 있다.
      - 설정상 수백개의 인스턴스를 가질수 있으며, 이점이 분산배치와의 차이점이다.
      - 인스턴스의 위치를 알기위한 메타 데이터를 가지고 있다.

탄력적 네트워크 인터페이스(ENI)
-
- Logical component in a VPC that represents a virtual network card
  - The ENI can have the following attributes:
    - Primary private IPv4, one or more secondary IPv4
    - Oner Public IPv4
    - One or more security groups
    - A MAC address
  - You can create ENI independently and attach them on the fly on EC2 instnaces for failover
  - Bound to specific available zone

EC2 Hibernate(절전 모드)
-
- we know we can stop and terminate instances
- EC2 Hibernate preserves in memory(RAM) state which makes instance boots faster!
- under the hood, RAM states is written in the file in the (root) EBS volume
- so EBS must be encrypted

- Use cases
  - Long-running process
  - Saving RAM state
  - Services that take some times to initialize