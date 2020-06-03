## String类型理解  

```Java```字符串是由Unicode字符序列组成的。``` Java```没有没有内置的字符串类型，而是由java.lang类库中提供了一个预定义String类。

```java
public final class String
  implements java.io.Serializable, Comparable<String>, CharSequence {
  /** The value is used for character storage. */
  private final char value[];
  /** Cache the hash code for the string */
  private int hash;  // Default to 0
  ...
}
```

**String部分源码**
 1）String类被final关键字修饰，意味着String类不能被继承，并且它的成员方法都默认为final方  法；字符串一旦创建就不能再修改。
 2）String类实现了Serializable、CharSequence、 Comparable接口。
 3）String实例的值是通过字符数组实现字符串存储的。

1. **“+”连接符的实现原理**
    - 在```Java```中String对象可以使用“+”连接其他对象，其字符串连接是通过StringBuilder(或StringBuffer)类及append方法实现的，最后通过toString()方法转为String类型。

    ```java
    /**
    * 反编译前
    */
    public class Test {
       public static void main(String[] args) {
            int i = 10;
            String s = "abc";
            System.out.println(s + i);
       }
    }
    /**
    * 反编译后
    */ 
    public class Test {
        public static void main(String[] args) {
            byte byte0 = 10;     
            String s = "abc";     
            System.out.println((new StringBuilder()).append(s).append(byte0).toString());
        }
    }
    ```
    - “+”连接符的效率问题
        1)当我们使用“+”连接符时，JVM会隐式创建StringBuilder，一般情况下并不会造成效率损失，但当我们进行大量字符串拼接时则需要注意，因为会创建大量的StringBuilder在堆内存中，造成效率的损失。
        2)当”+”两端均为编译期确定的字符串常量时，编译器会进行相应的优化，直接将两个字符串常量拼接好

2. **字符串常量池**
    在Java的内存分配中，总共3种常量池，分别是Class常量池、运行时常量池、字符串常量池。
    因为字符串在程序中是常用的类，JVM为了提高性能和减少内存消耗，会在实例化字符串时会使用字符串常量池：
        1)创建字符串常量时，JVM会首先检查字符串常量池。
        2)如果该字符串已经存在常量池中，那么就直接返回常量池中的实例引用。
        3)如果字符串不存在常量池中，就会实例化该字符串并且将其放到常量池中。
        4)由于String字符串的不可变性，常量池中一定不存在两个相同的字符串。
        

    