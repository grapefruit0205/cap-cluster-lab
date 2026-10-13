---
template: doc
theme: paper
lang: ko
title: cap 클러스터 실습 가이드
subtitle: Lab02 · AWS EC2에서 Kubernetes 클러스터를 만드는 5단계
---
SkillBoost 쇼핑몰의 7일 누적 실습을 위한 기반을 만듭니다. SSH 포트를 열지 않고 Session Manager로 관리합니다.

## A 시작 전에

이 가이드는 제공된 Lab02 교안을 바탕으로 구성했습니다. 명령은 **실행 위치 → 의미 → 예상 결과**를 확인하며 따라갑니다.

| 환경 | 기준 |
| --- | --- |
| 노드 | cap-master 1대, cap-node1·cap-node2 2대 |
| 기반 | Ubuntu 24.04, containerd 2.x, Kubernetes v1.36, Calico v3.32.1 |
| AWS | 서울 리전, 노드는 모두 2a, 2c 서브넷은 7일차 ALB용 |
| 유지 | 7일차까지 삭제하지 않습니다 |

버전과 명령은 교안 기준입니다. 이 문서 제작 과정에서 AWS 실습 명령을 실행하지는 않았습니다.

## B 다섯 단계

| 순서 | 페이지 | 다음으로 넘어가는 기준 |
| --- | --- | --- |
| ① | [콘솔에서 인프라 준비](lab02-step1.html) | 마스터 SSM Online |
| ② | [마스터에 공통 기반 설치](lab02-step2.html) | containerd CRI ok, 패키지 설치·버전 고정 |
| ③ | [AMI로 워커 복제](lab02-step3.html) | 세 노드의 고유 hostname, SSM Online |
| ④ | [클러스터 초기화·CNI](lab02-step4.html) | 세 노드 Ready |
| ⑤ | [검증·채점](lab02-step5.html) | 노드 간 HTTP·DNS·AWS 채점 통과 |

## C 먼저 알아둘 경계

**CloudShell과 노드 셸은 다릅니다.** AWS 설정 조회는 CloudShell, Kubernetes 설치와 검증은 노드 셸에서 수행합니다.

**AMI는 init 전에 만듭니다.** 프로그램은 복제하되 클러스터 인증서와 etcd 상태는 복제하지 않습니다.

**안전 주의:** SSM 에이전트를 정지하면 연결이 끊길 수 있습니다. ③의 정리 절차는 완료를 확인하고 진행해야 합니다.

## D 전체 토폴로지

![관리 화면과 아웃바운드 SSM 경로를 구분한 cap 클러스터 구성](/home/grapefruit/cap-cluster-lab02/site/assets/topology.png)

[① 인프라 준비부터 시작하기](lab02-step1.html)
