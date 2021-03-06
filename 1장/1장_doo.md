# 비즈니스 민첩성

- 비즈니스 민첩성은 성공적인 기업을 만드는 데에 중요한 요소이다.
→ 아마존은 0.66초에 한번씩 배포를 진행한다.
- 변화하는 비즈니스를 빠르게 적용하여 사용자에게 개선된 서비스를 제공할 수 있다.

## 클라우드 인프라

클라우드 인프라는 서비스 개발에 필요한 인프라 요소를 클라우드 플랫폼 벤더를 이용하여 사용하는 것

- 이전에는 인프라 구성을 위해 서버실을 만들어 장비를 구입하고 네트워크를 연결하였기 때문에 시간과 비용이 많이 들어갔다.
→ 좋은 아이디어가 있어도 들어가는 코스트가 많기 때문에 빠르게 실행하기가 어렵고, 빨리 실행해서 런칭했다해도 성과가 좋지 않으면 인프라를 구축하는데 들어간 비용을 건지기 어려울 수 있다.
- 클라우드 인프라를 사용하면서 사용량에 따른 비용을 유연하게 조절할 수 있게되었다.
- 애플리케이션이 탑재되는 클라우드 인프라는 사용한 단위 만큼만 비용을 지불하므로 애플리케이션 블록이 작으면 작을수록 효율적이다.
→ ~~의문인 것이 어쨌든 그 작게 쪼개놓은 애플리케이션을 합치면 전체 덩어리 만큼의 비용이 드는건 똑같은거 아닌가? 작게 쪼개놓은 애플리케이션을 1,1,1 만큼 쓰는 것을 뭉치면 전체 큰 한 덩어리의 3을 사용하는 것과 같은거 아닌가?~~ 
→ 아래의 스케일 아웃 과정은 동일한 인스턴스를 복제해서 사용하기 때문에 만약 애플리케이션이 모두 뭉쳐져있어서 **큰 한 덩어리로 되어 있다면 복제했을 때 불필요하게 큰 인스턴스가 복제될 수 있다**. 그리고 이는 비용 부과로 이어져서 **불필요한 비용을 내야할 수 있기 때문에 애플리케이션 블록이 작을수록 효율적**이다.
- 사용량이 증가할 운영 시점이라면 서비스 비용을 유연하게 관리할 수 있다.

### 스케일 업과 스케일 아웃

- **스케일 업** : 기존 시스템 자체의 **물리적 용량을 증가**시켜 성능을 높이는 방법
- **스케일 아웃** : **기존 시스템과 용량이 같은 다수의 장비를 병행 추가**해서 가용성을 높이는 방법
→ **사용량을 분산시켜 전체적으로 장애 없이 운영**할 수 있다.

만약 쇼핑몰을 운영하는데 타임 세일 이벤트를 진행한다고 가정할 때, 전체 시스템의 늘어날 트래픽을 고려해서 우선 **스케일 업을 시도**할 수 있다. 하지만, **예상했던 트래픽을 초과하면 시스템이 다운될 위험**이 있다.

다음으로 **스케일 아웃을 시도**해볼 수 있다. **CPU나 메모리의 트래픽 양이 지정한 수치 이상으로 증가**하면 **인스턴스를 설정된 개수로 복제해서 증가**시킨다. 그러면 **늘어난 인스턴스로 트래픽이 적절히 분산**되어 나뉠 것이다.

⇒ 인스턴스 자체의 크기가 큰 상황에서는 스케일 아웃을 시도했을 때 불필요하게 큰 크기의 인스턴스가 복제될 수 있다. 그래서 큰 한 덩어리의 애플리케이션을 운영했을 때 스케일 아웃 과정에서 불필요한 비용이 부과되어 애플리케이션을 작게 가져가는 것이 비용적인 측면에서 더 유리하다고 한 것 같다.

[ 예시 ]

**기존 전체 시스템의 크기가 16G** 라고 할 때, 해당 인스턴스를 스케일 아웃하면 **16G 짜리의 인스턴스를 여러개 복제**해야한다. (기존 시스템과 용량이 같은 크기의 장비를 추가하므로 16G씩 증가) 

