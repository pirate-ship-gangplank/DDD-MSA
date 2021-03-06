마이크로서비스 설계에서 중요한 것은 **응집성을 높이고, 의존성을 줄이는 것**이다.

# 1. 마이크로서비스를 도출하는 방법

## 비즈니스 능력에 근거한 도출

비즈니스 부서가 가진 역할, 처리 능력을 체계적으로 분리한 업무 기능 분해에 따라 마이크로서비스를 나눈 것

- 각 도메인에서는 비즈니스가 규정하는 일하는 방식과 조직, 부서 체계가 이미 정의돼 있고, 이러한 부서는 이미 업무 처리에서의 응집성을 가지고 있으며 타 부서와의 의존도는 낮을 것이다.
- 서비스가 소유해야 할 **데이터 식별에 적합하지 않고**, **기능과 데이터가 분리**되고 **하나의 통합 데이터가 여러 기능에서 사용**되도록 하는 모델링 방식이다. 
따라서, 비즈니스를 처리하는 기능과 그 기능에 영향을 받는 데이터가 분리되는 경향이 있다.
→ 이를 아래의 바운디드 컨텍스트 기반 도출에서 해결한다.

## DDD의 바운디드 컨텍스트 기반 도출

데이터를 기능과 분리해서 식별하지 않고, 문제 영역인 하위 도메인마다 별도의 도메인 모델로 정의하는 방법

- 서비스가 소유권을 가진 데이터를 독립적으로 식별한다.

# 2. DDD에서의 설계

**바운디드 컨텍스트** : 비즈니스 응집성이 있는 컨텍스트를 구분하는 것. 마이크로서비스를 식별하기 위한 훌륭한 단위가 될 수 있다.

- 비즈니스 변화에 빠르게 대응하기 위해 클라우드와 마이크로서비스를 사용한 것처럼, 빠르게 변화하는 구현 기술에도 유연하게 대응할 수 있는 애플리케이션을 설계하는 것이 중요하다.

# 3. DDD의 전략적 설계

## 도메인과 서브도메인

DDD에서는 하나의 큰 도메인을 전략적 중요도에 따라 도메인을 나누고, 각 도메인을 각각 하나씩 해결하는 방법을 기본으로 삼는다. 

- **서브도메인** : 많은 개념들이 복잡하게 엮인 **비즈니스 도메인을 논리적으로 구분되는 여러 개의 하위 영역으로 분리한 하위 도메인**

**[ 서브도메인 구분 ]**

서비도메인을 중요도에 따라 3가지 유형으로 구분한 것

- **핵심 서브도메인** : 다른 경쟁자와 차별화를 만들 비즈니스 영역. 기업이 높은 우선순위를 갖는 영역이자 소프트웨어 개발에서 전략적으로 가장 큰 투자가 필요한 영역
- **지원 서브도메인** : 비즈니스에 필수적이지만 핵심은 아닌 부분. 핵심 도메인을 성공시키기 위해서는 반드시 필요한 영역으로, 핵심 서브도메인 다음으로 중요한 영역이다.
- **일반 서브도메인** : 비즈니스적으로 특화된 부분은 아니지만, 전체 비즈니스 솔루션에는 필요한 부분. 기존 제품을 구매해서 대체할 수 있다.

## 유비쿼터스 언어, 도메인 모델, 바운디드 컨텍스트

### 유비쿼터스 언어

특정 도메인에서 **의도를 명확히 반영하고 도메인의 핵심 개념을 잘 전달할 수 있는 언어**

- 설계자와 개발자가 동일한 개념을 서로 다른 용어로 부르면서 오는 혼동을 방지하기 위한 공통 언어
- 한 도메인 안에서 모든 관계자들이 용어를 공통으로 정의하여 오해를 없앨 수 있게 된다.
- 특정 업무와 관련된 사람들 간에 자율적으로 정의되고 통용되는 개념

ex) 같은 '고객'이어도 결제 서비스에서는 '결제를 하는 결제자'를 의미하고, 배송 서비스에서는 '상품을 배송받는 수취자'의 의미를 가진다. 
→ 이건 반대로 서로 다른 의미의 개념을 명확하지 않은 용어로 혼용하면서 발생하는 오해인듯하다.

- 정의한 유비쿼터스 언어는 설계에도 사용하고, 소스코드에도 사용한다.

