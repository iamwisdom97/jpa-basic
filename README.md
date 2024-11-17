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