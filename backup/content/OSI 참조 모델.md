---
title: "OSI 참조 모델"
description: "다른 시스템 간의 원활한 통신을 위해 ISO 에서 제안한 통신 규약이다.전송에 필요한 두 장치 간의 접속과 절단 기계적, 전기적, 기능적, 절차적 특성에 대한 규칙두 개의 인접한 개방 시스템 간에 신뢰성 있고 효율적인 정보 전송.송신측과 수신 측의 속도 차이를 해결하기"
date: 2021-05-07T05:24:03.410Z
tags: ["정보처리기사"]
---
## 정의
- 다른 시스템 간의 원활한 통신을 위해 ISO 에서 정한 통신 규약이다. 
- 컴퓨터 통신 논리구조

![](/images/043eca15-fd2e-48fc-9434-0040776394fa-image.png)

### 물리 계층
- 전송에 필요한 두 장치 간의 접속과 절단 
- 기계적, 전기적, 기능적, 절차적 특성에 대한 규칙
- Transmit raw data between devices electrically/optically

### 데이터 링크 계층
- 두 개의 인접한 개방 시스템 간에 신뢰성 있고 효율적인 정보 전송.
- 송신측과 수신 측의 속도 차이를 해결하기 위한 흐름 제어.
- 프레임 동기화
- 오류 검출 회복을 위한 오류 제어.
- Transfer data from node-to-node packaged into frames. (corrects errors) 
- Contains MAC(Media Access Control) and LLC(logical Link Control)

### 네트워크 계층
- 개방 시스템들 간의 네트워크 연결을 관리하는 기능과 데이터의 교환 및 중계. 
- Receive frame from data-link layer and deliver them to intended destination based on address inside the frame. 
- Finds destination by using logical addreses such as IP

### 전송 계층
- 논리적 안정과 균일한 데이터 전송 서비스 제공.
- Manage delivery and error checking of data packets. TCP

### 세션 계층
- 송수신 측 간의 관련성을 유지하고 대화 제어를 당담. 
- Controls conversations between different computers.

### 표현 계층
- 데이터를 세션 계층에 보내기 전에 통신에 적당 형태로 변환한다.
- Translate data for application layer based on syntax/semantics application accepts.

### 응용 계층
- 사용자가 OSI 환경에 접근할 수 있는 서비스를 제공. - Interacts with sw application 

## 참고
https://www.forcepoint.com/ko/cyber-edu/osi-model