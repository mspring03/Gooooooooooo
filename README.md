# Go 옹부 시작
## 초기 환경 설정

1. Go [설치]([Downloads - The Go Programming Language (golang.org)](https://golang.org/dl/))

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

