1. 单例

   * ```java
     public class AtomicSingleton  
      {  
         private static AtomicReference<AtomicSingleton> INSTANCE   
                   = new AtomicReference<>();  
         private AtomicSingleton() {}  

         public static AtomicSingleton getInstace(){  
             AtomicSingleton current = INSTANCE.get();  
             for (;;) {  
                 if(current != null){  
                     return current;  
                 }  
                 current = new AtomicSingleton();  

                 if(INSTANCE.compareAndSet(null, current))  
                 {  
                     return current;  
                 }  

             }  
         }  
     }
     ```



