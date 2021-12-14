A class is a user-defined data type that is composed of field data and members that operate on this data (such as constructors, properties, methods, events etc.). A set of field data represents the "state" of a class instance or object. Class type is the most fundamental programming construct of .NET platform.
```csharp
class Car
{
    // The state of the Car
    public string petName;
    public int currSpeed;

    //The functionality of the Car
    public void PrintState()
        => Console.WriteLine("{0} is going {1} MPH", petName, currSpeed);
    
    public void speedUp(int delta)
        => currspeed += delta;
}
```
The example class ```Car``` has two public field members and two public method that work on the field data members.  
