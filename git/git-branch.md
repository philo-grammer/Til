# 브랜치 생성

### git branch : 브랜치를 보는 방법

`git branch` 명령어는 브랜치 목록을 표시하고, 현재 어떤 브랜치를 사용하는지 확인할 수 있는 명령어입니다.

### git checkout -b : 브랜치를 만들고 변경하는 방법

```
$ git checkout -b feature-A
```

이는

```
$ git branch feature-A
$ git checkout feature-A
```

를 순서대로 실행하는 것과 동일하게 작동합니다.

### git merge : 브랜치 merge

feature-A 브랜치를 master 브랜치에 merge 하겠습니다.

```
$ git checkout master
$ git merge --no-ff feature-A
```

브랜치로부터 merge하는 것을 기록으로 명확히 남기려면 --no-ff 옵션을 주어서 merge commit을 작성하면 됩니다.

### git log --graph : 브랜치를 시각적으로 확인

토픽 브랜치(feature-A)에 commit된 내용이 merge된 것을 확인할 수 있습니다.




