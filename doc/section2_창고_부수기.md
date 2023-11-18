# 강의 개요  
* Physics 다루는 법  
* 씬에서 발사체를 스폰하여 런타임에 다양한 사물이 추가되도록 다양한 오브젝트로 스폰하는 방법 
* 발사체를 조준하는 방법  
* 언리얼의 툴 중 BXP라는 툴 씬을 만드는 레벨 빌드
* 총알 개수 제한하고 총알이 몇 개 남았는지 세고 표시하는 메커니즘
* 레벨을 다시 로드하려면 어떻게 하는 지  

## ✔️용어집 (섹션 2 전체) 
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

_Booleans and Branches_  
* Branch : 부울을 바탕으로 뭔가를 하거나 안 하는 것 
* Booleans : 참 혹은 거짓을 갖는 데이터 타입  
* Comparison 비교 연산자 : 작거나 크거나 같다 등의 부울을 반환하는 것  
 
_Pure Functions_  
* Side effect : 눈에 보이는 효과  
* Pure Function : side effect가 없는 함수, 뭔가 가져오거나 질문에 대답하는 함수  

_멤버 함수_  
* Object Oriented Programming : 함수와 함수가 조작하는 데이터가 함께 사는 것  
* Member function : 클래스의 함수, 항상 특정 인스턴스에서 호출되는 함수
* Self : 멤버 함수 안에서 사용 가능한 노드이며 우리가 사용하는 현재 인스턴스를 항상 가리킴  

