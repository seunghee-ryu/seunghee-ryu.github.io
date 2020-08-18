---
layout: post
title:  "How to make LinkedList"
categories: TLI
layout : single
---
# TLI How to make LinkedList

## 01) LinkedList 클래스 정의

```java
// 01
public class MyLinkedList {

}
```

## 02) 값을 담을 노드 클래스를 설계한다.

```java
// 01
public class MyLinkedList {

// 02
    // 용도?
    // - Node 클래스는 목록에서 각 항목의 값을 보관하는 객체로 역할을 수행한다.
    // 스태틱 클래스?
    // - 여러개의 MyLinkedList 객체가 공요하는 클래스이기 때문에 static으로 node 클래스를 설계한다.
    static class Node {
        Object value;
        Node next;
    }
}
```

## 03) 첫번째 노드와 마지막 노드의 주소를 담을 필드와 목록 크기를 저장할 필드를 추가한다.

```java
// 01
public class MyLinkedList {
        
// 03
    // 값을 찾을때는 첫번째 노드부터 따라간다.
    Node first;
    // 값을 추가할 때는 마지막 노드에 연결한다.
    Node last;
    // MyLinkedList 목록 크기를 보관한다.
    int size;

// 02
    static class Node {
        Object value;
        Node next;
    }
}
```

## 04) 목록에 값을 추가하는 add() 메서드를 정의한다.

```java
// 01
public class MyLinkedList {

// 03
    Node first;
    Node last;
    int size;

// 02
    static class Node {
        Object value;
        Node next;
    }

// 04
    public boolean add(Object e) {
        Node node = new Node();
        node.value = e;

        // first 변수가 null이면 first 변수에 node 주소를 넣고
        if (first == null) {
            first = node;
        // first 변수가 null이 아니면 last 변수(노드?)의 next 부분에 node 주소를 넣는다.
        } else {
            last.next = node;
        }
        // last 변수에 node new node 주소를 넣는다.
        last = node;
        size++;
        return true;
    }
}
```

## 05) 목록에서 값을 조회하는 get() 메서드를 정의한다.

```java
// 01
public class MyLinkedList {

// 03
    Node first;
    Node last;
    int size;

// 02
    static class Node {
        Object value;
        Node next;
    }

// 04
    public boolean add(Object e) {
        Node node = new Node();
        node.value = e;

        if (first == null) {
            first = node;
        } else {
            last.next = node;
        }
        last = node;
        size++;
        return true;
    }

// 05
    public Object get(int index) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        // node를 가리키는 cursor를 사용한다.
        // 커서는 처음 node부터 순서대로 움직인다.
        // 오른쪽에서부터 실행한다.
        // cursor.next 변수의 주소값을 cursor에 넣는다.
        Node cursor = this.first;
        for (int i = 1; i <= index; i++) {
            cursor = cursor.next;
        }
        return cursor.value;
    }
}
```

## 06) 목록에서 특정 인덱스 위치에 값을 삽입하는 add(in, Object) 메서드를 정의한다.
- Node의 생성자를 추가한다.

```java
// 01
public class MyLinkedList {

// 03 
    Node first;
    Node last;
    int size;

// 02 // 06
    static class Node {
        Object value;
        Node next;

        // 기본 생성자와 value를 파라미터로 가지는 생성자를 만든다.
        public Node() {}
        public Node(Object value) {
            this.value = value;
        }
    }

// 04
    public boolean add(Object e) {
        Node node = new Node();
        node.value = e;

        if (first == null) {
            first = node;
        } else {
            last.next = node;
        }
        last = node;
        size++;
        return true;
    }

// 05
    public Object get(int index) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node cursor = this.first;
        for (int i = 1; i <= index; i++) {
            cursor = cursor.next;
        }
        return cursor.value;
    }

// 06
    public void add(int index, Object element) {
        // index == size 면 마지막에 붙이는 것이 되어 인덱스가 유효하다.
        if (index < 0 || index > size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node node = new Node(element);
        size++;

        // 인덱스가 0 이면 first 주소를 변경해서 first Node를 바꿔줘야 한다.
        if (index == 0) {
            node.next = first;
            first = node;
            return;
        }
        // 커서는 인덱스 바로 전까지 움직인다.
        Node cursor = this.first;
        for (int i = 1; i <= index - 1; i++) {
            cursor = cursor.next;
        }
        // 커서가 가리키는 노드의 next 값을 삽입하려는 node의 next에 넣어준다.
        node.next = cursor.next;
        // 노드의 주소를 커서가 가리키는 노드의 next에 넣는다.
        cursor.next = node;

        // 마지막에 삽입한 후에는 last를 바꿔줘야 한다.
        // 마지막 노드의 next는 null인 것을 이용한다.
        if (node.next == null) {
            last = node;
        }
    }
}
```