### 도메인 모델

- 특정 비즈니스 맥락에서 통용되는 개념들의 관계를 잘 정의한 모형이다.
- 도메인과 관련된 제품 책임자, 도메인 전문가, 개발자를 비롯한 모든 구성원들이 업무를 이해하는 기본 모형이 되어야한다.

### 바운디드 컨텍스트

- 도메인 모델 간의 경계이다. 각 도메인 모델에서 사용하는 언어와 개념이 서로 다른 그 경계가 바운디드 컨텍스트이다.

## 컨텍스트 매핑

바운디드 컨텍스트를 식별할 때 각 컨텍스트는 내부적으로 응집성이 높고, 다른 컨텍스트와는 의존성이 낮아야한다. 하지만, 그렇다고 컨텍스트 간에 아무런 관계가 없다는 의미는 아니다.

비즈니스 수행을 위해 **여러 개의 컨텍스트가 연계해야 하는 경우**가 발생하는데, 이러한 **컨텍스트 간의 의존 관계**를 DDD에서는 **컨텍스트 매핑**이라고 한다. (연관관계가 있는 두 컨텍스트 사이에 선을 그려서 표시한다.)

**[ 주요 컨텍스트 매핑 관계 ]**

### 공유 커널

**바운디드 컨텍스트 사이에 공통적인 모델을 공유하는 관계**

- 두 개 이상의 팀에서 작지만 공통의 모델을 공유하는 관계이다.
- 각 팀이 공유하는 모델에 대해 서로 합의해야 하며, 보통 공통 라이브러리 등이 여기에 해당된다.


### 소비자와 공급자

**공급하는 컨텍스트는 상류(upstream)**로, **소비하는 컨텍스트는 하류(downstream)**로 표시한다.

- **데이터의 흐름은 상류에서 하류로** 흐른다. 반대는 가능하지 않기에 상류의 변화가 있으면 하류에서 변화를 따라야한다. 공급자는 소비자가 원하는 기능을 제공해야 한다.
- 상류가 데이터를 제공하기 때문에 REST-API를 제공한다. 핵심 서브도메인이 지원 및 일반 서브도메인의 데이터를 사용하는 형태가 많기 때문에 핵심 서브도메인이 하류, 지원 서브도메인 및 일반 서브도메인이 상류인 경우가 많다. (뒤에 나오는 '컨텍스트 맵'에 예시 그림 참고)


### 준수자

**소비자/공급자와 유사하지만, 상류 팀이 하류 팀의 요구를 지원하지 않거나 못하는 경우 사용**한다. 

- 이런 상황에서 하류 팀은 상류팀에서 제공하는 모델을 그대로 사용한다.


### 충돌 방지 계층

하류 팀이 상류 팀의 모델에 영향을 받을 때 **하류 팀의 고유 모델을 지키기 위한 번역 계층을 만드는 것**

- 상류 모델의 변경 없이 하위 모델과 통합하기 위해 데이터를 변환하는 매커니즘을 구현한 것이다.
- 기존 레거시 시스템이 REST API 방식을 지원하지 않을 경우, 레거시 시스템을 변경하지 않고 **새로운 시스템에 충돌 방지 계층을 구현**해서 **레거시 시스템의 기존 연동 방식을 그대로 유지**하면서 새로운 시스템과 통신하게 한다.
- 나중에 레거시 시스템을 걷어내면, 새로운 시스템에 구현했던 충돌 방지 계층만 없애고 연동하면 문제없이 연동이 가능해진다.


### 공개 호스트 서비스 (OHS : Open Host Service)

**바운디드 컨텍스트에 대한 접근을 제공하는 프로토콜이나 인터페이스를 정의**한다.

- 이 프로토콜은 하류의 컨텍스트가 상위 컨텍스트에서 제공하는 기능을 용이하게 사용할 수 있도록 공개되어 있다.
- 보통 다른 컨텍스트에서 사용할 수 있는 공유된 API가 여기에 해당된다.


### 발행된 언어 (PL : Published Language)

하류의 컨텍스트가 상류의 컨텍스트가 제공하는 기능을 사용하게 하기 위한 간단한 사용과 번역을 가능케하는 문서화된 정보 교환 언어

- XML이나 JSON 스키마로 표현될 수 있으며, **주로 공개 호스트 서비스와 짝을 이뤄 사용**된다.


