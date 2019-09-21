# AWS 

AWS를 사용하며 나온 ISSUE와 AWS에 있는 많은 서비스의 사용법이나 용도에 대한 기록이다.

- [EC2](/AWS/EC2/README.md)
- [RDS](/AWS/RDS/README.md)
- [CloudWatch](/AWS/CloudWatch/README.md)
- [CodeBuild](/AWS/CodeBuild/README.md)

## VPC(Virtual Private Cloud)

아마존에서 사용을 하는 리소스 접근 제어 방식중 하나로, A라는 서비스에서 B라는 서비스에 접근을 하려면 2가지가 필요한데 권한과 같은 VPC내에 존재해야 한다는점이다. 다른 VPC에 존재하는 서비스에 접근을 하려면 복잡한 방법으로 해야하는 것으로 보인다. 그러나 제대로 사용을 하면 서비스간에 네트워크가 분리를 해주어 보안이 올라가는 효과가 있을것으로 보인다.

