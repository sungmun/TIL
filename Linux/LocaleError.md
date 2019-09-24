# locale Error

mariaDB를 설치 후 mycli를 이용하여 처음 시작시 나온 Error로 언어 타입이 맞지 않아 나오는 Error로 보인다

Linux(Ubuntu 18.04.2 LTS)

mariaDB 10.1.40

mycli 1.8.1

```
Traceback (most recent call last):
  File "/usr/bin/mycli", line 11, in <module>
    load_entry_point('mycli==1.8.1', 'console_scripts', 'console')()
  File "/usr/lib/python3/dist-packages/click/core.py", line 722, in __call__
    return self.main(*args, **kwargs)
  File "/usr/lib/python3/dist-packages/click/core.py", line 676, in main
    _verify_python3_env()
  File "/usr/lib/python3/dist-packages/click/_unicodefun.py", line 118, in _verify_python3_env
    'for mitigation steps.' + extra)
RuntimeError: Click will abort further execution because Python 3 was configured to use ASCII as encoding for the environment.  Consult http://click.pocoo.org/python3/for mitigation steps.

This system supports the C.UTF-8 locale which is recommended.
You might be able to resolve your issue by exporting the
following environment variables:

    export LC_ALL=C.UTF-8
    export LANG=C.UTF-8
```

이 Error는 언어타입을 UTF-8로 변경을 해주면 해결이 되며, 위에 나온데로 `export LC_ALL=C.UTF-8`를 해도 해결이 된다. 그러나 `export`를 통해 해결을 하면, 로그아웃시 초기화가 되어 로그인시마다 다시 해줘야한다는 단점이 있다.이를 해결하기 위해 `locale`의 default값을 변경해주어야 하는데 이경우 방법이 3가지가 있다

## 1.

```
sudo nano /etc/default/locale

# File generated by update-locale
LANG="ko_KR.UTF-8"
LANGUAGE="ko_KR:ko"
```

`/etc/default/locale`를 수정을 하는 방법

## 2.

```
sudo dpkg-reconfigure locales
```

방향키와 스페이스바를 이용해서 `ko_KR.UTF-8`을 찾아 선택을 하는 방법

## 확인

위의 방법을 이용후

```
#locale

LANG=ko_KR.UTF-8
LANGUAGE=
LC_CTYPE="ko_KR.UTF-8"
LC_NUMERIC="ko_KR.UTF-8"
LC_TIME="ko_KR.UTF-8"
LC_COLLATE="ko_KR.UTF-8"
LC_MONETARY="ko_KR.UTF-8"
LC_MESSAGES="ko_KR.UTF-8"
LC_PAPER="ko_KR.UTF-8"
LC_NAME="ko_KR.UTF-8"
LC_ADDRESS="ko_KR.UTF-8"
LC_TELEPHONE="ko_KR.UTF-8"
LC_MEASUREMENT="ko_KR.UTF-8"
LC_IDENTIFICATION="ko_KR.UTF-8"
LC_ALL=ko_KR.UTF-8
```

이를 이용해서 확인을 한다.

대다수의 경우 위의 방법을 이용해서 해결이 되나, 되지 않는 경우도 있는데 그경우에는 로그인시마다 자동으로 `export LC_ALL="ko_KR.UTF-8"`입력이 되도록 하는 방법으로
`~/.bashrc`파일에 `export LC_ALL="ko_KR.UTF-8"`을 추가를 해주는 방법이다.