# Go for Beginners --- Complete Learning Guide

> A structured, practical introduction to the Go programming language.
>
> **Goal:** understand Go step by step, write small programs
> confidently, and build a solid foundation for backend development,
> command-line tools, and concurrent applications.

------------------------------------------------------------------------

# 1. How to Use This Guide

Follow the chapters in order.

For each topic:

1.  Read the explanation.
2.  Type the example yourself.
3.  Change the example and observe the result.
4.  Solve the practice task without looking at the solution.
5.  Move to the next chapter only when the idea feels familiar.

The examples use modern Go and favor clear, idiomatic code. Unless noted
otherwise, snippets belong inside a `.go` file with `package main`.

------------------------------------------------------------------------

# 2. What Is Go?

Go (also called Golang) is an open-source, compiled programming language
designed for simplicity, efficiency, and reliable software.

Go is commonly used for:

-   backend services and REST APIs
-   command-line applications
-   cloud infrastructure and DevOps tools
-   networking software
-   distributed systems
-   concurrent programs

Go has a small language specification, a built-in toolchain, garbage
collection, and first-class support for concurrency.

A simple Go program:

``` go
package main

import "fmt"

func main() {
    fmt.Println("Hello, Go!")
}
```

`fmt.Println()` prints text followed by a newline.

------------------------------------------------------------------------

# 3. Installing and Running Go

Install Go using the instructions at <https://go.dev/dl/>.

Check the installation:

``` bash
go version
```

Create a file named `main.go` and run it:

``` bash
go run main.go
```

Compile an executable:

``` bash
go build
```

Format a file:

``` bash
gofmt -w main.go
```

Go's standard toolchain includes formatting, testing, documentation,
dependency management, and static analysis commands.

------------------------------------------------------------------------

# 4. Your First Go Program

A Go source file commonly starts with a package declaration.

``` go
package main

import "fmt"

func main() {
    fmt.Println("Hello, world!")
}
```

Important parts:

-   `package main` declares an executable program.
-   `import "fmt"` makes the formatting package available.
-   `func main()` is the entry point of an executable.
-   `{}` delimit blocks.
-   Go statements usually do not need semicolons.

Go is case-sensitive. `Println` and `println` are different identifiers.

------------------------------------------------------------------------

# 5. Comments

Comments are ignored by the compiler.

## Single-line comments

``` go
// This is a comment.
var age = 20
```

## Multi-line comments

``` go
/*
This is a
multi-line comment.
*/
```

Use comments to explain why something is done, not to narrate every
obvious line.

------------------------------------------------------------------------

# 6. Variables

Variables store values.

Use `var` for a variable declaration:

``` go
var age int = 20
var name string = "Alex"
```

Go can infer the type:

``` go
var country = "Latvia"
```

Inside functions, the short declaration `:=` is common:

``` go
func main() {
    score := 100
    username := "Alex"

    fmt.Println(score, username)
}
```

`:=` declares a new variable. It cannot be used at package level.

Variables declared with `var` but not initialized receive their zero
value.

``` go
var count int
var message string
var active bool

fmt.Println(count)   // 0
fmt.Println(message) // ""
fmt.Println(active)  // false
```

------------------------------------------------------------------------

# 7. Constants

Use `const` for values that do not change.

``` go
const pi = 3.14159
const appName = "Task Tracker"
```

Constants are evaluated at compile time and cannot be reassigned.

``` go
const maxUsers = 100

// maxUsers = 200 // Compile error
```

Go constants can be untyped until a concrete type is needed.

------------------------------------------------------------------------

# 8. Naming Conventions

Go uses `MixedCaps` / `camelCase` rather than underscores for most
identifiers.

``` go
userName := "Alex"
totalPrice := 100
isLoggedIn := true
```

Exported identifiers start with an uppercase letter:

``` go
func CalculateTotal() int {
    return 0
}

var DefaultTimeout = 30
```

Unexported identifiers start with a lowercase letter:

``` go
func calculateTotal() int {
    return 0
}
```

An identifier is exported when its name begins with an uppercase Unicode
letter. Exported names are visible to other packages.

Prefer short, meaningful names. A short name such as `i` is fine for a
small loop; use descriptive names when the scope or purpose is broader.

------------------------------------------------------------------------

# 9. Basic Data Types

Go is statically typed: each variable has a type.

Common types include:

  Type                                            Meaning
  ----------------------------------------------- --------------------------------------------------
  `bool`                                          `true` or `false`
  `string`                                        text
  `int`, `int8`, `int16`, `int32`, `int64`        signed integers
  `uint`, `uint8`, `uint16`, `uint32`, `uint64`   unsigned integers
  `byte`                                          alias for `uint8`
  `rune`                                          alias for `int32`, commonly a Unicode code point
  `float32`, `float64`                            floating-point numbers
  `complex64`, `complex128`                       complex numbers

Example:

``` go
var age int = 20
var price float64 = 19.99
var isStudent bool = true
var name string = "Alex"

fmt.Println(age, price, isStudent, name)
```

Use `int` for ordinary integer calculations unless a specific size is
required by an API or data format.

------------------------------------------------------------------------

# 10. Zero Values

Every Go type has a zero value.

``` go
var number int       // 0
var decimal float64  // 0
var text string      // ""
var ready bool       // false
var pointer *int     // nil
```

The zero value is useful: a variable is initialized even when you do not
provide an explicit value.

For structs, arrays, and other composite values, each field or element
is initialized to its own zero value.

------------------------------------------------------------------------

# 11. Checking and Converting Types

Go does not automatically convert between different numeric types.

``` go
var whole int = 42
var decimal float64 = float64(whole)

fmt.Println(decimal)
```

Convert a floating-point number to an integer:

``` go
price := 19.99
roundedDown := int(price)

fmt.Println(roundedDown) // 19
```

This conversion truncates the fractional part; it does not round.

Use `fmt.Printf` with format verbs to inspect values and types:

``` go
age := 20

fmt.Printf("value: %v, type: %T\n", age, age)
```

------------------------------------------------------------------------

# 12. Strings

A string is an immutable sequence of bytes, usually containing UTF-8
text.

``` go
name := "Alex"
message := "Hello, Go!"
```

Join strings with `+`:

``` go
firstName := "Alex"
lastName := "Smith"

fullName := firstName + " " + lastName
fmt.Println(fullName)
```

Use `fmt.Sprintf` to build formatted strings:

``` go
name := "Alex"
age := 20

message := fmt.Sprintf("My name is %s and I am %d years old.", name, age)
fmt.Println(message)
```

Raw string literals use backticks:

``` go
text := `This string can contain
multiple lines and "quotes".`
```

Useful standard-library functions from `strings`:

``` go
import "strings"

message := "  Hello, Go!  "

fmt.Println(len(message))                       // byte length
fmt.Println(strings.TrimSpace(message))
fmt.Println(strings.ToUpper(message))
fmt.Println(strings.ToLower(message))
fmt.Println(strings.Contains(message, "Go"))
fmt.Println(strings.HasPrefix(message, "  Hello"))
fmt.Println(strings.ReplaceAll(message, "Go", "Golang"))
```

