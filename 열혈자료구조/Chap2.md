# 1. 함수의 재귀적 호출의 이해

## 재귀함수란

- 재귀함수: 함수 내에서 자기 자신을 다시 호출하는 함수

```jsx
function recursive(){
  console.log("Recursive call!");
  recursive(); // 자기 자신을 재 호출
};
```

- recusive함수를 복사하여 CPU로 이동하여 실행
- 여러 recusive함수가 CPU로 복사 될 수있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/eec7b6e8-de70-4193-a1f3-6ffc5be78311/Untitled.png)

<aside>
💡 재귀함수에는 탈출 조건이 필요하다
탈출 조건이 없으면 무한루프에 빠질 수 있다

</aside>

```jsx
function recursive(num) {
  if (num <= 0) return; //재귀 탈출 조건
  console.log("Recursive call!");
  recursive(); // 자기 자신을 재 호출
}
```

- recursive(3) 함수의 호출 과정

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/23a55451-98f8-4f47-83de-1f7b7310b5aa/Untitled.png)

## 재귀함수의 디자인 사례

- 팩토리얼
    
    $n! = n * (n-1)*(n-2)*(n-3)*....*2*1$
    
    n!은 n과(n-1)!으로 표현 가능
    
    $n!=n*(n-1)!$
    
    $f(n)=\left\{\begin{matrix}
     n*f(n-1)&.... n\geq1  \\
     1&....n=0  \\
    \end{matrix}\right.$
    
    ```c
    int Factorial(int n)
    {
    	if (n == 0) //n이 0일때
    		return 1;
    	else
    		return n * Factorial(n - 1); //n이 1이상일때
    }
    ```
    

# 2. 재귀의 활용

## 피보나치 수열

- 피보나치 수열: 앞엣것 두 개 더해서 현재의 수를 만들어 가는 수열
0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, . . . .

$fib(n)=\left\{\begin{matrix}
0 & ....n=1 \\
1 &  ....n=2\\
fib(n-1)+fib(n-2) &  otherwise\\
\end{matrix}\right.$

```c
int Fibo(int n)
{
	printf("func call param %d \n", n);

	if (n == 1) // n이 1일때
		return 0;
	else if (n == 2) // n이 2일때
		return 1;
	else
		return Fibo(n - 1) + Fibo(n - 2); // otherwise
}
```

- Fibo(6) 함수 호출 순서

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/63235251-e07f-49f8-860d-2a4d015593ac/Untitled.png)

- 재귀 시간 복잡도: $O(2^n)$
    - fibo(3)이 세번 fibo(4)가 두번 중복되어 실행됨
    - n이 커지면 더 중복되어 실행되기 때문에 비효율 적
- 반복 시간 복잡도: $O(n)$

## 이진탐색 알고리즘

- 이진 탐색 알고리즘의 반복 패턴
    1. 탐색 범위의 중앙에 목표 값이 저장되었는지 확인
    2. 저장되지 않았다면 탐색 범위를 범위를 반으로 줄여서 다시 탐색 시작
- 탈출 조건
    1. first가 last보다 커질 때
    2. target 값을 찾았을 때

```c
int BSearchRecur(int ar[], int first, int last, int target) 
{
	int mid;
	if (first > last) // 탈출조건 1
		return -1;
	mid = (first + last) / 2;

	if (ar[mid] == target) // 1번의 경우, 탈출조건 2
		return mid;
	// 2의 경우
	else if (target < ar[mid])
		return BSearchRecur(ar, first, mid - 1, target);
	else
		return BSearchRecur(ar, mid + 1, last, target);
}
```

## 하노이타워

- 하노이타워 반복패턴
    1. 작은 원반 n-1개를(맨 아래의 원반을 제외한 나머지 원반을) A에서 B로 이동
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ac39fb2d-d08c-4c9b-9706-c6c60a05571d/Untitled.png)
        
    2. 큰 원반 1개를(맨 아래의 원반) A에서 C로 이동
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/09a8456e-28b4-4450-b28b-c13414aa43dc/Untitled.png)
        
    3. 작은 원반 n-1개를(1단계에서 옮겨진 원반) B에서 C로 이동
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/851720fc-e415-4625-9d95-56f7e21cdcc9/Untitled.png)
        

```jsx
const hanoiTowerMove = (num, from, by, to) => {
  if (num == 1) {
    console.log(`원반 1을 ${from}에서 ${to}로 이동합니다`);
  } else {
    hanoiTowerMove(num - 1, from, to, by); // 1번의 경우
    console.log(`원반 ${num}을(를) ${from}에서 ${to}로 이동합니다`); // 2번의 경우
    hanoiTowerMove(num - 1, by, from, to); // 3번의 경우
  }
};
```