## 학습 내용
### ✔️블루프린트 예시
![](https://velog.velcdn.com/images/kuronuma_daisy/post/14bd3c3e-06f5-4962-9f01-7ab6f9d1fc2d/image.png)  
왼쪽 노드는 '게임이 시작하면' 을 의미
가운데 노드는 화면에 String을 출력하는 기능의 노드
오른쪽 노드는 또다른 String 출력 노드

#### 실행 모습  
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

### ✔️에셋 가져오기
1. 에픽게임즈 런처 -> 언리얼 엔진 -> 마켓플레이스
구매 -> 다운로드 -> 프로젝트에 추가하기

`콘텐츠 드로어 단축키 Ctrl + Space`

2. 다운로드한 에셋 폴더 > Meshes
에서 원하는 에셋을 드래그해서 쉽게 사용할 수 있음
![](https://velog.velcdn.com/images/kuronuma_daisy/post/89a8803b-fc7d-46b0-aa5b-a5d0b2627d10/image.png)  


### ✔️지오메트리 브러시(BSP, Binary Space Partitioning)
#### 새 레벨 만들기
`파일 탭 > 새 레벨 > 빈 레벨 > 생성하기` 
(강의에서는 Basic 레벨 골랐지만 나에게는 Basic 레벨이 없었다...
![](https://velog.velcdn.com/images/kuronuma_daisy/post/f14c40df-6a52-4057-ade5-a63d5a6d9fbf/image.png)  
기본 환경 세팅하기 : `창 탭 > 환경 라이트 믹서 > 모두 다 켜기`
-> 핑크 네모 모두 클릭
![](https://velog.velcdn.com/images/kuronuma_daisy/post/27919482-3f74-4381-bd8d-edc5105c2587/image.png)  
그럼 레벨에 조명이 생긴다!  

#### 지오메트리 브러시를 이용해서 기본 맵 만들기
`프로젝트에 빠르게 추가 > 액터 배치 패널 > 지오메트리 > 박스`  

이름 바꾸기 `F2` 

1. Walls로 이름을 바꾸고 디테일의 `브러시 세팅`에서 크기를 각각 36m, 29m, 9.6m로 설정
2. Walls를 복사해서 이름을 Walls Subtract로 변경
3. Walls Subtract의 브러시 세팅에서 크기를 각각 200씩 즉, 2m씩 감소시킴
4. Walls Subtract의 브러시 세팅에서 `브러시 타입`을 Subtractive로 변경

그럼 Walls 공간에서 Walls Subtract 공간을 뺀 방이 생김!

#### 프로젝트 켤 때 새로 만든 레벨이 열리도록 설정하기
`Ctrl + S` 로 레벨 저장 (이름 'Main'으로 저장했다)
`세팅 > 프로젝트 세팅 > 맵 & 모드 > 에디터 시작 맵, 게임 기본 맵을 Main으로 변경`
![](https://velog.velcdn.com/images/kuronuma_daisy/post/ad28ef1e-0d4e-4eab-a4f9-7926c4c1479d/image.png)  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/5a198b96-a225-40c3-89f3-6ff891d38841/image.png)  

#### 창문 만들어보기
지오메트리 브러시 이용해서 Substractive 타입으로 창문 생성

`Alt + 마우스 이동` : 복제하며 이동 가능

1. 한 벽면에 창문을 여러 개 만들고 Shift 클릭으로 전체 선택해서
2. 반대편 벽면에 Alt로 복제 이동
![](https://velog.velcdn.com/images/kuronuma_daisy/post/fdf20f6d-3a57-4200-81c2-c865811d2bdb/image.png)  

(이전 레벨에서의 블루프린트 모두 복사해서 새 레벨에 붙여넣기)  
### ✔️재료와 조명(Materials and Lighting)  
#### 조명  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/1298ae9a-249e-4243-8802-d3393e14efdb/image.png)  
`DirectionalLight`의 방향을 조절해서 태양광으로 인한 그림자를 제어해서 원하는 공간의 분위기를 조성할 수 있음

#### 머티리얼(Material, 재료라는 뜻)
`콘텐츠 드로어 필터링 - 머티리얼`
원하는 머티리얼 골라서 드래그하면 지오메트리 브러시 표면으로 설정됨  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/101c1cdb-6a01-4670-8a73-aa48bec284aa/image.png)  
저는 바닥과 천장에 잔디를 깔아보았습니다...ㅎㅅㅎ  

### ✔️액터 컴포넌트(Actor Conponent)
액터에 하나 이상의 정적 메시 컴포넌트(StaticMeshComponent)를 가질 수 있음  
하나의 컴포넌트는 액터의 루트가 될 것이고 다른 것들은 자식이 됨  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/940d2201-76bc-4bd8-bc1d-8ded67c2ce67/image.png)  
선반 다리에 선반 판을 합치기 위해 선반 다리의 정적 메시 컴포넌트에 드래그 해줌  
-> 판이 다리의 자식이 됨
* 다른 컴포넌트의 자식일 경우 그 위치는 부모의 위치에서 상대적으로 표현됨 

### ✔️충돌 메시(Collision Meshed)  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/0ba0ccc9-10f8-4881-a906-551af806ae6a/image.png)  
배럴을 쌓아 올리고 각각의 physics를 활성화 시킨 뒤 플레이하면 배럴들이 튀어오름
`뷰 모드 > 플레이어 콜리전`
충돌할때 적용되는 mesh가 이렇게 울퉁불퉁하게 생겼기 때문  

![](https://velog.velcdn.com/images/kuronuma_daisy/post/b89a6a31-787f-4013-acf7-e7f1c0f1b5e7/image.png)  
1. 컨텐츠 드로어에서 배럴 더블 클릭  
2. 뷰 모드 '플레이어 콜리전'  
3. 콜리전 제거  
4. 10면체 Z 단순화 콜리전 추가  
5. 배럴의 블루프린트 클래스를 만들어서 마음껏 사용하기~!
![](https://velog.velcdn.com/images/kuronuma_daisy/post/e0a3969e-64c7-49a4-a642-3231c743d582/image.png)  

### ✔️변수 
![](https://velog.velcdn.com/images/kuronuma_daisy/post/74f206f7-fbb8-4521-b9e3-177f6e920fab/image.png)  
정수 타입의 ammo 변수, default 값 20 설정
`ctrl + 드래그` : Get
`Alt + 드래그` : Set
![](https://velog.velcdn.com/images/kuronuma_daisy/post/72145348-4cd9-47af-89f9-23149022f16c/image.png)  
발사체 발사 후 ammo 변수가 1씩 줄어드는 블루프린트  

### ✔️부울과 분기(Booleans and Branches)
* Boolean은 참 혹은 거짓의 두 가지만 저장하는 변수
* Branch Nodes : 무언가 참인지 거짓인지 확인한 다음 그 결과에 따라 무언가를 하도록 만드는 노드, 한마디로 조건문
```
배고프냐?
만약 배고프면 -> 음식을 꺼내 먹는다.
배고프지 않으면 -> 게임을 계속 플레이한다.
```
![](https://velog.velcdn.com/images/kuronuma_daisy/post/8b88be87-2c7a-41ea-bdb1-5e9ab6dd7762/image.png)  

`Branch` 노드를 보면
ammo 변수가 0보다 클때만 발사체를 발사, 
ammo가 0 이하면 "Out of Ammo!" 출력 

### ✔️함수 functions
지저분한 블루프린트 노드들을 정리하는 방법들이 있음.  
* 주석으로 묶기  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/84a7e4e4-533d-4c37-b406-43b28db7b78d/image.png)  
발사체를 생성하고 발사하는 노드를 묶어 `C 키` 클릭 시 노드를 묶어주는 코멘트(주석) 작성 가능  
엄청 좋은 방법은 아님 함수라는 더 좋은 방법이 있기 때문 ~.~  
함수 사용하면 재사용도 편해니까 굿  

* 함수로 묶기  
한 함수로 묶을 노드들 `드래그` > `우클릭` > `함수로 접기` 클릭
![](https://velog.velcdn.com/images/kuronuma_daisy/post/d881a267-8476-49a9-bc83-e4abe80928ee/image.png)

* 기능을 함수로 추출한 비포-애프터 비교  

|before|after|
|---|---|
|![](https://velog.velcdn.com/images/kuronuma_daisy/post/4529ab9b-22f2-4cb0-9a82-8a07924b3995/image.png)|![](https://velog.velcdn.com/images/kuronuma_daisy/post/d92f034e-9550-41b2-9eb6-eb222f0fae79/image.png)|

게임의 흐름 이해가 훨씬 쉽다.

> 만든 함수들
* Print Welcome Messages
* Decreasing Ammo
* Print Ammo

게임의 기능 이해도 훨씬 잘 되도록 정리됨
이렇게 따로 문서나 주석 없이 이해되는 코드를 `self documenting code` 라고 함

### ✔️리턴 타입
`내 블루프린트 > 함수 추가` : 새로운 함수 만들 수 있음  
`디테일 창 > 입력 '+'아이콘 or 출력 '+'아이콘` : 함수의 input과 output을 추가할 수 있음
![](https://velog.velcdn.com/images/kuronuma_daisy/post/71393b8c-1b83-4e3d-a69f-2ab7d449cfa3/image.png)  

브랜치의 조건 부분을 함수로 변경해볼 것임 -> Ammo가 있는지 확인하는 함수!  

|이벤트그래프|Has Ammo 함수 내부|
|---|---|
|![](https://velog.velcdn.com/images/kuronuma_daisy/post/f541b264-bb19-4dc3-a0c0-5843da8b8665/image.png)|![](https://velog.velcdn.com/images/kuronuma_daisy/post/3384b66a-e8ac-470b-8775-87d010041c8c/image.png)  

### ✔️순수 함수(Pure Functions)
위에서 만든 'Has Ammo' 함수에 실행 핀이 생긴 것은 좀 이상함 -> 순수 함수로 만들면 좋음  

+ 순수 함수 : side effects가 없고 return value는 있는 함수(이 함수 실행해서 무언가 상황이 바뀌면 side effects가 있는 것), **실행 핀이 없는 함수**  
ex) 'Get Ammo 함수', 'Get Actor Forward Vector 함수', Multiply, Minus, Greater, ...  

![](https://velog.velcdn.com/images/kuronuma_daisy/post/56323883-afd6-425b-a751-c55205d7ad1d/image.png)  

`함수 디테일 > 퓨어 활성화` : 실행 핀 없는 퓨어 함수 만들어짐  

* Has Ammo 함수는 퓨어 함수 가능!  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/b459a663-ce5d-49be-82da-02831d5796e9/image.png)  


### ✔️멤버 함수
암묵적으로 모든 멤버 함수는 현재 타켓이나 현재 인스턴스라는 파라미터 갖고 있음.
Spawn Projectile 함수 내에 임펄스 추가하는 노드들을 묶어 `BP_Projectile`의 멤버 함수로 넣었음.
각 발사체의 레퍼런스는 `self` 노드로 얻을 수 있음.

|Projectile의 멤버 함수 Launch 내부|Spawn Projectile 함수 속 Launch 함수|
|---|---|
|![](https://velog.velcdn.com/images/kuronuma_daisy/post/94095767-a2eb-4ae7-ba3e-ce6cae165971/image.png)|![](https://velog.velcdn.com/images/kuronuma_daisy/post/905390ec-d6fc-49f3-93cf-90850d4d9214/image.png)|


### ✔️Loading Levels & Delay Nodes (레벨 로드와 지연 노드)
현재 Ammo가 0 이하면 "Out of Ammo!"를 출력하고 더 이상 게임이 진행되지 않음  

* Ammo 0 이하면 "Out of Ammo! Restarting in 5 seconds..." 출력 후 현재 Level을 다시 Open하도록 변경  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/f0fe06fa-ffc5-453e-99b4-aa275d2ac4e1/image.png)    

*그걸 다시 함수로 변경  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/4ae0089b-7f65-4f10-8b0f-7b01d54fc6cb/image.png)  

### ✔️결과물
* 결과물 (1.75배속)
20발 총알 발사 가능하고 총알 소진 시 5초 후 Restart하는 모습.
![](https://velog.velcdn.com/images/kuronuma_daisy/post/83f10a2f-4ed5-430f-b3f5-3e0ddfebf8b9/image.gif)  
 
* 블루프린트 이벤트 그래프 
![](https://velog.velcdn.com/images/kuronuma_daisy/post/87926a4d-5707-4627-babb-73fcd0aa1b43/image.png)
