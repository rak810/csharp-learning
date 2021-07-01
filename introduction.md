# C# Programming Language

C# is an object oriented, strongly typed programming language. It is a part of Microsoft .NET framework. 
To run C# .NET core SDKs must be installed.
A simple C# program is as follows:
```csharp
using System;

namespace SampleCSharpApp 
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```
Every C# application must contain a class defining  ``` Main()``` method. This is the entry point of the application.
There are variations on the ``` Main() ``` method. Following codes  also can be used for method:
```csharp
// int return type, array of strings as the parameter.
static int Main(string[] args)
{
    //Must return a value before exiting
    return 0;
}

// No return type, no parameters
static void Main()
{

}

//int return type, no parameters 
static int Main()
{
    //Must return a value before exiting
    return 0;    
}

```

## Processing Command Line Arguments
---
As seen previously that  ```Main()``` method can have an argument as following  ```string[] args```. this ```args``` array of string contains the command line arguments. Following code shows print operation with command line arguments.
```csharp
static int Main(string[] args) 
{
    //Loop throug the args array using foreach
    foreach(string arg in args) 
    {
        Console.WriteLine("Arg: {0}", arg);
    }

    return 0;
}
```
Also, command-line arguments can be accessed using statc ```GetCommandLineArgs``` method of the ```System.Environment``` type. The return value if this method is an array of strings containing the arguments.
```csharp
using System;

namespace SampleCSharpApp 
{
    class Program
    {
        static void Main()
        {
            //Get the arguments using System.Environment
            string[] Args = Environment.GetCommandLineArgs();

            foreach(string arg in Args) 
            {
                Console.WriteLine("Arg: {0}", arg);
            }
        }
    }
}
```
## Basic Input Output with ```System.Console``` class
---
This class encapsulates input, output, and error-stream manipulations for console-based applications. The static methods that can be used to capture the input and output are the following:

| Function Name | Task        | 
| ------------- |:-------------:|
| ```Console.WriteLine()```  | Output a text string with newline characted in the end      | 
| ```Console.Write()``` | Output a text string without the newline character|
| ```Console.ReadLine()```| Reads the input stream until Enter key is pressed|
|```Console.Read()```| Read a single character from the input stream |

```csharp
class Program 
{
    static void Main(string[] args)
    {
        Console.WriteLine("This is a string.");
        Console.ReadLine();
    }
}
```
There are other methods  available in this class that can be used to manipulate the terminal.

### Formatting Console Output
---
Outputs can be formatted using the ```Console.WriteLine``` method. 

```csharp
/// prints -> Argument : 10
Console.WriteLine("Argument : {0}", 10);
/// prints -> 10, 20, 30
Console.WriteLine("{0}, {1}, {2}", 10, 20, 30);
```
Here in the method the first argument is the string that will be printed to the console. This string can contain place holders that can show additional data. `{}` is used as placeholder as seen in the examples. The first number of curly-bracket palce holder always begins with 0. And the remaining parameters are simply the values to be inserted into the respective placeholder.

### Formatting Numerical Data
---
Additional formatting also can be done to the numerical data.
| String Format Character | Meaning        | 
| ------------- |:-------------:|
|C or c| Used to format currency. By default ```$``` will be prefixed to the output |
|D or d| Used to format decimal numbers. Also may specify minimum padding value |
|E or e| Used for exponential notation. Casing controls the expoential constant. |
|F or f| Used for fixed-point formatting. Also may specify the minimum padding value.|
|G or g| Stands for *general*. This can be used to format fixed or expoenetial format. |
|N or n| Used for basic numerical formatting with commas. |
|X or x| Used for hexadecimal formatting. If you used and uppercase `X`, your hex format will also contain uppercase `X`|

This format character are suffixed to a given placeholder value using the colon token(e.g ```{0:C}```, ```{1:d}```, ```{2:X}```). 

```csharp
    /// outputs $99,999.00
    Console.WriteLine("c format : {0:c}", 99999);
    /// outputs 000099999
    Console.WriteLine("d9 format : {0:d9}", 99999);
    /// outputs 99999.000
    Console.WriteLine("f3 format : {0:f3}", 99999);
    /// outputs 99,999.00
    Console.WriteLine("n format : {0:n}", 99999);
    /// outputs 9.999900e+004
    Console.WriteLine("E format : {0:e}", 99999);
```
This type of formatting also can be done in other programs other than console applications. ```string.Format()``` method can help to format text data.
```csharp
    string msg = string.Format("99999 in hex is {0:x}", 99999);
```

