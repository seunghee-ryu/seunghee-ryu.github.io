---
layout: post
title: JavaAlgorithm02
categories: JavaAlgorithm
layout : single
toc : true 
toc_sticky : true
---

# 02 기본 자료구조

## 02-1배열

### 자료구조

- 데이터 단위와 데이터 자체 사이의 물리적 또는 논리적인 관계.
- 데이터 단위는 데이터를 구성하는 한 덩어리.
- 자료구조는 자료를 효율적으로 이용할 수 있도록 컴퓨터에 저장하는 방법.



### 배열

- 같은 자료형의 변수로 이루어진 구성 요소가 모인 것.
- 배열 구성 요소의 자료형은 어떤 형이든 상관없다.

```
int[] a; // a는 자료형이 int 형인 배열 - 형식 A
int a[]; // a는 자료형이 int 형인 배열 - 형식 B
// 형식 A쪽이 많이 사용된다.

a = new int[5]; // a는 길이가 5일 배열을 참조한다.
```



### 구성요소

- 배열의 개별 요소에 접근하기 위해 사용하는 것이 연산자 [] 안에 넣는 정수형 인덱스이다.
- 첫번째 배열 요소의 인덱스는 0으로 정해져 있다.
- 배열 변수 이름[인덱스]



### 구성 요솟수(길이)

- 배열의 구성 요솟수는 배열의 길이를 말한다.
- 배열 변수 이름.length



### 기본값

- 배열의 구성 요소는 자동으로 0으로 초기화된다.



### 초기화

- 배열 초기화를 사용하면 배열 본체의 생성과 동시에 각 요소의 초기화가 가능하다.

```
int[] a = {1, 2, 3, 4, 5}; // 배열 초기자에 의해 생성

// new 연산자를 사용하면 좀 더 명확하게 선언할 수 있다.
int[] a = new int[] {1, 2, 3, 4, 5}; // 배열 초기자에 의해 생성
```



### 배열의 복제

- Clone 메서드를 호출하면 쉽게 만들 수 있다.

- 배열이름.clone()



### 배열 요소의 최댓값

```
max = a[0];

for (i = 1; i < n; i++;)
	if (a[i] > max) max = a[i];
```

- 배열의 요소를 하나씩 차례로 살펴보는 과정을 알고리즘 용어로 주사라고 한다.



### 난수를 사용해 배열의 요솟값 설정하기

- 배열의 요소에 값을 하나씩 입력하는 것이 귀찮을 경우 각 요소에 난수를 대입하면 된다.

- 난수를 생성할 때 random 클래스를 사용한다.

```
inport java.util.Random;
// 배열 요소의 최댓값을 나타낸다(값을 난수로 생성)

Class MaxOfArrayRand {
	// 배열 a의 최댓값을 구하여 반환하는 메서드
}

public static void main(String[] args) {

	Random rand = new Random();
	
	int num = stdIn.nextInt(); // 배열의 요솟수를 입력 받음
	
	int[] height = new int[num];
	
	for (int i = 0; i < num; i++) {
		height[i] = 100 + rand.nextInt(90); // 요소의 값을 난수로 결정
		}
}
```

- nextInt(n)가 반환하는 것은 0부터 n-1 까지의 난수이다.
- 컴퓨터에 의해 생성된 것은 의사 난수이다.(실제 난수가 아니고 난수와 유사한 난수이다.)



### 배열 요소를 역순으로 정렬하기

- 교환 횟수는 요소개수/2
  - 나눗셈에서 나머지는 버린다.
    - 가운데 요소는 교환할 필요가 없기 때문이다.

```
// 요소 개수가 n개인 배열 요소를 역순으로 정렬하는 알고리즘
for(i = 0; i < n / 2; i++) // a[i]와 a[n - i - 1]의 값을 교환
```



### 두 값의 교환

- 요소 교환이 총 n/2회 필요하다.
- 교환을 위해 자료형을 가진 변수t를 하나 더 사용한다.
  - t = x; - x값을 t에 보관
  - x = y; - y값을 x에 대입
  - y = t; - t에 보관한 처음 x 값을 y에 대입



### 두 배열의 비교

- 판단은 세 단계로 수행한다.
  - 두 배열 a, b의 요솟수[길이]를 비교한다.
  - 두 배열을 for문으로 처음부터 스캔하면서 요소 a[i]와 b[i]의 값을 비교하는 것을 반복한다.
  - 프로그램의 흐름이 끝까지 도달하면 true를 반환하고 중간에 멈출 경우는 false를 반환한다.



### 기수 변환

