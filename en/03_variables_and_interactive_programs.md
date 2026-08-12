# Variables and interactive programs

In this module you will learn to write interactive Python programs.

An interactive program communicates with the use: it reads and processes input and generates output accordingly.

An example of an interactive program would be a program that asks the user to enter two numbers, calculates their sum and shows the sum to the user. In this case the input is read from the user (for example numbers 2 and 3), the input is processed by calculating the sum and the output is shown to the user (sum of the numbers is 5).

## Printing

Let's start with Python's printing function called print. The following program prints out the text "Hello, world!":

```python
print('Hello, world!')
```

The printing is handled with a Python built-in function called print. The argument to the function is called inside brackets. In this case the message to print is a string literal "Hello, world!". A string literal is a string that is written directly into the program code. A string literal is written inside apostrophes ' ' or quotation marks " ". The same program could also be written as shown here:

```python
print("Hello, world!")
```

What if you need to print out a message that includes apostrophes or quotation marks? The solution is to write the symbol inside a string literal using the other alternative symbol to enclose the string literal:

```python
print('"Hello", said Joe')
```

When a program has multiple print statements, a line break is printed after each of them automatically:

```python
print("Good")
print("morning")
```

Output:

```monospace
Good
morning
```

The above program shows one of the basic structures of programming: sequences. By default, statements are executed in the order they have been written in the program code. Other basic structures are selections and loops. They will be introduced later.

You can also print a message with line breaks with a single line of code: It is possible to write a line break symbol `\n` inside a string literal. You can get the same output as before by writing:

```python
print("Good\nmorning")
```

## Inputs, variables, and assignment statements

You have now learned how to create simple programs that generate the same output on each run. However, usually it is required that a program reads inputs from the users and uses the input to execute tasks.

Let's write a program the asks the user for their name and then greets the user with their name. This can be done as follows:

```python
user = input('Enter your name: ')
print("Nice to meet you, " + user + "!")
```

The user input is read using the built-in input function. The function receives the text to be printed on the screen as an argument. The text should tell the user what information they are expected to enter.

The built-in input function waits for input from the user's keyboard. The user ends the input with the Enter key. When the input has been give, the value of the input function is the string entered by the user.

The string must be saved into a _variable_ so that it can be used later in the program. Here we are using a variable called _user_. User input is saved into the memory of the computer and can be fetched from memory using the name of the variable. The name of a variable is a sort of a handle or name tag that can be used to retrieve the value from memory.

A variable can be given a value using an assignment statement. The assignment statement uses an equals symbol (=). The name of the variable is on the left side and the expression that determines the value to be assigned to the variable is written on the right side.

### More about variables and the assignment operator

In programming, **variables** can be thought of as named boxes that store information. This information can be numbers, text, or more complex structures. When stored data is needed later in a program, it can be accessed simply by referring to the box by its name.

For example, suppose we want to store the color of something. We create a variable named `color` and assign it the value `"blue"` like this:

```python
color = "blue"
```

In the example above, `color` is a **variable** whose **value is the string** `"blue"`.

Variable names may contain letters, digits, and underscores, but they cannot start with a digit or contain spaces. As good programming practice, give variables descriptive names; this makes the code easier to read.

The assignment operator (`=`) is written as a single equals sign (`=`). Its job is to set the value of the expression on the right-hand side as the value of the variable on the left-hand side — in other words, to store the value in the memory slot reserved for the variable.

You can visualize the example like this:

```txt
  Variable        Assignment operator      Value
+-----------+    +-----------------+    +----------+
|   color   | <- |        =        | <- | "blue"   |
+-----------+    +-----------------+    +----------+
```

When Python executes the line `color = "blue"`, it performs the following steps:

1. Evaluate the expression on the right-hand side of the assignment and store the result temporarily. In this case the expression is the simple string literal `"blue"`, but the expression can also include more complex operations, such as reading input with the `input()` function.
2. Create a variable named `color` and allocate memory for it. If the variable `color` has already been created earlier in the program, the existing memory slot is used.
3. Store the value computed in step 1 (`"blue"`) as the value of the variable `color`. If the variable already existed, its previous value is overwritten and lost.

