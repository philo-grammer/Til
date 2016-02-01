## 2.7 팁과 트릭

#### Git Alias

git config를 사용하여 가 명령의 Alias를 쉽게 만들 수 있다.<br/>
아래는 Alias을 만드는 예이다.

```
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
```

이미 있는 명령을 편리하고 새로운 명령으로 만들어 사용할 수 있다.<br/>
예를 들어 파일을 Unstage 상태로 변경하는 명령을 만들어서 불편함을 덜 수 있다.<br/>
다음과 같이 unstage라는 Alias를 만든다.

```
$ git config --global alias.unstage 'reset HEAD --'
```

아래 두 명령은 동일한 명령이다.

```
$ git unstage fileA
$ git reset HEAD fileA
```

추가로 last 명령을 만들어보자.

```
$ git config --global alias.last 'log -l HEAD'
```

이제 최근 커밋을 좀 더 쉽게 확인할 수 있다.

```
$ git last
commit 66938dae....................04646
Author: Josh Goebel <dreamer3@example.com>
Date:   Tue Aug 26 19:48:51 2008 +0800

   test for current head

   Signed-off-by: Scott Chacon <schacon@example.com>
```

!를 제일 앞에 추가하면 외부 명령을 실행한다.<br/>
아래 명령은 git visual이라고 입력하면 gitk가 실행된다.

```
$ git config --global alias.visual "!gitk"
```

