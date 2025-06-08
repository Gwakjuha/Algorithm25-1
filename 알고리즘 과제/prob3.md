# 문제 3. 최대 이익 배낭 문제 (Fractional Knapsack)

## 선택 알고리즘 : 탐욕 알고리즘 (Greedy)

## 어떤 기준으로 선택했는가?

- **단위 무게당 가치(value/weight)**가 가장 높은 물건부터 선택
- 배낭의 용량이 허용되면 전부 담고, 안 되면 **일부만 쪼개서 담음**

---

## 탐욕 전략이 유효한가?

- **Fractional Knapsack 문제에서는 탐욕 전략이 항상 최적해를 보장**


---

## 구현 코드 및 주석 설명

```python
# 누적 이익을 저장할 변수 (소수점 처리를 위해 float)
total_value = 0.0

# 단위 무게당 가치가 높은 물건부터 차례로 담기 시도
for weight, value in items:
    
    # 현재 물건을 통째로 담을 수 있는 경우
    if capacity >= weight:
        capacity -= weight              # 배낭 용량에서 해당 물건 무게만큼 차감
        total_value += value            # 전체 이익에 물건의 가치를 그대로 더함

    else:
        # 물건을 전부 담을 수 없다면 → 남은 용량만큼 쪼개서 담기
        fraction = capacity / weight    # 해당 물건의 몇 %를 담을 수 있는지 계산
        total_value += value * fraction # 가치도 같은 비율만큼 더해줌
        break                           # 배낭이 가득 찼으므로 루프 종료

# 최종 누적된 이익 반환
return total_value
```
---

## 전체 코드 
```python

def fractional_knapsack(capacity, items):
    items.sort(key=lambda x: x[1]/x[0], reverse=True)
    total_value = 0.0
    for weight, value in items:
        if capacity >= weight:
            capacity -= weight
            total_value += value
        else:
            fraction = capacity / weight
            total_value += value * fraction
            break
    return total_value

capacity = 50
items = [(10, 60), (20, 100), (30, 120)]
print(fractional_knapsack(capacity, items))  
# 출력: 240.0
```