## 컨텍스트 맵

**하나의 큰 도메인을 여러 개의 바운디드 컨텍스트로 식별하고, 이들 간의 관계를 표현한 그림**


- 핵심 서브도메인이 동작하기 위해 지원 서브도메인과 일반 서브도메인의 정보를 활용하고, 지원 서비스 도메인 역시 동작을 위해 일반 서브도메인을 활용하고 있다.
- 충돌 방지 계층 : 하류 컨텍스트는 충돌 방지 계층을 구현하여 상류에서 내려오는 정보를 번역하여 사용할 수 있게했다.
- 공개 호스트 서비스(OHS)/발행된 언어(PL) : 상류 컨텍스트는 OHS와 PL을 통해 하류에 API를 제공한다.

**[ 컨텍스트 맵 사례 ]**


- 공급자 컨텍스트들은 HTTP/JSON 기반의 REST-API를 통해 동기 통신의 서비스를 제공한다.
- 사용자 컨텍스트 → 계정 컨텍스트, 주문 컨텍스트 → 재고 컨텍스트 방향으로 각각 비동기 이벤트 메세지를 발행한다.

# 4. 이벤트 스토밍을 통한 마이크로서비스 도출

**이벤트 스토밍 : 이벤트 중심으로 이해관계자들이 모여 브레인 스토밍하는 워크숍**

- 모든 이해관계자가 모여 서로가 가지고 있는 각 관점을 논의하며, 그 차이점을 이해하고 공유할 수 있다.

**[ 이벤트 스토밍 워크숍 진행 순서 ]**

1. 도메인 이벤트 찾기
    - 시간의 흐름에 따라 시스템의 동작을 의미하는 도메인 이벤트를 도출한다. 데이터나 데이터의 구조가 아닌 비즈니스 흐름에서 발생한 이벤트에 초점을 두는 것이 중요하다.
    - 이벤트는 왼쪽에서 오른쪽으로 시간 흐름순으로 붙이되 이벤트가 연쇄적으로 발생하는 경우 바로 옆에 붙인다. 또한 같은 시점에 비즈니스 조건에 따라 대체적으로 발생할 수 있는 이벤트는 세로로 아래쪽에 같은 선상에 붙인다.
    - 도메인 이벤트는 비즈니스의 어떤 상태를 생성, 변경, 삭제하는 요소다. 시스템의 화면을 연상하지 말고 비즈니스가 흘러감에 따라 비즈니스를 구성하는 요소들의 상태가 어떻게 변경되는지 생각한다.
2. 외부 시스템 도출
    - 이벤트를 도출하면서 레거시 시스템이나 외부 시스템과의 연계를 통해 업무의 흐름이 진행될 때는 이 프로세스의 이름을 스티커에 작성해서 이벤트의 오른쪽 상단에 붙이고 화살표를 그려 이 외부 시스템을 호출한다는 것을 표시한다.
    - 시스템 구현 범위에 있는 기능이 아니더라도 시스템의 기능 구현을 위해 연계가 필요한 시스템들은 모두 도출한다.
3. 커맨드 도출
    - 도메인 이벤트를 찾은 후에 이 이벤트를 동작하게 하는 커맨드(Command)를 찾는다. 커맨드명은 도메인 이벤트를 동작하게 하는 것으로 명령형, 즉 동사 형태로 작성한다. 커맨드는 앞에서 식별한 도메인 이벤트를 보면 쉽게 유추할 수 있다.
    - 하나의 커맨드에 의해 여러 개의 이벤트가 동시 또는 연속해서 발생할 수 있으며, 조건에 따라 하나의 커맨드에 여러 개의 다른 이벤트가 발생할 수 있음에 유의한다.
4. 핫스팟 도출
    - 핫스팟은 워크샵을 진행하는 과정에서 의문 사항이 생기거나 참여하는 사람들이 결정하기 힘든 사항, 다른 부서나 외부에 문의할 필요가 있는 사항과 같이 워크샵 중에 해결하거나 정의할 수 없는 것들이다.
    - 이러한 내용들은 잊지 않고 기록하기 위해 가정, 경고, 질문, 미결정 사항 등을 작성해서 문제가 되는 위치에 붙인다.
