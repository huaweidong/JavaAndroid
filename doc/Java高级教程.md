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

Java 提供了一种对象序列化的机制，该机制中，一个对象可以被表示为一个字节序列，该字节序列包括该对象的数据、有关对象的类型的信息和存储在对象中数据的类型。

将序列化对象写入文件之后，可以从文件中读取出来，并且对它进行反序列化，也就是说，对象的类型信息、对象的数据，还有对象中的数据类型可以用来在内存中新建对象。(google protobuf也是序列化的方法）

一个类的对象要想序列化成功，必须满足两个条件：

1. 该类必须实现 java.io.Serializable 对象。
2. 该类的所有属性必须是可序列化的。如果有一个属性不是可序列化的，则该属性必须注明是短暂的。

类ObjectInputStream 和ObjectOutputStream是高层次的数据流，它们包含序列化和反序列化对象的方法。

```java
public final void writeObject(Object x) throws IOException
public final Object readObject() throws IOException, ClassNotFoundException
```

示例：

```java
// 序列化
Employee e = new Employee();
      e.name = "Reyan Ali";
      e.address = "Phokka Kuan, Ambehta Peer";
      e.SSN = 11122333;
      e.number = 101;
FileOutputStream fileOut =
         new FileOutputStream("/tmp/employee.ser");
         ObjectOutputStream out = new ObjectOutputStream(fileOut);
         out.writeObject(e);
         out.close();
         fileOut.close();
// 反序列化
Employee e = null;
FileInputStream fileIn = new FileInputStream("/tmp/employee.ser");
         ObjectInputStream in = new ObjectInputStream(fileIn);
         e = (Employee) in.readObject();
         in.close();
         fileIn.close();
```



## 网络编程

java.net包提供了两种常见的网络协议的支持TCP和UDP

## 多线程编程

进程：一个进程包括由操作系统分配的内存空间，包含一个或多个线程。一个线程不能独立的存在，它必须是进程的一部分。一个进程一直运行，直到所有的非守候线程都结束运行后才能结束。

每一个Java线程都有一个优先级，这样有助于操作系统确定线程的调度顺序。Java优先级在MIN_PRIORITY（1）和MAX_PRIORITY（10）之间的范围内。默认情况下，每一个线程都会分配一个优先级NORM_PRIORITY（5）。

### 通过实现Runable接口

```java
class NewThread implements Runnable {
   Thread t;
   NewThread() {
      // 创建第二个新线程
      t = new Thread(this, "Demo Thread");
      System.out.println("Child thread: " + t);
      t.start(); // 开始线程
   }
   
   // 第二个线程入口
   public void run() {
      try {
         for(int i = 5; i > 0; i--) {
            System.out.println("Child Thread: " + i);
            // 暂停线程
            Thread.sleep(50);
         }
     } catch (InterruptedException e) {
         System.out.println("Child interrupted.");
     }
     System.out.println("Exiting child thread.");
   }
}
```



### 通过继承Thread类本身

```java
class NewThread extends Thread {
   NewThread() {
      // 创建第二个新线程
      super("Demo Thread");
      System.out.println("Child thread: " + this);
      start(); // 开始线程
   }
  
   // 第二个线程入口
   public void run() {
      try {
         for(int i = 5; i > 0; i--) {
            System.out.println("Child Thread: " + i);
                            // 让线程休眠一会
            Thread.sleep(50);
         }
      } catch (InterruptedException e) {
         System.out.println("Child interrupted.");
      }
      System.out.println("Exiting child thread.");
   }
}
```

Thread Method实例方法：

1. public void start(): 使该线程开始执行；Java 虚拟机调用该线程的 run 方法。
2. public void run(): 如果该线程是使用独立的 Runnable 运行对象构造的，则调用该 Runnable 对象的 run 方法；否则，该方法不执行任何操作并返回。
3. public final void setName(String name)
4. public final void setPriority(int priority)
5. public final void setDaemon(boolean on): 将该线程标记为守护线程或用户线程。
6. public final void join(long millisec): 等待该线程终止的时间最长为 millis 毫秒。
7. public void interrupt()
8. public final boolean isAlive(): 测试线程是否处于活动状态。

Thread Method静态方法：

1. void yield(): 暂停当前正在执行的线程对象，并执行其他线程。
2. void sleep(long millisec):  在指定的毫秒数内让当前正在执行的线程休眠（暂停执行），此操作受到系统计时器和调度程序精度和准确性的影响。
3. Thread currentThread(): 返回对当前正在执行的线程对象的引用。
4. void dumpStack(): 将当前线程的堆栈跟踪打印至标准错误流。



