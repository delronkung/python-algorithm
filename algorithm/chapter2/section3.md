# 双向链表
一种更复杂的链表是“双向链表”或“双面链表”。每个节点有两个连接：一个指向前一个节点，（当此“连接”为第一个“连接”时，指向空值或者空列表）；而另一个指向下一个节点，（当此“连接”为最后一个“连接”时，指向空值或者空列表）
##操作
isEmpty() 链表是否为空  
size() 链表长度  
add() 链表头部添加  
append()  链表尾部添加  
insert() 中间位置添加  
remove() 删除节点   
search() 查找节点是否存在  
index() 求出指定节点的位置
##实现
```
class Node(object):
    def __init__(self,val,p=0):
        self.data = val
        self.next = p
        self.prev = p

class LinkList(object):
    def __init__(self):
        self.head = 0
    #获取指定位置的值
    def __getitem__(self, key):
        if self.isEmpty():
            print 'linklist is empty.'
            return
        elif key <0  or key > self.getlength():
            print 'the given key is error'
            return
        else:
            return self.getitem(key)

    def __setitem__(self, key, value):
        if self.isEmpty():
            print 'linklist is empty.'
            return
        elif key <0  or key > self.getlength():
            print 'the given key is error'
            return
        else:
            self.delete(key)
            return self.insert(key)

    #初始化一个链表，并循环用data里的元素的值赋给链表
    def initlist(self,data):
        self.head = Node(data[0])
        p = self.head
        for i in data[1:]:
            node = Node(i)
            p.next = node
            node.prev  = p
            p = p.next

    #获取链表长度
    def getlength(self):
        p =  self.head
        length = 0
        while p!=0:
            length+=1
            p = p.next
        return length


    def isEmpty(self):
        if self.getlength() ==0:
            return True
        else:
            return False

    #清空链表
    def clear(self):
        self.head = 0

    #在尾部添加节点
    def append(self,item):
        q = Node(item)
        if self.head ==0:
            self.head = q
        else:
            p = self.head
            while p.next!=0:
                p = p.next
            p.next = q
            q.prev = p

    def getitem(self,index):
        if self.isEmpty():
            print 'Linklist is empty.'
            return
        j = 0
        p = self.head
        while p.next!=0 and j <index:
            p = p.next
            j+=1
        if j ==index:
            return p.data
        else:
            print 'target is not exist!'

    def insert(self,index,item):
        if self.isEmpty() or index<0 or index >self.getlength():
            print 'Linklist is empty.'
            return
        if index ==0:
            q = Node(item,self.head)
            self.head = q
        p = self.head
        post  = self.head
        j = 0
        while p.next!=0 and j<index:
            post = p
            p = p.next
            j+=1
        if index ==j:
            q = Node(item,p)
            post.next = q
            q.prev = post
            q.next = p
            p.prev = q

    def remove(self,index):
        if self.isEmpty() or index<0 or index >self.getlength():
            print 'Linklist is empty.'
            return
        if index ==0:
            q = Node(item,self.head)
            self.head = q
        p = self.head
        post  = self.head
        j = 0
        while p.next!=0 and j<index:
            post = p
            p = p.next
            j+=1
        if index ==j:
            post.next = p.next
            p.next.prev = post

    def index(self,value):
        if self.isEmpty():
            print 'Linklist is empty.'
            return
        p = self.head
        i = 0
        while p.next!=0 and not p.data ==value:
            p = p.next
            i+=1
        if p.data == value:
            return i
        else:
            return -1

if __name__=="__main__":
    l = LinkList()
    l.initlist([1,2,3,4,5])
    print l.getitem(4)
    l.append(6)
    print l.getitem(5)

    l.insert(4,40)
    print l.getitem(3)
    print l.getitem(4)
    print l.getitem(5)

    l.delete(5)
    print l.getitem(5)

    l.index(5)
```
