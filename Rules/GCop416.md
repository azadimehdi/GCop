﻿# GCop 416

> *"Merge `else` clause with nested `if` statement"*

## Rule description

To simplify the code and improve the code readability we can combine the `else` clause with nested `if` statement.

## Example

```csharp
if (condition1)
{
    Foo();
}
else
{ 
    if (condition2)
    {
        Bar();
    }
}
```

*should be* 🡻

```csharp
if (condition1)
{
    Foo();
}
else if (condition2)
{
    Bar();
}
```
