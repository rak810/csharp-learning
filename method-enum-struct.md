# Methods

Methods are defined by an access modifier, return type and may or may not take parameters. A method that returns a value to the caller is referred to as a function, while methods that do not return a value are commonly knowns as methods.
```csharp
// returnType MethodName (parameter_list)
int Add(int x, int y) 
{
    return x+y;
}
```
Another way of writing simple method like the example ```Add()``` that returns value is the following:
```csharp
int Add(int x, int y) => x+y;
```
From C# 7, it is possible to create methods within methods, which is officially known as *local functions*.
```csharp
int AddWrapper() 
{
    //Do something;
    return Add();

    int Add()
    {
        return x + y;
    }
}
``` 
In C# 8, local functions can be declared as *static*. By doing so, local functions can't reference the variable from the main function directly.
```csharp
/// AddWrapper() method with side effects
int AddWrapper() 
{
    //Do something;
    return Add();

    int Add()
    {
        // local function changing the variables from main function directly.
        x += 1;
        return x + y;
    }
}
```
If we don't want this or something like this to happen *static* local function should be used.

```csharp
int AddWrapper() 
{
    //Do something;
    return Add();
    // Can't access variable from the main function directly.
    static int Add()
    {
        return x + y;
    }
}
```
## Method Parameters
---
Method parameters are used to pass data into the method call. By default, a parameter is sent into a method is ***by value***. This means that a copy of the data is passed into the function.
```csharp
int Add(int x, int y)
{
    x = 5000;
    y = 1000;
    return x+y;
}
int x = 10, y = 20;
// Outputs -> Value of x : 10, value of y : 20
Console.WriteLine("Value of x : {0}, value of y : {1}", x, y);
// Outputs -> Value of Add() : 6000
Console.WriteLine("Value of Add() : {0}", Add(x, y));
// Outputs -> Value of x : 10, value of y : 20
Console.WriteLine("Value of x : {0}, value of y : {1}", x, y);
```
Following are the method parameter modifiers:
###  The ```out``` modifier
---
The methods that have been defined to take the ```out``` modified parameters are under obligation to assign them appropiate value before exiting the main function. This modifier can be used to obtain multiple values from a single method.
```csharp
// Out parameters must be assigned value by caller method
static void Add(int x, int y, out int ans)
{
    ans = x + y;
}
// Calling methods with out modifier
int ans;
Add(90, 100, out ans);
// Out parameter do not nedd to be declared before using 
Add(100, 40, out int answer);
```

###  The ```ref``` modifier
---
This can be thought as C/C++ pass by reference. This modifier can be used to work on data in the caller's scope. There are some distinction between ```out``` and ```ref``` modifiers:
+ Output parameters do not need to be initialized before they are passed to the method. The reason for this is that the method must assign output parameters before exiting.
+ Reference parameters must be initialized before they are passed to the method. The reason for this is that  you are passing a reference to an existing variable. If it isn't assinged to an initial value, that would be equivalent of operating on unassigned local variable.

```csharp
// ref modifier
void SwapStrings(ref string s1, ref string s2)
{
    string temp = s1;
    s1 = s2;
    s2 = temp;
}
string str1 = "Flip";
string str2 = "Flop";
// outputs -> Before: Flip, Flop
Console.WriteLine("Before: {0}, {1} ", str1, str2);
SwapStrings(ref str1, ref str2);
// outputs -> After: Flop, Flip
Console.WriteLine("After: {0}, {1} ", str1, str2);
``` 

### The ```in``` modifier
---
The ```in``` modifier passes a value by reference and prevents the caller from modifying the value.
```csharp
static int Add(in int x, in int y)
{
    /// Following causes error. in makes variable read only.
    x = 100;
    y = 200;
    return x + y;
}
```

### The ```params``` modifier
---
The ```params``` modifier allows you to pass into a method a variable number of identically typed parameters as a single logical parameter. This helps us to pass any number of arguments of same type to methods. To avoid ambiguity, only a single ```params``` argument can be passed.

```csharp
static double CalcAvg(params double[] values)
{
    double sum = 0;
    if (values.Length == 0) 
    {
        return sum;
    }
    for (int i = 0; i < values.Length; i++)
    {
        sum+=values[i];
    }

    return (sum/values.Length);
}



double avg = CalcAvg(4.0, 3.2, 4.7, 54);
double[] data = {3.0, 2.0, 4.5};
avg = CalcAvg(data);
```

