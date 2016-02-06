## 3.6 Rebase 하기

Git에서 한 브랜치에서 다른 브랜치로 합치는 방법은 두 가지가 있다.<br/>
하나는 Merge이고 다른 하나는 Rebase다.

#### Rebase의 기초

* 그림 3-27 두 개의 브랜치로 나누어진 커밋 히스토리

![rebase-1](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-1.png)

이 두 브랜치를 합치는 가장 쉬운 방법은 앞에서 살펴본 대로 Merge 명령을 사용하는 것이다. 두 브랜치의 마지막 커밋 두 개(C3,C4)와 공통 조상(C2)을 사용하는 3-way Merge로 그림 3-28처럼 새로운 커밋을 만들어 낸다.

* 그림 3-38 나뉜 브랜치를 Merge 하기

![rebase-2](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-2.png)

비슷한 결과를 만드는 다른 방식으로, C3에서 변경된 사항을 패치(Patch)로 만들고 이를 다시 C4에 적용시키는 방법이 있다. Git에서는 이런 방식을 Rebase라고 한다. Rebase 명령으로 한 브랜치에서 변경된 사항을 다른 브랜치에 적용할 수 있다.

```
$ git checkout experiment
$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: added staged command
```

실제로 일어나는 일을 설명하자면 일단 두 브랜치가 나뉘기 전인 공통 커밋으로 이동하고 나서 그 커밋부터 지금 Checkout한 브랜치가 가리키는 커밋까지 diff를 차례로 만들어 어딘가에 임시로 저장해 놓는다. Rebase할 브랜치(experiment)가 합칠 브랜치(master)가 가리키는 커밋을 가리키게 하고 아까 저장해 놓았던 변경사항을 차례대로 적용한다.

* 그림 3-29 C3의 변경사항을 C4에 적용하는 Rebase 과정

![rebase-3](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-3.png)

그러고 나서 master 브랜치를 Fast-forward 시킨다.

* 그림 3-30 master 브랜치를 Fast-forward 시키기

![rebase-4](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-rebase-4.png)

C3`로 표시된 커밋에서의 내용은 Merge 예제에서 살펴본 C5 커밋에서의 내용과 같을 것이다.<br/>
Merge이든 Rebase든 둘 다 합치는 관점에서는 서로 다를 게 없다.<br/>
하지만, Rebase가 좀 더 깨끗한 히스토리를 만든다. 일을 병렬로 동시에 진행해도 Rebase하고 나면 모든 작업이 차례대로 수행된 것처럼 보인다.

Rebase는 보통 리모트 브랜치에 커밋을 깔끔하게 적용하고 싶을 때 사용한다.<br/>
Rebase를 하든지, Merge를 하든지 최종 결과물은 같고 커밋 히스토리만 다르다는 것이 중요하다.


<br/>
#### 좀 더 Rebase

* 그림 3-31 다른 토픽 브랜치에서 갈라져 나온 토픽 브랜치

![reabse-5](https://git-scm.com/book/en/v2/book/03-git-branching/images/interesting-rebase-1.png)

이때 테스트가 덜 된 server 브랜치는 그대로 두고 client 브랜치만 master로 합치려는 상황을 생각해보자. server와는 아무 관련이 없는 client 커밋은 C8, C9이다. 이 두 커밋을 master 브랜치에 적용하기 위해서 --onto 옵션을 사용하여 아래와 같은 명령을 실행한다

```
$ git rebase --onto master server client
```

이 명령은 client 브랜치를 Checkout 하고 server와 client의 공통조상 이후의 Patch를 만들어 master에 적용한다. 조금 복잡하긴 해도 꽤 쓸모 있다.

* 그림 3-32 다른 토픽 브랜치에서 갈라져 나온 토픽 브랜치를 Rebase하기

![rebase-6](https://git-scm.com/book/en/v2/book/03-git-branching/images/interesting-rebase-2.png)

이제 master 브랜치로 돌아가서 Fast-forward 시킬 수 있다.

```
$ git checkout master
$ git merge client
```

server 브랜치의 일이 다 끝나면 git rebaes [basebranch] [topicbranch] 라는 명령으로 Checkout 하지 않고 바로 server 브랜치를 master 브랜치로 rebase 할 수 있다. 이 명령은 토픽(server) 브랜치를 Checkout하고 베이스(master) 브랜치에 Rebase 한다.

```
$ git rebase master server
``` 

* 그림 3-33 master 브랜치를 client 브랜치 위치로 진행시키기

![rebase-7](https://git-scm.com/book/en/v2/book/03-git-branching/images/interesting-rebase-3.png)

* 그림 3-34 master 브랜치에 server 브랜치의 수정 사항을 적용

![rebase-8](https://git-scm.com/book/en/v2/book/03-git-branching/images/interesting-rebase-4.png)

그러고 나서 master 브랜치를 Fast-forward 시킨다.

```
$ git checkout master
$ git merge server
```

모든 것이 master 브랜치에 통합됐기 때문에 더 필요하지 않다면 client난 server 브랜치는 삭제해도 된다. 브랜치를 삭제해도 커밋 히스토리는 다음과 같이 여전히 남아 있다.

![rebase-9](https://git-scm.com/book/en/v2/book/03-git-branching/images/interesting-rebase-5.png)

```
$ git branch -d client
$ git branch -d server
```

<br/>
#### Rebase의 위험성

**이미 공개 저장소에 Push한 커밋을 Rebase하지 마라**

이 지침만 지키면 Rebase를 하는 데 문제 될 게 없다.