5. 액터 도출
    - 액터(Actor)는 사용자 또는 조직, 역할자를 의미한다. 액터는 추상적으로 식별하지 않고, 비즈니스를 수행하는 구체적인 역할을 고려해서 도출한다. 즉, 단순히 모든 업무에서 보편적으로 사용되는 회원이나 관리자로 정의하지 않고, 특정 비즈니스를 실제로 수행하는 판매자, 구매자같은 명확한 역할자를 도출하려고 노력해야 한다.
    - 액터를 도출하면서 이전에 식별하지 못했던 커맨드와 도메인 이벤트가 추가로 도출된다면, 추가로 식별되는 사항들을 모델링 공간에 붙인다.
6. 애그리거트 정의
    - 애그리거트는 커맨드와 도메인 이벤트가 영향을 주는 데이터 요소로, 도메인의 실체 개념을 표현하는 객체인 엔티티가 된다.
    - 액터와 마찬가지로 애그리거트도 구체적인 표현으로 도출하는 것이 좋다.
7. 바운디드 컨텍스트 그리기
    - 이름이 같거나 유사한 애그리거트를 완전히 다른 애그리거트와 구분해서 경계를 그려야한다. 또한 그동안 도출했던 도메인 이벤트, 커맨드, 액터, 애그리거트를 모두 고려해서 경계를 식별한다. 이 경계를 바운디드 컨텍스트라고 한다.
    - 컨텍스트의 이름은 바운디드 컨텍스트 내의 애그리거트 이름으로 정의하며, 컨택스트 내에 여러 개의 애그리거트 이름이 있는 경우 전체를 아우를 수 있는 대표 이름을 정한다.
8. 컨텍스트 매핑
    - 대략의 바운디드 컨텍스트가 식별되고 파악된 각 바운디드 컨텍스트 간의 관계를 바탕으로 별도의 컨텍스트 맵을 표현할 수 있다. 컨텍스트 관계를 작성할 때는 호출 관계의 방향을 고려해야 한다.
    - 또한 호출할 때 호출 방식을 고려해야 하는데, 컨텍스트 간에 항상 일관된 데이터가 필요한 관계는 동기 호출로 표현하고 결과적 일관성으로 충분히 처리 가능한 관계는 비동기 방식의 호출로 표현한다.

# 5. 마이크로서비스 상세 설계

## 프론트엔드 모델링

**[프론트 아키텍처 정의]**

- 모바일, 웹, 앱 모든 채널을 고려하고 사용자 경험에 민감하게 반응할 수 있는 반응형 UI를 지향하는 것이 좋다.
- 프론트엔드 프레임워크가 정의되면 백엔드 AP와 연계되는 스파이크 솔루션을 통해 아키텍처가 사용자 요건을 만족하는지 검토할 필요가 있다.
- **스파이크 솔루션** : eXtream Programming(XP) 방법론에서 나온 용어로, 문제 영역을 해결하기 위해 실제로 간단히 구현해 보는 프로그램

**[표준 레이아웃 정의]**

- 시스템의 목적과 기능을 고려하여 화면의 표준 레이아웃을 정의해야 한다.
- 비즈니스 처리를 위해 많이 사용되는 모록, 조회, 수정, 삭제 등의 대표적인 업무 화면 유형을 정의한다.

**[UI 레이아웃 정의]**

- 표준 유형을 기반으로 개별 UI 레이아웃을 정의한다. 화면에 입출력될 속성 정보를 식별하고 기능을 수행할 버튼 등을 정의한다.

**[UI 디자인 및 UI 레이아웃 반영]**

- 표준 화면 유형에 맞는 UI 디자인을 정의한다.

**[이벤트 반영]**

- 화면의 이벤트 변화에 따라 백엔드 API를 호출하는 방식을 정의한다.

## 백엔드 모델링

백엔드 마이크로서비스를 위한 설계는 헥사고날 아키텍처를 적용해 외부 영역과 내부 영역으로 구분되어 진행된다.

**외부 영역 설계**는 프론트엔드와 연계되는 `API 설계`로, **내부 영역 설계**는 비즈니스 로직을 구현하는 `도메인 모델링`, `데이터 모델링`으로 구체화되어 진행된다.

### API 설계

프론트엔드와 백엔드 간의 연계를 위한 계약이 필요한데, 이것이 API 설계이다.

**API는 백엔드에 존재**하지만 **프론트엔드의 요구사항을 충족**하도록 정의해야 한다.

