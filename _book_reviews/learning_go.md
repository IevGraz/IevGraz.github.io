---
title: 'Learning Go'
subtitle: An Idiomatic Approach to Real-World Go Programming
author:  Jon Bodner
rating: 5
date: 2024-11-03
goodreads_link: https://www.goodreads.com/book/show/55841848-learning-go
---

**Why I read this book:** I’ve been coding with Ruby for the past 5 years in my current job. Some time ago Go was chosen as the second official programming language in the company. Time finally came for me to do some coding with Go. But I’ve heard many Go developers complain about people new to the language writing some ugly and complex code. I wanted to avoid making the same mistakes. In the foreword of this book it literally says “This book is for a reader that wants to write Go code that looks like Go code”. So it seemed like exactly the book I needed.


### Summary

I want to share some of the interesting things I’ve found in the book. I present them here not in the order they were provided in the book, but rather  grouped into categories that made sense for me.


#### The philosophy of Go

Go is hard to categorize:
* It isn’t a strictly procedural language
* It isn’t a functional language
* It isn’t a particularly object oriented language (it lacks method overriding, inheritance)

If you try to shoehorn Go into one of the above categories, the result is non idiomatic Go code. 

Two **goals of Go** with some examples of how that affects the way Go is written or encouraged to be used:
* <span style="text-decoration:underline;">Fast compiler:</span> The garbage collector used by Go runtime favors low latency (finishing the scan as quickly as possible). If your Go program creates lots of garbage, Garbage Collector won’t be able to find it all during a cycle, slowing down the collector and increasing memory usage. This is why Go encourages us to use the pointers sparingly. 
* <span style="text-decoration:underline;">Easy to understand source code:</span> Go uses a returned error instead of a thrown exception, because it favors clear code, even if it takes more lines. Making errors into returned values forces developers to either check and handle errors or make it explicit that they are ignoring errors by using an underscore (_) as variable name


#### Some interesting features of the language

**How strongly typed it is**: 
* Different-sized integers need to be converted to the same type to interact.
* Functions in Go are also values. The type of a function is built out of the keyword func and the types of parameters and return values.

**Comma ok idiom** - it is common for methods in Go to return 2 values: the actual return value + a boolean that tells if the value was really present. This is used with maps, type assertions, channels. 

```Go
m := map[string]int {
    "hello": 5,
    "goodbye": 10
}

v, ok = m["hello"]
```

**Go doesn’t have classes**, because it doesn’t have inheritance. You can declare a type based on another type. This is not inheritance: you can’t use the two types interchangeably and the methods defined on one type are not present on the other. This is just for the sake of documentation - expressing that you have same underlying data, but different sets of operations

**Closures** - functions declared inside of functions that are able to access and modify variables declared in outer functions. Functions usually return closures so that the calling functions can call them via *defer* keyword and trigger some required cleanup this way. *defer* keyword delays function invocation until the surrounding function exits. You can defer multiple closures, they run in last in first out (LIFO) order - last defer registered runs first. 

Defining a closure within a function:

```Go
func getFile(name string) (*os.File, func(), error) {
    file, err := os.Open(name)
    if err != nil {
        return nil, nil, err
    }

    return file, func() {
        file.Close()
    }, nil
}
```

Defering of the closure:

```Go
f, closer, err = getFile("MyFile")
if err != nil {
    log.Fatal(err)
}

defer closer()
```

**Call by value** - when you supply a variable for a parameter to a function, Go always makes a copy of the value of the variable. If you need to modify the parameter within a function - use pointers. If a pointer is passed to a function, the function gets a copy of the pointer. This still points to the original data.

**Embedding**. Go doesn’t have inheritance, but it encourages code reuse via built-in support for composition and promotion. You can embed a field into a struct. Any fields or methods declared on the embedded field are promoted to the containing struct and can be invoked directly on it. I especially liked the following **warning**: many developers try to understand embedding by treating it as inheritance. *That way lies tears*. You cannot assign the new type to a variable that requires the embedded type. 

```Go
type Item struct {
    baseItem // embedded field
    str string
}
```

**Interfaces**  in Go are implicit: a concrete type does not declare that it implements an interface. If the type has all the methods defined on the interface, the concrete type implements the interface. 

Experienced Go developers say “***Accept interfaces, return structs***”.

**Struct tags** - strings that are written after the fields in a struct. Composed of one or more tag/ value pairs, written as *tagName*: “*tagValue*” and separated by spaces. They cannot extend past a single line. Because struct tags are just strings, the compiler cannot validate that they are formatted correctly, but `go vet` does. They are used for specifying rules for processing JSON, reading values from environment variables etc. 

