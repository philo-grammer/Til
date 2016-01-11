
## Git 최소 설정

Git을 설치하고 나면 Git의 사용 환경을 적절하게 설정해 주어야 한다. 한 번만 설정하면 된다. 설정한 내용은 Git을 업그레이드해도 유지된다. 언제든지 다시 바꿀 수 있는 명령어가 있다.

'git config'라는 도구로 설정 내용을 확인하고 변경할 수 있다. Git은 이 설정에 따라 동작한다. 이때 사용하는 설정 파일은 세 가지나 된다.

- /etc/gitconfig 파일 : 시스템의 모든 사용자와 모든 저장소에 적용되는 설정이다. git config --system 옵션으로 이 파일을 읽고 쓸 수 있다.
- ~/.gitconfig 파일 : 특정 사용자에게만 적용되는 설정이다. git config --global 옵션으로 이 파일을 읽고 쓸 수 있다.
- .git/config : 이 파일을 Git 디렉터리에 있고 특정 저장소(혹은 현재 작업 중인 프로젝트)에만 적용된다. 각 설정은 역순으로 우선시 된다. 그래서 .git/config가 /etc/gitconfig보다 우선한다.

윈도용 Git은 $HOME 디렉터리(C:\Documents and Settings\$USER)에 있는 .gitconfig 파일을 찾는다. msysGit에도 /etc/gitconfig 파일이 있다. 경로는 MSys 루트에 따른 상대 경로다. 인스톨러로 msysGit을 설치할 때 설치 경로를 선택할 수 있다.

### 사용자정보

Git을 설치하고 나서 가장 먼저 해야 한는 것은 사용자 이름과 이메일 주소를 설정하는 것이다. Git은 Commit할 때마다 이 정보를 사용한다. 한 번 커밋한 후에는 정보를 변경할 수 없다.

```
$ git config --global user.name "philo-grammer"
$ git config --global user.name great1106@gmail.com
```

다시 말하자면 --global 옵션으로 설정한 것은 딱 한 번만 하면 된다. 해당 시스템에서 해당 사용자가 사용할 때에는 이 정보를 사용한다. 만약 프로젝트마다 다른 이름과 이메일주소를 사용하고 싶으면 --global 옵션을 빼고 명령을 실행한다. 

#### 추가
Local에 sourcetree가 설치 되어있는 경우, 환경설정 > General > Default user information에 체크가 되어있는 상태로 clone을 한다면, github 계정과 맞지 않을 수가 있다. 그럴 경우 해당 repository로 이동해서 위의 명령문 중 --global 옵션을 빼고 실행한다. 그러면 local git의 사용자정보가 github 계정과 동일하게 설정된다.

### 편집기

사용자 정보를 설정하고 나면 Git에서 사용할 텍스트 편집기를 고른다. 기본적으로 Git은 시스템의 기본 편집기를 사용하고, 보통 편집기는 Vi나 Vim이다. 하지만, Emacs 가튼 다른 텍스트 편집기를 사용할 수 있고 다음과 같이 실행하면 된다.

```
$ git config --global core.editor emacs
```

### Diff 도구

Merge 충돌을 해결하기 위해 사용하는 Diff 도구를 설정할 수 있다. vimdiff를 사용하고 싶으면 다음과 같이 실행한다.

```
$ git config --global merge.tool vimdiff
```

이렇게 kdiff3, tkdiff, meld, xxdif, emerge, vimdiff, gvimdiff, ecmerge, opendiff를 사용할 수 있다. 물론 다른 도구도 사용할 수 있다.

### 설정 확인

git config --list 명령을 실행하면 설정한 모든 것을 보여준다.

```
$ git config --list
user.name=philo-grammer
user.email=great1106@gmail.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
```

Git은 같은 키를 여러 파일(/etc/gitconfig와 ~/.gitconfig 같은)에서 읽기 때문에 같은 키가 여러개 있을 수도 있다. 이러면 Git은 나중 값을 사용한다.
git config {key} 명령으로 Git이 특정 Key에 대해 어떤 값을 사용하는지 확인할 수 있다.

```
$ git config user.name
philo-grammer
```


## 도움말

명령어에 대한 도움말이 필요할 때 도움말을 보는 방법은 세 가지다.명령어에 대한 도움말이 필요할 때 도움말을 보는 방법은 세 가지다.

```
$ git help <verb>
$ git <verb> --help
$ git man git-<verb>
```

예를 들어 다음과 같이 실행하면 config 명령에 대한 도움말을 볼 수 있다

```
$ git help config
```

