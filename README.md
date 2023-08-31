
最小堆
## 类UML图

```mermaid
classDiagram

class T{
    <<>>
}
Heap ..> T

class Heap {
    <<abstract>>
    +insert_value(value:T)* : void %% 插入元素
    +remove_min()* : T %%取出堆顶元素
    +empty()* : void %%判断堆中是否有元素
}

MinHeap --|> Heap
MinHeap ..> T
class MinHeap {
    <<interface>>
    -Insert(value: T) : void %% 插入元素
    -DeleteMin() : void %%删除元素
    -PercolateDown(hole: Int) : void %%从第hole个位置元素开始下沉
    +insert_value(value: T) : void %% 插入元素
    +remove_min() : T %%取出堆顶元素
    +empty() : void %%判断堆中是否有元素

    -vector&#60T&#62 array %%存储堆元素的数组
    -int size %%堆的实际大小
}
```

## 插入元素函数Insert流程图
先放到末尾，再依次与父节点比较，逐渐上浮！！！
```mermaid
graph TB
A(begin)
A--输入value-->B[/判断堆的大小是否填满了array数组/]
B--是-->C1[arrary扩容为原来的两倍]-->D
B--否-->D[hole指针指向插入元素将要存储的位置,初值是已存数据的末尾]
D-->E[/判断hole指针是否指向指向堆顶元素并且待插入元素是否小于父节点/]
E--是-->F[父节点存储到hole指针指向的位置]
F-->G[hole指针指向父节点的位置]
G-->E
E--否-->F1[把待插入元素插入到hole指针指向的位置]
```
## 删除堆顶元素函数DeleteMin流程图
把最后一个元素放到开头，依次比较进行沉降！！！
```mermaid
graph TB
A(begin)
A-->B[把已存数据的最后一个元素取出来覆盖到堆顶位置]
B-->C
subgraph C[从堆顶元素位置hole开始下沉]
    C1[/判断当前hole指针指向的节点是否存在左子节点/]
    C1--存在-->C2[得到左子节点的索引给child]
    C2-->C22[/如果当前左节点不是最后一个节点,并且右子节点的值小于左子节点/]
    C22--成立-->C23[得到右子节点的索引child]
    C22--不成立-->C24
    C23-->C24[/如果当前hole节点的子节点有小于堆顶的元素/]
    C24--有-->C25[交换元素,hole节点指向孩子节点]-->C1
    C24--无-->C26-->C3
    C1--不存在-->C3[把堆顶元素存放到hole指针指向的位置]
end
```


## 注意
1. array数组初始化的第一个元素，不存放数
2. 由于第一个位置不存放元素, 
   1. 因此数组第i个位置的父节点是 i/2;
   2. 数组第i个位置的子节点是 2i, 2i+1
