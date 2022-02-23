# Java  
## Intro to Java
- java programs and other programming have keywords
- Notes: keywords ARE case sensitive
- Public is an access modifier
- Access modifier: allows us to define the scope or how other parts of your code or even someone else's cide can access this code
- Class: used to define a class with the name following the keyword "{ }" defube the class block
- to define a class requires an optional access modifier, followed by class, followed by { }
- anything between { } is apart of the class data and code included
- Method? a collection of statments 1 or + that performs an operation
- Main method is entry point in any java code, java looks for it when running program
- Can create your own methods

![image](https://user-images.githubusercontent.com/95253821/154185703-c1384d57-acbc-4847-94db-18a5bb9a667e.png)
- public is the access modifier
- Static will get to later
- Void the method will not return anything
- () needed for method declaration, can include one or more parameter
- String[] args is the parameter within the ()
- {} below main method is code block
- Code block is used to define a block of code, mandatory to have one in methind declaration
- System.out.println() is a statement
- statement is a complete command to be executed and include one or more expressions
- Variables are a way to store info on computer. variables can be accessed by a name we give them and computer figures out where it gets stored in RAM
- Variabel can be changed, just variable
- Multiple data types in keywords
- Int = integer a whole number
- To define variable need to specify data type, give name, and optionall add an expression
- declaration statement used to define variable by indication data type, and the name , and optionally set the variable to certain value

![image](https://user-images.githubusercontent.com/95253821/154187371-4a3455f7-ae57-4460-b6f9-7aa7891abcad.png)
- the type is int, name is myFirstNumber and the value assigned or initialized to variable is 72. Declaring a variable of type int with name myFirstNumber and assigning the value 72 to it
- int myFirstNumber cna be changed to anything like so
- String literal is any sequence of characters surrounded by double quotes. Value cannot be changed not variable
- operators perform and operation on a variable or value + - / *. Lots more

![image](https://user-images.githubusercontent.com/95253821/154191293-c2e7ba97-3896-4c3b-bf28-8c5ce8ae27fe.png)
### Primitive Types
- Primitive types: boolean, byte, char, short, int, long, float, double
- These building blocks of data manipulation
- Java packages are ways to organize java projects, consider as folders for now
- companies use domain names reversed learnprogramming.academy becomes academy.learnprogramming

![image](https://user-images.githubusercontent.com/95253821/154193645-b44e64f0-9f66-435d-94e1-3b4025b840de.png)
- Java uses concept of Wraooer class for all 8 primitive types, int we use Integer, and by doing that it gives us wats to perform operations on an int
- Using Min_Value and Max_Value to get Java to tell us min and max range of numbers that can be stored
- Overflow more the max vualue and Underflow less than min. Causes computer to skip to the opposoite important concept
- Byte occupies 8 bits width of 8, short is 16 bits width of 16, int occcupies 32 occupies 32 bits, long with of 64
- Casting means to treat or convert a number from one type to another but the type of number in parenthesis
- (byte)(myMinByte/2);
- Other languages have casting too
- FLoating Point numbers are fractional parts as decimal points still primitive
- floting point numbers also known as real number
- Single precision (float) 32 bits and double precision (double) 64 bits
- in general float and double are great for general floating point operations
- Java has a class called BigDecimal 
- Unicode is an international encoding standard for use with diff languages and scripts
- boolean allows for two choices T/F, Yes/No, 1/0
### Specifically String
- String is not primitive type but it is actually a class (easier than regular class)
- String is a sequence of characters
- String in Java are immutable, means you can't change a strin after it's created but a new one is created example

![image](https://user-images.githubusercontent.com/95253821/154790572-0e3993bd-7fd1-4e6f-9944-63d05143226f.png)
- Code is quie inefficient would prefer StringBuffer

### Operators Operands and Expressions
- operators are special symbols that perform specific operations on one, two, or three operands then returns resuls ie + operator
- What is Operand? terms used to describe any object manupulated by operator
- int myVar = 15 + 12;
- + is operator and 15 and 12 operands
- formed by combining variables literals method return values and operators
-  // are ignored anything after that are ignored use it to describe
-  = assigns the variable
-  == is the actual "equal", are the operands identical to each other

### if then statment
- the most basic of all control flow statements, known as conditional logic, does certain section of code if certain expression evaluates as true
- no code block only 1 line will be executed, always use code block for if then statements
- 
