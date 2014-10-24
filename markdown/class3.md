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

* If
* If-else
* Boolean
* conditional logic (Not, AND, OR)
* Methods
* programming algorithms

--

* If and If-else statement
<br><br>
<img src="http://khengineering.github.com/FRCJavaCourse2015/Images/class1/ifstatement.png" width="1000" height="600">
<br><br>

> Note: Java syntax, don't put a semicolon on the same line as `if` or `else`

--

##Boolean & Conditional Operators

The **condition** in parenthesis must evaluate to a `true` or `false`
<br><br>
Boolean is a data type in Java which can only be true or false `boolean check = true` or `boolean canBuy = (price < bank)`;
Java has many operators which allow the user to compare items


| Math Notation | Name                      | Java Notation | Example        |
| ------------- | --------                  | ------------- | -------------- |
| =             | Equal to                  |  ==           | x + 7 == 2 * y |
| &ne;          | Not Equal to              | !=            | score != 0     |
| >             | Greater Than              | >             | time > limit   |
| <             | Less Than                 | <             | pressure < max |
| &le;          | Less Than, or Equal to    | <=            | time <= limit  |
| &ge;          | Greater Than, or Equal to | >=            | age >= 21      |


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


--

##A better way using a `method`

The code above works, but we were forced to write the same/similar lines of code multiple times. This is a nightmare for code maintenance

<br><br>

```java
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

--


##Review of Last Class 1

* Computers only understand 0's and 1's, humans use programming languages to avoid writing machine language
* Compilers translate programming languages to machine code - called "compiling"
* Java is the language we use on this team for Robotics Competition

<br><br>
&#8659;
More

--

##Review of Last Class 1(cont. 2)

* Java compiles to Byte-code first, and uses an interpreter on the computer to convert byte-code to 0's and 1's
* The interpreter works by converting a single line to byte code, executing it, then moving to the next byte code line
* The interpreter is called the JVM, and your byte code can run on any computer as long as a JVM is installed

<br><br>
&#8659;
More

--

##Review of Last class 1(cont. 3)

* we wrote our first java program
* defined `class header`, `class body`, `method header`, `method body`, `main method`
* every java program is a class with a main method defined 

--

##Review of Last class 1(cont. 4)
* learned we could print statements using `System.out.println("say something");`
* every java statement ends with a semi-colon ( ; )
* java is case sensitive
* java has built in math operations for `+, -. * (asterisk), / (forward slash)`
 

--

##Review of Last class 1(cont. 5)
* Java allows to create variables, but you must declare the type of data you want to use it for
 - `int`: allows you to store integers (e.g whole numbers like 1, -30, 45, 10003)
 - `double`: allows you to store decimal numbers (e.g 1.0, 2.5, -35.6, 3.141519)
 - `String`: allows you to store text but must be placed in quotations (e.g. "hello", "my name is kevin")
* using the word `final` before any variable allows us to make it a constant


<br><br>
&#8659;
More

--

##Review of Last class 1(cont. 5)
* Using the ( = ) operator we can assign values to variables, and use those variables later in our program
* there are rules for naming variables `topSpeed, bankRate1, timeOfArrival`
* there are rules for naming constants `MY_NAME, PENNIES_PER_DOLLAR, MY_AGE`
* we can use the ( + ) operator for combining Strings as well as addition

--

##Review of Last class 1(cont. 6)

###Most Important thing we learned last week

* You wrote real computer programs
* Realized that java is a language, just like English or French, it has rules for sentence structure, but other wise can be learned with a little practice

---

##Objects

Java is known as an object oriented programming (OPP) language
<br><br>
Today were going to talk about what that means, and how we can use it in our programs.

--

##Objects

The world around us is made up of objects:

* people
* automobiles
* buildings
* streets
* paper

<br><br>

> Each of these objects can perform some action and affects other objects in the world. OPP is a programming methodology which similarly contains objects that performs actions.

--

##Objects

Object-oriented programming has its own terminology
<br><br>

* The Objects are called, appropriately enough, `objects`
* The actions that object can perform are called `methods`
* Objects of the same type are said to be of the same `type` or in the same `class`
* All objects of the same class can perform the same actions (called `methods`)

--

##How we use Objects
For example, in an Airport simulation program
<br><br>
All Airplanes might be long to the same class, probably called the `Airplane` class
All airplanes have the same methods such as taking off, flying to a location, landing, etc.
<br><br>

However, all airplanes are not identical, and they can have difference characteristics, for example
each plane can be flying at a different speed or altitude.

--

##Objects

For now you can think of Objects as custom data types.
<br><br>
So far we have been using `int`, `double`, and `boolean`. These are pre-defined in java and are called `primitive` data types
<br><br>
You can think of objects as custom data types the user can create in Java. The way you define your object is in a `class`
<br><br>
Every time you make a new variable using your object, you can say that variable is an `instance` of the object.
<br><br>

> An object differs from a primitive type in that objects have data as well as actions (called methods) where as primative types only store data

<br><br>

> In Java you **can not** create your own primitive types

---

##Class definitions

Lets create our first object


```java
public class Date 
{
    public String month;
    public int day;
    public int year; // a four digit number
	
	
    public void writeOutput()
    {
	System.out.println(month + "" + day + "," + year);
    }
}
```

<br><br>

> Must be saved in a file called `Date.java`

--

##Lets break it down

The above class named `DateFirstTry` is unrealistically simple, but will help you learn the syntax for creating an object

<br><br>
Each object of this class has 3 pieces of data associated with it, a `String` for the month name, a integer for the day, and another integer for the year.

```java
public String month;
public int day;
public int year; // a four digit number

