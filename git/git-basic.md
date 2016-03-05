
## Git Basic

1. $ git init 
2. $ git clone username@host:/remote/repository/path
3. $ git add <file name>
4. $ git commit -m "commit message"
5. $ git push origin master

#### git init : 리포지토리 초기화

Git에서는 `git init` 명령어로 초기화를 수행합니다.
.git 이라는 폴더에 현재 폴더와 관련된 리포지토리 관리 정보가 저장됩니다.
Git에는 이 디렉토리 이하의 내요을 해당 리포지토리와 관련된 'working tree(워킹 트리)'라고 부릅니다.

#### git status : 리포지토리 상태 확인

`git status` 명령어는 Git 리포지토리의 상태를 표시하는 명령어 입니다. 자주 사용하는 명령어이므로 반드시 기억하기 바랍니다.

commit이란, working tree에 있는 모든 파일의 특정 시점 상태를 기록한 것입니다.

#### git add : 스테이지 영역에 파일 추가

파일을 Git 리포지토리에서 관리하도록 하려면 `git add` 명령어로 스테이지 영역이라 불리는 장소에 파일을 등록해야 합니다. 스테이지 영역이란 commit하기 전의 임시 영역입니다.

#### git commit : 리포지토리 변경 내용을 기록

`git commit` 명령어는 스테이지 영역에 기록된 시점의 파일들을 실제 리포지토리의 변경 내역에 반영하는 것입니다.

#### git log : commit 확인

`git log` 명령어는 리포지토리에 commit 된 로그를 확인할 수 있는 명령어입니다.

#### git diff : 변경 내역 확인

`git diff` 명령어는 working tree, 스테이지 영역, 최신 commit 사이의 변경을 확인할 때 사용합니다.

* working tree와 스테이지 영역의 차이를 확인하는 방법
	* git diff 명령어를 실행하면 현재 working tree와 스테이지 영역 사이의 차이를 확인할 수 있습니다.

* working tree에서 최근에 변경된 부분을 확인하는 방법
	* git commit 명령어를 실행하기 전에 git diff  HEAD 명령어를 실행하는 버릇을 길러 둡시다. 이렇게 하면 현재 commit과 이전 commit의 차이를 한눈에 확인할 수 있습니다. 현재 명령어에입력한 HEAD는 현재 작업하고 있는 브랜치의 최신 commit을 참조하는 포인터입니다.

<br/>
## Git Branch

* $ git checkout -b feature_x
* $ git checkout master
* $ git branch -d feature_x
* $ git push origin <branch name>

<br/>
## Git Merge

* $ git pull (= fetch + merge)

<br/>
## Git Reset (삭제한 파일 복구하기)

* $ git reset --hard HEAD

<br/>
## Git working tree 전체 원복

* git checkout -f : 변경된 파일들을 HEAD로 모두 원복 <br/>(아직 커밋하지 않은 워킹트리와 index의 수정사항 모두 사라짐. 신규추가 파일 제외)

