## Introduction
```cs
Console.Beep();
```
This command will make the terminal beep when the line is reached.

### Write/WriteLine
```cs
Console.Write() // Will write text without the new line
Console.WriteLine() // Will write text with a new line char after
```

### ReadKey
When we don't want a program to end until the user hits a key in the console, we can use:
`Console.ReadKey()`

### Type Casting
```cs
double a = 3.14;
int b = Convert.ToInt32(a)
```
- Converting a double to an integer will get rid of any decimal values.
- `a.GetType()` will get the type of `a`. Here, it would be `System.Double`. `System.Int32`, etc
`Convert.To$DataType$()` is the basic syntax

### User Input
```cs
Console.WriteLine("What's your name?")
String name = Console.ReadLine()
```
The input will be stored inside of `name`.

```cs
Console.WriteLine("What's your age?")
int age = Convert.ToInt32(Console.ReadLine())
```
This will get the user inputted string, convert it to int, and store it inside `age`.

### (Pseudo) Random Numbers
To create random numbers, we will need to initialize a `Random` object:
```cs
Random RandomObj = new Random();
random.Next(); // Will generate a integer between 0 and integer upper limit
random.Next(1, 7); // Will generate a integer between [1, 7) <- not including 7
random.NextDouble(); // Will generate a number between 0 and 1
```