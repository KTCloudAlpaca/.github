# kTCloud Tech up 클라우드 인프라 5기 기본 프로젝트 (1팀 알파카) 

본 프로젝트는 kTCloud Tech up 클라우드 인프라 5기에서 진행한 기본 프로젝트입니다. 


<br>

## 💡프로젝트 개요 

온프레미스 Kubernetes 클러스터에 장애가 나면 AWS의 DR 서버로 서비스를 자동 전환하고, 온프레가 복구되면 데이터를 가지고 다시 돌아오는 하이브리드 클라우드 DR 프로젝트입니다. DR 서버는 평소 쿠버네티스만 설치된 빈 상태로 대기해 비용을 줄이고, 장애가 나면 온프레를 만든 Terraform 코드 그대로 같은 환경을 만들어 두 환경의 설정 차이를 없앴습니다. 하트비트 감지부터 CloudWatch, EventBridge, CodeBuild, SSM으로 이어지는 복구 과정은 사람 개입 없이 자동으로 진행됩니다.

온프레로 돌아올 때는 쓰기 중지, 덤프, 복원 순서를 지키는 페일백으로 DR 기간에 쌓인 데이터까지 유실 없이 옮깁니다.


<br>
<br>

## 💬기획 의도 및 주제 선정 


### 문제 인식

<img width="749" height="388" alt="image" src="https://github.com/user-attachments/assets/eca2fde7-8331-4e21-be5c-acf5325608b7" />

최근 연이어 발생한 대규모 서버 장애 사례를 보며, 저희 팀은 왜 같은 문제가 반복되는지 의문을 갖게 되었습니다. 두 사건의 공통점은 서버 이중화가 되어 있지 않았고, 수동 복구에 의존해 대응이 늦어졌다는 점이었습니다. 결국 핵심은 장애 상황에서 서버를 유연하게 운영할 수 있는 구조가 없었다는 데 있었고, 이를 통해 장애 시에는 빠른 대응과 데이터 무결성이 가장 중요하다는 것을 깨달았습니다.

<br>

### 아이디어

<img width="781" height="362" alt="image" src="https://github.com/user-attachments/assets/2fb55067-b1ce-4718-a37d-37245c0ffbb0" />

모든 서비스를 온프레미스에만 두는 대신, 장애가 났을 때만 AWS에서 서비스를 구동한다면 비용을 크게 늘리지 않고도 서비스 중단을 최소화할 수 있지 않을까 생각했습니다. 그래서 자동화와 서버 이중화를 통해 탄력적으로 서버를 운영할 수 있다는 것을 직접 구현해 보여주고자 했습니다.

<br>

### 차별화 포인트

<img width="764" height="387" alt="image" src="https://github.com/user-attachments/assets/3a3a348e-aa10-43e0-aea2-49c0bf5c9535" />

DR 서버는 평소 쿠버네티스만 설치된 상태로 대기하고, 장애가 나면 온프레미스를 만든 Terraform 코드 그대로 같은 환경을 빠르게 구축합니다. 또한 실제 장애 시나리오로 복구와 페일백을 검증해 RTO와 RPO를 측정했고, 짧은 시간 안에 환경을 다시 구축할 수 있음을 확인했습니다.

<br>

### 프로젝트 목표

<img width="770" height="401" alt="image" src="https://github.com/user-attachments/assets/7349c992-22e1-46df-8b33-c53ba5183cf9" />

하트비트로 장애를 자동 감지하고, 1시간마다 백업되는 데이터를 바탕으로 DR 서버에 서비스를 복구합니다. 온프레미스가 정상화되면 DR 기간에 쌓인 데이터를 가지고 다시 온프레미스로 페일백합니다. 이를 통해 평소에는 AWS 비용을 최소화하고, 장애가 났을 때만 AWS에서 서비스를 운영하는 구조를 만드는 것이 목표입니다.

<br>
<br>

## 🛠️활용한 기술 