Remember: `len(s)` returns the number of bytes, not necessarily the
number of Unicode characters.

------------------------------------------------------------------------

# 13. Runes and UTF-8

A `rune` represents a Unicode code point. A string may contain multiple
bytes for one visible character.

``` go
text := "Привет"

fmt.Println(len(text))         // number of bytes
fmt.Println(len([]rune(text))) // number of Unicode code points
```

Iterate over Unicode code points with `range`:

``` go
for index, character := range text {
    fmt.Printf("%d: %c\n", index, character)
}
```

The index from `range` over a string is a byte offset.

For user-perceived characters (grapheme clusters), a rune count may
still not be sufficient; some visible characters consist of multiple
code points.

------------------------------------------------------------------------

# 14. Numbers and Arithmetic

Basic arithmetic operators:

``` go
fmt.Println(5 + 5)   // addition
fmt.Println(10 - 3)  // subtraction
fmt.Println(4 * 3)   // multiplication
fmt.Println(10 / 2)  // division
fmt.Println(10 % 3)  // remainder
```

Integer division discards the fractional part:

``` go
fmt.Println(7 / 2) // 3
fmt.Println(7.0 / 2) // 3.5
```

Go does not have a built-in exponentiation operator. Use `math.Pow` for
floating-point powers:

``` go
import "math"

fmt.Println(math.Pow(2, 3)) // 8
```

Increment and decrement are statements:

``` go
count := 1
count++
count--

fmt.Println(count)
```

Unlike some languages, Go does not allow `count++` as an expression.

------------------------------------------------------------------------

# 15. Operators

## Assignment

``` go
score := 10

score += 5
score -= 2
score *= 2
score /= 2
score %= 3
```

## Comparison

``` go
fmt.Println(5 > 3)
fmt.Println(5 < 3)
fmt.Println(5 >= 5)
fmt.Println(4 <= 10)
fmt.Println(10 == 10)
fmt.Println(10 != 5)
```

Equality uses `==`; inequality uses `!=`.

Unlike JavaScript, Go does not have a separate strict-equality operator.
Go's type system prevents many cross-type comparisons.

------------------------------------------------------------------------

# 16. Boolean and Logical Operators

Go has two boolean values: `true` and `false`.

## AND --- `&&`

Both conditions must be true.

``` go
age := 20
hasTicket := true

if age >= 18 && hasTicket {
    fmt.Println("Access granted")
}
```

## OR --- `||`

At least one condition must be true.

``` go
isAdmin := false
isModerator := true

if isAdmin || isModerator {
    fmt.Println("You can manage content")
}
```

## NOT --- `!`

Reverses a boolean value.

``` go
isLoggedIn := false

if !isLoggedIn {
    fmt.Println("Please log in")
}
```

Go's `&&` and `||` operators use short-circuit evaluation.

------------------------------------------------------------------------

# 17. Conditions: `if`, `else if`, and `else`

``` go
age := 20

if age >= 18 {
    fmt.Println("You are an adult.")
} else {
    fmt.Println("You are not an adult.")
}
```

Multiple branches:

``` go
score := 75

if score >= 90 {
    fmt.Println("Excellent")
} else if score >= 70 {
    fmt.Println("Good")
} else {
    fmt.Println("Keep practicing")
}
```

Parentheses around conditions are optional and are not normally used.

Go allows a short statement before the condition:

``` go
if score := 85; score >= 70 {
    fmt.Println("Passed:", score)
}
```

The variable declared in the `if` statement is scoped to that `if` and
its `else` blocks.

------------------------------------------------------------------------

# 18. `switch`

A `switch` selects one matching case.

``` go
day := "Monday"

switch day {
case "Monday":
    fmt.Println("Start of the week")
case "Friday":
    fmt.Println("Almost the weekend")
default:
    fmt.Println("Regular day")
}
```

Go automatically stops after the first matching case. You usually do not
need `break`.

A switch can have multiple values in one case:

``` go
day := "Saturday"

switch day {
case "Saturday", "Sunday":
    fmt.Println("Weekend")
default:
    fmt.Println("Weekday")
}
```

A condition-only switch is also possible:

``` go
temperature := 28

switch {
case temperature >= 30:
    fmt.Println("Hot")
case temperature >= 20:
    fmt.Println("Warm")
default:
    fmt.Println("Cool")
}
```

Use `fallthrough` only when you deliberately want execution to continue
into the next case.

------------------------------------------------------------------------

# 19. Loops: `for`

Go has one looping keyword: `for`.

## Traditional `for`

``` go
for count := 1; count <= 5; count++ {
    fmt.Println(count)
}
```

## While-style loop

``` go
count := 1

for count <= 5 {
    fmt.Println(count)
    count++
}
```

## Infinite loop

``` go
for {
    fmt.Println("Running")
    break
}
```

Go does not have `while` or `do...while` keywords.

------------------------------------------------------------------------

# 20. `break` and `continue`

`break` stops the loop:

``` go
for i := 1; i <= 10; i++ {
    if i == 5 {
        break
    }

    fmt.Println(i)
}
```

`continue` skips the current iteration:

``` go
for i := 1; i <= 5; i++ {
    if i == 3 {
        continue
    }

    fmt.Println(i)
}
```

------------------------------------------------------------------------

# 21. Functions

Functions group reusable logic.

``` go
func greet() {
    fmt.Println("Hello!")
}

func main() {
    greet()
}
```

A function declaration includes:

-   `func`
-   a function name
-   parameters in parentheses
-   optional return types
-   a function body

------------------------------------------------------------------------

# 22. Parameters and Return Values

``` go
func greetUser(name string) {
    fmt.Println("Hello,", name)
}
```

Call the function:

``` go
greetUser("Alex")
```

A function can return a value:

``` go
func addNumbers(a int, b int) int {
    return a + b
}

func main() {
    result := addNumbers(6, 7)
    fmt.Println(result)
}
```

When consecutive parameters have the same type, the type can be written
once:

``` go
func multiply(a, b int) int {
    return a * b
}
```

------------------------------------------------------------------------

# 23. Multiple Return Values

Go functions can return more than one value.

``` go
func divide(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("cannot divide by zero")
    }

    return a / b, nil
}
```

Call it:

``` go
result, err := divide(10, 2)
if err != nil {
    fmt.Println("Error:", err)
    return
}

fmt.Println(result)
```

Multiple return values are commonly used to return a result together
with an error.

------------------------------------------------------------------------

# 24. Named Return Values

A function can name its return values:

``` go
func rectangleArea(width, height float64) (area float64) {
    area = width * height
    return
}
```

A bare `return` returns the named result variables.

Named returns can be useful in small functions, but avoid them when they
make the data flow less clear.

------------------------------------------------------------------------

# 25. Variadic Functions

A variadic function accepts zero or more values of the same parameter
type.

``` go
func sum(numbers ...int) int {
    total := 0

    for _, number := range numbers {
        total += number
    }

    return total
}

func main() {
    fmt.Println(sum(1, 2, 3, 4))
}
```

The variadic parameter behaves like a slice inside the function.

You can pass a slice using `...`:

``` go
numbers := []int{1, 2, 3}
fmt.Println(sum(numbers...))
```

