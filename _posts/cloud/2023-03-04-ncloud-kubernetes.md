---
layout: single
title: "어플리케이션 개발환경 구축을 위한 cloud 환경설정 - 쿠버네티스 환경 구성"
categories: cloud
tag: [cloud, ncloud, svelte, sveltekit]
comments: true
---

# ncloud 환경구성

## 목표
- ncloud에서 kubernetes 서비스 및 서버 등 구성하기

## 도전!

### step 1

#### 진행
- naver cloud platform 가입 및 콘솔버튼 클릭

#### 결과
![ncloud 메인화면](../../assets/images/cloud-kubernetes-1.png)

### step 2

#### 진행
- VPC → Kubernetes Service → Clusters

#### 결과 
![ncloud 메인화면](../../assets/images/cloud-kubernetes-2.png)

### step 3

#### 진행
- Kubernetes 설정 
- VPC, Subnet, LB Private 서브넷 만들어야됨.

#### 결과 
![ncloud 메인화면](../../assets/images/cloud-kubernetes-3.png)

#### 각 항목 설명(said chatGPT)

##### CNI Plugin
- CNI Plugin은 Kubernetes 클러스터 내에서 컨테이너 간 통신 및 호스트와의 통신을 관리하는 플러그인입니다. Kubernetes에서는 다양한 CNI Plugin을 지원하며, 예를 들어 Calico, Flannel, Weave 등이 있습니다.
- 선택의 여지가 없음.

##### VPC
- VPC(Virtual Private Cloud)는 클라우드 컴퓨팅에서 사용되는 개념으로, 논리적으로 격리된 가상 네트워크를 생성하는 기능입니다. VPC를 사용하면 클라우드 환경에서 논리적으로 격리된 네트워크를 구성할 수 있습니다.

##### Subnet
- Subnet은 VPC 내에서 논리적으로 분리된 네트워크입니다. VPC를 사용하여 생성한 가상 네트워크 안에서 서브넷을 생성하면, 서브넷 내에서는 논리적으로 격리된 네트워크를 사용할 수 있습니다.
 
#### LB Private 서브넷
- LB Private 서브넷은 Application Load Balancer(ALB) 등의 로드 밸런서를 프라이빗 서브넷에 생성하는 방법입니다. 이 방법을 사용하면 로드 밸런서와 백엔드 서버 간의 트래픽이 VPC 내에서 안전하게 전송될 수 있습니다.

#### Audit Log
- Audit Log는 시스템에서 발생하는 모든 이벤트를 기록하는 로그입니다. Kubernetes에서는 Audit Log를 사용하여 클러스터의 모든 작업을 추적하고 감사할 수 있습니다.

### step 4

#### 진행
- VPC 이름 및 IP대역설정
![ncloud 메인화면](../../assets/images/cloud-kubernetes-4.png)

#### 결과
- 운영중이라고 뜨면 정상
![ncloud 메인화면](../../assets/images/cloud-kubernetes-4-2.png)
- 클러스트 생성 화면에서 새로고침 버튼 누르면 방금 생성한 VPC를 선택할수 있게 됨.
![ncloud 메인화면](../../assets/images/cloud-kubernetes-4-3.png)

### step 5

#### 진행
- 서브넷 생성
![ncloud 메인화면](../../assets/images/cloud-kubernetes-5.png)
 
#### 결과
![ncloud 메인화면](../../assets/images/cloud-kubernetes-5-2.png)

### step 6

#### 진행
- LB(Load Balancer) 서브넷 생성
  ![ncloud 메인화면](../../assets/images/cloud-kubernetes-6.png)

#### 결과
![ncloud 메인화면](../../assets/images/cloud-kubernetes-6-2.png)

### step 7

#### 진행
- VPC, Subnet, LB Subnet 선택
![ncloud 메인화면](../../assets/images/cloud-kubernetes-7.png)

#### 결과
- NAT Gateway 만들고 오라고 오류
![ncloud 메인화면](../../assets/images/cloud-kubernetes-7-2.png)

