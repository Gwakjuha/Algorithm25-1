# 문제 4. 작업 지연 최소화

## 문제 정의

- 각 작업은 `(소요시간, 마감시간)`으로 구성됨
- 작업은 순차적으로 하나씩만 수행 가능
- 마감 시간을 넘긴 경우 지연 발생
- 모든 작업을 완료했을 때 총 지연 시간을 최소화하는 작업 순서를 구하는 문제

---

## 입력

작업 리스트 = [(3,4), (2,2), (1,3)] # (duration, deadline)


---

## 선택 알고리즘 : 탐욕 알고리즘 (Greedy)

---

## 선택 기준 및 설명

- **마감 시간이 빠른 작업부터 먼저 처리**
- 정렬 기준: `sorted(tasks, key=lambda x: x[1])`
- 이유: 마감이 급한 작업부터 해결하면 전체 지연을 줄일 수 있음
- 알고리즘 전략: **Earliest Deadline First**

---

## 다른 작업 순서와 결과 비교

| 작업 순서 | 총 지연 시간 | 설명 |
|-----------|---------------|------|
| [3, 2, 1] | **0**        | 마감시간 내 완벽하게 완료 |
| [1, 2, 3] | 2             | 3번 작업이 2초 지연 |
| [2, 1, 3] | 1             | 3번 작업이 1초 지연 |

---

##  구현 코드

```python
def minimize_total_delay(tasks):
    # enumerate로 인덱스를 부여하여 작업 번호를 추적 (1번 작업, 2번 작업처럼 표시)
    #  각 작업은 (작업번호, (소요시간, 마감시간)) 구조로 변환됨
    #  key=lambda x[1][1] → 마감시간 기준으로 정렬 (Earliest Deadline First)
    sorted_tasks = sorted(enumerate(tasks, 1), key=lambda x: x[1][1])

    order = []         #  최종적으로 출력할 작업 수행 순서를 저장하는 리스트
    current_time = 0   #  현재까지 작업이 진행된 시간 (누적 작업 시간)
    total_delay = 0    #  총 지연 시간을 누적하는 변수

    # 마감이 빠른 작업부터 순차적으로 실행
    for idx, (duration, deadline) in sorted_tasks:
        current_time += duration  # 작업을 수행하는 데 걸리는 시간을 누적
        delay = max(0, current_time - deadline)  # 마감시간을 초과한 경우만 지연 발생
        total_delay += delay  # 총 지연 시간에 반영
        order.append(idx)     # 실행한 작업 번호를 결과 리스트에 저장

    return order, total_delay


# 입력
tasks = [(3,4), (2,2), (1,3)]

# 실행
order, total_delay = minimize_total_delay(tasks)
print("작업 순서:", order)
print("총 지연 시간:", total_delay)
```

**작업 순서: [3, 2, 1]**
**총 지연 시간: 0**