------------------------------------------------------------------------

# 26. Scope

Scope determines where an identifier can be used.

``` go
package main

import "fmt"

var globalName = "Alex"

func example() {
    localName := "Sam"

    fmt.Println(globalName)
    fmt.Println(localName)
}

func main() {
    example()
}
```

`localName` cannot be accessed outside `example`.

Variables declared inside a block are limited to that block and its
nested blocks.

------------------------------------------------------------------------

# 27. Arrays

An array stores a fixed number of values of the same type.

``` go
var numbers [3]int

numbers[0] = 10
numbers[1] = 20
numbers[2] = 30

fmt.Println(numbers)
```

You can initialize an array directly:

``` go
colors := [3]string{"red", "green", "blue"}
fmt.Println(colors[0])
```

Array length is part of its type. `[3]int` and `[4]int` are different
types.

------------------------------------------------------------------------

# 28. Slices

Slices are more flexible than arrays and are used frequently in Go.

``` go
numbers := []int{10, 20, 30, 40}

fmt.Println(numbers[0])
fmt.Println(len(numbers))
fmt.Println(cap(numbers))
```

A slice is a descriptor referring to an underlying array. It has a
length and a capacity.

## Slice expressions

``` go
numbers := []int{10, 20, 30, 40, 50}

fmt.Println(numbers[1:4]) // [20 30 40]
fmt.Println(numbers[:2])  // [10 20]
fmt.Println(numbers[2:])  // [30 40 50]
```

The start index is included; the end index is excluded.

------------------------------------------------------------------------

# 29. Slice Operations

Append values:

``` go
numbers := []int{1, 2, 3}
numbers = append(numbers, 4, 5)

fmt.Println(numbers)
```

Create a slice with `make`:

``` go
scores := make([]int, 3)
scores[0] = 100

fmt.Println(scores)
```

Create a slice with a specified length and capacity:

``` go
items := make([]string, 2, 5)
fmt.Println(len(items)) // 2
fmt.Println(cap(items)) // 5
```

Copy elements:

``` go
source := []int{1, 2, 3}
destination := make([]int, len(source))

copy(destination, source)
fmt.Println(destination)
```

`append` may allocate a new underlying array. Always use its returned
slice:

``` go
numbers = append(numbers, 6)
```

------------------------------------------------------------------------

# 30. Iterating with `range`

Use `range` to iterate over arrays, slices, maps, strings, and channels.

``` go
languages := []string{"Go", "JavaScript", "Python"}

for index, language := range languages {
    fmt.Println(index, language)
}
```

If you only need the value, ignore the index with `_`:

``` go
for _, language := range languages {
    fmt.Println(language)
}
```

If you only need the index:

``` go
for index := range languages {
    fmt.Println(index)
}
```

------------------------------------------------------------------------

# 31. Maps

Maps store key-value pairs.

``` go
ages := map[string]int{
    "Alex": 20,
    "Sam":  25,
}

fmt.Println(ages["Alex"])
```

Add or update a value:

``` go
ages["Taylor"] = 30
ages["Alex"] = 21
```

Delete a key:

``` go
delete(ages, "Sam")
```

Check whether a key exists:

``` go
age, exists := ages["Alex"]
if exists {
    fmt.Println("Age:", age)
}
```

The zero value of a map is `nil`; initialize a map with a literal or
`make` before assigning entries.

Map iteration order is unspecified. Do not rely on a particular order.

------------------------------------------------------------------------

# 32. Structs

A struct groups fields into one type.

``` go
type User struct {
    Name  string
    Age   int
    Email string
}
```

Create a value:

``` go
user := User{
    Name:  "Alex",
    Age:   20,
    Email: "alex@example.com",
}

fmt.Println(user.Name)
```

You can also use a zero-valued struct:

``` go
var user User
user.Name = "Sam"
```

Prefer keyed fields in struct literals when it improves clarity.

------------------------------------------------------------------------

# 33. Struct Methods

Methods are functions associated with a receiver type.

``` go
type User struct {
    Name string
}

func (u User) Greet() string {
    return "Hello, " + u.Name
}

func main() {
    user := User{Name: "Alex"}
    fmt.Println(user.Greet())
}
```

The receiver `(u User)` is a value receiver. The method receives a copy
of the value.

------------------------------------------------------------------------

# 34. Pointer Receivers

Use a pointer receiver when a method needs to modify the original value
or when copying the value would be undesirable.

``` go
type Counter struct {
    Value int
}

func (c *Counter) Increment() {
    c.Value++
}

func main() {
    counter := Counter{}
    counter.Increment()

    fmt.Println(counter.Value)
}
```

Go automatically handles taking the address for many method calls on
addressable values.

Choose value or pointer receivers consistently for a type.

------------------------------------------------------------------------

# 35. Pointers

A pointer stores the memory address of a value.

``` go
number := 42
pointer := &number

fmt.Println(number)
fmt.Println(pointer)
fmt.Println(*pointer)
```

-   `&value` gets the address.
-   `*pointer` accesses the value at that address.

Change a value through a pointer:

``` go
number := 10
pointer := &number

*pointer = 20

fmt.Println(number) // 20
```

The zero value of a pointer is `nil`.

------------------------------------------------------------------------

# 36. `new` and `make`

Both are built-in functions, but they serve different purposes.

`new(T)` allocates zeroed storage for a value of type `T` and returns
`*T`:

``` go
pointer := new(int)
fmt.Println(*pointer) // 0
```

`make` initializes slices, maps, and channels:

``` go
numbers := make([]int, 3)
scores := make(map[string]int)
messages := make(chan string)
```

Use `make` for these built-in reference-like types; it does not return a
pointer.

------------------------------------------------------------------------

# 37. Interfaces

An interface specifies a set of methods.

``` go
type Speaker interface {
    Speak() string
}
```

A type implements an interface by implementing its methods. No explicit
`implements` declaration is needed.

``` go
type Dog struct{}

func (Dog) Speak() string {
    return "Woof!"
}

func saySomething(s Speaker) {
    fmt.Println(s.Speak())
}

func main() {
    saySomething(Dog{})
}
```

Interfaces are most useful when they let code depend on behavior rather
than a specific concrete type.

------------------------------------------------------------------------

# 38. The Empty Interface and `any`

The empty interface has no methods, so every type implements it.

``` go
func printValue(value any) {
    fmt.Println(value)
}
```

`any` is an alias for `interface{}`.

Use `any` when a value can genuinely be of different types. Prefer
specific types when possible because they make code easier to understand
and validate.

------------------------------------------------------------------------

# 39. Type Assertions and Type Switches

A type assertion extracts a concrete value from an interface:

``` go
var value any = "hello"

text, ok := value.(string)
if ok {
    fmt.Println(text)
}
```

The two-result form avoids a panic if the dynamic type does not match.

A type switch handles multiple possible types:

``` go
func describe(value any) {
    switch v := value.(type) {
    case string:
        fmt.Println("String:", v)
    case int:
        fmt.Println("Integer:", v)
    case bool:
        fmt.Println("Boolean:", v)
    default:
        fmt.Printf("Other type: %T\n", v)
    }
}
```

