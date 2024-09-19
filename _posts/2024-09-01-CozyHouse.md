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
Java, Spring Boot, Spring Data JPA, Spring Security, MySQL

<br/>

# 💡 담당 기능

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

<br/>

# 🛠️ 트러블슈팅 내용

## 문제 상황 
1. 소셜 로그인 구현 시, 일반 로그인처럼 엑세스 토큰과 리프레시 토큰을 HTTP 응답 헤더로 받으려 했습니다.
2. 그러나 하이퍼링크를 통해 리다이렉션되는 과정에서 응답 헤더에 직접 접근할 수 없는 상황이 발생했습니다.
3. 이로 인해 JWTFilter는 요청 헤더에서 받은 엑세스 쿠키로 인증을 하게 되었고, 이로 인해 일관성이 떨어지는 문제가 발생했습니다.

## 해결 방안
1. **쿠키를 통한 토큰 전송**  
   - 소셜 로그인 후, 엑세스 토큰과 리프레시 토큰을 서버에서 쿠키로 설정해 클라이언트에 전송.  
   - HttpOnly 속성을 사용하여 JavaScript에서 쿠키에 접근할 수 없도록 설정해 XSS 공격에 대한 보안을 강화.

2. **엑세스 토큰 요청 헤더로 변환**  
   - 로그인 성공 핸들러를 통해 JWT를 발급하는 방식이 쿠키와 헤더로 다르기 때문에, 쿠키에 저장된 엑세스 토큰을 클라이언트에서 요청 헤더로 변환하여 백엔드에 요청.  
   - 서버에서 새로운 엑세스 토큰을 응답 헤더로 받아올 수 있도록 하여 JWTFilter의 일관성을 유지하고, 모든 인증 로직을 요청 헤더 방식으로 통합.  

3. **로컬 스토리지에 저장**  
   - 서버에서 받은 엑세스 토큰은 로컬 스토리지에 저장해 클라이언트에서 쉽게 접근할 수 있도록 설정.  
   - 로컬 스토리지에 저장된 토큰이 XSS 공격에 노출되지 않도록 콘텐츠 보안 정책(CSP, Content Security Policy)을 설정.  
   
## 결론
1. 소셜 로그인 과정에서 하이퍼링크로 인한 리다이렉션 문제 때문에, 쿠키를 사용해 토큰을 전송하는 방식을 선택했습니다.
2. 이후, 엑세스 토큰을 요청 헤더로 변환하여 클라이언트에 전달함으로써 일관성을 유지했습니다.
3. 로그인 성공 핸들러에서 JWT 발급 방식을 통합해 JWTFilter의 일관성을 확보했으며, 이는 보안과 사용성을 동시에 고려한 해결책으로 효과적으로 적용되었습니다.

## 느낀 점
1. JWT 토큰을 활용하여 쿠키와 요청 헤더를 조합한 인증 방식이 효과적이라는 것을 깨달았습니다.
2. 특히 HttpOnly 속성의 중요성을 통해 XSS 공격 방어를 강화할 수 있음을 배웠고, CSP(Content Security Policy)와 로컬 스토리지로 클라이언트 측 보안을 높일 수 있었습니다.
3. 이번 경험을 통해 웹 보안의 중요성을 깊이 이해하게 되었고, 앞으로 JWT를 활용해 안전하고 효율적인 시스템을 구축하는 데 기여하고 싶습니다.

<br/>

# 프로젝트 설정

이 프로젝트를 실행하기 위해서는 몇 가지 환경 설정이 필요합니다. 아래의 단계를 따라주세요.


## 1. 데이터베이스 설정
1. MySQL에서 cozy-house 데이터베이스를 생성합니다.
2. 아래의 정보를 바탕으로 application.properties 파일을 설정합니다.

## 2. application.properties 설정

src/main/resources/application.properties 파일을 다음과 같이 생성 후 설정합니다:

- ### 애플리케이션 이름 및 포트
spring.application.name=backend  
server.port=8081  

- ### 파일 업로드 디렉토리
file.upload-dir=C:\\파일경로\\file\\  
spring.servlet.multipart.enabled=true  
spring.servlet.multipart.max-file-size=50MB  
spring.servlet.multipart.max-request-size=50MB  

- ### MySQL 설정
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver  
spring.datasource.url=YOUR_URL_HERE  
spring.datasource.username=YOUR_username_HERE  
spring.datasource.password=YOUR_PASSWORD_HERE  

