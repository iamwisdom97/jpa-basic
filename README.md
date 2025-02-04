# 자바 ORM 표준 JPA 프로그래밍 - 기본편

## JPA 시작하기  
- H2 database 실행 
- 라이브러리 셋팅
- persistence.xml 에 대해
- JPA는 항상 하나씩 EntityMangerFactory 띄워서 돌아간다.
- JPA는 요청이 올때마다 EntityManger 를 통해서 작업해야한다.
- JPA는 데이터 변경은 트랜잭션 안에서 일어나야 한다.
- commit 필수!
- 자원을 다 쓰면 닫아줘야 한다.
- was가 내려가면 EntityManagerFactory 를 닫아줘야한다.

## 영속성 관리 - 내부 동작 방식
- JPA에서 가장 중요한 2 가지
  - 객체와 관게형 데이터베이스 매핑하기
  - 영속성 컨텍스트 : 엔티티를 영구 저장하는 환경, 눈에 보이지 않는다.
- 엔티티 생명주기
  - 비영속, 영속, 준영속, 삭제
- 영속성 컨텍스트 장점
  - 1차 캐시(한 번 조회한거 또 한번 쿼리에서 조회하지 않음)
  - 동일성 보장
  - 트랜잭션을 지원하는 쓰기 지연
  - 변경 감지(update 자동 인식)
  - 지연 로딩(쿼리를 나중에 날림)
- 플러시 
  - 커밋이나 쿼리를 실행할 때 플러시(내가 직접 플러시 할 수 있다.)
  - 영속성 컨텍스트를 비우지 않음
  - 영속성 컨텍스트의 변경내용을 데이터베이스에 동기화
  - 트랜잭션이라는 작업 단위가 중요 -> 커밋 직전에만 동기화 하면 됨

## 엔티티 매핑
- @Entity 가 붙은 클래스는 JPA가 관리 -> 엔티티라 한다.
- 데이터베이스 스키마 자동 생성
  - DDL을 애플리케이션 실행 시점에 자동 생성
  - 테이블 중심 -> 객체 중심 
  - 데이터베애스 방언을 활용해서 데이터베이스에 맞는 적절한 DDL 생성
- 속성
  - create : 기존테이블 삭제 후 다시 생성 (DROP + CREATE)
  - create-drop : create와 같으나 종료시점에 테이블 DROP
  - update : 변경분만 반영(운영DB에는 사용하면 안됨)
  - validate : 엔티티와 테이블이 정상 매핑되었는지만 확인
  - none : 사용하지 않음
- 매핑 어노테이션 정리
  - @Column : 컬럼 매핑
  - @Temporal : 날짜 타입 매핑
  - @Enumerated : enum 타입 매핑 (ORIGINAL 사용x)
  - @Lob : BLOB, CLOB 매핑
  - @Transient : 특정 필드를 컬럼에 매팡히자 않음(매핑 무시)
- 기본 키 매핑
  - IDENTITY 전략 특징
    - 기본 키 생성을 데이터베이스에 위임
    - 주로 MySQL, PostgreSQL, SQL Server, DB2에서 사용
    - JPA는 보통 트랜잭션 커밋 시점에 INSERT SQL 실행
    - AUTO_INCREMENT는 데이터베이스에 INSERT SQL을 실행한 이후에 ID 값을 알 수 있음
    - IDENTITY 전략은 em.persist() 시점에 즉시 INSERT SQL 실행하고 DB에서 식별자를 조회
  - TABLE 전략
    - 키 생성 전용 테이블을 하나 만들어서 데이터베이스 시퀀스를 흉내내는 전략
    - 장점 : 모든 데이터베이스에 적용 가능
    - 단점 : 성능
  - 권장하는 식별자 전략
    - 기본 키 제약조건 : null 아님, 유일, 변하면 안된다.
    - 미래까지 이 조건을 만족하는 자연키는 찾기 어렵다. 대리키(대체키)를 사용하자.
    - 예를 들어 주민등록번호도 기본 키로 적절하지 않다.
    - 권장 : Long형 + 대체키 + 키 생성전략 사용
















