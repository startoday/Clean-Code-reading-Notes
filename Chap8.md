### 边界 Boundaries

1. Using Third-Party Code
    例子： 我们想使用第三方Code Map，但是不想提供map的clear 功能， 比较整洁的做法是：
     ```
      public class Sensors {
        private Map sensors = new HashMap();
        public Sensor getById(String id) {
        return (Sensor) sensors.get(id);
        }
        //snip
        }
     ```
    这样做的话map是隐藏的
    
    **Advice** 
    
    not pass Maps (or any other interface at a boundary) around your system. If you use a boundary interface like Map, keep it inside the class, or close family
of classes, where it is used. Avoid returning it from, or accepting it as an argument to, public APIs.
    
    不要pass/return any other interface at a boundary to 公共api， 将其包含在classzhong
    
2. Exploring and Learning Boundaries

    - may be in our best interest to write tests for the third-party code we use
    - we could write some tests to explore our understanding of the third-party code.
    - 尽量写learning test 来学习这个API
    - If the third-party package changes in some way incompatible withour tests, we will find out right away
    
3. Using Code That Does Not Yet Exist
    
4. Clean Boundaries
    - Code at the boundaries needs clear separation and tests that define expectations.
    - We should avoid letting too much of our code know about the third-party particulars. 
    It’s betterto depend on something you control than on something you don’t control
   - 尽量少用第三方boundaries； 有时候需要wrap/写adptors
