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

        if (first == null) {
            first = node;
        } else {
            last.next = node;
        }
        last = node;
        size++;
        return true;
        }
    }
```