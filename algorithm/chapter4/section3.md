# 双端队列
###操作
* Deque() 创建一个空的双端队列
* addFront(item) 从队头加入一个item元素
* addRear(item) 从队尾加入一个item元素
* removeFront() 从队头删除一个item元素
* removeRear() 从队尾删除一个item元素
* isEmpty() 判断双端队列是否为空
* size() 返回队列的大小
```
class Deque:
    def __init__(self):
        self.items = []

    def isEmpty(self):
        return self.items == []

    def addFront(self, item):
        self.items.append(item)

    def addRear(self, item):
        self.items.insert(0,item)

    def removeFront(self):
        return self.items.pop()

    def removeRear(self):
        return self.items.pop(0)

    def size(self):
        return len(self.items)
```
###双端队列应用
一个有趣的问题，可以很容易地解决了使用队列的数据结构是典型的回文问题。回文数是一个字符串，读取相同的向前和向后的，例如,"sbbs"我们想构造一个算法，输入一个字符串是否回文。这个问题的解决方案将使用一个队列来存储字符串的字符。我们将从左到右弦和添加的每个字符的双端队列后。在这一点上，deque将会表现的非常像一个普通的队列。然而，我们现在可以利用该容器的双重功能。该容器前将字符串和该容器后的第一个字符将举行的最后一个字符
