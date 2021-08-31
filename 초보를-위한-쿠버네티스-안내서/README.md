# 목차

1. [쿠버네티스 시작하기](#1-쿠버네티스-시작하기)
2. [쿠버네티스 알아보기](#2-쿠버네티스-알아보기)
3. [쿠버네티스 실습 준비](#3-쿠버네티스-실습-준비)
4. [쿠버네티스 기본 실습](#4-쿠버네티스-기본-실습)


# 1. 쿠버네티스 시작하기



<details>
<summary>1. 컨테이너 오케스트레이션 1/4(서버를 관리한다는것)</summary>

## 1. 컨테이너 오케스트레이션 1/4(서버를 관리한다는것)

- 처음에는 ppt와 같은 문서로 서버를 관리 했지만, 너무 복잡했었다.
- 그래서 등장한게 CHEF, ANSIBLE, PUPPET 와 같이 문서보다는 코드로 관리하게 되었다.
- 이 설정 관리 도구도 공부를 해야 된다는 문제도 있었고, 서버를 복잡하게 관리하다보면 결국 관리 자체도 쉽지 않았다.
- 그래서 나타난 것이, 가상 머신이다. 서버 하나에 가상머신 여러개! 조금 느리고 관리가 불편하지만 나쁘지 않았다.
- 하지만, 이것도 클라우드에는 적용이 안되고, 특정 벤더에 dependency도 생기고 느리다는 단점 등이 존재 했다.
- 이때, 도커가 등장하게 된다.

</details>





<details>
<summary>2. 컨테이너 오케스트레이션 2/4(도커의 등장)</summary>

## 2. 컨테이너 오케스트레이션 2/4(도커의 등장)

- 모든 실행환경을 컨테이너로!
- 어디서든 동작하고 쉽고 효율적이다.

### 컨테이너의 특징
- 가상 머신과 비교하여 컨테이너 생성이 쉽고 효율적
- 컨테이너 이미지를 이용한 배포와 롤백이 간단
- 언어나 프레임워크에 상관없이 애플리케이션을 동일한 방식으로 관리
- 개발, 테스팅, 운영 환경은 물론 로컬 피시와 클라우드까지 동일한 환경을 구축
- 특정 클라우드 벤더에 종속적이지 않음

![image](https://user-images.githubusercontent.com/28394879/131446052-22870fea-3eb5-4664-a4e0-d83fb3becd25.png)


![image](https://user-images.githubusercontent.com/28394879/131446177-cfc2c567-14a1-4d3c-ad09-50704e9fb7c0.png)
- 과거에는 어떤 언어나 프레임워크를 쓰느냐에 따라서 방법이 달랐었다.
- 도커 등장이후로 동일한 방식으로 배포가 가능하다.
- 하지만, 컨테이너가 많아질수록 관리가 힘들어지는 단점이 존재했었다.


</details>





<details>
<summary>3. 컨테이너 오케스트레이션 3/4(도커 그 이후)</summary>

## 3. 컨테이너 오케스트레이션 3/4(도커 그 이후)

### 1. 배포는 어떻게 할까 ?
- 컨테이너 기술이 좋긴 한데, 배포는 어떻게 해야 좋을까 ?
![image](https://user-images.githubusercontent.com/28394879/131446762-6455070d-ddd8-4e5f-a8da-2d8b4adbb1dd.png)
- 도커만으로는, 위에 사진 처럼 각 서버마다 들어가서 같은 작업을 해주어야 한다. 
- 하나하나 관리하는게 쉽지 않다.

![image](https://user-images.githubusercontent.com/28394879/131446911-08039b1b-9b6f-4a6e-8f0e-b035781ad07c.png)
- 이렇게 많은 도커를 사용하다 보면, 컨테이너가 실행 안되어 있는 서버가 존재한다.
- 어느 서버에 여유가 있는지 보려면, 모니터링 도구를 만들어야 될 수도 있고, 하나하나 접속해서 관리해야 되는 단점이 있다.

![image](https://user-images.githubusercontent.com/28394879/131447236-dd7c5889-fb5d-4241-88ce-5d3ed25af160.png)
- 그리고 또 하나의 문제는, 중앙에서 모든 컨테이너의 버전 업데이트를 하거나 롤백을 할때 일일이 관리하는게 쉽지가 않다.

### 2. 서비스 검색은 어떻게 할까 ?
![image](https://user-images.githubusercontent.com/28394879/131447415-1e76867c-8ccd-4a4c-b128-881fd16d4a3b.png)

### 3. 서비스 노출(Gateway)은 어떻게 할까?
![image](https://user-images.githubusercontent.com/28394879/131447498-35434a6a-6bcc-40c4-bd1c-d8048845bd70.png)
- 이렇게 구성하는게 간단하긴 하지만, 매번 nginx 설정을 해줘야 돼서 귀찮다.
- 이런 설정들을 자동으로 할 수 없을까 ? 

### 4. 서비스 이상, 부하 모니터링은 어떻게 할까?
![image](https://user-images.githubusercontent.com/28394879/131447660-4ea23021-af5a-4908-af3e-a1489d58b152.png)
- 여러개의 컨테이너중에 5개의 컨테이너가 죽었을때 어떻게 할까 ?
- 직접 다 들어가서 확인하기에는 번거롭고 쉽지 않다.


### 컨테이너 오케스트레이션
![image](https://user-images.githubusercontent.com/28394879/131447781-71a2f8c1-7f4c-4efc-b072-92344a9b7f7f.png)
- 컨테이너 기술 자체는 좋은데, 더 많은 컨테이너를 관리하기 위해서 나온 기술이다.

</details>





<details>
<summary>4. 컨테이너 오케스트레이션 4/4(컨테이너 오케스트레이션)</summary>

## 4. 컨테이너 오케스트레이션 4/4(컨테이너 오케스트레이션)

### 컨테이너 오케스트레이션
![image](https://user-images.githubusercontent.com/28394879/131447781-71a2f8c1-7f4c-4efc-b072-92344a9b7f7f.png)
- 서버관리자가 하는 일들을 대신하는 프로그램을 만든 것이다.

### 컨테이너 오케스트레이션 특징
1. CLUSTER 
- 중앙제어 (master-node): 마스터서버를 하나 두고 마스터 서버에 명령을 하면 node에 다 명령이 간다.
- 네트워킹: 노드들끼리의 네트워크 통신이 잘 되어야 함 
- 노드 스케일: 노드의 갯수와 상관없이 잘 돌아야 함

2. STATE
- 상태 관리

3. SCHEDULING
- 배포 관리: 서버를 새로 띄워서 배포하거나, 적절한 서버에 배포를 하는 작업

4. ROLLOUT & ROLLBACK
- 배포 버전관리

5. SERVICE & DISCOVERY
- 서비스 등록 및 조회

6. VOLUME
- 볼륨 스토리지: 각 서버의 적절한 스토리지가 관리 됨 (NFS, AWS EBS, GCE PD, ...)


- 여러 컨테이너 오케스트레이션이 등장했지만, 쿠버네티스가 표준처럼 등장하게 된다.


</details>





<details>
<summary>5. 왜 쿠버네티스인가?</summary>

## 5. 왜 쿠버네티스인가?

### 쿠버네티스 소개
- 컨테이너를 쉽고 빠르게 배포/확장하고 관리를 자동화해주는 오픈소스 플랫폼 
- 1주일에 20억개의 컨테이너를 생성하는 google이 컨테이너 배포 시스템으로 사용하던 borg를 기반으로 만든 오픈소스


### 쿠버네티스 특징
- 오픈소스
- 엄청난 인기
- 무한한 확장성
- 사실상의 표준 (de facto)

### 오픈소스
![image](https://user-images.githubusercontent.com/28394879/131449875-55e3ebe9-16fd-4b6d-8386-bf0ff5a9145c.png)

### 엄청난 인기 
![image](https://user-images.githubusercontent.com/28394879/131449949-36b699f9-2bd6-4370-81ee-32557a3574a3.png)
![image](https://user-images.githubusercontent.com/28394879/131450017-b01531a8-7398-475e-8a45-1c630cdd5bd3.png)

### 무한한 확장성
![image](https://user-images.githubusercontent.com/28394879/131450067-ecd01e07-b979-4386-b71c-99f2edfe4551.png)

### 사실상의 표준 (de facto)
![image](https://user-images.githubusercontent.com/28394879/131450369-4e88e005-2080-4962-8aa6-08e3afa7c524.png)
![image](https://user-images.githubusercontent.com/28394879/131450439-92b09d66-39b9-4ca5-adfe-5f5b9b9a6ed8.png)
![image](https://user-images.githubusercontent.com/28394879/131450482-dfd5f984-ffea-441d-88ed-ad80781ca449.png)
- Cloud Native의 핵심적인 역할을 한다.
- 사실상 표준이기 떄문에, 인프라를 위해서 찾아보면 왠만한 것들은 이미 다 나와 있다.




</details>



<details>
<summary>6. 어떤걸 배울까?</summary>

## 6. 어떤걸 배울까?

![image](https://user-images.githubusercontent.com/28394879/131450946-d9e8fed9-d997-4313-b947-5cb0dcbb5edc.png)
- 도커를 모른다면, 쿠버네티스를 완벽하게 이해할 수 없다.

![image](https://user-images.githubusercontent.com/28394879/131451015-c629fc08-21da-4f66-8eda-fd4745d5576d.png)

### 학습범위
- 도커 컨테이너 실행하기
    - 도커와 도커컴포즈를 이용한 멀티 컨테이너 관리
    
- 쿠버네티스에 컨테이너 배포하기
    - 실습(hands-on) 환경 만들기
    - kubectl 사용법
    - pod, deployment, service 등
    - 기본 리소스 학습
    
- 외부 접속 설정 하기
    - Cluster IP, NodePort, LoadBalancer, Ingress
    - 서비스 타입 학습
    - 서비스 디스커버리 학습 

- 스케일 아웃 하기
    - 부하에 따른 컨테이너 개수 조정
    - 최소 리소스 요청 설정
    - 오토스케일링

- 그외 고급기능 소개
    - HELM 패키지 매니저 소개
    - GitOps, ServiceMesh 소개

### 다루지 않는 범위
- 다양한 환경별 특징 (bare, metal, EKS, ...)
- 쿠버네티스 패턴 (사이드카, 어댑터, ...)
- 관련 생태계 (서비스메시, 서버리스, ...)
- GitOps CI/CD
- 승인제어 등 고급 기능

### 학슴 목표
- 구성요소 이해
- 동작원리 파악
- 기본적인 사용법






</details>






# 2. 쿠버네티스 알아보기

<details>
<summary> 1. 쿠버네티스 소개 </summary>

## 1. 쿠버네티스 소개

### 발음 정리
| 용어 | 발음
|-----|----|
|master|마스터|
|node|노드 (구 minion 미니언)|
|k8s|쿠버네티스, 케이에잇츠, 케이팔에스|
|kubectl|큐브 컨트롤, 큐브 시티엘, 큐브커들|
|etcd|엣지디, 엣시디, 이티시디|
|pod|팟,파드,포드|
|istio|이스티오|
|helm|헬름,핾,햄|
|knative|케이 네이티브|

### 쿠버네티스 소개
- 컨테이너화된 애플리케이션을 자동으로 배포, 스케일링 및 관리
- 컨테이너를 쉽게 관리하고 연결하기 위해 논리적인 단위로 그룹화
- Google에서 15년간 경험을 토대로 최상의 아이디어와 방법들을 적용

### CloudNative 소개
- 클라우드 이전
  - 리소스를 한땀 한땀 직접 관리 
- 클라우드 이후
  - 수많은 리소스를 자유롭게 사용하고 추상적으로 관리
- 클라우드 환경에서 어떻게 애플리케이션을 배포하는게 좋은걸까?  
  - 컨테이너
  - 서미스메시
  - 마이크로 서비스
  - API
  - 인프라 쓰고 버려
  - DevOps
  - 위에 나열된 방법들이 클라우드 스럽다 혹은 CloudNative 하다고 하는것이다.

</details>







<details>
<summary> 2. 쿠버네티스 아키텍처 1/3 (구성/설계) </summary>

## 2. 쿠버네티스 아키텍처 1/3 (구성/설계)


</details>




<details>
<summary> 3. 쿠버네티스 아키텍처 2/3 (오브젝트) </summary>

## 3. 쿠버네티스 아키텍처 2/3 (오브젝트)


</details>




<details>
<summary> 4. 쿠버네티스 아키텍처 3/3 (API 호출) </summary>

## 4. 쿠버네티스 아키텍처 3/3 (API 호출)


</details>









# 3. 쿠버네티스 실습 준비

# 4. 쿠버네티스 기본 실습
