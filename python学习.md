字符编码

```python
chr(65)  # 将数字转换成字符
ord('A')   # 将字符转换成ascii
```

##### bisect模块

bisect模块包含两个主要函数，bisect和insort，两个函数都利用二分查找算法来在有序序列中查找或插入元素。注意其操作的序列均为有序列。

###### bisect

bisect函数两个可选参数lo和hi，来缩小搜寻的范围。lo的默认值是0，hi的默认值是序列的长度，即len()作用于该序列的返回值。

其次，bisect函数其实是bisect_right函数的别名，后者还有个姊妹函数叫bisect_left。它们的区别在于，bisect_left返回的插入位置是原序列中跟被插入元素相等的元素的位置，也就是新元素会被放置于它相等的元素的前面，而bisect_right返回的则是跟它相等的元素之后的位置。

```python
import bisect
a=[1,3,5,6,7,89,222]
# 该函数传入一个有序序列和要插入的数字，返回要插入数字的位置
lo=bisect.bisect(a,8)
# lo=
```

```python
# 该代码展示了成绩的分档
import bisect
def grade(score, breakpoints=[60, 70, 80, 90], grades='FDCBA'):
    i=bisect.bisect(breakpoints,score)
    return grades[i]
lst=[grade(score) if score<=100 else '成绩有误' for score in [33, 99, 77, 70, 89, 90, 100,104]]
print(lst)
```

###### insort

insort(seq, item)把变量item插入到序列seq中，并能保持seq的升序顺序。

```python
import bisect
import random
SIZE=7
random.seed(1729)
my_list = []
for i in range(SIZE):
    new_item = random.randrange(SIZE*2)
    bisect.insort(my_list, new_item)
    print('%2d->'%new_item, my_list)
输出结果如下：
10-> [10]
 0-> [0, 10]
 6-> [0, 6, 10]
 8-> [0, 6, 8, 10]
 7-> [0, 6, 7, 8, 10]
 2-> [0, 2, 6, 7, 8, 10]
10-> [0, 2, 6, 7, 8, 10, 10]
```

##### 数组

###### array

```python
from array import array
from random import random

floats = array('d', (random() for _ in range(10 ** 7)))
fp = open('floats.bin', 'wb')
floats.tofile(fp)
fp.close()
floats2 = array('d')
fp = open('floats.bin', 'rb')
floats2.fromfile(fp, 10 ** 7)
fp.close()
```

###### 内存视图

memoryview是一个内置类，它能让用户在不复制内容的情况下操作同一个数组的不同切片。内存视图其实是泛化和去数学化的NumPy数组。它让你在不需要复制内容的前提下，在数据结构之间共享内存。其中数据结构可以是任何形式，比如PIL图片、SQLite数据库和NumPy的数组，等等。这个功能在处理大型数据集合的时候非常重要。

```
# 通过改变数组中的一个字节来更新数组里某个元素的值
>>> numbers = array.array('h', [-2,-1, 0, 1, 2])
>>> memv = memoryview(numbers) 
>>> len(memv)
5
>>> memv[0] 
-2
>>> memv_oct = memv.cast('B')  
>>> memv_oct.tolist（　） 
[254, 255, 255, 255, 0, 0, 1, 0, 2, 0]
>>> memv_oct[5] = 4  
>>> numbers
array('h', [-2,-1, 1024, 1, 2])  
```

###### deque

```
>>> from collections import deque
>>> dq = deque(range(10), maxlen=10)  ➊
>>> dq
deque([0, 1, 2, 3, 4, 5, 6, 7, 8, 9], maxlen=10)
>>> dq.rotate(3)  ➋
>>> dq
deque([7, 8, 9, 0, 1, 2, 3, 4, 5, 6], maxlen=10)
>>> dq.rotate(-4)
>>> dq
deque([1, 2, 3, 4, 5, 6, 7, 8, 9, 0], maxlen=10)
>>> dq.appendleft(-1)  ➌
>>> dq
deque([-1, 1, 2, 3, 4, 5, 6, 7, 8, 9], maxlen=10)
>>> dq.extend([11, 22, 33])  ➍
>>> dq
deque([3, 4, 5, 6, 7, 8, 9, 11, 22, 33], maxlen=10)
>>> dq.extendleft([10, 20, 30, 40])  ➎
>>> dq
deque([40, 30, 20, 10, 3, 4, 5, 6, 7, 8], maxlen=10)
```

##### 映射类结构

###### 字典

缺点：内存占用大，因为要维护一个散列表。

在做集合的迭代和更新时，不要同时进行这两个操作。

###### 集合

frozenset():返回一个冻结的集合，冻结后的集合不能再添加或者删除任何元素。

在集合的关系中，有集合中的元素是另一个集合，但是普通集合本身是可变的，它的实例不能放到另一个集合中（set中的元素必须是不可变的）。所以 frozenset提供了不可变集合。

##### 编码和解码

编码：把码位转换成字节序列的过程。

解码：把字节序列转换成码位的过程。
