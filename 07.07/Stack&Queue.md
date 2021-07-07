# Stack

## Stack의 특징

- LIFO (Last Input First Output) --> 가장 마지막에 들어온 데이터가 먼저 뺄 수 있음
- 계산기 (중위표기법 -> 후위표기법), DFS(깊이 우선 탐색) 알고리즘 등에 사용
- top : 스택의 가장 윗부분
- PUSH : 스택에 데이터를 넣는다.
- POP : 스택에 있는 데이터를 빼서 출력한다.

## 1. 배열을 이용한 Stack

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#define SIZE 10000
#define INF 99999999

int stack[SIZE];
int top = -1;

void push(int data)
{
	if (top == SIZE - 1) {
		printf("스택 오버플로우!!\n");
		return INF;
	}
	stack[++top] = data;
}

int pop()
{
	if (top == -1) {
		printf("스택 언더플로우!!\n");
		return -INF;
	}
	return stack[top--];
}

void show()
{
	printf("---- 스택 윗부분 ----\n");
	for (int i = top; i >= 0; i--) {
		printf("%d\n", stack[i]);
	}
	printf("---- 스택 아랫부분 ----\n");
}

int main()
{
	push(7);
	push(5);
	push(4);
	push(6);
	printf("pop : %d\n",pop());
	printf("pop : %d\n", pop());
	show();
	return 0;
}
```

## 2. 연결리스트를 이용한 Stack

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

typedef struct {
	int data;
	struct Node* next;
} Node;

typedef struct {
	Node* top;
	int count;
} Stack;

void push(Stack* stack, int data)
{
	Node* node = (Node*)malloc(sizeof(Node));
	node->data = data;
	if (stack->count == 0) {
		node->next = NULL;
	}
	else {
		node->next = stack->top;
	}
	stack->top = node;
	stack->count++;
}

int pop(Stack* stack)
{
	if (stack->top == NULL) {
		printf("스택 언더플로우 발생!\n");
		return;
	}
	Node* node = stack->top;
	int data = node->data;
	stack->top = node->next;
	free(node);
	return data;
}

void show(Stack* stack)
{
	Node* cur = stack->top;
	while (cur != NULL) {
		printf("%d\n", cur->data);
		cur = cur->next;
	}
}

int main()
{
	Stack stack;
	stack.count = 0;
	push(&stack, 7);
	push(&stack, 5);
	printf("pop : %d\n", pop(&stack));
	push(&stack, 4);
	push(&stack, 6);
	printf("pop : %d\n", pop(&stack));
	show(&stack);
	return 0;
}
```

# Queue

## Queue의 특징

- FIFO (First Input First Output) --> 먼저 들어온 데이터가 먼저 뺄 수 있음
- 프로세스 스케줄링, BFS(너비 우선 탐색) 알고리즘 등에 사용
- front : 큐의 제일 앞부분
- rear : 큐의 제일 뒷부분
- PUSH : 큐에 데이터를 넣는다.
- POP : 큐에 있는 데이터를 빼서 출력한다.

## 1. 배열을 이용한 Queue

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#define SIZE 10000
#define INF 99999999

int queue[SIZE];
int front = 0;
int rear = 0;

void push(int n)
{
	if (rear >= SIZE) {
		printf("큐 오버플로우 발생!!\n");
		return INF;
	}
	queue[rear++] = n;
}

int pop()
{
	if (front == rear) {
		printf("큐 언더플로우 발생!!\n");
		return -INF;
	}
	return queue[front++];
}

void show()
{
	printf("---- 큐 앞부분 ----\n");
	for (int i = front; i < rear; i++) {
		printf("%d\n", queue[i]);
	}
	printf("---- 큐 뒷부분 ----\n");
}

int main()
{
	push(7);
	push(5);
	printf("%d 출력\n", pop());
	push(4);
	printf("%d 출력\n", pop());
	push(6);
	show();
	return 0;
}
```

## 2. 연결리스트를 이용한 Queue

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <stdlib.h>

typedef struct {
	int data;
	struct Node* next;
} Node;

typedef struct {
	Node* front;
	Node* rear;
	int count;
} Queue;

void push(Queue *queue, int data)
{
	Node* node = (Node*)malloc(sizeof(Node));
	node->data = data;
	node->next = NULL;
	if (queue->count == 0) {
		queue->front = node;
	}
	else {
		queue->rear->next = node;
	}
	queue->rear = node;
	queue->count++;
}

int pop(Queue* queue)
{
	if (queue->count == 0) {
		printf("큐 언더플로우 발생!!\n");
		return;
	}
	Node* node = queue->front;
	int data = node->data;
	queue->front = node->next;
	free(node);
	return data;
}

void show(Queue *queue)
{
	Node* cur = queue->front;
	while (cur != NULL) {
		printf("%d\n", cur->data);
		cur = cur->next;
	}
}

int main()
{
	Queue queue;
	queue.count = 0;
	push(&queue, 7);
	push(&queue, 5);
	push(&queue, 4);
	pop(&queue);
	push(&queue, 6);
	pop(&queue);
	show(&queue);
	return 0;
}
```
