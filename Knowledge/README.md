## 목차

1. [MSA](#MSA)

## MSA

###### MicroService Architecture "마이크로서비스 아키텍쳐"

출처: https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-1-MSA%EC%9D%98-%EA%B8%B0%EB%B3%B8-%EA%B0%9C%EB%85%90-3sk28yrv0e

> MSA의 등장 배경

MSA의 등장을 살펴보기 위해, 기존에는 어떤 방식으로 개발을 진행해 왔는지를 살펴보자.

<img width="514" src="https://github.com/epikxm/docs/blob/main/Knowledge/ma_msa.jpg?raw=true" />

Monolithic Architecture란, 소프트웨어의 모든 구성요소가 통합되어 있는 형태이다.

아직까지 많은 소프트웨어가 Monolithic 형태로 구현되어 있고, 소규모 프로젝트에는 Monolithic Architecture가 훨씬 합리적이다.  
간단한 Architecture이고 유지보수가 용이하기 때문.

하지만 일정 규모 이상의 서비스, 혹은 수백명의 개발자가 투입되는 프로젝트에서 Monolithic Architecture는 한계가 있다.

1. 서비스/프로젝트가 커질수록 영향도 파악 및 전체 시스템 구보 파악이 어려움
2. 빌드 시간 및 테스트 시간, 배포 시간이 기하급수적으로 늘어남
3. 서비스를 부분적으로 scale-out하기 힘듦
4. 부분의 장애가 전체 서비스의 장애로 번질 수 있음

> 특징

1. 독립적 배포 가능
2. 개별 프로세스로 구동 가능
3. REST-API 같은 가벼운 방식으로 통신

> 장점

1. 서비스별 개별 배포 가능 (배포시 서비스 중단 없음)
2. 확장의 용이성
3. 장애 발생시 처리 용이 (개별 프로세스만 중단 가능)

> 단점

1. 서비스가 많아질수록 관리 포인트가 늘어남 (서비스별 연관성 및 의존성이 늘어남)
2. 하나의 서비스에서 결과가 나온다는 보장이 없음 (서비스의 분산 및 상호 의존성과 관련)
3. 서비스의 분산으로 인한 테스트의 어려움
