
## Git Basic

1. $ git init 
2. $ git clone username@host:/remote/repository/path
3. $ git add <file name>
4. $ git commit -m "commit message"
5. $ git push origin master

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