------------------------------------------------------------------------

# 40. Embedding and Composition

Go favors composition. A struct can embed another type:

``` go
type Address struct {
    City    string
    Country string
}

type User struct {
    Name string
    Address
}

func main() {
    user := User{
        Name: "Alex",
        Address: Address{
            City:    "Riga",
            Country: "Latvia",
        },
    }

    fmt.Println(user.City)
}
```

Embedding promotes fields and methods for convenient access. It is not
class inheritance.

------------------------------------------------------------------------

# 41. Packages

Packages organize related Go code.

A project might look like:

``` text
my-project/
├── go.mod
├── main.go
└── calculator/
    └── calculator.go
```

`calculator/calculator.go`:

``` go
package calculator

func Add(a, b int) int {
    return a + b
}
```

`main.go`:

``` go
package main

import (
    "fmt"

    "example.com/my-project/calculator"
)

func main() {
    fmt.Println(calculator.Add(2, 3))
}
```

The import path depends on the module path declared in `go.mod`.

------------------------------------------------------------------------

# 42. Go Modules

A module is a collection of related Go packages.

Create a module:

``` bash
mkdir my-project
cd my-project
go mod init example.com/my-project
```

This creates a `go.mod` file.

Common commands:

``` bash
go mod tidy
go list -m all
go get example.com/some/package
```

-   `go mod tidy` adds missing and removes unused module requirements.
-   `go get` adds or changes a dependency requirement.
-   `go.mod` describes module identity and dependencies.
-   `go.sum` records checksums for downloaded module content.

Commit `go.mod` and `go.sum` to version control for an application.

------------------------------------------------------------------------

# 43. Importing Packages

Import one package:

``` go
import "fmt"
```

Import several packages:

``` go
import (
    "fmt"
    "strings"
    "time"
)
```

Use a package through its package name:

``` go
fmt.Println(strings.ToUpper("hello"))
fmt.Println(time.Now())
```

Avoid dot imports in ordinary application code because they hide where
identifiers come from.

------------------------------------------------------------------------

# 44. The Standard Library

Go includes a rich standard library.

Useful packages include:

-   `fmt` --- formatted input and output
-   `strings` --- string operations
-   `strconv` --- conversions between strings and basic types
-   `math` --- mathematical functions
-   `time` --- dates, times, and durations
-   `os` --- operating-system interaction
-   `io` --- input/output interfaces
-   `bufio` --- buffered input and output
-   `encoding/json` --- JSON encoding and decoding
-   `net/http` --- HTTP clients and servers
-   `context` --- cancellation and request-scoped values
-   `log` --- basic logging
-   `testing` --- automated tests

Learn to search the official documentation at <https://pkg.go.dev/>.

------------------------------------------------------------------------

# 45. Input from the Console

Use `fmt.Scan` for simple whitespace-separated input:

``` go
var name string
var age int

fmt.Print("Enter your name and age: ")
_, err := fmt.Scan(&name, &age)
if err != nil {
    fmt.Println("Input error:", err)
    return
}

fmt.Printf("Hello, %s. You are %d.\n", name, age)
```

Use `bufio.Reader` when you need to read a full line containing spaces:

``` go
reader := bufio.NewReader(os.Stdin)

fmt.Print("Enter a sentence: ")
line, err := reader.ReadString('\n')
if err != nil && err != io.EOF {
    fmt.Println("Input error:", err)
    return
}

fmt.Println("You entered:", strings.TrimSpace(line))
```

This example requires imports for `bufio`, `fmt`, `io`, `os`, and
`strings`.

------------------------------------------------------------------------

# 46. Formatting Output

`fmt.Printf` uses format verbs:

``` go
name := "Alex"
age := 20
price := 19.99

fmt.Printf("Name: %s\n", name)
fmt.Printf("Age: %d\n", age)
fmt.Printf("Price: %.2f\n", price)
fmt.Printf("Value: %v\n", price)
fmt.Printf("Type: %T\n", price)
```

Common verbs:

  Verb    Meaning
  ------- --------------------------
  `%v`    default representation
  `%+v`   struct fields with names
  `%#v`   Go-syntax representation
  `%T`    type
  `%s`    string
  `%d`    decimal integer
  `%f`    floating-point number
  `%t`    boolean
  `%q`    quoted string

------------------------------------------------------------------------

# 47. Errors

Go commonly represents failure with an `error` value.

``` go
func findUser(id int) (string, error) {
    if id <= 0 {
        return "", fmt.Errorf("invalid user ID: %d", id)
    }

    return "Alex", nil
}
```

Handle errors explicitly:

``` go
name, err := findUser(10)
if err != nil {
    fmt.Println("Error:", err)
    return
}

fmt.Println(name)
```

`nil` means there is no error.

A common Go pattern is:

``` go
result, err := doSomething()
if err != nil {
    return err
}
```

Do not ignore errors unless you have a clear reason.

------------------------------------------------------------------------

# 48. Creating and Wrapping Errors

Create a simple error:

``` go
err := errors.New("something went wrong")
```

Format an error:

``` go
err := fmt.Errorf("could not load user %d", 42)
```

Wrap an existing error with `%w`:

``` go
if err != nil {
    return fmt.Errorf("load configuration: %w", err)
}
```

Use `errors.Is` to check for a particular error and `errors.As` to
inspect a particular error type:

``` go
if errors.Is(err, os.ErrNotExist) {
    fmt.Println("File does not exist")
}
```

Wrapping errors preserves the underlying error for inspection.

------------------------------------------------------------------------

# 49. `defer`

`defer` schedules a function call to run when the surrounding function
returns.

``` go
func example() {
    defer fmt.Println("This runs last")

    fmt.Println("This runs first")
}
```

Deferred calls run in last-in, first-out order:

``` go
func main() {
    defer fmt.Println("first defer")
    defer fmt.Println("second defer")
    fmt.Println("main")
}
```

Output:

``` text
main
second defer
first defer
```

`defer` is often used to close files and release resources:

``` go
file, err := os.Open("notes.txt")
if err != nil {
    return
}
defer file.Close()
```

Check errors from cleanup operations when they matter.

------------------------------------------------------------------------

# 50. `panic` and `recover`

`panic` stops normal execution of the current goroutine and begins
unwinding deferred calls.

``` go
func mustHaveValue(value string) {
    if value == "" {
        panic("value cannot be empty")
    }
}
```

`recover` can catch a panic only when called from a deferred function in
the same goroutine:

``` go
func protect() {
    defer func() {
        if value := recover(); value != nil {
            fmt.Println("Recovered:", value)
        }
    }()

    panic("unexpected problem")
}
```

Use ordinary error returns for expected failures. Do not use `panic` as
a replacement for normal error handling.

------------------------------------------------------------------------

# 51. Files

The `os` package provides basic file operations.

Read an entire file:

``` go
data, err := os.ReadFile("notes.txt")
if err != nil {
    fmt.Println("Read error:", err)
    return
}

fmt.Println(string(data))
```

Write a file:

``` go
content := []byte("Hello from Go!\n")

err := os.WriteFile("output.txt", content, 0644)
if err != nil {
    fmt.Println("Write error:", err)
    return
}
```

