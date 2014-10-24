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

##Review of Last Class

* Computers only understand 0's and 1's, humans use programming languages to avoid writing machine language
* Compilers translate programming languages to machine code - called "compiling"
* Java is the language we use on this team for Robotics Competition

<br><br>
&#8659;
More

--

##Review of Last Class (cont. 2)

* Java compiles to Byte-code first, and uses an interpreter on the computer to convert byte-code to 0's and 1's
* The interpreter works by converthing a single line to byte code, executing it, then moving to the next byte code line
* The interpreter is called the JVM, and your byte code can run on any computer as long as a JVM is installed

<br><br>
&#8659;
More

--

##Review of Last class (cont. 3)

* we wrote our first java program
* defined `class header`, `class body`, `method header`, `method body`, `main method`
* every java program is a class with a main method defined 

<br><br>
&#8659;
More

--

##Review of Last class (cont. 4)
* learned we could print statements using `System.out.println("say something");`
* every java statement ends with a semi colon ( ; )
* java is case sensitive
* java has built in math operations for `+, -. * (asterisk), / (forward slash)`

<br><br>
&#8659;
More

--

##Review of Last class (cont. 5)
* Java allows us to create variables, but you must decalare the type of data you want to use it for
 - `int`: allows you to store integers (e.g whole numbers like 1, -30, 45, 10003)
 - `double`: allows you to store decimal numbers (e.g 1.0, 2.5, -35.6, 3.141519)
 - `String`: allows you to store text but must be placed in quotations (e.g. "hello", "my name is kevin")
* using the word `final` before any variable allows us to make it a constant

<br><br>
&#8659;
More

--

##Review of Last class (cont. 6)
* there are rules for naming variables `topSpeed, bankRate1, timeOfArrival`
* there are rules for naming constants `MY_NAME, PENNIES_PER_DOLLAR, MY_AGE`
* Using the ( = ) operator we can assign values to variables, and use those variables later in our program
* we can use the ( + ) operator for combining Strings as well as addition

<br><br>
&#8659;
More

--

##Review of Last class (cont. 7)

###Most Important thing we learned last week

* You wrote real computer programs
* Realized that java is a language, just like English or French, it has rules for sentance structure, but other wise can be learned with a little practice

<br><br>

> This is where we will continue today

---

##Language Syntax

Syntax:  The arrangement of words and punctuations that are legal in a language, the grammar rules of a language

We have learned a few Syntax rules of the Java language so far

- java is case sensitive
- must write `public static void main(String[] args)` to start a program
- every program must be in a `class` definiton
- every statement must end with a semi colon ( ; )

<br><br>
If you do not follow the rules of the Java Syntax, your program will not run, because the compiler will be unable to convert it to 0's and 1's

<br><br>
&#8659;
More

--

##Language Keywords

Certain words in Java have special meanings and alter how the program is executed. These words are called keywords

```java 

public final class int double static 

```

> when these words are written, Java recognizes them as a special term used to control the program. We will learn more keywords as we learn the language

<br>

> You can not use a keyword as the name of any variable, class, or method... java will get confused. 

```java

double final = 37.6; //this is illegal because final is a keyword, 
                     //and can't be used as a variable name.
```

<br>
&#8659;
More

--

##Syntax Errors

One of the reasons we use the eclipse editor, is because it will tell us if we have made any syntax errors. Here we are missing a semi-colon at the end of the statement ( ; )

<img src = "http://khengineering.github.io/FRCJavaCourse2015/Images/class2/semicolonerror.png" height="600">

<br><br>
&#8659;
More

--

##More Syntax Errors

<img src = "http://khengineering.github.io/FRCJavaCourse2015/Images/class2/lowercaseerror.png" height="600">

> Error is Lower case S in System

<br><br>
&#8659;
More

--

##More Syntax Errors

<img src = "http://khengineering.github.io/FRCJavaCourse2015/Images/class2/multipleerrors.png" height="600">

> Error: Missing bracket, and trying to assign a value to a constant, but only shows one error

<br><br>
&#8659;
More

--

##Errors are Natural

As a programmer you will get errors, the key isn't to avoid them, but to be sure to recognize them
<br><br>

Sometimes the error message is a bit cryptic, with experience you will be able to determine what it means

<br><br>

In cases where you have multiple errors, the compiler will only show one, and you must continue to fix each error until the compiler is happy.

<br><br>

> The Compiler is the Java Language Instructor, you must follow the Java syntax rules, in order for your program to execute

