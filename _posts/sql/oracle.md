---
layout: post
title:  "Oracle 생활코딩"
categories: Sql
layout : single
toc : true 
toc_sticky : true
---

# 사용자와 스키마
- 스키마란?
  - 여러개의 테이블이 있을 때 연관된 것끼리 묶을 수 있도록 하는 체계
  - 연관된 표들을 그룹핑하는 체계
- 사용자
  - 사용자를 생성하면 그 사용자가 사용하는 스키마가 생성된다
  
# 사용자 생성
- sql plus 실행
- 관리자 권한으로 생성해야 한다.
  - sys as sysdba (관리자 권한)
  - 비밀번호 없이 엔터
    - 관리자로 접속
    - 사용자 생성
      - 구글 검색 oracle sql  reference create user
      - 오라클 공식 문서 (매뉴얼)
      - 네모 : 키워드 (그대로 써야한다)
      - 타원 : 바꿔야 할 내용
 - 유저 생성 = 스키마가 생성되었다고 보면 된다
 - 유저 생성 후 권한을 줘야한다
 
 # 사용자 권한 부여
 - 관리자로 권한 부여해야 한다
 - GRANT DBA TO username; 
   - 모든 권한을 주는 명령어
 - 유저로 접속
 
 # 표 만드는 방법
 - create table sql references oracle
 - 열(세로) : 컬럼 (id, title, description, created 등)
 - 행(가로) : 정보 1건 1건
 - CREATE TABLE topic (
    id NUMBER NOT NULL,
    title VARCHAR2(50) NOT NULL,
    description VARCHAR(4000),
    created DATE NOT NULL
    );
    - topic 은 table name 이다(변경가능)
    - 첫번째 : 데이터 타입
      - NUMBER 는 데이터 타입이다
      - 데이터 타입이 없으면 넣고 뺄때마다 데이터가 숫자인지 아닌지를 확인해야 한다
    - 두번째 : 반드시 있어야 하는지 아닌지
      - null 이냐 not null 이냐
      - null 일때는 적지 않아도 된다

# 행 추가
- INSERT INTO topic
  (id, title, description,created)
  VALUES
  (1,'ORACLE, NULL, SYSDATE);
  - SYSDATE를 사용하면 입력 당시의 시간이 저장된다
- commit; 을 해줘야 반영이 된다
  - 트랜잭션이라는 개념과 괸련이 있다
 
# SQL
- 데이터베이스 시스템은 명령어롤 통해 제어할 수 있기 때문에 자동화가 가능해진다
 
# 행 읽기
- SELECT * FROM topic;
  - 모든 행을 가져온다
- SELECT id, title, created FROM topic;
  - 컬럼을 제한하는 방법
- SELECT * FROM topic WHERE id = 1;
  - 아이디가 1인 데이터만 볼 수 있다
- SELECT * FROM topic WHERE id > 1;
  - 아이디가 1인 데이터를 제외하고 볼 수 있다
- SELECT id, title, created FROM topic WHERE id = 1;
  - 아이디가 1인 데이터의 id, title, created를 볼 수 있다
- SELECT * FROM topic ORDER BY id DESC;
  - 정렬을 할 수 있다(id를 기준으로 정렬을 하는데 큰 숫자가 먼저 나오도록 한다 반대는 asc)
- SELECT * FROM topic 
    OFFSET 1 ROWS
    FETCH NEXT 2 ROWS ONLY;
  - 원하는 행만 가져오는 행위를 페이징이라고 한다
    - OFFSET 은 어느 열부터 가져올 것인가를 정한다
    - FETCH 는 몇개를 가져올 것인가를 정한다
  - 위 sql의 결과로는 0번째 이후의 첫번째 행부터 2개를 가져오게 된다 

# 행 수정 & 삭제
- UPDATE topic SET title='MSSQL', description = 'MSSQL is ...' WHERE id = 3;
  - 컬럼의 아이디 값이 3인 행을 업데이트 하게 된다
- DELETE from topic WHERE id = 3;
  - 컬럼의 아이디 값이 3인 행을 삭제한다
 
 # PRIMARY KEY
 - 중복되지 않도록 식별해주는 식별자
 - CREATE TABLE topic (
    id NUMBER NOT NULL,
    title VARCHAR2(50) NOT NULL,
    description VARCHAR(4000),
    created DATE NOT NULL,
    CONSTRAINT PK_TOPIC PRIMARY KEY(id)
    );
- id 를 프라이머리 키로 지정
- 동일한 id를 가지는 데이터는 등록이 불가능하다
    
# SEQUENCE
- CREATE SEQUENCE SEQ_TOPIC;
- 시퀀스를 생성
- 시퀀스를 사용해서 자동으로 1씩 증가하는 패턴을 만들 수 있다
- INSESRT INTO topic (id, title, description, created)
  VALUES
  (SEQ_TOPIC_NEXTVAL, 'MongoDB', 'MongoDB is ...', SYSDATE);
- 결과적으로 id 값은 1씩 증가하는 PRIMARY KEY를 가지게 된다
- 가지고 있는 시퀀스 값을 알고 싶을때는
  - SELECT SEQ_TOPIC.CURRVAL FROM topic;
  
# 서버와 클라이언트
- 네트워크에 연결된 각각의 컴퓨터는 host 라고 한다
- 정보를 요청하는 컴퓨터와 정보를 응답하는 컴퓨터가 있다
  - 역할에 따라 부르는 표현이 달라진다
  - client 와 server
  - 요청하는 쪽이 클라이언트, 응답하는 쪽이 서버

