1. Small/Short!
    - 代码和缩进也应该保持不超过一行了；缩进层级不应该多于一层或两层
    - 函数就是越短越好！
 
2. Do one thing
    - FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY.
    - 判断一个函数是否只做了一件事只需要看其是否能再拆出一个函数
  
3. One Level of Abstraction per Function（为了保证函数只做一件事，函数中的语句都要在同一抽象层级上

4. 关于switch statement，可以参考其他设计方法尽可能化简

5. Use Descriptive Names
    - Don’t be afraid to make a name long. A long descriptive name is better than a short enigmatic name. 
 
6. Function Arguments
    - The ideal number of arguments for a function is zero (niladic). Next comes one (monadic), followed closely by two (dyadic). Three arguments (triadic) should be avoided where possible
    最好的参数数是0， 最好不要超过三个参数！
    - Arguments are even harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly. 
    参数越多，test 越难
    - Output arguments are harder to understand than input arguments. When we read a function, we are used to the idea of information going in to the function through arguments
and out through the return value. We don’t usually expect information to be going out through the arguments. So output arguments often cause us to do a double-take 
一般不会期望信息通过参数输出，而是return， 所以这会很让人困扰。。。
    - Flag arguments are ugly，  比如 render(boolean isSuite) helps a little, but not that much.最好是拆成两个: renderForSuite() and renderForSingleTest().
    - 二元函数比如笛卡尔坐标这种很合理，两个非自然的组合及排序的参数就会让人困惑。比如即便这个 assertEquals(expected, actual) 你也需要时时搞清楚expect 和actual的位置
    - 三元函数： 请慎之又慎！！  稍微比较好一点的： assertEquals(1.0, amount, .001).
    - 一旦需要两个及以上的函数参数，就请考虑写成class/objects  (Argument Objects)
    - Arguments List: 有时候我们需要传入可变数量的参数，那么有时候就相当于一个list 了！
    - 动词与关键字  Choosing good names for a function can go a long way toward explaining the intent of the function and the order and intent of the arguments
    write(name) 不错， 更好的：writeField(name) =》 我们要write 一个field 是name
    
7. Have no side effects
    - 有些函数可能会有hiden effects， 比如一个函数调用另一个函数来做某件事，那么可能就会有时序性问题
    - 避免output arguments 比如 appendFooter(s) =》report.appendFooter()
 
8. Command Query Separation：分离指令和询问
    - 函数要么做什么事 要么回答 什么事， 二者不可兼得 比如 public boolean set(String attribute, String value); 根据attribute 存不存在再set 某个值就很confusing
    好的做法：
    if (attributeExists("username")) {
        setAttribute("username", "unclebob");
        ... }
      
9. Prefer Exceptions to Returning Error Codes
   利用错误代码返回时，是在要求调用者立刻处理错误，容易导致更深层次的嵌套
   最好使用throw exception
   - 抽离 try catch！ 丑陋不堪！
   ```
    public void delete(Page page) {
       try {
       deletePageAndAllReferences(page);
       }
       catch (Exception e) {
       logError(e);
          }
       }
       
    private void deletePageAndAllReferences(Page page) throws Exception {
       deletePage(page);
       registry.deleteReference(page.name);
       configKeys.deleteKey(page.name.makeKey());
       }
       
    private void logError(Exception e) {
       logger.log(e.getMessage());
       }
     ```
    
    - Error Handling is ONE thing. 错误处理本身就是一件事了！
    if the keyword try exists in a function, it should be the very first word in the function and that there should be nothing after the catch/finally blocks
   
    - 在利用error Enum/ Error code 的时候会造成依赖！ 很多地方需要import这个class了
    比如 
    ```
    public enum Error {
      OK,
      INVALID,
      NO_SUCH,
      LOCKED,
      OUT_OF_RESOURCES,
      WAITING_FOR_EVENT;
      }
     ```
  
10. Don't Repeat Yourself
    - Repeat code can be a multiple-fold opportunity for an error of omission
    - Duplication may be the root of all evil in software

11. Structured Programming
    - every function, and every block within a function, should have one entry and one exit.(即函数中只应该有一个return =》 循环中不应该有break/continue） 
    对小函数用处不大，用时候return/break/continue 很不错，只需我们尽力保持函数短小
  
12. 那么，药（要）在哪里（怎样）才能买（做）的到呢？
    - 刚开始写出来可能都丑， 尽力打磨



    
 
