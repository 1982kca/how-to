Git 저장소 파일의 상태 실습
===

지난 시간에는 Untracked, Staged, Modified, Unmodified 상태에 대한 이론적인 이야기를 했다.    
하지만 이론을 이해한다고 다가 아니기에... 각각의 상황에서 어떤 명령어를 사용하는지 알아보자.

저장소를 만드는 방법
---

Git 저장소를 만드는 방법은 두 가지가 있다고 했다.

- (init) 새로운 디렉토리를 생성하고 새로운 프로젝트를 위한 Git 저장소를 생성한다.
- (clone) 기존에 존재하는 프로젝트의 Git 저장소를 내려 받아 프로젝트를 이어서 진행한다.

새로운 프로젝트를 위한 Git 저장소를 만들고자 한다면 프로젝트의 루트 디렉토리에서 다음 명령어를 사용하면 된다.

```bash
$ git init
```

지난 시간에 살짝 언급했지만 이 명령어를 사용하면 `.git` 이라는 이름의 특별한 디렉토리가 생성된다.    
Linux와 Mac에서 `.` 으로 시작하는 파일/디렉토리는 숨김 파일이다.    
따라서 현재 디렉토리의 파일들을 그냥 출력해보면 안보일 거고, 다음과 같이 숨김 파일을 포함해서 출력하라는 `-a` 플래그를 사용하면 이 디렉토리가 존재한다는 것을 확인할 수 있을 것이다.

```bash
$ ls -a
```

기존에 존재하는 Git 저장소를 내려 받고자 한다면 해당 저장소의 URL이 필요하다.    
그것은 개인 서버일 수도 있고 GitHub이나 GitLab, BitBucket 같은 Git 호스팅 사이트의 URL일 수도 있다.    
아무튼 `<Git URL>` 이라는 URL에 대하여 그것을 내려 받고자 한다면 프로젝트 디렉토리를 저장하고 싶은 곳에서 다음 명령어를 사용하면 된다.

```bash
$ git clone <Git URL>
```

