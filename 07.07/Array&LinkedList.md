# 배열 (== 배열 기반의 리스트)

## 1. 특징

- 데이터를 순차적으로 저장됨
- 배열의 크기를 미리 선언을 해야하기 때문에 메모리 낭비가 발생할 수 있음
- 데이터를 탐색하는데 상대적으로 용이함
- 데이터를 삽입 또는 삭제할 때 상대적으로 비효율적임

## 2. 코드

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#define SIZE 10000
#define INF 99999999

int arr[SIZE];
int count = 0;

void addBack(int data)
{
	arr[count++] = data;
}

void addFirst(int data)
{
	for (int i = count; i >= 0; i--) {
		arr[i + 1] = arr[i];
	}
	arr[0] = data;
	count++;
}

void removeAt(int index)
{
	if (index > count) {
		printf("IndexError!!\n");
		return INF;
	}
	for (int i = index; i < count; i++) {
		arr[i] = arr[i + 1];
	}
	count--;
}

void show()
{
	for (int i = 0; i < count; i++) {
		printf("%d ", arr[i]);
	}
	printf("\n");
}

int main()
{
	addFirst(4);
	addFirst(5);
	addFirst(1);
	addBack(7);
	addBack(6);
	addBack(8);
	show();
	removeAt(3);
	show();
	return 0;
}
```

# 연결 리스트

## 1. 특징

- 데이터가 추가될 때마다 메모리 할당을 받음
- 배열의 크기를 미리 선언할 필요가 없어서 메모리 낭비가 없음
- 데이터를 탐색하는데 최초노드부터 순차탐색을 해야하므로 상대적으로 비효율적임
- 데이터를 삽입 또는 삭제할 때 할당 해제만 하면 되기 때문에 상대적으로 효율적임

## 2. 코드 (단방향)

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

typedef struct {
	int data;
	struct Node* next;
} Node;


void addFront(Node *head, int data)
{
	Node* node = (Node*)malloc(sizeof(Node));
	node->data = data;
	node->next = head->next;
	head->next = node;
}

void addBack(Node* head, int data)
{
	Node* lastNode = head;
	Node* node = (Node*)malloc(sizeof(Node));
	while (lastNode->next != NULL) {
		lastNode = lastNode->next;
	}
	node->data = data;
	node->next = NULL;
	lastNode->next = node;
}

void deleteFront(Node* head)
{
	Node* node = head->next;
	head->next = node->next;
	free(node);
}

void showAll(Node* head)
{
	Node* cur = head->next;
	while (cur != NULL) {
		printf("%d\n", cur->data);
		cur = cur->next;
	}
}

void freeAll(Node* head)
{
	Node* cur = head->next;
	while (cur != NULL) {
		Node* next = cur->next;
		free(cur);
		cur = next;
	}
}

int main()
{
	Node* head = (Node*)malloc(sizeof(Node));
	head->next = NULL;

	addBack(head, 7);
	addBack(head, 8);
	addBack(head, 2);
	deleteFront(head);
	showAll(head);
	freeAll(head);
	return 0;
}
```
