---
layout: post
title:  "How to make ArrayList"
categories: TLI
layout : single
---

# TLI How to make ArrayList

## 01) 인스턴스의 주소를 담을 레퍼런스 배열을 준비한다.
- size = 리스트에 들어간 레퍼런스의 갯수(1부터 시작)
- index = 배열의 순서(0부터 시작)
- .length = 배열의 길이

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;
}
```

## 02) 인스턴스를 추가하는 add() 메서드 정의.

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;

// 02
    static public boolean add(Object e) {
        elementData[size++] = e;
        return true;
    }
}
```

## 03) 특정 인덱스의 인스턴스를 리턴하는 get(int) 메서드 정의.

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;

// 02
    static public boolean add(Object e) {
        elementData[size++] = e;
        return true;
    }

// 03
    static public Object get(int index) {
        return elementData[index];
    }
}
```

## 04) 인스턴스를 특정 위치에 삽입하는 add(int, Object) 메서드 정의.

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;

// 02
    static public boolean add(Object e) {
        elementData[size++] = e;
        return true;
    }

// 03
    static public Object get(int index) {
        return elementData[index];
    }

// 04
    static public void add(int index, Object element) {
        // 마지막 레퍼런스(size)부터 index의 레퍼런스까지 그 다음 칸으로 옮겨넣는 작업을 반복한다.
        // index - 1 다음에 index를 새로 만들어 넣는 것이기 때문에 i 는 index보다 커야한다.
        for (int i = size; i > index; i--) {
            elementData[i] = elementData[i - 1];
        }
        // 지정한 인덱스에 원하는 레퍼런스를 삽입한다.
        elementData[index] = element;
        // 레퍼런스가 하나 늘어났으니 배열을 하나 늘려준다.
        size++;
    }
}
```

## 05) 특정 위치의 항목을 다른 인스턴스로 교체하는 set(int, Object) 메서드 정의.

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;

// 02
    static public boolean add(Object e) {
        elementData[size++] = e;
        return true;
    }

// 03
    static public Object get(int index) {
        return elementData[index];
    }

// 04
    static public void add(int index, Object element) {
        for (int i = size; i > index; i--) {
            elementData[i] = elementData[i - 1];
        }
        elementData[index] = element;
        size++;
    }

// 05
    static public Object set(int index, Object element) {
        // 지정한 index에 있는 값을 새로운 변수를 만들어 넣어준다.
        Object old = elementData[index];
        // 지정한 index에 새 값을 넣는다.
        elementData[index] = element;
        // old 값을 리턴한다.
        return old;
    }
}
```

## 06) 특정 위치의 항목을 제거하는 remove(int) 메서드를 정의.

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;

// 02
    static public boolean add(Object e) {
        elementData[size++] = e;
        return true;
    }

// 03
    static public Object get(int index) {
        return elementData[index];
    }

// 04
    static public void add(int index, Object element) {
        for (int i = size; i > index; i--) {
            elementData[i] = elementData[i - 1];
        }
        elementData[index] = element;
        size++;
    }

// 05
    static public Object set(int index, Object element) {
        Object old = elementData[index];
        elementData[index] = element;
        return old;
    }

// 06
    static public Object remove(int index) {
        // 지정한 index의 레퍼런스를 새 변수에 담는다.
        Object old = elementData[index];
        // index에 들어있는 레퍼런스를 지우려면 index + 1, index + 2 ... size - 1(인덱스는 0부터, 사이즈는 1부터 시작하기 때문에 사이즈에서 -1을 빼야 배열의 마지막 인덱스 번호를 구할 수 있다) 번째까지의 레퍼런스를 한칸씩 앞으로 당겨넣는다.
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        // 레퍼런스가 하나 줄었으므로 배열도 하나 줄인다.
        size--;
        return old
    }
}
```

## 07) add() 할 때 배열의 크기를 넘는 경우 배열의 크기를 늘린다.

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;

