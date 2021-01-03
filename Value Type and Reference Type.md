## Variable and Type
A variable can be thought of a memory location (paired with an associated symbolic name) that holds values of a specific type. The value in a variable may change during the life of the program, hence the memory location is called "variable". Each variable has a specific type that indicates which type of value the variable holds. For example, a variable that holds an integer value is called integer variable.


## Value Type Vs. Reference Type
A value-type variable holds the value within its own memory location. It requires only a single segment of memory located in the Stack. In C# value types include:
- simple/primitive type: bool, byte, char, decimal, double, float, int, long, sbyte, short, uint, ulong, ushort
- enum type
- structure type (even if their members are reference types)
- nullable value type (since the underlying type is always simple types)


Unlike value-type variables, a reference-type variable doesn't hold values directly. Instead, it stores a reference, which points at another memory segment where the actual value is stored. A reference-type variable has two segments of memory. The actual data is stored in the Heap, while the reference is stored in the Stack. In C#, reference types include:
- String
- Array (even if its element are value types)
- Class
- Delegate

![](https://github.com/idanhuang/Learning_Note/blob/main/img/value_type_and_reference_type.PNG)


## Passing Variable
In general, when passing a value-type variable from one method to another, the system will create a copy of the variable in the calling method and pass it to the called method. If the value of the variable got changed in the called method, it won't affect the value in the calling method, and vice versa. 

When passing a reference-type variable from one method to another, the system doesn't create a copy. Instead, the system passes the variable's memory address (a.k.a., reference) from the calling method to the called method. Hence, if the value got changed in one method, it will be reflected in another method.


### Passing Value Type by Value
```i``` is a integer variable, which is a value-type variable. Its value remains unchanged int the ```Main()``` even after we pass it to the ```DoubleTheValue()``` and change its value.
```C#
public class Solution
{
    public void DoubleTheValue(int val)
    {
        val = val * 2; // val = 4
    }
    
    public static void Main(string[] args)
    {
        int i = 2;
        Solution sol = new Solution();        
        sol.DoubleTheValue(i);
        Console.WriteLine(i); // i = 2
    }
}
```

### Passing Value Type by Reference
In C#, we use ```ref``` or ```out``` to pass a variable by reference. In the following example, we pass the reference of ```i``` from ```Main()``` to ```DoubleTheValue()```, and the change is persist in called method ```DoubleTheValue()``` and calling method ```Main()```.
```C#
public class Solution
{
    public void DoubleTheValue(ref int val)
    {
        val = val * 2; // val = 4
    }
    
    public static void Main(string[] args)
    {
        int i = 2;
        Solution sol = new Solution();        
        sol.DoubleTheValue(ref i);
        Console.WriteLine(i); // i = 4
    }
}
```

### Passing Reference Type by Value 
When passing a reference type variable by value, it is possible to change the variable's value. However, we cannot change the reference itself, which is the memory address. For example, we CANNOT use the same reference to allocate new memory for a new object and have it persist in the calling method.

In the below example, ```arr``` is a reference-type variable and we pass it to ```ChangeArray()``` by value. It is possible to change the values of the array elements, but the attempt to allocate a new memory location for ```arr``` only  works inside the ```ChangeArray()```. In this case, when passing ```arr``` from ```Main``` to ```ChangeArray()```, a copy of ```arr``` is passed to ```ChangeArray()```, and any changes on the copied reference only take effect inside ```ChangeArray()```, but will not affect the orignal array in ```Main()```.
```C#
public class Solution
{
    public void ChangeArray(int[] arr)
    {
        for (int i = 0; i < arr.Length; i++)
            arr[i] = 2 * arr[i]; // this change is persist in the ChangeArray() and Main()

        arr = new int[] { 100, 100, 100 };
        Console.WriteLine(arr[0]); // 100. This change is local.
    }

    public static void Main(string[] args)
    {
        int[] arr = new int[] { 1, 2, 3 };
        Solution sol = new Solution();
        sol.ChangeArray(arr);
        Console.WriteLine(arr[0]); // 2
    }
}
```

### Passing Reference Type by Reference
In the following example we pass a reference-type variable by reference using ```ref```, thus any changes inside the called method will affect the calling method.
```C#
public class Solution
{
    public void ChangeArray(ref int[] arr)
    {
        for (int i = 0; i < arr.Length; i++)
            arr[i] = 2 * arr[i];

        arr = new int[] { 100, 100, 100 };
        Console.WriteLine(arr[0]); // 100
    }

    public static void Main(string[] args)
    {
        int[] arr = new int[] { 1, 2, 3 };
        Solution sol = new Solution();
        sol.ChangeArray(ref arr);
        Console.WriteLine(arr[0]); // 100
    }
}
```

### Special Case - Passing Immuable Reference Type
Immutable references like ```string``` behave just like regular refernce type except it doesn't provide a way to change its value when passing it by value. In the following example, when passing ```string``` type variable ```str``` to ```ChangeString()```, even the value of ```str``` is changed inside ```ChangeString()```, the change doesn't affect ```str``` in the calling method. 
```C#
public class Solution
{
    public void ChangeString(string str)
    {
        str = str.ToUpper(); // HELLO
        str = "Hello World"; // Hello World
    }

    public static void Main(string[] args)
    {
        Solution sol = new Solution();
        string str = "hello";
        sol.ChangeString(str);
        Console.WriteLine(str); // hello
    }
}
```

In order to keep the change persist in both calling method and called method, we need to pass the ```string``` type variable by reference.
```C#
public class Solution
{
    public void ChangeString(ref string str)
    {
        str = str.ToUpper(); // HELLO
        str = "Hello World"; // Hello World
    }

    public static void Main(string[] args)
    {
        Solution sol = new Solution();
        string str = "hello";
        sol.ChangeString(ref str);
        Console.WriteLine(str); // Hello World
    }
}
```

#### References
1. https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/passing-reference-type-parameters
2. http://www.leerichardson.com/2007/01/parameter-passing-in-c.html