A variable’s value can be changed at any time during program execution. For example:

```python
points = 50  # points is now 50
print(points)  # prints: 50

points = 120  # now points is 120
print(points)  # prints: 120
```

In this case `points` was initially `50`, but the **assignment operator** (`=`) changed its value to `120`.

### Using Variables in Output

Let's now take a closer look at the print statement.

If we only wanted to print the name entered by the user, we could replace the lower line with the following:

```python
print(user)
```

Note that now `user` is the name of a variable. It is not a string literal, and it is not written inside quotation marks.

However, we want the program to print a complete greeting text instead of just the name. The string being printed can be constructed from substrings by joining the parts together using the plus sign (+). The lower line of the original program constructs the output from three parts:

1. String literal "Nice to meet, "
2. The value of the _user_ variable
3. String literal "!"

The program works as follows:

```monospace
Enter your name: Joanne
Nice to meet you, Joanne!
```

## Variable Type

Above, variables were assigned simple values such as a string and an integer.

In Python, variables do not need to be declared in advance, nor does their type need to be specified. Instead, the type of a variable is determined automatically as a result of an assignment statement. The type indicates what kind of data the variable refers to: is the variable's value, for example, a string or a number?

Python has three basic variable types (primitive data types):

- string (_string_)
- number (_number_), which can be an integer (int), floating-point number (float), or complex number (complex)
- boolean (_boolean_), which can be `True` or `False`

In addition, other Python data structures can be assigned to variables, such as:

- list (_list_)
- tuple (_tuple_)
- dictionary (_dictionary_)

In addition, a variable can be a reference to an object. Lists, tuples, dictionaries, and object references will be covered later in the course. Next, we will take a closer look at numeric and string data types.

### Numeric Data Type

Python's numeric data type has three subtypes: integer (for example, 4 or 12756413000), floating-point number (for example, 7.28 or 4.0), and complex number (for example, 3-2i). Next, we create four variables: an integer is assigned to the first, a long integer to the second, a floating-point number to the third, and a complex number to the fourth. We then print the values of all four variables, as well as the real and imaginary parts of the complex number separately:

```python
first = -9
second = 12_456_123_180
third = 4.973
fourth = -4 + 2j

print(first)
print(second)
print(third)
print(fourth)
print(fourth.real)
print(fourth.imag)
```

When entering an integer, the digits can be grouped using the underscore symbol, as was done above for the variable toka. However, this is not mandatory. More memory is allocated for large integers than for ordinary integers.

Note that in a complex number, Python uses the letter j as the symbol for the imaginary part instead of the letter i, which is conventionally used in mathematics.

The example program produces the following output:

```monospace
-9
12456123180
4.973
(-4+2j)
-4.0
2.0
```

### String Data Type

A string is a data type used to represent text. It is a sequential series of characters, such as letters, numbers, and punctuation marks. In Python, strings are created by surrounding text with either single (`'`) or double (`"`) quotation marks. This provides flexibility when quotation marks themselves appear inside the string.

**Examples of strings:**

```python
name = "Petra"  # Double quotes
greeting = 'Hello, world!'  # Single quotes
number_as_string = "12345"  # Even though it contains digits, it is text because it is enclosed in quotes
empty_string = ""  # Empty string
sentence1 = "Bob said: 'Hello!'"  # Double quotes, single quotes as part of the string
sentence2 = 'Bob replied: "Hi!"'  # Single quotes, double quotes as part of the string
```

#### Internal Representation of Characters

All characters stored and processed by a computer are converted into numerical codes that the computer can "understand". In Python, all characters are represented as Unicode characters. _Unicode_ is a standard that defines its own character codes for most of the world's writing systems.

Text containing _Unicode_ characters can be stored on a computer using different encoding methods, or character encodings, such as _UTF-8_. An encoding is a set of rules for how this conversion is performed. In its simplest form, an encoding is a list of characters and the numbers corresponding to them, such as the old and limited _ASCII_ encoding.

## Mathematical Operations and Type Conversion

