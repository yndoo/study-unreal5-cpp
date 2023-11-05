# 강의 개요  
* Physics 다루는 법  
* 씬에서 발사체를 스폰하여 런타임에 다양한 사물이 추가되도록 다양한 오브젝트로 스폰하는 방법 
* 발사체를 조준하는 방법  
* 언리얼의 툴 중 BXP라는 툴 씬을 만드는 레벨 빌드
* 총알 개수 제한하고 총알이 몇 개 남았는지 세고 표시하는 메커니즘
* 레벨을 다시 로드하려면 어떻게 하는 지  

### ✔️용어집 (섹션 2 전체) 
_블루프린트_
* Event Graph 이벤트 그래프 : 블루프린트를 그릴 캔버스  
* Node : 블루프린트에서 사용할 수 있는 미리 만들어진 기능
* String : 언어 문자열
* Event : 언제 사건이 발생해야 하는지에 대한 노드
* Pin 핀 : 노드를 연결할 수 있는 소켓(화살표)
* Input Pin : 왼쪽에 있는 핀으로 언제 이 노드를 실행할 지 알려줌
* Output Pin : 이 노드 이후에 무엇을 할지 알려줌
* Connection : 두 핀 사이의 전선(?), '언제'와 '무엇'을 연결해 줌  

_오브젝트_
* Objects : 데이터와 기능의 집합  
* Actors : 레벨에 투입할 수 있는 오브젝트  
* Component : 액터 자체에 들어가는 오브젝트
* Reference : 주소, 오브젝트 위치
* Data Pin : 노드의 데이터 입력이나 출력 (블루프린트에서 레퍼런스 오른쪽 파란색 핀)
* Execution Pins : 노드를 언제 실행하는지 (흰색 핀)

### 🗨️블루프린트 예시
![](https://velog.velcdn.com/images/kuronuma_daisy/post/14bd3c3e-06f5-4962-9f01-7ab6f9d1fc2d/image.png)  
왼쪽 노드는 '게임이 시작하면' 을 의미
가운데 노드는 화면에 String을 출력하는 기능의 노드
오른쪽 노드는 또다른 String 출력 노드

#### 🗨️실행 모습  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/378b3f61-3345-48f6-bdda-9e96ec497a18/image.png)  


`Ctrl + Shift + S 로 전체 저장`

### ✔️Physics 피직스 시뮬레이션 
오브젝트 `디테일` 창 > 필터 리스트에서 `피직스` 선택 > 피직스와 관련된 액터의 프로퍼티들이 보임 
![](https://velog.velcdn.com/images/kuronuma_daisy/post/e1e2ec7f-e55b-4ae4-a0ca-8e82b3dd8295/image.png)  
* 피직스 시뮬레이트 : true로 체크하면 물리법칙이 적용됨. 끄면 물건이 아무 영향 안 받고 고정되는 느낌.(?)
* 질량 : 물질의 질량을 다루는 프로퍼티. 원하는 질량을 부여할 수 있음.
* 중력 활성화 : 비활성화하면 중력이 없는 것처럼 떠 다님.

### ✔️Objects 오브젝트
* 본질적으로 무언가를 대표하는 것
#### 예시1 - 모험가
* Data
   * 경험치 = 600
   * 레벨 = 2
* 기능
   * 화살 던지기
   * 점프
   ...
#### 예시2 - 리스트
* Data
   * items : 1, 2, 3, 4
* 기능
   * 마지막 원소 지우기
   * 끝에 데이터 추가하기
   ...

오브젝트와 기능 매핑이라고 할 수 있음

### ✔️Reference
주소로 오브젝트 데이터 가져오기
![](https://velog.velcdn.com/images/kuronuma_daisy/post/c07e0c67-4d47-4a97-aba1-154c216851d3/image.png)
* Cube의 주소 get -> Static Mesh Component(큐브에 있는 컴포넌트) 주소 get -> get 질량 -> print의 string값으로 전달
