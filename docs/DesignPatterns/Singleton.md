- 饿汉式

```java
public class Singleton {
    private static Singleton uniqueInstance = new Singleton();
    
    private Singleton() {
    }
    
    public static Singleton getUniqueInstance() {
    	return uniqueInstance;
    }
}
```


- 懒汉式

```java
public class Singleton {
    private volatile static Singleton uniqueInstance;
    
    private Singleton() {
    }
    
    public static Singleton getUniqueInstance() {
    	if (uniqueInstance == null) {
    		synchronized (Singleton.class) {
                if (uniqueInstance == null) {
                    uniqueInstance = new Singleton();
                }
    		}
    	}
    	return uniqueInstance;
    }
}
```

