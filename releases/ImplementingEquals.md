## Implementing equals method.

In this post, I will try to explain how to implement the equals. 

First of all, why should we implement the equals method? In java, equals operator "==" works as expected for only primitive types because they locate in Stack memory. 

As for Object types, which locate in heap memory, it does not work as expected because the operator compares their memory addresses but their values.

```java

Integer a=new Integer(10);
Integer b=new Integer(10);

a==b //false

```

That is why java objects have got the equals method. In java, every class is inherited from the **Object** class explicitly or implicitly. Therefore, your classes have the equals method even without you implemented it. The declaration of the equals method in the Object class looks like
   
```java 
public boolean equals(Object other){
    ...
}
```
This default implementation of the equals method compares the memory address of two objects to check if they are equal. 
Therefore, if you want to compare your objects' values instead of their memory addresses, you need to reimplement the equals method in your class. It is called method **overriding**.  

However, to use method overriding, the signature (declaration) of a method should match with the signature of its parent class. Let's say you write the equals method looks like below:

```java
public boolean equals(Cash other){
     ....
}
```   

Because the two equals methods argument does not match, java would understand it as different methods. It is called the method **overloading**. Therefore, your class looks like this:
   
```java
public class Cash {

    public boolean equals(Object other){
        ...
    }

    public boolean equals(Cash other){
        ...
    }

}
```

It works as expected for some cases like:
```java


Cash one_dollar=new Cash(1.0);
Cash another_dollar=new Cash(1.0);

assert one_dollar.equals(another_dollar);

```

But it does not work for some cases like:

```java

Cash one_dollar=new Cash(1.0);
Object another_dollar=new Cash(1.0);

assert one_dollar.equals(another_dollar);

```
In this case, another_dollar is declared as the "Object" and it is possible because all classes are subclasses of the "Object". Since the another_dollar is an Object, the former method would be called and could not run as expected.
