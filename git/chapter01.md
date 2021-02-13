Git 설치 및 초기 설정
===

Git을 어떻게 설치하는지, 그리고 어떻게 설정하는지 알아보자.    
앞으로 나오는 코드 상의 `$`는 프롬프트로, 이것 다음에 오는 명령어를 터미널에서 입력하되 `$`는 포함하지 않는다.

설치하기
---

Git을 어떻게 설치하는가! 는 운영체제에 따라 다르다.    
Linux/Mac/Windows 외의 운영체제를 사용하는 사람은 없으리라 믿고 이 세 가지 방식만 이야기하도록 하겠다.    
~~이랬는데 Solaris 사용자가 나타난다면? Solaris를 사용할 정도면 이 문서를 읽을 필요가 없지 않을까...~~

순서는 공평하게(?) 사전순으로 하겠다.    
~~사용자 수의 역순인 것 같다면 착각이다. 절대 작성자의 리눅스 편애가 아님을 밝힌다...?~~

### Linux에서 설치하기

Linux에서 Git을 설치하는 방법은 간단하다.    
터미널을 열고 명령어 한 줄만 입력하면 된다.

자신이 사용하는 Linux가 Fedora, CentOS 등 RedHat 계열의 Linux라면 다음과 같은 명령어를 입력한다.

```bash
$ sudo dnf install git
```

그리고 Ubuntu, Linux Mint 등 Debian 계열의 Linux에서는 다음과 같은 명령어를 입력한다.

```bash
$ sudo apt install git
```

이 때, 관리자 권한을 요구하는 `sudo` 명령어로 인해 비밀번호를 요구할텐데 화면에 입력되는 게 보이지 않아도 당황하지 말고 끝까지 입력하여 엔터를 누르면 된다.    
정말로 설치할 것이냐는 질문이 나오면 `Y`를 입력하여 설치하겠다고 한다.