- 정숫값을 임의의 기수로 변환하는 알고리즘.

  - 10진수 정수를 n진수 정수로 변환하려면 정수를 n으로 나눈 나머지를 구하는 동시에 그 몫에 대해 나눗셈을 반복해야 한다. 이 과정을 몫이 0이 될 때까지 반복하고, 이런 과정으로 구한 나머지를 거꾸로 늘어놓은 숫자가 기수로 변환한 숫자이다.

```
// 입력 받은 10진수를 2진수 ~ 36진수로 기수 변환하여 나타냄
Class CardConRev {

	static int cardConvR(int x, int r, char[] d) {
	// 정숫값 x를 r진수로 변환하여 배열 d에 아랫자리부터 넣어두고 자릿수를 반환한다.
		int digits = 0; // 변환 후의 자릿수
		String dchar = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";
		
		do {
			d[digits++] = dchar.charAt(x % r); // r로 나눈 나머지를 저장
			x /= r;
		} while (x != 0);
		return digits;
	}
```



### 소수의 나열

- 2부터 n-1까지의 어떤 정수로도 나누어 떨어지지 않으면 소수이다.
- 나누어 떨어지는 정수가 하나 이상 존재하면 그 수는 합성수이다.

```
for (int n = 2; n ,= 1000; n++) {
	int i;
	for (i = 2; i < n; i++) {
		counter++;
		if (n % i == 0) // 나누어 떨어지면 소수가 아님
    	break; // 더 이상의 반복은 불필요
    }
    if (n == i) // 마지막까지 나누어 떨어지지 않음
  }
}
```



- 3이 소수인지 아닌지 판단하는 과정

```
int counter = 0; // 나눗셈의 횟수
    int ptr = 0; // 찾은 소수의 개수
    int[] prime = new int[500]; // 소수를 저장하는 배열
    
    prime[ptr++] = 2;
    
    for (int n = 3; n < 1000; n +=2) {
      int i;
      for (i = 1; i < ptr; i++) {
        counter++;
        if (n % prime[i] == 0)
          break;
      }
      if (ptr == i) // 마지막까지 나누어떨어지지 않음
        prime[ptr++] = n; // 소수라고 배열에 저장
    }
    
    for (int i = 0; i < ptr; i++) 
      System.out.println(prime[i]);
    
    System.out.println("나눗셈을 수행한 횟수: " + counter);
  }
```

- 같은 답을 얻는 알고리즘은 하나가 아니다.
- 빠른 알고리즘은 메모리를 많이 요구한다.



- n의 제곱근을 구하는 것보다 제곱을 구하는 것이 간단하고 편할 때

```
int counter = 0; // 곱셈과 나눗셈의 횟수
    int ptr = 0; // 찾은 소수의 개수
    int[] prime = new int[500]; // 소수를 저장하는 배열
    
    prime[ptr++] = 2; // 2는 소수
    prime[ptr++] = 3; // 3은 소수
    
    for (int n = 5; n < 1000; n+= 2) { // 대상은 홀수만
      boolean flag = false;
      for (int i = 1; prime[i] * prime[i] <= n; i++) {
        System.out.println(n);
        counter+=2; //곱셈 + 나눗셈 연산 수행 
        if (n % prime[i] == 0) { // 나누어 떨어지면 소수가 아님
          flag = true;
          break; // 더이상의 반복은 불필요
        }
      }
      if (!flag) { // 마지막까지 나누어 떨어지지 않음
        prime[ptr++] = n; // 소수라고 배열에 저장
        counter++; // 안쪽 for문 본문으로 들어가지 않으므로 곱셈이 수행횟수에 포함X
      }
    }
    
    for (int i = 0; i < ptr; i++) // 찾은 ptr개의 소수를 출력
      System.out.println(prime[i]);
    System.out.println("나눗셈을 수행한 횟수: " + counter);
  }
```



### 다차원배열

- 배열을 구성 요소로 하는 것이 2차원 배열이며 2차원 배열을 구성 요소로 하는 것이 3차원 배열이다.
- 1차원 배열과 구별하기 위해 다차원 배열이라고 한다.

```
int[][] x = new int[2][4];
```

- 2행 4열의 2차원 배열 x는 가로와 세로로 행과 열이 늘어선 표와 같은 모양의 이미지임을 알 수 있다.
- 2차원 배열 안의 각 요소는 []를 2중으로 적용한 식 `x[i][j]`로 접근한다.
- 그런데 엄밀히 말해 Java에는 다차원 배열이 없다.
  - 2차원 배열을 배열의 배열로 생각하고 3차원 배열을 배열의 배열의 배열로 생각하기 때문이다.



### 한 해의 경과 일 수를 계산하는 프로그램

