# <b>Array</b>

Array are used to store multiple values of same data types. 

```csharp
string[] names; // for basic declaration

string[] names = {"Rakib", "Akib", "Shafin"};


// we can store any data-types
int[] roll = {74, 119, 115};


// To create an array with n elements to store letter
string[] names = new string[n];
```
<br>
<br>

To access array elements and assign

```csharp
Console.WriteLine(names[0]);

names[1] = "Saidul";
```
<br><br>

### Passing array to functions
<br>

```csharp
using Sytem;
public class Pass_Array{
    
    // Printing array function
    static void print_my_Array( int[] my_arr )
    {

        Console.Write("Your array is : ");
        
        for(int i = 0; i < my_arr.Length; i++)
        {
            Console.Write(my_arr[i]);
        }

        Console.WriteLine();
    }


    // Main function
    public static void Main(string[] args)
    {
        int[] arr = {1,2,3,4,5,6,7,8,9,10};
        print_my_Array(arr); // the array passed to the print_my_Array function
    }

}
```

<br>

## <b>Multidimensional Array</b>

<br>

The multidimensional array is also known as rectangular arrays in C#. It can be two dimensional or three dimensional. The data is stored in tabular form (row * column) which is also known as matrix.

```csharp
int[,] arr_2d = new int[4,4]; // 2D array

int[,,] arr_3s = new int[4.4.4]; // 3D array
```

Example <br>
There are 3 ways to initialize multidimensional array in C#

```csharp
int[,] arr = new int[3,3]= { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };  

// omit the array size
int[,] arr = new int[,]{ { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };  

// declaration and initialization at same time
int[,] arr = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };  
```
---

<br>Example<br>
An example of a multidimentsional array given

```csharp
using System;  
public class MultiArrayExample  
{  
    public static void Main(string[] args)  
    {  
        int[,] arr = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };

        for(int i=0;i<3;i++){  

            for(int j=0;j<3;j++){  
                Console.Write(arr[i,j]+" ");  
            }  
            Console.WriteLine();  
        }  
    }  
} 

/******

Output will be : 

1 2 3
4 5 6
7 8 9

*******/
```
---

<br>
<b>Example 3D array</b> <br>

An example of a 3D array given 
<br>

```csharp

using System;

public class Program
{
	public static void Main()
	{
		int[,,] arr3d1 = new int[1, 2, 2]{
			{{1, 2}, {3, 4}} // 1 row of two-dimensional array
		};
		
		int[,,] arr3d2 = new int[2, 2, 2]{ // 2 rows of two-dimensional array
			{{1, 2}, {3, 4}}, 
			{{5, 6}, {7, 8}}
		};
		
		int[,,] arr3d3 = new int[2, 2, 3]{ // 2 rows of two-dimensional array
			{{1, 2, 3}, {4, 5, 6}}, 
			{{7, 8, 9}, {10, 11, 12}}
		};
		
		Console.WriteLine("arr3d2 Values");
		Console.WriteLine(arr3d2[0, 0, 0]); // return 1
		Console.WriteLine(arr3d2[0, 0, 1]); // return 2
		Console.WriteLine(arr3d2[0, 1, 0]); // return 3
		Console.WriteLine(arr3d2[0, 1, 1]); // return 4
		Console.WriteLine(arr3d2[1, 0, 0]); // return 5
		Console.WriteLine(arr3d2[1, 0, 1]); // return 6
		Console.WriteLine(arr3d2[1, 1, 0]); // return 7
		Console.WriteLine(arr3d2[1, 1, 1]); // return 8
	}
}

```
In the above example, <br><br>
[1, 2, 2] of arr3d1 specifies that it will contain one row of two-dimensional array [2, 2].<br><br>
arr3d2 specifies dimensions [2, 2, 2], which indicates that it includes two rows of two-dimensional array of [2, 2]. <br><br>
Thus, the first rank indicates the number of rows of inner two-dimensional arrays. 

---

<br>
<b>Example 4D array</b> 
<br>

An example of a 4D array given 
<br>

