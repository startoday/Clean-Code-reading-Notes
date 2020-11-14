### 注释 

“Nothing can be quite so helpful as a well-placed comment. Nothing can clutter up a module more than frivolous dogmatic comments. Nothing can be quite so damaging as an old crufty comment that propagates lies and misinformation.”


* The proper use of comments is to compensate for our failure to express ourself in code 注释的恰当用法是要弥补代码表达意图的失败

如果发现自己需要写注释，那么想想能否避免！（ 哈哈哈 赞同！shout to Nav！）
  
  - 代码常常变动，注释却不一定总能得到维护
  - 把力气花在怎么写好代码上，直接保证无须编写注释
  
1. 注释不能美好糟糕的代码

2. 用代码来阐述你的（大部分）意图

3. 好注释/也许有必要的注释？
    - 法律信息，最好用link
    Where possible, refer to a standard license or other external document rather than putting all the terms and conditions into the comment.
    - 提供信息的注释（ 但还是尽量用函数名称传达信息）
        ```
        // Returns an instance of the Responder being tested.
        protected abstract Responder responderInstance();
        ```
        ==>  不如 responderBeingTested

        好一点的例子：
        ```
        // format matched kk:mm:ss EEE, MMM dd, yyyy
        Pattern timeMatcher = Pattern.compile(
         "\\d*:\\d*:\\d* \\w*, \\w* \\d*, \\d*");
        ```
        可以，但是还是不如直接用一个class 来解释

    - 对意图的解释， 提供某个决定后的意图， 也许你不同意这个写法，但是你会知道这个程序员当时是怎么想的
    - 阐释
      Sometimes it is just helpful to translate the meaning of some obscure argument or return value into something that’s readable
      常常，确认注释正确性是难的，还是 尽量能不要就不要, 要写就要写正确
    - 警示！ 这个一般都是有必要的
    - Todo 注释
    - 强调某些东西
    - 公共api中的doc
   
4. 肯定是坏的注释
    - 喃喃自语， 如果你决定写注释，就要花必要的时间确保写出最好的注释
    - 多余的注释
    - 误导性的注释
    - 废话注释
    - 位置标记： 鸡零狗碎，应当删除
    - 右括号后的注释，应当做的只是缩短函数
    - 归属署名， 版本控制就可以干这个
    - 注释掉的代码，要么删要么留，注释在那别人也不敢动！again 版本控制知道你每次的代码
    - 信息过多。。again， 读者未必想看到你的历史趣事
    - 注释和代码没有明显联系，不然加了不如没加还惹人迷惑
  
    
    
 

  

