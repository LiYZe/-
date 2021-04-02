# 集合包

## Collecetion

用于存放多个单对象。

```bash
创建：类的构造器

增加对象；add(E)

删除对象:remove(E)

获取单个对象:get(int index)

遍历对象:iterator

判断是否存在:contains(E)

```

### List

```bash
支持放入重复的对象
```

#### ArrayList

实现代码

```bash
super();
if (initialCapacity < 0)
  throw new IllegalArgumentException("Illegal Capacity: " + initialCapacity);
this.elementData = new Object[initialCapacity];
```
创建：ArrayList()

```bash
采用数组存放对象，默认调用ArrayList(int)创建，传入值为10。创建时，实例化一个Objecet数组，并将其赋值为实例的elementData属性。
```
 
 插入对象：
 
 add(E)
 
 ```bash
 1.将已有元素加一，产生一个名为minCapacity变量
 2.minCapacity与Object数组比大小
 3.若minCapacity大于Object数组
 4.将Object数组赋值给一个新数组
 5.计算新的数组容量：当前数组大小*1.5+1
 6.若仍小于，就以minCapacity作为新的容量值
 7.调用Arrays.copyOf生成新的数组
 8.将数组的末尾赋值为传入的对象
```
add(int,E)：将元素插入指定位置

```bash
1.确保插入位置存在于数组
2.确保数组容量够用
3.将当前数组对象进行复制
4.将目前index及其后的数据往后移动一位
5.将指定的index位置赋值为传入的对象
```

删除对象：remove(E)

```bash
1.判断对象是否为NULL
2.如果为NULL：
  （1）遍历数组中已有值的元素
  （2）比较是否为NULL
  （3）如果为NULL，调用fastRemove删除对应位置的对象
3.如果不为NULL；
  （1）通过E的equals比较元素是否相同
  （2）如果相同，调用fastRemove删除对象
  
fastRemove：将index后的对象往前复制一位，并将数组的最后一个元素值设为NULL
```

获取单个对象：get(int)

```bash
1.数组范围检测
2.直接返回数组位于此位置的对象
```

遍历对象:iterator()

```bash
由ArrayList的父类AbstractList实现，每次调用iterator方法，会创建一个新的AbstractList内部类Itr的实例

hasNext():
1.比较当前指向的数组是否和数组中已有的元素大小相等
2.相等，返回false
3.不相等，返回true

next():
1.比较创建此Iterator时获取的modeCount与目前的modCount
2.如果不相等，则说明在获取next元素时，集合大小被改变，抛出 ConcurrentModificationException
3.如果相等，调用get方法获取当前位置元素
```

判断对象是否存在：contains(E)

```bash
1.遍历整个数组
2.如果E为NULL
  （1）判断已有元素是否为NULL
  （2）有，返回true
3.如果E不为NULL
  （1）判断E.euqals和元素是否相等
  （2）相等，返回true
```
#### LinkedList
实现

```bash
基于双向链表机制。以一个内部的Entry类代表集合中的元素，元素的值赋给element属性，next属性指向后一个元素，previous属性指向前一个元素
```

创建：LinkedList()

```bash
创建一个element属性为null、next属性为null以及previous属性为null的Entry对象，并赋值给全局的header属性。
执行构造器时，将header的next和previous都指向header本身，形成闭环。
```
 
 插入对象：add(E)
 
 ```bash
 1.创建一个Entry对象
 2.next指向header
 3.previous指向header.previous
```

删除对象：remove(E)

```bash
1.遍历所有元素，寻找匹配元素（方法与ArryList基本相同）
2.直接删除链表上的当前元素
3.将当前元素中的element、previous、next设置为null
```

获取单个对象：get(int)

```bash
1.判断传入的index值大小是否小于0或者大于/等于当前LinkedList的size值
2.符合上述情况
  （1）抛出IndexOutOfBoundsException
3.不符合上述情况
  （1）如果需要获取的位置小于LinkedList值的一半，则从头找到index位置所对应的next元素
  （2）从队列的尾部往前，一直找到index位置所对应的previous元素
```

遍历对象:iterator()

```bash
由ArrayList的父类AbstractList实现，每次调用iterator方法，会创建一个ListItr对象，负责保存cursor位置

hasNext():
1.判断cursor位置是否等于LinkedList的size变量
2.相等，返回true
3.不相等，返回false

next():
1.调用get方法实现
2.传入cursor位置
3.获得相应元素对象
```

判断对象是否存在：contains(E)

```bash
1.遍历所有元素
2.如果E为NULL
  （1）判断已有元素是否为NULL
  （2）有，返回true
3.如果E不为NULL
  （1）判断E.euqals和元素是否相等
  （2）相等，返回true
```
#### Vector

#### Stack

### Set

不支持放入重复的对象

#### HashSet

#### TreeSet

## Map

### HashMap

创建：HashMap()

```bash
将loadFactor设置为默认值 0.75，threshold设置为 12，创建一个大小为1的Entry对象数组
```
 
 插入对象：put(Object key,Object value)
 
 ```bash
 1.key为null
  （1）获取Entry数组中的第一个对象
  （2）遍历
  （3）将value赋值为新的value
  （4）如果遍历后，没有key属性为null的对象
  （5）获取当前数组第一个Entry对象：e
  （6）增加一个Entry对象，key为null，value为新传入的对象，next为之前获得的e
 2.key不为null
  （1）获取key对象本身的hashCode
  （2）对此hashCode做hash操作
  （3）将hash后的值与Entry对象数组的大小减一的值进行按位与操作，得出存储位置
 4.如果Entry数组大小>=threshold,将数组扩大两倍
 5.扩大时，对当前数组中的元素重新hash
 6.填充数组
 7.重新设置threshold
```
获取单个对象：get(Object key)

```bash
1.key为null则从第一个对象的进行遍历，找到，返回value，没找到，返回null；
2.key不为null，则对key进行hash和按位与操作，找到对应存储位置，获得对象，遍历，找到hash值相等且key相等的Entry对象
```

删除对象：remove(Object key)

```bash
1.过程与get类似
2.
```

遍历对象:iterator()

```bash
由ArrayList的父类AbstractList实现，每次调用iterator方法，会创建一个新的AbstractList内部类Itr的实例

hasNext():
1.比较当前指向的数组是否和数组中已有的元素大小相等
2.相等，返回false
3.不相等，返回true

next():
1.比较创建此Iterator时获取的modeCount与目前的modCount
2.如果不相等，则说明在获取next元素时，集合大小被改变，抛出 ConcurrentModificationException
3.如果相等，调用get方法获取当前位置元素
```

判断对象是否存在：contains(E)

```bash
1.遍历整个数组
2.如果E为NULL
  （1）判断已有元素是否为NULL
  （2）有，返回true
3.如果E不为NULL
  （1）判断E.euqals和元素是否相等
  （2）相等，返回true
``
