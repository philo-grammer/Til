## 2.2 수정하고 저장소에 저장하기

워킹 디렉터리의 모든 파일은 크게 Tracked(관리대상임)와 Untracked(관리대상이아님)로 나눈다.
Tracked 파일은 이미 스냅샷에 포함돼 있던 파일이다. Tracked 파일은 또 Unmodified(수정하지 않음)와 Modified(수정함) 그리고 Staged(커밋하면 저장소에 기록되는) 상태 중 하나이다.

![File Status Lifecycle](http://git-scm.com/figures/18333fig0201-tn.png)

처음 저장소를 Clone하면 모든 파일은 Tracked이면서 Unmodified 상태가 된다. 
파일을 Checkout하고 나서 아무것도 수정하지 않았기 때문에 그렇다.


#### 파일의 상태 확인하기

파일의 상태를 확인하려면 보통 git status 명령을 사용한다.

```
$ git status
# On branch mster
nothing to commit (working directory clean)
```

위의 내용은 파일을 하나도 수정하지 않았다는 것을 말해준다. 즉, Tracked와 Modified 상태의 파일이 없다.

프로젝트에 README 파일을 만들어보자. README 파일은 새로 만든 파일이이기 때문에 git status를 실행하면 'Untracked files'에 들어 있다.

```
$ vim README
$ git status
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#   README
nothing added to commit but untracked files present (use "git add" to track)
```

Git은 Untracked 파일을 아직 스냅샷(커밋)에 넣어지지 않은 파일이라고 본다. 파일이 Tracked 상태가 되기 전까지는 Git은 절대 그 파일을 커밋하지 않는다. 그래서 일하면서 생성하는 바이너리 파일 같은 것을 커밋하는 실수는 하지 않게 된다. README 파일을 추가해서 직접 Tracked 상태로 만들어보자.


#### 파일을 새로 추적하기

git add 명령을 실행하면 Git은 README 파일을 추적한다.

```
$ git add README
```

git status 명령을 다시 실행하면 README 파일이 Tracked 상태이면서 Staged 상태라는 것을 확인할 수 있다.

```
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   new file:  README
#
```

'Changes to be committed'에 있는 파일은 Staged 상태라는 것을 의미한다. 커밋하면 git add를 실행한 시점의 파일이 저장소 히스토리에 저장된다.
앞에서 git init 명령을 실행했을 때 바로 git add (files) 명령을 실행했었다. 이 명령은 워킹 디렉터리에 있는 파일을 새로 추적하게 한다. 


