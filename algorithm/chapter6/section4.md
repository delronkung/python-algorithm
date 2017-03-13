# 快速排序

快速排序（英语：Quicksort），又称划分交换排序（partition-exchange sort），通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以递归进行，以此达到整个数据变成有序序列。

步骤为：
1. 从数列中挑出一个元素，称为"基准"（pivot），
2. 重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区结束之后，该基准就处于数列的中间位置。这个称为分区（partition）操作。
3. 递归地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。

递归的最底部情形，是数列的大小是零或一，也就是永远都已经被排序好了。虽然一直递归下去，但是这个算法总会结束，因为在每次的迭代（iteration）中，它至少会把一个元素摆到它最后的位置去。


## 快速排序的分析
![quicksort1](/images/quicksort1.png)
![quicksort2](/images/quicksort2.png)
```python
def quick_sort(alist, first, last):
    # first为第一个元素的下标，last为最后一个元素的下标

    # 递归的结束条件
    if first<last:
        # 以第一个元素为基准，比较后面的元素
        mid = alist[first]
        left = first + 1
        right = last
        # 将left与right向中间移动，当left与right汇合时停止
        while left<right:
            # 找到right位置元素比基准小的
            while left<right and alist[right]>=mid:
                right -= 1
            # 找到left位置元素比基准大的
            while left<right and alist[left]<mid:
                left += 1
            # 交换元素，将比基准小的放到左边，比基准大的放到右边
            alist[left], alist[right] = alist[right], alist[left]
        # 此时left与right相等,
        if alist[left] <= mid:
            # 若alist[left]不大于mid, left为基准位
            alist[first], alist[left] = alist[left], alist[first]
        else:
            # 若alist[left]大于mid，则left后退一步
            left -= 1
        # 递归快排基准左边的元素
        quick_sort(alist, first, left-1)
        # 递归快排基准右边的元素
        quick_sort(alist, left+1, last)
alist = [54,26,93,17,77,31,44,55,20]
quick_sort(alist,0,8)
print(alist)
```
## 时间复杂度
+ 最优时间复杂度：O(nlogn)
+ 最坏时间复杂度：O(n<sup>2</sup>)
+ 稳定性：不稳定

从一开始快速排序平均需要花费O(n log n)时间的描述并不明显。但是不难观察到的是分区运算，数组的元素都会在每次循环中走访过一次，使用O(n)的时间。在使用结合（concatenation）的版本中，这项运算也是O(n)。

在最好的情况，每次我们运行一次分区，我们会把一个数列分为两个几近相等的片段。这个意思就是每次递归调用处理一半大小的数列。因此，在到达大小为一的数列前，我们只要作log n次嵌套的调用。这个意思就是调用树的深度是O(log n)。但是在同一层次结构的两个程序调用中，不会处理到原来数列的相同部分；因此，程序调用的每一层次结构总共全部仅需要O(n)的时间（每个调用有某些共同的额外耗费，但是因为在每一层次结构仅仅只有O(n)个调用，这些被归纳在O(n)系数中）。结果是这个算法仅需使用O(n log n)时间。

## 快速排序演示
![quicksort](/images/quicksort.gif)