```

The word `public` is a keyword, and simply means there are no restictions on how we can use these variables when we create classes in our programs

<br><br>

We will see later what happens when they are not public

--

##Lets break it down (cont.)
The objects only have one method, named `writeOutput`

```java
public void writeOutput()
{
	System.out.println(month + "" + day + "," + year);
}
```

--

##Using our object in a program

```java
public class DateProgram
{

    public static void main()
    {
        Date date1, date2;

	date1 = new DateFirstTry();
	date2 = new DateFirstTry();

	date1.month = "December";
	date1.day = 31;
	date.year = 2007;

	System.out.println("date1: ");
	date1.writeOutput();


	date2.month = "July";
	date2.day = 4;
	date2.year = 1776;
	
	System.out.println("date2: ");
	date2.writeOutput();
	

    }
}
```


<br><br>

> Saved in file `DateProgram.java`

--

##Lets break it down

```Java
Date Date1, Date2;
```

Declares two new variables `date1`, and `date2` of type Date similar to how we declare variables of `int` or `double` 

<br><br>
This gives us variables of type `DateFirstType`, but we still need to instantiate them with an `object`

```java
date1 = new Date();
date2 = new Date();
```
<br><br>

We will discuss this kind of statement in more detail later when we discuss something called a `constructor`, but for now just remember we use the `new` operator to instantiate an object.


--

##Lets break it down (cont.)

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class3/classdefinition.png">


---

##Instance Variable and Methods
Each Instance of the object has its own copy of the member variables, and can be used like any other variable.

date1 has the following instance variables

```java
date1.month
date1.day
date1.year
```

date2 has the following instance variables which are or the same type, but can have different values

```java
date2.month
date2.day
date2.year
```

> we can access instance variables, and methods associated with that class using the Dot (period symbol) operator

--

##Instance Variables 

Can be used like any other variable, for example `date2.month` can be used like any other `String`.
<br><br> 
Instance variables `date2.year` and `date2.day` can be used like any other `int` variable.
<br><br>

So even though the below doesn't make sense, it is possible to do the following:

```java
date2.month = "Hello Falcons";

date2.day = 36;

date2.year = -3;
```

> we will see later how to prevent incorrect values from being assigned to our class.

--

##Methods

The class we defined so far, has one method named `writeOutput()`

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class3/methodbody.png">

<br><br>

Everytime we call this method using `date1.WriteOutput()` or `date2.writeOutput()` the code inside the method will execute for that object only.

--

## The `new` Operator

An object of a class is named or declared by a variable of the class type:
`ClassName  objectName;`

<br><br>

The new operator must then be used to create the object and associate it with its variable name (however, some few exceptions do exist): 
`objectName = new ClassName();`

<br><br>

These can be combined as follows:
`ClassName objectName = new ClassName();`

<br><br>

Example: 
```java
Car c1 = new Car(); // Car is the class name and
				  // c1 is the object name
```

--

##Instance Variables & Methods

Instance variables (attributes) can be defined as in the following two examples
Note the public modifier (for now):

```java
 public int  numberOfDoors;
 public double  Price;
