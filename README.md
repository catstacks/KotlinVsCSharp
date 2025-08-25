
# Syntax and Features

## Filtering with predicates vs LINQ

A **predicate** is a lambda function that takes a collection element and returns a boolean value. If a value of `true` is returned, it means the collection element and predicate were matched.

The `::` syntax lets you pass a function without invoking it.

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
### Kotlin
```kotlin
import kotlinx.coroutines.*

suspend fun fetchData(): String {
    delay(1000)  // suspend without blocking thread
    return "Data"
}

fun main() = runBlocking {
    val result = fetchData()
    println(result)
}
```
### C#
```csharp
using System.Threading.Tasks;

async Task<string> FetchDataAsync() 
{
    await Task.Delay(1000);  // non-blocking wait
    return "Data";
}

static async Task Main() 
{
    var result = await FetchDataAsync();
    Console.WriteLine(result);
}
```

## Lambda functions
### Kotlin example
```kotlin
fun isEven(n: Int) = n % 2 == 0
```

### C# example
```csharp
bool IsEven(int n) => n % 2 == 0;
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
