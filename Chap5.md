### 格式 Formatting

" If people see a scrambled mass of code that looks like it was written by a bevy of drunken sailors, 
then they are likely to conclude that the same inattention to detail pervades every other aspect of the project"


1. The Purpose of Formatting
    - Code formatting is about communication
  
2. Vertical Formatting
    - Small files are usually easier to understand than large files are
    - Each line represents an expression or a clause, and each group of lines represents a complete thought. 每个空白行都是一条新线索
    - 垂直方向需要更靠近，要尽量更少的移动头部和眼球
    - 尽量把在关系密切的概念放在相同的文件中（所以其实应该避免使用protected， 省得读者需要在文件中跳来跳去
    - 变量声明要尽可能的靠近使用位置
    - Instance variables, on the other hand, should be declared at the top of the class. C++一般是在底部，Java是在顶部
    - Dependent Functions:相关函数  If one function calls another, they should be vertically close, the caller should be above the callee。 call 人的放在被call的上面
    - 概念相关的代码应该放的越近越好
  
3. Horizontal Formatting （一行代码应该有多宽）
    - 还是尽量减少需要滚动的次数，尽力保持代码短小
    - 注意缩进，注意while/if 等语句单行的时候 （ 我觉得似乎有了spotless 之后就不是事儿了）
    
4. Team Roles
    - 要遵循团队的规则