| 분류 | 기술 |
| --- | --- |
| **On-Prem / K8s** | ![Rocky Linux](https://img.shields.io/badge/Rocky%20Linux-9.8-10B981?style=for-the-badge&logo=rockylinux&logoColor=white) ![Kubernetes](https://img.shields.io/badge/Kubernetes-v1.36.3-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white) ![containerd](https://img.shields.io/badge/containerd-575757?style=for-the-badge&logo=containerd&logoColor=white) ![Flannel](https://img.shields.io/badge/Flannel-6B7280?style=for-the-badge) ![Istio](https://img.shields.io/badge/Istio-466BB0?style=for-the-badge&logo=istio&logoColor=white) ![MetalLB](https://img.shields.io/badge/MetalLB-6B7280?style=for-the-badge) ![NFS CSI](https://img.shields.io/badge/NFS%20CSI-6B7280?style=for-the-badge) ![full-cluster-backup.sh](https://img.shields.io/badge/full--cluster--backup.sh-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white) |
| **AWS DR** | ![EC2](https://img.shields.io/badge/EC2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white) ![S3](https://img.shields.io/badge/S3-569A31?style=for-the-badge&logo=amazons3&logoColor=white) ![ECR](https://img.shields.io/badge/ECR-FF9900?style=for-the-badge) ![CloudWatch](https://img.shields.io/badge/CloudWatch-FF4F8B?style=for-the-badge&logo=amazoncloudwatch&logoColor=white) ![EventBridge](https://img.shields.io/badge/EventBridge-FF4F8B?style=for-the-badge) ![CodeBuild](https://img.shields.io/badge/CodeBuild-FF9900?style=for-the-badge) ![SSM](https://img.shields.io/badge/SSM-FF4F8B?style=for-the-badge) ![Route 53](https://img.shields.io/badge/Route%2053-8C4FFF?style=for-the-badge&logo=amazonroute53&logoColor=white) ![IAM](https://img.shields.io/badge/IAM-DD344C?style=for-the-badge&logo=amazoniam&logoColor=white) |
| **IaC / Automation** | ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white) ![Bash](https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white) |
| **App / Data** | ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white) ![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black) ![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=for-the-badge&logo=mongodb&logoColor=white) ![Nginx](https://img.shields.io/badge/Nginx-009639?style=for-the-badge&logo=nginx&logoColor=white) ![S3 Backup](https://img.shields.io/badge/S3%20Backup-569A31?style=for-the-badge&logo=amazons3&logoColor=white) ![WireGuard](https://img.shields.io/badge/WireGuard-88171A?style=for-the-badge&logo=wireguard&logoColor=white) ![SSH](https://img.shields.io/badge/SSH-231F20?style=for-the-badge&logo=openssh&logoColor=white) |
| **Monitoring / Test** | ![Prometheus](https://img.shields.io/badge/Prometheus-E6522C?style=for-the-badge&logo=prometheus&logoColor=white) ![Grafana](https://img.shields.io/badge/Grafana-F46800?style=for-the-badge&logo=grafana&logoColor=white) ![Alertmanager](https://img.shields.io/badge/Alertmanager-E6522C?style=for-the-badge&logo=prometheus&logoColor=white) ![CSI](https://img.shields.io/badge/CSI-6B7280?style=for-the-badge) |

<br>
<br>


## 📑전체 아키텍쳐 구성도 

<img width="743" height="408" alt="image" src="https://github.com/user-attachments/assets/ff5c0a89-3039-45e7-8e48-2c221814f6ca" />

<br>


### 🖥️ 온프레미스 구성도 

<img width="807" height="389" alt="image" src="https://github.com/user-attachments/assets/71473b8e-e39b-4f45-9252-fa268d37d184" />

<br>


### 🖥️ AWS Cloud단 구성도 

<img width="752" height="405" alt="image" src="https://github.com/user-attachments/assets/2c89035d-b989-4685-aa65-bfcb868907ff" />


<br>
<br>


## 👥팀원 

<img width="780" height="364" alt="image" src="https://github.com/user-attachments/assets/248a9c29-6f71-427c-ae0f-78b96b6c4a97" />


## 👥 Team

<table>
  <tr>
    <th align="center" width="160">On-Prem · CloudWatch</th>
    <th align="center" width="160">App · IaC · DR 자동화</th>
    <th align="center" width="160">DNS Failover</th>
    <th align="center" width="160">DB 백업 · 네트워크</th>
    <th align="center" width="160">Monitoring</th>
  </tr>
  <tr>
    <td align="center"><img src="https://github.com/ionacat.png" width="90" /></td>
    <td align="center"><img src="https://github.com/wonee1.png" width="90" /></td>
    <td align="center"><img src="https://github.com/junsung.png" width="90" /></td>
    <td align="center"><img src="https://github.com/doycho1007.png" width="90" /></td>
    <td align="center"><img src="https://github.com/develchoi.png" width="90" /></td>
  </tr>
  <tr>
    <td align="center"><a href="https://github.com/ionaca">신경빈</a></td>
    <td align="center"><a href="https://github.com/wonee1">김채원</a></td>
    <td align="center"><a href="https://github.com/junsung">권준성</a></td>
    <td align="center"><a href="https://github.com/doycho1007">조동연</a></td>
    <td align="center"><a href="https://github.com/develchoi">최동경</a></td>
  </tr>
  <tr>
    <td align="center"><b>온프레미스, CloudWatch</b><br>K8s 클러스터, Heartbeat, Alarm<br>온프레미스 K8s 운영, 1분 Heartbeat, CloudWatch Alarm 검증</td>
    <td align="center"><b>app, IaC, DR 자동화</b><br>Terraform, EventBridge, CodeBuild<br>aws-bootstrap, 복구 파이프라인, SSM, recover.sh, failback.sh, application 개발</td>
    <td align="center"><b>DNS Failover</b><br>Route 53, Health Check<br>Primary·Secondary 레코드, Failover·Failback 검증</td>
    <td align="center"><b>DB 백업, 네트워크, AWS VPC 구성</b><br>MongoDB, S3<br>정기 백업·복원, RPO 검증 테스트</td>
    <td align="center"><b>모니터링</b><br>Prometheus, Grafana<br>모니터링 스택, 장애·복구 상태 검증, 관측성 확보</td>
  </tr>
</table>


<br>


## 🗓️프로젝트 수행 일정 

2026.09.30 ~ 2026.10.29 / 전체 수행 일정

| 단계 (Phase) | 기간 | 주요 수행 | 핵심 산출물 |
| --- | --- | --- | --- |
| **1. 기획 및 환경 준비** | 09/30 ~ 10/05 | 프로젝트 주제 선정, 팀 빌딩 및 역할 분담 확정<br>K8s 클러스터 설치, IP 대역 설정 및 네트워크 연결 검증 | 역할 분담 시트<br>K8s 기본 인프라 |
| **2. 서비스 구축 및 멘토링** | 10/10 ~ 10/17 | K8s 내 담당 서비스 배포 및 서비스 간 통신·볼륨 연결 확인<br>기술 멘토링 피드백 반영, 트러블슈팅 및 기술 스택 발표 | 중간 보고서<br>기술 스택 발표 자료 |
| **3. DR 핵심 기능 구현** | 10/14 ~ 10/19 | **S3 백업:** 1시간 주기 자동 백업 파이프라인 및 네트워크 구축<br>**Route 53:** Primary/Secondary 장애 조치 및 Health Check 구성<br>**CloudWatch:** 1분 주기 하트비트(Cron) 모니터링 및 알람 설정<br>**IaC & 복구:** Terraform(DR, Bootstrap) 및 Failback 자동화 구현 | DR 아키텍처 구축 완료<br>Terraform / Failback 코드 |
| **4. 안정화 및 테스트** | 10/19 ~ 10/26 | 통합 트러블슈팅 및 DR 시나리오(Failover/Failback) 검증<br>종일 멘토링 Q&A 점검 및 시스템 부하 테스트 수행 | DR 테스트 결과<br>최종 보고서(PPT) 초안 |
| **5. 최종 제출 및 발표** | 10/28 ~ 10/29 | 최종 보고서(PPT) 드라이브 제출 (10/28 18:00 마감)<br>최종 발표 및 DR 시연 진행 (10/29 11:00)<br>프로젝트 산출물 정리 및 GitHub 리포지토리 공개 | 최종 발표 PPT<br>GitHub 저장소 |

<br>


## 구현 단계 


<br>


## RTO / RPO 검증 






