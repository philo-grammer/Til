
## 사용자정보

Git은 Commit할 때마다 사용자정보(사용자이름과 이메일주소)를 사용한다. 한 번 커밋한 후에는 정보를 변경할 수 없다.

Local에 sourcetree가 설치 되어있는 경우, 환경설정 > General > Default user information에 체크가 되어있는 상태로 clone을 한다면, github 계정과 맞지 않을 수가 있다. 그럴 경우 아래와 같이 local git의 사용자정보를 github 계정과 동일하게 설정해주면 된다.

```
$git config --local user.name "philo-grammer"
$git config --local user.name great1106@gmail.com
```

### 추가

[--local]이 아닌 [--global] 옵션으로 설정하면, 딱 한 번만 설정하면 된다. 해당 시스템에서 해당 사용자가 사용할 때에는 이 정보를 사용한다. 만약 프로젝트마다 다른 이름과 이메일주소를 사용하고 싶으면 [--global] 옵션을 빼고 명령을 실행한다.


