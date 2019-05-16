## IEnumberable vs IEmumerator

Code Example of how to use:
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

    // IEnumerator which could use while to loop access all items.
    IEnumerator<int> ienumerator = oyears.GetEnumerator();
    while(ienumerator.MoveNext())
    {
        Console.WriteLine(ienumerator.Current);
    }
```

NOTE: The differnece between the two is that IEnumerator knows the current state when passing as a paramenter.

## See difference
If we have two methods Iterate09to10 and Iterate11to13 as following codes:
```csharp
       static void Iterate09to10(IEnumerable<int> e)
        {
            foreach (var item in e)
            {
                Console.WriteLine(item);
                if (item > 2010)
                    Iterate11to13(e);
            }
        }

        static void Iterate09to10(IEnumerator<int> e)
        {
            while(e.MoveNext())
            {
                Console.WriteLine(e.Current);
                if(e.Current>2010)
                {
                    Iterate11to13(e);
                }
            }
        }

        static void Iterate11to13(IEnumerable<int> e)
        {
            foreach (var item in e)
            {
                Console.WriteLine(item);                
            }
        }

        static void Iterate11to13(IEnumerator<int> e)
        {
            while (e.MoveNext())
            {
                Console.WriteLine(e.Current);                
            }
        }
```

if we call
```csharp
IEnumerable<int> ienum = (IEnumerable<int>)oyears;
Iterate09to10(ienum); // output wired sequences because it iterates from the very beginning each time to call the Iterate11to13(IEnumberable<int>)
```
the output is:
2009
2010
2011
2009
2010
2011
2012
2013
2012
2009
2010
2011
2012
2013
2013
2009
2010
2011
2012
2013

else if we call
```csharp
IEnumerator<int> ienumerator = oyears.GetEnumerator();
Iterate09to10(ienumerator); // output all oyears values because it knows the state
```
the output is
2009
2010
2011
2012
2013