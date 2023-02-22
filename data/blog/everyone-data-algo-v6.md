---
title: 누구나 자료구조와 알고리즘) 06. 긍정적인 시나리오 최적화(삽입 정렬)
date: '2022-11-02'
tags: ['자료구조', '알고리즘']
draft: false
summary: 알고리즘을 평가할 때, 최악의 시나리오를 가정하고 얼마나 많은 단계가 걸리는지 초점을
맞춘다! 
images: []
---

# 6. 긍정적인 시나리오 최적화 (삽입 정렬)

알고리즘을 평가할 때, 최악의 시나리오를 가정하고 얼마나 많은 단계가 걸리는지 초점을 맞춘다!

![스크린샷 2022-11-02 오후 5.05.39.png](/static/images/data/data06/01.png)

## 왜냐하면!!

최악의 시나리오 평가하면 다른 과정에서도 일이 순조롭기 때문이다.

**그러나 6장에서는 모든 시나리오를 고려할 수 있는 능력을 배워보자!**

## 6.1 삽입 정렬

삽입 정렬을 통해 최악의 사나리오가 아닌 시나리오를 분석해보자!

1. 1번째 인덱스의 값을 삭제하고 임시 변수에 저장한다.

![스크린샷 2022-11-02 오후 5.10.36.png](/static/images/data/data06/02.png)

1. 임시 변수의 값과 공백 칸 왼쪽의 값을 비교하고 임시 변수의 값이 작으면 공백 칸 왼쪽의 값을 오른쪽으로
   시프트 한다.

![스크린샷 2022-11-02 오후 5.12.20.png](/static/images/data/data06/03.png)

임시 변수의 값보다 작은 값을 만나거나 배열의 왼쪽 끝에 도달하면 시프트를 종료한다.

1. 임시 변수를 현재 공백 칸에 삽입한다.

![스크린샷 2022-11-02 오후 5.13.15.png](/static/images/data/data06/04.png)

1. 배열이 완벽히 정렬될 때까지 반복한다.

## 6.2 삽입 정렬해보기

![스크린샷 2022-11-02 오후 5.16.01.png](/static/images/data/data06/05.png)

## 6.3 삽입 정렬 구현

```python
# 아.. 나는 자바스크립트가 좋은데;;
def insertion_sort(array):
	for index in range(1, len(array)):
		position = index
		temp_value = array[index]

		while position > 0 and array[position - 1] > temp_value:
		# position > 0 : 배열 왼쪽 끝에 도달했는지 파악하기 위함.
			array[position] = array[position - 1]
			position = position - 1

		array[position] = temp_value

```

## 6.4 삽입 정렬의 효율성

### 비교

역순으로 정렬된 최악의 경우,

temp_value = 1

비교의 경우 왼쪽 값과 비교하기 때문에 index = 비교 수행 횟수 = 배열의 길이 - 1

마지막 패스스루에서 최대 n-1번의 비교가 일어난다.

원소가 10개면 1 + 2 + 3 + 4 + 5 + 6 + 7 + 8 + 9(10-1) = 45번

결국 원소가 n개인 배열일 경우 대략 n의 2제곱 / 2

### 시프트

역순으로 정렬된 최악의 경우,

비교가 일어날 때마다 값을 오른쪽으로 시프트!

![스크린샷 2022-11-02 오후 5.58.15.png](/static/images/data/data06/06.png)

### 삽입과 삭제

삭제와 삽입의 과정은 패스스루 마다 일어나기 때문에 N-1번!

![스크린샷 2022-11-02 오후 6.03.55.png](/static/images/data/data06/07.png)

즉! 계산 결과

# $O(N^2 + N)$

![스크린샷 2022-11-02 오후 6.08.35.png](/static/images/data/data06/08.png)

![스크린샷 2022-11-02 오후 6.08.53.png](/static/images/data/data06/09.png)

N이 증가할수록 가장 큰 N 차수가 중요해진다.

![스크린샷 2022-11-02 오후 6.09.47.png](/static/images/data/data06/10.png)

버블 정렬과 선택 정렬은 모두 $O(N^2)$ 이지만 실제로는 선택 정렬이 버블 정렬보다 2배 빠른 것 처럼
버블 정렬과 같이 삽입 정렬도 선택 정렬에 비해 느릴 것이라고 생각할 수 있지만 그렇게 간단하지 않다.

## 6.5 평균적인 경우

최악의 시나리오에서는 선택 정렬이 삽입 정렬보다 빠른게 사실이다. 하지만 가장 자주 일어나는 경우는
평균 시나리오다.

최악의 시나리오에서는 모든 데이터를 비교하고 시프트 하지만 평균 시나리오에서는 대체적으로 데이터의 반을 비교하고 시프트할 것이다.

최악의 시나리오 = $O(N^2 + N)$

평균 시나리오 = $O(N^2 / 2)$

![스크린샷 2022-11-03 오전 11.17.47.png](/static/images/data/data06/11.png)

**그렇다면 선택 정렬과 삽입 정렬 중에 뭐가 더 빠를까?**

상황마다 다 다르다고 하신다….

평균적인 경우에는 비슷하고, 거의 정렬된 데이터는 삽입 정렬, 역순으로 정렬된 데이터는 선택 정렬

## 6.6 실제 예제

[3, 1, 4, 2] 과 [4, 5, 3, 6] 사이에 있는 교집합을 구하시오!

- 답
  ```jsx
  function intersection(first_array, second_array) {
    var result = []
    for (var i = 0; i < first_array.length; i++) {
      for (var j = 0; j < second_array.length; j++) {
        if (first_array[i] === second_array[j]) {
          result.push(first_array[i])
        }
      }
    }
    return result
  }
  ```
  ![스크린샷 2022-11-03 오전 11.27.42.png](/static/images/data/data06/12.png)
- 수정안
  ```jsx
  function intersection(first_array^ second_array){
  	var result = [];
  	for (var i = 0; i < first_array.length; i++) {
  		for (var j = 0; j < second_array.length; j++) {
  			if (first_array[i] === second_array[j]) {
  				result.push(first_array[i]);
  				break;
  			}
  		}
  	}
  	return result;
  }
  ```

## 6.7 마무리

[https://youtu.be/EdIKIf9mHk0](https://youtu.be/EdIKIf9mHk0)

---

##### 해당 스터디는 팀원들과 함께 진행한 스터디이기에 모든 장을 혼자서 발표한 것이 아닙니다.

##### 다른 장도 궁금하다면 [노션](https://amplified-neptune-cfd.notion.site/HBT-9081eb15c1a04c9a821bb72052631e00)을 방문해주세요 :)