- API 영역은 **헥사고날의 외부 영역**이고, **인바운드 어댑터**로서 어떠한 호출 방식도 허용되는 유연한 공간이다.
- 요즘 추세는 **HTTP 프로토콜과 JSON 포맷**을 사용하는 **REST AP**I가 표준처럼 사용되고 있다.
→ 간단한 HTTP 메서드 형식, 취급하기 쉬운 JSON 포맷 등의 특징 덕분에 쉽고 명확하게 이해할 수 있기 때문이다.

**[ REST API 개념 ]**

**REST API**는 **HTTP 프로토콜을 사용하는 네트워크 기반 아키텍처 스타일**이다. 아키텍처를 표현하는 구성요소로 `자원(Resource), 행위(Verb), 표현(Representations)`이 있다.

ex) `A라는 이름의 유저를 생성한다`고 하면 REST API는 아래와 같다.

```json
HTTP POST http://example.com/users/
{
		"users": {
				"name": "A"
		}
}

자원은 'users'이고, 행위는 'POST'이고 표현은 'A'라는 JSON으로 표현된다.
URI는 'http://example.com/users/' 가 된다.
```

**[ REST API 성숙도 ]**

- **레벨 0** : REST API의 매커니즘을 전혀 사용하지 않고 전통적인 원격 프로시저 호출 방식으로 HTTP 프로토콜만 사용한 것. URI의 매개변수인 Flag를 통해 어떤 메서드인지 파악이 가능한 방식이다.
    - 'ProductService?Flag=create' 하나의 URI 주소에 GET 방식의 URI 매개변수인 Flag를 통해 생성, 수정, 삭제를 처리한다.
- **레벨 1** : URI에 개별적인 자원을 표현하는 것
    - '/products/apple'과 같이 여러 기능을 사용하기 위해 하나의 URI에 요청하지 않고, 대상을 특정한다.
- **레벨 2** : 약속된 HTTP 메서드들을 사용하는 것.
    - 레벨 0, 레벨 1 모두 HTTP 메서드를 사용했지만 GET과 POST로 모든 요청을 처리했다.
    - 레벨 2는 HTTP메서드인 GET, POST, PUT, DELETE로 각각 처리한다.
- **레벨 3** : HATEOAS 방식으로 요청한다.
    - 특정 요청을 하게 되면 반환값에 기대했던 결과에 덧붙여 추가로 사용자가 그다음에 무엇을 할 수 있는지와 그것을 하기 위해 다룰 수 있는 URI 값을 보내준다.
    - 즉, 사용자에게 좀 더 리소스를 탐색해서 활용할 수 있는 가능성을 제공한다.

**[ API 설계 문서화 ]**

프론트엔드와 백엔드 간의 협업 차원에서 문서화는 중요하다.

wiki의 형태나 엑셀 형태로 정리할 수 있으며, 어떤 형태든 최소한 다음 항목은 포함하도록 한다.

- 서비스명, API 명, 리소스(URI)
- 요청 매개변수, 요청 샘플
- 응갑 매개변수, 응답 샘플

# 6. 도메인 모델링

마이크로서비스는 각 서비스마다 내부 아키텍처 구조를 서비스 특성에 맞게 수립할 수 있다. 각 마이크로서비스는 도메인 모델 중심으로 만들 수도 있고, 트랜잭션 스크립트 형태로 만들 수도 있다.

비즈니스가 복잡하지 않다면 트랜잭션 스크립트 형태로 만들 수도 있지만, 점점 복잡해질수록 도메인 모델 구조가 효과적이다. → 비즈니스 개념들을 잘 구조화할 수 있기 때문

**[ 도메인 모델 형태의 헥사고날 구조 ]**

- 도메인 모델을 중심으로 모델링 되어있다.
- 서비스가 모든 로직을 처리하지 않고, 비즈니스 로직이 도메인 모델로 위임되어 적절히 분산될 것이다.
- 백엔드 팀원이 객체지향 설계 및 문화에 익숙한 상황에서 적용하는 것이 좋다.

**[ 트랜잭션 스크립트 형태의 헥사고날 구조 ]** 

- 도메인 모델에 행위(메서드) 없이 속성(필드)만 가지고 있는 형태이다.

## 도메인 모델링 구성 요소 (DDD의 전술적 설계)

