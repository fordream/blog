Title:命令行指定Java class path的坑
Date:2015-08-08
Category:坑

时间：2014.07.24上午

写了一个最简单的Java class

	public class Hello{
		public static void main(String[]args){
     		System.out.println("Hello,java");
     	}
	}
然后用gradle编译打包成jar文件，运行

	java Hello -cp test.jar
报错：

	Exception in thread "main" java.lang.NoClassDefFoundError: Hello
	Caused by: java.lang.ClassNotFoundException: Hello
	    at java.net.URLClassLoader$1.run(URLClassLoader.java:202)
	    at java.security.AccessController.doPrivileged(Native Method)
	    at java.net.URLClassLoader.findClass(URLClassLoader.java:190)
	    at java.lang.ClassLoader.loadClass(ClassLoader.java:306)
	    at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:301)
	    at java.lang.ClassLoader.loadClass(ClassLoader.java:247)
	    
jar tvf test.jar。很明显Hello.class存在于jar中

	0 Thu Jul 24 11:27:00 CST 2014 META-INF/
    25 Thu Jul 24 11:27:00 CST 2014 META-INF/MANIFEST.MF
	517 Thu Jul 24 11:26:56 CST 2014 Hello.class
	
非常诡异，google半天无发现。然后灵机一动，调整了参数顺序：

	java -cp ScalaTest.jar Hello
	
成功。。。。。。

对这种命令行无力吐槽。