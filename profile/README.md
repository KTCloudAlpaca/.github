# ktCloud Tech up 클라우드 인프라 5기 기본 프로젝트 (1팀 알파카) 

<br>

## 💡프로젝트 개요 
온프레미스 Kubernetes에 장애가 나면 AWS의 DR 서버에 같은 Terraform 코드로 같은 환경을 자동으로 만들고, 온프레가 살아나면 데이터를 가지고 되돌아오는(페일백) 하이브리드 클라우드 DR 프로젝트

<br>
<br>

## 💬기획 의도 및 주제 선정 

<img width="749" height="388" alt="image" src="https://github.com/user-attachments/assets/eca2fde7-8331-4e21-be5c-acf5325608b7" />

<img width="781" height="362" alt="image" src="https://github.com/user-attachments/assets/2fb55067-b1ce-4718-a37d-37245c0ffbb0" />

<img width="764" height="387" alt="image" src="https://github.com/user-attachments/assets/3a3a348e-aa10-43e0-aea2-49c0bf5c9535" />

<img width="770" height="401" alt="image" src="https://github.com/user-attachments/assets/7349c992-22e1-46df-8b33-c53ba5183cf9" />

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


## 전체 아키텍쳐 구성도 

<img width="743" height="408" alt="image" src="https://github.com/user-attachments/assets/ff5c0a89-3039-45e7-8e48-2c221814f6ca" />

<br>


### 온프레미스 구성도 

<img width="807" height="389" alt="image" src="https://github.com/user-attachments/assets/71473b8e-e39b-4f45-9252-fa268d37d184" />

<br>


### AWS Cloud단 구성도 

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


## 🗓️프로젝트 수행 절차


<br>


## 구현 단계 


<br>


## RTO / RPO



