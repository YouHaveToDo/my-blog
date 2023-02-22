---
title: 누구나 자료구조와 알고리즘) 12. 이진 트리로 속도 향상
date: '2022-11-22'
tags: ['자료구조', '알고리즘']
draft: false
summary: 정렬된 배열도, 해시 테이블도 각자의 문제가 있고 완벽하지 않다.
images: []
---

# 12. 이진 트리로 속도 향상

정렬된 배열도, 해시 테이블도 각자의 문제가 있고 완벽하지 않다.

이번 시간에는 이진 트리를 공부해보자.

## 12.1 이진트리

11장에서 연결 리스트라는 노드 기반의 자료 구조를 배웠지만,
트리는 조금 다르다. 트리는 각 노드에 여러 노드로의 링크를 포함할 수 있다.

![요런식으로 ㅎㅎ..](/static/images/data/data12/01.png)

요런식으로 ㅎㅎ..

트리는 나무 .. 노드는 뿌리, 줄기 .. 여러개의 노드 = 트리

**트리의 세 가지 고유 용어**

1. 루트 : 가장 상위 노드
2. 부모노드와 자식노드
3. 레벨

잘 모르겠다면 HTML을 예시로 들어보자.

다들 아시겠지만 HTML에도 돔 트리라는 트리가 있고 트리를 구성하는 각각의 노드가 있다.

![스크린샷 2022-11-15 오전 2.04.42.png](/static/images/data/data12/02.png)

돔 트리 또한 가장 상위 노드(요소)인 Document를 루트라고 부르고,

body 노드는 h1의 부모노드이며, 반대로 h1은 body의 자식 노드 입니다.

레벨은.. DOM에서는 다른 의미니깐 패스합시다. 그냥 뎁스라고 생각하면 편합니다.

![스크린샷 2022-11-15 오전 2.07.07.png](/static/images/data/data12/03.png)

그 중에서, 우리가 배울 이진 트리는 다음과 같은 규칙을 따르는 트리입니다.

1. 각 노드의 자식은 2개 이하다.
2. 한 노드에 자식이 둘이면 한 자식은 부모보다 작은 값, 다른 자식은 부모보다 큰 값을 가져야 한다.

![이진 트리 O](/static/images/data/data12/04.png)

이진 트리 O

![이진 트리 X](/static/images/data/data12/05.png)

이진 트리 X

## 12.2 검색

컴퓨터는 어떻게 이진트리를 활용해서 검색을 할까?

![스크린샷 2022-11-15 오전 2.12.57.png](/static/images/data/data12/06.png)

루트를 기점으로 아래의 순서대로 진행한다.

1. 노드의 값을 확인한다.
2. 노드의 값이 찾고 있는 값이면 땡큐 ㅋ
3. 찾고 있는 값이 노드의 값보다 작은면 왼쪽 하위 노드
4. 크다면 오른쪽 하위 노드

예시를 파이썬 코드로 보자

```python
def search(valuej node):
# 기저 조건: 노드가 없거나
# 찾고 있던 값이면
	if node is None or node.value == value:
		return node
	# 찾고 있는 값이 현재 노드보다 작으면 # 왼쪽 자식을 검색한다.
	elif value < node.value:
		return search(value, node.leftChild)
	# 찾고 있는 값이 현재 노드보다 크면 # 오른쪽 자식을 검색한다.
	else: # value > node.value
		return searchCvalue^ node.rightChild)
```

문제!
1부터 100사이에서 61를 찾아보자

![스크린샷 2022-11-15 오전 2.16.42.png](/static/images/data/data12/07.png)

- 답
  ![스크린샷 2022-11-15 오전 2.17.47.png](/static/images/data/data12/08.png)
  이진 트리의 검색을 빅오 표기법으로 표현하면 O( log N ) 이다.
  단계를 수행할 때 마다 남은 공간의 반을 제거하기 때문.

## 12.3 삽입

사실 이진 트리를 쓰는 이유는 삽입 때문이라고 할 정도로 효율이 좋다.

아래 트리를 보고 45라는 값을 넣는 과정을 빅오 표현해보자!

![스크린샷 2022-11-15 오전 2.21.15.png](/static/images/data/data12/09.png)

- 답
  O(log N)

정렬된 배열과 비교했을 때, 배열에서 값을 추가하기 위해서는 탐색 과정을 거치고, 값을 삽입할 공간을 만들기 위해 넣으려고 하는 값보다 큰 값들을 오른쪽으로 시프트 하기 때문에 O(N)의 과정이 걸린다.

그래서 이진 트리가 상대적으로 매우 효율적이다.

## **12.4 삭제**

삭제는 쉽지 않다. 눈 크게 뜨고 정신 집중해서 보자.

![스크린샷 2022-11-15 오전 2.26.28.png](/static/images/data/data12/10.png)

위 트리에서 4를 삭제해보자.

뭐 하나 삭제하는 건 어렵지 않다. 25 → 10 → 4 이런식으로 찾아가면 되니깐.

하지만 10도 삭제하고 싶다면?

![11과의 관계가 사라진다.](/static/images/data/data12/11.png)

11과의 관계가 사라진다.

위 문제를 해결하기 위해 10의 자리에 11를 넣어 문제를 해결할 수 있다.

지금까지 배운 삭제 알고리즘을 보면

1. 삭제할 노드에 자식이 없으면 삭제한다.
2. 삭제할 노드에 자식이 하나면 삭제하고 그 자식을 삭제한 노드 자리에 위치시킨다.