The permission mode is interpreted according to operating-system rules.
Be deliberate about permissions and file paths.

------------------------------------------------------------------------

# 52. Working with File Handles

Open a file for reading:

``` go
file, err := os.Open("notes.txt")
if err != nil {
    return err
}
defer file.Close()
```

Create or truncate a file for writing:

``` go
file, err := os.Create("output.txt")
if err != nil {
    return err
}
defer file.Close()

_, err = file.WriteString("Hello!\n")
if err != nil {
    return err
}
```

For large files, use streaming APIs such as `bufio.Scanner`,
`bufio.Reader`, or `io.Copy` rather than loading the entire file into
memory.

------------------------------------------------------------------------

# 53. JSON

JSON is a common format for exchanging data.

Use struct tags to map Go fields to JSON keys:

``` go
type User struct {
    Name  string `json:"name"`
    Age   int    `json:"age"`
    Email string `json:"email,omitempty"`
}
```

Encode a value:

``` go
user := User{Name: "Alex", Age: 20}

data, err := json.Marshal(user)
if err != nil {
    return err
}

fmt.Println(string(data))
```

Decode JSON:

``` go
input := `{"name":"Alex","age":20}`

var user User
err := json.Unmarshal([]byte(input), &user)
if err != nil {
    return err
}

fmt.Println(user.Name)
```

`json.Unmarshal` needs a pointer so it can populate the destination
value.

------------------------------------------------------------------------

# 54. Dates and Times

Use the `time` package.

``` go
now := time.Now()

fmt.Println(now)
fmt.Println(now.Year())
fmt.Println(now.Month())
fmt.Println(now.Day())
```

Create a duration:

``` go
timeout := 5 * time.Second
fmt.Println(timeout)
```

Add time:

``` go
tomorrow := time.Now().Add(24 * time.Hour)
fmt.Println(tomorrow)
```

Go formats dates using a reference time:

``` go
now := time.Now()
fmt.Println(now.Format("2006-01-02 15:04:05"))
```

Use the exact reference layout values shown above; Go does not use
`YYYY-MM-DD` as the layout.

Be aware of time zones when storing or comparing times. Use UTC where
appropriate and convert for display.

------------------------------------------------------------------------

# 55. Regular Expressions

The `regexp` package supports regular expressions.

``` go
pattern := regexp.MustCompile(`(?i)go`)

fmt.Println(pattern.MatchString("I am learning Go"))
```

For input that may be invalid, use `regexp.Compile` and handle its
error:

``` go
pattern, err := regexp.Compile(`^[a-z]+$`)
if err != nil {
    return err
}

fmt.Println(pattern.MatchString("hello"))
```

Prefer simple string functions when a regular expression is unnecessary.

------------------------------------------------------------------------

# 56. Generics

Generics let functions and types work with multiple types while
preserving compile-time type checking.

``` go
func Min[T ~int | ~float64](a, b T) T {
    if a < b {
        return a
    }
    return b
}

func main() {
    fmt.Println(Min(3, 7))
    fmt.Println(Min(2.5, 1.5))
}
```

`T` is a type parameter. The constraint limits which types can be used.

Generics are useful for reusable algorithms and data structures. Do not
use them when a simple concrete function is clearer.

------------------------------------------------------------------------

# 57. Goroutines

A goroutine is a lightweight unit of concurrent execution managed by the
Go runtime.

Start a goroutine with `go`:

``` go
func sayHello() {
    fmt.Println("Hello from a goroutine")
}

func main() {
    go sayHello()

    time.Sleep(100 * time.Millisecond)
}
```

The sleep only demonstrates that the program may give the goroutine time
to run. It is not a reliable way to coordinate goroutines in real
applications.

Use synchronization tools such as channels, `sync.WaitGroup`, or
contexts to coordinate work.

------------------------------------------------------------------------

# 58. WaitGroups

A `sync.WaitGroup` waits for a collection of goroutines to finish.

``` go
var wg sync.WaitGroup

for i := 1; i <= 3; i++ {
    wg.Add(1)

    go func(number int) {
        defer wg.Done()
        fmt.Println("Worker", number)
    }(i)
}

wg.Wait()
fmt.Println("All workers finished")
```

Call `Add` before starting the goroutine. Each goroutine should call
`Done`, commonly with `defer`.

------------------------------------------------------------------------

# 59. Channels

Channels let goroutines communicate and synchronize.

Create a channel:

``` go
messages := make(chan string)
```

Send a value:

``` go
messages <- "hello"
```

Receive a value:

``` go
message := <-messages
```

A complete example:

``` go
func main() {
    messages := make(chan string)

    go func() {
        messages <- "Hello from another goroutine"
    }()

    message := <-messages
    fmt.Println(message)
}
```

An unbuffered channel send and receive synchronize with each other.

------------------------------------------------------------------------

# 60. Buffered Channels

A buffered channel can hold a limited number of values without an
immediate receiver.

``` go
messages := make(chan string, 2)

messages <- "one"
messages <- "two"

fmt.Println(<-messages)
fmt.Println(<-messages)
```

A send blocks when the buffer is full. A receive blocks when the buffer
is empty.

Choose buffer sizes based on the design of the program, not by
guesswork.

------------------------------------------------------------------------

# 61. Closing Channels and `range`

A sender can close a channel to indicate that no more values will be
sent.

``` go
numbers := make(chan int)

go func() {
    defer close(numbers)

    for i := 1; i <= 3; i++ {
        numbers <- i
    }
}()

for number := range numbers {
    fmt.Println(number)
}
```

Only the sender (or a coordinator that knows sending is finished) should
close a channel. Sending to a closed channel causes a panic.

A receive can use the two-result form:

``` go
value, ok := <-numbers
```

`ok` is false when the channel is closed and drained.

------------------------------------------------------------------------

# 62. `select`

`select` waits on multiple channel operations.

``` go
select {
case message := <-messages:
    fmt.Println(message)
case <-time.After(time.Second):
    fmt.Println("Timed out")
}
```

If multiple cases are ready, Go chooses one pseudo-randomly.

A `default` case makes the select non-blocking:

``` go
select {
case message := <-messages:
    fmt.Println(message)
default:
    fmt.Println("No message ready")
}
```

------------------------------------------------------------------------

# 63. Mutexes and Shared State

When multiple goroutines access shared mutable data, protect it from
concurrent access.

``` go
type SafeCounter struct {
    mu    sync.Mutex
    value int
}

func (c *SafeCounter) Increment() {
    c.mu.Lock()
    defer c.mu.Unlock()

    c.value++
}

func (c *SafeCounter) Value() int {
    c.mu.Lock()
    defer c.mu.Unlock()

    return c.value
}
```

A mutex protects a critical section. Keep lock scopes small and ensure
every successful lock is eventually unlocked.

------------------------------------------------------------------------

# 64. The `context` Package

A context carries cancellation signals, deadlines, and request-scoped
values across API boundaries.

``` go
func doWork(ctx context.Context) error {
    select {
    case <-time.After(2 * time.Second):
        fmt.Println("Work completed")
        return nil
    case <-ctx.Done():
        return ctx.Err()
    }
}
```