## 07) 목록에서 특정 인덱스의 값을 제거하는 remove(int) 메서드를 정의한다.

```java
// 01
public class MyLinkedList {

// 03 
    Node first;
    Node last;
    int size;

// 02 // 06
    static class Node {
        Object value;
        Node next;

        public Node() {}
        public Node(Object value) {
            this.value = value;
        }
    }

// 04
    public boolean add(Object e) {
        Node node = new Node();
        node.value = e;

        if (first == null) {
            first = node;
        } else {
            last.next = node;
        }
        last = node;
        size++;
        return true;
    }

// 05
    public Object get(int index) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node cursor = this.first;
        for (int i = 1; i <= index; i++) {
            cursor = cursor.next;
        }
        return cursor.value;
    }

// 06
    public void add(int index, Object element) {
        if (index < 0 || index > size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node node = new Node(element);
        size++;

        if (index == 0) {
            node.next = first;
            first = node;
            return;
        }

        Node cursor = this.first;
        for (int i = 1; i <= index - 1; i++) {
            cursor = cursor.next;
        }

        node.next = cursor.next;
        cursor.next = node;

        if (node.next == null) {
            last = node;
        }
    }

    public Object remove(int value) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        size--;

        if (index == 0) {
            Node old = first;
            first = old.next;
            // 가비지가 다른 인스턴스를 가리키지 않게 한다.
            old.next = null;
            return old.value;
        }
        
        // 커서는 오른쪽 처음에서부터 인덱스 바로 전까지 움직인다.
        Node cursor = this.first;
        for (int i = 1; i <= index - 1; i++) {
            cursor = cursor.next;
        }

        // 가비지가 다른 인스턴스를 가리키지 않게 한다.
        Node old = cursor.next;
        cursor.next = old.next;
        old.next = null;

        if (cursor.next == null) {
            last = cursor;
        }
        return old.value;

    }
}
```

## 08) 목록에서 특정 인덱스의 값을 바꾸는 set(int, Object) 메서드를 정의한다.

```java
// 01
public class MyLinkedList {

// 03 
    Node first;
    Node last;
    int size;

// 02 // 06
    static class Node {
        Object value;
        Node next;

        public Node() {}
        public Node(Object value) {
            this.value = value;
        }
    }

// 04
    public boolean add(Object e) {
        Node node = new Node();
        node.value = e;

        if (first == null) {
            first = node;
        } else {
            last.next = node;
        }
        last = node;
        size++;
        return true;
    }

// 05
    public Object get(int index) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node cursor = this.first;
        for (int i = 1; i <= index; i++) {
            cursor = cursor.next;
        }
        return cursor.value;
    }

// 06
    public void add(int index, Object element) {
        if (index < 0 || index > size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node node = new Node(element);
        size++;

        if (index == 0) {
            node.next = first;
            first = node;
            return;
        }

        Node cursor = this.first;
        for (int i = 1; i <= index - 1; i++) {
            cursor = cursor.next;
        }

        node.next = cursor.next;
        cursor.next = node;

        if (node.next == null) {
            last = node;
        }
    }

// 07
    public Object remove(int value) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        size--;

        if (index == 0) {
            Node old = first;
            first = old.next;
            old.next = null;
            return old.value;
        }

        Node cursor = this.first;
        for (int i = 1; i <= index - 1; i++) {
            cursor = cursor.next;
        }

        Node old = cursor.next;
        cursor.next = old.next;
        old.next = null;

        if (cursor.next == null) {
            last = cursor;
        }
        return old.value;
    }

// 08
    public Object set(int index, Object element) {
        if (index < 0 || index >= this.size) {
        throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
    }

        Node cursor = this.first;
        for (int i = 1; i <= index; i++) {
        cursor = cursor.next;
        }

        Object old = cursor.value;
        cursor.value = element;

        return old;
  }
}
```

## 09) 목록의 데이터를 새 배열에 담아 리턴하는 toArray() 메소드를 정의한다.

