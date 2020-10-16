# Shallow Copy and Deep Copy
## Shallow Copy
### Example
```C#
using System;

public class StringClass
{
    public string strVal;

    public StringClass(string str)
    {
        strVal = str;
    }
}
public class CopyTest
{
    public int intVal { get; set; }
    public int[] intArr { get; set; }

    public StringClass strClass { get; set; }

    public CopyTest(int val, int[] arr, StringClass strclass)
    {
        intVal = val;
        intArr = arr;
        strClass = strclass;
    }

    public static void Main(string[] args)
    {
        CopyTest ct1 = new CopyTest(1, new int[] { 1, 2, 3, 4 }, new StringClass("str1"));
        // CopyTest ct2 = ct1; // Assignment operator will do a shallow copy
        CopyTest ct2 = (CopyTest)ct1.MemberwiseClone();
        Console.WriteLine("Orignal Data:");
        Console.WriteLine("ct1: " + ct1.intVal + ", " + ct1.intArr[0] + ", " + ct1.strClass.strVal);
        Console.WriteLine("ct2: " + ct2.intVal + ", " + ct2.intArr[0] + ", " + ct2.strClass.strVal);

        ct1.intVal = 2;
        ct1.intArr[0] = 3; // new int[]{ 5,6,7,8,9 };
        ct1.strClass.strVal = "newStr";
        Console.WriteLine("Updated Data:");
        Console.WriteLine("ct1: " + ct1.intVal + ", " + ct1.intArr[0] + ", " + ct1.strClass.strVal);
        Console.WriteLine("ct2: " + ct2.intVal + ", " + ct2.intArr[0] + ", " + ct2.strClass.strVal);
    }
}
```
### Output
Orignal Data:</br>
ct1: 1, 1, str1</br>
ct2: 1, 1, str1</br>
Updated Data:</br>
ct1: 2, 3, newStr</br>
ct2: 1, 3, newStr</br>

</br></br>

## Deep Copy
### Example
```C#
using System;

public class StringClass
{
    public string strVal;

    public StringClass(string str)
    {
        strVal = str;
    }
}
public class CopyTest
{
    public int intVal { get; set; }
    public int[] intArr { get; set; }
    public StringClass strClass { get; set; }

    public CopyTest(int val, int[] arr, StringClass strclass)
    {
        intVal = val;
        intArr = arr;
        strClass = strclass;
    }

    public static void Main(string[] args)
    {
        CopyTest ct1 = new CopyTest(1, new int[] { 1, 2, 3, 4 }, new StringClass("str1"));
        int[] arr2 = new int[ct1.intArr.Length];
        Array.Copy(ct1.intArr, arr2, ct1.intArr.Length);
        CopyTest ct2 = new CopyTest(ct1.intVal, arr2 , new StringClass(ct1.strClass.strVal));
        Console.WriteLine("Orignal Data:");
        Console.WriteLine("ct1: " + ct1.intVal + ", " + ct1.intArr[0] + ", " + ct1.strClass.strVal);
        Console.WriteLine("ct2: " + ct2.intVal + ", " + ct2.intArr[0] + ", " + ct2.strClass.strVal);

        ct1.intVal = 2;
        ct1.intArr[0] = 3; // new int[]{ 5,6,7,8,9 };
        ct1.strClass.strVal = "newStr";
        Console.WriteLine("Updated Data:");
        Console.WriteLine("ct1: " + ct1.intVal + ", " + ct1.intArr[0] + ", " + ct1.strClass.strVal);
        Console.WriteLine("ct2: " + ct2.intVal + ", " + ct2.intArr[0] + ", " + ct2.strClass.strVal);
    }
}
```

### Output
Orignal Data:</br>
ct1: 1, 1, str1</br>
ct2: 1, 1, str1</br>
Updated Data:</br>
ct1: 2, 3, newStr</br>
ct2: 1, 1, str1</br>
