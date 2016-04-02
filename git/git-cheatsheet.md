# Git 작업 흐름과 명령어

도움말 : git "명령어" --help
Git의 글로벌 설정은 $HOME/.gitconfig에 저장 (git config --help)

## 생성

##### 새 저장소 생성하기

cd ~/projects/myproject
git init
git add .

##### 기존 저장소 Clone 하기

git clone ~/existing/rego ~/new/repo
git clone git://host.org/project.git
git clone you@host.org/project.git

## 보기

##### 워킹 디렉터리의 파일 상태 보기

git status

##### 파일의 변경사항 보기

git diff

##### $ID1과 $ID2 사이의 변경사항 보기

git diff $id1 $id2

##### 커밋 히스토리 보기

git log

##### 특정 파일의 커밋 히스토리별 변경사항 보기

git log -p $file $dir/ec/tory/

##### 특정 파일을 누가 언제 고쳤는지 보기

git blame $file

##### $ID 커밋 보기

git show id

##### $ID 버전의 파일 보기

git show $id:$file

##### 로컬 브랜치들 보기

git branch
 
## Git Basic

master : default branch

origin : default remote branch

HEAD : current branch

HEAD^ : HEAD's parent

HEAD~3 : HEAD's parent's parent's parent