```java
// 01
public class MyLinkedList {

// 03 
    Node first;
    Node last;
    int size;

// 02 // 06
    static class Node {
        Object value;
        Node next;

        public Node() {}
        public Node(Object value) {
            this.value = value;
        }
    }

// 04
    public boolean add(Object e) {
        Node node = new Node();
        node.value = e;

        if (first == null) {
            first = node;
        } else {
            last.next = node;
        }
        last = node;
        size++;
        return true;
    }

// 05
    public Object get(int index) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node cursor = this.first;
        for (int i = 1; i <= index; i++) {
            cursor = cursor.next;
        }
        return cursor.value;
    }

// 06
    public void add(int index, Object element) {
        if (index < 0 || index > size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node node = new Node(element);
        size++;

        if (index == 0) {
            node.next = first;
            first = node;
            return;
        }

        Node cursor = this.first;
        for (int i = 1; i <= index - 1; i++) {
            cursor = cursor.next;
        }

        node.next = cursor.next;
        cursor.next = node;

        if (node.next == null) {
            last = node;
        }
    }

// 07
    public Object remove(int value) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        size--;

        if (index == 0) {
            Node old = first;
            first = old.next;
            old.next = null;
            return old.value;
        }

        Node cursor = this.first;
        for (int i = 1; i <= index - 1; i++) {
            cursor = cursor.next;
        }

        Node old = cursor.next;
        cursor.next = old.next;
        old.next = null;

        if (cursor.next == null) {
            last = cursor;
        }
        return old.value;
    }

// 08
    public Object set(int index, Object element) {
        if (index < 0 || index >= this.size) {
        throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }

        Node cursor = this.first;
        for (int i = 1; i <= index; i++) {
        cursor = cursor.next;
        }

        Object old = cursor.value;
        cursor.value = element;

        return old;
    }

// 09
    public Object[] toArray() {
        Object[] arr = new Object[this.size];

        int i = 0;
        Node cursor = first;
        while (cursor != null) {
            arr[i++] = cursor.value;
            cursor = cursor.next;
        }
        return arr;
    }
}
```

## 10) 인스턴스 필드에 대해 캡슐화를 적용한다.

- 목록 크기를 리턴하는 size()를 추가로 정의한다.

```java
// 01
public class MyLinkedList {

// 03 // 10
    private Node first;
    private Node last;
    private int size;

// 02 // 06
    static class Node {
        Object value;
        Node next;

        public Node() {}
        public Node(Object value) {
            this.value = value;
        }
    }

// 04
    public boolean add(Object e) {
        Node node = new Node();
        node.value = e;

        if (first == null) {
            first = node;
        } else {
            last.next = node;
        }
        last = node;
        size++;
        return true;
    }

// 05
    public Object get(int index) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node cursor = this.first;
        for (int i = 1; i <= index; i++) {
            cursor = cursor.next;
        }
        return cursor.value;
    }

// 06
    public void add(int index, Object element) {
        if (index < 0 || index > size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        Node node = new Node(element);
        size++;

        if (index == 0) {
            node.next = first;
            first = node;
            return;
        }

        Node cursor = this.first;
        for (int i = 1; i <= index - 1; i++) {
            cursor = cursor.next;
        }

        node.next = cursor.next;
        cursor.next = node;

        if (node.next == null) {
            last = node;
        }
    }

// 07
    public Object remove(int value) {
        if (index < 0 || index >= this.size) {
            throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }
        size--;

        if (index == 0) {
            Node old = first;
            first = old.next;
            old.next = null;
            return old.value;
        }

        Node cursor = this.first;
        for (int i = 1; i <= index - 1; i++) {
            cursor = cursor.next;
        }

        Node old = cursor.next;
        cursor.next = old.next;
        old.next = null;

        if (cursor.next == null) {
            last = cursor;
        }
        return old.value;
    }

// 08
    public Object set(int index, Object element) {
        if (index < 0 || index >= this.size) {
        throw new IndexOutOfBoundsException("인덱스가 유효하지 않습니다.");
        }

        Node cursor = this.first;
        for (int i = 1; i <= index; i++) {
        cursor = cursor.next;
        }

        Object old = cursor.value;
        cursor.value = element;

        return old;
    }

// 09
    public Object[] toArray() {
        Object[] arr = new Object[this.size];

        int i = 0;
        Node cursor = first;
        while (cursor != null) {
            arr[i++] = cursor.value;
            cursor = cursor.next;
        }
        return arr;
    }

// 10
    public int size() {
        return this.size;
    }
}
```