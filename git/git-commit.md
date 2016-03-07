# commit을 변경하는 조작

### git resert : 과거 상태로 복원

### git commit --amend : commit 메시지 수정

직전에 작성했던 commit 메시지를 수정하고 싶을 때는 git commit --amend 명령어를 사용합니다.

### git rebase -i : 변경 내역 조작

ex) $ git rebase -i HEAD~2
현재 브랜치의 HEAD(최신 commit)를 포함한 두 개의 변경 내역과 관련된 내용이 에디터에 표시됩니다.

