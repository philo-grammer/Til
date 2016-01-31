## bash 프롬프트에 Git 상태 표시

#### bash_profile 파일에 아래 내용을 추가

$ vi ~/.bash_profile

* .bash_profile 을 찾지 못하면, .bash_login 을 찾고, 없다면 .profile 을 찾는다.<br/>
(난 .profile 에 추가했다.)

``` 
c_cyan=`tput setaf 6`
c_red=`tput setaf 1`
c_green=`tput setaf 5`
c_sgr0=`tput sgr0`
parse_git_branch () {
  if git rev-parse --git-dir >/dev/null 2>&1
  then
    gitver=$(git branch 2>/dev/null| sed -n '/^\*/s/^\* //p')
  else
    return 0
  fi
  echo -e "" $gitver
}
branch_color () {
  if git rev-parse --git-dir >/dev/null 2>&1
  then
    color=""
    if git diff --quiet 2>/dev/null >&2
    then
      color="${c_green}"
    else
      color=${c_red}
    fi
  else
    return 0
  fi
  echo -ne $color
}
export PS1='\w\[$(branch_color)\]$(parse_git_branch)\[${c_sgr0}\]\$ '
```
