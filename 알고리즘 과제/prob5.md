# 문제 5. 최소 동전 개수

## 문제 설명

- 주어진 동전 종류로 목표 금액을 만들 때 **필요한 최소 동전 개수**를 구하는 문제
- 각 동전은 **무한히 사용 가능**
- 대표적인 **동적 계획법(DP)** 문제

---

## 입력 예시

- 금액 = 11
- 동전 종류 = [1, 3, 5]
---
## 출력력
3 → (5 + 5 + 1)


---

## 선택 알고리즘: Bottom-Up 동적 계획법 (DP)

---

## DP 점화식 및 설명

- `dp[i]`는 **금액 i를 만들기 위한 최소 동전 개수**
- 초기 상태:
  - `dp[0] = 0` (0원을 만드는 데는 동전 0개 필요)
  - 나머지는 `inf`로 초기화

- 점화식:

```python
    # 1원부터 target원까지 순서대로 최소 동전 수 계산
    for x in range(1, target + 1):
        for coin in coins:
            if x - coin >= 0:  # 현재 동전이 x원을 만드는 데 사용 가능하다면
                # x원을 만들기 위해 coin을 쓰면
                # 나머지 금액(x - coin)의 최소 동전 수 + 1개
                dp[x] = min(dp[x], dp[x - coin] + 1)


```
---
## 구현 코드 
```python

def min_coin_count(coins, target):
    # dp[i]: i원을 만들기 위한 최소 동전 개수
    dp = [float('inf')] * (target + 1)
    dp[0] = 0  # 0원을 만들기 위해 필요한 동전은 0개

    # 1원부터 target원까지 순서대로 최소 동전 수 계산
    for x in range(1, target + 1):
        for coin in coins:
            if x - coin >= 0:  # 현재 동전이 x원을 만드는 데 사용 가능하다면
                # x원을 만들기 위해 coin을 쓰면
                # 나머지 금액(x - coin)의 최소 동전 수 + 1개
                dp[x] = min(dp[x], dp[x - coin] + 1)

    return dp[target] if dp[target] != float('inf') else -1  # 만들 수 없으면 -1

# 예시 실행
coins = [1, 3, 5]
target = 11
print(min_coin_count(coins, target))  # 출력: 3 (5 + 5 + 1)
```
