
## 2.4 되돌리기

### 커밋 수정하기

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


