﻿# GCop 520

> *"Write it as `foo.Intersects(bar)`"*

## Rule description

The `Intersect` method returns the common elements between two collections. It is faster and more readable than a manual implementation of that logic using `Any` with `Contains`.

## Example
```csharp
var foo = new List<string>();
var bar = new List<string>();
var res = foo.Any(f => bar.Contains(f));
```

*should be* 🡻

```csharp
var foo = new List<string>();
var bar = new List<string>();
var res = foo.Intersect(bar).Any();
```