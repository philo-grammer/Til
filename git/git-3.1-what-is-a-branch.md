## 3.1 브랜치란 무엇인가

파일이 3개 있는 디렉토리가 하나 있고 이 파일을 Staging Area에 저장하고 커밋하는 예제를 살펴 보자. 파일을 Stage 하면 Git 저장소에 파일을 저장하고(Git은 이것을 Blob이라고 부른다) Staging Area에 해당 파일의 체크섬을 저장한다(Chapter 1 에서 살펴본 SHA-1을 사용한다).

```
$ git add README test.rb LICENSE
$ git commit -m 'initial commit of my project'
```

git commit으로 커밋하면 먼저 루트 디렉토리와 각 하위 디렉토리의 트리 개체를 체크섬과 함께 저장소에 저장한다. 그다음에 커밋 개체를 만들고 메타데이터와 루트 디렉토리 트리 개체를 가리키는 포인터 정보를 커밋 개체에 넣어 저장한다. 그래서 필요하면 언제든지 스냅샷을 다시 만들 수 있다.

이 작업을 마치고 나면 Git 저장소에는 다섯 개의 데이터 개체가 생긴다. 각 파일에 대한 Blob 세 개, 파일과 디렉토리 구조가 들어 있는 트리 개체 하나, 메타데이터와 루트 트리를 가리키는 포인터가 담긴 커밋 개체 하나이다.

![커밋과트리데이터](https://git-scm.com/book/en/v2/book/03-git-branching/images/commit-and-tree.png)

다시 파일을 수정하고 커밋하면 이전 커밋이 무엇인지도 저장한다.

![커밋과 이전 커밋](https://git-scm.com/book/en/v2/book/03-git-branching/images/commits-and-parents.png)

Git의 브랜치는 커밋 사이를 가볍게 이동할 수 있는 어떤 포인터 같은 것이다. 기본적으로 Git은 master 브랜치를 만든다. 최초로 커밋하면 Git은 master라는 이름의 브랜치를 만든다. 커밋을 만들 때 마다 브랜치가 자동으로 가장 마지막 커밋을 가리키게 한다.

* Git 버전 관리 시스템에서 “master” 브랜치는 특별하지 않다. 다른 브랜치와 다른 것이 없다. 다만 모든 저장소에서 “master” 브랜치가 존재하는 이유는 git init 명령으로 초기화할 때 자동으로 만들어진 이 브랜치를 애써 다른 이름으로 변경하지 않기 때문이다.

![브랜치와 커밋 히스토리](https://git-scm.com/book/en/v2/book/03-git-branching/images/branch-and-history.png)

<br/>
#### 새 브랜치 생성하기

```
$ git branch testing
```

![한커밋히스토리](https://git-scm.com/book/en/v2/book/03-git-branching/images/head-to-master.png)

git log 명령에 --decorate 옵션을 사용하면 쉽게 브랜치가 어떤 커밋을 가리키는지도 확인할 수 있다.

```
$ git log --oneline --decorate
f30ab (HEAD, master, testing) add feature #32 - ability to add new
34ac2 fixed bug #1328 - stack overflow under certain conditions
98ca9 initial commit of my project
```

<br/>
#### 브랜치 이동하기

```
$ git checkout testing
```

![HEAD](https://git-scm.com/book/en/v2/book/03-git-branching/images/head-to-testing.png)

이제부터가 핵심!
```
$ vim test.rb
$ git commit -a -m 'made a change'
```

![commmit](https://git-scm.com/book/en/v2/book/03-git-branching/images/advance-testing.png)

이 부분이 흥미롭다. 새로 커밋해서 testing 브랜치는 앞으로 이동했다. 하지만, master 브랜치는 여전히 이전 커밋을 가리킨다. master 브랜치로 되돌아가보자.

```
$ git checkout master
```

![checkout](https://git-scm.com/book/en/v2/book/03-git-branching/images/checkout-master.png)

일을 수정하고 다시 커밋을 해보자.

```
$ vim test.rb
$ git commit -a -m 'made other changes'
```

![recommit](https://git-scm.com/book/en/v2/book/03-git-branching/images/advance-master.png)

git log 명령으로 쉽게 확인할 수 있다. 현재 브랜치가 가리키고 있는 히스토리가 무엇이고 어떻게 갈라져 나왔는지 보여준다. git log --oneline --decorate --graph --all이라고 실행하면 히스토리를 출력한다.

```
$ git log --oneline --decorate --graph --all
* c2b9e (HEAD, master) made other changes
| * 87ab2 (testing) made a change
|/
* f30ab add feature #32 - ability to add new formats to the
* 34ac2 fixed bug #1328 - stack overflow under certain conditions
* 98ca9 initial commit of my project
```

브랜치를 만들어야 하면 프로젝트를 통째로 복사해야 하는 다른 버전 관리 도구와 Git의 차이는 극명하다. 통째로 복사하는 작업은 프로젝트 크기에 따라 다르겠지만 수십 초에서 수십 분까지 걸린다. 그에 비해 Git은 순식간이다. 게다가 커밋을 할 때마다 이전 커밋의 정보를 저장하기 때문에 Merge 할 때 어디서부터(Merge Base) 합쳐야 하는지 안다. 이런 특징은 개발자들이 수시로 브랜치를 만들어 사용하게 한다.
