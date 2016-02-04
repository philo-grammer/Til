## 3.1 브랜치란 무엇인가?

### 브랜치의 기초

먼저 커밋을 몇 번 했다고 가정하면 다음과 같다.

![현재커밋히스토리](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-branching-1.png)

<br/>
다음과 명령으로 iss53 브랜치를 만든다.

```
$ git branch iss53
```

branch를 만들면서 Checkout까지 동시에 하려면 git checkout 명령에 -b 옵션을 준다.

```
$ git checkout -b iss53
Switched to a new branch 'iss53'
```
위 명령은 아래 명령을 줄여놓은 것이다.

```
$ git branch iss53
$ git checkout iss53
```

위 명령의 결과는 다음과 같다.

![branch](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-branching-2.png)

<br/>
iss53 브랜치를 Checkout했기 때문에(즉, HEAD는 iss53 브랜치를 가리킨다) 뭔가 일을 하고 커밋하면 iss53 브랜치가 앞으로 진행한다.

```
$ vim index.html
$ git commit -a -m 'added a new footer [issue 53]'
```

![commit](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-branching-3.png)

<br/>
아직 커밋하지 않은 파일이 Checkout할 브랜치와 충돌 나면 브랜치를 변경할 수 없다. 브랜치를 변경할 때에는 워킹 디렉토리를 정리하는 것이 좋다. 이런 문제를 다루는 방법은(주로, Stash이나 커밋 Amend에 대해) 나중에 다룰 것이다. 지금은 작업하던 것을 모두 커밋하고 master 브랜치로 옮긴다.

```
$ git checkout master
Switched to branch 'master'
```

Git은 자동으로 워킹 디렉토리에 파일들을 추가하고, 지우고, 수정해서 Checkout한 브랜치의 스냅샷으로 되돌려 놓는다는 것을 기억해야 한다.

hotfix라는 브랜치를 만들고 새로운 이슈를 해결할 때까지 사용한다.

```
$ git checkout -b hotfix
Switched to a new branch 'hotfix'
$ vim index.html
$ git commit -a -m 'fixed the broken email address'
[hotfix 3a0874c] fixed the broken email address
 1 files changed, 1 deletion(-)
 ```
 
 ![newBranchCommit](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-branching-4.png)
 
 <br/>
 운영 환경에 적용하려면 문제를 제대로 고쳤는지 테스트하고 master 브랜치에 합쳐야 한다. git merge 명령으로 다음과 같이 한다.
 
 ```
$ git checkout master
$ git merge hotfix
Updating f42c576..3a0874c
Fast-forward
 README | 1 -
 1 file changed, 1 deletion(-)
 ```
 
Merge 메시지에서 'Fast-forward'가 보이는가? Merge할 브랜치가 가리키고 있던 커밋이 현 브랜치가 가리키는 것보다 '앞으로 진행한' 커밋이기 때문에 master 브랜치 포인터는 최신 커밋으로 이동한다. 이런 Merge 방식을 'Fast forward'라고 부른다. 다시 말해서 A 브랜치에서 다른 B 브랜치를 Merge할 때 B가 A 이후의 커밋을 가리키고 있으면 그저 A가 B의 커밋을 가리키게 할 뿐이다.

이제 hotfix는 master 브랜치에 포함됐고 운영환경에 적용할 수 있다.

![merge](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-branching-5.png)

<br/>
문제를 급히 해결하고 master 브랜치에 적용하고 나면 다시 일하던 브랜치로 돌아가야 한다. 하지만, 그전에 필요없는 hotfix 브랜치를 삭제한다. git branch 명령에 -d 옵션을 주고 브랜치를 삭제한다.

```
$ git branch -d hotfix
Deleted branch hotfix (was 3a0874c).
```

자 이제 이슈 53번을 처리하던 환경으로 되돌아가서 하던 일을 계속 하자.

```
$ git checkout iss53
Switched to branch 'iss53'
$ vim index.html
$ git commit -a -m 'finished the new footer [issue 53]'
[iss53 ad82d7a] finished the new footer [issue 53]
 1 file changed, 1 insertion(+)
```

![checkout](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-branching-6.png)

