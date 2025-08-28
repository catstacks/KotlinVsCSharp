
# Syntax and Features
NB: Some definitions and examples have been quoted directly or paraphrased from the [official Kotlin docs](https://kotlinlang.org/docs/home.html).

## Filtering with predicates vs LINQ

A **predicate** is a lambda function that takes a collection element and returns a boolean value. If a value of `true` is returned, it means the collection element and predicate were matched.

In this example, the `::` syntax lets you pass a function without invoking it. The `::` syntax can also be used for concise property referencing and constructor referencing.

### Kotlin
```kotlin
// General structure
list.filter { predicate }

// Standard filter example 
val numbers = listOf(1, 2, 3, 4, 5)
val evens = numbers.filter { it % 2 == 0 }
println(evens)  // output: [2, 4] 

// Named predicate example
fun isEven(n: Int) = n % 2 == 0
val evens = numbers.filter(::isEven)
```
### C#
```csharp
// General structure
list.Where(predicate)

// Standard filter example 
var numbers = new List<int> { 1, 2, 3, 4, 5 };
var evens = numbers.Where(n => n % 2 == 0).ToList();
Console.WriteLine(string.Join(", ", evens));  // output: 2, 4

// Named method example
bool IsEven(int n) => n % 2 == 0;
var evens = numbers.Where(IsEven).ToList(); // pass function reference instead of calling it
```
## Coroutines vs Async/Await  

A coroutine is defined as *an instance of a suspendable computation* and can be thought of as a *lightweight thread*.  
Whilst similar to threads with regards to concurrency, coroutines are not bound to any particular thread and can **suspend** their execution in one thread and resume in another one.

### Kotlin
```kotlin
import kotlinx.coroutines.*

fun main() = runBlocking {
    doWorld()
    println("Done") // runs once coroutines finish
}

// launch two coroutines, suspend until both have finished
suspend fun doWorld() = coroutineScope {
    launch {
        delay(2000L)
        println("World 2")
    }
    launch {
        delay(1000L)
        println("World 1")
    }
    println("Hello") // runs immediately
}

/*
output:
Hello
World 1
World 2
Done
*/
```
### C#
```csharp
using System;
using System.Threading.Tasks;

static async Task Main()
{
    await DoWorld();
    Console.WriteLine("Done"); // runs once tasks finish
}

static async Task DoWorld()
{
    // fire off two tasks
    var task1 = Task.Run(async () =>
    {
        await Task.Delay(2000);
        Console.WriteLine("World 2");
    });

    var task2 = Task.Run(async () =>
    {
        await Task.Delay(1000);
        Console.WriteLine("World 1");
    });

    Console.WriteLine("Hello"); // runs immediately

    // concurrency equivalent, wait for both tasks to finish
    await Task.WhenAll(task1, task2);
}
/*
output:
Hello
World 1
World 2
Done
*/
```

## Lambda functions
### Kotlin example
```kotlin
{ n: Int -> n % 2 == 0 }   // explicit type + parameter
{ n -> n * 2 }             // inferred type
{ it * 2 }                 // single-parameter shorthand
{ a, b -> a + b }          // multiple parameters
```

### C# example
```csharp
n => n % 2 == 0        // single parameter
n => n * 2             // inferred type
(x, y) => x + y        // multiple parameters
() => 42               // no parameters
```
## Null safety

### Kotlin example
```kotlin
var a: String? = "letter a"
a = null

// returns null
print(a)

// results in compiler error
val b = a.length
print(b)

// safe call operator ?. checks nullability, returns length or null
val c = a?.length
print(c)
```

### C# example
```csharp
string? a = "letter a";

a = null;

// returns null
Console.WriteLine(a);

// results in compiler error
int b = a.Length;
Console.WriteLine(b);

// safe call operator ?. checks nullability, returns length or null
int? c = a?.Length;
Console.WriteLine(c);

```
## Types and type inferencing

### Kotlin
`val` = immutable reference  
`var` = mutable reference
```kotlin
// Numbers
val byteVal: Byte = 127
val shortVal: Short = 32000
val intVal: Int = 1_000_000
val longVal: Long = 1_000_000_000L
val floatVal: Float = 3.14F
val doubleVal: Double = 3.1415926535

// Characters and Strings
val charVal: Char = 'A'
val stringVal: String = "Hello Kotlin"

// Booleans
val boolVal: Boolean = true

// Arrays
val intArray: IntArray = intArrayOf(1, 2, 3)
val stringArray: Array<String> = arrayOf("a", "b", "c")

// Nullable type
val nullableString: String? = null

// Any (base type for all non-nullable types)
val anyVar: Any = 42

// Unit (similar to void in C#)
fun returnUnit(): Unit { println("Unit function") }

// Nothing (a function that never returns)
fun throwError(): Nothing { throw Exception("Oops!") }

```
### C# 
```csharp
// Numbers
byte byteVar = 127;
short shortVar = 32000;
int intVar = 1_000_000;
long longVar = 1_000_000_000L;
float floatVar = 3.14F;
double doubleVar = 3.1415926535;

// Characters and Strings
char charVar = 'A';
string stringVar = "Hello C#";

// Booleans
bool boolVar = true;

// Arrays
int[] intArray = new int[] { 1, 2, 3 };
string[] stringArray = new string[] { "a", "b", "c" };

// Nullable type
string? nullableString = null;

// Object (base type for all reference types)
object anyVar = 42;

// void method
void ReturnVoid() { Console.WriteLine("Void method"); }

// method that never returns
void ThrowError() { throw new Exception("Oops!"); }

```
## Extension methods
### Kotlin example
```kotlin
// General structure
fun TypeName.functionName(): ReturnType {
    // implementation
}

// Example extension method
fun String.getFirstChar(): Char {
    return this[0]
}

// Call extension method - acts as if getFirstChar() is a method of String

val word = "Kotlin"
println(name.getFirstChar()) // output: K
```
### C# example
```csharp
// General structure
public static class Extensions 
{
    public static ReturnType MethodName(this TypeName obj) 
    {
        // implementation
    }
}

// Example extension method - must be a static method inside a static class 
public static class StringExtensions 
{
    public static char GetFirstChar(this string str) 
    {
        return str[0];
    }
}

// Call extension method
string name = "Csharp";
Console.WriteLine(name.GetFirstChar()); // output: C
```
