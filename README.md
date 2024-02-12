# 지정 Project : 가상 MSP 고객을 대상으로 인프라 구축
![image](https://github.com/RoDawn/-MSP-/assets/143478463/d93ea1cc-3a10-4141-8509-6202a07c888c)
- **기간 :** 2024.01.25 ~ 2024.02.07
- **팀 프로젝트** (3명)
- **나는? :** 전체 일정과 해야할 일을 선정하고 팀원에게 분배, 인프라 구축, PPT 제작 
- **주제 선정 이유 :** 교육 기관에서 지정해준 주제로 프로젝트를 진행했습니다. 고객 미팅, 견적서 작성, 인프라 구축, 고객 대응 등의 과정을 겪으며 현업의 체험을 할 수 있었습니다. 이를 통해 이론으로만 배웠던 클라우드를 실전에서 어떻게 적용되는지 알 수 있었습니다. 특히 Systemc Security Checker를 이용해 OS, WAS의 취약점을 체크하고 점검하는 과정을 통해 Linux의 활용법에 대해 크게 배울 수 있어서 좋았습니다.

## STEP1. 아키텍쳐
![image](https://github.com/RoDawn/-MSP-/assets/143478463/ef4218d6-f66e-4430-a83c-c341ecb2214f)
- **Point1 :** 멀티존, 고가용성을 위해 Auto-Scaling과 Load Balancer 를 이용
- **Point2 :** Web, Was를 모두 Private에 두고, 별도의 관리 서버를 구축
- **Point3 :** 동영상, 이미지에 대한 트래픽 부하 분산을 위해 Object Storage와 CDN+ 연동 
- **Point4 :** Cloud insight를 이용한 Management 상품 구축 


## STEP2. 사용 기술
- AWS & NCP : VPC, ACG, Subnet, EC2 & VM, Load Balancer
- OS : Ubunt
- NginX, Apache Tomcat
  
## STEP3. 구현 결과
1. Linux에서 NAS 자동 MOUNT 설정

2. Linux에서 고객 전용 USER 설정 후, Pem key 없이 원격 접속 가능하도록 설정

3. Systemc Security Checker를 이용해 OS, WAS의 취약점을 체크
- /etc/ssh/sshd_config 를 이용해 Root 계정 원격 접속 제한
- pwquality.conf 에서 패스워드 복잡성 설정
- commont-auth와 commnond-password 에서 계정 임계값 설정
- chmod 644 /etc/shadow 를 이용해 파일 소유자 및 권한 설정
- chmod 400 /etc/hosts 를 이용해 파일 소유자 및 권한 설정
- chmod 400 /etc/syslog.conf 를 이용해 파일 소유자 및 권한 설정
- chmod 640 /etc/hosts.allow and deny 를 이용해 파일 소유자 및 권한 설정 

4. WMS에 알림 설정 후 트러블 슈팅 대응

5. Global CDN과 Object Storage 를 연동해서 속도 향상. 기존 Object만 단독 사용시보다 3초 단축

6. J-meter를 이용해 1천명, 3천명, 5천명 트래픽 부하 테스트

## STEP4. 결과
- 5개의 팀이 경쟁했습니다. 저희 팀은 1명이 부족했고, 전공자가 한 명도 속해있지 않았습니다. 그러한 상황 속에서 팀원 모두 마음을 모아 최선을 다해 경쟁했고 우수상을 수여받았습니다.
  
## STEP5. 느낀점
- 평소 구축하던 3-Tier 이외에 WMS 를 비롯한 Management 상품을 구축해서 운영 경험을 할 수 있었습니다.
- System security checker 를 통해 os, was를 점검했습니다. 이를 통해 os에서 각 파일별로 권한을 달리 해야함을 배울 수 있었습니다.
- 최우수상을 받았던 팀은 구축 전에 J-meter를 이용해 스펙 선정을 했습니다. 왜 3-Tier 인지? 왜 이런 스펙으로 구축했는지? 에 대한 디테일함이 돋보였습니다. 저도 다음에는 왜 이런 인프라, 구성, 스펙을 선정했는지에 대한 실험과 테스트가 필요하다고 느꼈습니다.