가령 GitHub에 있는 [1982kca/how-to](https://github.com/1982kca/how-to) 저장소를 내려받고 싶다면

```bash
$ git clone https://github.com/1982kca/how-to.git
```

이렇게 하면 기본적으로 저장소 이름과 동일한 이름의 디렉토리가 생성된다.    
위 명령어의 경우 `how-to` 라는 이름의 디렉토리를 생성하며 그 디렉토리는 `.git` 디렉토리와 프로젝트 파일들을 가지고 있다.

만약 디렉토리를 다른 이름 `<Directory Name>` 으로 저장하고 싶다면 다음과 같이 할 수 있다.

```bash
$ git clone <Git URL> <Directory Name>
```

앞서 언급된 저장소를 `kca-docs` 라는 이름의 디렉토리로 내려 받고 싶다면 다음과 같이 하는 식이다.

```bash
$ git clone https://github.com/1982kca/how-to.git kca-docs
```

이미 Git 저장소 디렉토리인 곳에 `git init` 을 시도하면 오류가 발생한다.    
그리고 이미 Git 저장소 디렉토리인 곳에 `git clone` 을 할 경우 Git 저장소가 내려 받아지기는 하나, Git 저장소가 중첩되면서 의도치 않은 동작을 야기할 수 있으니 사용 시 유의하도록 하자.

실습
---

자, 이제 직접 Git 저장소 디렉토리를 만들고 파일들의 상태를 변환해보자.    
우선 새 디렉토리를 생성하고 그것을 Git 저장소 디렉토리로 만든다.

```bash
$ mkdir git-example
$ cd git-example
git-example$ git init
Initialized empty Git repository in /path/to/git/repo/directory/git-example/.git/
```

`git-example`이라는 이름의 디렉토리를 만들고 그것을 Git 저장소 디렉토리로 만들었다.    
디렉토리 내 파일을 숨김 파일을 포함하여 출력해보면 현재 디렉토리(`.`), 상위 디렉토리(`..`) 그리고 Git 디렉토리(`.git`)가 존재하는 것을 알 수 있다.

```bash
git-example$ ls -a
.  ..  .git
```

파일의 상태를 확인하기 위해서는 다음과 같은 명령어를 사용한다.

```bash
git-example$ git status
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

아직 그 어떤 파일도 생성하지 않았기 때문에 위와 같이 출력될 것이다.    
(git 버전에 따라 `main` 이 아니라 `master` 일 수도 있다.)

이제 파일을 하나 생성해보자.

```bash
git-example$ touch testfile
```

`touch` 명령어는 내용이 비어 있는 파일을 생성한다.    
디렉토리 내 파일을 출력해보면 새 파일이 생성된 것을 확인할 수 있다.

```bash
git-example$ ls
testfile
```

새로 만든 파일은 아직 staging area에 올리지 않았으니 Untracked 상태다.    
실제로 확인해보면,

```bash
git-example$ git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	testfile

nothing added to commit but untracked files present (use "git add" to track)
```

`testfile`이라는 이름의 Untracked file이 있음을 확인할 수 있다.    
이것을 staging area에 추가(add)하기 위해서는 말 그대로 `add` 를 하면 된다.

```bash
git-example$ git add testfile
```

`git add` 명령어 뒤에는 기본적으로 파일 이름이 붙지만 디렉토리 이름이 오면 해당 디렉토리와 하위 모든 파일들을 Staged 상태로 만든다.    
또한 애스터리스크(`*`)를 통해 파일을 일괄적으로 선택할 수 있다.    
예를 들어 `*`라고 하면 모든 파일을, `test*`라고 하면 `test`로 시작하는 모든 파일을 의미한다.    
그리고 띄어쓰기 간격으로 여러 개의 파일을 한 번에 추가할 수 있으며, 저장소 디렉토리에 있는 모든 파일을 추가하고자 한다면 `--all` 플래그를 사용할 수 있다.

이제 파일의 상태를 다시 확인해보면,

```bash
git-example$ git status
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
	new file:   testfile
```

staging area에 올라가 이제 commit 할 수 있는 파일이 하나 있으며 그 이름이 `testfile`임을 알 수 있다.    
staging area에서 제외하고자 한다면 `git rm --cached`를 사용하면 되는데, 이 때 `--cached` 플래그를 사용하지 않으면 파일 자체가 삭제됨을 주의하자.    
말 나온 김에 이야기하자면, 저장소 디렉토리에서 파일을 삭제하면 그것은 Git에 반영되지 않는다.    
파일이 삭제되었다는 사실을 staging area에 알려야 하는데 이 때 플래그가 붙지 않은 `git rm`가 사용된다.

staging area에서 파일을 제외해보고자 한다면 다음을 실행하자.

```bash
git-example$ git rm --cached testfile
```

이것을 해보았다면 다음 실습을 이어 나가기 위해 다시 위에서 한 것처럼 staging area에 추가한다.

staging area의 파일을 Git 저장소에 기록(commit)하고자 한다면 다음과 같은 명령어를 사용한다.

```bash
git-example$ git commit -m "Initial Commit"
[main (root-commit) 2671ca0] Initial Commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 testfile
```

(출력되는 문자열에 차이가 있을 수 있는데 `2671ca0`에 해당하는 부분은 각 commit의 고유한 해시값으로 각자 차이가 있을 것이다.)

commit은 항상 무엇을 변경하였는지 설명하는 간단한 메시지를 포함하는데 `-m "<Message>"` 플래그를 통해 메시지를 작성할 수 있다.    
혹은, 그냥 `git commit` 까지만 입력할 경우, 운영체제에 기본 편집기로 지정되어 있는 편집기가 열리면서 commit 메시지를 작성하라고 한다.

commit을 한 후 파일의 상태를 확인해보면,

```bash
git-example$ git status
On branch main
nothing to commit, working tree clean
```

commit 하기 위한 staging area에 아무 것도 없음을 알 수 있다. (staging area를 작업 트리[working tree]라고도 한다.)    
Unmodified 상태가 된 것이다.

이번에는 파일을 수정해보자.    
각자 편한 편집기를 사용하여 파일을 열고 다음과 같이 작성하여 저장해보자.

```
hello, KCA!
```

그리고 상태를 확인해보면

```bash
git-example$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   testfile

no changes added to commit (use "git add" and/or "git commit -a")
```

`modified` 라고 표시되며 `git add` 혹은 `git restore` 를 사용하여 commit하거나 변경 사항을 무시할 수 있다는 알림이 뜬다.    
이와 같은 Modified 상태에서는 가장 마지막으로 commit된 상태랑 비교할 수 있는데, `git diff` 명령을 사용하면 된다.

```bash
git-example$ git diff
diff --git a/testfile b/testfile
index e69de29..495566b 100644
--- a/testfile
+++ b/testfile
@@ -0,0 +1 @@
+hello, KCA!
```

직전 commit(`a`)보다 현재 상태(`b`)가 `testfile`이라는 파일에 한 줄 많으며 `hello, KCA!` 가 추가되었음을 확인할 수 있다.    
제거된 부분은 앞에 `-` 가 붙어서 표시되며 추가된 부분은 앞에 `+` 가 붙어서 표시된다.    

직전 commit이 아닌 오래 전의 commit과 비교하기 위해서는 해당 commit의 해시값을 사용한다.

commit의 해시값은 commit을 하는 순간 `2671ca0`와 같은 단축형으로 나오며, `git log`를 통해 전체 해시값을 확인할 수 있다.

```bash
git-example$ git log
commit 2671ca0ae1f5c2af61d642044ae6e81d320c614f (HEAD -> main)
Author: Pt J <peter.j@kakao.com>
Date:   Sun Feb 14 19:55:21 2021 +0900

    Initial Commit
```

단축형은 해시값의 처음 7자리 수로, `git log`에 `--oneline` 플래그를 설정해 확인할 수 있다.

```bash
git-example$ git log --oneline 
2671ca0 (HEAD -> main) Initial Commit
```

해시값을 사용할 땐 전체 해시값과 단축형 둘 다 사용 가능하다. 즉,

```bash
git-example$ git diff 2671ca0ae1f5c2af61d642044ae6e81d320c614f
```

와

```bash
git-example$ git diff 2671ca0
```

는 정확히 동일한 출력을 갖는다.

현재 상태, 즉 Modified 상태에서 이 파일을 `git rm --cached` 하면 저장소에 있던 파일은 삭제된 것으로 간주되며 해당 파일은 Unstaged 상태가 된다.    
물론 Git 입장에서만 파일이 제거된 것뿐, 디렉토리에 잘 남아아있다.    
그리고 이걸 다시 `git add` 를 통해 staging area에 추가하면 Staged 상태가 된다.

```bash
git-example$ git rm --cached testfile 
rm 'testfile'
git-example$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	deleted:    testfile

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	testfile
git-example$ git add testfile
git-example$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   testfile
```

`modified` 가 적혀 있지만 아까와의 차이점이 있다면 `Changes not staged for commit` 이 아니라 `Changes to be committed` 라는 점이다.    
`git rm --cached` 를 하지 않은 Modified 상태에서는 `git add` 명령어를 통해 이 상태로 전환할 수 있다.    
`git rm --cached` 를 통해 staging area에서 내릴 수 있는 것은 Unmodified 상태에서도 마찬가지이며 다시 `git add` 명령어를 사용하면 아무 일도 없던 것처럼 돌아간다.

그리고 이 상태에서 `git restore --staged` 명령어를 사용하면 이전의 Modified 상태로 돌아간다.

```bash
git-example$ git restore --staged testfile
git-example$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   testfile

no changes added to commit (use "git add" and/or "git commit -a")
```

Staged 상태의 파일이 없을 땐 commit을 할 수 없다.    
지금 Modified 상태인 파일만 둔 채 commit을 시도하면

```bash
git-example$ git commit -m "modified"
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   testfile

no changes added to commit (use "git add" and/or "git commit -a")
```

commit할 변동사항이 없다고 한다.    
로그를 찍어보면 방금 입력한 commit 메시지로 아무것도 commit되지 않은 것을 확인할 수 있다.

```bash
git-example$ git log
commit 2671ca0ae1f5c2af61d642044ae6e81d320c614f (HEAD -> main)
Author: Pt J <peter.j@kakao.com>
Date:   Sun Feb 14 19:55:21 2021 +0900

    Initial Commit
```

물론 다시 staging area에 올리면 commit 할 수 있게 된다.

```bash
git-example$ git add testfile 
git-example$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   testfile

git-example$ git commit -m "modified"
[main 4172fad] modified
 1 file changed, 1 insertion(+)
git-example$ git log
commit 4172fad95f508e7bc63c6167fd870522d686e58f (HEAD -> main)
Author: Pt J <peter.j@kakao.com>
Date:   Mon Feb 15 00:02:54 2021 +0900

    modified

commit 2671ca0ae1f5c2af61d642044ae6e81d320c614f
Author: Pt J <peter.j@kakao.com>
Date:   Sun Feb 14 19:55:21 2021 +0900

    Initial Commit
```

마지막으로 staging area에 파일을 추가한 후에 수정하는 경우를 확인해보겠다.    
`testfile` 파일을 열어 다음과 같이 내용을 추가한다.

```
hello, KCA!
it will be added
```

그리고 staging area에 추가하여 Staged 상태로 만든다.

```bash
git-example$ git add testfile
git-example$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   testfile
```

이 상태로 `testfile` 파일을 다시 열어 내용을 또 추가한다.

```
hello, KCA!
it will be added
just modified
```

이번엔 이걸 staging area에 추가하지 않고(!) 상태를 확인해보겠다.

```bash
git-example$ git status
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   testfile

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   testfile
```

Staged 상태의 `testfile` 과 Modified 상태의 `testfile` 이 존재함을 알 수 있다.    
이 둘은 실제로는 같은 파일이며 단지 어떤 순간을 기록해놓았는가의 차이다.    
이 상태에서 commit을 하면 Staged 상태의 `testfile` 만 반영되고 Modified 상태의 것은 Modified인 채로 남는다.

```bash
git commit -m "Test modify"
[main fd9efd7] Test modify
 1 file changed, 1 insertion(+)
git-example$ git status
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   testfile

no changes added to commit (use "git add" and/or "git commit -a")
```

`git diff` 명령어로 비교해보면 마지막 문장이 추가되지 않은 상태의 것이 commit 되었음을 확인할 수 있다.

```bash
git-example$ git diff
diff --git a/testfile b/testfile
index 58f1019..539b123 100644
--- a/testfile
+++ b/testfile
@@ -1,2 +1,3 @@
 hello, KCA!
 it will be added
+just modified
```

추가적으로, 어떤 파일에 대한 반영 사항을 무시하고 마지막 commit 상태로 돌아가고 싶다면 다음 명령어를 사용할 수 있다.

```bash
git-example$ git restore testfile
```

정리
---

사실 어떤 상태에서 다른 상태로 가는 모든 변환을 다 기억하고 있지 않아도 된다.    
Unmodified에서 Unstaged로 가고, 이런 건 실제로 그리 자주 사용되지 않는다.

앞서 다룬 내용을 간단히 요약하자면 다음과 같다.

- Unstaged 또는 Modified 상태의 파일은 `git add` 명령어를 통해 Staged 상태가 된다.    
- Staged 상태의 파일은 `git commit` 명령어를 통해 Unmodified 상태가 된다.    
- Staged 또는 Unmodified 상태의 파일을 수정하면 Modified 상태가 된다. (단 Staged 상태였던 파일은 Staged 상태를 남겨둔 채 Modified 상태가 추가된다.)    
- 모든 상태의 파일은 `git rm --cached` 명령어를 통해 Unstaged 상태가 된다.    
- 마지막 commit 상태로 돌아가려면 `git restore` 명령어를 사용할 수 있다.

파일의 이름을 변경할 땐 `git mv <Original Name> <New Name>` 으로 하면 된다는 건 여담.

처음에는 다 외우려고 하기 보다는 "staging area에 올리는 명령어가 뭐였지?"하며 자료를 참고해서 해보는 것으로 충분하다.    
어느 정도 익숙해질 때까지 앞서 만든 저장소 디렉토리에서 파일을 생성 및 수정하며 파일의 상태를 여러 방향으로 전환해보는 것도 괜찮은 선택이다.    

다음 시간에는 commit들을 쌓아가며 프로젝트를 관리하는 것에 대한 이야기를 하도록 하겠다.    
[>>> 04. branch란 무엇인가](chapter04.md)
