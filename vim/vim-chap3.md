#### 3장에서 살펴볼 기능

|살펴볼 기능 |명령어  |
|:-----------|:-------|
|옵션 설정   |:set ...|
|옵션 파일   |.vimrc (혹은 _vimc)|
|색상 테마   |:colo ...|
|도움말      |:help|
|검색어 확장 |CTRL-D|

## 3.1 Vim의 옵션

#### set 명령어 사용법

|명령어          |설명|
|:---------------|:---|
|:set            |현재 옵션 설정을 보여줍니다.|
|:set all        |모든 옵션 설정을 보여줍니다. (off 상태의 옵션까지 모두 출력)|
|:set [no]name   |name에 해당하는 옵션을 켜거나 끕니다. 앞에 no를 붙이면 off 상태가 됩니다.|
|:set name!      |name 옵션의 on, off 상태를 전환(toggle)합니다.|
|:set name=value |name에 해당하는 옵션에 value 값을 할당합니다.<br/>name만 지정하면 해당 옵션의 value 값을 보여줍니다.|

#### 편집에 관련된 기초 옵션들

|옵션 이름(괄호 안은 긴 이름) |설명 |
|:----------------------------|:----|
|nu (number)           |화면에 행 번호를 표시합니다.|
|ai (autoindent)       |자동 들여쓰기를 사용합니다.|
|cindent               |C 언어 스타일의 들여쓰기를 사용합니다.|
|ts=value (tabstop)    |탭 크기를 value로 지정합니다.|
|sw=value (shiftwidth) |블록 이동시 열의 너비입니다.|
|tw=value(textwidth)   |편집할 화면의 열 길이를 정합니다.(0이면 비활성화)|

<br/>
## 3.2 옵션과 색상 테마 저장하기(vim 설정 파일)

#### .vimrc 파일에 넣을 내용

```
" vim runtime configuration file
set ai cindent
set ts=4 sw=4
"
```

설정 파일의 내용은 Vim에서 강제로 불러오지 않는 한 시작할 때 한 번만 읽힙니다. 그러므로 .vimrc 파일을 변경한 후 적용하려면 Vim을 종료하고 다시 시작해야 합니다.

#### syntax 명령어

|명령어         |설명|
|:--------------|:---|
|:syntax enable |문법 표시를 사용합니다.|
|:syntax clear  |문법 표시를 사용하지 않습니다.|

#### colorscheme 명령어

|명령어               |설명|
|:--------------------|:---|
|:colorcheme (scheme) |(scheme) 색상을 사용합니다.|

#### .vimrc 파일에 syntax와 colorscheme(colo) 추가

```
" vim runtime configuration file
set ai cindent
set ts=4 sw=4
syntax enable
colo shine
"
```


