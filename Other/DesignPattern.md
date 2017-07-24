### 设计模式

> [单例模式](#单例模式)、

#### 单例模式

```java
//懒汉式	用时再加载
public class Singleton {
	private static Singleton sSingleton;
  	private Singleton() {
	}
  	public static Singleton getInstance(){
      if(sSingleton==null) {
        sSingleton=new Singleton();
      }
      return sSingleton;
  	}
}
```

