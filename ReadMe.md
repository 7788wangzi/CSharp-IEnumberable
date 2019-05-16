## IEnumberable vs IEmumerator

Code Example:
```csharp
    List<int> oyears = new List<int>();
    oyears.Add(2009);
    oyears.Add(2010);
    oyears.Add(2011);
    oyears.Add(2012);
    oyears.Add(2013);

    // IEnumerable which could use foreach to loop access all items.
    IEnumerable<int> ienum = (IEnumerable<int>)oyears;
    foreach (int i in ienum)
    {
        Console.WriteLine(i);
    }

    // IEnumberator which could use while to loop access all items.
    IEnumerator<int> ienumerator = oyears.GetEnumerator();
    while(ienumerator.MoveNext())
    {
        Console.WriteLine(ienumerator.Current);
    }
```