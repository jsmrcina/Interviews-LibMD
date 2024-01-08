# C#

# Common Datatypes
# Math Utils
```cs
Math.Abs(f);
Math.Ceiling(f);

```


# Arrays
## 1D
### Example
```cs
var arr = new int[10];
```

## 2D
### Square
```cs
int[,] arr = new int[5, 10];
int rowsOrHeight = arr.GetLength(0);
int colsOrLength = arr.GetLength(1);
int numDimensions = arr.Rank;

int totalEls = arr.Length;
```
### Jagged

# Dynamic List
```cs
using System.Collections.Generic;

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
```cs
using System.Collections.Generic;

var ll = new LinkedList<T>();

// Create a linked list from an array
string[] words = { "one", "two", "three" };
var ll2 = new LinkedList<string>(words);

// Add an item to the front of the list
ll2.AddFirst("four");

// Move a node from the front to the back
LinkedListNode<string> front = ll2.First;
ll2.RemoveFirst();
ll2.AddLast(front);

// Remove the last node
ll2.RemoveLast();

// Move a node from the back to the front
LinkedListNode<string> back = ll2.Last;
ll2.RemoveLast();
ll2.AddFirst(back);

// Find the last node containing the string "two"
LinkedListNode<string> node = ll2.FindLast("two");

// Add a node after or before another node, these will throw InvalidOperationException if the node already belongs to the list
ll2.AddAfter(node, "abc");
ll2.AddBefore(node, "def");

// Remove a node by reference
ll2.Remove(node);

// Remove the first node with a specificed value
ll2.Remove("three");

// Copy linked list to array
string[] copy = new string[ll2.Count];
ll2.CopyTo(copy, 0);

// Print elements
foreach(string s in ll2)
{
    Console.WriteLine(s);
}

// Clear the list
ll2.Clear();

```

# Queue
```cs
using System.Collections.Generic;

var queue = new Queue<string>();

// Enqueue an item into the queue
queue.Enqueue("one");

// Print all elements of the queue
foreach(var el in queue)
{
    Console.WriteLine(el);
}

// Dequeue the front element, InvalidOperationException if empty
var el = queue.Dequeue();

// Peek at the front of the queue, InvalidOperationException if empty
var el2 = queue.Peek();

// Copy queue to another queue
var queue2 = new Queue<string>(queue.ToArray());

// Check if queue contains element
var contains = queue.Contains("two");

// Clear the queue
queue.Clear();

// Try variants of Dequeue and Peek
string item;
var success = queue.TryDequeue(out item);
success = queue.TryPeek(out item);
```

# Stack
```cs
using System.Collections.Generic;

var stack = new Stack<string>();

// Push an element into the stack
stack.Push("one");

// Print all elements of the stack 
foreach(var el in stack)
{
    Console.WriteLine(el);
}

// Pop an element off of the stack
var el = stack.Pop();

// Peek at the top of the stack
var el2 = stack.Peek();

// Copy stack to another stack
var stack2 = new Stack<string>(stack.ToArray());

// Check if stack contains element
var contains = stack.Contains("two");

// Clear the stack
stack.Clear();

// Try variants of Pop and Peek
string item;
var success = stack.TryPop(out item);
success = stack.TryPeek(out item);
```

# Dictionary
```cs
using System.Collections.Generic;

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
foreach(string v in vals)
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

// Get a key or return a default value if it doesn't exist
var def = CollectionExtensions.GetValueOrDefault(dict, "key", "default");
Console.WriteLine(def);
```

# Sorted Set
# Unsorted Set
```cs
var set = new HashSet<T>();

// Union with another collection (set union coll)
set.UnionWith(coll);

// Intersect with another collection (set intersect coll)
set.IntersectWith(coll);

// Subtract another collection from the set (set - coll)
set.ExceptWith(coll);

// Exclusive or with another collection (set xor coll)
set.SymmetricExceptWith(coll);

// Add element to set, returns false is element is already present
set.Add(x);

// Clears the set
set.Clear();

// Checks if set contains X
set.Contains(x);

// Ensures set capacity is at least new_cap
set.EnsureCapacity(new_cap);

// Is set a subset of coll, but not equal to coll
set.IsProperSubsetOf(coll);

// Is set a supserset of coll, but not equal to coll
set.IsProperSupersetOf(coll);

// Is set a subset or equal to coll
set.IsSubsetOf(coll);

// Is set a superset or equal to coll
set.IsSupersetOf(coll);

// Returns true if set and coll share at least one common element
set.Overlaps(coll);
```

# Bit Arrays
# Object Comparison
## IEquatable

# Collection Utils
# Threading (Pools)
# Enumeration
# Async
# Testing Framework
# Object Comparison
## IComparer



## IEquatable
# Additional Language Specific Topics
## LINQ