위에서 작업한 hotfix가 iss53 브랜치에 영향을 끼치지 않는다는 점을 이해하는 것이 중요하다. git merge master 명령으로 master 브랜치를 iss53 브랜치에 Merge하면 iss53 브랜치에 hotfix가 적용된다. 아니면 iss53 브랜치가 master에 Merge할 수 있는 수준이 될 때까지 기다렸다가 Merge하면 hotfix와 iss53가 합쳐진다.


<br/>
#### Merge 의 기초

```
$ git checkout master
Switched to branch 'master'
$ git merge iss53
Merge made by the 'recursive' strategy.
README |    1 +
1 file changed, 1 insertion(+)
```

hotfix를 Merge 했을 때와 메시지가 다르다. 현재 브랜치가 가리키는 커밋이 Merge 할 브랜치의 조상이 아니므로 Git은 Fast-forward로 Merge 하지 않는다. 이 경우에는 Git은 각 브랜치가 가리키는 커밋 두 개와 공통 조상 하나를 사용하여 3-way Merge를 한다.

![basic-merging-1](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-merging-1.png)

단순히 브랜치 포인터를 최신 커밋으로 옮기는 게 아니라 3-way Merge 의 결과를 별도의 커밋으로 만들고 나서 해당 브랜치가 그 커밋을 가리키도록 이동시킨다. 그래서 이런 커밋은 부모가 여러 개고 Merge 커밋이라고 부른다.

![basic-merging-2](https://git-scm.com/book/en/v2/book/03-git-branching/images/basic-merging-2.png)

iss53 브랜치를 master에 Merge 하고 나면 더는 iss53 브랜치가 필요 없다. 다음 명령으로 브랜치를 삭제하고 이슈의 상태를 처리 완료로 표시한다.

```
$ git branch -d iss53
```

<br/>
#### 충돌의 기초

가끔씩 3-way Merge가 실패할 때도 있다. Merge 하는 두 브랜치에서 같은 파일의 한 부분을 동시에 수정하고 Merge 하면 Git은 해당 부분을 Merge 하지 못한다. 

```
$ git merge iss53
Auto-merging index.html
CONFLICT (content): Merge conflict in index.html
Automatic merge failed; fix conflicts and then commit the result.
```

Git은 자동으로 Merge 하지 못해서 새 커밋이 생기지 않는다. 변경사항의 충돌을 개발자가 해결하지 않는 한 Merge 과정을 진행할 수 없다. Merge 충돌이 일어났을 때 Git이 어떤 파일을 Merge 할 수 없었는지 살펴보려면 git status 명령을 이용한다.

```
[master*]$ git status
index.html: needs merge
# On branch master
# Changed but not updated:
#   (use 'git add <file>...' to update what will be committed)
#   (use 'git checkout -- <file>...' to discard changes in working
# directory)
#
#   unmerged:   index.html
#
```

충돌이 일어난 파일은 unmerged 상태로 표시된다. Git은 충돌이 난 부분을 표준 형식에 따라 표시해준다. 그러면 개발자는 해당 부분을 수동으로 해결한다. 충돌 난 부분은 아래와 같이 표시된다.

```
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer">
 please contact us at support@github.com
</div>
>>>>>>> iss53:index.html
```

======= 위쪽의 내용은 HEAD 버전(merge 명령을 실행할 때 작업하던 master 브랜치)의 내용이고 아래쪽은 iss53 브랜치의 내용이다. 충돌을 해결하려면 위쪽이나 아래쪽 내용 중에서 고르거나 새로 작성하여 Merge 한다.

충돌을 해결하고 나서 해당 파일이 Staging Area에 저장됐는지 확인했으면 git commit 명령으로 Merge 한 것을 커밋한다. 충돌을 해결하고 Merge 할 때에는 커밋 메시지가 아래와 같다.

```
Merge branch 'iss53'

Conflicts:
    index.html
#
# It looks like you may be committing a merge.
# If this is not correct, please remove the file
#	.git/MERGE_HEAD
# and try again.
#
```
어떻게 충돌을 해결했고 좀 더 확인해야 하는 부분은 무엇이고 왜 그렇게 해결했는지에 대해서 자세하게 기록한다. 자세한 기록은 나중에 이 Merge 커밋을 이해하는데 도움을 준다.