그리고 만약 "내가 쓰는 Linux가 어떤 계열인지 모르겠다"면, [공식 문서](https://git-scm.com/download/linux)를 참고하자.    
~~다행히 Soliris 사용자도 그것이 Unix 계열이기에 이 문서를 통해 설치 방법을 확인할 수 있다!~~

다음 명령어를 통해 잘 설치가 되었는지 확인할 수 있다.    
버전명이 출력된다면 잘 설치된 것이다.
```bash
$ git --version
```

### Mac에서 설치하기

Mac을 사용한다면 높은 확률로 Git을 따로 설치할 필요가 없다.    
Mac의 개발도구인 Xcode를 사용한다면, Git을 바로 사용할 수 있을 것이다.

터미널을 열고 다음 명령어를 실행해보자.

```bash
$ git --version
```

좀 더 최신 버전의 Git이 필요하거나 Git이 설치되어 있지 않다면 다음 명령어를 통해 최신 버전의 Git을 설치할 수 있다.

```bash
$ brew install git
```

### Windows에서 설치하기

Windows에서 Git을 설치하는 방법은 여러 가지가 있다.    
[공식 배포판](https://git-scm.com/download/win)을 설치할 수도 있고, GitHub라는 Git 저장소 호스트에서 제공하는 [GitHub Desktop](https://desktop.github.com)을 사용할 수도 있다.    
Windows PC에 소프트웨어를 설치해봤다면 어렵지 않게 설치할 수 있을 것이다.    
~~사실 필자는... Windows에서 Git을 설치해본 적이 없어서... 잘 모르겠닼~~

초기 설정
---

Git은 세 가지 설정 파일을 가진다.    
하나는 운영체제 내 전체 사용자를 대상으로 한 설정 파일이고,        
하나는 현재 운영체제에 로그인 되어 있는 사용자를 대상으로 한 설정 파일이며,    
나머지 하나는 특정 저장소를 대상으로 한 설정 파일이다.

운영체제 내 전체 사용자를 대상으로 한 설정 파일은 `/etc/gitconfig`에 저장된다.    
Windows 사용자라면 `C:\ProgramData\Git\config`에 저장된다고 한다.    
이것은 시스템 전체 설정 파일이기 때문에 수정하고자 하면 관리자 권한이 필요하다.    
`git config` 명령어에 `--system` 플래그를 설정하여 이 파일을 수정할 수 있다.

현재 로그인 되어 있는 사용자를 대상으로 한 설정 파일은 해당 사용자의 홈 디렉토리에 `~/.gitconfig` 또는 `~/.config/git/config`으로 저장된다.    
Widows에서는 `C:\Users\사용자명`, 다른 운영체제에서는 `/home/사용자명` 아래에서 확인할 수 있다.    
이것은 현재 로그인된 사용자의 모든 저장소에 적용된다.    
운영체제 내에 N명의 사용자가 있다면 N명이 각각 자신의 설정 파일을 가지고 있는 것이다.    
위의 설정 파일과 충돌하는 내용은 이 설정 파일을 기준으로 적용된다.    
`git config` 명령어에 `--global` 플래그를 설정하여 이 파일을 수정할 수 있다.

특정 저장소를 대상으로 한 설정 파일은 해당 저장소 디렉토리에 `.git/config`으로 저장된다.    
이것을 사용하면 동일 사용자의 다른 프로젝트에 서로 다른 Git 설정을 적용할 수 있다.    
위의 설정 파일과 충돌하는 내용은 이 설정 파일을 기준으로 적용된다.    
`git config` 명령어에 `--local` 플래그를 설정하여 이 파일을 수정할 수 있다.    
그 어떤 플래그도 설정하지 않고 `git config` 명령어를 사용한다면 기본적으로 이 파일을 대상으로 한다.

저장소 파일의 변동 사항을 Git에 기록할 때 Git 설정 파일에 있는 사용자 정보가 사용되는데, 어떤 저장소에서 기록에 사용자 정보를 사용하고 나면 해당 저장소에서는 사용자 정보를 변경할 수 없다.    
프로젝트마다 다른 사용자 정보를 사용하고자 한다면 해당 저장소를 대상으로 한 설정 파일을 수정하도록 하자.

기본적으로는 현재 사용자의 모든 Git 저장소에 적용되는 `--global` 플래그를 사용하여 사용자 정보를 설정한다.    
필수적으로 등록해야 하는 것은 사용자 이름과 이메일이다.    
만약 사용자 이름이 `Pt J`라면 다음과 같이 사용자 이름을 등록할 수 있다.

```bash
$ git config --global user.name "Pt J"
```

사용자 이름에 띄어쓰기가 없다면 따옴표는 생략할 수 있다.    
그리고 사용자 이메일이 `peter.j@kakao.com`이라면 다음과 같이 사용자 이메일을 등록할 수 있다.

```bash
$ git config --global user.email peter.j@kakao.com
```

이메일은 띄어쓰기를 포함하지 않으므로 따옴표 사용은 선택적이다.

그리고 필수적이지는 않지만 편집기 설정이 있다.     
간혹 운영체제에서 기본으로 사용하는 편집기가 사용자가 익숙한 편집기가 아니라서 당황하는 경우가 있다.    
숙련된 사용자라면 시스템 기본 편집기를 변경하겠지만 Git 설정 파일에 Git에서 사용할 편집기를 지정해놓는 것도 하나의 방법이다.

Vim을 사용하고 싶다면

```bash
$ git config --global core.editor vim
```

Emacs를 사용하고 싶다면

```bash
$ git config --global core.editor emacs
```

와 같이 설정할 수 있다.

Windows 사용자의 경우

```bash
$ git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -nosession"
```

또는

```bash
$ git config --global core.editor "'C:/Program Files (x86)/Notepad++/notepad++.exe' -multiInst -nosession"
```

와 같이 편집기 실행 파일의 전체 경로를 입력해주어야 한다.

추가적으로, 이후에 브랜치라는 개념을 배우게 될텐데, Git은 기본적으로 `master` 라는 이름의 브랜치를 자동 >생성한다.     
그런데 master-slave 용어에 대한 비판으로 요즘은 `master` 대신 `main` 이라는 이름을 사용하는 추세다.     
기본 브랜치를 `master` 가 아닌 `main` 으로 변경하고자 한다면 다음 명령어를 사용한다. 
 
```bash 
$ git config --global init.defaultbranch main  
``` 

지금까지 설정한 내용을 확인하고 싶다면 다음 명령어를 통해 확인할 수 있다.

```bash
$ git config --list
```

혹은, 사용자 이름에 대한 설정 정보만 알고 싶다는 등 특정 부분만 알고 싶다면 다음과 같이 할 수 있다.

```bash
$ git config user.name
```

유용한 도구
---

지금까지 한 것처럼 명령어를 입력하여 실행하는 방식을 **CLI; Command-Line Interface**라고 한다.    
Git은 CLI뿐만 아니라 버튼을 클릭하는 등의 **GUI; Graphic User Interface**를 통해 사용할 수도 있다.    
하지만 GUI로 할 수 있는 모든 것은 CLI로 할 수 있지만 CLI로 할 수 있는 것 중 일부는 GUI에서 지원하지 않는다.    
그리고 처음 배울 땐 하나하나 직접 입력해가며 배우는 것이 좋다고 생각하여 여기서는 CLI를 기준으로 설명할 것이다.    

물론 어느 정도 Git에 익숙해지고 나서는 GUI 도구를 이용해도 좋다.    
Git과 함께 사용하기 좋은 유용한 GUI 도구를 몇 가지 소개하고 다음으로 넘어가도록 하겠다.    

- SourceTree    
Mac과 Windows에서 사용 가능한 도구    
자세한 내용은 [홈페이지](https://www.sourcetreeapp.com)를 참고할 것

- GitHub Desktop    
'Windows에서 설치하기'에서 언급된 그것    
Mac과 Windows에서 사용 가능한 도구    
자세한 내용은 [홈페이지](https://desktop.github.com)를 참고할 것

- GitKraken    
Linux와 Mac과 Windows에서 사용 가능한 도구    
자세한 내용은 [홈페이지](https://www.gitkraken.com)를 참고할 것

- VSC (Visual Studio Code)    
엄밀히 말하면 Git GUI 도구는 아니지만, 여러 가지 확장이 가능한 편집기로서, Git과 유관한 확장 기능도 제공된다.    
Linux와 Mac과 Windows에서 사용 가능한 도구    
자세한 내용은 [홈페이지](https://code.visualstudio.com)를 참고할 것

이 중 어떤 도구가 좋은지는... 글쎄, GUI 도구를 잘 안써봐서 모르겠다.    
VSC 밖에 안써봤는데 나쁘지 않았다.    
~~다만 습관적으로 GUI 놔두고 VSC 내장 터미널에서 CLI로 사용해서 Git GUI 도구로서 어떤지는 잘 모르겠다.~~    
개인 취향 차이도 어느 정도 있을거고... 직접 비교해보며 판단하는 게 가장 좋다고 생각한다.

자, 그러면 Git을 사용할 준비가 되었다고 생각하고 다음으로 넘어가도록 하겠다.    
[>>> 02. Git 저장소 파일의 상태](chapter02.md)