Use a timeout:

``` go
ctx, cancel := context.WithTimeout(context.Background(), time.Second)
defer cancel()

if err := doWork(ctx); err != nil {
    fmt.Println("Work stopped:", err)
}
```

Pass contexts explicitly, usually as the first parameter. Do not store
them in structs or use them as optional function parameters.

------------------------------------------------------------------------

# 65. HTTP Client

The `net/http` package provides an HTTP client.

``` go
resp, err := http.Get("https://example.com")
if err != nil {
    return err
}
defer resp.Body.Close()

body, err := io.ReadAll(resp.Body)
if err != nil {
    return err
}

fmt.Println(resp.Status)
fmt.Println(string(body))
```

Always close response bodies. For production code, use an `http.Client`
with appropriate timeouts and check HTTP status codes.

------------------------------------------------------------------------

# 66. Building an HTTP Server

A basic HTTP server:

``` go
func helloHandler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintln(w, "Hello from Go!")
}

func main() {
    http.HandleFunc("/", helloHandler)

    log.Println("Server listening on :8080")
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```

Run it:

``` bash
go run .
```

Open `http://localhost:8080` in a browser.

For production services, configure server timeouts, graceful shutdown,
logging, and error handling.

------------------------------------------------------------------------

# 67. HTTP Methods and Request Data

An HTTP handler can inspect the request method and URL:

``` go
func usersHandler(w http.ResponseWriter, r *http.Request) {
    if r.Method != http.MethodGet {
        http.Error(w, "Method not allowed", http.StatusMethodNotAllowed)
        return
    }

    name := r.URL.Query().Get("name")
    fmt.Fprintf(w, "Hello, %s", name)
}
```

Use `http.MethodGet`, `http.MethodPost`, and related constants instead
of hard-coded method strings.

Validate input and avoid trusting request data.

------------------------------------------------------------------------

# 68. Middleware

Middleware wraps an HTTP handler to add behavior such as logging or
authentication.

``` go
func loggingMiddleware(next http.Handler) http.Handler {
    return http.HandlerFunc(func(w http.ResponseWriter, r *http.Request) {
        log.Println(r.Method, r.URL.Path)
        next.ServeHTTP(w, r)
    })
}
```

Use it:

``` go
mux := http.NewServeMux()
mux.HandleFunc("/", helloHandler)

server := &http.Server{
    Addr:    ":8080",
    Handler: loggingMiddleware(mux),
}
```

Middleware is ordinary composition: a handler receives a request and can
call another handler.

------------------------------------------------------------------------

# 69. Testing Basics

Go has a built-in testing package.

Create a file ending in `_test.go`:

``` go
package calculator

import "testing"

func Add(a, b int) int {
    return a + b
}

func TestAdd(t *testing.T) {
    got := Add(2, 3)
    want := 5

    if got != want {
        t.Fatalf("Add(2, 3) = %d; want %d", got, want)
    }
}
```

Run tests:

``` bash
go test ./...
```

A test function begins with `Test` and takes `*testing.T`.

------------------------------------------------------------------------

# 70. Table-Driven Tests

Table-driven tests make it easy to check multiple cases.

``` go
func TestAdd(t *testing.T) {
    tests := []struct {
        name string
        a, b int
        want int
    }{
        {"positive", 2, 3, 5},
        {"zero", 0, 4, 4},
        {"negative", -2, 1, -1},
    }

    for _, test := range tests {
        t.Run(test.name, func(t *testing.T) {
            got := Add(test.a, test.b)
            if got != test.want {
                t.Fatalf("got %d, want %d", got, test.want)
            }
        })
    }
}
```

Table-driven tests are a common Go convention.

------------------------------------------------------------------------

# 71. Benchmarks

Benchmarks measure performance.

``` go
func BenchmarkAdd(b *testing.B) {
    for i := 0; i < b.N; i++ {
        Add(10, 20)
    }
}
```

Run benchmarks:

``` bash
go test -bench=.
```

Measure before optimizing. Benchmark realistic workloads and avoid
drawing conclusions from tiny or noisy measurements.

------------------------------------------------------------------------

# 72. Fuzzing

Go supports fuzz testing through the `testing` package.

``` go
func FuzzParseNumber(f *testing.F) {
    f.Add("42")

    f.Fuzz(func(t *testing.T, input string) {
        _, _ = strconv.Atoi(input)
    })
}
```

Run fuzzing:

``` bash
go test -fuzz=FuzzParseNumber
```

Fuzzing supplies many generated inputs to help discover edge cases and
crashes.

------------------------------------------------------------------------

# 73. Debugging

Useful commands:

``` bash
go run .
go test ./...
go test -v ./...
go vet ./...
gofmt -w .
```

Use your editor's debugger to:

-   set breakpoints
-   step over and into functions
-   inspect variables
-   inspect the call stack
-   evaluate expressions

`fmt.Println` and structured logging are useful, but a debugger can
reveal how the program reaches a particular state.

------------------------------------------------------------------------

# 74. Formatting and Code Quality

Go has an official formatter: `gofmt`.

Format a file:

``` bash
gofmt -w main.go
```

Format a project:

``` bash
gofmt -w .
```

Other useful checks:

``` bash
go vet ./...
go test ./...
```

Follow the conventions in *Effective Go* and the Go Code Review Comments
document. Consistent formatting is expected in Go projects.

------------------------------------------------------------------------

# 75. Project Structure

A small application might look like:

``` text
task-app/
├── go.mod
├── go.sum
├── main.go
├── internal/
│   └── tasks/
│       ├── service.go
│       └── service_test.go
└── README.md
```

A few guidelines:

-   Start with a simple structure.
-   Group code by responsibility.
-   Use `internal` for packages that should not be imported by code
    outside the parent module tree.
-   Avoid creating many packages before there is a real need.
-   Keep package names short and descriptive.

There is no single directory layout required for every Go project.

------------------------------------------------------------------------

# 76. Command-Line Arguments

The `os` package exposes command-line arguments.

``` go
func main() {
    fmt.Println(os.Args)
}
```

`os.Args[0]` is the program name; later elements are the supplied
arguments.

For flags, use the standard `flag` package:

``` go
name := flag.String("name", "Guest", "name to greet")
flag.Parse()

fmt.Println("Hello,", *name)
```

Run:

``` bash
go run . -name=Alex
```

------------------------------------------------------------------------

# 77. Environment Variables

Use `os.Getenv` to read an environment variable:

``` go
port := os.Getenv("PORT")
if port == "" {
    port = "8080"
}

fmt.Println("Port:", port)
```

Use `os.LookupEnv` when you need to distinguish an unset variable from
one set to an empty string.

Do not hard-code secrets in source code or commit them to version
control.

------------------------------------------------------------------------

# 78. Common Beginner Mistakes

## Mistake 1: Forgetting that Go is statically typed

``` go
var age int = "20" // Compile error
```

Use a conversion when appropriate:

``` go
age := 20
```

## Mistake 2: Declaring a variable and never using it

Unused local variables and unused imports cause compile errors.

Remove them or use them.

## Mistake 3: Forgetting to handle errors

