1. Comparable v.s. Comparator
2. compile java file with jar package

	there is a problem when I am running

	`javac -cp some.jar another.java`
	
	`java -cp some.jar another`
	
		Error: Could not find or load main class SelectionBars

	试了无数种方法,最后加一个`:`解决了问题：
	
	首先documentation里是这么提到的：
	
		-classpath <class search path of directories and zip/jar files>
                  A : separated list of directories, JAR archives,
                  and ZIP archives to search for class files.

	但是比较蛋疼的是，只引用一个jar包的时候，也需要`:`
	
	`java -cp some.jar: another`
	        
	不知道别的系统上是不是也是这样。

3. Warning

		private static boolean less(Comparable v, Comparable w) {
			return (v.compareTo(w) < 0);                                                                                                                        
		}
	`warning: [unchecked] unchecked call to compareTo(T) as a member of the raw type Comparable`
	
	这里的错误，我现在理解的是，comparaTo是针对一种Item的，但这里Comparable v, w会传入不同的generic type。
	
	解决方案是：
	
		private static <T extends Comparable<? super T>> boolean less(T v, T w) {                                                                               
			return (v.compareTo(w) < 0);
		}

	解释在这里：
	`http://stackoverflow.com/questions/4830400/java-unchecked-call-to-comparetot-as-a-member-of-the-raw-type-java-lang-compa`
	
	大致意思是，如果你想使用一个generic的api，并且得到warning需要将某一个函数改成generic的，那么需要使得整个class都定义成generic的，这样，就不会出现generic type各种混乱使用的情况。