# 코멘토-직무부트캠프

> [1주차](#1주차-) - 스프링 프레임워크와 Maria DB 설정 후 테스트 화면 출력 </br>
[2주차](#2주차-) - HTTP와 REST API, 통계 API 초안 작성 </br>
[3주차](#3주차-) - 스프링 부트 개발 환경 셋팅, 통계 API 수정, 통계 API 위한 SQL문 작성해보기 </br>
[4주차](#4주차-) - API 개발

</br>

---

### 1주차 </br>
> 스프링 프레임워크와 Maria DB 설정 후 테스트 화면 출력

**1. 개발환경 셋팅** </br>
- JDK: 11.0.14
- IDE: Eclipse 2019-06
- spring: 5.3.23
- tomcat: 9.06.68
- DB
  - MariaDB: 10.2.14
    - [이슈] 기존 설치한 MySQL과 충돌
      - 포트: 3307로 변경
  - myBatis: 3.4.4

</br>

**2. mariaDB 예제 추가** </br>
- 데이터베이스 만들기(완료)
- movie 테이블 생성(완료)
- movie 테이블 예제 데이터 추가(완료)

<img src="https://user-images.githubusercontent.com/74169420/202148295-6575904b-55f2-4561-9e84-f8d1326bdad2.jpg" width="500" height="">

</br>

**3. spring, MriaDB, MyBatis 연동 및 데이터 조회** </br>
- [이슈] 한글로 인한 xml 파싱 오류
  - pom.xml에 파싱 디펜던시 추가
  - 참고: https://beautifulkim.tistory.com/480
- [이슈] XmlBeanDefinitionStoreException
  - root-context.xml에 spring-context 스키마 추가
  - 참고: https://bears25.tistory.com/99
- MVC 패턴으로 MariaDB 데이터 조회 후 웹 출력 테스트(완료)

<img src="https://user-images.githubusercontent.com/74169420/202148374-76deccc2-e284-445c-b75f-3376c558dd30.jpg" width="500" height="">


</br>

---

### 2주차 </br>
**1. 개념 학습** </br>
> 개념 정리하여 pdf 파일 작성하여 document 브랜치에 업로드
- HTTP에 대하여
- 브라우저에서 HTTP 요청 흐름
- REST API와 HTTP 메서드, HTTP 상태코드

</br>

**2. API 초안 작성해보기** </br>
> API 작성은 직무부트캠프의 전체적인 내용으로 추후에 계속 수정할 것!

>document 브랜치에 API 초안.pdf로 업로드

- 5개 통계 API 구축
  - 월별 접속자 수
  - 일자별 접속자 수
  - 평균 하루 로그인 수
  - 휴일을 제외한 로그인 수
  - 부서별 월별 로그인 수

</br>

---

### 3주차 </br>
> 스프링 부트 개발 환경 세팅 및 20년도 로그인 수 API 테스트, 통계 API 위한 SQL 작성해보기

>springBoot 브랜치에 업로드

**1. 스프링 부트 개발 환경 세팅** </br>
- 빌드 방식: Maven
- JDK: 11.0.14
- spring version: 2.2.2RELEASE
- JSP 테스트
  - pom.xml에 jasper와 jstl 디펜던시 추가
  - test.jsp 작성
    - src/main/webapp/WEB-INF/views 에 파일 생성
    <img src="https://user-images.githubusercontent.com/74169420/203818727-3c654d7d-9f89-4af5-a40d-7368d0d11f57.JPG" width="200" height="">
  - 컨트롤러 작성
  - 테스트 확인
  <img src="https://user-images.githubusercontent.com/74169420/203818947-4b6a2fbe-a3b6-4701-b2f3-cb97b747abd5.JPG" width="500" height="">

</br>

**2. 통계 API를 위한 DB 세팅** </br>
- statistic DB 생성
- requestInfo 테이블
  - 로그인, 로그아웃, 보드삭제, 보드기록 로그 기록
  <img src="https://user-images.githubusercontent.com/74169420/203819059-9490c42a-7bf5-48d6-aa47-2b50c120fe2b.JPG" width="500" height="">
- requestCode 테이블
  - 로그인, 로그아웃, 보드기록, 보드삭제
  <img src="https://user-images.githubusercontent.com/74169420/203819064-ec69d218-c635-4c82-8410-440a2f59adf3.JPG" width="500" height="">
- uesr 테이블
  - ID, 이름, 부서
  <img src="https://user-images.githubusercontent.com/74169420/203819073-518942d9-2b6b-4648-825b-6c863c164f10.JPG" width="500" height="">

</br>

**3. mybatis, mariaDB 연동 테스트 - 20년도 로그인 수 API 테스트** </br>
- 프로젝트 구조

  <img src="https://user-images.githubusercontent.com/74169420/203819261-6e766839-2fd6-40e6-924c-5a03015b9bb1.JPG" width="200" height="">
- mybatis 설정 코드
  - MybatisConfig.java
- mapper 작성
  - dao 패키지
  - StatisticMapper.java: 연도 입력하면 해시로 반환하는 인터페이스
  - statisticMapper.xml: xml 파일 통한 쿼리문
- service 작성
  - service 패키지
  - StatisticService.java: 인터페이스
  - StaticServiceImpl.java: 구현체
- controller 작성
  - test 패키지
  - settingTest.java
  - "/sqlyearStatistic" 매핑
- 테스트 화면
<img src="https://user-images.githubusercontent.com/74169420/203819838-7a5cb6fd-3d12-4c8e-bcd2-76bfdc98cbee.JPG" width="500" height="">

</br>

**4. 통계 API를 위한  SQL 작성해보기** </br>
- SW활용률 API 수정 후 업로드
  - document 브랜치 SW활용률 API.pdf 이름으로 업로드
  - 날짜 데이터 포맷 변경
  - 중복 URI 변경
- SQL 작성
  - document 브랜치 SQL 작성 폴더에 업로드
  - 월별 접속자 수, 일자별 접속자 수, 부서별 월별 로그인 수 작성
  - 추후 수정 필요

---
### 4주차 </br>
> API 문서와 DB를 참고하여 API 개발 </br> 
 코드: springBoot 브랜치 </br>
 API 문서 및 SQL 문서: document 브랜치

**1. 프로젝트 구조**

<img src="https://user-images.githubusercontent.com/74169420/205085870-159f7ce3-de13-462a-b2cc-44b6e6ab5ff0.JPG" width="200" height="">

- dto
  - LoginUser
  <img src="https://user-images.githubusercontent.com/74169420/205086406-fc6e701f-5182-48d1-b2c6-3af292741be6.JPG" width="300" height="">
  
  - MonthCnt
  <img src="https://user-images.githubusercontent.com/74169420/205086536-102aca00-b96f-4aab-89d0-2ee98cc67c0f.JPG" width="300" height="">

- dao
  - StatisticList.java: statisticList.xml 매핑
  - statisticList.xml: SW 활용률 API 개발 위한 쿼리문
- Service
  - StatisticService.java: 인터페이스
  - StatisticServiceImpl.java: 구현체, SW 활용률 API 개발 위한 서비스 로직
- Controller
  - LoginCntController.java: SW 활용률 API 개발 위한 서비스 로직, URI 매핑

</br>

**2. 월별 접속자 수 API**
- dao
  - 인터페이스
    - `public List<LoginUser> selectMonth(String month);`
    - 파라미터: month
    - 반환: LoginUesr 리스트
  - SQL
    - id : selectMonth

- service
  - `public HashMap<String,Object> monthLoginUser(String month);`
    - 파라미터: month
    - 반환: Json 데이터를 위한 HashMap
    - HashMap: 월별 접속자 수, 월, 성공여부, 접속자 리스트 받음
- controller
  - 매핑 URI: login/months
- 실행 예시
  - http://localhost:8031//login/months?month=08 
  <img src="https://user-images.githubusercontent.com/74169420/205084775-b6afd908-e06a-4813-9eb1-2d1bcaf6cb24.JPG" width="500" height="">


</br>

**3. 일자별 접속자 수 API**
- dao
  - 인터페이스
    - `public List<LoginUser> selectDay(String day);`
    - 파라미터: day
    - 반환: LoginUesr 리스트
  - SQL
    - id : selectDay

- service
  - `public HashMap<String,Object> dayLoginUser(String day);`
    - 파라미터: day
    - 반환: Json 데이터를 위한 HashMap
    - HashMap: 일별 접속자 수, 일, 성공여부, 접속자 리스트 받음
- controller
  - 매핑 URI: /login/days
- 실행 예시
  - http://localhost:8031//login/days?day=22
  <img src="https://user-images.githubusercontent.com/74169420/205084786-c890a887-6019-4466-8bb5-8e87a6e59764.JPG" width="500" height="">

</br>

**4. 평균 하루 로그인 수 API**
- dao
  - 인터페이스
    - `public int selectTotalMonth(String yearMonth);`
    - 파라미터: yearMonth
    - 반환: int
  - SQL
    - id : selectTotalMonth

- service
  - `public HashMap<String,Object> avgDayLoginCnt(String yearMonth);`
    - 파라미터: yearMonth
    - 반환: Json 데이터를 위한 HashMap
    - HashMap: 평균 하루 로그인 수, 년도 월, 성공 여부
  - 매핑 URI: login/avg 
- 실행 예시
  - http://localhost:8031/login/avg?yearMonth=2007
  <img src="https://user-images.githubusercontent.com/74169420/205084813-25c3aa54-ac25-4303-8a07-b0b56e427c2e.JPG" width="500" height="">

</br>

**5. 부서별 월별 로그인 수 API**
- dao
  - 인터페이스
    - `public List<MonthCnt> selectMonthDepartment(String department);`
    - 파라미터: department
    - 반환: MonthCnt 리스트
  - SQL
    - id : selectMonthDepartment

- service
  - `public HashMap<String,Object> monthDepartmentLoginUser(String department);`
    - 파라미터: department
    - 반환: Json 데이터를 위한 HashMap
    - HashMap: 부서, 성공여부, 월별 로그인 수 리스트
- controller
  - 매핑 URI: /login/month/departments
- 실행 예시
  - http://localhost:8031/login/months/departments?department=IT 
  <img src="https://user-images.githubusercontent.com/74169420/205084821-333cc7ad-a4bb-4d39-9828-b389cf7cf9f7.JPG" width="500" height="">

</br>

**6. 휴일을 제외한 로그인 수 API**
- 공휴일 API 받아오기
  - 공공 데이터 포털 사이트 이용
  - https://www.data.go.kr/data/15012690/openapi.do
  - 연도, 월 입력하면 공휴일 리스트 받음
- `com.devfun.settingweb_boot.API.HolidayInfoAPI.class`
  - 위 사이트 활용하여 공휴일 API 받아옴
  - 주요 기능
    - 공휴일 API 조회 후 json으로 받음
    - 받은 json 데이터 파싱 후 날짜만 추출하여 Set으로 담아 리턴
- dao
  - YYMM 포맷 날짜 String 파라미터 보내면 해당 월에 로그인한 유저 리스트 반환
  - 인터페이스
    - `public List<LoginUser> selectYearMonth(String yearMonth);`
    - 파라미터: yearMonth
    - 반환: LoginUser 리스트
  - SQL
    - id : selectYearMonth

- service
  - `public HashMap<String,Object> monthWeekdayLoginUser(String yearMonth);`
    - 파라미터: yearMonth
    - 반환: Json 데이터를 위한 HashMap
    - HashMap: 휴일을 제외한 로그인 수, 부서, 성공여부, 휴일을 제외한 로그인 유저 리스트
- controller 
  - 매핑 URI: /login/months/weekdays
- 실행 예시(22년 09월 검색)
  - DB에서 22년 09월 로그인 기록 확인
    - 4개 조회
    - 22년 9월 11일은 추석 공휴일 -> 휴일 제외한 로그인을 조회하면 이 9월 11월 데이터는 없어야 함
  <img src="https://user-images.githubusercontent.com/74169420/205426339-504b3fe2-321f-406b-b86a-3305bfe9edf8.jpg" width="500" height="">

  - 실제 테스트
    - http://localhost:8031/login/months/weekdays?yearMonth=2209 검색
    - 9월 11일을 제외한 나머지 2개 데이터만 출력 확인
  <img src="https://user-images.githubusercontent.com/74169420/205426337-27673bce-9cb5-4581-aa5f-b23d7eed010b.jpg" width="500" height="">

**7. API구축 후 API와 SQL 문서 수정**
- document 브랜치에서 확인 가능