```

In order to refer to a particular instance variable, preface it with its object name as follows:

```java
c1.price
c2.price
c1.numberOfDoors
```


C1 & c2 are just two objects from the class


--

##Instance Variables & Methods

Method definitions are divided into two parts:  a `heading` and a `method body`

Methods are invoked using the name of the calling object and the method name as follows:
 `objName.methodName();`
Example: 
`C1.getNumberOfDoors();`

Invoking a method is equivalent to executing the method body

---

##More on methods

Method Definitions

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class3/methodbody2.png">

--

As we noted, the methods you defined are of 2 types:
methods that perform an action and return a value, and methods that perform an action but don't return a value

Both kind of methods have a method heading and a method body

Does not return a value:
```java
public void Method_Name(Parameter_List)
```

Returns a value:

```java
public Return_Type Method_Name(Paramerer_List)

public String myMethod() // always returns a string
public double yourMethod() //always returns a double

```

> If a method returns a value, it may return different values in different situations, but must always be a value of the specified `return_type`

--

##Returning a Value

When a method returns value, it can be used as an expression in an assignment:

```java
double d = anObject.yourMethod();
String sysOutput = anObject.myMethod();
```
A void method does not return a value, but simply performs an action.

anObject.ourMethod();

> Think of the word `void` to mean "Does not return a value"


--

##Returning a value

```java
public String getMonth()
{
   return month;
}

public int getDay()
{
   return day;
}

public int getYear()
{
   return year;
}
````

> A method returning a value must use the `return` keyword to specify what value to return, after the value is return, the method is finished executing

--

##Parameters


```java
public void setMonth (String inputMonth)
{
    month = inputMonth;   
}

public void setDay (int inputDay)
{
    day = day;
}

public void setYear (int inputYear)
{
    year = inputYear;
}

```

> the parameters are passed by a program using the object

--

##Using the methods we just added


```java

public class DateProgram
{

    public static void main()
    {
        Date date1, date2;

	date1 = new Date();
	date2 = new Date();

        //using new methods
	date1.setMonth("December");
	date1.setDay(31);
	date.setYear(2007);

	System.out.println("date1: ");
	date1.writeOutput();

        //using no methods
	date2.month = "July";
	date2.day = 4;
	date2.year = 1776;
	
	System.out.println("date2: ");
	date2.writeOutput();
	

    }
}

```

---

##Writing advanced Methods

So far the methods don't do any error checking and allow the user to set wrong dates

Lets fix that

```java
public void setDay (int inputDay)
{
    if (inputDay >=1 && inputDay <=31)
        day = inputDay;
    else       
        System.out.println("Sorry incorrect day value provided");      
}

public void setYear (int inputYear)
{
    if (inputYear >=1 || inputYear <=12)
        year = inputYear;
    else
        System.out.println("Sorry incorrect year value provided");
}

```

--

##Writing advanced Methods

```java
	public void setMonth (String inputMonth)
	{
		//One Very Long Conditional statement
	    if (inputMonth.equals("Dec") || inputMonth.equals("Nov") || inputMonth.equals("Oct")
	    		|| inputMonth.equals("Sep") || inputMonth.equals("Aug") || inputMonth.equals("Jul")
	    		|| inputMonth.equals("Jun") || inputMonth.equals("May") || inputMonth.equals("Apr")
	    		|| inputMonth.equals("Mar") || inputMonth.equals("Feb") || inputMonth.equals("Jan"))
	    {
	    	month = inputMonth;
	    }
	    else
	    	System.out.println("Sorry incorrect Month value provided"); 
	}
```

--

##Using our Methods

```java
public class DateProgram
{

    public static void main(String[] args)
    {
        Date date1, date2;

		date1 = new Date();
		date2 = new Date();
	
	        //using new methods
		date1.setMonth("Dec");
		date1.setDay(31);
		date1.setYear(2007);
	
		System.out.println("date1: ");
		date1.writeOutput();
	
	    //using no methods
		date2.setMonth("July");
		date2.setDay(4);
		date2.setYear(1776);
		
		System.out.println("date2: ");
		date2.writeOutput();
    }
}

```

<br><br>
> We see now if we try to pass incorrect data for a date, the user is given a warning message

--
 
 ##Error Checking Input Values
 
 
 <img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class3/methoderrorcheck.png>

> Even though the input parameters can take on any value allowed by that dataType, we can write our methods to ensure the proper data is provided, and provide an error message to the user when the data is incorrect