하지만, **부하가 많은 애플리케이션을 쪼개서 4G 크기로 만들었을 때**, 부하가 많을 것 같은 애플리케이션만 스케일 아웃하면 되기 때문에 **4G 짜리 인스턴스를 여러개 복제**하여 사용하면 된다.

### 클라우드 프렌들리 / 클라우드 네이티브

**클라우드 프렌들리** : 큰 덩어리로 클라우드 환경에 올라가 수 있게만 한 애플리케이션

**클라우드 네이티브** : 독립적으로 분리되어 배포될 수 있는 조각으로 구성된 애플리케이션. 클라우드 인프라에 가장 어울리고 효과적이라는 의미로 클라우드 네이티브라고 부른다.

- 궁극적으로 **클라우드 프렌들리 → 클라우드 네이티브**로 가는 것이 효율적이다.

# 마이크로 서비스

## 모노리스 VS 마이크로 서비스

### 모노리스

**하나의 단위로 개발되는 일체식 애플리케이션**

- **3티어로 구성** : 클라이언트(사용자 인터페이스) + 서버(모노리스) + 데이터베이스
- 아무리 **작은 변화**에도 새로운 버전으로 **전체를 빌드해서 배포**해야 한다.
- 단일 프로세스에서 실행되기 때문에, 확장이 필요한 경우 특정 기능만 확장할 수 없고 **반드시 전체 애플리케이션을 동시에 확장**해야 한다.
→ 보통 로드 밸런서를 앞에 두고 여러 인스턴스 위에 큰 덩어리를 복제해 수평으로 확장한다.
- 여러개의 모노리스를 수평으로 확장했기 때문에 **여러 개의 모노리스 시스템을 전부 다시 빌드하고 배포**해야 한다.
- 또한, **데이터베이스는 통합되어 하나만** 있기 때문에 **탄력적 대응이 어렵고, 사전에 성능을 감당하기 위한 스케일 업을 해둬야한다.**

### 마이크로 서비스

**여러 서비스 인스턴스가 모여 하나의 비즈니스 애플리케이션을 구성한 것**. 서버 측이 여러 개의 조각으로 구성되어 별개의 인스턴스로 로딩된다.

- **각기 데이터베이스가 달라서** 업무 단위로 **모듈 경계가 명확하게 구분**된다.
- 따라서 확장 시에 특정 기능별로 **독립적으로 확장이 가능**하다.
→ A, B, C 기능 중에 B만 확장하고 싶으면 B 인스턴스만 스케일 아웃하면 된다.
- 특정 서비스를 변경할 필요가 있다면 **해당 서비스만 빌드해서 배포**하면 된다.
- 각 서비스가 독립적이기 때문에 **서로 다른 언어로 개발하는 것이 가능**하다.
→ 서비스의 소유권을 분리해 서로 다른 팀이 개발 및 운영할 수 있다.

## SOA 와 마이크로 서비스

공통점 : 여러 개의 응집된 비즈니스 서비스의 집합으로 시스템을 개발한다는 점에서 비슷하다.

### SOA

- **구체적이지 않고 이론적**이며, 실제 비즈니스 **성공 사례가 많지 않다.**
- **데이터베이스 분리를 하지 못했다.**
→ **데이터의 강한 결합**으로 애플리케이션도 독립적으로 사용하기 힘들었다.

### MSA

- **클라우드 인프라 기술의 발전과 접목되어** 아마존과 넷플릭스에 의해 구체화되고 비즈니스 성공 사례로 알려져있다. 
→ **클라우드 인프라의 등장**으로 **하드웨어를 유연하게 다룰 수 있게 되면서 실현**됐다.
- **각 서비스 별로 데이터베이스(저장소)가 분리**되어있다. → (서비스 + 데이터베이스) 세트로 구성
- **다른 서비스 및 데이터베이스와 격리**되어 있으며, **API를 통해서 느슨하게 결합**되어 있다.
- **독립적 확장**이 가능하고, **독립적으로 배포**가 가능하다.
- 서비스 별로 언어와 저장소를 선택할 수 있다. → **폴리글랏(Polyglot)**하다.
→ 이처럼 특정 서비스를 구축하는 데 사용하는 언어나 저장소를 자율적으로 선택할 수 있는 방식을 '폴리글랏하다'라고 말한다.

