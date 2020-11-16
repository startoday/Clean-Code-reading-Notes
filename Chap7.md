### 错误处理 Error Handling

1. Use Unchecked Exceptions

2. Provide Context with Exceptions
    - Create informative error messages and pass them along with your exceptions. Instead of only print stack, which will help a lot will you debug
  
3. Define Exception Classes in Terms of a Caller’s Needs

4. Define the Normal Flow
    ```
    try {
     MealExpenses expenses = expenseReportDAO.getMeals(employee.getID());
     m_total += expenses.getTotal();
    } catch(MealExpensesNotFound e) {
     m_total += getMealPerDiem();
    }
    ```
    this cut off the flow; We can change the ExpenseReportDAO to always returns a MealExpense object.
    ```
      public class PerDiemMealExpenses implements MealExpenses {
       public int getTotal() {
       // return the per diem default
       }
      }
     ```
     This is called the SPECIAL CASE PATTERN [Fowler]. You create a class or configure an object 
     so that it handles a special case for you. When you do, the client code doesn’t have to deal with exceptional behavior. 
     That behavior is encapsulated in the special case object.
   
5. Don’t Return Null
    When there is part not handle the null, it will create some unexpected NPE from deeper code, hard to find and debug.
    We can return an empty container instead.

6. Don’t Pass Null
    Kotlin 万岁！
