## Introduction
Introduction

## Value-type Variable Vs. Reference-type Variable

### Value-type Variable
A value-type variable contains an instance of the type. In C# value types include:
- simple/primitive type: bool, byte, char, decimal, double, float, int, long, sbyte, short, uint, ulong, ushort
- enum type
- structure type
- nullable value type

Value-type variable requires only a single segment of memory, which stores the actual data. Value-Type variable is stored in the stack.


### Reference-type Variable
Unlike the value-type variables, a reference-type variable doesn't store the values directly. Instead, it stores an address where the value is stored. In other words, a reference-type variable contains a pointer to another memory location (a.k.a, Heap) that holds the data. In C#, reference types include:
- String
- Array (even if its element are value types)
- Class
- Delegate

Reference-type variable has two segments of memory. The actual data is stored in the Heap while the refence is stored in the stack.


## Passing Variables

When passing a reference-type variable from one method to another, the system doesn't create a copy. Instead, the system passes the varaible's memory address. Hence, if the value got changed in one method, it will be reflected in another method.

When passing a value-type variable from one method to another, the system will create a separate copy of the variable in another method. If the value of the variable got changed in one method, it won't affect the value in another method.

## Passing Value-type Variable

* Passing Value-type Variable by Value

* Example 1: variable ```i``` remains unchanged even after we pass it to the ```DoubleTheValue()``` method and double its value.
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

* Example 2: structure ```C``` remains unchanged even after we pass it to ```RedefineLanuage()``` method and change its value.
```C#
public class Solution
{
    public struct Language
    {
        public string name;

        public Language(string n)
        {
            name = n;
        }
    }

    public Language RedefineLanguage(Language language, string n)
    {
        language.name = n;
        return language;
    }

    public static void Main(string[] args)
    {
        Solution sol = new Solution();
        Language C = new Language("C");
        Language CPlusPlus = sol.RedefineLanguage(C, "C++");
        Console.WriteLine(C.name); // C
    }
}
```

* Passing Value-type Variable by Reference
* Example 1: 
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
* Example 2: 
```C#
public class Solution
{
    public struct Language
    {
        public string name;

        public Language(string n)
        {
            name = n;
        }
    }

    public Language RedefineLanguage(ref Language language, string n)
    {
        language.name = n;
        return language;
    }

    public static void Main(string[] args)
    {
        Solution sol = new Solution();
        Language C = new Language("C");
        Language CPlusPlus = sol.RedefineLanguage(ref C, "C++");
        Console.WriteLine(C.name); // C++
    }
}
```


## Passing Reference-type Variable

* Passing Reference-type Variable by Value 
```C#
public class Solution
{
    public void ChangeArray(int[] arr)
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
        sol.ChangeArray(arr);
        Console.WriteLine(arr[0]); // 2
    }
}
```

* Passing Reference-type Variable by Reference


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
