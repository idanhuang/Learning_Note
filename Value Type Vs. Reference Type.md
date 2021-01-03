## Variable Vs. Type
A variable can be thought of a memory location that holds values of a specific type. The value in a variable may change during the life of the program, hence the memory location is called "variable". Each variable has a specific type, which indicates which type of data the variable may hold. For example, a varaible that holds an integer so it is called integer variable.


## Value Type Vs. Reference Type
A value type holds the value within its own memory location. It requires only a single segment of memory and is stored in the Stack. In C# value types include:
- simple/primitive type: bool, byte, char, decimal, double, float, int, long, sbyte, short, uint, ulong, ushort
- enum type
- structure type
- nullable value type


Unlike value type, reference type doesn't hold value directly. Instead, it stores an address (called reference) where the data is stored. Reference type requires two segments of memory. The actual data is stored in the Heap, while the reference is stored in the Stack. In C#, reference types include:
- String
- Array (even if its element are value types)
- Class
- Delegate


## Passing Variable
In general, when passing a value-type variable from one method to another, the system will create a copy of the variable in the calling method and pass it to the called method. If the value of the variable got changed in the called method, it won't affect the value in the calling method, and vice versa. 

When passing a reference-type variable from one method to another, the system doesn't create a copy. Instead, the system passes the varaible's memory address (a.k.a., reference) from the calling method to the called method. Hence, if the value got changed in one method, it will be reflected in another method.


### Passing Value Type by Value
variable ```i``` remains unchanged even after we pass it to the ```DoubleTheValue()``` method and change its value.
```C#
public class Solution
{
    public void DoubleTheValue(int val)
    {
        val = val * 2;
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
variable ```i```'s value is changed from 2 to 4 after we pass it to the ```DoubleTheValue()``` method since we pass the reference of ```i```. In C#, we use ```ref``` or ```out``` to pass a variable by reference.
```C#
public class Solution
{
    public void DoubleTheValue(ref int val)
    {
        val = val * 2;
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
When passing a reference type variable by value, it is possible to change the value that the reference points to. However, we cannot change the value (memory address) of the reference itself. For example, we can use the same reference to allocate new memory for a new object and have it persist in the calling method.

In the below example, ```arr``` is a reference-type variable and we pass it to ```ChangeArray()``` by value. It is possible to change the values of the array elements, but the attempt to allocate a new memory location for ```arr``` only  works inside the ```ChangeArray()``` method. In this example, a copy of the reference that points to ```arr``` is passed to ```ChangeArray()```. Any changes on the copied reference will not affect the orignal array.
```C#
public class Solution
{
    public void ChangeArray(int[] arr)
    {
        for (int i = 0; i < arr.Length; i++)
            arr[i] = 2 * arr[i]; // this change is persist in the calling method

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

## Immutable reference type
Immutable reference like ```string``` behaves like regular refernce type except it doesn't provide a way to change its value. In the following example, when passing ```string``` type variable ```str``` to ```ChangeString()```, even the value of ```str``` is changed inside ```ChangeString()```, the change doesn't affect the calling method. 
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

In order to keep the change persit in both calling method and called method, we need to pass the ```string``` type variable by reference.
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
3. https://www.oreilly.com/library/view/writing-word-macros/9781565927254/ch05s04.html#:~:text=A%20variable%20can%20be%20thought,of%20data%20it%20may%20hold.
