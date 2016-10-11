##Android性能优化系列-优良的数据结构
从这一篇文章开始记录一下我工作中遇到的数据优化的例子。
如题 本篇的主体跟数据结构有关系。
程序是数据结构➕算法，良好的数据结构选择是程序性能提升的重要部分。

Android系统基于Java，我们先来看看Java的数据结构相关的知识。


Java中数据类型，

包括基本数据类型：

boolean

byte  

short 

int

char

long

float

double 

还有以String类型为代表的Object对象数据。

String

Object

基本数据类型的选用，因为基本类型开辟的是固定的内存大小，像byte的1字节 int的4字节，所以要根据你的定义变量的意义和范围来取值，比如描述一个人年龄的变量只需要选择最大取值127的byte即可，选用其他的类型比如int则会造成浪费。

关于对象的内存分两部分，分别是引用变量的内存和引用变量所指向的对象的内存，引用变量指向对象的首地址。

来看一下常用的数据结构和他们在Java语言中的表现：

数组：插入块，如果知道下标，可以非常快速的存取，但是查找和删除慢，数组在Java语言中的表现，是普通的数组和arraylist，ArrayList内部也是数组实现。

有序数组：比无序数组查找快，删除和插入慢。

栈：提供后进后出的存取操作。

队列：提供先进先出的存取操作

链表：插入快，删除快，但是查找慢。

二叉树：查找、删除、插入都快，但是算法复杂。

哈希表：如果已经知道关键字则存取极快，插入快。

堆：插入删除快，对最大数据项的存取很快。

Java中关于数据集合的API：

Collection

├List

│├LinkedList

│├ArrayList

│└Vector

│　└Stack

└Set

Map

├Hashtable

├HashMap

└WeakHashMap

collection 是一个接口，所有的元素都继承这个接口，collection内部存储元素element。Java提供的数据结构都是实现了collection接口的。

collection的所有实现类都可以使用

List list = Collections.synchronizedList(new LinkedList(...)); 
方法实现数据结构的同步。

list是有序的collection，使用list可以精确的控制每一个元素的位置，可以根据元素的下标检索元素，有点类似数组。

list常见的实现类有：

LinkedList内部实现为链表，插入删除操作快速，遍历查找比较慢。有一些额外的在首尾的操作方法。

Arraylist是大小可变的数组，内部实现是数组，插入删除的时候动态改变内部数组的大小，允许所有元素包括null，arraylist遍历查找比较迅速，插入和删除都比较慢，因为要改变数组所有元素的位置。Arraylist有一个一个参数的构造方法，是确定内部数组的初始大小的，在插入较大数据的时候可以预先指定arraylist的大小可以提高插入的效率。

vector非常类似arraylist，但是vector是线程同步的，vector使用的时候注意迭代器的ConcurrentModificationException。

stack是一个堆栈结构，继承自vector，实现一个后进先出的结构。

set是一种不包含重复元素的collection，set最多有一个null元素。set内部维护一个map，使用map的key来储存数据。

hashtable和hashmap实现键值对形式，区别是hashtable是线程同步的，注意重写key的hashcode和equals方法的时候保证结果一致。

WeakHashMap是对hashmap的key实现了弱引用。




