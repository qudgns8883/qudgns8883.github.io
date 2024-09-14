---
layout: post
title:  "CozyHouse"
info: 쇼핑몰[진행 중]
tech: "Java, Spring Boot, Spring Data JPA, Spring Security, MySQL"
type: Team project
---

# 📌 CozyHouse
"cinema"와 "broadcast"의 결합으로 영화를 브로드캐스팅하여 사용자에게 최신 영화 정보와 편리한 예매 서비스를 제공합니다.

## 🖥️ 프로젝트 소개
스프링 부트를 이용해 오늘의 집 사이트를 참고하여 만든 쇼핑몰입니다.

## 👨‍👩‍👦 프로젝트 구성원
- **팀장**: 김민석 - 프론트엔드
- **팀원1**: 이병훈 - 백엔드
- **팀원2**: 김준모 - 백엔드


## ⚙️ 사용된 기술
JAVA, MYSQL, JPA, Spring Framework, CSS3, HTML5, BOOTSTRAP, JAVASCRIPT, JQUERY

# 💡 수행업무

## 회원가입
- OAuth2 방식을 사용하여 JWT를 이용한 회원가입 기능을 구현하였습니다.
-  모든 회원가입 로직은 백엔드에서 처리합니다.

## 로그인, 소셜로그인, 로그아웃
- OAuth2 방식으로 로그인 및 소셜 로그인 기능을 구현하였습니다.
- JWT를 사용하여 인증 토큰을 관리하고, 모든 인증 관련 로직은 백엔드에서 처리합니다.
- 여러 필터를 커스터마이즈하여 로그인, 로그아웃 및 JWT 검증을 관리합니다.
- 리프레시 토큰을 사용하여 세션 유지 기능을 구현하였으며, 리프레시 토큰 로테이션을 통해 보안성을 강화하였습니다.

## 전역예외처리
- AOP를 활용해 애플리케이션 전반에 걸쳐 발생하는 예외를 처리합니다.

## 글쓰기
- 파일 업로드를 위해 MultiparFile와 Java NIO를 사용하여 처리합니다.
