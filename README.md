# aws-loxilb-open5gs-topology

## 사용하기 전
먼저 terraform 설치가 필요합니다. [테라폼 설치 페이지]를 참고해서 설치해주세요.
AWS에 배포를 위해서 AWS 접근 권한을 가진 IAM 권한 설정이 필요합니다.   
AWS 사용자의 Access Key 정보 등록을 위해 aws CLI 설치가 필요합니다. [aws CLI 설치 페이지]를 참고해서 설치해주세요.

## 사용방법
다음 명령어로 aws 사용자의 access key 정보와 사용할 리전을 등록합니다.
```
$ aws configure
 AWS Access Key ID [None]: ~~~
 AWS Secret Access Key [None]: ~~~
 Default region name [None]: ap-northeast-2
 Default output format [None]: json
```

해당 저장소를 clone 합니다.
```
$ git clone https://github.com/backguynn/aws-loxilb-open5gs-topology.git
```

다음 명령어를 입력하면 배포가 완료됩니다.
```
cd aws-loxilb-open5gs-topology/use-ami
terraform init
terraform apply
```

배포 완료 후 다음 명령어를 사용하면 kubectl 사용에 필요한 kubeconfig 파일을 생성할 수 있습니다.
```
aws eks --region $(terraform output -raw region) update-kubeconfig --name $(terraform output -raw cluster_name)
```

배포한 토폴로지를 삭제하려면 다음 명령어를 사용합니다.
```
terraform destroy
```

[테라폼 설치 페이지]: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli
[aws CLI 설치 페이지]: https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/getting-started-install.html
