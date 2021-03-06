---
title: Object Oriented JavaScript
description: Pragim Technologies JavaScript Tutorial (Lessons 53-65)
---
<!-- markdownlint-disable MD022 MD024 MD032 -->
# JavaScript Tutorial
This [JavaScript Tutorial](https://www.youtube.com/playlist?list=PL6n9fhu94yhUA99nOsJkKXBqokT3MBK0b) series consists of 75 videos published by Pragim Technologies.

It was published from Oct 2014 thru Oct 2015 and covers JavaScript ES5 in the context of ASP.NET. While JavaScript and it's coding conventions have evolved since this series was released, many of the concepts are still relevant and applicable today.

The section of the series covered here, lessons 53-65, relates to using JavaScript in an object-oriented manner to replicate class-based inheritance. This is the style of JavaScript most commonly promoted by Microsoft for use in developing enterprise-based web application systems.

- [JavaScript YouTube playlist](https://www.youtube.com/playlist?list=PL6n9fhu94yhUA99nOsJkKXBqokT3MBK0b) - YouTube playlist of all 75 JavaScript Tutorial videos.
- [JavaScript Blog posts](http://csharp-video-tutorials.blogspot.com/2014/11/javascript-tutorial.html) - Text version of the material which includes notes, code samples, and slides.

## Pragim Technologies
Pragim Technologies publishes video tutorials on a broad range of Dot Net subjects including C#, SQL Server, ASP.NET, ASP.NET MVC, ASP.NET Core, ADO.NET, LINQ, Entity Framework, AngularJS, Angular, AngularCLI, JavaScript, jQuery, and much more.

- [Pragim Technologies on YouTube](https://www.youtube.com/channel/UCCTVrRB5KpIiK6V2GGVsR1Q) - This is the YouTube channel for Pragim Technologies.
- [Full list of video tutorials](https://www.youtube.com/user/kudvenkat/playlists) - A list of all YouTube playlists by Pragim Technologies.

---

## 53. JavaScript and object oriented programming

**JavaScript is object oriented programming language. The following are the 4 pillars of any object oriented programming language.** We will discuss examples of these in a later lesson.

1. Inheritance
1. Encapsulation
1. Abstraction
1. Polymorphism

In this lesson let's focus on **creating objects in JavaScript**. Objects in JavaScript can be broadly classified into 2 categories.

1. Standard built-in objects
1. Custom objects

**Standard built-in objects:** So far in this video series, we have already seen many of the JavaScript standard built-in objects. Examples include `string`, `array`, `RegExp`, `Date`, etc. In the example below we are creating Date object using the Date constructor function and then using it's getFullYear() method to get the year.

```js
var currentDate = new Date();
document.write(currentDate.getFullYear());
```

**Custom objects:** In C#, to create a custom object, we create a Custom class and then create an instance of a class. In JavaScript we don't have classes. Instead we use functions. **In JavaScript there are two ways to create a custom object**.

1. **Constructor function**
1. **Literal notation**

### Creating an object in JavaScript using constructor function

```html
<script type="text/javascript">
    // Constructor function
    function Employee(firstName, lastName) {
        this.firstName = firstName;
        this.lastName = lastName;

        this.getFullName = function () {
            return this.firstName + " " + this.lastName;
        }
    }

    var employee = new Employee("Pragim", "Tech");

    document.write("FirstName = " + employee.firstName + "<br/>");
    document.write("LastName = " + employee.lastName + "<br/>");
    document.write("FullName = " + employee.getFullName() + "<br/>");
</script>
```

**Live Sample:** [53-constructor-function.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/53-constructor-function.html)

### Creating an object in JavaScript using literal notation

```html
<script type="text/javascript">
    // Object literal notation
    var employee = {
        firstName: "Pragim",
        lastName: "Tech",

        getFullName: function () {
            return this.firstName + " " + this.lastName;
        }
    };

    document.write("FirstName = " + employee.firstName + "<br/>");
    document.write("LastName = " + employee.lastName + "<br/>");
    document.write("FullName = " + employee.getFullName() + "<br/>");
</script>
```

**Live Sample:** [53-literal-notation.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/53-literal-notation.html)

Both the examples above produce the same output

```text
FirstName = Pragim
LastName = Tech
FullName = Pragim Tech
```

What is the difference between creating an object using constructor function and literal notation.

1. In the constructor function the properties and their values separated using an equal-to sign(`=`) whereas in the literal version, they are separated using a colon(`:`)
1. In constructor function at the end of each property you can have a semi-colons(`;`) whereas in the literal version properties must be separated with a comma(`,`)
1. With literal notation you have already created an object, so to access `firstName` value you simply use `employee.firstName`. With the constructor function you have to first create an instance and then use the created instance and the property name separated by DOT as shown below.

    ```js
    var employee = new Employee("Pragim", "Tech");
    employee.firstName
    ```

## 54. Object literal vs object constructor

In this lesson we will discuss the main **difference between objects created using object literal and constructor function** and when to use one over the other. In Part 53 of JavaScript tutorial we discussed some of the syntactical differences.

### Creating an object using object literal notation

```js
var employee = {
    name: "John"
};

// Create a new variable and assign the employee object
var newEmployee = employee;

// Change the name property of the employee object using the new variable
newEmployee.name = "Mary";

// Retrieve the name property from the original employee object
// Notice that name is changed to Mary
document.write(employee.name);
```

**Live Sample:** [54-literal-notation.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/54-literal-notation.html)

```text
Output: Mary
```

**Objects created using object literals are singletons.** This means when a change is made to the object, it effects that object across the entire script.

### Creating an object using constructor function

```js
var Emp = function () {
    this.name = "John";
};

// Create an instance of employee
// employee.name will return John
var employee = new Emp();

// Create an other instance of employee
// newEmployee.name will return John
var newEmployee = new Emp();

// Change the name property of the newEmployee object
newEmployee.name = "Mary";

// Retrieve the name property from the original employee object
// Notice that name is not changed to Mary, it is still John
document.write(employee.name);
```

**Live Sample:** [54-constructor-function.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/54-constructor-function.html)

```text
Output : John
```

**Objects defined with the `new` keyword are created with the function acting as constructor function. Constructors function lets you have multiple instances of that object.** This means changes made to one instance, will not affect other instances.

If a function invocation is preceded with the **new** keyword, it is a constructor invocation.

> Note: It's good practice to name constructor functions with an upper-case first letter. (e.g. `Emp`)

### When to use one over the other
If you need **multiple instances** of the object **use constructor function** where as if you need just **one instance** of the object then **use literal notation**.

## 55. Global namespace pollution in JavaScript

In this lesson we will understand the **problem of global namespace pollution in JavaScript** with an example. When working with JavaScript on a big project, you might hear senior developers saying during the code review, this code pollutes the global scope.

In this lesson let's understand the problem of global namespace pollution. In our next lesson we will discuss how to write JavaScript in such a way that it does not pollute the global scope.

Let us say we have 2 software development teams (**TeamA** & **TeamB**) working on a large project for **Pragim Technologies**.

**TeamA** has created a `customer` constructor function with 2 parameters (`firstName` & `lastName`) and added it to **TeamA.js** file

```js
function customer(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.getFullName = function () {
        return this.firstName + " " + this.lastName;
    }
}
```

**TeamB** has also created a `customer` constructor function but with 3 parameters (`firstName`, `middleName` & `lastName`) and added it **TeamB.js** file.

```js
function customer(firstName, middleName, lastName) {
    this.firstName = firstName;
    this.middleName = middleName;
    this.lastName = lastName;

    this.getFullName = function () {
        return this.firstName + " " + this.middleName + " " + this.lastName;
    }
}
```

So at the moment we have **2 customer constructor functions**. One version has 2 parameters (`firstName` & `lastName`) and the other version has 3 parameters (`firstName`, `middleName` & `lastName`).

**HTML Page code:** In this HTML page we want to use the customer constructor function that has 2 parameters (firstName & lastName). Notice that in the header section we are first loading **TeamA.js** and then **TeamB.js**.

```html
<html>
    <head>
        <script type="text/javascript" src="TeamA.js" ></script>
        <script type="text/javascript" src="TeamB.js" ></script>
    </head>
    <body>
        <div id="resultDiv"></div>

        <script type="text/javascript">
            var customer1 = new customer('Tom', 'Grover');
            document.getElementById('resultDiv').innerHTML = customer1.getFullName();
        </script>
    </body>
</html>
```

When you view the page in the browser, we get the following output. We expected it to print to "Tom Grover".

```text
Tom Grover undefined
```

**This is because JavaScript does not support function overloading and as a result**, the `customer()` constructor function with 3 parameters simply overwrites the `customer()` constructor function with 2 parameters.

You may be wondering why didn't it happen the other way round. Why didn't `customer()` constructor function with 2 parameters overwrite the `customer()` constructor function with 3 parameters. That is because **TeamB.js** is loaded after **TeamA.js**. So the `customer()` constructor function in **TeamB.js** has overwritten the `customer()` constructor function in **TeamA.js**.

The reason, one of the `customer()` constructor function got overwritten is because we have already **polluted the global scope**. Let's understand what we mean by this.

1. `window` is the Global object in JavaScript.
1. When **TeamA.js** script file is loaded, the `customer()` function in **TeamA.js** file is added to the global namespace.
1. When **TeamB.js** script file is loaded, the `customer()` function in **TeamB.js** file is added to the global namespace. Since 2 functions with the same name cannot exist in the global namespace, the `customer()` function in **TeamB.js** overwrites the `customer()` function in **TeamA.js**. As a result we cannot use the `customer()` function in **TeamA.js** file.
1. In JavaScript if you declare a variable or a function second time, it simply overwrites the one you created earlier. JavaScript does not raise any errors like C# or Java if you redefine a variable or a function.

If we were to `console.log(this)` from the `customer()` function in TeamB.js as such.

```js
function customer(firstName, middleName, lastName) {
    this.firstName = firstName;
    this.middleName = middleName;
    this.lastName = lastName;

    this.getFullName = function () {
        return this.firstName + " " + this.middleName + " " + this.lastName;
    };

    console.log(this);
}
```

**Live Sample:** [55-collision.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/55-collision.html)

It would produce this.

```text
customer {firstName: "Tom", middleName: "Grover", lastName: undefined, getFullName: f}
```

### Summary
Polluting global namespace causes name collision. This is especially true in large projects where you may be using several JavaScript libraries (both internally developed as well as third party libraries). That's why it is very important not to add everything to the global namespace. If someone else use the same variable or function names it can lead to name collision.

In our next we will discuss, how to write JavaScript code in such a way that it does not pollute the global scope.

## 56. Namespaces in JavaScript

In this lesson, we will discuss **how to use namespaces to avoid polluting the global scope**. This is continuation to Part 55. Please watch Part 55 of JavaScript tutorial to understand the problem of global namespace pollution.

JavaScript lack namespaces. However we can use objects to create namespaces.

The following line says use the `PragimTech` object if it already exists, otherwise create an empty object.

```js
var PragimTech = PragimTech || {};
```

The following line adds a nested namespace. A nested namespace is a namespace inside another namespace. In JavaScript to define a nested namespace, you define an object inside another object.

```js
PragimTech.TeamA = PragimTech.TeamA || {};
```

Modify the script in **TeamA.js** file as shown below. In this example we are adding `customer()` function to `PragimTech.TeamA` namespace.

```js
var PragimTech = PragimTech || {};
PragimTech.TeamA = PragimTech.TeamA || {};

PragimTech.TeamA.customer = function (firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;

    this.getFullName = function () {
        return this.firstName + " " + this.lastName;
    };

    console.log(this);
    // {customer: f, firstName: "Tom", lastName: "Grover", getFullName: f}
};
```

PragimTech will be added to the global namespace. `window` is the alias for global namespace in JavaScript. You can now access `customer()` function as shown below.

```js
PragimTech.TeamA.customer("Tom", "Grover")
```

OR

```js
window.PragimTech.TeamA.customer("Tom", "Grover")
```

Modify the script in **TeamB.js** file as shown below. In this example we are adding `customer()` function to `PragimTech.TeamB` namespace.

```js
var PragimTech = PragimTech || {};
PragimTech.TeamB = PragimTech.TeamB || {};

PragimTech.TeamB.customer = function (firstName, middleName, lastName) {
    this.firstName = firstName;
    this.middleName = middleName;
    this.lastName = lastName;

    this.getFullName = function () {
        return this.firstName + " " + this.middleName + " " + this.lastName;
    };

    console.log(this);
    // {customer: f, firstName: "Tom", middleName: "T", lastName: "Grover", getFullName: f}
};
```

PragimTech will be added to the global namespace. You can now access `customer()` function as shown below.

```js
PragimTech.TeamB.customer("Tom", "T", "Grover")
```

OR

```js
window.PragimTech.TeamB.customer("Tom", "T", "Grover")
```

On any given HTML page you should be able to access both the versions of customer() function as shown below.

```html
<html>
    <head>
        <script type="text/javascript" src="TeamA.js" ></script>
        <script type="text/javascript" src="TeamB.js" ></script>
    </head>
    <body>
        <script type="text/javascript">
            var cust1 = new PragimTech.TeamA.customer("Tom", "Grover");
            var cust2 = new PragimTech.TeamB.customer("Tom", "T", "Grover");

            document.writeln(cust1.getFullName() + '<br>');
            document.writeln(cust2.getFullName());
        </script>
    </body>
</html>
```

**Live Sample:** [56-namespaces.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/56-namespaces.html)

## 57. Private members in JavaScript
In any object oriented programming language, **classes can have private and public members**. For example a class in C# can have private and public fields and functions.

An example is shown below.

```csharp
// CSharp
public class Employee
{
    // Private Field
    private string privateFullName;

    // Public Fields
    public string firstName;
    public string lastName;

    // Private Function
    private string privateGetFullName()
    {
        privateFullName = this.firstName + " " + this.lastName;
        return privateFullName;
    }

    // Public Function
    public string publicGetFullName()
    {
        return privateGetFullName();
    }
}
```

JavaScript is object oriented programming language, so objects in JavaScript can also have private and public fields and functions. An example is shown below.

```js
// JavaScript
function Employee(firstName, lastName) {
    // Private Field
    var privateFullName;

    // Public Fields
    this.firstName = firstName;
    this.lastName = lastName;

    // Private Function
    var privateGetFullName = function () {
        privateFullName = firstName + " " + lastName;
        return privateFullName;
    };

    // Privileged Function
    this.privilegedGetFullName = function () {
        return privateGetFullName();
    };

    // Public Function
    Employee.prototype.publicGetFullName = function () {
        return this.privilegedGetFullName();
    };
}
```

In the example above, we also have a privileged Function. **So, what is a Privileged Function?**

1. Privileged methods are created using `this` keyword and Public methods are created using `prototype` property of the constructor function.
1. Privileged method can access private variables and methods
1. Public methods can call Privileged methods but not Private methods.
1. Like Public methods, Privileged methods are also available outside the constructor function.

**Public fields and functions** are available both inside and outside of the `Employee()` constructor function.

**Private fields and functions** are available only inside the `Employee()` constructor function. Attempting to access private fields and properties outside of the constructor function will result in undefined error.

```js
var employee = new Employee("Tom", "Grover");

employee.publicGetFullName();       // Calling public function - "Tom Grover"
employee.privilegedGetFullName();   // Calling Privileged function - "Tom Grover"
employee.privateGetFullName();      // Calling private method - Uncaught TypeError
employee.privateFullName;           // Calling private field - undefined error
```

**Live Sample:** [57-member-calls.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/57-member-calls.html)

**Can we modify a private field outside of the constructor function?**
Straight answer, no you can't.

In the example below, when we call the private field `employee.privateFullName`, it results in `undefined` error. On the next line we are adding a new public field with same name as the private field to the employee object. Is this going to change the private field (privateFullName). The answer is NO. You cannot access or modify private fields outside of the object. In this example, you are just adding new public field (employee.privateFullName) to the employee object.

```js
var employee = new Employee("Tom", "Grover");
employee.privateFullName            // Calling private field - undefined error

employee.privateFullName = "ABC";   // Add a field with same name as private field
employee.publicGetFullName();       // "Tom Grover"
employee.privateFullName;           // "ABC"
```

### Summary

- **Private fields** - Declared using the `var` keyword inside the object, and can only be accessed by private functions and privileged methods.
- **Public fields** - Declared using `this` keyword and are available outside the object.
- **Private functions** - Declared inside the object using one of the two ways shown below. ***Private functions can only be called by privileged methods or other private functions.***

    ```js
    var privateGetFullName = function () {
        privateFullName = firstName + " " + lastName;
        return privateFullName;
    }

    // OR

    function privateGetFullName() {
        privateFullName = firstName + " " + lastName;
        return privateFullName;
    }
    ```

- **Privileged methods** - Declared using `this` keyword and are available both within and outside the object. ***Privileged methods can access private fields and private methods.***

    ```js
    this.privilegedGetFullName = function () {
        return privateGetFullName();
    }
    ```

- **Public methods** - Defined by using the object's prototype property and are available both within and outside the object. ***Public methods can call privileged methods but they cannot access private fields or call private methods.***

    ```js
    Employee.prototype.publicGetFullName = function () {
        return this.privilegedGetFullName();
    }
    ```

## 58. Properties in JavaScript
In an object oriented programming language, classes can have properties. For example a class in C# can have the following types of properties.

1. Read / Write properties
1. Read only properties
1. Write only properties

An example of a C# `Employee` class is shown below. `name` is read-only property and `age` is read/write property.

```csharp
// CSharp
public class Employee
{
    string _name;
    int _age;

    public Employee(string name, int age) {
        _name = name;
        _age = age;
    }

    // Read/Write property
    public int age {
        get { return _age; }
        set { _age = value; }
    }

    // ReadOnly property
    public string name {
        get { return _name; }
    }
}
```

Since JavaScript is also an object oriented programming language, objects in JavaScript can also have properties.

**Why do we need properties when we have public fields**
Encapsulation is one of the pillars of object oriented programming language. Properties provide encapsulation. If you use public fields you cannot control on what is assigned and returned from that public field.

In the example below we have an employee object with age public field. There is nothing stopping us from setting the age value of the employee object to 1000. Using properties you can control on what values can be assigned. You can also use properties to create just read-only or write-only properties.

```js
function Employee(age) {
    this.age = age;
}

var employee = new Employee(50);
// Nothing stops you from assigning a value of 1000 to age field
employee.age = 1000;
```

An example is shown below. In the example **name is read-only property** and **age is read/write property**.

```js
function Employee(name, age) {
    var _name = name;
    var _age = age;

    Object.defineProperty(this, 'age', {
        get: function () {
            return _age;
        },
        set: function (value) {
            if (value > 100 || value < 1) {
                alert("Invalid age");
            } else {
                _age = value;
            }
        }
    });

    Object.defineProperty(this, "name", {
        get: function () {
            return _name;
        }
    });
}

var employee = new Employee("Tom", 55);

employee.name = "Tommy";    // value of name property will not change (read-only)
employee.age = 195;         // Will alert an error - Invalid age

document.write(employee.name + " " + employee.age); // "Tom 55"
```

**Live Sample:** [58-properties.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/58-properties.html)

## 59. Static Members in JavaScript
In an object oriented programming language, classes can have **static members**, that is **static methods** and **static fields**. For example a class in C# is shown below. In this example PI is a static field and _radius is an instance field.

```csharp
public class Circle
{
    // Static field
    static float PI = 3.141F;

    // Instance field
    public int Radius;

    public Circle(int radius)
    {
        this.Radius = radius;
    }

    public float CalculateArea()
    {
        return Circle.PI * this.Radius * this.Radius;
    }
}
```

What is the difference between **static member** and **instance member** and when to use one over the other?

An instance member belong to a specific instance. So if I create 3 instances (objects) there will be 3 copies of instance fields in memory where as there will ever be only one copy of a static field no matter how many instances we create.

In the above example, radius is specific to the circle instance you are creating but the PI value need to be shared by all the circle objects. So, if you want a member to be shared by all instances then make it a static member.

Since JavaScript is also an object oriented programming language, objects in JavaScript can also have static and instance fields and methods. Here is an example. In this example PI is a static field and _radius is an instance field.

```js
function Circle(radius) {
    // Instance field
    this.Radius = radius;

    // Static field
    Circle.PI = 3.141;

    this.CalculateArea = function() {
        return Circle.PI * this.Radius * this.Radius;
    };
}

var circleObject = new Circle(10);
document.write('Area = ' + circleObject.CalculateArea());
```

**Live Sample:** [59-static-field.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/59-static-field.html)

### Points to remember

1. Define a static member using the name of the constructor function.
2. To invoke a static member use the name of the constructor function.
3. To invoke an instance member use the instance of the constructor function.

### Static methods in JavaScript
In the following example `ShowCount()` is a static method. Notice that, just like a static variable, static method is also defined using the name of the constructor function. To keep track of the number of Shape objects created we are using `Shape.Count` static field.

`Shape.ShowCount()` method returns the count of shapes when called.

```js
function Shape(shapeName) {
    // Instance field
    this.ShapeName = shapeName;

    // Static field
    Shape.Count = ++Shape.Count || 1;

    // Static method
    Shape.ShowCount = function() {
        return Shape.Count;
    };
}

var shape1 = new Shape('Circle');
var shape2 = new Shape('Rectangle');
var shape3 = new Shape('Triangle');

document.write('Shape.Count = ' + Shape.ShowCount());
```

**Live Sample:** [59-static-method.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/59-static-method.html)

Since we have created 3 shapes, the output will be 3.

## 60. Prototype in JavaScript
In this lesson we will discuss the **Prototype object** in JavaScript. Let us understand it's use with an example.

The following `Employee` constructor function constructs an Employee object.

```js
function Employee(name) {
    this.name = name;
}
```

There are several ways to add a function to the Employee object. One way is as shown below. This works but the problem with this approach is that, **if you create 100 employee objects there will be 100 copies of the `getName()` function**.

```js
function Employee(name) {
    this.name = name;

    // privileged method
    this.getName = function () {
        return this.name;
    }
} 

var e1 = new Employee("Mark");
var e2 = new Employee("Sara"); 

document.write("e1.name = " + e1.getName() + "<br/>");
document.write("e2.name = " + e2.getName() + "<br/>"); 
```

```text
Output:
e1.name = Mark
e2.name = Sara
```

**Live Sample:** [60-privileged-method.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/60-privileged-method.html)

We don't want to be creating copies of functions, instead **we want all the objects to share the same function code**. This can be achieved using JavaScript prototype object.

In this example, the `getName()` function is added just to the `e1` object, and not to `e2` object. So `e2.getName()` would throw an `undefined` error.

```js
function Employee(name) {
    this.name = name;
}

var e1 = new Employee("Mark");

// instance method
e1.getName = function () {
    return this.name;
}

var e2 = new Employee("Sara");

document.write("e1.name = " + e1.getName() + "<br/>");
document.write("e2.name = " + e2.getName() + "<br/>");
```

**Live Sample:** [60-instance-method.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/60-instance-method.html)

In the following example `getName()` function is added to the Employee object using the name of the constructor function. **This would also result in `undefined` error.**

```js
function Employee(name) {
    this.name = name;
}

// static method
Employee.getName = function () {
    return this.name;
}

var e1 = new Employee("Mark");
var e2 = new Employee("Sara");

document.write("e1.name = " + e1.getName() + "<br/>");
document.write("e2.name = " + e2.getName() + "<br/>");
```

**Live Sample:** [60-static-method.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/60-static-method.html)

### Using the prototype object to add functions
The following are the advantages of using the prototype object to add functions.

1. No matter how many objects you create, functions are loaded only once into memory
2. Allows you to override functions if required.

```js
function Employee(name) {
    this.name = name;
}

Employee.prototype.getName = function () {
    return this.name;
}

var e1 = new Employee("Mark");
var e2 = new Employee("Sara");

document.write("e1.name = " + e1.getName() + "<br/>");
document.write("e2.name = " + e2.getName() + "<br/>");
```

```text
Output:
e1.name = Mark
e2.name = Sara
```

**Live Sample:** [60-prototype-method.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/60-prototype-method.html)

## 61. Overriding JavaScript Functions
In this lesson we will discuss **how to override a JavaScript function**. This is continuation to Part 60. Please review Part 60 from JavaScript tutorial before proceeding.

In Part 60, we discussed that one of the advantages of using prototype property to add functions is that it enables us to **override an existing function** if required. Let us continue with the same example we worked with in Part 60.

```js
function Employee(name) {
    this.name = name;
}

Employee.prototype.getName = function () {
    return this.name;
}

var e1 = new Employee("Mark");
var e2 = new Employee("Sara");

document.write("e1.name = " + e1.getName() + "<br/>");
document.write("e2.name = " + e2.getName() + "<br/>");
```

```text
Output :
e1.name = Mark
e2.name = Sara
```

Let us say for some reason we want to override `getName()` function of Employee object. Notice that in `GetEmployeeDetails()` function we have overridden `getName()` function of the Employee object. The overridden version converts the name of the employee to UPPERCASE.

```html
<script type="text/javascript">
    GetEmployeeDetails();

    function GetEmployeeDetails() {
        Employee.prototype.getName = function () {
            return this.name.toUpperCase();
        }

        var e1 = new Employee("Mark");
        var e2 = new Employee("Sara");

        document.write("e1.name = " + e1.getName() + "<br/>");
        document.write("e2.name = " + e2.getName() + "<br/>");
    }

    function Employee(name) {
        this.name = name;
    }

    Employee.prototype.getName = function () {
        return this.name;
    }
</script>
```

```text
Output :
e1.name = MARK
e2.name = SARA
```

**Live Sample:** [61-override-function1.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/61-override-function1.html)

In this example, all the JavaScript is in the same file. i.e

1. The JavaScript that creates Employee constructor function and `getName()` function
2. The script that overrides `getName()` function

The JavaScript that creates Employee constructor function and `getName()` function could even be present in a separate JavaScript file.

1. Lets add a new JavaScript file and name it **EmployeeScript.js**.
2. Copy and paste the following JavaScript code in EmployeeScript.js file.

    ```js
    function Employee(name) {
        this.name = name;
    }

    Employee.prototype.getName = function () {
        return this.name;
    };
    ```

3. Modify the code on the HTML page as shown below.

    ```html
    <html>
        <head></head>
        <body>
            <script src="employee.js"></script>
            <script>
                GetEmployeeDetails();

                function GetEmployeeDetails() {
                    Employee.prototype.getName = function () {
                        return this.name.toUpperCase();
                    };

                    var e1 = new Employee("Mark");
                    var e2 = new Employee("Sara");

                    document.write("e1.name = " + e1.getName() + "<br/>");
                    document.write("e2.name = " + e2.getName() + "<br/>");
                }
            </script>
        </body>
    </html>
    ```

**Live Sample:** [61-override-function2.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/61-override-function2.html)

Run the page and the output should be exactly the same as the previous example.

JavaScript built-in methods can also be overridden. The following example overrides the built-in JavaScript `alert()` function.

```html
<script type="text/javascript">
    // Overriding JavaScript alert function to write to the page
    // instead of displaying the alert dialog box
    var alert = function (msg) {
        document.write(msg);
    };

    // The following calls will invoke the overridden alert() method   
    alert("Hello");
    window.alert(" JavaScript");
</script>
```

```text
Output : Hello JavaScript
```

**Live Sample:** [61-override-alert.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/61-override-alert.html)

## 62. Inheritance in JavaScript
In this lesson we will discuss **Inheritance in JavaScript** with an example.

Object oriented programming languages support inheritance. Since JavaScript is also an object oriented programming language, it supports inheritance.

In object-oriented programming, languages like C# and Java implement inheritance when a *class* inherits from another *class*.

In JavaScript, we don't have a traditional class inheritance model. Instead, **JavaScript inheritance is prototype-based**. This means that to implement inheritance in JavaScript, an *object* inherits from another *object*. Let us understand this with an example.

```html
<script type="text/javascript">
    // Employee will be the base object (Similar to base class in c#)
    var Employee = function (name) {
        this.name = name;
    };

    // getName() function is added to the base object (Employee)
    Employee.prototype.getName = function () {
        return this.name;
    };

    // PermanentEmployee will be the derived object
    var PermanentEmployee = function (annualSalary) {
        this.annualSalary = annualSalary;
    };

    // Use prototype to associate Employee as the base object for PermanentEmployee
    PermanentEmployee.prototype = new Employee("Mark");

    var pe = new PermanentEmployee(50000);
    // Derived object (permanentEmployee) can see the
    // base object (Employee) getName() method
    document.write(pe.getName());

    alert(pe instanceof Employee);          // Returns true
    alert(pe instanceof PermanentEmployee); // Returns true
</script>
```

**Live Sample:** [62-derived-object.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/62-derived-object.html)

Notice that the derived object (PermanentEmployee) can see the base object (Employee) `getName()` method. When `getName()` method is called, JavaScript first tries to find this method in the derived object. If it can't find the method there, it goes up the chain to the parent object and finds it there.

If you add a new method to the parent object, it becomes available in the derived object.

```html
<script type="text/javascript">
    var Employee = function (name) {
        this.name = name;
    };

    Employee.prototype.getName = function () {
        return this.name;
    };

    // Adding getNameLength() method to the parent object
    // which becomes available in the derived object
    Employee.prototype.getNameLength = function () {
        return this.name.length + " characters";
    };

    // PermanentEmployee will be the derived object
    var PermanentEmployee = function (annualSalary) {
        this.annualSalary = annualSalary;
    }

    PermanentEmployee.prototype = new Employee("Mark");

    var pe = new PermanentEmployee(50000);
    // Call getNameLength() method added to the parent object
    document.write(pe.getNameLength()); // Output: 4 characters
</script>
```

**Live Sample:** [62-derived-object2.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/62-derived-object2.html)

Use `hasOwnProperty()` method to determine if a property is defined on the actual object or it's prototype. Here is an example.

```html
<script type="text/javascript">
    var Employee = function (name) {
        this.name = name;
    };

    var PermanentEmployee = function (annualSalary) {
        this.annualSalary = annualSalary;
    };

    var employee = new Employee("Mark");

    PermanentEmployee.prototype = employee;

    var pe = new PermanentEmployee(50000);

    document.write("Employee.name: " +
                     employee.hasOwnProperty('name') + "<br/>");
    document.write("Employee.annualSalary: " +
                     employee.hasOwnProperty('annualSalary') + "<br/><br/>");

    document.write("PermanentEmployee.name: " +
                     pe.hasOwnProperty('name') + "<br/>");
    document.write("PermanentEmployee.annualSalary: " +
                     pe.hasOwnProperty('annualSalary') + "<br/>");
</script>
```

**Output**

```text
Employee.name: true
Employee.annualSalary: false

PermanentEmployee.name: false
PermanentEmployee.annualSalary: true
```

**Live Sample:** [62-hasOwn.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/62-hasOwn.html)

## 63. Abstract classes in JavaScript
In this lesson we will discuss, **how to implement the concept of abstract classes in JavaScript**.

Object oriented programming languages like C# and Java, support **abstract classes**. Abstract classes are incomplete in and of themselves. So, trying to create an instance of an abstract class raises a compiler error. Abstract classes can only be used as base classes.

Let us first look at a simple C# example.

1. Open visual studio and create a new empty asp.net web application project.

2. Add a web form to the project. Name it WebForm1.aspx. Copy and past the following code in the code-behind file.

```csharp
using System;
namespace Demo
{
    public partial class WebForm1 : System.Web.UI.Page
    {
        protected void Page_Load(object sender, EventArgs e)
        {
            // Error: Cannot create an instance of an abstract class
            // Shape s = new Shape();

            Circle circle = new Circle();
            circle.shapeName = "Circle";
            Response.Write(circle.draw() + "<br/><br/>");

            Response.Write(circle is Shape + "<br/>");  // Returns true
            Response.Write(circle is Circle + "<br/>"); // Returns true
        }
    }

    public abstract class Shape
    {
        public string shapeName = "None";
        public string draw()
        {
            return "Drawing " + this.shapeName;
        }
    }

    public class Circle : Shape
    {
        // Code specific to Circle class
    }
}
```

Since JavaScript is also an object oriented programming language, it also supports the concept of abstract classes. Here is an example.

Add a new HTML page to the project. Name it HTMLPage1.htm. Copy and paste the following code in HTMLPage1.htm. 

```html
<script type="text/javascript">
    // Create a Shape object which is abstract
    var Shape = function () {
        this.shapeName = "None";
        throw new Error("Cannot create an instance of abstract class");
    };

    // Error : Cannot create an instance of abstract class
    // var shape = new Shape();

    // Add draw function to the Shape prototype
    // Objects derived from Shape should be able to call draw() method
    Shape.prototype.draw = function () {
        return "Drawing " + this.shapeName;
    };

    // Create a Circle object
    var Circle = function (shapeName) {
        this.shapeName = shapeName;
    };

    // Make shape the parent for Circle
    // Object.create() allows to create an object without using constructor
    Circle.prototype = Object.create(Shape.prototype);

    var circle = new Circle("Circle");
    // Since Circle inherits from abstract Shape object, it can call draw() method
    document.write(circle.draw());

    alert(circle instanceof Circle); // Returns true
    alert(circle instanceof Shape);  // Returns true
</script>
```

**Live Sample:** [63-abstract-class.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/63-abstract-class.html)

## 64. Object reflection in JavaScript
In this lesson we will discuss, **object reflection in JavaScript** with an example.

Object oriented programming languages like C# and Java, support reflection. **Reflection allows us to inspect meta data of assemblies, modules and types.** Since JavaScript is also an object oriented programming language, it also supports the concept of reflection.

Let's understand object reflection in JavaScript with an example.

The `Employee` object in the following example has **4 public properties**.

1. `firstName`
2. `lastName`
3. `email`
4. `gender`

It also has **3 public functions**.

1. `getFullName()`
2. `getEmail()`
3. `getGender()`

```js
var Employee = function (firstName, lastName, gender, email) {
    this.firstName = firstName;
    this.lastName = lastName;
    this.gender = gender;
    this.email = email;
}

Employee.prototype.getFullName = function () {
    return this.firstName + " " + this.lastName;
}

Employee.prototype.getEmail = function () {
    return this.email;
}

Employee.prototype.getGender = function () {
    return this.gender;
}
```

### Sample 1
The following code creates an object instance and then retrieves all the **public properties and methods of the `employee1` object**.

**Code 1**

```js
var employee1 = new Employee("Mark", "Matt", "Male", "a@a.com");

for (var property in employee1) {
    document.write(property + "<br/>");
}
```

**Output 1**

```text
firstName
lastName
gender
email
getFullName
getEmail
getGender
```

**Live Sample:** [64-object-reflection1.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/64-object-reflection1.html)

### Sample 2

The following code retrieves all the **public properties & functions of the Employee object along with their values**.
 
**Code 2**

```js
for (var property in employee) {
    document.write(property + " : " + employee[property] + "<br/>");
}
```

**Output 2**

```text
firstName: Mark
lastName: Matt
gender: Male
email: a@a.com
getFullName: function () { return this.firstName + " " + this.lastName; }
getEmail: function () { return this.email; }
getGender: function () { return this.gender; }
```

**Live Sample:** [64-object-reflection2.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/64-object-reflection2.html)

### Sample 3

The following code retrieves only the public properties of the Employee object.

**Code 3**

```js
for (var property in employee) {
    if (typeof employee[property] != "function") {
        document.write(property + " : " + employee[property] + "<br/>");
    }
}
```

**Output 3**

```js
firstName : Mark
lastName : Matt
gender : Male
email : a@a.com
```

**Live Sample:** [64-object-reflection3.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/64-object-reflection3.html)

### Sample 4

The following code retrieves only the public functions of the Employee object. 

**Code 4**

```js
for (var property in employee) {
    if (typeof employee[property] == "function") {
        document.write(property + " : " + employee[property] + "<br/>");
    }
}
```

**Output 4**

```text
getFullName : function () { return this.firstName + " " + this.lastName; }
getEmail : function () { return this.email; }
getGender : function () { return this.gender; }
```

**Live Sample:** [64-object-reflection4.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/64-object-reflection4.html)

### Sample 5

When 2 objects are related thru inheritance, the child object will have access to parent object methods and properties. In this example, `PermanentEmployee` is a child of `Employee`. The following code shows all the properties and methods of the `PermanentEmployee` object including those it inherited from the Employee object.

**Code 5**

```js
var employee = new Employee("Mark", "Matt", "Male", "a@a.com"); 

var PermanentEmployee = function (annualSalry) {
    this.annualSalary = annualSalry;
};

PermanentEmployee.prototype = employee;

var pe = new PermanentEmployee(50000);

for (var property in pe) {
    document.write(property + " : " + pe[property] + "<br/>");
}
```

**Output 5**

```text
annualSalary : 50000
firstName : Mark
lastName : Matt
gender : Male
email : a@a.com
getFullName : function () { return this.firstName + " " + this.lastName; }
getEmail : function () { return this.email; }
getGender : function () { return this.gender; }
```

**Live Sample:** [64-object-reflection5.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/64-object-reflection5.html)

### Sample 6

In this example, we are using `hasOwnProperty()` method to determine if a property is defined on the actual object or it's prototype. This method returns `true` if the property is defined by the object itself, otherwise `false`.

The following code retrieves only the public members that are defined in the `PermanentEmployee` object. The members inherited from the base `Employee` object are excluded.

**Code 6**

```js
for (var property in pe) {
    if (pe.hasOwnProperty(property)) {
        document.write(property + " : " + pe[property] + "<br/>");
    }
}
```

**Output 6**

```text
annualSalary : 50000
```

**Live Sample:** [64-object-reflection6.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/64-object-reflection6.html)

### Sample 7

The following code retrieves only the public members inherited from the parent object. Public members defined in PermanentEmployee object are excluded.

**Code 7**

```js
for (var property in pe) {
    if (!pe.hasOwnProperty(property)) {
        document.write(property + " : " + pe[property] + "<br/>");
    }
}
```

**Output 7**

```text
firstName : Mark
lastName : Matt
gender : Male
email : a@a.com
getFullName : function () { return this.firstName + " " + this.lastName; }
getEmail : function () { return this.email; }
getGender : function () { return this.gender; }
```

**Live Sample:** [64-object-reflection7.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/64-object-reflection7.html)

## 65. Polymorphism in JavaScript
In this lesson we will discuss, **how to implement polymorphism in JavaScript** with an example.

Object oriented programming languages like C# and Java, support polymorphism. Here is a C# example.

```csharp
public partial class WebForm1 : System.Web.UI.Page
{
    protected void Page_Load(object sender, EventArgs e)
    {
        Shape[] shapes = new Shape[]
        {
            new Shape(), new Circle(), new Square(), new Triangle()
        };

        foreach (Shape shape in shapes)
        {
            Response.Write(shape.draw() + "<br/>");
        }
    }
}

public class Shape
{
    public virtual string draw()
    {
        return "I am a generic shape";
    }
}

public class Circle : Shape
{
    public override string draw()
    {
        return "I am a circle";
    }
}

public class Square : Shape
{
    public override string draw()
    {
        return "I am a square";
    }
}

public class Triangle : Shape
{ }
```

**Output**

```text
I am a generic shape
I am a circle
I am a square
I am a generic shape 
```

Since JavaScript is also an object oriented programming language, it also supports the concept of polymorphism. Here is an example.

```html
<script type="text/javascript">
    // Shape object is be the base object
    var Shape = function () { };

    // Add draw function to the Shape prototype
    // Objects derived from Shape will be able to override the draw() method
    Shape.prototype.draw = function () {
        return "I am a generic shape";
    };

    // Create a Circle object
    var Circle = function () { }

    // Make shape the parent for Circle
    Circle.prototype = Object.create(Shape.prototype);

    // Circle object overrides draw() method
    Circle.prototype.draw = function () {
        return "I am a circle";
    };

    var Square = function () { };
    Square.prototype = Object.create(Shape.prototype);
    Square.prototype.draw = function () {
        return "I am a square";
    };

    var Triangle = function () { };
    Triangle.prototype = Object.create(Shape.prototype);

    var shapes = [new Shape(), new Circle(), new Square(), new Triangle()];

    shapes.forEach(function (shape) {
        document.write(shape.draw() + "<br/>");
    });
</script>
```

**Live Sample:** [65-polymorphism.html](https://james-priest.github.io/code-exercises/javascript_exercises/javascript-csharp/public/65-polymorphism.html)

**Output**

```text
I am a generic shape
I am a circle
I am a square
I am a generic shape
```
