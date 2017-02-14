# 单项循环链表
在一个 循环链表中, 首节点和末节点被连接在一起。这种方式在单向和双向链表中皆可实现。要转换一个循环链表，你开始于任意一个节点然后沿着列表的任一方向直到返回开始的节点。再来看另一种方法，循环链表可以被视为“无头无尾”,可以解决约瑟夫问题
##操作
add() 添加一个节点
remove()  删除一个节点
search()  查找节点是否存在
size()  返回链表的长度
empty() 判断链表是否为空
##实现
```
class Node:
    def __init__(self, initdata):
        self.__data = initdata
        self.__next = None
    def getData(self):
        return self.__data
    def getNext(self):
        return self.__next
    def setData(self, newdata):
        self.__data = newdata
    def setNext(self, lnode):
        self.__next = lnode


class SinCycLinkedlist:
    def __init__(self):
        self._head = Node(None)
        #让第一个节点自己指向自己
        self._head.setNext(self._head)

    #添加一个节点
    def add(self, item):
        temp = Node(item)
        #添加的节点指向_head
        temp.setNext(self._head.getNext())
        #_head指向添加的temp节点
        self._head.setNext(temp)

    #删除一个节点
    def remove(self, item):
        prev = self._head
        while prev.getNext() != self._head:
            cur = prev.getNext()
            if cur.getData() == item:
                prev.setNext(cur.getNext())
            prev = prev.getNext()

    #查找节点是否存在
    def search(self, item):
        cur = self._head.getNext()
        while cur != self._head:
            if cur.getData() == item:
                return True
            cur = cur.getNext()
        return False

    #清空链表
    def empty(self):
        return self._head.getNext() == self._head

    #求出链表的大小
    def size(self):
        count = 0
        cur = self._head.getNext()
        while cur != self._head:
            count += 1
            cur = cur.getNext()
        return count
```
