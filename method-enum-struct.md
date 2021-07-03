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