---

##Branching with Java

We may wish to write a program that makes decisions, and executes different code depending on the situation.

```java
//program to calculate salary for hourly employee
public static void main(String[] args)
{
    int hoursWorked = 40; //declare int and initialze
    double pay; //declared double unitialized
    final double PAY_PER_HR = 18; //18 dollars per hr

    if (hoursWorked > 40)
        pay = PAY_PER_HR * 40 + 1.5*PAY_PER_HR*(hoursWorked-40); //40 hrs at regular pay +
                                                                 //remainder at overtime pay
    else
        pay = PAY_PER_HR * hoursWorked;

    System.out.println("Hours Worked This Week: " + hoursWorked);
    System.out.println("Your PayRate is: " + PAY_PER_HR);
    System.out.println("This week's paycheck is: " + pay);
}
```


<br><br>
&#8659;
More

--

##Let's break it down

```java
public static void main(String[] args)
{
    int hoursWorked = 40; //declare int and initialze

    double pay; //declared double unitialized

    final double PAY_PER_HR = 18.0; //18 dollars per hr
```

We start our program and declare `hourWorked` as an `int` and set it to a value of 40 hours.
<br><br>
We also declare the variable `pay` as a type of `double` but do not set a value
We then create a constant of type `double` named `PAY_PER_HR`


<br><br>
&#8659;
More

--

##Let's break it down (cont)

```java
public static void main(String[] args)
{

    if (hoursWorked > 40)
        pay = PAY_PER_HR * 40 + 1.5*PAY_PER_HR*(hoursWorked-40);
    else
        pay = PAY_PER_HR * hoursWorked;
```
<br><br>
if the value of hoursWorked is greater than 40, java will execute

```java
pay = PAY_PER_HR * 40 + 1.5*PAY_PER_HR*(hoursWorked-40);
```

<br><br>
&#8659;
More

--


##Let's break it down (cont)

```java
public static void main(String[] args)
{

    if (hoursWorked > 40)
        pay = PAY_PER_HR * 40 + 1.5*PAY_PER_HR*(hoursWorked-40);
    else
        pay = PAY_PER_HR * hoursWorked;
```

<br><br>
if the value of hoursWorked is less than **or equal** to 40, java will execute

```java
pay = PAY_PER_HR * hoursWorked;
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
If the statement under `if` or `else` is made up of more than one statement, they must be enclosed in curly braces ({ })
<br><br>
```java
if (amount < balance)
{
    System.out.println(“Thank you. Withdrawal will take place”);
    balance = balance – amount;
}
else
{
    System.out.println("Insufficient Funds");
    System.out.println("Please enter a lower amount");
}

```

> Any statements inside of the brackets under the `if` will be executed when ever the condition of the IF statement is true. 

<br><br>
&#8659;
More

--

##Omitting the `Else`
Sometimes, we want to branch where we do nothing if the condition is `false`

```java
public static void main(String[] args)
{

  double x = 10;
  
  if (x < 10)
      System.out.println("Hello World")
      
   System.out.println("Good-bye world");
}
```

> In those cases we can omit the `else` to just have an `if` statement

<br><br>

> Notice we can ommit any brackets under the if statement if we only want to execute one line. This is allowed in the Java **Syntax**


---

##Conditional Operators

The **condition** in parenthesis must evaluate to a `true` or `false`
<br><br>
Java has many operators which allow the user to compare items


| Math Notation | Name                      | Java Notation | Example        |
| ------------- | --------                  | ------------- | -------------- |
| =             | Equal to                  |  ==           | x + 7 == 2 * y |
| &ne;          | Not Equal to              | !=            | score != 0     |
| >             | Greater Than              | >             | time > limit   |
| <             | Less Than                 | <             | pressure < max |
| &le;          | Less Than, or Equal to    | <=            | time <= limit  |
| &ge;          | Greater Than, or Equal to | >=            | age >= 21      |

<br>
&#8659;
More

--

##Practice with conditonal operators

```java

double pressure = 23.5;
final double MAX = 100; 

int age = 15;
int score = 93;

System.out.println( pressure < MAX );  //true
System.out.println( age == 0 ); //false
System.out.println( age != 0 ); //true
System.out.println( score >= 90 );  //true

