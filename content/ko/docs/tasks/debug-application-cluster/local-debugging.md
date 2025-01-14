---
title: 로컬에서 서비스 개발 및 디버깅
content_type: task
---

<!-- overview -->

쿠버네티스 애플리케이션은 일반적으로 각각 자체 컨테이너에서 실행되는 여러 개의 개별 서비스로 구성된다. 원격의 쿠버네티스 클러스터에서 이러한 서비스를 개발하고 디버깅하는 것은 번거로울 수 있으며 [동작중인 컨테이너의 셸에 접근](/docs/tasks/debug-application-cluster/get-shell-running-container/)하고 원격 셸 내에서 도구를 실행해야 한다.

`텔레프레즌스`는 원격 쿠버네티스 클러스터로 서비스를 프록시하면서 로컬에서 서비스를 개발 및 디버깅하는 과정을 용이하게 하는 도구이다. `텔레프레즌스`를 사용하면 로컬 서비스에 대해 디버거 및 IDE와 같은 사용자 지정 도구를 사용할 수 있고 원격 클러스터에서 실행되는 컨피그맵(ConfigMap), 시크릿(Secret) 및 서비스(Service)에 대한 전체 접근 권한을 서비스에 제공할 수 있다.

이 문서는 `텔레프레즌스`를 사용하여 원격 클러스터에서 실행되는 서비스를 로컬로 개발하고 디버그하는 방법을 설명한다.




## {{% heading "prerequisites" %}}


* 쿠버네티스 클러스터가 설치되어 있어야 한다.
* `kubectl`은 클러스터와 통신하도록 구성되어 있어야 한다.
* [텔레프레즌스](https://www.telepresence.io/reference/install)가 설치되어 있어야 한다.



<!-- steps -->

## 원격 클러스터에서 셸 가져오기

터미널을 열고 인수 없이 `텔레프레즌스`를 실행하여 `텔레프레즌스` 셸을 가져온다. 이 셸은 로컬에서 실행되어 로컬 파일 시스템에 대한 전체 접근 권한을 제공한다.

`텔레프레즌스` 셸은 다양한 방식으로 사용할 수 있다. 예를 들어, 랩탑에서 셸 스크립트를 작성하고 셸에서 실시간으로 직접 실행한다. 원격 셸에서도 이 작업을 수행할 수 있지만 원하는 코드 편집기를 사용하지 못할 수 있으며 컨테이너가 종료되면 스크립트가 삭제된다.

종료하고 셸을 닫으려면 `exit`를 입력한다.

## 기존 서비스 개발 또는 디버깅하기

쿠버네티스에서 애플리케이션을 개발할 때 일반적으로 단일 서비스를 프로그래밍하거나 디버그한다. 서비스는 테스트 및 디버깅을 위해 다른 서비스에 접근해야 할 수 있다. 한 가지 옵션은 지속적인 배포 파이프라인을 사용하는 것이지만 가장 빠른 배포 파이프라인이라도 프로그램 또는 디버그 주기에 지연이 발생한다.

`--swap-deployment` 옵션을 사용하여 기존 배포를 텔레프레즌스 프록시로 교체한다. 스와핑을 사용하면 서비스를 로컬에서 실행하고 원격 쿠버네티스 클러스터에 연결할 수 있다. 원격 클러스터의 서비스는 이제 로컬에서 실행 중인 인스턴스에 접근할 수 있다.

`--swap-deployment`로 텔레프레즌스를 실행하려면 다음을 입력한다.

`telepresence --swap-deployment $DEPLOYMENT_NAME`

여기서 $DEPLOYMENT_NAME은 기존 배포의 이름이다.

이 명령을 실행하면 셸이 생성된다. 셸에서 서비스를 시작한다. 그런 다음 로컬에서 소스 코드를 편집하고 저장하고 변경 사항이 즉시 적용되는 것을 확인할 수 있다. 디버거 또는 기타 로컬 개발 도구에서 서비스를 실행할 수도 있다.



## {{% heading "whatsnext" %}}

핸즈온 튜토리얼에 관심이 있다면 구글 쿠버네티스 엔진에서 방명록 애플리케이션을 로컬로 개발하는 과정을 안내하는 [이 튜토리얼](https://cloud.google.com/community/tutorials/developing-services-with-k8s)을 확인한다.

텔레프레즌스에는 상황에 따라 [많은 프록시 옵션](https://www.telepresence.io/reference/methods)이 있다.

자세한 내용은 [텔레프레즌스 웹사이트](https://www.telepresence.io)를 참고하길 바란다.


