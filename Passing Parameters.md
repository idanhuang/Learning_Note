## Introduction
Introduction

## Value-type Variable Vs. Reference-type Variable

### Value-type Variable
A value-type variable contains an instance of the type. In C# value types include:
- simple/primitive type: bool, byte, char, decimal, double, float, int, long, sbyte, short, uint, ulong, ushort
- enum type
- structure type
- nullable value type

Value-type variable requires only a single segment of memory, which stores the actual data


### Reference-type Variable
Unlike the value-type variables, a reference-type variable doesn't store the values directly. Instead, it stores an address where the value is stored. In other words, a reference-type variable contains a pointer to another memory location (a.k.a, Heap) that holds the data. In C#, reference types include:
- String
- Array (even if its element are value types)
- Class
- Delegate



## Passing Variable

When passing a value-type variable from one method to another, the system will create a separate copy of the variable in another method. If the value of the variable got changed in one method, it won't affect the value in another method.
* Example 1: variable ```i``` remains unchanged even after we pass it to the ```DoubleTheValue()``` method and double its value.
```C#
public class Solution
{
    public int DoubleTheValue(int val)
    {
        return val * 2;
    }
    public static void Main(string[] args)
    {
        Solution sol = new Solution();
        int i = 2;
        int j = sol.DoubleTheValue(i);

        Console.WriteLine(i); // i = 2
        Console.WriteLine(j); // i = 4
    }
}
```
* Example 2: structure ```C``` remains unchanged even after we pass it to ```RedefineLanuage()``` method and change its fields' values.
```C#
public class Solution
{
    public struct Language
    {
        public string name;
        public bool IsOOP;

        public Language(string n, bool oop)
        {
            name = n;
            IsOOP = oop;
        }
    }

    public Language RedefineLanguage(Language language, string n, bool oop)
    {
        language.name = n;
        language.IsOOP = oop;
        return language;
    }
 
    public static void Main(string[] args)
    {
        Solution sol = new Solution();
        Language C = new Language("C", false);
        Language CPlusPlus = sol.RedefineLanguage(C, "C++", true);
        Console.WriteLine(string.Format("{0},{1}", C.name, C.IsOOP)); // C,false
    }
}
```


When passing a reference-type variable from one method to another, the system doesn't create a copy. Instead, the system passes the varaible's memory address. Hence, if the value got changed in one method, it will be reflected in another method.
* Example: If we define ```Language``` as a Class instead of a Structure, values of varaible ```C```'s field's will be changed.
```C#
public class Solution
{
    public class Language
    {
        public string name;
        public bool IsOOP;

        public Language(string n, bool oop)
        {
            name = n;
            IsOOP = oop;
        }
    }

    public Language RedefineLanguage(Language language, string n, bool oop)
    {
        language.name = n;
        language.IsOOP = oop;
        return language;
    }
 
    public static void Main(string[] args)
    {
        Solution sol = new Solution();
        Language C = new Language("C", false);
        Language CPlusPlus = sol.RedefineLanguage(C, "C++", true);
        Console.WriteLine(string.Format("{0},{1}", C.name, C.IsOOP)); // C++,true      
    }
}
```
