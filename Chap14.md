### 逐步改进 Successive Refinement

- You will see a module that started well but did not scale. Then you will see how the module was refactored and cleaned.

一个 example code 对于 parse args 的实现 
You can see how simple this is. We just create an instance of the Args class with two parameters. The first parameter is the format, or schema, string: “l,p#,d*.” It defines three command-line arguments. The first, -l, is a boolean argument. The second, -p, is an integer argument. The third, -d, is a string argument. The second parameter to the Args constructor is simply the array of command-line argument passed into main

```

  public static void main(String[] args)   {

       try {

         Args arg = new Args(“l,p#,d*”, args);

         boolean logging = arg.getBoolean(’l’);

         int port = arg.getInt(’p’);

         String directory = arg.getString(’d’);

         executeApplication(logging, port, directory);

       } catch (ArgsException e) {

         System.out.printf(“Argument error: %s\n”, e.errorMessage());

       }

     }
```
