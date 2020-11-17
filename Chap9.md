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
     我们可以看到这个string的方法没有很高效,但是因为stringBuffer的方法很丑陋，可以选择不使用，因为测试大概完全没有资源（CPU）的限制
  
4. One Assert per Test
    - consider! every test function in a JUnit test should have one and only one assert statement.
    - function name: given-when-then convention.
    - the number of asserts in a test ought to be minimized 不必惧怕多于一个assertion， 但是要尽可能的减少同一个test里的assertion数
  
5. Single Concept per Test
    - we want to test a single concept in each test function
    - you should minimize the number of asserts per concept and test just one concept per test function.
  
6. F.I.R.S.T.
    - **Fast** 
    
    Tests should be fast. 
    
    They should run quickly. When tests run slow, you won’t want to run them frequently. 
    
    If you don’t run them frequently, you won’t find problems early enough to fix them easily. 
    
    You won’t feel as free to clean up the code. Eventually the codewill begin to rot.
    
    - **Independent** 
    
    Tests should not depend on each other. 
    
    One test should not set up the conditions for the next test. 
    
    You should be able to run each test independently and run the tests in any order you like. 
    
    When tests depend on each other, then the first one to fail causes a cascade of downstream failures, making diagnosis difficult and hiding downstream defects.
    
    - **Repeatable**
    
    Tests should be repeatable in any environment. 
    
    You should be able to run the tests in the production environment, in the QA environment, and on your laptop whileriding home on the train without a network.
    
    If your tests aren’t repeatable in any environment, then you’ll always have an excuse for why they fail. 
    
    You’ll also find yourself unable to run the tests when the environment isn’t available.
    
    - **Self-Validating**
    
    The tests should have a boolean output. Either they pass or fail. 
    
    You should not have to read through a log file to tell whether the tests pass. 
    
    You should not have to manually compare two different text files to see whether the tests pass. 
    
    If the tests aren’t self-validating, then failure can become subjective and running the tests can require a long manual evaluation.
    
    - **Timely** 
    
    The tests need to be written in a timely fashion. 
    
    Unit tests should be written just before the production code that makes them pass. 
    
    If you write tests after the production code, then you may find the production code to be hard to test. 
    
    You may decide that some production code is too hard to test. You may not design the production code to be testable.