// 02 // 07
    static public boolean add(Object e) {
        // 07의 grow() 호출
        // size와 배열의 길이가 같을 경우 배열을 늘려준다.
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03
    static public Object get(int index) {
        return elementData[index];
    }

// 04
    static public void add(int index, Object element) {
        for (int i = size; i > index; i--) {
            elementData[i] = elementData[i - 1];
        }
        elementData[index] = element;
        size++;
    }

// 05
    static public Object set(int index, Object element) {
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06
    static public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
        return old
    }

// 07 - 02의 add()에서 grow() 호출
    static void grow() {
        // static 배열은 여러개 만들 수 없다.
        // 그러므로 새 배열을 만들어 기존의 배열을 복사 붙여넣기 한 다음 새 배열의 주소를 기존 배열의 주소가 들어있던 곳에 넣어준다.
        // 새 배열의 길이는 보통 기존 배열 길이의 절반을 덧붙여 만든다.
        // 비트 연산자를 쓰는 경우가 많다. (>> 1 == / 2)
        Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        // 기존의 배열을 새로운 배열에 복사 붙여넣기 한다.
        // i = index를 말한다.
        for (int i = 0; i < elementData.length; i++) {
            newArray[i] = elementData[i];
        }
        // 새 배열의 주소를 기존 배열의 주소를 넣던 곳에 넣어준다.
        elementData = newArray;
    }
}
```

## 08) add(int, Object)로 임의의 위치에 삽입할 때
- 배열의 크기가 작으면 늘린다.
- 인덱스가 유효하지 않으면 예외를 발생시킨다.

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;

// 02
    static public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03
    static public Object get(int index) {
        return elementData[index];
    }

// 04 // 08
    static public void add(int index, Object element) {
        // 배열을 늘린다.
        if (size == elementData.length) {
            grow();
        }
        // index의 범위를 지정하고 예외 발생시킨다.
        if (index < 0 || index > size) {
            throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        for (int i = size; i > index; i--) {
            elementData[i] = elementData[i - 1];
        }
        elementData[index] = element;
        size++;
    }

// 05
    static public Object set(int index, Object element) {
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06
    static public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
        return old
    }

// 07 
    static void grow() {
        Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        for (int i = 0; i < elementData.length; i++) {
            newArray[i] = elementData[i];
        }
        elementData = newArray;
    }
}
```

## 09) get(int)으로 유효하지 않은 인덱스의 값을 꺼낼 때 예외를 발생시킨다.

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;

// 02
    static public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09
    static public Object get(int index) {
        // index의 범위를 지정
        // size는 index보다 1이 크기 때문에 index가 size 보다 크거나 같으면 범위를 벗어난다.
        // 예: size가 12345 일 때 index는 01234 이다.
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08
    static public void add(int index, Object element) {
        if (size == elementData.length) {
            grow();
        }
        if (index < 0 || index > size) {
            throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        for (int i = size; i > index; i--) {
            elementData[i] = elementData[i - 1];
        }
        elementData[index] = element;
        size++;
    }

// 05
    static public Object set(int index, Object element) {
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10
    static public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
        return old
    }

// 07 
    static void grow() {
        Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        for (int i = 0; i < elementData.length; i++) {
            newArray[i] = elementData[i];
        }
        elementData = newArray;
    }
}
```

## 10) remove()를 수행한 다음 맨 끝에 남아있는 주소를 null로 설정하여 인스턴스의 레퍼런스 카운트를 한 개 줄인다.

```java
public class MyArrayList {
// 01
    static Object[] elementData = new Object[5];
    static int size;

// 02
    static public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09
    static public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08
    static public void add(int index, Object element) {
        if (size == elementData.length) {
            grow();
        }
        if (index < 0 || index > size) {
            throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        for (int i = size; i > index; i--) {
            elementData[i] = elementData[i - 1];
        }
        elementData[index] = element;
        size++;
    }

// 05
    static public Object set(int index, Object element) {
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10
    static public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;

        // 쓰지않는 인스턴스의 주소를 제거하여 가비지가 될 수 있게 한다.
        elementData[size] = null;
        return old
    }

// 07 
    static void grow() {
        Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        for (int i = 0; i < elementData.length; i++) {
            newArray[i] = elementData[i];
        }
        elementData = newArray;
    }
}
```