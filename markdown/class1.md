##Navigation
* These slides are organized by topic and run completely in your browser
* Press Left, Right, Up, Or Down to Navigate through the slides
* Press (Esc) to see the entire slide package
* Press (F) to full screen the presentation
<br><br>

> These are `cubed` slides when you see the **&#8659; More** Symbol, press the down key to move down to the next slide in the section.

<br><br>

> Once the section is finished, move to the right to continue to the next section of the presentation.

<br><br>

> The Navigation Icon in the bottom right corner will tell you which directions you can move.

---

##What is Java?
Java is a programming language, designed to be written by humans, and executed by computers
<br></br>
It is a language humans can use to tell a computer (machine) what to do.
<br></br>
&#8659;
More

--

##Why do we have programming languages?
Computers need to be told what to do. A computer program is a set of instructions for the computer to execute in a particular order.
<br></br>
Digital computers are designed to *ONLY* understand instructions of 0's and 1's. This is called machine language.

```java
000000 0001000 000100 010010 011011
```

However, writing these instructions are very hard for humans to do, so modern programming languages were developed which are easier for humans to write, these are called High-level languages (HLL):

```java
System.out.print("Hello World");
```

&#8659;
More

--

##Computers Cant Read High Level Languages!
Since computers only understand 0's and 1's but humans want to write instructions using words, we need some way to convert the text instructions humans understand to 0's and 1's which computers understand.
<br></br>
Programs called compilers were developed to convert the HLLs to 0's and 1's. So in order to execute your code, you need to "Compile" it first.

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class1/compiler.png">

Compilers act as translators between the human language and the machine language.

<br></br>
&#8659;
More

--


##Problems with Compiling
Compilers translate your code to machine code directly **For one type of processor ONLY**
<br></br>
If you were a developer, and wanted to share your code with the world, you need to compile your code for every type of possible computer processor.
<br></br>
This became a very time consuming process, especially when you updated the code, everything needs to re-compiled again, for each processor.
<br></br>
This is how C++ Works!
<br></br>
&#8659;
More

--

##How is Java Different?
###It's pretty ingenious
* Java doesn't compile directly to machine code, instead Java compilers translate your high level code into something called __Byte-Code__ <br></br>
   - Byte-Code is the machine language for a fake virtual computer made-up by the Java Developers called the Java Virtual Machine 
   - The Java Byte-Code is then translated to machine code by a program called an **Interpreter**.

&#8659;
More

--

##The Java Interpreter
<img src="http://KHEngineering.github.io/FRCJavaCourse2015/Images/class1/runanywhere.png" width="1000" height="600">

&#8659;
More

--

##The Java Interpreter
The Java Interpreter is called the Java Virtual Machine (JVM). It lives on the target (desktop, Robot, etc.)
<br></br>
It's job is to convert the Byte-code in machine code for the computer of the device it is on. 

<br></br>

* The JVM "Interprets" each line of code. This means for each line in the Byte-code:
 - The JVM converts one line of byte-code to machine code
 - Then executes that machine code
 - Then moves on to the next line in the Byte-code, converts it, etc. This cycle continues for each line of byte-code until the program is complete

<br></br>
This makes Java code very portable, because after you compile the Java code into Byte-Code, you can run it any any machine that has a JVM!
<br></br>
&#8659;
More

--

##Why do we use Java for Robotics?
Today there are literally thousands of different programming languages to choose from. Each having their own pros and cons, and varying difficulty of learning.

 - High Level Languages: C++, C# (pronounced c-sharp), python, perl, ada, fortran, etc.
 - Low Level Languages: assembly (varies for each processor)
<br></br>
####The reason we choose to use Java is Simple:
As of Today, Java is the **#1** taugh language at College Universities. We use Java in hopes you will learn enough to prepare for college and the future.
<br></br>
The marjority of other FRC Teams use either Java, C++, Labview, or Python to program their robots.
<br></br>
> ***The remainder of these courses will focus on Java, as it applies to developing code for Robots competing in the First Robotics Competition***

---

##My First Java Program
The only way to learn Java is to jump right in!
<br></br>
```java
public class MyFirstPRogram()
{
   public static void main(String[] args)
   {
     System.out.println("Hello World");
   }
}
```
<br></br>
&#8659;
More

--