```csharp
using System;

public class Program
{
	public static void Main()
	{
		int[,,,] arr4d1 = new int[1, 1, 2, 2]{
			{
				{{1, 2}, {3, 4}}
			}
		};
		
		int[,,,] arr4d2 = new int[1, 2, 2, 2]{
			{
				{{1, 2}, {3, 4}},
				{{5, 6}, {7, 8}}
			}
		};
		
		Console.WriteLine("arr4d1");
		Console.WriteLine(arr4d1[0, 0, 0, 0]); // return 1
		Console.WriteLine(arr4d1[0, 0, 0, 1]); // return 2
		Console.WriteLine(arr4d1[0, 0, 1, 0]); // return 3
		Console.WriteLine(arr4d1[0, 0, 1, 1]); // return 4
		
		Console.WriteLine("arr4d2");
		Console.WriteLine(arr4d2[0, 0, 0, 0]); // return 1
		Console.WriteLine(arr4d2[0, 0, 0, 1]); // return 2
		Console.WriteLine(arr4d2[0, 0, 1, 0]); // return 3
		Console.WriteLine(arr4d2[0, 0, 1, 1]); // return 4
		Console.WriteLine(arr4d2[0, 1, 0, 0]); // return 5
		Console.WriteLine(arr4d2[0, 1, 0, 1]); // return 6
		Console.WriteLine(arr4d2[0, 1, 1, 0]); // return 7
		Console.WriteLine(arr4d2[0, 1, 1, 1]); // return 8
	}
}
```

In the above example, the four-dimensional array arr4d1 specifies [1, 1, 2, 2], which indicates that it includes one row of the three-dimensional array.

---

## <b>Jagged Array</b>
<br>
Jagged array is also known as "array of arrays". That means it contains array.
Its data type is array so it will declare using " type_of_array[]"<br>
<br>
An example is given: <br>

```csharp
int[][] arr = new int[2][]; // jagged array with 2 elements
int[][] arr = new int[n][]; // with n elements
```
<br>

Example of initialization of jagged array
```csharp
// The element array size can be different
arr[0] = new int[4]; 
arr[1] = new int[3];

// Initialization with elements
arr[0] = new int[4] { 1, 2, 3, 4 };
arr[1] = new int[3] { 5, 6, 7 };


// Size of elements-array in jagged array is optional

arr[0] = new int[] { 1, 2, 3, 4, 5, 6, 7, 8};
arr[1] = new int[] { 9, 10 };
```
<br>

<b>Jagged array example 01:</b>

```csharp
public class JaggedArrayTest  
{  
    public static void Main()  
    {  
        int[][] arr = new int[2][];// Declare the array  
  
        arr[0] = new int[] { 1, 2, 3, 4 };// Initialize the array          
        arr[1] = new int[] { 5, 6, 7, 8, 9, 10 };  
  
        // Traverse array elements  
        for (int i = 0; i < arr.Length; i++)  
        {  
            for (int j = 0; j < arr[i].Length; j++)  
            {  
                System.Console.Write(arr[i][j]+" ");  
            }  
            System.Console.WriteLine();  
        }  
    }  
} 

/* Output will be:

1 2 3 4
5 6 7 8 9 10

*/
```
<br>

<b>Jagged array example 02:</b>

```csharp
public class JaggedArrayTest  
{  
    public static void Main()  
    {  
		// initialization of jagged array while declaration
        int[][] arr = new int[3][]{  
        new int[] { 1, 2, 3, 4 },  
        new int[] { 5, 6, 7, 8, 9, 10 },  
        new int[] { 11, 12 }  
        };  
  
        for (int i = 0; i < arr.Length; i++)  
        {  
            for (int j = 0; j < arr[i].Length; j++)  
            {  
                System.Console.Write(arr[i][j]+" ");  
            }  
            System.Console.WriteLine();  
        }  
    }  
} 

/* Ouput will be:
1 2 3 4
5 6 7 8 9 10
11 12
/*
```

<br>
<br>
<br>
<br>
The resources are : <br>
<ul>
<li><a href="https://www.javatpoint.com/c-sharp-arrays">Javapoint</a</li>
<li><a href="https://www.geeksforgeeks.org/c-sharp-jagged-arrays/">GFG</a</li>
<li><a href="https://www.tutorialsteacher.com/csharp/csharp-multi-dimensional-array">Tutorials_Teacher</a</li>