``` go
data, err := os.ReadFile("notes.txt")
if err != nil {
    return
}
_ = data
```

Handle the error meaningfully rather than ignoring it.

## Mistake 4: Confusing arrays and slices

`[3]int` is an array with a fixed length. `[]int` is a slice.

## Mistake 5: Forgetting that maps are not safe for concurrent writes

Protect shared maps with synchronization or use another concurrency-safe
design.

## Mistake 6: Using `time.Sleep` to coordinate goroutines

Use channels, wait groups, or contexts instead.

## Mistake 7: Forgetting to close response bodies and files

Use `defer` after checking that the resource was opened successfully.

------------------------------------------------------------------------

# 79. Clean Code Principles

Prefer:

``` go
totalPrice := calculateTotal(items)
```

over:

``` go
x := calc(items)
```

Good Go code is:

-   readable
-   simple
-   explicit
-   consistently formatted
-   organized into focused packages
-   careful about errors
-   easy to test
-   deliberate about concurrency

Avoid unnecessary abstractions. In Go, straightforward code is often the
most idiomatic solution.

------------------------------------------------------------------------

# 80. Security Basics

Every Go developer should understand:

-   input validation
-   authentication and authorization
-   secure handling of secrets
-   TLS and HTTPS
-   safe file path handling
-   SQL injection prevention
-   request size limits
-   timeouts and resource limits
-   dependency updates
-   safe error messages that do not leak secrets

Use parameterized SQL queries rather than building SQL statements by
concatenating untrusted input.

For HTTP servers, set sensible timeouts and validate incoming data.

------------------------------------------------------------------------

# 81. Performance Basics

Go can be efficient, but performance still depends on program design.

Learn to recognize:

-   unnecessary allocations
-   repeated work
-   excessive goroutine creation
-   lock contention
-   unbounded queues
-   inefficient I/O
-   large memory retention
-   excessive network requests

Useful tools include:

``` bash
go test -bench=.
go test -bench=. -benchmem
go test -cpuprofile=cpu.out
go test -memprofile=mem.out
```

Use Go's `pprof` tooling to inspect profiles. Measure before optimizing.

------------------------------------------------------------------------

# 82. Concurrency vs. Parallelism

Concurrency is about structuring a program so multiple tasks can make
progress independently.

Parallelism is about executing multiple tasks at the same time, often on
multiple CPU cores.

Goroutines make concurrent programming convenient. The Go runtime
schedules goroutines onto operating-system threads.

Concurrency does not automatically make a program faster. It can add
coordination costs and complexity.

------------------------------------------------------------------------

# 83. Race Detection

A data race happens when multiple goroutines access the same memory
concurrently and at least one access is a write without proper
synchronization.

Run tests with the race detector:

``` bash
go test -race ./...
```

You can also run an application with:

``` bash
go run -race .
```

The race detector is a valuable development tool, but it does not prove
that a program is free of every concurrency bug.

------------------------------------------------------------------------

# 84. Useful Go Tools

Become familiar with:

-   `go run` --- compile and run a program
-   `go build` --- compile packages
-   `go test` --- run tests
-   `go fmt` / `gofmt` --- format code
-   `go vet` --- report suspicious constructs
-   `go mod` --- manage modules
-   `go doc` --- view documentation
-   `go env` --- inspect Go environment settings
-   `go tool` --- access Go toolchain utilities

The official documentation is available at <https://go.dev/doc/>.

------------------------------------------------------------------------

# 85. Mini Project 1 --- Number Guessing Game

Build a command-line game that:

1.  generates a random number
2.  asks the player to guess
3.  tells the player whether the guess is too high or too low
4.  counts attempts
5.  stops when the player guesses correctly

Concepts practiced:

-   variables
-   input
-   conditions
-   loops
-   random numbers
-   type conversion
-   error handling

For modern Go, use the `math/rand` package. Do not use random numbers
for security-sensitive tokens; use `crypto/rand` for that.

------------------------------------------------------------------------

# 86. Mini Project 2 --- Todo CLI

Build a command-line todo application.

Start with a task type:

``` go
type Todo struct {
    ID        int
    Title     string
    Completed bool
}
```

Add operations to:

1.  add a task
2.  list tasks
3.  mark a task complete
4.  delete a task
5.  save tasks to a JSON file
6.  load tasks when the program starts

Concepts practiced:

-   structs
-   slices
-   functions
-   JSON
-   file operations
-   error handling

------------------------------------------------------------------------

# 87. Mini Project 3 --- REST API

Build a small HTTP API for tasks.

Possible endpoints:

``` text
GET    /tasks
GET    /tasks/{id}
POST   /tasks
PUT    /tasks/{id}
DELETE /tasks/{id}
```

Add:

1.  JSON request decoding
2.  input validation
3.  appropriate HTTP status codes
4.  error responses
5.  tests for handlers
6.  graceful server shutdown

Concepts practiced:

-   `net/http`
-   structs
-   JSON
-   methods and interfaces
-   errors
-   testing
-   context

------------------------------------------------------------------------

# 88. Mini Project 4 --- Concurrent URL Checker

Build a command-line program that checks several URLs.

The program should:

1.  read a list of URLs
2.  send HTTP requests
3.  limit the number of concurrent workers
4.  record status codes and durations
5.  handle timeouts and errors
6.  print a summary

Concepts practiced:

-   goroutines
-   channels
-   wait groups
-   HTTP clients
-   contexts
-   synchronization

Avoid starting an unlimited number of goroutines for untrusted or very
large input.

------------------------------------------------------------------------

# 89. Recommended Learning Order

## Stage 1 --- Core Syntax

Learn:

``` text
variables
constants
basic types
zero values
operators
conditions
switch
for loops
functions
```

## Stage 2 --- Data Structures

Learn:

``` text
arrays
slices
maps
structs
pointers
range
```

## Stage 3 --- Go Design

Learn:

``` text
methods
interfaces
composition
packages
modules
generics
```

## Stage 4 --- Errors and I/O

Learn:

``` text
error values
error wrapping
defer
files
console input
JSON
dates and times
```

## Stage 5 --- Concurrency

Learn:

``` text
goroutines
channels
select
wait groups
mutexes
context
race detection
```

## Stage 6 --- Backend Development

Learn:

``` text
HTTP clients
HTTP servers
handlers
middleware
REST APIs
timeouts
graceful shutdown
```

## Stage 7 --- Professional Workflow

Learn:

``` text
testing
table-driven tests
benchmarks
fuzzing
gofmt
go vet
debugging
profiling
Git
```

------------------------------------------------------------------------

# 90. Practice Tasks

Solve these without copying the examples.

## Beginner

1.  Declare a variable containing your name and print it.
2.  Create two integers and print their sum.
3.  Check whether a number is positive, negative, or zero.
4.  Print numbers from 1 to 20.
5.  Write a function that returns the square of an integer.
6.  Find the largest number in a slice.
7.  Count how many numbers in a slice are even.
8.  Create a struct representing a book.
9.  Write a function that converts Celsius to Fahrenheit.
10. Count the number of runes in a string.

## Intermediate