```
<br><br>
&#8659;
More

--

##Pitfall: Using `==` with String
Although `==` correctly tests two values of primative types such as two numbers, it does't work on strings.

```java
final String MY_NAME = "Kevin";
System.out.println(MY_NAME == "Kevin"); //true, sometimes
System.out.println(MY_NAME == "kevin"); //false
```

<br><br>
&#8659;
More

--

##Pitfall: Using `==` with String (cont.)

We can use a special syntax to **GUARANTEE** string comparison will always work using the equals method

```java
System.out.println(MY_NAME.equals("Kevin"));
```

<br><br>

```java
String s1 = "Hello";
String s2 = "hello";

if(s1.equals(s2);
    System.out.println("They are equal strings");
 else
    System.out.println("They are not equal strings");
```

<br><br>

> Remember java is case sensitive, in order for strings to be equal to each character must be of the same case, and appear in the same order. If you want to ignore case use `equalsIgnoreCase`, instead of `equals`

<br>
&#8659;
More

--

##Pitfall: Using `==` with String (cont.)

We will talk more about this type of syntax but for now you can do the following for any `String`

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class2/stringcompare.png">

<br><br>
&#8659;
More

---

##Boolean Data Type

We saw in the previous example all of the conditional statements evaluated to `true` or `false`
<br><br>
Java has an additional datatype which stores the results of conditional statements
<br><br>
`boolean` **CAN NOT** store numbers, text, or anything other than `true` or `false` **WITHOUT QUOTES**

<br><br>

```java
boolean choice = true;
boolean isEnabled = false;

boolean legalAge = age >= 21;
```

<br><br>

> `boolean` is a datatype just like `int`, `double`, and `String`. `true` and `false` are keywords in Java

<br><br>
&#8659;
More

--

##Building Boolean Expressions

Java has additional operators, called `conditional operators` which allow us to build complex boolean expressions (conditional statements)
<br><br>
! Logical Not <br>
&& Locical AND <br>
|| Logical OR <br>

<br><br>

* `NOT` negates the value (if the expression evalues to true), !, will return false
* `AND`, ALL expressions must be true, so that the final result can be true
* `OR`, ANY part of the expression must be true

<br><br>
&#8659;
More

--

##Boolean Expression Examples

```java

boolean madeIt = (time < limit ) && ( limit < max ); //AND

if ( (personAge > 21) || withAGuardien )  //OR

System.out.println(!true); //NOT
```

<br><br>

> The first statement before the operator is evalued, then the statement after the operator is evaluated, finally the results of both statements are compared using the boolean operator, and the final result is returned.

<br><br>

> Use parenthesis ( ) to control which statements are evalued first similar to PEMDAS for math operators

<br>
&#8659;
More

--

##Boolean Truth Tables

NOT

| X       |  ! X |
| ------ | ----- |
| true   | false |

<br><br>
AND, OR

| X        | Y       |  x && y   |  x &#124; &#124; y  |
| -------  | ------- | ---------   | ---------- | 
| true     | true    |  true       | true       |
| true     | false   |  false      | true       |
| false    | true    |  false      | true       |
| false    | false   |  false      | false      |




---

##Flow Control

* **Flow Control** in Java referes to the ability to control programs by branching or looping
* Several Branching Mechanism: `if-else`, `if`, `switch` exist
* Several Looping Exists: `while`, `do-while`, `for` loops
* Most Bracnching and looping expressions are controlled by **Boolean Expressions**
 - A boolean expression evaluates to either true or false

<br><br> 

> We rarely use `switch`, `while`, `do-while`, or `for` statements in robotics, we will will cover them as needed

<br><br>
&#8659;
More
 

--

##Loops

Java has three types of loops

* the `while` loop
* the `do-while` loop
* the `for` loop

> it is generally a bad idea to use loops for robotics, I am only touching this topic so you are aware loops exist in java

<br><br>

> There are some cases where loops are useful in robotics, and we will learn more about loops when we reach those cases

<br><br>
&#8659;
More

--

##The `while` Loop

```java
public static void main(String[] args)
{

  int x = 10;
  
  //while loop continue to execute as long as condition is true
  while ( x <= 10 )
  {
      System.out.println("X is now: " + x);
      x = x-1; 
  }
  
  System.out.println("Loop is finished"); //lets us know the loop is done
```

<br><br>
&#8659;
More

--

##Lets break it down

```java
while (x <= 10)
{
```

<br><br>

> Tell Java we want to perform the following statements while this condition holds true. The condition is
x is less than or equal to the value of 10.

<br><br>
&#8659;
More

--

## Lets break it down (cont)

```java
while (x >= 0)
{
   System.out.prinln("X is now: " + x );
   x = x -1;
}
```

<br><br>

> the statements inside the bracket will execute once, and then the condition is checked again. IF the condition holds true, the statements will execute again, and keep doing so until the condition evaluates to  `false`.

<br><br>

> we can modify variables inside loops, in this case, each loop cycle we subtract 1 from the value of x. The new value of x is used each time the condition is evaluated, so eventually when x becomes -1, the loop will end.


<br><br>
&#8659;
More

--


##`while` Loop Syntax

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class2/whileloop1.png">

<br><br>
&#8659;
More

--

##`while` Loop Syntax (cont.)
<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class2/whileloop2.png">

<br><br>
&#8659;
More

--

##PITFALL: Infintite Loop

An Infinite loop is a loop that never ends, and thus the program never ends, and appears to hang. This is bad,

```java

int x = 10
while (x <= 10;)
{
   System.out.println("X is now: " + x);
   x = x-1;
}   
```

> use ctrl-c to break out of a program with an infinite loop. This just shows one of the dangers of loops, so use them wisely!.

<br><br>
&#8659;
More

--

##`do-while` Loops

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class2/dowhile1.png">

<br><br>
&#8659;
More

--

##`For` Loops

---

##Methods

Let's go back to our Salary calculating program we created earlier. 

We are asked to update our program so we can calculate the Salary for everyone in the office, but they each have a different hourly rate 

<br><br>

* Mary: 40 hours per week, at $18 per hour
* John: 25 hours per week, at $20 per hour
* Steve: 50 hours per week, at $17 per hour

<br><br>
So what can we do?
<br><br>
&#8659;
More

--

##Using what we know so far

```java

final double PAY_RATE1 = 18;  //Mary
final double PAY_RATE2 = 20;  //John
final double PAY_RATE3 = 17;  //Steve

double pay = 0;

String name = "Mary";
double hoursWorked = 40;

if (name.equalsIgnoreCase("Mary");
{
    if(hoursWorked <= 40)   //nested if
        pay = PAY_RATE1*hoursWorked;
    else
        pay = PAY_RATE1*40 + 1.5*PAY_RATE1*(hoursWorked-40);
}
    
if (name.equalsIgnoreCase("John")
{
    if(hoursWorked <= 40)
        pay = PAY_RATE2*hoursWorked;
    else
        pay = PAY_RATE2*40 + 1.5*PAY_RATE2*(hoursWorked-40);
}

if (name.equalsIgnoreCase("Steve");
{
    if(hoursWorked <= 40)
        pay = PAY_RATE3*hoursWorked;
    else
        pay = PAY_RATE*40 + 1.5*PAY_RATE3*hoursWorked-40);
}

System.out.println(pay);

```

<br>

> change name from "Mary" to "John" or "Steve" to see if the program works for them as well

--

##A better way using a `method`

The code above works, but we were forced to write the same/similar lines of code multiple times. This is a nightmare for code maintenance

<br><br>

```
public static void main(String[] args)java
{
    final double PAY_RATE1 = 18;
    final double PAY_RATE2 = 20;
    final double PAY_RATE3 = 17;
    
    if (name.equalsIgnoreCase("Mary")
        pay = class2.salary(hoursWorked, PAY_RATE1);
    if (name.equalsIgnoreCase("John")
        pay = class2.salary(hoursWorked, PAY_RATE2);
    if (name.equalsIgnoreCase("Steve")
        pay = class2.salary(hoursWorked, PAY_RATE3);
    
System.out.println(name + " worked " + hoursWorked + 
    " hours and should be payed $" + pay );
}

public static double salary(double hours, final double PAY_RATE)
{
   if(hoursWorked <= 40)
      return hoursWorked*PAY_RATE;
   else
      return 40*PAY_RATE + 1.5 * (hoursWorked - 40);

}
```

> Compare output to previous code, is it the same? Which program is shorter and easier to understand

--

##Lets break it down

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class2/methodbreakdown.png">

<br><br>
Clearer, more consiced code

Reuse code multiple times, while only have to write it once.



---

##Indenting
We will say more about indenting as we introduce more Java. However, the general
rule is easy to understand and easy to follow. 

<br><br>

When one structure is nested inside another structure, the inside structure is indented one more level. For example, in our
programs, the main method is indented one level, and the statements inside the main
method are indented two levels. 

<br><br>

We prefer to use four spaces for each level of indenting.
More than four spaces eats up too much line length. Less than 4, and its hard to tell if the line is indented


  
