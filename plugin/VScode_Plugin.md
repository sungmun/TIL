# VScode Plugin

현재 내가 사용하고 있는 vscode의 플러그인 및 유용하다고 생각이 되는 플러그인들을 소개하고 간단한 사용법을 소개할것이다. 

## Project Manager
|     | 설명 |
--- |---
이름  | Project Manager 
Id    | alefragnani.project-manager
설명  | Easily switch between projects
버전  | 10.6.0
게시자| Alessandro Fragnani
링크  | https://marketplace.visualstudio.com/items?itemName=alefragnani.project-manager

이 플러그인은 여러개의 프로젝트를 유지할시 유용한 플러그인으로, 프로젝트의 전환이 잦은 사람들에게 유용한 프로젝트이다. 크게 3개의 명령어를 사용하므로 3개에 대해서만 설명하겠다.

 - Save Project : 현재 프로젝트를 저장을 하는 명령어이다.
 - List Project to Open : 저장한 프로젝트를 불러오는 명령어이다.
 - Edit Projects : Projects.json파일을 여는 명령어로, Project Manager에 저장이된 Project의 설정들을 볼 수 있다.
 
## Korean Language Pack for Visual Studio Code

|     | 설명 |
--- |---
이름| Korean Language Pack for Visual Studio Code
Id| ms-ceintl.vscode-language-pack-ko
설명| Language pack extension for Korean
버전| 1.37.3
게시자| Microsoft
링크| https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-ko

이 플러그인은 VScode를 처음 설치시 기본 설정이 영문을 한국어로 변경을 해주는 플러그인으로, 설치후 재시작을 하면 영문으로 되있던 부분이 한글로 번역이되어 준다.

## REST Client
|     | 설명 |
--- | ---
이름| REST Client
Id| humao.rest-client
설명| REST Client for Visual Studio Code
버전| 0.22.0
게시자| Huachao Mao
링크| https://marketplace.visualstudio.com/items?itemName=humao.rest-client

이 플러그인은 웹개발시 유용한 플러그인으로, 통 합테스트시 사용을 하면 편리하며, *.http파일을 만들면 이 파일을 기준으로 http요청을 보내는 플러그인이다. 형식은 다음과 같다
```
get https://localhost/version
Content-Type: application/x-www-form-urlencoded

data
```
위 와 같이 사용을 하면 되며, 첫번째 값으로는 요청(*Post*,*Get*, *Put*,*Delete*)을,  두번째 값으로는 URL을 정해준다.
그 다음에는 header값을 정해주는데, json형식으로 data를 보내지 않으면, content-type에 데이터를 추가를 해줘야 한다.
3번째 값으로는 data값을 넣어준다. 이때, data값은 기본은 json형식이며, header값과 1칸의 개행을 넣어주어야 한다.
여기까지가 가장 기본적인 사용법이며 좀더 자세한 설명은 [Rest Client Plugin](/plugin/RestClientPlugin.md)을 보면 된다.

## Prettier - Code formatter
|     | 설명 |
--- | ---
이름| Prettier - Code formatter
Id| esbenp.prettier-vscode
설명| VS Code plugin for prettier/prettier
버전| 1.9.0
게시자| Esben Petersen
링크| https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode

이 플러그인은 코드포맷터 플러그인으로, 코드 작성시 코드의 성능향상보다는 **코드 Style의 규격**을 맞추는데 도움을 주는 플러그인이다. 
이 코드의 규격은 설정파일에 의해 정해지는데, 설정파일은 **Json, Js, YAML, TOML**방식이 있으나, Json형식으로 설명 하겠다,
우선 설정 파일은 프로젝트의 루트 디렉토리에 있어야하며, 파일명은 **.prettierrc**이어야한다.
```json
{
  "trailingComma": "es5",
  "tabWidth": 4,
  "semi": false,
  "singleQuote": true
}
```
### option
 - printWidth (기본값 : 80): 이 줄 한도 내에서 코드 맞추기
 - tabWidth (기본값 : 2): 탭당 사용해야하는 space수
 - singleQuote (기본값 : false): 참이면 큰 따옴표 대신 작은 따옴표를 사용합니다
 - trailingComma (기본값 : 'none'): 가능한 경우 후행 쉼표 인쇄를 제어합니다.
    "none" : 후행 쉼표 없음
    "es5" : ES5에서 유효한 후행 쉼표 (객체, 배열 등)
    "all" : 가능하면 후행 쉼표 (함수 인수)
 - bracketSpacing (기본값 : true): 객체 리터럴 내부의 공백 인쇄를 제어합니다
 - jsxBracketSameLine (기본값 : false): true 인 경우 >여러 줄 jsx 요소를 다음 줄에 혼자 두지 않고 마지막 줄 끝에 놓습니다.
 - parser (기본값 : 'babylon')-JavaScript 만: 사용할 파서. 유효한 옵션은 'flow'및 'babylon'입니다.
 - semi (기본값 : true): 모든 줄의 끝에 세미콜론을 추가할지 (세미 : true) 또는 ASI 실패를 일으킬 수있는 줄의 시작에만 세미콜론을 추가할지 (세미 : false)
 - useTabs (기본값 : false): 참이면 탭이있는 줄을 들여 쓰기
 - proseWrap (기본값 : 'preserve'): (마크 다운)은 여러 줄에 걸쳐 산문을 랩핑합니다.
 - arrowParens (기본값 : 'avoid'): 단독 화살표 함수 매개 변수 주위에 괄호 포함
 - jsxSingleQuote (기본값 : false): JSX에서는 큰 따옴표 대신 작은 따옴표를 사용하십시오.
 - htmlWhitespaceSensitivity (기본값 : 'css'): HTML 파일의 전역 공백 감도를 지정하십시오. 
 - endOfLine (기본값 : 'auto'): 더 예쁘게 사용할 줄 끝을 지정하십시오. 
 - quoteProps (기본값 : '필요에 따라'): 객체의 속성이 인용 될 때 변경합니다.

더 자세한 설정은 [여기](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)에서 확인하세요

