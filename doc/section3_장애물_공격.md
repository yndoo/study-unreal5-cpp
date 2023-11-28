## 강의 개요
* 함수, 변수, 브랜치 in C++
* C++로 자체 액터 생성하기
* C++ 코드 구조
* C++ 컴파일, 언리얼 라이브 코딩 시스템  
* 블루프린트와 C++ 연결
* 템블릿에 포함된 표준 에셋 외의 커스텀 캐릭터 클래스 설정하는 법

### '장애물 공격' 게임 Action Plan
1. 프로젝트 생성하고 여러 에셋 가져오기  
2. C++를 위한 툴 설치
3. C++ 기본 문법, C++ 간단 작업 방법
4. 플랫폼을 계속 움직이게 하기
5. 플랫폼의 설정 구성(움직이는 속도 등)  
6. 이 플랫폼을 다시 보내서 앞뒤로 움직이게 하기
7. 회전하는 플랫폼 만들기

## ✔️용어집(섹션3 전체)
_컴파일러와 에디터_
* Source Code : 사람이 작성하는, 읽을 수 있는 코드 (C++처럼)
* Binary Executable 바이너리 실행 코드 : 0과 1로 구성된 기계가 읽을 수 있는 코드
* Compiler : 소스 코드를 바이너리 코드로 변환해 주는 소프트웨어, 인간이 읽는 C++나 블루프린트를 기계 언어로 변환해줌
* Surce Code Editor : C++처럼 사람이 읽는 코드를 쓸 때 더 편하게 만들어 주는 것, 맞춤법 검사 같은 것

## 학습 내용
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

### ✔️컴파일러와 에디터
![](https://velog.velcdn.com/images/kuronuma_daisy/post/620c2565-2511-4287-99dc-897d41f7bfd5/image.png)  

### ✔️Visual Studio, .NET, VS Code 설치하기
[언리얼 버전에 따라 맞는 비쥬얼 스튜디오 버전 확인하기](https://docs.unrealengine.com/5.3/en-US/setting-up-visual-studio-development-environment-for-cplusplus-projects-in-unreal-engine/)  
[.NET SDK 설치](https://dotnet.microsoft.com/ko-kr/download/dotnet?cid=getdotnetcore)  
[VS Code 설치](https://code.visualstudio.com/)  


* 나는 비.스 깔려있어서 워크로드에서 `C++을 사용한 게임 개발`과 `언리얼 엔진 installer`를 포함하도록 수정했음  
* .NET 6.0 다운로드 했음
* VS Code 설치 했음

### ✔️C++ 프로젝트 컴파일링하기
`편집 탭 > 에디터 개인설정 > 일반 > 소스 코드 > 소스 코드 에디터 > "Visual Studio Code"로 설정`  
`툴 탭 > 새로운 C++ 클래스 > 움직이는 플랫폼을 만들 것이기 때문에 "Actor" 부모 클래스 선택`  (여기서 발생하는 몇몇 에러는 언리얼 업데이트 등으로 해결했음..)  
`VS Code > Terminal 탭 > "Run Build Task > "ObstacleAssaultEditor Win64 Development Build"` (Run Build Task : Ctrl + Shift + B)  

-> MovingPlatform의 클래스가 생김(완전히 빈 상태인 액터)  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/5d861abd-e34d-48ee-811d-5d7a3aaa68f2/image.png)  

---


### 👾gitignore의 중요성
처음 repository 생성할 때 `.gitignore` 파일을 만들지 않아서 생긴 문제!!
바로바로 용량 문제이다. 현재 깃허브 Free버전을 사용하고 있기 때문에 한 파일의 크기가 100MB가 넘으면 LFS를 사용해서 커밋해야한다. 그리고 한 파일의 크기 1GB를 넘으면 유료버전을 사용해야만 올릴 수 있다..!   
[100MB 이상의 파일 깃허브에 올리는 방법..](https://medium.com/@stargt/github%EC%97%90-100mb-%EC%9D%B4%EC%83%81%EC%9D%98-%ED%8C%8C%EC%9D%BC%EC%9D%84-%EC%98%AC%EB%A6%AC%EB%8A%94-%EB%B0%A9%EB%B2%95-9d9e6e3b94ef)  
[Git LFS Data 1GB 이상 사용 시 유료로..](https://hbase.tistory.com/221)  

그치만 문제의 파일을 보니 pch 파일? 미리 컴파일된 헤더 파일이라는데 그거를 왜올려!!! 뭔가 이상해서 보니 이 저장소에 `.gitignore`파일이 없었다는 것을 알게 되었다..
![](https://velog.velcdn.com/images/kuronuma_daisy/post/49a696a5-77d2-4aad-b31a-be6639f2db2f/image.png)  

"Unreal Engine", "Visual Studio", "Visual Studio Code" 에 해당하는 gitignore 파일을 생성 및 적용하여 용량문제는 해결하였다!!  

문제 해결에 도움을 주신 인디게임 머시깽이 오픈카톡 선생님들께 감사하당...😭

---  

### ✔️UPROPERTY 변수
