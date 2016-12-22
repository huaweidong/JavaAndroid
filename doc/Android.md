# Android入门

## 简介

### 框架

* 应用程序框架支持组件的重用与替换（app发布时遵守了框架的约定，其他app也可以使用该模块）
* Dalvik虚拟机:专门为移动设备优化 -集成的浏览器:开源的WebKit引擎
* SQLite结构化的数据存储
* 优化的图形库,多媒体支持,GSM电话技术,蓝牙等
* 采用软件叠层方式构建

![framework](http://www.runoob.com/wp-content/uploads/2015/06/16510882.jpg)

Libraries(库) + Android Runtime(Android运行时) Android给我们提供了一组C/C++库，为平台的不同组件所使用，比如媒体框架；而Android Runtime则由Android核心库集 + Dalvik虚拟机构成，Dalvik虚拟机是针对移动设备的虚拟机，它的特点:不需要很快的CPU计算速度和大量的内存空间;而每个App都单独地运行在单独的Dalvik虚拟机内每个app对于一条Dalvik进程）

简单运行流程如下：

![](http://www.runoob.com/wp-content/uploads/2015/06/12352621.jpg)

### 术语

* Dalvik： Android特有的虚拟机,和JVM不同,Dalvik虚拟机非常适合在移动终端上使用!
* AVD： (android virtual machine):安卓虚拟设备,就是安卓的模拟器
* ADT： (android development tools)安卓开发工具
* SDK：(software development kit)软件开发工具包,就是安卓系统,平台架构等的工具集合,如adb.exe
* DDMS：(dalvik debug monitor service)安卓调试工具
* adb：安卓调试桥,在sdk的platform-tools目录下,功能很多,命令行必备
* DX工具：将.class转换成.dex文件
* AAPT：(android asset packing tool),安卓资源打包工具
* R.java文件：由aapt工具根据App中的资源文件自动生成,可以理解为资源字典
* AndroidManifest.xml：app包名 + 组件声明 + 程序兼容的最低版本 + 所需权限等程序的配置文件

### adb

![adb](http://www.runoob.com/wp-content/uploads/2015/06/95349283.jpg)

### APP打包安装流程

![](http://www.runoob.com/wp-content/uploads/2015/06/5918079.jpg)

![](http://www.runoob.com/wp-content/uploads/2015/06/30239720.jpg)

### 目录结构

![](http://www.runoob.com/wp-content/uploads/2015/06/36216159.jpg)

* src目录：包含App所需的全部程序代码文件，我们大多数时候都是在这里编写我们的Java代码的
* gen目录：只关注R.java文件，它是由ADT自动产生的，里面定义了一个R类，可以看作一个id(资源编号)的字典，包含了用户界面，图形，字符串等资源的id，而我们平时使用资源也是通过R文件来调用的，同时编译器也会看这个资源列表，没有用到的资源不会被编译进去，可以为App节省空间
* assets目录：存放资源，而且不会再R.java文件下生成资源id，需要使用AssetsManager类进行访问
* libs目录：存放一些jar包，比如v4,v7的兼容包，又或者是第三方的一些包
* res资源目录：存放资源的，drawable：存放图片资源；layout：存放界面的布局文件，都是XML文件； values：包含使用XML格式的参数的描述文件，如string.xml字符串，color.xml颜色，style.xml风格样式等
* AndroidManifest.xml配置文件：系统的控制文件，用于告诉Android系统App所包含的一些基本信息，比如组件，资源，以及需要的权限，以及兼容的最低版本的SDK等

使用mipmap会在图片缩放在提供一定的性能优化，分辨率不同系统会根据屏幕分辨率来选择hdpi，mdpi，xmdpi，xxhdpi下的对应图片。本该加载ldpi文件夹下的图片资源,但是ldpi下没有,那么加载的还会是hdpi下的图片hdpi,mdpi目录下有,ldpi下没有,那么会加载mdpi中的资源! 原则是使用最接近的密度级别!另外如果你想禁止Android不跟随屏幕密度加载不同文件夹的资源,只需在AndroidManifest.xml文件中添加android:anyDensity="false"字段即可!

### res资源

1. 图片：
   1. drawable: 存放位图
   2. mipmap-hdpi(高)/mipmap-mdpi(中等)/mipmap-xhdpi/mipmap-xxhdpi/mipmap-xxxhdpi
2. layout
3. values:
   1. demens.xml：定义尺寸资源
   2. string.xml：定义字符串资源
   3. styles.xml：定义样式资源
   4. colors.xml：定义颜色资源
   5. arrays.xml：定义数组资源
   6. attrs.xml：自定义控件时用的较多，自定义控件的属性！
   7. theme主题文件
4. raw: 用于存放各种原生资源(音频，视频，一些XML文件等)，我们可以通过openRawResource(int id)来获得资源的二进制流！
5. 动画：
   1. animator：存放属性动画的XML文件
   2. anim：存放补间动画的XML文件

Java代码使用

```java
txtName.setText(getResources().getText(R.string.name));
imgIcon.setBackgroundDrawableResource(R.drawable.icon);
txtName.setTextColor(getResouces().getColor(R.color.red)); 
setContentView(R.layout.main);
txtName = (TextView)findViewById(R.id.txt_name);
```

xml使用

```xml
<TextView android:text="@string/hello_world" android:layout_width="wrap_content" android:layout_height="wrap_content" android:background = "@drawable/img_back"/>
```

### AndroidManifest.xml配置文件

```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    package="jay.com.example.firstapp" >

    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:theme="@style/AppTheme" >
        <activity
            android:name=".MainActivity"
            android:label="@string/app_name" >	<!--name报考所在的包和app名，前面部分可以用.表示-->
            <intent-filter>
                <action android:name="android.intent.action.MAIN" /> <!--决定程序的入口-->
                <category android:name="android.intent.category.LAUNCHER" /> <!--被显示在Home的程序列表中-->
            </intent-filter>
        </activity>
    </application>

</manifest>
```

除以上内容外

>①如果app包含其他组件的话,都要使用类型说明语法在该文件中进行声明 Server:元素 BroadcastReceiver元素 ContentProvider元素 IntentFilter<intent-filter>元素。
>②权限的声明: 在该文件中显式地声明程序需要的权限。android.permission.SEND_SMS 有这句话表示app需要使用发送信息的权限,安装的时候就会提示用户。

### 签名

作用：

1. **应用程序升级**：如果你希望用户无缝升级到新的版本，那么你必须用同一个证书进行签名。这是由于只有以同一个证书签名，系统才会允许安装升级的应用程序。如果你采用了不同的证书，那么系统会要求你的应用程序采用不同的包名称，在这种情况下相当于安装了一个全新的应用程序。如果想升级应用程序，签名证书要相同，包名称要相同。
2. **应用程序模块化**： Android系统可以允许同一个证书签名的多个应用程序在一个进程里运行，系统实际把他们作为一个单个的应用程序，此时就可以把我们的应用程序以模块的方式进行部署，而用户可以独立的升级其中的一个模块。
3. **代码或者数据共享**： Android提供了基于签名的权限机制，那么一个应用程序就可以为另一个以相同证书签名的应用程序公开自己的功能。以同一个证书对多个应用程序进行签名，利用基于签名的权限检查，你就可以在应用程序间以安全的方式共享代码和数据了。 不同的应用程序之间，想共享数据，或者共享代码，那么要让他们运行在同一个进程中，而且要让他们用相同的证书签名。 

方法：

1. 默认生成的apk在：app/build/outputs/apk目录下

2. Build -> Generate Signed APK...按步骤执行即可

   ![](http://www.runoob.com/wp-content/uploads/2015/06/44688629.jpg)

3. 验证：

   ```
   jarsigner -verbose -certs -verify app-release.apk
   ```

### 反编译

1. apktool：获取资源文件，提取图片文件，布局文件，还有一些XML的资源文件
2. dex2jar：将APK反编译成Java源码(将classes.dex转化为jar文件)
3. jd-gui：查看2中转换后的jar文件，即查看Java文件

### 代码混淆

代码混淆（Obfuscated code）亦称花指令，是将计算机程序的代码，转换成一种功能上等价，但是难于阅读和理解的形式的行为。混淆的目的是为了加大反编译的成本，但是并不能彻底防止反编译。

代码混淆影响到的元素有：类名、变量名、方法名、报名、其他元素。

代码混淆方法：将build.gradle里的minifyEnabled设置为true即可。

详见[这里](http://blog.csdn.net/qq_35224673/article/details/52038093)

## UI

所有Android可显示元素都是View和ViewGroup，View是显示的控件，ViewGroup是容器。

### 布局

#### LinearLayout

![](http://www.runoob.com/wp-content/uploads/2015/07/15116314.jpg)

layout_weight

1. layout_width=0时，按比例分配
2. layout_width=wrap_content，也是按比例分配
3. layout_width=match_parent(fill_parent)时，需计算。layout_weight的真实含义是：**View的宽度等于原有宽度(android:layout_width)加上剩余空间的占比**，例如1:2，两个都是fill_parent，那么总宽是2L，剩余宽度是L-2L=-L，左边宽度=L+1/3*(-L)=2/3，右边宽度=L+2/3*(-L) = 1/3.

```java
setLayoutParams(new LayoutParams(LayoutParams.FILL_PARENT, LayoutParams.WRAP_CONTENT, 1)); 
```

分割线

1. View法

2. 使用LinearLayout的一个divider属性：

   ```xml
   android:divider="@drawable/ktv_line_div"  
   android:showDividers="middle"
   android:dividerPadding="10dp"  
   ```

gravity

当 android:orientation="vertical" 时， 只有水平方向的设置才起作用，垂直方向的设置不起作用。 即：left，right，center_horizontal 是生效的。 

当 android:orientation="horizontal" 时， 只有垂直方向的设置才起作用，水平方向的设置不起作用。 即：top，bottom，center_vertical 是生效的。

所以：在一个LinearLayout的水平方向中布置两个TextView,想让一个左，一个右，没法搞，得用RelativeLayout.

#### RelativeLayout

![](http://www.runoob.com/wp-content/uploads/2015/07/797932661.png)

margin针对的是容器中的组件，而padding针对的是组件中的元素。

margin可以设置为负数。

#### TableLayout

#### FrameLayout

#### AbsoluteLayout

#### GridLayout

### TextView

### EditText

### Button&ImageButton

### ImageView

### RadioButton&CheckBox

### ToggleButton&Switch

### ProgressBar

### SeekBar

### RatingBar

### ScrollView

### Date&Time

### Adapter

### LIstView

### BaseAdapter

### GridView

### Spinner

### AutoCompleteTextView

### ExpandableListView

### ViewFlipper

### Toast

### Notification

### AlertDialog

### PopupWindow

### Menu

### ViewPager

### DrawerLayout







