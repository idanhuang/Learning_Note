## Mutability And Immutability
An immutable object is an object whose state cannot be modified after it's created.This is in contrast to a mutable object, which have methods to change the value of the object.

```String``` is an example of immutable object, while ```StringBuilder``` is a mutable object that has method to change its value.

```C#
string str = "hello";
str[0] = 'H'; // compile error. string[int] is read-only.
string str1 = str.ToUpper(); // str1 = "HELLO", str = "hello"
```

```C#
// StringBuilder Example
StringBuilder sb = new StringBuilder("hello");
sb.Append("world");   // helloworld
sb.Remove(0, 5);      // world
sb.Replace('o', 'O'); // wOrld
sb.Insert(0, "hello");// hellowOrld
```

## Differences between String and StringBuilder
```String``` is an immutable object. To add something to the end of a ```String```, program will create a new String object, and then point the reference to the new object. While ```StringBuilder``` is a mutable object. When adding something to the end of a ```StringBuilder```, reference will point at the same object.

Using immutable object ```String``` to concatenate strings will create a lot of temporary copies. Suppose we concatenate n strings, then the first the string will be copied n times, the second string will be copied n - 1 times, and so on. So it will take O(N^2) to concatenate n strings. ```StringBuilder``` uses an internal data structure which helps minimize the copying. So when concatenating a large number of strings, it's better to use ```StringBuilder```.

![](https://github.com/idanhuang/Learning_Note/blob/main/img/concatenate_strings.PNG)

```C#
// concatenate strings by using String
string str = "a";
str = str + "b";

// concatenate strings by using StringBuilder
StringBuilder sb = new StringBuilder("a");
sb.Append("b");
```


### References
1. https://en.wikipedia.org/wiki/Immutable_object
2. https://web.mit.edu/6.005/www/fa16/classes/09-immutability/#:~:text=Other%20objects%20are%20mutable%3A%20they,example%20of%20a%20mutable%20type
3. https://social.msdn.microsoft.com/Forums/vstudio/en-US/c0c45944-dcf0-4732-8e87-845fcc1e8f6b/stringbuilder-method-performance?forum=csharpgeneral
