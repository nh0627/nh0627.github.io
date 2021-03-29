---
title: Stack & Queue
layout: single
categories:
- Data Structure
tags:
- java
- programming basics
- data structure
last_modified_at: '2021-03-29 14:00:00 +08000'
---
> Learning stack and queue in Java with [udemy course - Practical Data Structures & Algorithms in Java](https://www.udemy.com/course/practical-data-structures-algorithms-in-java/)

## Stack
- FILO (First In Last Out)
- "top" indicates the index point where insertion and deletion happens
- push() for insertion and pop() for deletion are the primary operations

```java
public class Stack {

	private int maxSize;
	private long[] stackArray;
	private int top; // represent the index position of the last(recent) item

	public Stack(int size) {
		this.maxSize = size;
		this.stackArray = new long[maxSize];
		this.top = -1;
	}

	public void push(long j) {
		if (isFull()) {
			System.out.println("The stack is already full!");
		} else {
			top++;
			this.stackArray[top] = j;
		}
	}

	public long pop() {
		if (isEmpty()) {
			System.out.println("The stack is already empty!");
			return -1;
		} else {
			int oldTop = top;
			top--;
			return stackArray[oldTop]; // the actual data is not removed, only the pointer is reduced
		}
	}

	public long peak() {
		return stackArray[top];
	}

	public boolean isEmpty() {
		return (top == -1);
	}

	public boolean isFull() {
		return (maxSize - 1 == top);
	}
}
```

## Queue
- FIFO (First In First Out)
- "front" indicates the index point where deletion happens
- "rear" indicates the index point where insertion happens
- Data will be inserted at the "rear" point but deleted from the "front" point
- enQueue() for insertion and deQueue() for deletion are the primary operations

```java
public class Queue {

	private int maxSize; // initialize the set number of slots
	private long[] queArray; // slots to maintain the data
	private int front; // the index position for the element in the front
	private int rear; // the index position for the element at the back of the line
	private int nItems; // count to maintain the number of items in our queue
	
	public Queue(int size) {
		this.maxSize = size;
		this.queArray = new long[size];
		this.front = 0; // index position of the first slot of the array.
		this.rear = -1; // there is no item in the array yet to be considered as the last item.
		this.nItems = 0; // no element in the array yet
	}
	
	public void insert(long j) {
		if (rear == maxSize -1) {
			rear = -1; // circular queue - we can set rear back to -1 so we can just overwrite data
		}
		rear++;
		queArray[rear] = j;
		nItems++;
	}
	
	public long remove(){
		long temp = queArray[front];
		front++;
		if (front == maxSize) {
			front = 0; // we can set front back to the 0th index to utilize the entire array again
		}
		nItems--;
		return temp;
	}
	
	public long peekFront() {
		return queArray[front];
	}
	
	public boolean isEmpty() {
		return (nItems == 0);
	}
	
	public boolean isFull() {
		return (nItems == maxSize);
	}
	
	public void view() {
		System.out.print("[ ");
		for(int i = 0; i <queArray.length; i++) {
			System.out.print(queArray[i] + " ");
		}
		System.out.print("]");
	}

}
```

### Source
[Practical Data Structures & Algorithms in Java](https://www.udemy.com/course/practical-data-structures-algorithms-in-java/)
