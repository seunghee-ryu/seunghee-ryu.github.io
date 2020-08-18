---
layout: post
title:  "How to make ArrayList02"
categories: TLI
layout : single
---
# TLI How to make ArrayList02

## 11) set()을 호출할 때 인덱스가 유효하지 않으면 예외를 발생시킨다.

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

// 05 // 11
    static public Object set(int index, Object element) {
        // index의 범위를 지정
        // size는 index보다 1이 크기 때문에 index가 size 보다 크거나 같으면 범위를 벗어난다.
        // 예: size가 12345 일 때 index는 01234 이다.
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
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

## 12) 여러개의 목록을 동시에 관리할 수 있도록 MyArrayList에 선언된 레퍼런스 배열을 스태틱 대신 인스턴스로 전환한다.
- 개별적으로 관리해야 할 데이터는 인스턴스 변수를 사용해야 한다.

```java
public class MyArrayList {
// 01 // 12
    Object[] elementData = new Object[5];
    int size;

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12
    public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
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

## 13) 캡슐화를 적용하여 공개할 멤버와 공개하지 말아야 할 멤버를 구분한다.

```java
public class MyArrayList {
// 01 // 12 // 13
    private Object[] elementData = new Object[5];
    private int size;

// 13 
    // size에 직접적으로 접속할 수 없으니 생성자를 만들어 준다.
    public int size() {
        return this.size;
    }

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12
    public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
        elementData[size] = null;
        return old
    }

// 07 // 13
    private static void grow() {
        Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        for (int i = 0; i < elementData.length; i++) {
            newArray[i] = elementData[i];
        }
        elementData = newArray;
    }
}
```

## 14) ArrayList 인스턴스를 생성할 때 배열의 초기 크기를 설정할 수 있도록 생성자를 추가한다.

```java
public class MyArrayList {
// 01 // 12 // 13 // 14
    private Object[] elementData;
    private int size;

// 14
    public MyArrayList() {
        elementData = new Object[5];
    }

// 13 
    public int size() {
        return this.size;
    }

// 14 
    public MyArrayList(int initialCapacity) {
        elementData = new Object[initialCapacity];
    }

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12
    public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
        elementData[size] = null;
        return old
    }

// 07 // 13
    private static void grow() {
        Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        for (int i = 0; i < elementData.length; i++) {
            newArray[i] = elementData[i];
        }
        elementData = newArray;
    }
}
```

## 15) ArrayList 인스턴스를 생성할 때 초기 크기를 지정하지 않고 생성할 수 있도록 기본 생성자를 추가한다.

```java
public class MyArrayList {
// 01 // 12 // 13 // 15
    private Object[] elementData;
    private int size;

// 13 
    public int size() {
        return this.size;
    }

// 14 
    public MyArrayList(int initialCapacity) {
        elementData = new Object[initialCapacity];
    }

// 15
    public MyArrayList() {
        elementData = new Object[5];
    }

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12
    public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
        elementData[size] = null;
        return old
    }

// 07 // 13
    private static void grow() {
        Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        for (int i = 0; i < elementData.length; i++) {
            newArray[i] = elementData[i];
        }
        elementData = newArray;
    }
}
```

## 16) 배열 크기를 지정할 때 기본 크기보다 큰 값이 되도록 생성자를 변경한다. (기본 크기를 5로 가정)

```java
public class MyArrayList {
// 01 // 12 // 13 // 15
    private Object[] elementData;
    private int size;

// 13 
    public int size() {
        return this.size;
    }

// 14 // 16
    public MyArrayList(int initialCapacity) {
        // 기본 크기보다 size가 작으면 배열을 기본 크기만큼만 만들고
        if (initialCapacity < 5) {
            elementData = new Object[5];
        // 그 외에는 size 만큼 배열을 만든다.
        } else {
            elementData = new Object[initialCapacity];
        }
    }

// 15
    public MyArrayList() {
        elementData = new Object[5];
    }

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12
    public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
        elementData[size] = null;
        return old
    }

