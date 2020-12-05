### 味道与启发

#### things lookings bad:
1. Comments
  - Inappropriate Information
  - Obsolete Comment
  - Redundant Comment
  - Poorly Written Comment
  - Commented-Out Code (just delete them in the source control system)
  
2. Environment
  - Build Requires More Than One Step => Building a project should be a single trivial operation. 
  - Tests Require More Than One Step = > You should be able to run all the unit tests with just one command. 

3. Functions
  - Too Many Arguments => Functions should have a small number of arguments. No argument is best, followed by one, two, and three. 
  - Output Arguments => Readers expect arguments to be inputs, not outputs.
  - Flag Arguments => Boolean arguments loudly declare that the function does more than one thing. They are confusing and should be eliminated.
  - Dead Function => Methods that are never called should be discarded. Keeping dead code around is wasteful. Don’t be afraid to delete the function. Remember, your source code control system still remembers it.
  
4. GENERAL
  - Multiple Languages in One Source File
  - Obvious Behavior Is Unimplemented
  - Incorrect Behavior at the Boundaries
  
    Don’t rely on your intuition. Look for every boundary condition and write a test for it.
    
  - Overridden Safeties 忽视安全， 不要随意忽视警告 掩耳盗铃
  - Duplication 
  - Code at Wrong Level of Abstraction
    
    We want all the lower level concepts to be in the derivatives and all the higher level concepts to be in the base class.
    
  - Base Classes Depending on Their Derivatives
    When we see base classes mentioning the names of their derivatives, we suspect a problem. In general, base classes should know nothing about their derivatives.
   
  - Too Much Information
 
    Concentrate on keeping interfaces very tight and very small. Help keep coupling low by limiting information.
  
  - Dead Code
  
    Dead code is code that isn’t executed. When you find dead code, do the right thing. Give it a decent burial. Delete it from the system.
    
  - Vertical Separation
  
    Local variables should be declared just above their first usage and should have a small vertical scope. We don’t want local variables declared hundreds of lines distant from their usages.
    
  - Inconsistency
  - Clutter（混淆视听）
    
    Of what use is a default constructor with no implementation? All it serves to do is clutter up the code with meaningless artifacts. Variables that aren’t used, functions that are never called, comments that add no information, and so forth.
    没有实现的构造器有什么用 没有用到的变量，从不调用的函数，没有信息量的注释， 都是应该移除的废物
  
 - Artificial Coupling
 
    不相互依赖的东西不该耦合
 - Feature Envy（特性依恋）
 
    The methods of a class should be interested in the variables and functions of the class they belong to, and not the variables and functions of other classes. 
    
    ```
      public class HourlyPayCalculator {

       public Money calculateWeeklyPay(HourlyEmployee e) {

         int tenthRate = e.getTenthRate().getPennies();

         int tenthsWorked = e.getTenthsWorked();

         int straightTime = Math.min(400, tenthsWorked);

         int overTime = Math.max(0, tenthsWorked - straightTime);

         int straightPay = straightTime * tenthRate;

         int overtimePay = (int)Math.round(overTime*tenthRate*1.5);

         return new Money(straightPay + overtimePay);
           }
         }
       
     ```
   The calculateWeeklyPay method reaches into the HourlyEmployee object to get the data on which it operates. (NO GOOD!)
  
 - Selector Arguments
 
    ```
      public int calculateWeeklyPay(boolean overtime) {

       int tenthRate = getTenthRate();

       int tenthsWorked = getTenthsWorked();

       int straightTime = Math.min(400, tenthsWorked);

       int overTime = Math.max(0, tenthsWorked - straightTime);

       int straightPay = straightTime * tenthRate;

       double overtimeRate = overtime ? 1.5 : 1.0 * tenthRate;

       int overtimePay = (int)Math.round(overTime*overtimeRate);

       return straightPay + overtimePay;

       }

    ``` 
  you have to remember what overtime means in the function (NO GOOD!)
  
  Of course, selectors need not be boolean. They can be enums, integers, or any other type of argument that is used to select the behavior of the function. In general it is better to have many functions than to pass some code into a function to select the behavior.

- Obscured Intent
  
  代码要尽可能具有表达力， 下面这个东西就 很难理解
    ```
       public int m_otCalc() {

     return iThsWkd * iThsRte +

       (int) Math.round(0.5 * iThsRte *

         Math.max(0, iThsWkd - 400)

       );

      }
    ```
  
- Misplaced Responsibility

  make wise decision on where to put code; put a place easy for people not only u!
  
- Inappropriate Static
  
  In general you should prefer nonstatic methods to static methods. When in doubt, make the function nonstatic. If you really want a function to be static, make sure that there is no chance that you’ll want it to behave polymorphically.

- Use Explanatory Variables
  
  One of the more powerful ways to make a program readable is to break the calculations up into intermediate values that are held in variables with meaningful names.
  
    ```
      Matcher match = headerPattern.matcher(line);

       if(match.find())

       {

         String key = match.group(1);

         String value = match.group(2);

         headers.put(key.toLowerCase(), value);

       }
     ```
   
 解释了中间步骤的意思
 
- Function Names Should Say What They Do
- Understand the Algorithm
- Make Logical Dependencies Physical

  If one module depends upon another, that dependency should be physical, not just logical. 比如我要打印一个文件，那么page size 不应该作为常量形成一个logic 依赖，而应该是 get page size ，仅仅成为一个物理依赖
   
- Prefer Polymorphism to If/Else or Switch/Case

  consider polymorphism before using a switch.

- Follow Standard Conventions
- Replace Magic Numbers with Named Constants
- Be Precise 准确
  
  Ambiguities and imprecision in code are either a result of disagreements or laziness. In either case they should be eliminated.
  
- Structure over Convention 结构往往比约定更重要
  
  比如 用基类和具体类 比switch 更好
  
- Encapsulate Conditionals
  
  Boolean logic is hard enough to understand without having to see it in the context of an if or while statement. Extract functions that explain the intent of the conditional.
  比如  if (shouldBeDeleted(timer)) 比 if (timer.hasExpired() && !timer.isRecurrent()) 更好
  
- Avoid Negative Conditionals
  
  否定比肯定难明白一些，尽可能将 条件式改为 肯定的形式， 比如 if (buffer.shouldCompact()) 比 if (!buffer.shouldNotCompact()) 好
  
- Functions Should Do One Thing
- Hidden Temporal Couplings（掩蔽时序耦合）=》 不应该！！！
  
    ```
        public class MoogDiver {

         Gradient gradient;

         List<Spline> splines;



         public void dive(String reason) {

           saturateGradient();

           reticulateSplines();

           diveForMoog(reason);

         }

         …

       }
     ```
     比如上面这段代码，是有先后顺序的， 但是却没有展现出来，这样使用者可能调用错误顺序而导致一些异常； 可以通过创建顺序队列来暴露时序耦合； 每个函数都产生出下一个函数所需的结果
     
- Don’t Be Arbitrary 不要太随意
- Encapsulate Boundary Conditions
  
  Boundary conditions are hard to keep track of. Put the processing for them in one place. Don’t let them leak all over the code. We don’t want swarms of +1s and -1s scattered hither and yon. 出现超过一次的时候就应该封装边界条件
  
- Functions Should Descend Only One Level of Abstraction
- Keep Configurable Data at High Levels
- Avoid Transitive Navigation


    


  
  



 

 
 
