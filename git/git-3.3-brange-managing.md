## 3.3 브랜치 관리

git branch 명령을 아무런 옵션 없이 실행

```
$ git branch
  iss53
* master
  testing
```

git branch -v : 브랜치마다 마지막 커밋 메시지도 함께 출력

```
$ git branch -v
  iss53   93b412c fix javascript issue
* master  7a98805 Merge branch 'iss53'
  testing 782fd34 add scott to the author list in the readmes
```

git branch --merged : 이미 Merge한 브랜치 목록 확인

```
$ git branch --merged
  iss53
* master
```

\* 기호가 붙어 있지 않은 브랜치는 git branch -d 명령으로 삭제해도 되는 브랜>    치이다. 이미 다른 브랜치와 Merge 했기 때문에 삭제해도 정보를 잃지 않는다. 

git branch --no-merged : 현재 Checkout한 브랜치에 Merge 하지 않은 브랜치를 확인

```
$ git branch --no-merged
  testing
```

아직 Merge하지 않은 커밋을 담고 있기 때문에 git branch -d 명령으로 삭제되지 않는다.

```
$ git branch -d testing
error: The branch 'testing' is not fully merged.
If you are sure you want to delete it, run 'git branch -D testing'.
```

Merge 하지 않은 브랜치를 강제로 삭제하려면 -D 옵션으로 삭제한다.
