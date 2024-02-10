# 지정 Project : 가상 MSP 고객을 대상으로 인프라 구축
![image](https://github.com/RoDawn/-MSP-/assets/143478463/d93ea1cc-3a10-4141-8509-6202a07c888c)
- **기간 :** 2024.01.25 ~ 2024.02.07
- **팀 프로젝트** (3명)
- **나는? :** 전체 일정과 해야할 일을 선정하고 팀원에게 분배, 인프라 구축, PPT 제작 
- **주제 선정 이유 :** 교육 기관에서 지정해준 주제로 프로젝트를 진행했습니다. 고객 미팅, 견적서 작성, 인프라 구축, 고객 대응 등의 과정을 겪으며 현업의 체험을 할 수 있었습니다. 이를 통해 이론으로만 배웠던 클라우드를 실전에서 어떻게 적용되는지 알 수 있었습니다. 특히 Systemc Security Checker를 이용해 OS, WAS의 취약점을 체크하고 점검하는 과정을 통해 Linux의 활용법에 대해 크게 배울 수 있어서 좋았습니다.

## STEP1. 아키텍쳐
![image](https://github.com/RoDawn/-MSP-/assets/143478463/5774eb1b-6944-4897-b397-02970976fe6c)
- **Point1 :** 멀티존, 고가용성을 위해 Auto-Scaling과 Load Balancer 를 이용
- **Point2 :** 동영상, 이미지에 대한 트래픽 부하 분산을 위해 Object Storage와 CDN+ 연동 
- **Point3 :** Cloud insight를 이용한 Management 상품 구축 

## STEP2. 사용 기술
- AWS & NCP : VPC, ACG, Subnet, EC2 & VM, Load Balancer
- OS : Ubunt
- NginX, Apache Tomcat
  
## STEP3. 구현 사진
Linux에서 NAS 자동 MOUNT 설정

Linux에서 고객 전용 USER 설정 후, Pem key 없이 원격 접속 가능하도록 설정

Systemc Security Checker를 이용해 OS, WAS의 취약점을 체크

=> /etc/ssh/sshd_config 를 이용해 Root 계정 원격 접속 제한 
=> pwquality.conf 에서 패스워드 복잡성 설정
=> commont-auth와 commnond-password 에서 계정 임계값 설정 
=> chmod 644 /etc/shadow 를 이용해 파일 소유자 및 권한 설정 
=> chmod 400 /etc/hosts 를 이용해 파일 소유자 및 권한 설정 
=> chmod 400 /etc/syslog.conf 를 이용해 파일 소유자 및 권한 설정 
=> chmod 640 /etc/hosts.allow and deny 를 이용해 파일 소유자 및 권한 설정 

WMS에 알림 설정 후 트러블 슈팅 대응

Global CDN과 Object Storage 를 연동해서 속도 향상. 기존 Object만 단독 사용시보다 3초 단축

J-meter를 이용해 1천명, 3천명, 5천명 트래픽 부하 테스트







## STEP4. 결과
- 3-Tier 까지 구축한다고 했을 때, Concole은 13분 -> Terraform 6분, 작업 시간 2배 단축
- Prometheus, Grafana 설치 스크립트도 포함 시켜서 Node 역할로 프로비저닝
   
## STEP5. NEXT Action
- NLB & Auto-Scaling 도 Terraform으로 코드 작성하기

## STEP6. 느낀점
- Concole로 작업했을 때 ACG Rule 등 Network 쪽에서 많은 실수가 발생했었습니다. Terraform 으로 작업하면 실수가 거의 0%에 가까워졌기에 작업의 효율성이 증가해서 좋았습니다.
- 동일한 3-Tier를 3개 구축한다고 했을 때, 일일이 손으로 다 설정해줘야 하는 불편함이 있었습니다. IaC 덕분에 동일한 작업 경우 시간을 엄청 단축할 수 있었습니다.
- 클라우드만 공부하다가 Code 계열의 작업을 해서 적응하는데 시간이 오래 걸렸습니다. 욕심 같아선 Terraform code 한 줄을 전부 해석 할 수 있으면 좋겠지만 당장은 과하다고 생각했습니다. 우선은 공식 문서 등에 나와있는 코드를 활용하며 하나의 코드 묶음이 어떤 역할을 하는지, 만약 CIDR 등을 바꾸고 싶다면 어떤 것을 바꿔야 하는지? 위주로 활용해가고자 합니다.
