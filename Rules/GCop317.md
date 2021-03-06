﻿# GCop 317

> *"This code is repeated 'repetition count' times in this method. If its value remains the same during the method execution, store it in a variable. Otherwise define a method (or Func<T> variable) instead of repeating the expression. 'expression type'"*

## Rule description

We should write as short and simple code as it is possible. Repetition will reduce the clarity of the code.

## Example 1

CastExpression

```csharp
if(condition)
{
    Bar((int)Status.Wait, "this");
}
else 
{
    Bar((int)Status.Wait, "that");
}

```

*should be* 🡻

```csharp
public void MyMethod()
{
    int waitStatus = (int)Status.Wait;
    
    if(condition)
    {
        Bar(waitStatus, "this");
    }
    else 
    {
        Bar(waitStatus, "that");
    }
}
```

## Example 2

ReturnStatement

```csharp
public ServerResult MyMethod()
{
    if(something == otherthing) return new ServerResult { Success = false, Message = "sometext" };
    try
    {
        ...
    } 
    catch
    {
        return new ServerResult { Success = false, Message = "sometext" };
    }
}
```

*should be* 🡻

```csharp
public ServerResult MyMethod()
{
    if(something == otherthing) return CreateError();
    
    try
    {
        ...
    } 
    catch
    {
        return CreateError();
    }
}

ServerResult CreateError() => new ServerResult { Success = false, Message = "sometext" };
```

*OR it can even be an inline method inside the parent method* 🡻

```csharp
public ServerResult MyMethod()
{
    ServerResult error() => new ServerResult { Success = false, Message = "sometext" };
    
    if(something == otherthing) return error();
    
    try
    {
        ...
    } 
    catch
    {
        return error();
    }
}
```