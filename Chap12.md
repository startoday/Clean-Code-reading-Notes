### 迭进 Emergence

According to Kent, a design is “simple” if it follows these rules:

• Runs all the tests

• Contains no duplication

• Expresses the intent of the programmer

• Minimizes the number of classes and methods

The rules are given in order of importance.

1. RUNS ALL THE TESTS

    The more tests we write, the more we’ll continue to push toward things that are simpler to test. So making sure our system is fully testable helps us create better designs.
    
 
2. REFACTORING

    For each few lines of code we add, we pause and reflect on the new design. Did we just degrade it? If so, we clean it up and run our tests to demonstrate that we haven’t broken anything. The fact that we have these tests eliminates the fear that cleaning up the code will break it!
    Eliminate duplication, ensure expressiveness, and minimize the number of classes and methods.
  
3. NO DUPLICATION

    Lines of code that are similar can often be massaged to look even more alike so that they can be more easily refactored. And duplication can exist in other forms such as duplication of implementation. 
    
    eg:These can be cleaned:
    The way we write these two functions, instead of do a size and a boolean checking, we can do:
    
        int size() {}
        boolean isEmpty() {}

        boolean isEmpty() {
            return 0 == size();
         }
 
4.表达力 EXPRESSIVE

  code should clearly express the intent of its author. The clearer the author can make the code, the less time others will have to spend understanding it. This will reduce defects and shrink the cost of maintenance.
    
  - good names
  - keeping your functions and classes small
  - using standard nomenclature
  - Well-written unit tests are also expressive
  - the most important way to be expressive is to try 在写好代码之后不停思考是否可以调整优化更清晰

5. MINIMAL CLASSES AND METHODS
  
  Our goal is to keep our overall system small while we are also keeping our functions and classes small. Remember, however, that this rule is the lowest priority of the four rules of Simple Design. So, although it’s important to keep class and function count low, it’s more important to have tests, eliminate duplication, and express yourself.
  
    
         