// 07 // 13
    private static void grow() {
        Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        for (int i = 0; i < elementData.length; i++) {
            newArray[i] = elementData[i];
        }
        elementData = newArray;
    }
}
```

## 17) 배열의 기본 크기를 직접 숫자로 지정하지 말고 상수를 사용하여 지정한다.

```java
public class MyArrayList {
// 17
    private static final int DEFAULT_CAPACITY = 5;

// 01 // 12 // 13 // 15
    private Object[] elementData;
    private int size;

// 13 
    public int size() {
        return this.size;
    }

// 14 // 16 // 17
    public MyArrayList(int initialCapacity) {
        if (initialCapacity < DEFAULT_CAPACITY) {
            elementData = new Object[DEFAULT_CAPACITY];
        } else {
            elementData = new Object[initialCapacity];
        }
    }

// 15 // 17
    public MyArrayList() {
        elementData = new Object[DEFAULT_CAPACITY];
    }

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12
    public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
        elementData[size] = null;
        return old
    }

// 07 // 13
    private static void grow() {
        Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        for (int i = 0; i < elementData.length; i++) {
            newArray[i] = elementData[i];
        }
        elementData = newArray;
    }
}
```

## 18) 배열의 크기를 늘릴 때 자바에서 제공하는 Arrays를 사용하여 처리한다.

```java
public class MyArrayList {
// 17
    private static final int DEFAULT_CAPACITY = 5;

// 01 // 12 // 13 // 15
    private Object[] elementData;
    private int size;

// 13 
    public int size() {
        return this.size;
    }

// 14 // 16 // 17
    public MyArrayList(int initialCapacity) {
        if (initialCapacity < DEFAULT_CAPACITY) {
            elementData = new Object[DEFAULT_CAPACITY];
        } else {
            elementData = new Object[initialCapacity];
        }
    }

// 15 // 17
    public MyArrayList() {
        elementData = new Object[DEFAULT_CAPACITY];
    }

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12
    public Object remove(int index) {
        Object old = elementData[index];
        for (int i = index; i < size - 1; i++) {
            elementData[i] = elementData[i +1];
        }
        size--;
        elementData[size] = null;
        return old
    }

// 07 // 13 // 18
    private static void grow() {
        // for 문을 사용해서 반복문을 쓰지 않아도 간편하게 배열을 늘릴 수 있다.
        // 길이가 늘어난 새로운 배열을 만들고
        int newCapacity = elementData.length + (elementData.length >> 1);
        // 그 배열의 레퍼런스를 기존 배열의 레퍼런스가 들어있던 곳에 넣는다.
        // Arrays.copyOf(기존배열, 새 배열);
        elementData = Arrrays.copyOf(elementData, newCapacity);
        // Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        // for (int i = 0; i < elementData.length; i++) {
        //     newArray[i] = elementData[i];
        // }
        // elementData = newArray;
    }
}
```

## 19) 배열의 특정 항목을 삭제할 때 배열 복사 기능을 이용하여 처리한다.

```java
public class MyArrayList {
// 17
    private static final int DEFAULT_CAPACITY = 5;

// 01 // 12 // 13 // 15
    private Object[] elementData;
    private int size;

// 13 
    public int size() {
        return this.size;
    }

// 14 // 16 // 17
    public MyArrayList(int initialCapacity) {
        if (initialCapacity < DEFAULT_CAPACITY) {
            elementData = new Object[DEFAULT_CAPACITY];
        } else {
            elementData = new Object[initialCapacity];
        }
    }

// 15 // 17
    public MyArrayList() {
        elementData = new Object[DEFAULT_CAPACITY];
    }

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12 // 19
    public Object remove(int index) {
        Object old = elementData[index];

        System.arraycopy(
            elementData,            // 복사 대상
            index + 1,              // 복사할 항목의 시작 인덱스
            elementData,            // 목적지
            index,                  // 복사 목적지 인덱스
            // 인덱스가 0부터 시작하기 때문에 갯수는 +1을 해줘야 한다
            this.size - (index + 1) // 복사할 항목의 갯수
        );
        // for (int i = index; i < size - 1; i++) {
        //     elementData[i] = elementData[i +1];
        // }
        size--;
        elementData[size] = null;
        return old
    }

// 07 // 13 // 18
    private static void grow() {
        int newCapacity = elementData.length + (elementData.length >> 1);
        elementData = Arrrays.copyOf(elementData, newCapacity);
        // Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        // for (int i = 0; i < elementData.length; i++) {
        //     newArray[i] = elementData[i];
        // }
        // elementData = newArray;
    }
}
```

## ArrayList에 보관되어 있는 인스턴스 목록을 배열로 리턴하는 toArray() 메서드를 추가한다.

```java
public class MyArrayList {
// 17
    private static final int DEFAULT_CAPACITY = 5;

// 01 // 12 // 13 // 15
    private Object[] elementData;
    private int size;

// 13 
    public int size() {
        return this.size;
    }

// 14 // 16 // 17
    public MyArrayList(int initialCapacity) {
        if (initialCapacity < DEFAULT_CAPACITY) {
            elementData = new Object[DEFAULT_CAPACITY];
        } else {
            elementData = new Object[initialCapacity];
        }
    }

// 15 // 17
    public MyArrayList() {
        elementData = new Object[DEFAULT_CAPACITY];
    }

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12 // 19
    public Object remove(int index) {
        Object old = elementData[index];

        System.arraycopy(
            elementData,           
            index + 1,              
            elementData,            
            index,                  
            this.size - (index + 1) 
        );
        // for (int i = index; i < size - 1; i++) {
        //     elementData[i] = elementData[i +1];
        // }
        size--;
        elementData[size] = null;
        return old
    }

// 07 // 13 // 18
    private static void grow() {
        int newCapacity = elementData.length + (elementData.length >> 1);
        elementData = Arrrays.copyOf(elementData, newCapacity);
        // Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        // for (int i = 0; i < elementData.length; i++) {
        //     newArray[i] = elementData[i];
        // }
        // elementData = newArray;
    }

// 20
    public Object[] toArray() {
        Object[] arr = new Object[this.size];
        // i는 인덱스
        for (int i = 0; i < arr.length; i++) {
            arr[i] = elementData[i];
        }
        return arr;
    }
}
```

## 21) toArray()에서 배열을 복사할 때 Arrays.copyOf() 메서드를 활용한다.

```java
public class MyArrayList {
// 17
    private static final int DEFAULT_CAPACITY = 5;

// 01 // 12 // 13 // 15
    private Object[] elementData;
    private int size;

// 13 
    public int size() {
        return this.size;
    }

// 14 // 16 // 17
    public MyArrayList(int initialCapacity) {
        if (initialCapacity < DEFAULT_CAPACITY) {
            elementData = new Object[DEFAULT_CAPACITY];
        } else {
            elementData = new Object[initialCapacity];
        }
    }

// 15 // 17
    public MyArrayList() {
        elementData = new Object[DEFAULT_CAPACITY];
    }

// 02 // 12
    public boolean add(Object e) {
        if (size == elementData.length) {
            grow();
        }
        elementData[size++] = e;
        return true;
    }

// 03 // 09 // 12
    public Object get(int index) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        return elementData[index];
    }

