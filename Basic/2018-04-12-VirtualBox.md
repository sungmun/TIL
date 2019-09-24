# VirtualBox란

VirtualBox는 기존의 운영체제(Host OS)위에 가상의 운영체제(Guest OS)를 올려주는 프로그램으로 보통 다른 운영체제를 경험을 해보던가 자신이 만든 프로그램을 실행을 해볼때 다른 운영체제에서 어떤 식으로 실행이 되는지, Host OS가 아닌 다른 운영체제의 프로그램을 만들 때, 사용이 된다. 

## VirtualBox 설치

설치 페이지 : https://www.virtualbox.org/wiki/Downloads

## 사용하는 이유

일단 윈도우에서는 VirtualBox를 사용하며 여러가지 환경 설정을 하기가 쉬워진다. 왜냐하면, 일단 다수의 개발 프로그램은 윈도우를 기준으로 만들기 보다는 리눅스를 기준으로 만들던가 아니면 Mac을 기반으로 만드는 커널기반으로 만들다 보니 Windows에서는 별도의 설정을 해주는 데 걸리는 시간이 상당하다. 

거기에 개발자가 서버 개발자일 경우 서버는 대부분 Linux기반 운영체제라서 Linux에서 테스트를 해야 하는데, VirtualBox에 공유폴더 기능을 이용해서 개발은 Windows에서 하고 테스트는 Guest OS에서 하는 방식으로 만들면 상당히 편하다.

특히 Node나 Python같이 여러 오픈소스를 이용해서 만드는 경우는 VirtualBox를 통해서 두개의 개발환경을 분리가 가능하기 때 문에 상당히 깔끔해 보인다