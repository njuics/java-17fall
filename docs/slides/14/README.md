
## 输入输出

<small>I/O是Java最重要的API之一</small>

<small>https://docs.oracle.com/javase/tutorial/essential/io/index.html</small>

🚺

---

## java.io

- 标准Java包
  + 定义输入/输出类
  + 支持console，files，network connections......
  + 支持raw I/O（未经处理的二进制数据），formatted I/O（经过一定编码处理后符合某种特定格式的数据）
  + 不支持绘制和显示图形界面，不支持鼠标
- 基于Stream

---

## Stream

- A ***stream*** is an abstraction of the continuous one-way flow of data.
- 流是一种有序的字节数据对象。流又分为输入流（InputStream）和输出流（OutputStream）。输入流从外部资源（文件，内存，socket等）读入字节数据到Java对象；输出流则把Java对象（字节数据等）写入到外部资源。
- 所有Java I/O都可以归类为以下两类：1.字节数据输入输出I/O；2.字符数据输入输出I/O。

---

## Stream

![](http://yp.njuics.cn:7911/Stream.jpeg)<!-- .element height="60%" width="60%" -->

---

## Stream

- Java的I/O库提供了一个称做链接（Chaining）的机制，可以将一个流处理器跟另一个流处理器首尾相接，以其中之一的输出为输入，形成一个流管道的链接。

![](http://yp.njuics.cn:7911/Chaining.jpeg)<!-- .element height="80%" width="80%" -->

---

## Input Stream

- source可以是键盘输入、磁盘文件、物理设备、另外一个程序，或者同一个程序中的数组或字符串

![](http://yp.njuics.cn:7911/InputStream.jpeg)<!-- .element height="60%" width="60%" -->

---

## Output Stream

- destination可以是控制台、磁盘文件、物理设备、另外一个程序，或者同一个程序中的数组或字符串

![](http://yp.njuics.cn:7911/OutputStream.jpeg)<!-- .element height="60%" width="60%" -->

---

## 流的特性

- FIFO：先进先出，最先写入输出流的数据最先被输入流读到
- 顺序存取：可以一个接一个地往流中写入一串字节，读出时也将按写入顺序读取一串字节，不能随机访问中间的数据。
- 只读或只写，每个流只能是输入流或输出流的一种，不能同时具备两个功能，在一个数据传输通道中，如果既要写又要读，则要分别提供两个流。

<span style="color:#0099ff">特例：RandomAccessFile</span><!-- .element: class="fragment" -->

---

## 字节流 vs 字符流

- 面向字节的流（Byte Stream）：数据的处理以字节为基本单位
  + 每次读写8位二进制，也称为二进制字节流或位流
- 面向字符的流（Character Stream）：用于字符数据的处理
  + 一次读写16位二进制，并将其作为一个字符而不是二进制位来处理

<span style="color:#0099ff">Java语言的字符编码采用的是16位的Unicode码，而普通文本文件中采用的是8位ASCII码</span><!-- .element: class="fragment" -->


---

## 面向字节的输入流

- 字节流以字节为传输单位，用来读写8位的数据，除了能够处理纯文本文件之外，还能用来处理二进制文件的数据。

---

## 面向字节的输入流

- InputStream类（抽象类）中包含一套所有输入都需要的方法，可以完成最基本的从输入流读入数据的功能。

![](http://yp.njuics.cn:7911/ByteInputStreamTree.png)<!-- .element height="60%" width="60%" -->


---

## 面向字节的输出流

- OutputStream类（抽象类）中包含一套所有输出都需要的方法，可以完成最基本的向输出流写入数据的功能。

![](http://yp.njuics.cn:7911/ByteOutputStreamTree.jpg)<!-- .element height="60%" width="60%" -->

---

## 标准输入输出

- System.in：read()方法从键盘缓冲区读入一个字节的二进制数据，返回以此字节为低位字节，高位字节为0的整型数据。
- System.out：向屏幕输出不同类型数据的方法print()和println()。
- System.err：为用户显示错误信息。print()和println()将信息输出到err流并且显示在屏幕上，以方便用户使用和调试程序。

---

## 面向字符的输入流


- <font size=6>字符流是针对字符数据的特点进行过优化的，因而提供一些面向字符的有用特性，字符流的源或目标通常是文本文件。</font>
- <font size=6>Reader和Writer的子类又可以分为两大类：一类用来从数据源读入数据或往目的地写出数据（称为节点流），另一类对数据执行某种处理（称为处理流）。</font>

---

## 面向字符的输入流

![](http://yp.njuics.cn:7911/ReaderTree.jpg)<!-- .element height="50%" width="50%" -->


---

## 面向字符的输出流

![](http://yp.njuics.cn:7911/WriterTree.jpg)<!-- .element height="60%" width="60%" -->


---

## 字节流 vs 字符流

- <font color=red>最佳实践</font>：使用带有Text I/O的字符流
  + This is preferred for text I/O because it accounts for the “local” character set and supports internationalization with little additional effort.

---

## 缓冲流

- <font size=6>为了提高数据的传输效率，引入了缓冲流（Buffered Stream）的概念，即为一个流配备一个缓冲区（Buffer），一个缓冲区就是专门用于传送数据的一块内存。</font>

- <font size=6>当向一个缓冲流写入数据时，系统将数据发送到缓冲区，而不是直接发送到外部设备。缓冲区自动记录数据，当缓冲区满时，系统将数据全部发送到相应的外部设备。</font>

- <font size=6>当从一个缓冲流中读取数据时，系统实际是从缓冲区中读取数据，当缓冲区为空时，系统就会从相关外部设备自动读取数据，并读取尽可能多的数据填满缓冲区。</font>

---

## 缓冲流

- <font color=red>最佳实践</font>：用Buffered Streams包装字节流或字符流
 + 例如：BufferedReader stdin = new BufferedReader(new InputStreamReader(System.in));

---

## 文件与目录管理

- java.io.File 管理磁盘文件和目录
  + <font size=6>每个 File 类对象表示一个磁盘文件或目录，其对象属性中包含了文件或目录的相关信息。通过调用File类提供的各种方法，能够创建、删除、重命名文件、判断文件的读写权限以及是否存在，设置和查询文件的最近修改时间等。不同操作系统具有不同的文件系统组织方式，通过使用File类对象，Java程序可以用与平台无关的、统一的方式来处理文件和目录。</font>

```java
public File(String path)
public File(String path, String name)
public File(File dir, String name)
public File(URI uri)

```

---

## File类的基本方法

```java
boolean exists();
boolean createNewFile();
boolean isFile();
boolean isDirectory();
String getName();
String getPath();
String[] list();
boolean delete();
boolean mkdir();
boolean renameTo(File newFile)

```

---

## 文件的随机读写

- public class RandomAccessFile extends Object implements DataOutput, DataInput, Closeable

- 用于随机文件的创建和访问。可以跳转到文件的任意位置读写数据。可以在随机文件中插入数据，而不破坏该文件的其他数据。程序也可以更新或删除先前存储的数据，而不用重写整个文件。

---

## 文件的随机读写

- 构造函数
```java
public RandomAccessFile(String name, String mode)
public RandomAccessFile(File file, String mode)
```
- mode表示所创建的随机读写文件的操作状态，其取值包括：
 + r:表示以只读方式打开文件
 + rw:表示以读写方式打开文件，使用该模式只用一个对象即可同时实现读写操作。

--

## 文件的压缩处理

- java.util.zip包：提供对文件的压缩和解压缩进行处理的类
- GZipOutputStream/ZipOutputStream：把数据压缩成GZip和Zip格式
- GZipInputStream/ZipInputStream：将压缩的数据进行还原

---

## Serializable

- Java序列化，就是指将一个对象转化为二进制的<font color=red>byte</font>流，然后以文件的方式进行保存，或者通过网络传输。
- java.io.Serializable 接口：对象的序列化和反序列化可以通过将对象实现Serializable接口，然后用对象的输入输出流进行读写。
- 在实现序列化时，用ObjectOutputStream实现；而反序列化时，用ObjectInputStream实现。

---

## Serializable

- <font color=red>注意：</font>Java序列化是不能序列化static变量的，因为其保存的是对象的状态，而static变量保存在全局数据区，在对象未实例化时就已经生成，属于类的状态。

---

## 序列化过程

- 凡是实现Serializable接口的类都有一个表示序列化版本标识符的静态变量：
  + private static final long serialVersionUID

- 序列化
  + 1） 创建一个对象输出流，它可以包装一个其他类型的目标输出流，如文件输出流；
  + 2） 通过对象输出流的writeObject()方法写对象。

---

## 反序列化过程


- 反序列化
  + 1） 创建一个对象输入流，它可以包装一个其他类型的源输入流，如文件输入流；
  + 2） 通过对象输入流的readObject()方法读取对象。


---

## 序列化控制

- transient保留字用来标记对象中不可序列化的域

```java
public class Foo implements java.io.Serializable{
    private int v1;
    private static double v2;
    private transient A v3 = new A();
}

class A {} //A is not serializable.
```
<font color=red>只有v1被序列化！</font>

---

## 序列化控制

- Externalizable接口
  + 实现Externalizable代替实现Serializable接口来对序列化过程进行控制。
  + Externalizable继承了Serializable接口，同时增添了两个方法：writeExternal()和readExternal()。



---

## java.nio.*

- <font size=6>Java NIO（New IO）是从Java 1.4版本开始引入的一个新的IO API，可以替代标准的Java IO API。</font>

- <font size=6>Java NIO提供了与标准IO不同的IO工作方式：</font>

 + <font size=6>Channels and Buffers（通道和缓冲区）：数据总是从通道读取到缓冲区，或者从缓冲区写入到通道中。</font>
 + <font size=6>Asynchronous IO（异步IO）：当线程从通道读取数据到缓冲区时，线程还可以进行其他事情。当数据被写入缓冲区时，线程可以继续处理它。从缓冲区写入通道也类似。</font>
 + <font size=6>Selectors （选择器）：选择器用于监听多个通道的事件，因此，单个线程可以监听多个数据通道。</font>

---

## Java NIO

- <font size=6>Channels</font>

  + <font size=6>FileChannel, DatagramChannel, SocketChannel, ServerSocketChannel...</font>

- <font size=6>Buffers</font>

  + <font size=6>ByteBuffer, CharBuffer, DoubleBuffer, FloatBuffer, IntBuffer, LongBuffer, ShortBuffer...</font>

![](http://tutorials.jenkov.com/images/java-nio/overview-channels-buffers.png)<!-- .element height="40%" width="40%" -->


---

## Java NIO

- Selector
  + <font size=6>允许单线程处理多个Channel。</font>
  + <font size=6>要使用Selector，得向Selector注册Channel，然后调用它的select()方法。这个方法会一直阻塞到某个注册的通道有事件就绪。一旦这个方法返回，线程就可以处理这些事件。</font>

![](http://tutorials.jenkov.com/images/java-nio/overview-selectors.png)<!-- .element height="40%" width="40%" -->


---

## NIO vs. IO

- IO: Steam oriented; NIO: Buffer oriented
- IO: Blocking IO;  NIO: Non-blocking IO
- NIO: selectors

---

## java.nio.file.* (from jdk7)

- 新类：java.nio.file.Files 工具类
- 新类：java.nio.file.FileSystem 抽象类
- 新类：java.nio.file.FileSystems 工厂类
- 新类：java nio.file.Paths   工具类
- 新接口：java.nio.file.Path  表示与平台无关的路径

---

## I/O异常

- java.io.IOException
  + FileNotFoundException
  + EOFException
  + InterruptedIOException
  + ObjectStreamException
  + ...

---

## I/O异常处理

```java

public static void main(String[] args){
  //code to open file
  BufferedReader input;
  try{
    input = new BufferedReader(new FileReader("test.txt"));
  }
  catch(IOException e){
    System.err.println("Error opening file");
    return;
  }
  //code to read from file
  //code to close file
} 

```


---

## Java I/O 设计模式

- 装饰器模式（Decorator）：在由InputStream，OutputStream，Reader和Writer代表的等级结构内部，有一些流处理器可以对另一些流处理器起到装饰作用， 形成新的具有改善了的功能的流处理器。装饰者模式是Java I/O库的整体设计模式

```java
  BufferedReader stdin = new BufferedReader(new InputStreamReader(System.in));
  PrinterWriter out = new PrintWriter(new BufferedWriter(new FileWriter("demo.out")));

```

---

让你的葫芦娃们和外界联系起来！

---

# END