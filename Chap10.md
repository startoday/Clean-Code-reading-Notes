###  类 Class

1. Class Organization
  - For Java， a class should begin with a list of variables. Public static constants, if any, should come first. Then private static variables, followed by private instance variables. There is seldom a good reason to have a public variable. Java的规则，先public static const， privat static，再private，一般尽量不要用public variable
  
2. Classes Should Be Small!
  - smaller is the primary rule when it comes to designing classes. 
  - With functions we measured size by counting physical lines. With classes we use a different measure. We count responsibilities
    对function 我们计算size来控制大小，对于class 我们对小的控制来自于 count responsibilities
  - The name of a class should describe what responsibilities it fulfills.  If we cannot derive a concise name for a class, then it’s likely too large. 

3. The Single Responsibility Principle
  - The Single Responsibility Principle (SRP)2 states that a class or module should have one, and only one, reason to change
  - We want our systems to be composed of many small classes, not a few large ones

4. Cohesion 内聚
  - 尽量让class 内聚，保持class之间的联系紧密 class就会更短小
  - Maintaining Cohesion Results in Many Small Classes

5. Organizing for Change
  - In a clean system we organize our classes so as to reduce the risk of change.
  - We want to structure our systems so that we muck with as little as possible when we update them with new or changed features. In an ideal system, we incorporate new features by extending the system, not by making modifications to existing code. 当我们要升级/增加新东西的时候 我们只需要extend system 而不是 modify现有code，这是个好的系统
  - Isolating from Change
    - A client class depending upon concrete details is at risk when those details change. We can introduce interfaces and abstract classes to help isolate the
impact of those details.
    - A client class depending upon concrete details is at risk when those details change. We can introduce interfaces and abstract classes to help isolate the
impact of those details.
    我们不依赖于Portfolio 类的任何细节，而是利用StockExchange接口来写test
 
      public interface StockExchange {
       Money currentPrice(String symbol);
      }
      public Portfolio {
       private StockExchange exchange;
       public Portfolio(StockExchange exchange) {
       this.exchange = exchange;
       }
       // ...
      }
    
       private FixedStockExchangeStub exchange;
         private Portfolio portfolio;
         @Before
         protected void setUp() throws Exception {
         exchange = new FixedStockExchangeStub();
         exchange.fix("MSFT", 100);
         portfolio = new Portfolio(exchange);
         }
         @Test
         public void GivenFiveMSFTTotalShouldBe500() throws Exception {
         portfolio.add(5, "MSFT");
         Assert.assertEquals(500, portfolio.value());
         }
        }
 
  - By minimizing coupling in this way, our classes adhere to another class design principle known as the Dependency Inversion Principle (DIP)
  - In essence, the DIP says that ourclasses should depend upon abstractions, not on concrete details.