**[ MSA에 있고, SOA에 없는 2가지 ]**

1. **서비스별 저장소를 분리**해서 **다른 서비스가 저장소를 직접 호출하지 못하도록 캡슐화**한다.
→ 다른 서비스에 **접근할 수 있는 수단은 API 뿐**이다.
2. **REST API와 같은 가벼운 개방형 표준**을 사용해 **각 서비스가 느슨하게 연계되고 누구나 쉽게 사용**할 수 있다.
→ REST API가 가볍다는 의미 : SOA에 사용되는 SOAP 프로토콜과 XML 보다 **HTTP 프로토콜과 JSON 데이터 형태가 단순하고 쉽다는 의미**이다.

# 마이크로 서비스를 위한 조건

**MSA의 성공**이 단순히 기술에만 의존한 아키텍처 스타일을 추구하는 데 그치지 않고, **개발 환경, 문화, 일하는 방식과도 연관이 있음**을 보여준다.

### 조직의 변화 : 업무 기능 중심 팀

역할 또는 기술별로 팀이 분리되는 것이 아니라 **업무 기능을 중심**으로 **기술이 다양한 사람들이 하나의 팀**이 되어 서비스를 만드는 것 

- 서버 개발팀, 클라이언트 개발팀, 디자인팀과 같이 모여있는 것이 아닌 한 팀에 서버 개발자, 클라이언트 개발자, 디자이너가 모두 있는 팀
→ 하나의 마이크로 서비스를 만드는 데에 필요한 기능과 기술을 팀 내부에 모두 가지고 있다
- **같은 공간, 같은 시간을 공유**하기 때문에 **의사소통도 원활하고 의사결정도 빠르게 진행**될 수 있다.

### 관리체계의 변화 : 자율적인 분권 거버넌스, 폴리글랏

- 중앙의 강력한 거버넌스를 추구하지 않고, **팀별로 효율적인 방법론과 도구, 기술을 찾아 적용**한다.
- 각 팀의 도메인에 적합한 **언어와 저장소를 선택**할 수 있다. → 폴리글랏 프로그래밍, 폴리글랏 저장소

### 개발 생명 주기의 변화 : 프로젝트가 아닌 제품 중심으로

- 비즈니스의 갑작스러운 트렌드 변화에 유연하게 대처해야한다.
- 개발 뿐만 아니라 운영을 포함한 소프트웨어의 전체 생명주기를 책임진다.
- 폭포수 모델 혹은 빅뱅 방식으로 진행하는 것이 아니라, 애자일 개발 방식을 채용한다.
→ 2~3주 단위의 스프린트를 통해 소프트웨어를 개발 및 배포해서 바로 피드백을 받아 제품에 반여할 수 있도록 한다.

### 개발 환경의 변화 : 인프라 자동화

- 개발이 완료된 이후애 필요한 빌드, 테스트, 배포와 같은 개발지원과정의 속도를 높이는 것이 중요하다.
- 빌드/배포 파이프라인은 일반적으로 '소스코드 빌드 → 개발환경 배포 → 스테이징 → 환경 배포 → 운영 환경 배포'로 구성된다.
- **Infra as Code (IaC)** : '코드'를 이용해 인프라 구성부터 애플리케이션 빌드, 배포를 정의하는 것
→ 수많은 하드웨어 리소스 설정을 동일하게 통제할 수 있으며, 좋은 코드를 재활용하거나 다른 사람에게 공유가 가능하여 인프라를 효율적으로 관리할 수 있다.

### 저장소의 변화 : 통합 저장소가 아닌 분권 데이터 관리

- **각 저장소가 서비스별로 분산**되어 있어야 하며, **다른 서비스의 저장소를 직접 호출할 수 없고** **API를 통해서만 접근**해야 한다. → 폴리글랏 저장소

**[ 문제점 ]**

비즈니스 처리를 위해 일부 데이터의 복제와 중복 허용이 필요한 경우에, `데이터 일관성 문제`가 생긴다.
→ 각 마이크로 서비스의 저장소에 담긴 **데이터의 비즈니스 정합성을 맞춰야하는 문제**