```
public class DayOfYear {
  static int[][] mdays = {
      {31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31},
      {31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31}
  };
  
  // 서기 year년은 윤년인가?
  static int isLeap(int year) {
    return (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) ? 1 : 0;
  }
  
  static int dayOfYear(int y, int m, int d) {
    int days = d;
    for (int i = 0; i < m; i++) 
      days += mdays[isLeap()][i - 1];
    return days;
  }
  
  public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    int retry;
    
    System.out.println("그 해의 경과 일수를 구합니다.");
    
    do {
      System.out.print("년? ");
      int year = sc.nextInt();
      System.out.print("월? ");
      int month = sc.nextInt();
      System.out.print("일? ");
      int day = sc.nextInt();
      
      System.out.printf("%s일이 경과되었습니다.", dayOfYear(year, month, day));
      System.out.println("다시 하시겠습니까? (예: 1 | 아니오: 0");
      retry = sc.nextInt();
    } while (retry == 1);
  }
}
```



### 배열에 관한 보충

- 배열의 접근은 모두 런타임(실행 시)에 검사된다.
- 배열 요솟수는 0이어도 된다. 빈 배열이라고 부른다.
- 배열 초기화는 마지막 요소에 대한 초기화 뒤에 “추가로” 쉼표를 넣을 수 있따.
  - int[] a = {1, 2, 3, 4,}
- 확장된 for문은 배열의 스캔을 매우 간단하게 구현할 수 있다.
  - for (double i : a) {}
  - 콜론(:)d은 “~의 안에 있는”이라는 뜻이다.
  - 그래서 확장 for문을 for-in문/for-each문이라고도 부른다.
  - 여기서 변수 i는 인덱스를 나타내는 것이 아니라 double 형 실수의 값인 스캔할 때 주목하고 있는 요소를 나타낸다.
  - 배열의 길이를 조사하는 수고를 덜 수 있다.
  - iterator와 같은 방법으로 스캔할 수 있다.
  - 배열의 모든 요소를 스캔하는 과정에서 인덱스 자체의 값이 필요하지 않으면 그 스캔은 확장 for문에 의해 구현하는 것이 좋다.
- 다차원 배열의 복제는 최상위 1레벨만 수행한다.





## 02-2클래스

- 임의의 데이터형을 자유로이 조합하여 만들 수 있는 자료 구조.
- 한 사람의 데이터를 저장할 때 개인의 데이터가 같은 인덱스에 저장되는 관계가 프로그램에 직접 나타나지 않는다.



### 클래스의 배열

- 사람들의 신체검사 데이터를 보여줄 때, 신체검사 데이터를 따로따로인 배열의 모임이 아닌 클래스의 배열로 구현한 프로그램.

```
// 신체검사 데이터용 클래스 배열에서 평균 키와 시력의 분포를 구함.
public class PhysicalExamination {
  
  // 시력 분포(0.0에서 0.1단위로 21개)
  static final int VMAX = 21;
  
  static class PhyscData {
    String name;
    int height;
    double vision;
    
    //생성자
    PhyscData(String name, int height, double vision) {
      this.name = name;
      this.height = height;
      this.vision = vision;
    }
    
  }
  
  // 키의 평균값
  static double aveHeight(PhyscData[] dat) {
    double sum = 0;
    for (int i = 0; i < dat.length; i++) {
      sum += dat[i].height;
    }
    return sum/dat.length;
   }
  
  // 시력 분포 
  static void distVision(PhyscData[] dat, int[] dist) {
    int i = 0;
    dist[i] = 0;
    for (i = 0; i < dat.length; i++) {
      if (dat[i].vision >= 0.0 && dat[i].vision <= VMAX / 10.0)
        dist[(int)dat[i].vision*10]++;
    }
  }
  
  public static void main(String[] args)  {
    Scanner sc = new Scanner(System.in);
    PhyscData[] x = { 
        new PhyscData("박현규", 162, 0.3),
        new PhyscData("함진아", 173, 0.7),
        new PhyscData("최윤미", 175, 2.0),
        new PhyscData("홍연의", 171, 1.5),
        new PhyscData("이수진", 168, 0.4),
        new PhyscData("김용준", 174, 1.2),
        new PhyscData("박용규", 169, 0.8),
    };
    int[] vdist = new int[VMAX]; // 시력 분포.
    
    System.out.println("신체검사 리스트");
    System.out.println("이름   키    시력");
    System.out.println("----------------");
    for (int i = 0; i < x.length; i++)
      System.out.printf("%-8s%3d%5.1f\n",
         x[i].name, x[i].height, x[i].vision);
    System.out.printf("\n평균키: %5.1fcm\n", aveHeight(x));
    
    distVision(x, vdist); // 시력 분포를 구함.
    
    System.out.println("\n시력분포");
    for (int i = 0; i < VMAX; i++)
      System.out.printf("%3.1f ~ : %2d명\n", i/10.0, vdist[i]);
    
  } 
}
```