// 04 // 08 // 12
    public void add(int index, Object element) {
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

// 05 // 11 // 12
    public Object set(int index, Object element) {
        if (index < 0 || index >= size) {
        throw new ArrayIndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Object old = elementData[index];
        elementData[index] = element;
        return old;

// 06 // 10 // 12 // 19
    public Object remove(int index) {
        Object old = elementData[index];

        System.arraycopy(
            elementData,           
            index + 1,              
            elementData,            
            index,                  
            this.size - (index + 1) 
        );
        // for (int i = index; i < size - 1; i++) {
        //     elementData[i] = elementData[i +1];
        // }
        size--;
        elementData[size] = null;
        return old
    }

// 07 // 13 // 18
    private static void grow() {
        int newCapacity = elementData.length + (elementData.length >> 1);
        elementData = Arrrays.copyOf(elementData, newCapacity);
        // Object[] newArray = new Object[elementData.length + (elementData.lengt >> 1)];
        // for (int i = 0; i < elementData.length; i++) {
        //     newArray[i] = elementData[i];
        // }
        // elementData = newArray;
    }

// 20
    public Object[] toArray() {
        // copyOf​(original, int newLength)
        Object[] arr = Arrays.copyOf(elementData, this.size);
        return arr;
        // Object[] arr = new Object[this.size];
        // for (int i = 0; i < arr.length; i++) {
        //     arr[i] = elementData[i];
        // }
        // return arr;
    }
}
```