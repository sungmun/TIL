# Issue

여기에서는 EC2를 사용하며 나온 오류를 기록하고, 해결방법을 서술할 것이다.

---
```bash
 Load key "~/.ssh/*.pem": bad permissions
```
EC2를 생성시 pem파일을 주는데 이때 파일의 권한은 400으로 주어야 권한 오류가 나지 않는다.

---

```bash
 ubuntu@{endPoint}: Permission denied (publickey,gssapi-keyex,gssapi-with-mic).
```

ec2의 경우 무조건적으로 ubuntu가 사용자 명이지는 않는다.

- Amazon Linux 2 또는 Amazon Linux AMI의 경우 사용자 이름은 `ec2-user`입니다.
- CentOS AMI의 경우 사용자 이름은 `centos` 입니다.
- Debian AMI의 경우 사용자 이름은 `admin` 또는 `root` 입니다.
- Fedora AMI의 경우 사용자 이름은 `ec2-user` 또는 `fedora` 입니다.
- RHEL AMI의 경우 사용자 이름은 `ec2-user` 또는 `root` 입니다.
- SUSE AMI의 경우 사용자 이름은 `ec2-user` 또는 `root` 입니다.
- Ubuntu AMI의 경우 사용자 이름은 `ubuntu` 입니다.

---

