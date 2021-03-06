# Insertion Sort (삽입 정렬)

## 1. 삽입 정렬이란?

- 앞에서부터 차례대로 이미 정렬된 배열과 비교하여 삽입하여 정렬한다.
- 예를 들면 손 안에 카드의 순서를 정렬할 때 순서에 맞게 다른 카드를 중간에 삽입을 하게 되는데 이와 비슷하다.
- 구현이 비교적 간편한 장점이 있지만 Worst Case 시 Swap 연산이 많이 발생하게 된다.

## 2. 삽입 정렬의 단계별 순서 및 예제

- 오름차 순 정렬 예제

```
[3, 2, 1, 4] 와 같은 배열이 있다.
[(3), (2), 1, 4]
첫 번째 원소 3과 2의 크기 비교를 수행한다.
2가 3보다 작으므로 두 원소 위치를 swap 한다.
[3, 2, 1, 4] -> [2, 3, 1, 4]

세 번째 원소 1과 기존 정렬된 구간 [2, 3]이 삽입될 위치를 찾는다.
먼저 3과 1을 비교한다. 1보다 3이 크므로 두 원소 위치를 swap한다.
[2, 3, 1, 4] -> [2, 1, 3, 4]
다음 2와 1을 비교한다. 1보다 2가 크므로 두 원소 위치를 swap 한다.
[2, 1, 3, 4] -> [1, 2, 3, 4]

네 번째 원소 4과 기존 정렬된 구간 [1, 2, 3]이 삽입될 위치를 찾는다.
먼저 4와 3을 비교한다. 3보다 4가 크므로 두 원소 위치를 swap하지 않는다.
[1, 2, 3, 4] -> [1, 2, 3, 4]
```

## 3. 알고리즘 (오름차 기준)

- 먼저 정렬 대상이 N개 있을 때 2번째 원소($a_2$)부터 비교를 시작한다.
- 조건이 $a_1 < a_2$ 을 만족할 경우 Swap하지 않으며, 불만족할 경우 Swap 한다.
- 그러면 원소 $a_1 , a_2$ 는 상호간의 대소 관계가 정립된 상태가 된다. 이후 3번째 원소($a_3$)와 기존 정렬된 원소 간 비교를 시작한다.
- 먼저 $a_2 < a_3$ 조건을 만족할 경우 Swap하지 않으며, 불만족할 경우 Swap 한다. Swap이 수행 된 경우 Swap된 상태에서 $a_1 < a_2$ 간 비교를 수행한다. 조건이 $a_1 < a_2$ 을 만족할 경우 Swap하지 않으며, 불만족할 경우 Swap 한다.
- 그러면 원소 $a_1,a_2,a_3$ 는 상호간의 대소 관계가 정립된 상태가 된다. 이후 3번째 원소($a_4$)와 기존 정렬된 원소 간 비교를 시작한다.
- 위 작업을 일반화 하면 정렬 대상이 N개 있을 때 $n(1 <n < N)$ 번째 원소($a_n$)부터 비교를 시작하여 조건이 $a_i \le a_n < a_{i+1}$ 을 만족하는 순서 $i$ 에 원소 $a_n$ 을 삽입하는 동작으로 일반화 할 수 있다.

## 4. Loop 횟수 및 시간 복잡도

- N개의 원소가 존재 시, Best Case 상황에는 N개의 원소만큼만 비교작업을 수행하므로 (항상 $a_n < a_{i+1}$ 을 만족하므로 swap 발생하지 않고, 비교 연산을 N번만 수행해도 됨) 해당 Case에서의 시간 복잡도는 $O(n)$ 이 된다.
- 하지만 Worst Case 및 Average Case 에서는 $O(n^2)$ 가 된다.

## 5. 코드 구현

- C 코드로 구현

```c
//200320 jhpark
void insertion_sort(int a[], int size)
{
    int swap, tmp;
    for (int i = 1; i < size; i++) {
        tmp = a[i];
        for (int j = i; j > 0; j--) {
            if(tmp <= a[j - 1])
            {
                swap = a[j - 1];
                a[j - 1] = a[j];
                a[j] = swap;
            }
            else
            {
                break;
            }
        }
    }
}
```

