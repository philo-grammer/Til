## Git Rebase 방법 (Default)

1. git checkout master : 내 branch에서 master로 이동
2. git pull
3. git checkout [branch name] : 내 branch로 이동
4. git rebase master : master로 rebase
5. git push origin [branch name] -f 
	* 서버(origin)의 내 branch에 강제 push 

## Git Rebase 방법 : 여러 개의 커밋 합쳐서 Rebase
1. git rebase -i HEAD~[합칠커밋개수] - 예:HEAD~6
2. git commit --amend
3. (수정 파일에서) 가장 위에 있는 pick을 제외한 나머지 pick을 모두 s 로 변경
	* 하나로 합칠 commit message 도 수정 가능
4. git push origin [branch name] -f

