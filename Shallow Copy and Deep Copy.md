# Shallow Copy and Deep Copy

## Introduction
In object-oriented programming, object copying is creating a copy of an existing object. The result object is called object copy or simply copy. There are two main copy methods: Shallow Copy and Deep Copy.

## Shallow Copy
Shallow copy is a field by field copy. If the field value is a primitive type, then shallow copy copies the value. If the field value is a reference type, then shallow copy copies the reference, i.e., source and copy share the same memeory. 

![Shallow Copy](img/ShallowCopy.PNG)


## Deep Copy
Deep Copy is a process of creating a new object and then copying the fields of the source object to the object copy. If the field is a value type, then deep copy copies the value. If the field is a reference type, then the copy will have different memory.

![Deep Copy](img/DeepCopy.PNG)

## Example
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
    public int intVal { get; set; }  // primitive type
    public int[] intArr { get; set; } // reference type
    public StringClass strClass { get; set; } // reference type

    public CopyTest ShallowCopy(CopyTest copyTest)
    {
        return (CopyTest)copyTest.MemberwiseClone();
    }

    public CopyTest DeepCopy(CopyTest copyTest)
    {
        CopyTest cp = (CopyTest)copyTest.MemberwiseClone();
        cp.strClass = new StringClass(copyTest.strClass.strVal);
        cp.intArr = new int[copyTest.intArr.Length];
        for (int i = 0; i < copyTest.intArr.Length; i++)
            cp.intArr[i] = copyTest.intArr[i];
        return cp;
    }

    public static void Main(string[] args)
    {
        CopyTest ct1 = new CopyTest();
        ct1.intVal = 1;
        ct1.intArr = new int[] { 1, 2, 3 };
        ct1.strClass = new StringClass("str1");

        // Shallow Copy
        CopyTest ct2 = ct1.DeepCopy(ct1);

        // Deep Copy
        // CopyTest ct2 = ct1.DeepCopy(ct1);
        
        Console.WriteLine("Orignal Data:");
        Console.WriteLine("ct1: " + ct1.intVal + ", " + ct1.intArr[0] + ", " + ct1.strClass.strVal);
        Console.WriteLine("ct2: " + ct2.intVal + ", " + ct2.intArr[0] + ", " + ct2.strClass.strVal);

        ct1.intVal = 2;
        ct1.intArr[0] = 4;
        ct1.strClass.strVal = "str2";
        Console.WriteLine("Updated Data:");
        Console.WriteLine("ct1: " + ct1.intVal + ", " + ct1.intArr[0] + ", " + ct1.strClass.strVal);
        Console.WriteLine("ct2: " + ct2.intVal + ", " + ct2.intArr[0] + ", " + ct2.strClass.strVal);
    }
}
```
### Shallow Copy Output
Orignal Data:</br>
ct1: 1, 1, str1</br>
ct2: 1, 1, str1</br>
Updated Data:</br>
ct1: 2, 4, str2</br>
ct2: 1, 4, str2</br>

### Deep Copy Output
Orignal Data:</br>
ct1: 1, 1, str1</br>
ct2: 1, 1, str1</br>
Updated Data:</br>
ct1: 2, 4, str2</br>
ct2: 1, 1, str1</br>
