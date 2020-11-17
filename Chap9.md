### Unit Tests

1. The Three Laws of TDD
    - **First Law** You may not write production code until you have written a failing unit test.
    - **Second Law** You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
    - **Third Law** You may not write more production code than is sufficient to pass the currently failing test.
    测试和 生产代码一起编写，会导致很多的测试，可能会比较难以管理 日后
    
2. Keeping Tests Clean
    - dirty tests is equivalent to, if not worse than, having no tests 脏测试等于没测试
    - *Test code is just as important as production code*
    - The higher your test coverage, the less your fear
  
3. Clean Tests
    - What makes a clean test? Three things. **Readability, readability, and readability**. =》clarity, simplicity, and density of expression
    - BUILD-OPERATE-CHECK pattern 
    - 测试代码和生产代码可以拥有双重标准：
    这是之前的代码，看上去已经不错了，对吧
    ```
     @Test
     public void turnOnLoTempAlarmAtThreashold() throws Exception {
       hw.setTemp(WAY_TOO_COLD);
       controller.tic();
       assertTrue(hw.heaterState());
       assertTrue(hw.blowerState());
       assertFalse(hw.coolerState());
       assertFalse(hw.hiTempAlarm());
       assertTrue(hw.loTempAlarm());
     }
     ```
     但是读状态的时候我要来回扫视True/False， 并且思考，乏味且低效，来看看修改后的code， 利用大小写来区分State on/off， 一目了然，简短精悍
     ```
     @Test
     public void turnOnCoolerAndBlowerIfTooHot() throws Exception {
       tooHot();
       assertEquals("hBChl", hw.getState());
     }
     @Test
     public void turnOnHeaterAndBlowerIfTooCold() throws Exception {
       tooCold();
       assertEquals("HBchl", hw.getState());
     }

     public String getState() {
       String state = "";
       state += heater ? "H" : "h";
       state += blower ? "B" : "b";
       state += cooler ? "C" : "c";
       state += hiTempAlarm ? "H" : "h";
       state += loTempAlarm ? "L" : "l";
       return state;
     }
     ```
     我们可以看到这个string的方法没有很高效
