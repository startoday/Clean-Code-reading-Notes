### 系统 Systems

1. Separate Constructing a System from Using It
    bad example of mix run time logic and construction 
    ```
    public Service getService() {
     if (service == null)
     service = new MyServiceImpl(...); // Good enough default for most cases?
     return service;
    }
    ```
    - This is the LAZY INITIALIZATION/EVALUATION idiom
      - merits/goodness: 只有需要用时才会创建类，少了一些overhead，所以会比较快，也可以保证null不会被return
      - badness：我们会有对MyServiceImpl的依赖 We can’t compile without resolving these dependencies, even if we never actually use an object of this type at runtime! 
        同时test也变得棘手，需要mock该对象
 2. Separation of Main
    - One way to separate construction from use is simply to move all aspects of construction to main, 
    
      or modules called by main, 

      and to design the rest of the system assuming that all objects have been constructed and wired up appropriatel.

      一个方法就是把这些建造都放到main里面/或者是main来call这些modules，其他的时候假设已经建立好这些所需的东西了
      
      图例的话就是从main指出来的箭头都指向了其他application的部分，其他部分不需要知道main的任何knowledge
      
3. Factories
