---
layout:     post
title:      2017.3.28大一的基础学习记录
subtitle:   旧的回忆,慢慢积累
date:       2018-09-11
author:     YELLOW
header-img: img/post-bg-rwd.jpg
catalog: true
tags:
    - 笔记
    - 个人
---

# 3.28.2017
## IO流
IO流可以实现将程序的数据向文件或其他端口输出数据，java。IO.提供的流类型主要继承了输出流，输入流，字节流，字符流。是数据源和程序之间的连接通道。
```
int b = 0;
FileInputStream in = null;
FileOutputStream out = null;
try{
    in = new FileInputStream("test");//文件地址
    out = new FileOutputStream("test");
    while((b = in.read())!=-1){//读取一个字节，如果读取不到则返回-1，自动移动读取
        out.write(b);
    }
    in.close();
    out.close();
}catch(FileNotFoundExcetpion e){
    System.out.println("~~");//错误提示
}catch(IOException e){//read方法的异常
    System.out.println("!!!");
}
```
以上为文件的复制

除了FileInputStream外还有不同的流，带缓冲区的流Buffered，例：
```
try{
    BufferedInputStream bis = new BufferedInputStream(new FileInputStream("test");
    int c = 0;
    System.out.println(bis.read());
    bis.mark(100);//标记到第100个字节，以这个点为初始位置开始读取
    for(int i = 0; i<10&&(c = bis.read()!=-1;i++){
        System.out.println(c);//输出C
    }
      bis.reset();重新设置，文件指针回到标记处
      for(int i = 0;i<10&&(c = bis.read())!-1;i++){
          System.out.println(c);
      }
      bis.close();
}catch(IOExcepiton e){
    e.printlnStackTrace();
}
bis.newLine();//对文件换行
bis.fulsh();//将管道中的数据全部输入
bis.
bis.readLine();//一次读一行的字节
```
转换流将In/outputStream 转换成Reader/Writer,进行更多字节的读取

数据流DateIn/outputStream直接读入读取数据

print流，输出流，只能输出不能输入

Object流，直接输出输入某个对象，输出输入的对象必须implements Serializable
class T implements Serializable

==**流的报错问题比较频繁，在读取文件的时候很容易报错，Object的readObject方法从文件里读取容器的时候会抛EOFExcepiton，显示流的读取超过了文件的末端**==