![만약 자식이 2개라면?](/static/images/data/data12/12.png)

만약 자식이 2개라면?

1. 자식이 둘인 노드를 삭제할 때는 삭제된 노드를 후속자 노드로 대체한다.
   (후속자 노드: 삭제된 노드보다 큰 값 중 최솟값 … ?)

컴퓨터는 삭제된 값의 오른쪽 자식에 내려갔다가 이후 왼쪽 자식이 없어 질 때 까지 내려갔다가 바닥 값을 만나면 그게 후속자 노드를 찾는 방법이다.

![케이윌?](/static/images/data/data12/13.png)

케이윌?

**그러면 진짜 마지막으로 후속자 노드에 오른쪽 자식이 있으면?**

1. 후속자를 삭제된 노드가 있던 자리에 넣고, 후속자 노드의 오른쪽 자식을 **후속자 노드의 원래 부모의 왼쪽 자식으로 넣는다.**

![스크린샷 2022-11-15 오전 2.36.54.png](/static/images/data/data12/14.png)

```python
def delete(valueToDelete, node):
	# 트리 밑바닥에 도달해서 부모 노드에 자식이 없으면 기저 조건이다. if node is None:
	if node is None:
		return None
		# 삭제하려는 값이 현재 노드보다 작거나 크면,
		# 현재 노드의 왼쪽 혹은 오른쪽 하위 트리에 대한 재귀 호출의 반환값을 # 왼쪽 혹은 오른쪽 자식에 할당한다.
	elif valueToDelete < node.value:
		node.leftChild = delete(valueToDelete, node.leftChild) # 현재 노드(와 존재한다면 그 하위 트리)를 반환해서
		# 현재 노드의 부모의 왼쪽 혹은 오른쪽 자식의 새로운 값으로 쓰이게 한다.
		return node
	elif valueToDelete > node.value:
		node.rightChild = delete(valueToDelete, node.rightChild)
		return node
		# 현재 노드가 삭제하려는 노드인 경우
	elif valueToDelete = node.val니e:
		# 현재 노드에 왼쪽 자식이 없으면,
		# 오른쪽 자식(과 존재한다면 그 하위 트리)을 반환함으로써 삭제하고， # 그 부모의 새 하위 트리가 될 수 있도록 한다.
		if node.leftChild is None:
			return node.rightChild
# (현재 노드에 왼쪽 또는 오른쪽 자식이 없으면,
# 이 함수 코드 첫 줄에 따라 None으로 끝날 것이다.)
	elif node.rightChild is None:
		return node.leftChild
# 현재 노드에 자식이 둘이면,
# 현재 노드의 값을 후속자 노드의 값으로 바꾸는 # (아래) lift 함수를 호출함으로써 삭제한다.
	else:
		node.rightChild = Uft(nt)de.广ightChild_» node)
		return node

def lift(node, nodeToDelete):
# 이 함수의 현재 노드에 왼쪽 자식이 있으면,
# 왼쪽 하위 트리로 계속해서 내려가도록 함수를 재귀적으로 호출함으로써 # 후속자 노드를 찾는다.
	if node.leftChild:
		node.leftChild = lift(node.leftC hild, nodeToDelete)
		return node
# 현재 노드에 왼쪽 자식이 없으면,
# 이 함수의 현재 노드가 후속자 노드라는 뜻이므로
# 현재 노드의 값을 삭제하려는 노드의 새로운 값으로 할당한다.
	else:
		nodeToDelete.value = node.value
# 후속자 노드의 오른쪽 자식이 부모의 왼쪽 자식으로 쓰일 수 있도록 반환한다. return node.rightChild
```

## 12.5 이진 트리 다뤄보기

정렬된 배열과 이진 트리가 검색에서는 비슷할지 몰라도, 삽입과 삭제가 훨씬 빠르므로 데이터 수정이 많은 경우에
효율적이다.

우리가 책 리스트가 자주 바뀌는 앱을 만든다고 생각해보자.

조건은 이렇다!

1. 알파벳 순
2. 리스트 변경 가능
3. 제목 검색 가능.

우선, 알파벳 순으로 책 제목을 출력하고 싶다면 모든 노드에 방문 할 수 있어야 한다.
(자료구조에서 모든 노드를 방문하는 것을 **자료 구조 순회**라고 한다.)

다음, 리스트를 순서대로 출력할 수 있도록 알파벳 오름차순으로 순회해야 한다. 책에서는 **중위 순회**

이를 코드로 표현하면 이렇다.

```python
def traverse_and_print(node):
	if node is None:
		return
traverse_and_print(node.leftChild )
print(node.value)
traverse_and_print(node.rightChild)
```

![스크린샷 2022-11-15 오전 2.49.36.png](/static/images/data/data12/15.png)

![스크린샷 2022-11-15 오전 2.49.50.png](/static/images/data/data12/16.png)

책에서는 이렇게 설명하는데.. 나는 그냥 이해하기 쉽게 생각해보면

순서대로 찾기 위해서

알파벳 순서가 빠른 곳부터 느린 곳까지 확인 하기 위해, 왼쪽에서 오른쪽 순으로 간다고 생각하자.

---

##### 해당 스터디는 팀원들과 함께 진행한 스터디이기에 모든 장을 혼자서 발표한 것이 아닙니다.

##### 다른 장도 궁금하다면 [노션](https://amplified-neptune-cfd.notion.site/HBT-9081eb15c1a04c9a821bb72052631e00)을 방문해주세요 :)