##Java Program Structure
<img src="http://khengineering.github.com/FRCJavaCourse2015/Images/class1/programstructure1.png" width="1000" height="600">
<br></br> 
Every java program is defined inside of a `class`
<br></br>
&#8659;
More

--

## Java Program Structure (cont)
<img src="http://khengineering.github.com/FRCJavaCourse2015/Images/class1/programstructure2.png" width="1000" height="600">
<br></br>
The `main` method is where your program starts. Every program must have a  `main` method defined somewhere, and its header must be written exactly as above!
<br></br>
&#8659;
More

--

##Let's break it down
A Java program is really a `class`  definition (what ever that means) with a method named `main`
<br></br>
Whe the program is called to run, the main method is **invoked**, meaning the action specified by the main method is carried out.
<br></br>
The body of the `main` method is enclosed in brackets `{ }`, so what when the program runs, the statements between the brackets are executed.
<br></br>
Every java statement is terminated with a semicolon (`;`). This tells java the line is done, and move to the next one
<br></br>
(If you are not familiar with the words `class` and `method`, don't worry they will be explained soon.
<br></br>
&#8659;
More

--

##Lets break it down (cont.)
The following line says that the program is called **MyFirstProgram**

```java
public class MyFirstProgram
{
```

The next two lines, shown below, being the definiton of the `main` method:

```java
public static void main(String[] args)
{
```
<br></br>
The details of exactly what a class is, and what words like `public`, `static`, `void`, and so forth mean will be explained in detail later. Until then, you can think of these lines as a rather wordy way of saying "Begin the program named MyFirstProgram"
<br></br>

```java
public class MyFirstProgram
{
   public static void main(String[] args)
   {
```

<br></br>
&#8659;
More

--

## Simple Program Example
<img src="http://khengineering.github.com/FRCJavaCourse2015/Images/class1/simpleprogram.jpg" width="1000" height="600">


---

##Arithmatic in Java
Java can do math and allows for all of the the standard math operations:

```java
public static void main(String[] args)
{
   System.out.println(3 + 3); //addition
   System.out.println(3 - 3); //subtraction
   System.out.println(3 * 3); //multiplication
   System.out.println(3 / 3); //division (more on this later)
   
   System.out.println( 2.5 * 3.6 ); //we can even use decimals
}
```
<br></br>
Java can do complex calculations, and follows the standard rules of PEMDAS, you can use parenthesis to control how the statement is evaluated:

```java
{
   System.out.println(3 + 5 * 10 - 2);
   System.out.println(3 + (5 *10) - 2);
   System.out.println((3+5) * 10 - 2);
   System.out.println((3+5) * (10 -2));
}
```

---

##Variables
Programs wouldn't be useful if you had to write a separate program to perform the same calculation on a different set of numbers.
<br><br>
Variables allow you to make your programs more flexible.
<br></br>
In Java the variable must be created before it can be used. The programmer must also specify the type of data that the variable will represent.

```java
public static void main(String[] args)
{
   int numToDisplay = 5;
   int increaseDisplay = 10;
   
   System.out.println(numToDisplay);
   System.out.println(numToDisplay + 10);
}
```
After we define the variable, the variable name can be used inside the program, and the value of that variable will be used to evaulate the statement.
<br></br>
&#8659;
More

--

##Let's break it down
`int` is the type of variable we wish to decalre, `numToDisplay` is the name of the variable and `= 5` means assign the value of 5 to the value.
<br><br>

`int` variables can store whole numbers like `1, 3, 2000, -1 -234323`. Java has other variables for different types of data.
<br></br>
 
* For numbers we have the following types:
   - `int` stores whole numbers like 1, 3, -2000
   - `double` stores decimal numbers like 1.0, 3.0, -2.35
<br></br>
* For text we have the following types:
   - `char` for single characters like 'A', 'J', 'b'
   - `String` for fill sentences like this one

<br></br>
&#8659;
More

--

##Lets break it down (cont.)
After you declare the **type** of variable, you need to give it a name that you will use to refer to that variable. It must be unique from other variables, and there are rules and limitations on how you can name a variable. We will talk about those later.
<br><br>
The `=` operator is used to assign a value to the variable, which will be substituted anytime the variable is used inside of the program.
<br></br>
All number values for `int` and `double` are enterd as is, any text value for `char` or `String` is entered using quotation marks `" "`
<br></br>
```java
{
   int myInt = 5;
   double myDouble = 6.0;
   
   char yesOrNo = "y";
   String mySentence = "Hello World";
}
```
&#8659;
More

--

##Lets break it down (cont.)
After declairing the variable, you can then use it in your program anywhere you are allowed to use that type of data. 
<br><br>
Java automatically knows that name is now a variable, so you don't need any special brackets or qutations to use the variable in your program.


```java
{
  System.out.println(mySentance);
  System.out.println(mydouble * myInt);
}
```

<br></br>
&#8659;
More

--

##Variable Names

* Identifiers: The name of a variable or other item (class, method, object, etc.) defined in a program
   - The name of a Java identifier may include letters, digits, or the underscore symbol ( _ ), and it must **NOT** start with a digit <br><br>
   - identifiers can theoretically be of any lenght <br><br>
   - Java is a case sensitive language: `Rate`, `rate`, and `RATE`, can be used for three different variables <br><br>
   - You can not use the same identifier to define multiple variables in the same scope (more on this later) 

<br></br>
&#8659;
More

--

##Just one more thing on Variables
You don't always have to assign a value to the variable immediately, writing the below is perfectly legal for any type:

```java
int age; //declare value

//some code

age = 3; //assign value later
```

You see we did not specify the value at the same time as when we declared the value.
<br><br>
This is called `declaring an uninitialized variable`, it means we declared a variable, but did not assign it a begining value.

> There are perfectly legitimate reasons to declare an uninitialized variable, however avoid doing so if you can. If you don't know what the value should be when you create the variable, initilize it to zero for numbers or a blank text for characters or strings `""`

--

##Variable Naming Convention

On this team we follow the general java naming convetion used by a majority of programmers world-wide
<br><br>
* Start the names of variables, and methods with a lower case letter
* indicate word boundaries with an upper case letter
* restrict the remaining characters to digitals and lowecase letters
* use whole words, and abbreviate only when it is clear on what the variable is for

```java
topSpeed    bankRate1      timeOfArrival
```
<br><br>
*Start the names of classes with an Uppercase letter, and otherwise adhere to the rules above

```java
FirstProgram      MyClass
```

<br><br>
Remember: Java won't accept a name that starts with a number, and the name can not contain any other symbol than otherscore.

---

##Assignments
Now that we have a variable, we can use them in our program. The program can even change the value of the variable which is extrmely helpful.
<br><br>
In java, we use the equal sign ( `=` ) to make assignments


```java
public static void main(String[] args)
{
  int numOfCookies = 5; //variable declaration
  
  System.out.println(numOfCookies);
  
  System.out.println("I just baked 10 more cookies");
  
  numOfCookies = 15; //change value of variable
  
  System.out.println(numOfCookies);
}
```
<br><br>
&#8659;
More

--

##Lets break it down
In the first line we declare a new `int` variable with the `identifier` "numOfCookies". We assign it a value of `5` using the assinment operator, the `=` sign.

```java
int numOfCookies = 5;
```

We then print to the screen the value of our variable, and that we baked 10 more cookies
```java
  System.out.println(numOfCookies);
  System.out.println("I just baked 10 more cookies");
```

Using the assignment operator, we change the value of our variable to another whole number inside the program.
We don't need to use the keyword `int` again, because we have already defined it as an `int` above.

```java
   numOfCookies = 15; 
```
<br><br>
&#8659;
More

--

##Lets break it down (cont.)
* In java the assignment operator is used to change the values of a variable
* An assignment statement consist of a `variable` on the left side of the operator, and an `expression` on the right side
> __Variable__ = __Expression__;

<br></br>
An expression can constist of any mix of variables, numbers, operators, or method invocations

```java
temperature = 98.6;
count = numberOfBeans;

formula = 6 + 9 * 37 + temperature;
```
<br><br>
&#8659;
More

--

##Lets put it together (exercise 1)

>Lets write a program which calculates the circumferance of a circle of any radius, and prints the result to the screen.

```java
public class Circumference
{
  public static void main(String[] args)
  {
    
     double pi = 3.141519;
     double radius = 5;
     
     double circumference = 2 * pi * radius;
     
     System.out.prinln(circumference);
}
```
<br><br>
Change the value assigned to radius to calculate the circumference of a difference circle.

---

##Constants
There is a problem with out previous program. The number `pi` in the real world never changes. Pi is always 3.141519...
<br><br>
However, nothing in the program prevents us from changing the value of pi. In a really big program we may accidently change the variable by accident.

For example we can do this, unintentionally

```java

double pi = 3.14159;

// some more code between here
// some where later

pi = 3;


// more code
```
After that, anywhere we use PI the value the resulting calculation will be incorrect, and may be very hard to detect.
We can prevent this from happning by making pi a `constant`
<br>
&#8659;
More

--

##Constants

We use the `final` keyword to tell Java we never want to allow the value to change after we declare it.
<br><br>
If we try to change the value, the compiler will throw an error and alert us to the problem. 
<br>
```java
final int THIS_IS_A_CONSTANT = 3;

final double PI = 3.141519;

//now since these are finals 
/trying to do this is illegal
pi = 3;
```
<br>
>Always use a constant when you want to be sure, the value doesn't change after you set it!

<br><br>
&#8659;
More

--

##Constant Naming Conventions
When you declare a constant using the `final` keyword, we following a different naming convention for the `identifier`

* Use all capital letters for the identifier
* Any words are separated with an underscore _
* Do not abbreviate words

```java
final String MY_NAME;
final int MY_AGE;

fina int NUM_OF_DAYS_PER_WEEK = 7;

final double PI = 3.14159;
final double PENNIES_PER_DOLLAR = 100.0;
```

--

##Fixing our previous exercise
Now that we know about constants, lets fix the solution to our previous example:

```java
public class Circumference
{
  public static void main(String[] args)
  {
    
     final double PI = 3.141519;
     double radius = 5;
     
     double circumference = 2 * PI * radius;
     
     System.out.prinln(circumference);
}
```
>Remember Java is case sensitive, so you can't make the constant `PI`, but try to call it as `pi` or `Pi`

---

## The Plus ( + ) Operator
We previously learned that equal ( = ) is the assignment operator, well the plus ( + ) operator has a special funcation in the java language as well.
<br><br>
The plus operator can be used for addition in math equations such as:

```java
System.out.println(5 + 6* 9);
```
<br><br>
But can also be used to `add` Strings together

```Java
String text1 = "My name is Kevin";

String text2 = "And I am an Aluminum Falcon";

String text3 = text1 + text2;

System.out.println(text3);
```
<br><br>
&#8659;
More

--

##The plus ( + ) operator (cont.)

We can fix the the sentance by adding a space between both sentences in line.
<br><br>
```java
String text3 = text1 + " " + text2;
```
<br><br>
Simply putting a space between quotation markes allows us to combine the strings properly. When we combine strings it is called `concatination`
<br><br>
We can also use the plus operator to combine a string and a varibale we are printing;

```java
System.out.println("My name is " + MY_NAME);
```
<br><br>
&#8659;
More

--

##Putting it together

Using `concatination` we can write better programs

```java
public class Circumference
{
  public static void main(String[] args)
  {
    
     final double PI = 3.141519;
     double radius = 5;
     
     double circumference = 2 * PI * radius;
     
     System.out.prinln("The circumference of " + radius + 
     		" is: " circumference; //we can span multiple lines
}
```
<br><br>
> Notice the space markes in the text, this allows the text to display properly on the screen. You need to add spaces yourself when concatinating strings

---

##Branching with the `IF` statement
We can make decisions in programs using the IF statement

```java
public static void main(String[] args)
{

  double x = 10;
  
  if (x < 10)
      System.out.println("Hello World")
      
   System.out.println("Good-bye world");
}
```
<br><br>
&#8659;
More

--

##Lets break it down
<br><br>
<img src="http://khengineering.github.com/FRCJavaCourse2015/Images/class1/ifstatement.png" width="1000" height="600">
<br><br>
&#8659;
More

--

##Compound Statement  
If the statement under if is made up of more than one statement, they must be enclosed in curly braces ({ })
<br><br>
```java
if (amount < balance)
{
	System.out.println(“Thank you. Withdrawal will take place”);
	balance = balance – amount;
}
```

> Any statements inside of the brackets undeer the `if` will be executed when ever the condition of the IF statement is true. 

---

##END
