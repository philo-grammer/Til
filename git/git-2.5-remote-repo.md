##  2.5 리모트 저장소

리모트 저장소를 관리할 줄 알아야 다른 사람과 함께 일할 수 있다.<br/>
다른 사람들과 함께 일한다는 것은 리모트 저장소를 관리하면서 데이터를 거기에 Push하고 Pull하는 것이다.

<br/>
#### 리모트 저장소 확인하기

git remote 명령으로 현재 프로젝트에 등록된 리모트 저장소 확인 가능

```
$ git remote
orign
```

-v 옵션을 주어 단축이름과 URL을 함께 볼 수 있다.

```
$ git remote -v
origin	git://github.com/schacon/ticgit.git (fetch)
origin	git://github.com/schacon/ticgit.git (push)
```

리모트 저장소가 여러 개 있다면  이 명령은 전부 보여준다.

```
$ git remote -v
defunkt  git://github.com/defunkt/grit.git
koke      git://github.com/koke/grit.git
origin    git@github.com:mojombo/grit.git
```

origin 만 SSH URL이기 때문에 origin에만 Push 할 수 있다.

<br/>
#### 리모트 저장소 추가하기

git remote add [단축이름] [url] 명령을 실행한다.

```
$ git remote
origin

$ git remote add pb git://github.com/paulboone/ticgit.git
$ git remote -v
origin  git://github.com/schacon/ticgit.git
pb  git://github.com/paulboone/ticgit.git
```

<br/>
#### 리모트 저장소를 Pull하거나 Fetch하기

리모트 저장소에서 데이터를 가져오려면 간단히 다음과 같이 실행한다.

```
$ git fetch [remote-name]
```

이 명령은 로컬에는 없지만, 리모트 저장소에는 있는 데이터를 모두 가져온다.

fetch 명령은 리모트 저장소의 데이터를 모두 로컬로 가져오지만, 자동을 머지하지 않는다.<br/>
그래서 로컬에서 하던 작업을 정리하고 나서 수동으로 머지해야 한다.

그냥 쉽게 git pull 명령으로 리모트 저장소 브랜치에서 데이터를 가져올 뿐만 아니라 자동으로 로컬 브랜치와 머지시킬 수 있다.

<br/>
#### 리모트 저장소에 Push 하기

이 명령은 git push [리모트 저장소 이름][브랜치 이름]으로 단순하다.

```
$ git push origin master
```

<br/>
#### 리모트 저장소 살펴보기

git remote show [리모트 저장소 이름] 명령으로 리모트 저장소의 구체적인 정보를 확인할 수 있다.

```
$ git remote show origin
* remote origin
  Fetch URL: git@github.com/schacon/ticgit.git
  Push  URL: git@github.com/schacon/ticgit.git
  HEAD branch: master
  Remote braches:
    master    tracked
    ticgit    tracked
  Local branch configured for 'git pull' :
    master merges with remote master
  Local ref configured for 'git push' :
    master pushes to master (up to date)
```

<br/>
#### 리모트 저장소 이름을 바꾸거나 리모트 저장소를 삭제하기

git remote rename 명령으로 리모트 저장소의 이름을 변경할 수 있다.<br/>
예를 들어 pb를 paul로 변경하려면 git remote rename 명령을 사용한다.

```
$ git remote rename pb paul
$ git remote
origin
paul
```

리모트 저장소를 삭제해야 한다면 git remote rm 명령을 사용한다. 

```
$ git remote rm paul
$ git remote
origin
```

