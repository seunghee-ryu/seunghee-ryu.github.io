# mysql zip 설치 방법

- mysql 5.7.34 zip 파일을 다운받는다
  - https://dev.mysql.com/downloads/mysql/5.7.html?tpl=version&amp;os=src&amp;version=5.7

- 파일 압축을 풀어 C:\에 위치시킨다

- 메모장으로 my.ini 파일을 만든다.
  - 안에 아래 내용을 적는다.
  - [mysqld]

    # set basedir to your installation 
    basedir=C:\mysql-5.7.34-winx64

    # set datadir to the location of your data directory
    datadir=C:\mysql-5.7.34-winx64/data

    port=3306
  - 다른 이름으로 저장을 누르고 인코딩을 ANSI로 변경한다.
    
- 명령 프롬프트를 관리자 모드로 실행한다.
  - C:\mysql-5.7.34-winx64>cd bin 로 이동한다.

- mysqld.exe --install 명령어를 실행한다.
  - C:\mysql-5.7.34-winx64\bin>mysqld.exe --install
    Service successfully installed.

- net start mysql 명령어를 실행한다.
  - C:\mysql-5.7.34-winx64\bin>net start mysql
    MySQL 서비스를 시작합니다..
    MySQL 서비스가 잘 시작되었습니다.
    
- data 폴더가 생성되었으면 그 안의 DESKTOP_NAME-DRVVOPF를 메모장으로 연다.
  - 임시 비밀번호를 확인한다.
    - 2021-06-22T03:16:16.630822Z 1 [Note] A temporary password is generated for root@localhost: 임시비밀번호

- 임시 비밀번호를 사용하여 mysql의 루트 관리자로 접속한다.
  - C:\mysql-5.7.34-winx64\bin>mysql -u root -p
    Enter password: ************
    Welcome to the MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 3
    Server version: 5.7.34

    Copyright (c) 2000, 2021, Oracle and/or its affiliates.

    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' to clear the current input statement. 
    
- 비밀번호를 변경한다.
  - mysql> alter user 'root'@'localhost' identified by '비밀번호';
    Query OK, 0 rows affected (0.00 sec)
    
- 버전을 확인한다.
  - mysql> select version();
    +-----------+
    | version() |
    +-----------+
    | 5.7.34    |
    +-----------+
    1 row in set (0.00 sec)