- ### JPA 설정
spring.jpa.properties.hibernate.show_sql=true  
spring.jpa.properties.hibernate.format_sql=true  
spring.jpa.hibernate.ddl-auto=update  
spring.jpa.database-platform=org.hibernate.dialect.MySQL8Dialect  
spring.jackson.property-naming-strategy=SNAKE_CASE  
spring.jwt.secret=YOUR_SECRET_KEY_HERE  

- ### 보안 로깅
logging.level.org.springframework.security=DEBUG  

- ### kakao OAuth2
spring.security.oauth2.client.registration.kakao.client-name=Kakao  
spring.security.oauth2.client.registration.kakao.client-id=YOUR_CLIENT_ID  
spring.security.oauth2.client.registration.kakao.client-secret=YOUR_CLIENT_SECRET  
spring.security.oauth2.client.registration.kakao.redirect-uri=http://localhost:8081/login/oauth2/code/kakao  
spring.security.oauth2.client.registration.kakao.authorization-grant-type=authorization_code  
spring.security.oauth2.client.registration.kakao.scope=account_email, profile_nickname  
spring.security.oauth2.client.registration.kakao.client-authentication-method=client_secret_post  
spring.security.oauth2.client.provider.kakao.authorization-uri=https://kauth.kakao.com/oauth/authorize  
spring.security.oauth2.client.provider.kakao.token-uri=https://kauth.kakao.com/oauth/token  
spring.security.oauth2.client.provider.kakao.user-info-uri=https://kapi.kakao.com/v2/user/me  
spring.security.oauth2.client.provider.kakao.user-name-attribute=id  

- ### Google OAuth2
spring.security.oauth2.client.registration.google.client-name=google  
spring.security.oauth2.client.registration.google.client-id=YOUR_CLIENT_ID  
spring.security.oauth2.client.registration.google.client-secret=YOUR_CLIENT_SECRET  
spring.security.oauth2.client.registration.google.redirect-uri=http://localhost:8081/login/oauth2/code/google  
spring.security.oauth2.client.registration.google.authorization-grant-type=authorization_code  
spring.security.oauth2.client.registration.google.scope=profile,email  

- ### GitHub OAuth2
spring.security.oauth2.client.registration.github.client-name=GitHub  
spring.security.oauth2.client.registration.github.client-id=YOUR_CLIENT_ID  
spring.security.oauth2.client.registration.github.client-secret=YOUR_CLIENT_SECRET  
spring.security.oauth2.client.registration.github.redirect-uri=http://localhost:8081/login/oauth2/code/github  
spring.security.oauth2.client.registration.github.authorization-grant-type=authorization_code  
spring.security.oauth2.client.registration.github.scope=SCOPE_read:user,SCOPE_user:email  
spring.security.oauth2.client.registration.github.client-authentication-method=client_secret_post  
spring.security.oauth2.client.provider.github.authorization-uri=https://github.com/login/oauth/authorize  
spring.security.oauth2.client.provider.github.token-uri=https://github.com/login/oauth/access_token  
spring.security.oauth2.client.provider.github.user-info-uri=https://api.github.com/user  
spring.security.oauth2.client.provider.github.user-name-attribute=id  

- ### Naver OAuth2
spring.security.oauth2.client.registration.naver.client-name=naver  
spring.security.oauth2.client.registration.naver.client-id=YOUR_CLIENT_ID  
spring.security.oauth2.client.registration.naver.client-secret=YOUR_CLIENT_SECRET  
spring.security.oauth2.client.registration.naver.redirect-uri=http://localhost:8081/login/oauth2/code/naver  
spring.security.oauth2.client.registration.naver.authorization-grant-type=authorization_code  
spring.security.oauth2.client.registration.naver.scope=name,email  
spring.security.oauth2.client.provider.naver.authorization-uri=https://nid.naver.com/oauth2.0/authorize  
spring.security.oauth2.client.provider.naver.token-uri=https://nid.naver.com/oauth2.0/token  
spring.security.oauth2.client.provider.naver.user-info-uri=https://openapi.naver.com/v1/nid/me  
spring.security.oauth2.client.provider.naver.user-name-attribute=response  

- ### CoolSMS 설정(회원가입 인증코드 비활성화했습니다.)
coolsms.api.key=YOUR_COOLSMS_API_KEY  
coolsms.api.secret=YOUR_COOLSMS_API_SECRET  
coolsms.from=YOUR_COOLSMS_FROM_NUMBER  

- ### Redis 설정
spring.data.redis.host=localhost  
spring.data.redis.port=6379  

## 3. 프론트엔드 실행방법
1. 프론트엔드 디렉터리 이동 
   - cd frontend  
2. 의존성 설치
   - npm install
3. 애플리케이션 설치
   - npm run dev