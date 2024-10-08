---
layout: post
title:  "CinemaCast"
info: "영화예매사이트"
tech : "Java, Spring Boot, Spring Data JPA, Spring Security, MySQL"
type: Team project
---

# 🖥️ 프로젝트 소개
영화관 사이트를 참고하여 "cinema"와 "broadcast"의 결합으로 영화 정보와 편리한 예매 기능을 제공하는 웹 애플리케이션을 개발하였습니다.

<br/>

## 🔗 GitHub 주소
[프로젝트 GitHub 저장소](https://github.com/qudgns8883/CINEMACAST)

## 📄 프로젝트 발표 자료
- 발표 자료는 [여기에서 다운로드할 수 있습니다](https://docs.google.com/presentation/d/1Ua3kVJtuOFLrB7LKAKkkmn6AiUeTZ_L_/edit?usp=drive_link&ouid=104385299162078736648&rtpof=true&sd=true).

## 👨‍👩‍👦 프로젝트 구성원
- **팀장**: 김소연 - 회원가입, 로그인, 관리자, 결제 페이지 개발
- **팀원1**: 조혜령 - 기획서 작성, 퍼블리싱, 좌석 선택 및 상영시간표 구현
- **팀원2**: 김우영 - TMDB.API를 이용한 영화 정보 페이지 개발
- **팀원3**: 이병훈 - TMDB.API를 이용한 영화 정보 페이지 및 고객센터 구현

## ⚙️ 사용된 기술
- **Java**: 서버 사이드 로직 구현
- **Spring Boot**: 애플리케이션의 빠른 개발을 위한 프레임워크
- **Spring Data JPA**: 데이터베이스와의 원활한 상호작용을 위한 ORM
- **Spring Security**: 안전한 인증 및 권한 관리를 위한 보안 프레임워크
- **MySQL**: 데이터 저장을 위한 관계형 데이터베이스
- **CSS3, HTML5, BOOTSTRAP, JAVASCRIPT, JQUERY**: 프론트엔드 개발

<br/>

# 💡 담당 기능

## 메인 페이지
- TMDB API를 호출하여 인기순위, 상영작, 개봉예정작 및 비디오 데이터를 처리하여 영화 정보를 제공합니다.

## 영화 상세페이지
 - TMDB API를 호출하여 영화의 상세 내용을 동적으로 로드하여 사용자에게 제공합니다.
 - 사용자가 영화에 대한 평점을 주고 리뷰를 작성할 수 있는 폼을 구현했습니다.
 - 영화 정보를 카카오톡으로 공유하는 기능을 추가하여, 사용자 간의 영화 정보 공유를 용이하게 하였습니다.

## 고객센터
-  Naver SMTP를 이용하여 사용자 문의 내용을 관리자에게 전송하는 기능을 구현 했습니다.
-  WebSocket을 사용하여 사용자와 관리자가 실시간으로 메시지를 주고받을 수 있도록 하였습니다.

## 공지사항, 이벤트
- 기본적인 CRUD 작업을 통해 이벤트 및 공지사항 관리 기능을 구현했습니다.

## 관리자 페이지
- 관리자는 지정된 ID와 비밀번호로 로그인 후 이벤트 및 공지사항의 CRUD 작업을 수행할 수 있습니다.
- 1대 1 채팅 및 사용자 문의에 대한 답변 기능을 구현했습니다.

<br/>

# 📦 배포 경험

### CI/CD 파이프라인 구성
- **GitHub Actions**를 활용하여 코드 변경 사항 발생 시 자동으로 빌드 및 배포되는 CI/CD 파이프라인을 설정하였습니다. 이를 통해 배포 과정에서의 인적 오류를 줄일 수 있었습니다.

### Docker를 활용한 환경 설정
- **Docker**와 **Docker Compose**를 사용하여 개발 환경과 배포 환경을 통일하였습니다. 이를 통해 로컬 개발 환경에서의 문제를 최소화하고, 운영 환경에 쉽게 배포할 수 있는 기반을 마련했습니다.

## 📝 노션 
[CICD 정리](https://bottlenose-asparagus-798.notion.site/GitHub-Actions-Docker-NGINX-EC2-RDS-CI-CD-1141bba98c5780a8b299e9806e62544e?pvs=74)

### ARCHITECTURE
<img class="selfie" alt="이병훈" src="/assets/img/architecture.png" />

<br/>

# 🛠️ 트러블슈팅 내용

## 문제 상황

1. Member와  Genre간의 관계를 설정할 때, genres필드가 초기화되지 않았습니다. 이로 인해 연관된 Genre엔티티를 추가할 때 예외가 발생.
2. DTO를 엔티티로 변환할 때, 컬렉션 필드가 초기화되지 않아 변환된 엔티티에서 데이터를 추가하는 과정에서 문제가 발생.
3. 트랜잭션 관리가 부족하여, 영화, 감독, 배우 데이터를 저장할 때 일부 데이터만 저장되고 나머지는 저장되지 않음.
4. 이로 인해 데이터베이스에 저장된 데이터의 일관성이 깨졌고, 데이터의 무결성이 손상.


## 해결 방안

1. **컬렉션 필드 초기화**

   연관 관계 컬렉션 필드를 초기화하여 데이터 추가 작업을 안전하게 처리할 수 있습니다. 이를 통해 NullPointerException 문제를 예방하고, 연관된 엔티티가 올바르게 관리되도록 합니다.

2. **DTO에서 엔티티 변환 시 필드 초기화**

   DTO를 엔티티로 변환할 때, 엔티티의 컬렉션 필드를 초기화하여 변환된 엔티티가 정상적으로 데이터를 추가할 수 있도록 합니다. 이를 통해 엔티티 생성 시 컬렉션 필드가 초기화되지 않아 발생할 수 있는 문제를 예방할 수 있습니다.

3. **트랜잭션 적용**

   서비스 계층에서 @Transactional 어노테이션을 사용하여 트랜잭션을 관리합니다. 이를 통해 데이터 저장 작업이 모두 성공하거나 모두 롤백되도록 하여 데이터 일관성을 보장합니다.

## 결과

1. **데이터 무결성 보장**: 연관된 컬렉션이 초기화되어 데이터 정상적으로 저장되고, DTO를 엔티티로 변환할 때 필드가 올바르게 초기화됩니다. 트랜잭션이 적용되어 데이터 저장 중 예외 발생 시 모든 작업이 롤백됩니다.
2. **예외 처리 개선**: NullPointerException과 같은 예외 발생 가능성이 줄어들고, 데이터 일관성이 유지됩니다.
3. **안정성 향상**: 연관된 엔티티와 데이터 저장 작업이 안정적으로 처리되어 애플리케이션의 신뢰성이 높아졌습니다.

## 느낀점

1. **컬렉션 필드와 DTO 초기화**: 이번 문제를 통해, 컬렉션 필드와 DTO에서 엔티티 변환 시 초기화가 중요하다는 점을 깨달았습니다. 적절한 초기화가 없으면 데이터 추가 작업에서 예외가 발생할 수 있음을 직접 경험했습니다.
2. **트랜잭션 관리의 중요성**: 트랜잭션을 통해 데이터 저장의 일관성과 무결성을 보장할 수 있다는 점도 매우 중요하다는 것을 배웠습니다.
3. **애플리케이션 설계의 안정성**: 작은 실수라도 데이터 무결성에 큰 영향을 미칠 수 있다는 점을 깨달았고, 이를 예방하기 위해 필드 초기화와 트랜잭션 관리를 항상 고려해야 한다는 점을 알게 되었습니다.