### 엔티티

**다른 엔티티와 구별**할 수 있는 **식별자를 가진 도메인의 실체 개념을 표현한 객체**이다.

- 식별자는 고유하되, 엔티티의 속성 및 상태는 계속 변할 수 있다.
- 식별자로 동일한 엔티티인지 아닌지를 구분한다.

### 값 객체 (VO : Value Object)

속성이 개별적으로 변화하지 않는 **개념적 완전성**을 모델링한다.

- **개념적 완전성** : 값 객체를 구성하는 특성들이 서로 연관되어 전체 의미를 이루는 것을 의미한다. 특성을 개별적으로 보면 의미가 없지만, 모든 특성들이 함께 있어야 의도에 맞는 의미가 된다.
- 개별 속성이 별개로 수정되지 않고 전체 객체가 한번에 생성되거나 삭제되는 객체이다.

**[ 값 객체의 특징 ]**

- 도메인 내의 어떤 대상을 측정하고, 수량화하고, 설명한다.
- 관련 특징을 모은 필수 단위로 개념적 전체를 모델링한다.
- 측정이나 설명이 변경될 땐 완벽히 대체 가능하다.
- 다른 값과 등가성을 사용해 비교할 수 있다.
- 값 객체는 일단 생성되면 변경할 수 없다.

### 표준 타입

**대상의 타입**을 나타내는 서술적 객체로, 엔티티나 값 객체의 속성을 구분하는 용도로 사용한다.

- 자바에서는 보통 열거형으로 정의한다. (타입에 따른 enum)

### 애그리거트

연관된 엔티티와 값 객체들의 묶음. 

- 애그리거트는 엔티티, 값 객체, 표준 타입 등으로 구성되는데, 이들 간에는 비즈니스 의존관계를 맺고 있으며 비즈니스 정합성을 맞출 필요가 있다.
→ 따라서 애그리거트 단위가 트랜잭션의 기본 단위가 된다.
- 애그리거트 내의 **엔티티 중 가장 상위의 엔티티**를 **애그리거트 루트**로 정하고, 이 애그리거트 루트를 통해서만 애그리거트 내의 엔티티나 값 객체를 변경할 수 있다.
- **보통 하나의 컨텍스트에 하나의 애그리거트**가 식별되나, 하나의 컨텍스트 안에 여라 개의 애그리거트가 존재할 수 있다.
- 애그리거트 간의 참조는 **애그리거트 루트의 식별자**를 활용해 **간점 참조**하는 것이 바람직하다.
→ 다른 애그리거트의 클래스를 직접 참조하면 별도로 마이크로서비스로 분리하기 힘들 것이다.

- **각 애그리거트는 각각의 단일 트랜잭션**으로 일관성을 유지하지만, **다른 애그리거트 사이의 일관성이 필요**하다면, **도메인 이벤트**를 통해 **결과적 일관성**을 통해 다른 애그리거트를 갱신하여 **일관성을 유지**한다.


### 도메인 서비스

**도메인의 비즈니스 로직 처리가 특정 엔티티나 값 객체에 속하지 않을 때 단독 객체를 만들어서 처리하는 것**

- 도메인 서비스에서는 **상태를 관리하지 않고, 행위만 존재**한다.
- 도메인 로직을 처리할 때 **엔티티나 값 객체와 함께 특정 작업을 처리**하고, **상태를 본인이 가지지 않고 엔티티나 값 객체로 전달**한다.

### 도메인 이벤트

DDD 및 이벤트 스토밍에서 말하는 도메인 이벤트의 구현체이다.

- 서비스 간 정합성을 일치시키기 위해 단위 애그리거트의 주요 상태 값을 담아 전달되도록 모델링한다.

- 주문 서비스에서 **주문 엔티티**와 **주문 아이템**이 생성되어 저장됨과 동시에 **주문됨 이벤트가 발행**된다.
→ 주문됨 이벤트 안에는 주문 상태를 나타내는 주요 주문 정보들이 포함되어 있다.
- **이벤트 발행**은 **주문 처리를 수행하는 트랜잭션과 묶어서 실행**되어야 한다.
- 발행된 이벤트는 메세지 처리 매커니즘을 통해 배송 서비스에 전달되며, 이를 통해 배송 서비스는 배송 처리를 수행할 수 있게 된다.
