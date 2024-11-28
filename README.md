# Hangle-test-function-project

## 웹사이트 주소 : [뭉클](https://moongcle.xyz)  
  
로그인을 해야하는 구조의 사이트입니다.  
간단한 시연한 영상을 첨부하겠습니다.  
[![Video Label](https://i.ytimg.com/vi/psoi1_03HzY/hqdefault.jpg?sqp=-oaymwE1CKgBEF5IVfKriqkDKAgBFQAAiEIYAXABwAEG8AEB-AH-CYAC0AWKAgwIABABGGUgZShlMA8=&rs=AOn4CLB3o-3CuJmmXZlH5OX5JQlnkQ-08w)](https://youtu.be/psoi1_03HzY)

## 웹 사이트 정리
Server : Ubuntu 24.04 LTS  
Frontend : ReactNative  
Backend : Node.js (pm2)  

## 데이터베이스 서버 정리
Server : Ubuntu 24.04  
Database : DB (가용 램 10GB)  

## 클라이언트 로컬 서버 프로그램
Backend : Django 5.0.2   
Language : Python 3.12  
Framework : pywin32, pillow, pyhwpx  


### 문제 업로드 기능과 미들웨어 프로그램 결합 
![alt text](image/image.png)  

### 시험지 조회 기능과 미들웨어 프로그램 결합
![alt text](image/image2.png)

### 출제 유형 3번 문제 선택기능과 미들웨어 프로그램 결합
![alt text](image/image3.png)

파이썬 프로그램으로 url 주소를 받아
win32를 통해 한글 프로그램을 컨트롤하여 데이터를 생성 및 DB에 업로드를 진행
이후 [시험지 생성 / 문제집 생성] 기능을 통해 생성된 데이터를 활용하여 시험지를 제작

## 주요 사이트 내부 작업 시퀀스 다이어그램 정리
### 회원가입 과정
```mermaid
sequenceDiagram
	회원가입->>DB[ID 테이블]: ID에 대한 DB 테이블 생성 (Node.js -> DB)
	회원가입->>DB[ID 테이블]: ID 저장 / PW(암호화) (Node.js -> DB)
	관리자->>DB[ID 테이블]: 권한 수락 (Node.js -> DB -> Node.js)
	회원가입->>DB[ID 테이블]: 전화번호 (Node.js -> DB)
	회원가입->>DB[ID 테이블]: 생년월일 (Node.js -> DB)
	회원가입->>DB[ID 테이블]: 가입일 (Node.js -> DB)
	회원가입->>DB[ID 테이블]: 이메일 (Node.js -> DB)
	사용자->>DB[ID 테이블]: 비밀번호 수정
	사용자->>DB[ID 테이블]: 학원 이미지 등록
	
```

### 문제 데이터 생성 및 시험지 출제 정리
```mermaid
sequenceDiagram
사용자 문제 업로드->>DB[문제 데이터 테이블]: 문제[id]
DB[문제 데이터 테이블]->>시험지[교사용]: 문제[id]
사용자 문제 업로드->>DB[문제 데이터 테이블]: 문제[HWP]
DB[문제 데이터 테이블]->>시험지[교사용]: 문제[HWP]
DB[문제 데이터 테이블]->>시험지[학생용]: 문제[HWP]
사용자 문제 업로드->>DB[문제 데이터 테이블]: 정답[TEXT]
사용자 문제 업로드->>DB[문제 데이터 테이블]: 정답[HWP]
DB[문제 데이터 테이블]->>시험지[교사용]: 해설[HWP]
사용자 문제 업로드->>DB[문제 데이터 테이블]: 해설[HWP]
DB[문제 데이터 테이블]->>시험지[교사용]: 정답[HWP]
```


### 시험지-QR정오표-학생성적표 결과
```mermaid
sequenceDiagram
시험지->>QR정오표: 문제 번호
시험지->>QR정오표: 정답[TEXT]
QR정오표->>학생 테이블: 정답개수
QR정오표->>학생 테이블: 오답문항 / 문제id
```

## 느낀점
공동으로 진행하는 프로젝트에서  
외주사 클라이언트와 소통에 어려움을 느꼈다.  
서버의 구성, 사용할 언어, 문제 상황 생성, 구조 설정 등  
다양한 문제/해결 과제를 정의하여 팀원과 잘 협의하여 제작하며   
이후 발생할 오류와 다음으로 데이터를 조회하는 쿼리를 개선해야할 부분 등  
작은 문제(단순 오류, 성능 개선)부터 큰 오류(시스템 다운, 소통 마비, 교착 지점 발생 등)을 작게나마 경험할 수 있었던 프로젝트였다.