Variables and constants can be used in mathematical operations. The order of operations can be indicated with parentheses when necessary.

The arithmetic operations are addition (`+`), subtraction (`-`), multiplication (`*`) and division (`/`). In addition, there is the modulo operator (`%`) for the remainder, as well as the floor division operator (`//`) and the exponential operator (`**`).

The program below asks for a temperature in Fahrenheit and converts it to Celsius. The conversion is done by subtracting 32 from the Fahrenheit temperature and multiplying the difference by the constant 5/9.

```python
fahrenheit_str = input("Enter a temperature in Fahrenheit: ")
fahrenheit = float(fahrenheit_str)
celsius = (fahrenheit-32)*5/9
print("The temperature in Celsius: " + str(celsius))
```

The program works as follows:

```monospace
Enter a temperature in Fahrenheit: 102
The temperature in Celsius: 38.888888888888886
```

Notice that the value returned by the input function is always interpreted as a string even if it contains numbers only. A string can be converted into a float with the _float_ function or into an integer with the _int_ function.

Furthermore, a number can be converted into a string with the _str_ function. In the example program the conversion must be done to add the calculated Celsius degrees to the output string. Both parts of the print must be strings.

Functions will be covered in more detail later.

## Output Formatting

Sometimes we want to control how output is formatted: how many decimal places floating-point numbers are displayed with, or how much space, for example, is reserved for a string.

This can be done using a so-called formatted string literal, in which the string being printed contains formatting codes.

Let's look at this through an example. We will modify the output of the last example program so that the Celsius degrees are always shown with two decimals.

```python
print(f"The temperature in Celsius: {celsius:6.2f}")
```

Note that the argument of the `print` function call now begins with the letter `f`, which indicates that the string being printed contains expressions to be formatted. Without the letter f, the string literal would be printed exactly as it appears in the program code, including the curly braces.

The expression to be formatted, together with its formatting code, is written inside curly braces. In the example, the expression being formatted is the value of the variable `celsius`.

The formatting code in this case is `6.2f`. The letter `f` indicates that the expression is printed as a floating-point number. The notation `6.2` preceding the `f` specifies that the result is displayed in a field six characters wide, and that the floating-point number is displayed with two decimal places.

Here are examples of formatting codes:

- `.5f`: floating-point number with five decimal places
- `10.2f`: floating-point number with two decimal places in a field ten characters wide
- `<20s`: string in a field 20 characters wide, aligned to the left
- `8d`: integer in a field eight characters wide

Writing formatting codes is optional. Nevertheless, using formatted string literals makes it easier to combine numeric and string-formatted output because it is not always necessary to use `str` functions and other conversion functions. Above, we could simply print the Celsius temperature without a formatting code:

```python
print(f"The temperature in Celsius: {celsius}")
```

The same formatted string literal can include multiple expressions to format and their possible format codes. The following program outputs the value of two natural constants: pi and Euler's number (e) so that the name of each constant is printed in a field of 12 characters and their corresponding values are printed in a field of 10 characters using 5 decimals:

```python
import math

print(f"{'Pi':12s}:{math.pi:10.5f}")
print(f"{'e':12s}:{math.e:10.5f}")
```

Above, the mathematical constants pi and Euler's number were printed using Python's mathematics library. They were referenced using the expressions `math.pi` and `math.e`. The mathematics library can be used when the library import statement `import math` has been added to the beginning of the program.

Lastly, Python offers multiple ways of formatting outputs. Formatted string literals introduces here are quite a new way of formatting that has been available since Python version 3.6. It is enough to learn one good way of formatting output, but you might see alternative methods in online learning materials and when looking at program code made by others. These alternative methods are:

1. using the `str.format()` function
2. using format specifiers and a list of expressions (% operator notation)
3. using template strings

The alternative methods listed above are not covered here. More information on the subject can be found in the Python 3 language documentation: [https://docs.python.org/3/tutorial/inputoutput.html](https://docs.python.org/3/tutorial/inputoutput.html)

---

[The next module covers the if conditional structure.](04_conditional_structure.md)

---
