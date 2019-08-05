# Express Project 구조

express 프로젝트를 할 경우, 내가 사용하는 프로젝트 구조로 사용자별로 천차만별이니 참고만 하기를 바란다. ( /으로 시작하는 부분은 디렉토리를 의미한다.)

## 구조

- /
  - /src
    - /model
      - /domains ...
        - domain.model
    - /router
      - /domain ...
        - domain.controller
        - index
      - index
    - /service
      - /domain ...
        - domain.service
    - /middleware
      - middleware ...
      - index
    - /util
      - util ...
      - index
    - index
    - express(option)
  - /config
    - config.json
  - settingfile

### /src

프로젝트의 source파일이 있는 디렉토리로 빌드를 하지 않은 상태의 코드가 있는 코드들이다. 이 디렉토리 내부에 있는 파일은 index파일과 express파일이 존재한다

- index : 가장 기본이 되는 루트 파일로 이곳에서 express를 띄우고, DB를 커넥션하는등 기본적인 설정을 해주는 곳이다
- express : express를 사용시 미들웨어가 많던가 기본적으로 포함해야하는 부분이 많다고 느껴질때 추가되는 곳이다.

### /src/model

ORM을 사용하는 경우 필요한 부분으로 ORM에서 model정의부분을 담당한다. 이부분은 ORM별로 다 틀려 자세한 설명은 생략한다

### /src/router

프로젝트의 router를 담당하는 디렉토리로 하위 폴더에 controller를 담당하는 코드를 작성을 하고, 하위폴더에서 값을 불러와서 사용한다.

### /src/router/domain ...

domain폴더는 도메인별로 만들며, 예시로 domain라고 만들었다

- index : 이곳에서 라우팅을 한후 export를 하거나 class의 instance를 만들어 export해준다.
- domain.controller : 클래스 형식으로 하는경우 생성자에서 routing을 해주며, 아닌경우 export만해준다. controller에서는 인자값 mapping만 해서 service함수를 호출하여 사용을 해준다.

### /src/service/domain ...

service폴더는 도메인별로 만드는 것을 기본으로 하며, 추가적으로 필요한경우 추가적으로 만들어도 된다. service로직은 req나 res를 인자값으로 받지 않도록 노력하며, 일반적인 함수로 만들어 Test Code를 만들기 쉽게 만든다. 만약 controller로직에서 Test를 하면 통합테스트를 하게 되기 때문에 Unit테스트를 위해서는 service로직을 분리해주는게 좋다.

### /src/middleware

middleware는 Error처리나 인증을 하기위한 부분으로 함수별로 파일을 만들어서 처리를 해준다. 이때 Error처리는 Error 클래스를 상속받아 사용하면 추가적인 데이터를 받을수 있다.(logger의 데이터 조작이 필요한 경우도 있다)

### /src/util

test Case나 다른 코드에서 반복되는 부분을 모아둔 부분으로 클래스나 다른곳에 두기 얘매한 코드가 자리한다. 협업을 하는경우 util에 있는 코드는 문서화가 필수이다.

### /config

DB접속정보나 코드의 설정이 있는 json파일들의 모음