## C# Data Types
---
C# is strongly typed programming language. So, it defines keywords for fundamental data types. These data types are defined in the ```System``` namespace. And most of them are  So every working C# program must use this namespace.  
C# is strongly typed programming language. So, it defines keywords for fundamental data types. These data types are defined in the ```System``` namespace. So every working C# program must use this namespace. And most of them are **Common Language Specification (CLS)** complaint. CLS-compliant .NET code can be used by any other .NET core programming languages like VB.NET or F#.

| C# name | CLS Compliant? | Meaning |
| ------------- |:-------------:|:-------------:|
|bool|Yes| Represents true or false|
|sbyte| No| Signed 8-bit number|
|byte| Yes| Unsigned 8-bit number|
|short|Yes| Signed 16-bit number|
|ushort|No| Unsigned 16-bit number|
|int | Yes| Signed 32-bit number|
|uint| No| Unsigned 32-bit number|
|long|Yes| Signed 64-bit number|
|ulong|No| Unsigned 64-bit number|
|char|Yes| Single 16-bit Unicode character |
|float| Yes| 32-bit floating-point number|
|double|Yes| 64-bit floating-point number|
|decimal| Yes| 128-bit signed number|
|string|Yes| Represents a set of Unicode characters|
|object|Yes| The base class of all types in the .NET framework|

Other than this data types, the ```System``` namespace defines a few useful data types for which there are no C# name/keyword. These are:
+ System.DateTime
+ System.TimeSpan
+ System.Guid
+ System.Void
  
## Variables and Constant Declaration 
---
Local variable declaration of C# is similar to C/C++. First the data type is declared and then the variable name follows.
```csharp
int myInt;
string str;
myInt = 0;
str = "This is a string";
bool b1 = true, b2 = false;
double d = 0.0;
```
In C#, there is ```default``` literal that can be used to assign a variable the default value for the data type. 
```csharp
int myInt = default;
```
Variables can be declared using ```new``` keyword also. This also sets the value of the variable to default value.

```csharp
bool b = new bool(); // Set to false.
DateTime dt = new new DateTime(); // Set to 1/1/0001 12:00:00 AM.
double d = new double(); // Set to 0.
```

![class hierarchy](images\class-hierarchy.png)

The numerical data types derive from a class named ```System.ValueType```. Descendants of this class are automatically allocated on the stack, and, therefor,e have a predictable lifetime and are quite efficient. Those types that don't belong to the ```System.ValueType``` are not allocated on the stack but on the garbage-collected heap. And all the .NET core data types are arranged in a class hierarchy. Each type is ultimately derived from the ```System.Object```, which also defines a set of methods that are common to all the types in the .NET core base class libraries.

### The ```System.Numerics``` namespace
---
This namespace defines a structure named ```BigInteger ```. This data type can be used to represent very big numerous values that are not constrained by a fixed upper or lower limit.
Also another structure ```Complex``` can model mathematically complex numerical data (eg. imaginary units, hyperbolic tangents).

## Working with Strings
---
```System.String``` provides a number of properties and methods to work with the strings. This methods can be accessed using dot operator. Also, there are static methods that can't be accessed this way. 
Some methods are following:
```csharp
string name = "Korim";
// outputs Name : Korim
Console.WriteLine("Name : {0}", name); 
// outputs Name Length : 5
Console.WriteLine("Name Length : {0}", name.Length) 
// outputs Name in uppercase : KORIM
Console.WriteLine("Name in uppercase : {0}", name.ToUpper());
// outputs Name in lowercase : korim
Console.WriteLine("Name in lowercase: {0}", name.ToLower());
// outputs Name contains o? : True
Console.WriteLine("Name contains o?: {0}", name.Contains("o"));
// outputs Name after replace : Rohim
Console.WriteLine("Name after replace: {0}", name.Replace("Kor", "Roh"));
// outputs Name : Korim
Console.WriteLine("Name : {0}", name); 
```
Here we can see that even after ```Replace()``` method the ```name``` isn't changed at all; rather a new string with the modified value was recieved as output. This is because the strings in C# are immutable. It means that the assigned to a variable can't be modified. 

