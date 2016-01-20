## 2.2 수정하고 저장소에 저장하기

워킹 디렉터리의 모든 파일은 크게 Tracked(관리대상임)와 Untracked(관리대상이아님)로 나눈다.
Tracked 파일은 이미 스냅샷에 포함돼 있던 파일이다. Tracked 파일은 또 Unmodified(수정하지 않음)와 Modified(수정함) 그리고 Staged(커밋하면 저장소에 기록되는) 상태 중 하나이다.

![File Status Lifecycle](http://git-scm.com/figures/18333fig0201-tn.png)

처음 저장소를 Clone하면 모든 파일은 Tracked이면서 Unmodified 상태가 된다. 
파일을 Checkout하고 나서 아무것도 수정하지 않았기 때문에 그렇다.

<br/>
#### 파일의 상태 확인하기

파일의 상태를 확인하려면 보통 git status 명령을 사용한다.

```
$ git status
# On branch mster
nothing to commit (working directory clean)
```

위의 내용은 파일을 하나도 수정하지 않았다는 것을 말해준다. 즉, Tracked와 Modified 상태의 파일이 없다.

프로젝트에 README 파일을 만들어보자. README 파일은 새로 만든 파일이이기 때문에 git status를 실행하면 'Untracked files'에 들어 있다.

```
$ vim README
$ git status
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#   README
nothing added to commit but untracked files present (use "git add" to track)
```

Git은 Untracked 파일을 아직 스냅샷(커밋)에 넣어지지 않은 파일이라고 본다. 파일이 Tracked 상태가 되기 전까지는 Git은 절대 그 파일을 커밋하지 않는다. 그래서 일하면서 생성하는 바이너리 파일 같은 것을 커밋하는 실수는 하지 않게 된다. README 파일을 추가해서 직접 Tracked 상태로 만들어보자.

<br/>
#### 파일을 새로 추적하기

git add 명령을 실행하면 Git은 README 파일을 추적한다.

```
$ git add README
```

git status 명령을 다시 실행하면 README 파일이 Tracked 상태이면서 Staged 상태라는 것을 확인할 수 있다.

```
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   new file:  README
#
```

'Changes to be committed'에 있는 파일은 Staged 상태라는 것을 의미한다. 커밋하면 git add를 실행한 시점의 파일이 저장소 히스토리에 저장된다.
앞에서 git init 명령을 실행했을 때 바로 git add (files) 명령을 실행했었다. 이 명령은 워킹 디렉터리에 있는 파일을 새로 추적하게 한다. 


<br/>
#### Modified 상태의 파일을 Stage하기

이미 Tracked 상태인 파일을 수정하는 법을 알아보자. benchmarks.rb라는 파일을 수정하고 나서 git status 명령을 다시 실행하면 결과는 다음과 같다.

```
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   new file:   README
# Changed but not updated:
#   (use "git add <file>..." to update what will be committed)
#
#   modified:  benchmarks.rb
#
```

위 benchmarks.rb 파일은 Tracked 상태이지만 아직 Staged 상태는 아니라는 것이다. *Staged 상태로 만들려면 git add 명령을 실행해야 한다.* git add는 파일을 새로 추적할 때도 사용하고 수정한 파일을 Staged 상태로 만들 때도 사용한다. git add를 실행하여 benchmarks.rb 파일을 Staged 상태로 만들고 git status 명령을 결과를 확인해보자.

```
$ git add benchmarks.rb
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   new file: README
#   modified: benchmarks.rb
#
```

위의 Staged 상태에서 benchmarks.rb 파일을 더 수정한다면, Git은 아직 커밋할 준비가 아닌 상태이다. 더 수정한 후 다시 git status 명령으로 상태를 확인해보자.

```
$ vim benchmarks.rb
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   new file: README
#   modified: benchmarks.rb
#
# Changed but not updated:
#   (use "git add <file>..." to update what will be committed)
#
#   modified: benchmarks.rb
#
```

benchmarks.rb가 Staged 상태이면서 동시에 Unstaged 상태로 나온다. git add 명령을 실행하면 Git은 파일을 바로 Staged 상태로 만든다. 지금 이 시점에서 커밋을 하면 git commit 명령을 실행하는 시점의 버전이 커밋되는 것이 아니라 마지막으로 git add 명령을 실행했을 때의 버전이 커밋된다. 즉, *git add 명령을 실행한 후에 또 파일을 수정하면 git add 명령을 다시 실행해서 최신 버전을 Staged 상태로 만들어야 한다.*

```
$ git add benchmarks.rb
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   new file: README
#   modified: benchmarks.rb
#
```

<br/>
#### 파일 무시하기

보통 로그 파일이나 빌드 시스템이 자동으로 생성한 파일을 무시하려면 .gitignore 파일을 만들고 그 안에 무시할 파일 패턴을 적는다.

```
$ cat .gitignore
*.[oa]		// 확장자가 .o나 .a인 파일을 Git이 무시
*~			// ~로 끝나는 모든 파일을 무시
```

.gitignore 파일은 보통 처음에 만들어 두는 것이 편리하다. 그래서 Git 저장소에 커밋하고 싶지 않은 파일을 실수로 커밋하는 일을 방지할 수 있다.
.gitignore 파일에 입력하는 패턴은 아래 규칙을 따른다.

* 아무것도 없는 줄이나, #로 시작하는 줄은 무시한다.
* 포준 Glob 패턴을 사용한다.
* 디렉터리는 슬래시(/)를 끝에 사용하는 것으로 표현한다.
* 느낌표(!)로 시작하는 패턴의 파일은 무시하지 않는다.

Glob 패턴은 정규표현식을 단순하게 만든 것으로 생각하면 되고 보통 셸에서 많이 사용한다. 애스터리스크(\*)는 문자가 하나도 없거나 하나 이상을 의미하고, [abc]는 중괄호 안에 있는 문자 중 하나를 의미한다(그런니까 이 경우에는 a, b, c). 물음표(?)는 문자 하나를 말하고, [0-9]처럼 중괄호 안의 캐릭터 사이에 하이픈(-)을 사용하면 그 캐릭터 사이에 있는 문자 하나를 말한다.
다음은 .gitignore 파일의 예이다.

```
# a comment - 이 줄은 무시한다.
*.a           # 확장자가 .a인 파일 무시
!lib.a        # 윗 줄에서 확장자가 .a인 파일은 무시하게 했지만 lib.a는 무시하지 않는다.
/TODO         # 루트 디렉터리에 있는 TODO 파일은 무시하고 subdir/TODO처럼
			  # 하위 디렉터리에 있는 파일은 무시하지 않는다.
build/        # build/ 디렉터리에 있는 모든 파일은 무시한다.
doc/*.txt     # 같은 파일은 무시하지 않는다.
```

<br/>
#### Staged와 Unstaged 상태의 변경 내용을 보기

어떤 내용이 변경됐는지 살펴보기엔 git status 명령이 아니라 git diff 명령을 사용해야 한다.

README 파일을 수정해서 Staged 상태로 만들고 benchmarks.rb 파일은 그냥 수정만 해둔다. 이 상태에서 git status 명령을 실행하면 다음과 같은 메시지를 볼 수 있다.

```
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#   new file: README
#
# Changed but not updated:
#   (use "git add <file>..." to update what will be committed)
#
#   modified: benchmarks.rb
#
```

git diff 명령을 실행하면 수정했지만 아직 staged 상태가 아닌 파일으 ㄹ비교해 볼 수 있다.

```
$ git diff
diff --git a/benchmarks.rb b/benchmarks.rb
index 3cb747f..da65585 100644
--- a/benchmarks.rb
--- b/benchmarks.rb
@@ -36,6 +36,10 @@ def main
           @commit.parents[0].parents[0].parents[0]
         end

+        run_cod(x, 'commits 1') do
+          git.commits.size
+        end
+
         run_code(x, 'commits 2') do
           log = git.commits('master', 15)
           log.size
```

이 명령은 워킹 디렉터리에 있는 것과 Staging Area에 있는 것을 비교한다. 그래서 아직 수정하고 아직 Stage하지 않은 것을 보여준다.

꼭 잊지 말아야 할 것이 있는데 git diff 명령은 마지막으로 커밋한 후에 수정한 것을 보여주지 않는다. git diff는 Unstaged 상태인 것들만 보여준다.

benchmarks.rb 파일을 Stage한 후에 다시 수정해도 git diff 명령을 사용할 수 있다. 이때는 Staged 상태인 것과 Unstaged 상태인 것을 비교한다.

```
$ git add benchmarks.rb
$ echo '# test line' >> benchmarks.rb
$ git status
#
# Changes to be committed:
#
#   modified: benchmarks.rb
#
# Changed but not updated:
#
#   modified: benchmarks.rb
#
```

git diff 명령으로 Unstaged 상태인 변경 부분을 확인해 볼 수 있다.

```
$ git diff
diff --git a/benchmarks.rb b/benchmarks.rb
index 445e28..86b2f7c 100644
--- a/benchmarks.rb
+++ b/benchmarks.rb
@@ -127,3 +127,4 @@ end
 main()

 ##pp Grit::GitRuby.cache_client.stats
+# test line
```

Staged 상태인 파일은 git diff --cached 옵션으로 확인한다.

```
$ git diff --cached
diff --git a/benchmarks.r b/benchmarks.rb
index 3cb747f..e445e28 100644
--- a/benchmarks.rb
+++ b/benchmarks.rb
@@ -36,6 +36,10 @@ def main
          @commit.parents[0].parents[0].parents[0]
        end

+        run_code(x, 'commits 1') do
+          git.commits.size
+        end
+
        run_code(x, 'commits 2') do
          log = git.commits('master', 15)
          log.size
```

<br/>
#### 변경사항 커밋하기

Unstaged 상태의 파일은 커밋되지 않는다는 것을 기억해야 한다.<br/>
Git은 생성하거나 수정하고 나서 git add 명령으로 추가하지 않은 파일은 커밋하지 않는다. 그 파일은 여전히 Modified 상태로 남아 있다.

커밋하기 전에 git status 명령으로 모든 것이 Staged 상태인지 확인할 수 있다.<br/>
그리고 git commit을 실행하여 커밋한다.

```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file: README
#       modified: benchmarks.rb
~
~
~
".git/COMMIT_EDITING" 10L, 283C
```

자동으로 생성되는 커밋 메시지의 첫 줄은 비어 있고 둘째 줄부터 git status 명령의 결과가 채워진다.<br/>
git commit에 -v 옵션을 추가하면 편집기에 diff 메시지도 추가된다.

메시지를 인라인으로 첨부할 수도 있다. 

```
$ git commit -m "Story 182: Fix benchmarks for speed"
[master]: created 463dc4f: "Fix benchmarks for speed"
2 files changed, 3 insertions(+), 0 deletions(-)
create mode 100644 README
```

* Git은 Staging Area에 속한 스냅샷을 커밋한다는 것을 기억해야 한다.


#### Staging Area 생략하기

git commit 명령을 실행할 때 -a 옵션을 추가하면 Git은 Tracked 상태의 파일을 자동으로 Staging Area에 넣는다.<br/>
그래서 git add 명령을 실행하는 수고를 덜 수 있다.

```
$ git status
# On branch master
# 
# Changed but not update:
#
#   modified:  benchmarks.rb
#
$ git commit -a -m 'added new benchmarks'
[master 83e38c7] added new benchmarks
 1 files changed, 5 insertions(+), 0 deletions(-)
```

이 예제에서는 커밋하기 전에 git add 명령으로 benchmarks.rb 파일을 추가하지 않았다는 점을 눈여겨보자.


