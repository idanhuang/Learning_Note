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


### References
1. https://en.wikipedia.org/wiki/Immutable_object
2. https://web.mit.edu/6.005/www/fa16/classes/09-immutability/#:~:text=Other%20objects%20are%20mutable%3A%20they,example%20of%20a%20mutable%20type.
