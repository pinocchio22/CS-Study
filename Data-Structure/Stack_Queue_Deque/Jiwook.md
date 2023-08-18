# 목차 
[1. Stack](#stack) <br>
[2. Queue](#queue) <br>
[3. Deque](#deque) <br>
[4. 요약](#요약) <br><br>


## Stack
스택은 컴퓨터에서 정말 많이 쓰이는 구조이다.
가장 최근에 들어온 데이터가 가장 위에 있게 되고, 또 먼저 나가게 된다. 이런 입출력 형태를 `후입선출(LIFO: Last-In-First-Out)`이라고 한다.
스택에서의 입출력은 맨 위에서만 일어나고 스택의 중간에서는 데이터를 삭제할 수 없다.
스택의 상단을 `Top`, 바닥부분을 `Bottom`이라고 한다.

<img src="https://github.com/z-wook/z-wook/assets/101041221/e89de2d1-98de-4faf-b5a2-9a20e7e1fb54">

스택은 특히 자료의 출력 순서가 입력순서의 역순으로 이루어져야 할 경우에 매우 요긴하게 사용된다.
예를 들어 컴퓨터의 연산(후위연산)

스택에서는 두 가지의 기본 연산이 있다. 하나는 `삽입 연산(push)`, 또 하나는 `삭제 연산(pop)`이 있다.

- 스택 구현
```swift
struct Stack<T> {
    private var elements: [T] = []
    
    // 스택에 요소 추가
    mutating func push(_ element: T) {
        elements.append(element)
    }
    
    // 스택에서 요소 제거 및 반환
    mutating func pop() -> T? {
        return elements.popLast()
    }
    
    // 스택의 가장 위(최근) 요소 반환
    func peek() -> T? {
        return elements.last
    }
    
    // 스택이 비어있는지 확인
    var isEmpty: Bool {
        return elements.isEmpty
    }
    
    // 스택의 요소 개수 반환
    var count: Int {
        return elements.count
    }
}
```
하지만! 굳이 Stack을 만들어 사용하지 않아도, 배열을 Stack처럼 사용 가능하다.
<br><br>


## Queue
큐는 먼저 들어온 데이터가 먼저 나가는 구조로 `선입선출(FIFO: First-In-First-Out)`이라고 한다.
큐는 뒤에서 새로운 데이터가 추가되고 앞에서 데이터가 하나씩 삭제되는 구조를 가지고 있다.
구조상으로 큐가 스택과 다른 점은 스택의 경우, 삽입과 삭제가 같은 쪽에서 일어나지만 큐에서는 삽입과 삭제가 다른 쪽에서 일어난다는 것이다.
큐에서 삽입이 일어나는 곳을 `후단(rear)`라고 하고 삭제가 일어나느 곳을 `전단(front)`라고 한다.

큐에서 연산은 `삽입 연산(enqueue)`와 `삭제 연산(dequeue)`이 있다.

- 선형 큐

<img src="https://github.com/z-wook/z-wook/assets/101041221/b0ec8835-8aed-463f-8a0b-db2d7279b1e4">

```swift
struct Queue<T> {
    private var elements: [T] = []
    
    // 큐에 요소 추가
    mutating func enqueue(_ element: T) {
        elements.append(element)
    }
    
    // 큐에서 요소 제거 및 반환
    mutating func dequeue() -> T? {
        return elements.isEmpty ? nil : elements.removeFirst()
    }
    
    // 큐의 가장 앞(첫 번째) 요소 반환
    func peek() -> T? {
        return elements.first
    }
    
    // 큐가 비어있는지 확인
    var isEmpty: Bool {
        return elements.isEmpty
    }
    
    // 큐의 요소 개수 반환
    var count: Int {
        return elements.count
    }
}
```

- 원형 큐
<img src="https://github.com/z-wook/z-wook/assets/101041221/369c8306-adc4-42e1-aaf0-55b43853e60e">

```swift
struct CircularQueue<T> {
    private var elements: [T?]
    private var head: Int = 0
    private var tail: Int = 0
    
    init(_ capacity: Int) {
        elements = Array(repeating: nil, count: capacity)
    }
    
    var isEmpty: Bool {
        return head == tail && elements[head] == nil
    }
    
    var isFull: Bool {
        return head == tail && elements[head] != nil
    }
    
    mutating func enqueue(_ element: T) {
        if !isFull {
            elements[tail] = element
            tail = (tail + 1) % elements.count
        } else {
            // 큐가 가득 찬 경우 예외 처리 가능
            print("Queue is full")
        }
    }
    
    mutating func dequeue() -> T? {
        if !isEmpty {
            let element = elements[head]
            elements[head] = nil
            head = (head + 1) % elements.count
            return element
        } else {
            // 큐가 비어있는 경우 예외 처리 가능
            print("Queue is empty")
            return nil
        }
    }
    
    func peek() -> T? {
        return elements[head]
    }
    
    var count: Int {
        return isEmpty ? 0 : (tail >= head ? tail - head : elements.count - head + tail)
    }
}
```
<br><br>


## Deque
덱(deque)은 double-ended-queue의 줄임말로서 큐의 전단(front)과 후단(rear)에서 모두 삽입과 삭제가 가능한 큐를 의미한다.

<img src="https://github.com/z-wook/z-wook/assets/101041221/42fd544c-1abc-444b-8d0f-95577429cf4d">

덱은 스택과 큐의 연산들을 모두 가지고 있다.
예를 들어 add_front와 delete_front 연산은 스택의 push와 pop 연산과 동일하다.
또한 add_rear 연산과 delete_front 여산은 각각 큐의 enqueue와 dequeue 연산과 같다.

```swift
struct Deque<T> {
    private var array: [T] = []

    var isEmpty: Bool {
        return array.isEmpty
    }

    var count: Int {
        return array.count
    }

    mutating func enqueueFront(_ element: T) {
        array.insert(element, at: 0)
    }

    mutating func enqueueBack(_ element: T) {
        array.append(element)
    }

    mutating func dequeueFront() -> T? {
        if isEmpty {
            return nil
        } else {
            return array.removeFirst()
        }
    }

    mutating func dequeueBack() -> T? {
        if isEmpty {
            return nil
        } else {
            return array.popLast()
        }
    }

    func front() -> T? {
        return array.first
    }

    func back() -> T? {
        return array.last
    }
}
```

## 요약
- 스택(Stack): 가장 최근에 들어온 데이터가 가장 위에 있게 되고, 또 먼저 나가는 `후입선출(LIFO: Last-In-First-Out)`구조이다.
- 큐(queue): 먼저 들어온 데이터가 먼저 나가는 구조로 `선입선출(FIFO: First-In-First-Out)`이라고 한다.
- 덱(deque)은 double-ended-queue의 줄임말로서 큐의 `전단(front)`과 `후단(rear)`에서 모두 삽입과 삭제가 가능한 큐를 의미한다.