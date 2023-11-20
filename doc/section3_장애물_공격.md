## 강의 개요
* 함수, 변수, 브랜치 in C++
* C++로 자체 액터 생성하기
* C++ 코드 구조
* C++ 컴파일, 언리얼 라이브 코딩 시스템  
* 블루프린트와 C++ 연결
* 템블릿에 포함된 표준 에셋 외의 커스텀 캐릭터 클래스 설정하는 법

## '장애물 공격' 게임 Action Plan
1. 프로젝트 생성하고 여러 에셋 가져오기  
2. C++를 위한 툴 설치
3. C++ 기본 문법, C++ 간단 작업 방법
4. 플랫폼을 계속 움직이게 하기
5. 플랫폼의 설정 구성(움직이는 속도 등)  
6. 이 플랫폼을 다시 보내서 앞뒤로 움직이게 하기
7. 회전하는 플랫폼 만들기

### ✔️프로젝트 셋업
두 에셋 사용  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/cb6f23bf-813d-4184-b913-3fc590984a76/image.png)  

* 러닝 키트의 레벨을 복제해서 Main 레벨로 사용  
* 캐릭터 키트 에셋을 임포트해서 3D 캐릭터 얹어놓기  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/2bdd790b-4457-47bd-ae7d-74f4b325af91/image.png)

캐릭터의 Mesh가 마네킹 모양  

### ✔️캐릭터 커스터마이징하기
꺼낸 3D 캐릭터 액터의 `자손 블루프린트 클래스` 생성 > 디테일 창의 `플레이어 자동 빙의` Defualt에서 `Player 0`으로 변경
> 엔진에 이 캐릭터가 자동으로 빙의되어야 해서 Player 0이 자동으로 제어해야 한다고 말하는 것임  


자손 클래스 말고 원본의 블루프린트에서 컴파일 오류가 있다면 해결해주어야 함.
나의 경우엔 Turn Right Rate, Turn Right 이벤트 노드를 각각 사용해서 오류를 해결했다.


* "BP_ThirdPersonCharacter"의 `메시` 컴포넌트에서 `스켈레탈 메시 에셋`을 다른 것으로 설정  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/69270ce7-164d-42bc-8b52-5ec847fc935a/image.png)  