```Go
type Item struct {
    ID string `json:"id"`
    Name string `json:"name"`
}
```

**Concurrency in Go**. According to the philosophy of Go, using things like mutexes to handle concurrency in a program obscures the flow of data. Go uses Goroutines (lightweight processes managed by Go runtime) and Channels (special data types) to handle concurrency. When a value is passed from goroutine to goroutine over a series of channels, the data flow is clear. However there seem to be a lot going on to support the Goroutine approach - done channel pattern, wait groups, buffered vs unbuffered channels. Those seemed quite hard to grasp.

Also - Go does have support for mutexes, but they are not reentrant - if a go routine tries to acquire the  same lock twice, it deadlocks waiting for itself to release the lock

**The context**. Idiomatic Go encourages explicit data passing via function parameters. The same is true for the context. It is just another parameter to your function. By convention, the context is explicitly passed through your program as the first parameter. The usual name for the context parameter is ***ctx***. What kind of values should be kept in the context, instead of being passed as separate parameters? The information that is meant for management of your application (e.g. tracking GUID)  instead of being part of the business state. Copy values from context to explicit parameters when they are needed for processing business logic.

**Go tests** are placed in the same directory and the same package as the production code. This way they are able to access and test unexported functions and variables. When writing tests it is good to keep in mind the [test tables pattern](https://github.com/uber-go/guide/blob/master/style.md#test-tables).


#### Main differences from Ruby

Some things that I was really used to in Ruby that are different in Go:



* Single quotes and double quotes are not interchangeable. Double quotes seem to be used in most cases. In Ruby single quotes are the default.
* You cannot treat another Go type as a boolean - non-zero numbers or non-empty strings cannot be considered “truthy”.
* It isn’t idiomatic to use **this** or **self** when naming a method receiver. 
* Using Camel case instead of Snake case for naming variables.
* Favoring short variable names: the smaller the scope for a variable, the shorter the name. Single letter variable names are common. If you find it hard to keep track of your short-named variables, it is likely that your block of code is doing too much. In Ruby, I’m used to making variable and method names as explicit and self explanatory as possible.


#### Gotchas

These are all related with Slices - Go data type that represents a sequence of values. All this weird behaviour comes from the fact that slices are implemented as pointers.

* **Appending to a slice of slice**. When you take a slice from a slice, you are not making a copy of the data - you now have 2 variables that are sharing memory. When append is used on a slice of slice, it creates very odd scenarios with multiple slices overriding each other's data.
* **Indexing and slicing of strings**. Go uses a sequence of bytes to represent a string. You can use slicing and indexing on strings, but you can get unexpected results with characters that take up more than one byte. You should instead use the  `for-range` loop to iterate over strings.
* **Passing a slice to a function** has a complicated behavior: any modifications to the contents is reflected in the original variable, but using append to change the length isn’t reflected. 

### What I liked

* The book is exactly what I was looking for - introduction to the programming language with explanations of what code is Go-like and why. 
* The explanations were really good. If I couldn’t grasp what was being said from the text alone, the code snippets usually helped me to figure it out. 
* It was the most interesting to read about all the under the hood stuff with pointers e.g. why passing a slice to a function behaves oddly: “*Slice is implemented as a struct with 3 fields: length, capacity and a pointer to a block of memory. When a slice is passed to a function, a copy is made of those 3 fields. Changing the value of the slice changes the memory the pointer points to. Changing the capacity means that the pointer is now pointing to a new, bigger, block of memory. Changing the length of the slice within the available capacity still does not change the length value of the original slice - it is not able to see the change, even if it happened in the same memory location.*”


### What I disliked

These are not necessarily dislikes, but some limitations of the book (or maybe me in some cases):



* There were places that I found hard to grasp. Mostly concurrency and reflections. But that might have required a bit more effort than I was willing to put in.
* My focus and effort dwindled towards the last chapters. Which is unfortunate as they were more complex and most likely more useful. 
* Only reading about the programming language is not enough to really learn it. I’ve heard that the second edition of the book has some exercises at the end of each chapter.  That could be a pretty big improvement. I’m hoping to cover this gap in my knowledge by attending a few workshops. 
* Since I read the first edition of the book, it only mentioned generics at the very last chapter as a newly added thing. Through the book there were quite a few places that emphasized something being done in a particular way because Go doesn’t have generics. 