예를 들어, 주문 서비스와 배송 서비스가 있고 각 저장소가 분리되어 있는 상황에서 주문 발생시 배송 처리가 되어야하는 비즈니스가 있다고 가정한다.

이를 위해 **2단계 커밋** 같은 **분산 트랜잭션 기법**을 사용하는데, **각각 다른 서비스를 하나의 트랜잭션**으로 묶다 보면 각 **서비스의 독립성도 떨어지고**, **2단계 커밋을 지원하지 않는 저장소(ex, NoSQL)도 있다는 문제**가 있다.

→ **데이터 일관성 문제를 해결하기 위해** 두 서비스를 단일 트랜잭션을 묶기 보다는 `비동기 이벤트 처리를 통한 협업`을 강조한다. 이를 '결과적 일관성'이라고 표현하기도 한다.

**결과적 일관성** : 여러 트랜잭션을 하나로 묶지 않고 **별도의 로컬 트랜잭션을 각각 수행**하고 일관성이 달라진 부분은 체크해서 **보상 트랜잭션으로 일관성을 맞추는 개념**
→ 두 서비스의 데이터가 일시적으로 불일치하거나 일관성이 없는 상태지만, **결국에는 두 데이터가 같아진다.**

- 분산 트랜잭션으로 묶으면 두 서비스 간의 강한 결합이 생겨서 서비스를 분리한 효과를 누리기 힘들다.

[ 해결 예시 ]

각 트랜잭션을 분리하고(로컬 트랜잭션), 큐 매커니즘을 이용해 보상 트랜잭션을 활용하는 방법

```java
1. 주문 서비스가 주문 처리 트랜잭션을 수행한다.
	1-1) 동시에 주문 이벤트를 발행한다.
	1-2) 주문 이벤트가 메시지 큐로 전송된다.
	1-3) 배송 서비스가 주문 이벤트를 인식한다.
2. 배송 서비스가 주문 처리에 맞는 배송 처리 트랜잭션을 수행한다. (비즈니스 일관성 만족)
3. 배송 처리 트랜잭션 중 오류로 트랜잭션을 실패한다.
	3-1) 배송 처리 실패 이벤트를 발행한다.
	3-2) 배송 처리 실패 이벤트가 메시지 큐로 전송된다.
	3-3) 주문 서빗 가 배송 처리 실패 이벤트를 인식한다.
4. 주문 서비스는 주문 취소(보상 트랜잭션)를 수행한다. (비즈니스 일관성 만족)
```

### 위기 대응 방식의 변화 : 실패를 고려한 설계

실패해서 더 는 진행할 수 없을 때도 자연스럽게 대응할 수 있도록 설계해야 한다. → 내결함성

- 완벽히 **테스트**할 수 있는 환경을 구축한다.
- **시스템의 실패를 감지**하고 대응하기 위해 **실시간 모니터링 체계**도 갖춰야한다. (cloud watch, grafana..)
- **서킷 브레이커 패턴** : 각 서비스를 모니터링하고 있다가 **한 서비스가 다운되거나 실패**하면 **이를 호출하는 서비스의 연계를 차단하고 적절하게 대응**하는 것
→ 서킷 브레이커가 없으면 문제를 인지하지 못하고 계속 요청을 보내면서 다른 서비스에도 영향을 미칠 수도 있다.
- **카오스 엔지니어링** : 운영 중인 서비스에서 발생할 수 있는 각종 장애 조건을 견딜 수 있는 신뢰성을 확보하기 위해 분산 시스템을 테스트하는 것

# 정리

- MSA는 단순히 기술이나 아키텍처 뿐만이 아니라, 다양한 사람들이 만나서 협업하는 방식, 조직 문화의 진화된 결과물이다.
- MSA의 성공을 위해서는 아키텍처 및 개인 역량에만 집중할 것이 아니라 일하는 문화, 일하는 절차 등을 고려해야 한다.
- 비즈니스 민첩성을 위한 3가지 요소
    1. 프로세스 : 점진 반복적인 개발 프로세스
    2. 아키텍처 : 유연하고 자동화된 개발 환경
    3. 조직문화 : 자율적인 업무 기능 팀과 개발 문화