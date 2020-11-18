---
layout: post
title:  "Regular Expression 01"
categories: Regular Expression
layout : single
toc : true 
toc_sticky : true
---

# 정규표현식

## 생활코딩

- Source : 

    - Case 1 : 
        - Regular Expression : 
            - First match : 
            - All match : 

    - Case 2 : 
        - Regular Expression : 
            - First match : 
            - All match : 

    - Case 3 : 
        - Regular Expression : 
            - First match : 
            - All match : 

    - Case 4 : 
        - Regular Expression : 
            - First match : 
            - All match : 

    - Case 5 : 
        - Regular Expression : 
            - First match : 
            - All match : 

    - Case 6 : 
        - Regular Expression : 
            - First match : 
            - All match : 

### 정규표현식의 패턴들 3~4) 위치와 이스케이핑
- Source : who is who

- Case 1 : ^ : 문자열이 시작되는 소스 상의 위치를 표현한다.
    - Regular Expression : ^who
        - First match : `who` is who
        - All match : `who` is who

- Case 2 : $ : 문자열이 끝나는 소스 상의 위치를 표현한다.
    - Regular Expression : who$
        - First match : who is `who`
        - All match : who is `who`

- Source : $12$ \-\ $25$

    - Case 1 : $로 시작하는 텍스트를 찾겠다.
        - Regular Expression : ^$
            - First match : $12$ \-\ $25$
            - All match : $12$ \-\ $25$
                - 작동하지 않는다.
                - 왜냐하면 $가 문자열의 끝을 의미하는 특수한 기호이기 때문에 
                    - 그렇다면 어떻게 $를 선택할 수 있을까.

    - Case 2 : 정규 표현식에서 의미가 있는 문자가 아니라 단순한 문자로 바꿔주는 역할을 \ 가 한다.
        - Regular Expression : \$ <- 문자 달러가 되는 것.
            - First match : `$`12$ \-\ $25$
            - All match : `$`12`$` \-\ `$`25`$`
                - \ 를 이스케이프 문자라고 한다.
                    - 어떤 역할이 있던 문자를 역할로부터 탈출시켜 주는 것을 의미한다.

    - Case 3 : 문자 달러가 맨 처음 시작되는 위치에 있는 것을 찾는다.
        - Regular Expression : ^\$
            - First match : `$`12$ \-\ $25$
            - All match : `$`12$ \-\ $25$

    - Case 4 :
        - Regular Expression : \$$
            - First match : $12$ \-\ $25`$`
            - All match : $12$ \-\ $25`$`

    - Case 5 : 이스케이프 문자가 뒤의 문자의 역할을 해지시킨다.
        - Regular Expression : \\
            - First match : $12$ `\`-\ $25$
            - All match : $12$ `\`-`\` $25$

### 정규표현식의 패턴들 5~6) 모든 문자

#### 5 : Point . matchtes any character
- Source : Regular expressions are powerful!!!

    - Case 1 : 어떠한 공백, 특수문자건 관계없이 모든 것을 가리키는 것
        - Regular Expression : .
            - First match : `R`egular expressions are powerful!!!
            - All match : `Regular expressions are powerful!!!`

    - Case 2 : : 어떤 문자든 상관없이 6개의 문자를 가지고 있는 것, 문자 6개를 한 덩어리로 엮어서 나누다 보니 마지막은 5개라서 선택되지 않는다.
        - Regular Expression : ......
            - First match : `Regula`r expressions are powerful!!!
            - All match : `Regular expressions are powerf`ul!!!
                - Regula/r expr/ession/s are /powerf / ul!!!

#### 6 : The point must be escaped if literal meaning is required
- Source : O.K.

    - Case 1 : 
        - Regular Expression : .
            - First match : `O`.K.
            - All match : `O.K.`

    - Case 2 : 
        - Regular Expression : \. 
            - First match : O`.`K.
            - All match : O`.`K`.`

    - Case 3 : 이스케이프 문자. anyChar 이스케이프 문자.
        - Regular Expression : \..\.
            - First match : O`.K.`
            - All match : O`.K.`
