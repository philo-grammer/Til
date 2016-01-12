## 2.1 Git 저장소 만들기

Git 저장소를 만드는 방법은 두 가지다.

1. 기존 프로젝트를 Git 저장소로 만드는 방법

2. 다른 서버에 있는 저장소를 Clone하는 방법이 있다.

#### 기존 디렉터리를 Git 저장소로 만들기

기존 프로젝트를 Git으로 관리하고 싶을 때, 프로젝트의 디렉터리로 이동해서 다음과 같은 명령을 실행한다.

```
$ git init
```

이 명령은 .git이라는 하위 디렉터리를 만든다.
.git 디렉터리에는 저장소에 필요한 뼈대 파일(Skeleton)이 들어 있다.
이 명령만으로는 아직 프로젝트의 어떤 파일도 관리하지 않는다.

Git이 파일을 관리하게 하려면 다음과 같이 저장소에 파일을 추가하고 커밋해야 한다.

```
$ git add *.c
$ git add README
$ git commit -m 'initial project version'
```


#### 기존 저장소를 Clone 하기

다른 프로젝트에 참여하거나(Contribute) Git  저장소를 복사하고 싶을 때 git clone 명령을 사용한다.
Git이 서브버전과 다른 가장 큰 차이점은 서버에 있는 데이터를 모두 복사한다는 것이다. git clone을 실행하면 프로젝트 히스토리를 전부 받아온다.

git clone [url] 명령으로 저장소를 Clone한다. Ruby용 Git 라이브러리인 Grit을 Clone하려면 아래와 같이 실행한다.

```
$ git clone git://github.com/schacon/grit.git
```
이 명령은 "grit"이라는 디렉터리를 만들고 그 안에 .git 디렉터리를 만든다.
그리고 저장소의 데이터를 모두 가져와서 자동을 가장 최신 버전을 Checkout해 놓는다.

아래와 같은 명령을 사용하여 저장소를 Clone하면 "grit"이 아니라 다른 디렉터리 이름(mygrit)으로 Clone할 수 있다.

```
$ git clone git://github.com/schacon/grit.git mygrit
```
