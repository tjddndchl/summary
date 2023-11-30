## **Lambda 함수란?**
Lambda 함수는 Python에서 익명의 간단한 함수를 생성하기 위한 도구입니다. 주로 `filter()`, `map()`, `sorted()`와 같은 함수들과 함께 사용됩니다. Lambda 함수는 간결하게 코드를 작성할 수 있게 해주지만, 복잡한 로직을 구현하는 데는 적합하지 않습니다.

기본 구조: 
```python
lambda arguments: expression
```

## **상황별 사용법**

### 1. **리스트 아이템 제곱하기**
```python
numbers = [1, 2, 3, 4]
squared = list(map(lambda x: x**2, numbers))
```

### 2. **리스트에서 짝수만 필터링하기**
```python
numbers = [1, 2, 3, 4]
evens = list(filter(lambda x: x%2 == 0, numbers))
```

### 3. **문자열 리스트 정렬하기**
- 문자열의 길이를 기준으로 정렬:
```python
words = ['apple', 'banana', 'cherry']
sorted_words = sorted(words, key=lambda x: len(x))
```

### 4. **딕셔너리 정렬하기**
- 딕셔너리의 값을 기준으로 정렬:
```python
data = {'apple': 10, 'banana': 5, 'cherry': 20}
sorted_data = sorted(data.items(), key=lambda x: x[1])
```

### 5. **함수의 인자로 사용하기**
```python
def math_operation(func, x, y):
    return func(x, y)
result = math_operation(lambda x, y: x * y, 5, 3)
```

### 6. **다수의 인자를 받는 Lambda 함수**
```python
result = (lambda x, y, z: x + y + z)(1, 2, 3)
```

### 7. **Lambda에서 조건 사용하기**
```python
numbers = [1, 2, 3, 4]
modified = list(map(lambda x: x**2 if x%2 == 0 else x, numbers))
```

### 8. **리스트 내의 리스트 정렬하기**
- 내부 리스트의 특정 인덱스 값을 기준으로 정렬:
```python
data = [[1, 2], [4, 5], [2, 0]]
sorted_data = sorted(data, key=lambda x: x[1])
```

### 9. **함수 리스트 사용하기**
```python
functions = [lambda x: x**2, lambda x: x**3]
results = [f(4) for f in functions]
```

### 10. **Lambda 함수 내에서 두 개의 리스트 조합하기**
```python
list1 = [1, 2, 3]
list2 = [4, 5, 6]
result = list(map(lambda x, y: x + y, list1, list2))
```

---

`lambda` 함수는 간결한 코드 작성을 도와주며, 특히 함수의 인자로 간단한 함수를 전달할 때 유용합니다. 그러나 복잡한 함수의 경우 일반 함수 정의를 사용하는 것이 더 가독성이 좋습니다.



## **for 리스트 컴프리헨션?**
Python에서 `for`문을 한 줄로 사용하는 것을 "리스트 컴프리헨션(list comprehension)"이라고 합니다. 이는 리스트를 생성하거나 기존 리스트를 변형하는 등의 작업을 간결하게 수행할 수 있게 해줍니다.
리스트 컴프리헨션의 기본 형식은 다음과 같습니다:
```python
[expression for item in iterable if condition]
```

### 예제:

1. **기본 사용법**:
```python
squared_numbers = [x**2 for x in range(10)]
print(squared_numbers)  # [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

2. **조건문을 포함한 경우**:
```python
even_numbers = [x for x in range(10) if x % 2 == 0]
print(even_numbers)  # [0, 2, 4, 6, 8]
```

3. **중첩된 `for`문**:
```python
combinations = [(x, y) for x in [1, 2, 3] for y in [3, 1, 4] if x != y]
print(combinations)  # [(1, 3), (1, 4), (2, 3), (2, 1), (2, 4), (3, 1), (3, 4)]
```

리스트 컴프리헨션은 단순하고 간결하게 리스트를 생성할 수 있지만, 너무 복잡한 로직이나 중첩이 많은 경우 가독성이 떨어질 수 있으므로 적절한 상황에서 사용하는 것이 좋습니다.
