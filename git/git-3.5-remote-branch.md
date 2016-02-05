## 3.5 리모트 브랜치

#### origin 의 의미

브랜치 이름으로 많이 사용하는 “master”라는 이름이 괜히 특별한 의미를 가지는 게 아닌 것처럼 “origin”도 특별한 의미가 있는 것은 아니다. git init 명령이 자동으로 만들기 때문에 사용하는 이름인 “master”와 마찬가지로 “origin”도 git clone 명령이 자동으로 만들어주는 리모트 이름이다. git clone -o booyah 라고 옵션을 주고 명령을 실행하면 booyah/master 라고 사용자가 정한 대로 리모트 이름을 생성해준다.

그림 3-22 저장소를 Clone하면 로컬 master 브랜치와 리모트 저장소의 master 브랜치를 가리키는 origin/master 브랜치가 생김

![remote-branches-1](https://git-scm.com/book/en/v2/book/03-git-branching/images/remote-branches-1.png)

그림 3-23 로컬과 서버의 커밋 히스토리는 독립적임

![remote-branches-2](https://git-scm.com/book/en/v2/book/03-git-branching/images/remote-branches-2.png)

리모트 서버로부터 저장소 정보를 동기화하려면 git fetch origin 명령을 사용한다. 명령을 실행하면 우선 origin 서버의 주소 정보(이 예에서는 git.ourcompany.com)를 찾아서, 현재 로컬의 저장소가 갖고 있지 않은 새로운 정보가 있으면 모두 내려받고, 받은 데이터를 로컬 저장소에 업데이트하고 나서, origin/master 포인터의 위치를 최신 커밋으로 이동시킨다.

![remote-branches-3](https://git-scm.com/book/en/v2/book/03-git-branching/images/remote-branches-3.png)

그림 3-25 서버를 리모트 저장소로 추가하기

![remote-branches-4](https://git-scm.com/book/en/v2/book/03-git-branching/images/remote-branches-4.png)

그림 3-26 로컬 저장소에 만들어진 teamone의 master 브랜치를 가리키는 포인터

![remote-branches-5](https://git-scm.com/book/en/v2/book/03-git-branching/images/remote-branches-5.png)


<br/>
#### Push 하기

serverfix라는 브랜치를 다른 사람과 공유할 때에도 브랜치를 처음 Push 하는 것과 같은 방법으로 Push 한다. 아래와 같이 git push (remote) (branch) 명령을 사용한다.

```
$ git push origin serverfix
Counting objects: 24, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (24/24), 1.91 KiB | 0 bytes/s, done.
Total 24 (delta 2), reused 0 (delta 0)
To https://github.com/schacon/simplegit
 * [new branch]      serverfix -> serverfix
```

나중에 누군가 저장소를 Fetch하고 나서 서버에 있는 serverfix 브랜치에 접근할 때 origin/serverfix라는 이름으로 접근할 수 있다.

```
$ git fetch origin
remote: Counting objects: 7, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/schacon/simplegit
 * [new branch]      serverfix    -> origin/serverfix
```

여기서 짚고 넘어가야 할 게 있다. Fetch 명령으로 리모트 브랜치를 내려받는다고 해서 로컬 저장소에 수정할 수 있는 브랜치가 새로 생기는 것이 아니다. 다시 말해서 serverfix라는 브랜치가 생기는 것이 아니라 그저 수정 못하는 origin/serverfix 브랜치 포인터가 생기는 것이다.

새로 받은 브랜치의 내용을 Merge하려면 git merge origin/serverfix 명령을 사용한다. Merge 하지 않고 리모트 브랜치에서 시작하는 새 브랜치를 만들려면 다음과 같은 명령을 사용한다.

```
$ git checkout -b serverfix origin/serverfix
Branch serverfix set up to track remote branch serverfix from origin.
Switched to a new branch 'serverfix'
```

그러면 origin/serverfix에서 시작하고 수정할 수 있는 serverfix라는 로컬 브랜치가 만들어진다.

<br/>
#### 리모트 브랜치 삭제

협업하는 데 사용했던 그 리모트 브랜치는 이제 안정화됐으므로 삭제할 수 있다.
serverfix 라는 리모트 브랜치를 삭제하려면 다음과 같이 실행한다.

```
$ git push origin --delete serverfix
To https://github.com/schacon/simplegit
 - [deleted]         serverfix
```

위 명령을 실행하고 나면 서버의 브랜치는 삭제된다.
이 명령은 앞서 살펴본 git push [remotename] [localbranch]:[remotebranch] 형식으로 기억하는 것이 좋다. [localbranch] 부분에 비워 둔 채로 실행하면 '로컬에서 빈 내용을 리모트의 [remotebranch]에 채워 넣어라'라는 뜻이 되기 때문이다.