### step 8

#### 진행
- NAT Gateway 생성
  ![ncloud 메인화면](../../assets/images/cloud-kubernetes-8.png)

#### 결과
- NAT Gateway 만들고 오라고 오류
  ![ncloud 메인화면](../../assets/images/cloud-kubernetes-8-2.png)

### step 9

#### 진행
- 노드풀 생성
![ncloud 메인화면](../../assets/images/cloud-kubernetes-9.png)
- 인증키 설정 : 키 이름 설정하고 생성하면 됨.(민감정보 이미지 비노출)
- 최종확인 : 생성정보 확인하고 생성 누르면 됨.(민감정보 이미지 비노출)

#### 결과
![ncloud 메인화면](../../assets/images/cloud-kubernetes-12.png)


### step 10
- cluster 접근하기 위한 서버 생성

#### 진행
- platform을 classic으로 변경
![ncloud 메인화면](../../assets/images/cloud-kubernetes-13.png)

- 서버 이미지 선택(Micro가 1년간 무료라 사용)
![ncloud 메인화면](../../assets/images/cloud-kubernetes-13-2.png)
![ncloud 메인화면](../../assets/images/cloud-kubernetes-13-3.png)
 
- 서버설정(Micro라 선택의 여지가 적음.)
![ncloud 메인화면](../../assets/images/cloud-kubernetes-13-4.png)

- 인증키 설정 : 키 이름 설정하고 생성하면 됨. 기존에 있는거 연결 가능.
- 네트워크접근설정  ACG연결. 생성하고 연결해도 됨.
![ncloud 메인화면](../../assets/images/cloud-kubernetes-13-5.png)
  
#### 결과
![ncloud 메인화면](../../assets/images/cloud-kubernetes-13-6.png)

### step11
- 인텔리J에서 서버 접속하기

#### 진행
- 새로 생성된 서버의 관리자 비밀번호를 알아낸다
![ncloud 메인화면](../../assets/images/cloud-kubernetes-13-7.png)
![ncloud 메인화면](../../assets/images/cloud-kubernetes-13-8.png)
![ncloud 메인화면](../../assets/images/cloud-kubernetes-13-9.png)

- IntelliJ에서 terminal을 켠다 : Alt+F12

- 명령어를 친다. : ssh -i [.pem키 경로] root@포트포워딩정보상의 서버접속용공인IP -p 포트
  ex) : ssh -i C:\test-key.pem root@000.000.000.000 -p 80

- 비밀번호 입력단계에서 관리자 비밀번호 입력해주면 끝.

#### 결과
- 아래처럼 뜨면 접속된 것.

![ncloud 메인화면](../../assets/images/cloud-kubernetes-13-10.png)

### step12
- micro서버에 쿠버네티스 & 도커 설치

#### 진행
- 아래 명령어 수행

```shell
sudo apt-get update
sudo apt-get install -y docker.io # 도커설치
sudo systemctl start docker # 도커실행
sudo systemctl enable docker # 부팅시 자동시작
 
```


- IntelliJ에서 terminal을 켠다 : Alt+F12

- 명령어를 친다. : ssh -i [.pem키 경로] root@포트포워딩정보상의 서버접속용공인IP -p 포트
  ex) : ssh -i C:\test-key.pem root@000.000.000.000 -p 80

- 비밀번호 입력단계에서 관리자 비밀번호 입력해주면 끝.

#### 결과
- 아래처럼 뜨면 접속된 것.


★ 해당 블로그는 끝없는 시행착오의 과정입니다. 문과 출신 개초보 프로삽질러 개발자라 용어의 사용이 정확하거나 적합하지 않을 수 있습니다. 혹시 잘못된 부분은 댓글 달아주시면 확인 후 시정토록 하겠습니다. 많이 배우겠으니 많은 지식의 공유가 이루어졌으면 좋겠습니다. 그리고 개발을 시작하는 분들에게도 작게나마 도움이 되길 바랍니다.