## Defining Optional Parameters
---
C# allows you to create method that can take optional arguments. This technique allows the caller to invoke as ingle method while omitting arugments deemed unnecessary. Assigned value must be known at the compile time and cannot be resolved at runtime.
```csharp
// owner variable has a default value 
static void PrintData(string msg, string owner = "Donnie")
{
    Console.WriteLine("Message : {0}", msg);
    Console.WriteLine("Owner : {0}", owner);
}
// output -> Message : I'm a walrus
// output -> Owner : Donnie
PrintData("I'm a walrus");

// output -> Message : Forget it, Donny
// output -> Owner : Walter
PrintData("Forget it, Donny", "Walter");

```

## Using Named Arguments
---
NAmed arguments allow us to invoke a method by specifying parameter values in any order we choose. 

```csharp
static void DisplayMsg(ConsoleColor textColor, string msg)
{
    Console.ForegroundColor = textColor;
    Console.WriteLine(msg);
}

// default way to calling the method 
DisplayMsg(ConsoleColor.DarkRed, "Jesus Quintana");
// calling the method using named arguments. Position doesn't matter.
DisplayMsg(msg: "Jesus Quintana", textColor: ConsoleColor.DarkRed);

```
## Method Overloading
---
Like other modern object-oriented programming languages C# allows method overloading. This means that we can have identically named methods but with different types and number of arguments.

```csharp
static int Add()
{
    return x + y;
}

static double Add(double x, double y)
{
    return x + y;
}

static long Add(long x, long y)
{
    return x + y;
}
```

# The ```enum``` Type

This is similar to the C/C++ ```enum```. This type can define named values and corresponding discrete numerical values.
```csharp
enum EmpTypeEnum
{ 
    Manager,        // = 0
    Grunt,          // = 1
    Contractor,     // = 2
    VicePresident   // = 3
}
```
Here ```EmpTypeEnum``` enumeration defines four named constants, corresponding to discrete numerical values. By default the first elemenet is set to the value zero(0). Enumeration doesn't need to have any sequential. The enumeration values are stored using C# ```int``` data type. This also can be changed.
```csharp
enum EmpTypeEnum : byte
{
    Manager = 10,
    Grunt = 1,
    Contractor = 100,
    VicePresident = 9
}
```
Enumerations can be declared as following:
```csharp
EmpTypeEnum emp = EmpTypeEnum.Grunt;
```
Enumeration gain functionality from the ```System.Enum``` class type. This class defines a number of methods that allow you to interrogate and transform a given enumeration. Some of them are following:

```csharp
EmpTypeEnum emp = EmpTypeEnum.Contractor;
// outputs -> EmpTypeEnum uses a byte storage
Console.WriteLine("EmpTypeEnum uses a {0} storage", Enum.GetUnderlyingType(emp.GetType()));
//Dynamically discovering name-value pairs
// outputs -> emp is Contractor
Console.WriteLine("emp is {0}", emp.ToString());
```
# Structure (Value Type)

A structure is a user defined type. It can contain any number of data fields and member that operate on these fields.
```csharp
struct Point
{
    public int X;
    public int Y;

    public void Increment()
    {
        X++;
        Y++;
    }

    public void Decrement()
    {
        X--;
        Y--;
    }

    public void Display()
    {
        Console.WriteLine("X = {0}, Y = {Y}", X, Y);
    }

}
```
There are different ways to create a structure variable. Also, the custom constructors are also possible. But the default constructor can't be edited.
```csharp
// Must assign all the public field data
Point p1;
p1.X = 10;
p1.Y = 30;
p1.Display();

// Using constructor will assign default values
Point p2 = new Point();
p1.Display();
```
# Tuples

Tuples are lightweight data structures that contain multiple fields. Tuple items can have different data types.
```csharp
(string, int, string) val1 = ("a", 5, "c");
var val2 = ("a", 1.5, 3, "fh");
```

By default compiler assigns each property the name name **```ItemX```**, where X represents the one-based position in the tuple.
```csharp
Console.WriteLine($"First item : {val1.Item1}");
Console.WriteLine($"Second item : {val1.Item2}");
Console.WriteLine($"Third item : {val1.Item3}");
```
But specific names also can be provided in following ways:
```csharp
(string a, string b, int c) vals = ("aafg", "fg", 3);
var vals = (a: "df", b: "dtrt", c: 3);
(int, int) exp = (custom1: 43, custom2: 645);
```
They can be accessed with their specified names.
```csharp
Console.WriteLine($"First item : {vals.a}");
Console.WriteLine($"Second item : {vals.b}");
Console.WriteLine($"Third item : {vals.c}");
```
Tuples can be used as method return values. 
```csharp
static (int, string, bool) getVals()
{
    return (9, "White boy summer", true);
}

var samples = getVals();
Console.WriteLine($"First item : {samples.Item1}");
Console.WriteLine($"Second item : {samples.Item2}");
Console.WriteLine($"Third item : {samples.Item3}");
```