# 3.29
# 线程
 线程额概念即是一个程序不同的执行路径。既可以有多个“同时”进行的路径。
 例：
 ```
 Runner r = new Runner();
 //r.run();//run方法不会出现多个线程，和平常的程序一样需要等run进行返回才能继续运行main方法
 Thread t = new Thread(r);//创建一个线程
 t.start();//线程准备就绪
 
 class Runner implements Runable{
     
 }
 ```
 线程的生命周期
 创建——>start(()——>就绪状态——>运行状态——>终止
                      ↓         ↓
                    阻塞解除  阻塞事件
                      ↓         ↑
                        阻塞状态
线程的常用方法有：
start() 使线程进入就绪状态
run() 定义线程的执行方法，一旦执行完run方法，线程就进入死亡状态
sleep(int) 使线程休眠，单位是毫秒，休眠的线程不占用CPU时间片
isAlive() 判断线程是否还存活
currentThread() 返回当前占用CPU的线程
interrupt() 强制让处于睡眠状态的线程运行
join() 使两个线程合并一起，合并后，需要等待某个线程的返回值才能进行、
yield() 让出CPU时间片，让其他线程进行。 

线程的优先级
Thread.MIN_PRIORTITY = 1;
Thread.MAX_PRIORITY  = 10;
Tread.NORM_PRITRITY = 5;
使用以下方法，设置优先级
  int getPriotity();
  void setPriority();


## 线程的同步
多个线程相互协调，比如，当多个线程访问同一个变量，而且一个线程对变量作出修改的时候，对这种事件的处理即是线程的同步。

在处理线程同步时，要做的第一件事就是把修改的数据的方法用关键字synchronized进行修饰，当一个线程A使用了这个方法，另外一个线程必须等A使用完才能使用者个方法。
关键字：synchronized对对象或方法进行锁定。

关键字：wait(), notifyAll和notify 使用wait方法可以中断方法的执行，使本线程等待，让出CPU的使用权，并且运行其他线程使用者个方法，其他线程如果在使用其他方法的时候不需要等待，则用notifyAll方法来通知所欲的使用这个方法的线程结束等待，wait的线程就会重新run,如果使用notify方法则只提醒一个线程结束等待

# 3.30
# 网络
将服务端和客户端建立连接需要两个类，
```
public class TCPServer{
    public static void main(String args[]){
while(true){
SewerSocket ss - new ServerSocket(6666);//端口，随意选择
DateInputStream dis = new DateInputStream(S.getInputStream());
Socket s = ss.accept();//是否接受连接，属于阻塞式，直到有端口连接。
System.out.println(dis.readUTF());//阻塞式，直到客户端写的东西过来
dis.flush();
dis.close();
s.close();
 }
}//以上为服务端的建立

public class TCPClient{
    public static void main(String args[]){
        Sockets s = new Socket("自己的IP地址",6666); //端口必须与服务端一样
        OutputStream os = s.getOutputStream();//得到输出管道
        DateOutputStream dos = new DateOutputStream(os);
        dis.writeUTF("!~~~~");//传输数据给服务端
        dos.flush();
        dos.close();
        dos.close();
    }
}//以上为客户端的建立
```
网络这一块只为兴趣了解，暂时不作太多接触。

# 3.31
开始Android的学习
了解Android程序框架
src 为防止代码的地方\
gen 有一个R.java文件，添加的任何资源都会在其中生成相应的资源id，这个文件永远不要手动修改它\
assets 存放一些随程序打包的文件\
bin 包含了一些在编译时自动产生的文件
还有其他部分等。

onCreat 中的setContentView来给当前的活动加载一个布局，用R.layout.布局文件名可以得到布局。
其余还有AndroidManifest中文件的注册，在活动中使用Toast等一些简单的用法。
给控件注册：
```
Button button1 = (Button)findViewById(R.id.button1);
```
其余控件的注册差不多，必须进行强制转换，还有挺多比较杂的知识不列举。

# 4.1
身体不舒服休息的一天。

# 4.2
## 活动的生命周期
## 活动状态
1.运行状态 一个活动位于返回栈的栈顶\
2.暂停状态，不处于返回栈的栈顶但仍然课件\
3.停滞状态，不处于栈顶并且完全不可见，系统仍然会为其提供成员变量，但不可靠，可能会被系统回收\
4.销毁状态，当一个活动从返回栈中移除后就变成销毁状态，系统会最倾向于回收处于这样状态的活动。\
## 活动的生存期
1.oncreate() 活动初始化时调用\
2.onStart() 活动由不可见变为可见时候调用\
3.onResume() 活动准备好喝用户进行交互的时候调用，此时活动必须处于返回栈栈顶\
4.onpause() 系统准备去启动或者回复一个活动的时候调用，将一些CPU资源释放掉\
5.onStop() 活动在完全不可见的时候调用，如果活动是对话框形式则调用onpause\
6.onDestroy() 这个方法在活动被销毁前使用，之后的活动变为销毁状态\
7.onRestart() 活动由停止变为运行前调用，活动从新启动。\
具体定义比较含糊，还是等实际用起来才能比较清晰

## 活动的启动模式
1.standard 默认启动模式，系统不会子阿虎这个活动是否在返回栈中存在，每次启动都会创建该活动的一个新的实例。\
2.singleTop 在启动活动时如果发现返回栈的栈顶已经是该活动，则认为可以直接使用它，不会再创建新的活动来实例。\
3.singleTask 每次启动该活动时系统首先会再返回栈中检查是否存在该活动的实例，如果有则直接使用该实例，并把这之上的所有活动统统出栈，如果没有就会创建一个新的活动实例\
4.singleInstance 在这种模式下回有一个单独的返回来管理者个活动，不管是哪个应用程序来访问这个程序，都共用同一个返回栈。

更改活动启动模式的方法：
```
<activity>
android:launchMode = "singleInstance">
```

# 4.3
学习了些常见控件的使用，TextView，button，EditText，ImageView。
比较多样化的是Button事件的监听器，
## 实现OnclickListener事件
1.实现View.OnclickListener接口\
2.使用内部类\
3.自定义方法，配置android：onclick属性

```
内部类实现
b1 = （Button) findViewById(R.id.Button);
b1.setOnclickListener(new View.OnclickListener){
    public void onclick(View v){
        按键方法
    }
}
```
```
实现接口
public class MainActivity implements OnClickListener{
    private Button button;
    protected void onCreate(Bundle savedInstanceState){
    button = (Button)findViewById(R.id.button);
    button.setOnlclickListener(this);
    }
    public void onclick(View v){
        switch(v.getId(){
            case R.id.button:
                break;
            default:
                break;
        }
    }
}

