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

_Spawn_
* Spawning : 플레이 중에 오브젝트를 만드는 것
* Transform : 위치, 회전, 스케일을 이야기 함, 게임에서 많이 사용
* Return pin : 노드의 출력, 노드를 실행시킨 결과로 나오는 데이터나 오브젝트

_데이터 유형_
* Struct : 작은 오브젝트?, 레퍼런스 사용하지 X
* Data type : 데이터의 "shape" 

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

### ✔️임펄스 추가하기
점프를 구현하기 위해 위로 움직이는 힘(Force, 포스)를 적용할 것인데, 여기서 적용하고자 하는 것은 포스가 아니고 임펄스이다.
피직스에서 포스와 임펄스는 다르다. 포스는 정해진 시간에 걸쳐 발생하는 반면, 임펄스는 즉각적이다.  
* Force = Mass * Acceleration
* Impulse = Mass * Velocity Change
#### 1. 질량 * 속도 를 Z축 방향으로 넣어주기
위로 점프하려면 Z축 방향으로 임펄스를 줘야 한다.
![](https://velog.velcdn.com/images/kuronuma_daisy/post/1d5cd4c4-dd32-4e9e-961b-7c067b6b28c8/image.png)  
* 질량 500kg * 속도를 Z축 방향으로 Impulse 부여.
* 4m/s를 원한다면 질량 * 400 (언리얼은 주요 단위가 cm)
#### 2. Vel Change 체크박스 체크 시
Add Impulse 노드의 Vel Change를 체크하면 질량을 무시하고 작성한 값의 속력을 적용한다.
![](https://velog.velcdn.com/images/kuronuma_daisy/post/26593692-4899-4bb1-9c5a-dc7822ef72ce/image.png)  
* 400 입력 시 똑같이 4m/s 속력 적용됨.
* 하지만 질량이 어떻든 똑같이 점프함. 

### ✔️블루프린트 클래스와 인스턴스
![](https://velog.velcdn.com/images/kuronuma_daisy/post/c09d6654-d4c8-48d3-8aa0-226d2d7bb11d/image.png)
> + `Abventurer`는 모험가 클래스로 기본 데이터와 일부 기능이 있다.
+ `Adventurer 1`과 같이 이 클래스의 인스턴스를 만들 수 있다. 예를 들어 모험가1이 Bob이라고 하면 Bob은 모험가 클래스의 고유한 데이터 사본을 갖고 있다.
+ Bob이 실제 오브젝트이며 클래스는 오브젝트를 만드는 원본이다.
+ Experience 데이터가 200인 모험가 인스턴스 2를 만들 수도 있다.


![](https://velog.velcdn.com/images/kuronuma_daisy/post/6c96085a-7e31-4117-882f-845595dc7d25/image.png)  
* 구체로 원하는 크기의 발사체를 생성했다. (BP_Projectile로 이름 설정함으로써 이름을 보고 바로 블루프린트 클래스임을 알 수 있음)
* 사진에 동그라미 표시된 부분의 버튼을 클릭해 이 발사체를 단일 오브젝트가 아닌 여러 오브젝트의 블루프린트 클래스로 변환할 수 있다.

![](https://velog.velcdn.com/images/kuronuma_daisy/post/c06c003b-61e6-45bb-98d8-fbf8aff4c966/image.png)  
* BP_Projectile 클래스의 프로퍼티를 몇 가지 변경하면?  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/200ffe11-1538-4af6-98fe-d77eee6a80e3/image.png)  
* BP_Projectile의 인스턴스들이 모두 변경되어 있다.

### ✔️액터 스폰(Spawn)하기
* `Spawn Actor from Class` 노드 사용
`Space Bar` 노드의 Pressed 핀과 `Spawn Actor from Class` 노드 연결해서 스페이스 바 누르면 발사체가 생성되도록 만들기 + 임펄스 추가
![](https://velog.velcdn.com/images/kuronuma_daisy/post/f25ab479-be3a-43c4-bc1d-ba3204e20f9f/image.png)

### ✔️데이터 타입  
컴퓨터 메모리의 특정한 이진법 데이터를 나타내는 한 방법
이 데이터로 무엇을 할 수 있는지 제한하는 방법
데이터의 "shape" 라고 생각할 수 있음
* Integer 정수
* Float 부동소수점
* String 텍스트
* Bools(Boolean) true/false

### ✔️폰(Pawn)과 액터 위치 
Pawn은 게임 월드 속에서 플레이어의 물리적 묘사
`F8`을 길게 눌러 폰에서 유체이탈(?)해서 구경 가능 (Default Pawn)
* `Get Player Pawn` 노드와 `Get Actor Location` 노드로 위치 가져올 수 있음
![](https://velog.velcdn.com/images/kuronuma_daisy/post/6b674d03-02e9-4910-b3c8-37309fef5f5a/image.png)  
(+ BP_Projectile의 질량 무겁게 바꿔서 발사체의 위력 높임)
여기까지 하면 플레이어 위치에서 앞으로만 총알(발사체)을 발사하는 게임이 됨, 카메라를 돌려도 발사체가 같은 방향으로만 향함.

### ✔️방향(회전) 다루기(1)
![](https://velog.velcdn.com/images/kuronuma_daisy/post/6258f23a-b321-4417-af89-f134ef0d67f2/image.png)  
플레이어의 위치를 얻어냈던 것과 마찬가지로 `Get Actor Rotation`을 사용해서 BP_Projectile에 방향값을 줘봐도 플레이할때 플레이어가 회전하는 방향값이 적용되지 않음  
> Default pawn과 카메라의 방향값이 같지 않기 때문!  

![](https://velog.velcdn.com/images/kuronuma_daisy/post/4ac8885a-a934-4b33-a409-dbece5737260/image.png)  
`Get Control Rotation`으로 카메라(시점)의 방향 얻을 수 있음
발사체 자체의 방향이 바뀌긴 하지만 원하던 의도가 아님 

### ✔️벡터의 덧셈과 곱셈
수학적으로 벡터는 3D 공간에서의 방향과 크기
컴퓨터적으로 벡터는 3개의 부동소수점 값 X, Y, Z

### ✔️전방 벡터 Forward Vector
앞 방향으로의 벡터
카메라 방향대로 회전한 후의 발사체의 전방을 가리키는 벡터
![](https://velog.velcdn.com/images/kuronuma_daisy/post/5b4c2fde-6008-4dc6-95f2-1dfe32329159/image.png)  
* 전방 벡터는 회전한 X 방향임(빨간 화살표 벡터)
* 회전한 Y축 벡터(연두색 벡터)도 있지만 우리는 발사체를 앞으로 보내고 싶은 것이므로 전방 벡터만 사용할 것이기 때문에 사용하지 않음
* 이 벡터들의 길이는 항상 1이기 때문에 이 방향으로 어떤 크기의 충격을 적용하고 싶을 때 원하는 값을 곱하기만 하면 된다!

### ✔️방향(회전) 다루기(2)
`Get Actor Forward Vector`와 `Multiply`노드 사용
발사체의 방향의 전방 벡터와 충격값을 곱하여 Impulse로 적용시키면 된다!
![](https://velog.velcdn.com/images/kuronuma_daisy/post/e1788880-c6ab-4e5d-8045-c61c50185de4/image.png)   
