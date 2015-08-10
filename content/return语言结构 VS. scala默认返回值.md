Title:return语言结构 Vs scala默认返回值
Date:2015-08-08
Category:编程语言

Scala函数默认使用最后一个语句的运行结果作为返回值。例如

def distance(a:Int,b:Int):Int={

　　a * a+b * b

}

以a * a+b * b的运行结果作为返回值。这种返回值的方式渊源于其他函数式语言Lisp/Haskell等（个人猜测）。

 在近期工作中，我写了如下的代码：
 	
	def brand_name_to_id(map:HashMap[List[Any],List[Any]])(srcs:List[Any]):List[Any]={
	    srcs(0)match {
      		case brand:String=>
	      	  if(brand.contains("_br_")){
      		    try {
	      	     List(map.get(List(brand.split("_br_")(0).toLowerCase())).get.head) //我期望在这里函数直接返回
      		    }catch {
      	      	case e:Throwable=>
      	      	  println("can't map brand name to id:"+brand)
      	      	  println(e)
      	    	}
      	  	}
      		case _=>
    	}
	    List(0)//失败情况下，在这里返回
	}
	
实际情况下，由于最后一行总是被执行，这个函数总是返回List(0)。

于是改为如下形式：

	def brand_name_to_id(map:HashMap[List[Any],List[Any]])(srcs:List[Any]):List[Any]={
    	srcs(0)match {
	      case brand:String=>
      	  	if(brand.contains("_br_")){
      	    	try {
      	      		List(map.get(List(brand.split("_br_")(0).toLowerCase())).get.head)
	      	    }catch {
      			      case e:Throwable=>
	      	      	  println("can't map brand name to id:"+brand)
      		      	  println(e)
      	      		  List(0)
      	    	}
     	   }
      		case _=> List(0)
    	}
	}
即，为在所有错误分支下返回 List(0)，必须在每个错误分支都写上 List(0)。这个例子只有两个错误分支。如果分支数目更多，将非常不方便。

这时，你将会喜欢使用下面的return写法

	def brand_name_to_id(map:HashMap[List[Any],List[Any]])(srcs:List[Any]):List[Any]={
    	srcs(0)match {
      		case brand:String=>
        		if(brand.contains("_br_")){
		          try {
           			return List(map.get(List(brand.split("_br_")(0).toLowerCase())).get.head)
		          }catch {
            		case e:Throwable=>
		              println("can't map brand name to id:"+brand)
             			 println(e)
          			}
        		}
	      case _=>
    	}
    	return List(0)
	}
	
是不是可以得出这样的结论：***return的表达能力>=Scala函数默认返回方式***？

既然已经有了return这样优良的语言结构，又何必再引入另外一种返回值方式呢？这无异于画蛇添足吧。