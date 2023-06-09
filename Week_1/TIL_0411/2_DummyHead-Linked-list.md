### 조금 변형된 연결 리스트
* 맨 앞에 dummy node를 추가한 형태로 확장해본다.

```python
#리스트 순회

class Node:

	def __init__(self, item):
		self.data = item
		self.next = None


class LinkedList:

	def __init__(self):
		self.nodeCount = 0
		self.head = Node(None)
		self.tail = None
		self.head.next = self.tail


	def __repr__(self):
		if self.nodeCount == 0:
			return 'LinkedList: empty'

		s = ''
		curr = self.head
		while curr.next:
			curr = curr.next
			s += repr(curr.data)
			if curr.next is not None:
				s += ' -> '
		return s


	def getLength(self):
		return self.nodeCount


	def traverse(self):
		result = []
		curr = self.head
		while curr.next:
			curr = curr.next
			result.append(curr.data)
		return result


	def getAt(self, pos):
		if pos < 0 or pos > self.nodeCount:
			return None

		i = 0
		curr = self.head
		while i < pos:
			curr = curr.next
			i += 1

		return curr


	def insertAfter(self, prev, newNode):
		newNode.next = prev.next
		if prev.next is None:
			self.tail = newNode
		prev.next = newNode
		self.nodeCount += 1
		return True


	def insertAt(self, pos, newNode):
		if pos < 1 or pos > self.nodeCount + 1:
			return False

		if pos != 1 and pos == self.nodeCount + 1:
			prev = self.tail
		else:
			prev = self.getAt(pos - 1)
		return self.insertAfter(prev, newNode)


	def concat(self, L):
		self.tail.next = L.head.next
		if L.tail:
			self.tail = L.tail
		self.nodeCount += L.nodeCount

```

* 단점 
    * 전진은 가능하지만, 거꾸로 가지 못한다.


