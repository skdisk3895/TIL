# 선택 정렬 (Selection Sort)

기존 위치에 맞는 원소를 선택하여 교환하는 방식

## 1. 정렬 방식

1. 아직 정렬이 안된 원소 중에 가장 앞에 원소를 최소 값으로 설정한다.

2. 가장 앞에 원소를 제외한 나머지 원소를 차례로 비교하고 최소값을 찾는다.

3. 찾은 최소값을 가장 앞에 원소와 교환

4. 정렬이 안된 원소들 가지고 반복

## 2. 특징

1. 최소값을 찾기 위한 비교횟수는 많지만 교환횟수는 적다.

2. 데이터의 개수가 적을 때 좋은 성능을 발휘한다.

3. 시간복잡도 : O(n^2)

## 3. 코드

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int arr[5] = { 5, 4, 3, 2, 1 };

void swap(int* a, int* b)
{
	int temp = *a;
	*a = *b;
	*b = temp;
}

int main()
{
	for (int i = 0; i < 4; i++) {
		int min_val = arr[i], idx = i;
		for (int j = i + 1; j < 5; j++) {
			if (min_val > arr[j]) {
				min_val = arr[j];
				idx = j;
			}
		}
		swap(&arr[i], &arr[idx]);
		for (int i = 0; i < 5; i++)
			printf("%d ", arr[i]);
		printf("\n");
	}

	return 0;
}
```

#

# 삽입 정렬 (Insertion Sort)

배열의 모든 요소를 앞에서부터 차례대로 비교하여, 자신의 위치를 찾아 삽입함으로써 정렬하는 알고리즘

## 1. 정렬 방식

1. 배열의 첫 번째 요소는 정렬 된 상태라고 가정한다.

2. 배열의 두 번째 요소부터 앞에 정렬된 배열을 차례대로 비교하며 교환한다.

3. 자신의 위치에 맞는 위치에 삽입된다.

4. 다음 요소에 대해서 같은 작업을 반복

## 2. 특징

1. 데이터 개수가 적을 때 효율이 좋다.

2. 시간복잡도 : O(n^2)

## 3. 코드

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int arr[5] = { 1, 5, 4, 3, 2 };

void swap(int* a, int* b)
{
	int temp = *a;
	*a = *b;
	*b = temp;
}

void print()
{
	for (int i = 0; i < 5; i++)
		printf("%d ", arr[i]);
	printf("\n");
}

int main()
{
	for (int i = 1; i < 5; i++) {
		int j = i;
		while (j >= 0 && arr[j - 1] > arr[j]) {
			swap(&arr[j-1], &arr[j]);
			j--;
		}
		print();
	}

	return 0;
}
```

#

# 버블 정렬 (Bubble Sort)

두 인접한 배열요소를 차례대로 검사를 하여 정렬을 하는 방식

## 1. 정렬 방식

1. 배열의 가장 앞에서 인접한 두 개의 요소에 대하여 비교를 한다. (배열의 첫 번째 요소와 두 번째 요소)

2. 배열의 다음 인접한 요소(두 번째와 세번째를 비교를 한다.)

3. 배열의 끝까지 반복을 한다. 한 사이클이 끝나면 배열의 맨 끝에는 정렬된 요소 하나가 정렬이 된 채 자리잡는다.

4. 정렬이 된 마지막 요소를 제외한 나머지에 대하여 1,2,3 번 과정을 반복한다.

## 2. 특징

1. 코드 구현이 간단하다.

2. 시간복잡도 : O(n^2)

## 3. 코드

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

int arr[5] = { 1, 5, 4, 3, 2 };

void swap(int* a, int* b)
{
	int temp = *a;
	*a = *b;
	*b = temp;
}

void print()
{
	for (int i = 0; i < 5; i++)
		printf("%d ", arr[i]);
	printf("\n");
}

int main()
{
	for (int i = 0; i < 4; i++) {
		for (int j = 0; j < 4 - i; j++) {
			if (arr[j] > arr[j + 1])
				swap(&arr[j], &arr[j + 1]);
		}
		print();
	}

	return 0;
}
```

#

# 계수 정렬 (Counting Sort)

배열 안에 각 숫자가 몇번 등장했는지 개수를 이용해 정렬하는 방식

## 1. 정렬 방식

1. 배열에 존재하는 모든 수를 카운팅한다.

2. 나온 수에 대해 누적합을 구한다.

3. 배열의 끝부분부터 누적합을 이용해서 해당되는 index에 삽입한다.

## 2. 특징

1. 일반적으로 가장 빠른 정렬 방법

2. 숫자 크기에 시간복잡도가 매우 큰 영향을 받는다.

3. 시간복잡도 : O(n)

## 3. 코드

```C
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>

#define MAX_SIZE 1000
#define MAX_NUM 10000

int main() {
    int N, A[MAX_SIZE + 1], B[MAX_SIZE + 1], count[MAX_NUM + 1], countSum[MAX_NUM + 1];

    scanf("%d", &N);

    for (int i = 0; i <= N; i++)
        count[i] = 0;

    for (int i = 1; i <= N; i++) {
        scanf("%d", &A[i]);
        count[A[i]]++;
    }

    countSum[0] = count[0];
    for (int i = 1; i <= MAX_NUM; i++)
        countSum[i] = countSum[i - 1] + count[i];

    for (int i = N; i >= 1; i--) {
        B[countSum[A[i]]] = A[i];
        countSum[A[i]]--;
    }

    for (int i = 1; i <= N; i++)
        printf("%d ", B[i]);

    return 0;
}
```
