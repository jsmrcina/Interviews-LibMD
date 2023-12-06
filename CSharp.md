# C#

# Common Datatypes
# Math Utils
# Arrays
## 1D
### Example
```
var arr = new int[10];
```

## 2D
### Square
### Jagged

# Dynamic List
## Example
```
// Can pass i32 for initial capacity, or another enumerable
var list = new List<T>(); 

// Adds an element to the end, O(1) amortized, O(n) worst
list.Add(t);

// Returns 't', TODO: not exists?
var tPrime = list[0];

// Removes item at index 0
list.RemoveAt(0); 

// Returns true if contains t
bool containsT = list.Contains(t);

// Returns the count of elements in the list
var numEls = list.Count;

// Adds elements from collection to end of list
list.AddRange(coll);

// Sorts the list using the default comparer, may use insertion, heapsort, or quicksort under the covers. Unstable
list.Sort();

// Only works on a sorted list, binary searches and returns index
list.BinarySearch(t);

// Searches for the specified object, starting at index
list.IndexOf(t, index);

// Inserts an item at the specified index. Throws ArgumentOutOfRangeException if index greater than count
list.Insert(index, T);

// Prints all items in the list
foreach(var item in list)
{
    Console.WriteLine(item);
}

// Clear the list
list.Clear();
```


# Linked List
## Example
```
var ll = new LinkedList<T>();
```

# Queue
## Example
```
var queue = new Queue<T>();
```

# Stack
## Example
```
var stack = new Stack<T>();
```

# Dictionary
## Example
```
var dict = new Dictionary<string, string>();

// Add a key to the dictionary, throws ArgumentException if key already exists
dict.Add("key", "value");

// Add a key to the dictionary, does not throw exceptions
var success = dict.TryAdd("key", "value");

// Get the value for key "key", throws KeyNotFoundException if it doesn't exist
var str = dict["key"];

// Get the value for key, but returns false if it doesn't exist
string value = "";
var exists = dict.TryGetValue("key", out value);
if(!exists) { /* Do stuff */ }

// Test if key exists before inserting using ContainsKey
if(!dict.ContainsKey("key")) { /* Do stuff */ }

// Iterate KV pairs
foreach(KeyValuePair<string, string> kvp in dict)
{
    Console.WriteLine(kvp.Key + " " + kvp.Value);
} 

// Get only the values
Dictionary<string, string>.ValueCollection vals = dict.Values;
foreach(string v in values)
{
    Console.WriteLine(v);
}

// Get only the keys
Dictionary<string, string>.KeyCollection keys = dict.Keys;
foreach(string k in keys)
{
    Console.WriteLine(k);
}

// Get the count of elements in the dictionary
var count = dict.Count;

// Removing a kvp, TODO: What if doesn't exist
dict.Remove("key");

// Clear the dictionary
dict.Clear();

// TODO: Get or default




```

# Set
## Example
```
var set = new HashSet<T>();
```

# Bit Arrays
# Object Comparison
## IEquatable

# Collection Utils
# Threading (Pools)
# Enumeration
# Async
# Additional Language Specific Topics
## LINQ