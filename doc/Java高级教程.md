# Java高级教程

## 数据结构

### Enumeration

Enumeration接口中定义了一些方法，通过这些方法可以枚举（一次获得一个）对象集合中的元素。

Method:

1. boolean hasMoreElements()
2. Object nextElement()

```java
import java.util.Vector;
import java.util.Enumeration;
 
public class EnumerationTester {
   public static void main(String args[]) {
      Enumeration days;
      Vector dayNames = new Vector();
      dayNames.add("Sunday");
      dayNames.add("Monday");
      dayNames.add("Tuesday");
      dayNames.add("Wednesday");
      dayNames.add("Thursday");
      dayNames.add("Friday");
      dayNames.add("Saturday");
      days = dayNames.elements();
      while (days.hasMoreElements()){
         System.out.println(days.nextElement());
      }
   }
}
```

### Bitset类

一个Bitset类创建一种特殊类型的数组来保存位值。BitSet中数组大小会随需要增加。

Method:

1. BitSet()/BitSet(int size)
2. void and(BitSet bitSet)/void andNot(BitSet bitSet)/void or(BitSet bitSet)/void xor(BitSet bitSet)
3. int cardinality()
4. void clear()/void clear(int index)/void clear(int startIndex, int endIndex)
5. Object clone()
6. boolean equals(Object bitSet)
7. void flip(int index)/void flip(int startIndex, int endIndex)
8. boolean get(int index)
9. BitSet get(int startIndex, int endIndex)
10. boolean intersects(BitSet bitSet)
11. boolean isEmpty()
12. int length()/int size()
13. int nextClearBit(int startIndex)/int nextSetBit(int startIndex)
14. void set(int index)/void set(int index, boolean v)/void set(int startIndex, int endIndex)/void set(int startIndex, int endIndex, boolean v)
15. String toString()

> [startIndex, endIndex)前闭后开

### Vector类

Vector类实现了一个动态数组。主要用在事先不知道数组的大小，或者只是需要一个可以改变大小的数组的情况。Vector是同步访问的。

Method：

1. 构造：
   1. Vector()默认大小为10
   2. Vector(int size)
   3. Vector(int size, int incr) incr是增量
   4. Vector(Collection c)
2. 添加:
   1. void add(int index, Object o)
   2. boolean add(Object o)
   3. boolean addAll(Collection c)
   4. boolean addAll(int index, Collection c)
   5. void addElement(Object o)
3. int capacity()容量
4. int size()个数
5. void clear()
6. Object clone()
7. boolean contains(Object e)/boolean containsAll(Collection c)
8. void copyInto(Object[] anArray)
9. Object elementAt(int index)
10. Enumeration elements()
11. void ensureCapacity(int minCapacity)
12. boolean equals(Object o)
13. Object firstElement()
14. Object get(int index)
15. int indexOf(Object e)/int indexOf(Object e, int index)
16. void insertElementAt(Object obj, int index)

## 集合框架

## 泛型

## 序列化

## 网络编程

## 发送邮件

## 多线程编程

## Applet基础

## 文档注释
