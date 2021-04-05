---
title: Linked Lists - 1
layout: single
categories:
- Data Structure
tags:
- java
- programming basics
- data structure
last_modified_at: '2021-03-31 14:00:00 +08000'
---

> Learning linked lists in Java with [Udemy course - Practical Data Structures & Algorithms in Java](https://www.udemy.com/course/practical-data-structures-algorithms-in-java/)

## Linked list

Unlike an array([]), elements of a linked list are not managed with continuous indexes. A linked list consists of nodes, and each node has data and a reference(link) to the next node. 
![Linked list](/assets/images/linked-list.JPG)

## Array vs. Linked list
It is easier in a linked list to insert/delete data compared to an array. By the way, the linked list without an index usually slows down the speed of searching because access to certain elements requires sequential searching. In other words, the insertion/deletion of the first data is performed within the time of O(1) in a linked list. When we insert or delete data in an array at a specific index, we have to move all the rest of the data to the back from the point, but in the case of a linked list, we do not have to do it. However, the addition/deletion of data at one point rather than the first one takes time to retrieve the data, so it has O(n) performance.

## Singly Linked List
It is the simplest form of a linked list only with reference to the following nodes.
```java
public class SinglyLinkedList {
	private Node first;

	public boolean isEmpty() {
		return (first == null);
	}
	
	// used to insert at the beginning of the list
	public void insertFirst (int data) {
		Node newNode = new Node();
		newNode.data = data;
		newNode.next = first;
		first = newNode;
	}
	
	public Node deleteFirst() {
		Node temp = first;
		first = first.next;
		return temp;
	}
	
	public void displayList() {
		System.out.println("List (first ===> last)");
		Node current = first;
		while(current != null) {
			current.displayNode();
			current = current.next;
		}
		System.out.println();
	}
	
	public void insertLast(int data) {
		Node current = first;
		while(current.next != null) {
			current = current.next; // we will loop until current.next is null
		}
		
		Node newNode = new Node();
		newNode.data = data;
		current.next = newNode;
	}
}
```

### Source
[Practical Data Structures & Algorithms in Java](https://www.udemy.com/course/practical-data-structures-algorithms-in-java/)
[나무위키](https://namu.wiki/w/%EC%97%B0%EA%B2%B0%20%EB%A6%AC%EC%8A%A4%ED%8A%B8)
