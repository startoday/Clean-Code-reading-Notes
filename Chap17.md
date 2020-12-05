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
