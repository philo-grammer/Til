
## 2.4 되돌리기

#### 커밋 수정하기

너무 일찍 커밋했거나 어떤 파일을 빼먹었을 때 그리고 커밋 메시지를 잘못 적었을 때, 다시 커밋하고 싶으면 --amend 옵션을 사용한다.

```
$ git commit --amend
```

커밋을 했는데 Stage하는 것을 깜빡하고 빠트린 파일이 있으면 다음과 같이 고칠 수 있다.

```
$ git commit -m 'initial commit'
$ git add forgotten_file
$ git commit --amend
```

여기서 실행한 명령어 3개는 모두 하나의 커밋으로 기록된다. 두 번째 커밋은 첫번째 커밋을 덮어쓴다.

<br/>
#### 파일 상태를 Unstaged로 변경하기

예를 들어 파일을 두 개 수정하고서 따로따로 커밋하려고 했지만, 실수로 git add * 라고 실행해 버렸다.<br/>
두파일 모두 Staging Area에 들어 있다. 이제 둘 중 하나를 어떻게 꺼낼까?<br/>
우선 git status 명령으로 확인해보자.

```
$ git add .
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#        modified:  README.txt
#        modified:  benchmarks.rb
#
```

Changes to be committed 밑에 git reset HEAD <file>... 이라는 문장을 볼 수 있다. 이 명령으로 Unstage 상태로 변경할 수 있다. 

```
$ git reset HEAD benchmarks.rb
benchmarks.rb: locally modified
$ git status
# On branch master
# Changes to be committed:
#    (use "git reset HEAD <file>..." to unstage)
#
#         modified:  README.txt
#
# Changed but not updated:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard change in working
# directory)
#
#        modified:  benchmarks.rb
# 
```

이제 benchmarks.rb 파일이 Unstage 상태가 됐다.


<br/>
#### Modified 파일 되돌리기

어떻게 해야 benchmarks.rb 파일을 수정하고 나서 다시 되돌릴 수 있을까?<br/>
바로 위에 있는 예제에서 Unstaged 부분에서 알려주는대로 해보자.

```
$ git checkout -- benchmarks.rb
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#      modified:  README.txt
#
```

정상적으로 복원되었지만, 이 명령은 꽤 위험한 명령이다.<br/>
수정 이전의 파일로 덮어썼기 때문에 수정했던 내용은 전부 사라진다. 수정한 내용이 진짜 마음에 들지 않을 때에만 사용하자.