11. Remove duplicate integers from a slice.
12. Count how often each word appears in a string.
13. Sort a slice of structs by one of their fields.
14. Read a text file and count its lines.
15. Encode a struct as JSON and decode it again.
16. Write a function that returns a value and an error.
17. Create an interface implemented by two different structs.
18. Write table-driven tests for a function.
19. Build a small HTTP handler.
20. Use a context with a timeout.

## Project Level

21. Build a Todo CLI.
22. Build a JSON-backed notes application.
23. Build a REST API.
24. Build a URL status checker with a worker pool.
25. Build a log file analyzer.
26. Build a small TCP chat server.
27. Build a concurrent image metadata scanner.

------------------------------------------------------------------------

# 91. Questions You Should Be Able to Answer

Before moving beyond beginner Go, make sure you can explain:

## Language basics

-   What is the purpose of `package main`?
-   What is the difference between `var` and `:=`?
-   What is a zero value?
-   What is the difference between a constant and a variable?
-   Why does Go require explicit type conversions?

## Data structures

-   What is the difference between an array and a slice?
-   What do `len` and `cap` return?
-   What does `append` do?
-   How do you check whether a map key exists?
-   What is a struct?
-   What is a pointer?

## Functions and types

-   What is a method receiver?
-   What is the difference between a value receiver and a pointer
    receiver?
-   How does a type implement an interface?
-   What does `any` mean?
-   What are generics and constraints?

## Errors and packages

-   Why does Go commonly return errors as values?
-   What do `errors.Is` and `errors.As` do?
-   What does `defer` do?
-   What is a Go module?
-   What makes an identifier exported?

## Concurrency

-   What is a goroutine?
-   What is a channel?
-   What is the difference between buffered and unbuffered channels?
-   What does `select` do?
-   When should you use a mutex?
-   What is a data race?
-   Why is `time.Sleep` not a reliable synchronization tool?

## Backend development

-   How do you create an HTTP handler?
-   Why should response bodies be closed?
-   What is middleware?
-   Why should a server use timeouts?
-   How can a context cancel work?

## Tooling

-   What does `gofmt` do?
-   How do you run all tests?
-   What does the race detector check?
-   How do you inspect CPU or memory performance?

------------------------------------------------------------------------

# 92. Final Mental Model

Think about Go as several connected layers:

``` text
1. Values and types
   ↓
2. Variables and constants
   ↓
3. Operators and expressions
   ↓
4. Conditions and loops
   ↓
5. Functions
   ↓
6. Arrays, slices, maps, and structs
   ↓
7. Pointers, methods, and interfaces
   ↓
8. Packages and modules
   ↓
9. Errors and resource management
   ↓
10. Files, JSON, and standard-library APIs
   ↓
11. Goroutines, channels, and synchronization
   ↓
12. HTTP services, tests, and tooling
```

The goal is not to memorize syntax.

The goal is to understand:

``` text
Input
  ↓
Data
  ↓
Logic
  ↓
Functions
  ↓
State
  ↓
Output
```

Once these concepts are clear, you can build command-line tools, backend
services, and concurrent applications with Go.

------------------------------------------------------------------------

# 93. Beginner Checklist

Use this checklist as a progress tracker.

## Core

-   [ ] `package main`
-   [ ] `import`
-   [ ] `func main`
-   [ ] Variables
-   [ ] `var`
-   [ ] `:=`
-   [ ] Constants
-   [ ] Basic data types
-   [ ] Zero values
-   [ ] Type conversion
-   [ ] Strings
-   [ ] Runes and UTF-8
-   [ ] Numbers
-   [ ] Operators

## Control Flow

-   [ ] `if`
-   [ ] `else`
-   [ ] `else if`
-   [ ] `switch`
-   [ ] `for`
-   [ ] `range`
-   [ ] `break`
-   [ ] `continue`

## Functions

-   [ ] Function declarations
-   [ ] Parameters
-   [ ] Return values
-   [ ] Multiple return values
-   [ ] Named return values
-   [ ] Variadic functions
-   [ ] Scope
-   [ ] Closures

## Data Structures

-   [ ] Arrays
-   [ ] Slices
-   [ ] `append`
-   [ ] `copy`
-   [ ] Maps
-   [ ] Structs
-   [ ] Pointers
-   [ ] `new`
-   [ ] `make`

## Go Design

-   [ ] Methods
-   [ ] Value receivers
-   [ ] Pointer receivers
-   [ ] Interfaces
-   [ ] Type assertions
-   [ ] Type switches
-   [ ] Composition and embedding
-   [ ] Generics
-   [ ] Packages
-   [ ] Modules
-   [ ] Exported identifiers

## Errors and Standard Library

-   [ ] Error values
-   [ ] `errors.New`
-   [ ] `fmt.Errorf`
-   [ ] Error wrapping
-   [ ] `errors.Is`
-   [ ] `errors.As`
-   [ ] `defer`
-   [ ] `panic` and `recover`
-   [ ] File operations
-   [ ] JSON
-   [ ] Dates and times
-   [ ] Regular expressions
-   [ ] Console input and output

## Concurrency

-   [ ] Goroutines
-   [ ] Wait groups
-   [ ] Channels
-   [ ] Buffered channels
-   [ ] Closing channels
-   [ ] `select`
-   [ ] Mutexes
-   [ ] Context
-   [ ] Race detector

## Backend

-   [ ] HTTP client
-   [ ] HTTP server
-   [ ] Handlers
-   [ ] HTTP methods
-   [ ] Middleware
-   [ ] JSON APIs
-   [ ] Timeouts
-   [ ] Graceful shutdown

## Tooling

-   [ ] `go run`
-   [ ] `go build`
-   [ ] `go test`
-   [ ] `gofmt`
-   [ ] `go vet`
-   [ ] Modules and dependencies
-   [ ] Debugging
-   [ ] Benchmarks
-   [ ] Fuzzing
-   [ ] Profiling
-   [ ] Git

------------------------------------------------------------------------

# 94. Next Step

Do not try to learn the entire guide in one pass.

A practical sequence is:

``` text
Learn a concept
    ↓
Write 3–5 small examples
    ↓
Solve a small exercise
    ↓
Build a mini feature
    ↓
Test and debug it
    ↓
Explain the concept in your own words
    ↓
Move forward
```

The most important milestone is not finishing the notes.

It is being able to open an empty Go project and build something without
following a tutorial line by line.

------------------------------------------------------------------------

# 95. Official Learning Resources

Use official sources as your reference:

-   [A Tour of Go](https://go.dev/tour/) --- interactive introduction to
    the language.
-   [Go Documentation](https://go.dev/doc/) --- installation, tutorials,
    and language documentation.
-   [Effective Go](https://go.dev/doc/effective_go) --- guidance for
    writing idiomatic Go.
-   [Go by Example](https://gobyexample.com/) --- concise examples of
    common language features.
-   [Go Package Documentation](https://pkg.go.dev/) --- documentation
    for standard-library and third-party packages.
-   [Go Blog](https://go.dev/blog/) --- articles about Go, its tools,
    and ecosystem.

Use this guide as a learning path, and use the official documentation to
verify details and explore topics more deeply.