---

##`private` keyword

We have seen the public keyword a lot so far, and have shown that it controls access to member variables and methods

For example when we use the dot operator on one of our objects we see the following:

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class3/publicdotoperator.png>

<br><br>
> We see our `public` member variables, some methods we wrote, and some methods we didn't write
--

##`private` keyword

However, there is a problem with our previous code, even though we wrote methods which checks the value before the date is set, because our member variables are `public` the user can still do:

date1.String = "Whatever I want";
date2.day = 2000;
date2.year = -26;

> Because the member variables are public, the user has direct access to them, and can bypass our error checking inside the method

--

##`private keyword

We can fix the problem by making our member variables private

```java
public class Date 
{
	private String month;
	private int day;
	private int year; // a four digit number
```

> Now there is no way Java will ever let the user have direct access to the member variables, the only way they can set the data is by using the methods we provide.

<br><br>

> this is called `Encapsulation`, and is an important part of OOP

--

##Encapsulation

So now that the member variables are private, when we use the dot operator we only see the following: 

<img src="http://khengineering.github.io/FRCJavaCourse2015/Images/class3/privatedotoperator.png>


<br><br>

All of the member variables we made `private` no longer shows.

> There is no way for the user to bypass our error checking: They must use the `setYear`, `setDay`, and `setMonth` methods now

<br><br>

> In general we always make member variables private, and control how the outside program can set their value through methods, this is know as Encapsulation

---

##Multiple input parameters

We can pass multiple input parameters to one method using a comma.

```java
public void setDate(String inputMonth, int inputDate, int inputYear)
{
    month = inputMonth;
    day = inputDate;
    year = inputYear;
}
```

<br><br>

```java
date2.setDate("Dec", 12, 2014);
date2.writeOutput();
```

--

##PitFall: Bypassing your own methods

What is wrong with the previous code?

It doesn't have any error checking, so the user can still assign incorrect values for a date

`date2.setDate("Hello", -12, -2014);`

We can fix this by calling our previous set methods inside of the `setDate` method
```java
public void setDate(String inputMonth, int inputDate, int inputYear)
{
    setMonth(inputMonth);
    setDay(inputDate);
    setYear(inputYear);
}
```

--

##Note on `public` and `private` keywords

The class definition always has access to all private, and public member variables, and methods, `public` and `private` only affect what is exposed when we try to use the object in a program

---

##Main is a `void` method
A program in Java is just a class that has a `main` method

When you give a command to run a Java program, the run-time system invokes the method `main`

Note that main is a `void` method, as indicated by its heading:
`public static void main(String[] args)`

--

##println method and String 

We have been using the `println` method of the `System.out` object:

which takes in a string parameters, and does not return a value.

`System.out.println("print this statement");

> println is a void method


String is also an object and has many methods available

.equals()
.equalsIgnoreCase()

--

##Correct way to compare strings

Instead of using the isequal operator (==) for strings:

```java

String name = "Mary";

if (name == "Jerry")
{
   ....
```

<br><br>

We can use the String methods
```java

String name = "Mary";

if (name.equals("mary") )  //false because is case sensitive
{
   ....
 
OR


 if (name.equalsIgnoreCase("mary") //true because it ignores case
```

---

##More Class Definitions

Lets write some more classes using what we have learned so far

```java
public class Person
{
    private String name;
    private Date born;
    private Date died;
    
 ```
 
 > Assignment: Class write methods which will set the values of each of these variables, and methods which will return the value of each of these variables   
  

--

##Solution

```java
public class Person
{
    private String name;
    private Date born;
    private Date died;
    
    public void setName(String inputName)
    {
    	name = inputName;
    }
    
    public void setBorn(String month, int day, int year)
    {
    	born = new Date(); //instantiate object
    	
    	born.setMonth(month);
    	born.setDay(day);
    	born.setYear(year);
    	
    }
    
    public void setDied(String month, int day, int year)
    {
    	died = new Date(); //instantiate object
    	
    	died.setMonth(month);
    	died.setDay(day);
    	died.setYear(year);
    	
    }
    
    public Date getBorn()
    {
    	return born; 
    } 
    
    public Date getDied()
    {
    	return died;
    }
    
}
```

<br><br>

> We will enhance this program next week

---

##Next Class

* Constructors
* Inheritance
* PolyMorphism

1st Hands on Lab

