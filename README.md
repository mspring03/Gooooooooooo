# Go 옹부 시작
## 초기 환경 설정

1. Go [설치](https://golang.org/dl/)

2. Go Workspace 설정

   프로젝트를 진행할 폴더를 생성합니다.

   그후에 반드시 ```bin```, ```pkg```, ```src``` 3개의 폴더를 생성합니다

   각 폴더의 역할은 다음과 같다

   > **bin 폴더** *: 소스파일 컴파일 후 운영체제별 실행 가능한 바이너리(Binary)파일이 저장되는 곳*  
   > **pkg 폴더** *: 프로젝트에 필요한 패키지가 컴파일 되어 라이브러리 파일이 저장되는 곳*  
   > **src 폴더** *: 직접 작성한 소스 코드 및 오픈 소스 코드를 저장하는 곳*

3. Workspace 환경 변수 설정

   > 윈도우 제어판 -> 시스템 -> 고급 시스템 설정 -> 환경 변수에 GOPATH 를 등록합니다.
   >
   > go env 명령어를 실행 후 위에서 설정한 GOPATH 경로가 정확한지 확인합니다.

   ```
   # mac os
   $ mkdir -p ~/workspace/go
   # 아래 환경변수 선언은 .bashrc에 작성하는 것이 좋음
   $ export GOPATH=~/workspaces/go
   ```

---
## **IDE**
`Goland` : JetBrains가 만든 Go 개발용 IDE  
<br>

### **간단 명령어**
`⌘,` : 설정(Preferences) 창을 엽니다.

`⌘E` : 최근 사용한 파일 목록을 조회합니다.(Recent files popup)

`Double⇧` : 가장 자주 사용되는 단축키 입니다. 파일, 클래스, 설정 등 키워드에 관련된 가능한 모든 것을 검색해 보여줍니다.( Search everywhere )

`⌥Space` : 구현된 코드를 조회합니다. (Quick Definition)  
`⌘B` : 해당 코드의 선언부로 이동.  
`⌘⌥B` : 해당 코드의 구현부로 이동.  
`⌥F7` : 해당 항목이 사용된 위치 검색   

`⌘D` : 라인 복제 (Duplicate current line)  
`⌘⌫` : 라인 삭제 (Delete line at caret)  
`⌥↑,⌥↓` : 커서 근처의 코드 선택 영역을 확대하거나 축소합니다.  
`⌥←,⌥→` : 단어별 포커스 이동  
`⌥⇧←,⌥⇧→` : 단어별 선택  
`fn↑,fn↓` : Page Up/Down  
`fn←,fn→` : 라인 시작,끝으로 이동  
`fn⇧←,fn⇧→` : 라인 전체 선택  
 
---
## **공식문서**
* [Golang](https://golang.org/doc/)
* [Gorm](https://gorm.io/ko_KR/)

## **내가 보고 공부한 블로그 & 흥미로운 글**
### **GO**
* [효과적인 Go 프로그래밍](https://gosudaweb.gitbooks.io/effective-go-in-korean/content/)

### **데이터 타입**
* [예제로 배우는 Go 프로그래밍](http://golang.site/Go/Basics)  
   **slice**
   * [Slice의 함정](https://docs.google.com/document/d/1t0LDzDEbc6zYlehlBWR8n6hdHyq89X8pYjs0wui_V40/mobilebasic)
   * [Slice는 포인터인가 포인터가 아닌가](https://docs.google.com/document/d/1t0LDzDEbc6zYlehlBWR8n6hdHyq89X8pYjs0wui_V40/mobilebasic)

### **Auth**
* [Go 언어로 jwt인증 서버 만들기](https://covenant.tistory.com/203)

### **Test**
* [Golang assert와 mock Testify 라이브러리 알아보기](https://minwook-shin.github.io/go-common-assertions-and-mocks-testify/)

### **docker** 
* [Go 프로젝트 docker 이미지 99.2% 줄이기](https://docs.google.com/document/d/1t0LDzDEbc6zYlehlBWR8n6hdHyq89X8pYjs0wui_V40/mobilebasic)

### **Architecture**
* [Trying Clean Architecture on Golang](https://medium.com/hackernoon/golang-clean-archithecture-efd6d7c43047)
* [주니어 개발자의 클린 아키텍처 맛보기](https://woowabros.github.io/tools/2019/10/02/clean-architecture-experience.html)

### **Tool**
* [호출 그래프에서 시작하는 Go 코드 읽기](https://docs.google.com/document/d/1TZ-SWt9StV_WPvBnBkbORci0fKSsc2TtUlsnPVVIlMU/mobilebasic)

