# C++
## Common Datatypes

| Data Type | Size (32-bit system) | Size (64-bit system) | Description |
|-----------|----------------------|----------------------|-------------|
| `bool`    | 1 byte               | 1 byte               | Boolean value (true or false) |
| `char`    | 1 byte               | 1 byte               | Character or small integer |
| `int`     | 4 bytes              | 4 bytes              | Integer |
| `float`   | 4 bytes              | 4 bytes              | Single-precision floating-point |
| `double`  | 8 bytes              | 8 bytes              | Double-precision floating-point |
| `short`   | 2 bytes              | 2 bytes              | Short integer |
| `long`    | 4 bytes              | 8 bytes              | Long integer |
| `long long` | 8 bytes            | 8 bytes              | Longer integer |
| `size_t`  | 4 bytes              | 8 bytes              | Unsigned integer type (for sizes) |
| `wchar_t` | 2 or 4 bytes         | 2 or 4 bytes         | Wide character |
| `void*`   | 4 bytes              | 8 bytes              | Pointer (any type) |

## Math Utils

| Function | Description | Sample Usage |
|----------|-------------|--------------|
| `std::abs` | Returns the absolute value of a number | `std::abs(-5) // returns 5` |
| `std::sqrt` | Calculates the square root of a number | `std::sqrt(16) // returns 4` |
| `std::pow` | Raises a number to a specified power | `std::pow(2, 3) // returns 8` |
| `std::exp` | Calculates the exponential function \( e^x \) | `std::exp(1) // returns 2.71828` |
| `std::log` | Calculates the natural logarithm (base \( e \)) | `std::log(2.71828) // returns 1` |
| `std::log10` | Calculates the logarithm to base 10 | `std::log10(100) // returns 2` |
| `std::sin` | Calculates the sine of an angle (in radians) | `std::sin(3.14159 / 2) // returns 1` |
| `std::cos` | Calculates the cosine of an angle (in radians) | `std::cos(3.14159) // returns -1` |
| `std::tan` | Calculates the tangent of an angle (in radians) | `std::tan(3.14159 / 4) // returns 1` |
| `std::asin` | Calculates the arcsine (in radians) | `std::asin(1) // returns 1.5708` |
| `std::acos` | Calculates the arccosine (in radians) | `std::acos(1) // returns 0` |
| `std::atan` | Calculates the arctangent (in radians) | `std::atan(1) // returns 0.785398` |
| `std::sinh` | Calculates the hyperbolic sine | `std::sinh(1) // returns 1.1752` |
| `std::cosh` | Calculates the hyperbolic cosine | `std::cosh(1) // returns 1.54308` |
| `std::tanh` | Calculates the hyperbolic tangent | `std::tanh(1) // returns 0.761594` |
| `std::ceil` | Rounds a number up to the nearest integer | `std::ceil(2.3) // returns 3` |
| `std::floor` | Rounds a number down to the nearest integer | `std::floor(2.7) // returns 2` |
| `std::round` | Rounds a number to the nearest integer | `std::round(2.5) // returns 3` |
| `std::fmod` | Computes the remainder of the division of two floating-point numbers | `std::fmod(5.3, 2) // returns 1.3` |
| `std::hypot` | Calculates the hypotenuse of a right-angled triangle | `std::hypot(3, 4) // returns 5` |

## Arrays
### 1D
```cpp
#include <memory>

int arr[20];
arr[0] = 1;

int* arr2 = new int[20];
delete[](arr2);

std::unique_ptr<int[]> arr3 = std::make_unique<int[]>(30);
arr3[1] = 0;
```
### 2D
```cpp
#include <memory>

int arr4[3][3] = { { 1, 2, 3 }, { 1, 2, 3 }, { 1, 2, 3 } };

int** arr5 = new int*[3];
arr5[0] = new int[3];
arr5[1] = new int[3];
arr5[2] = new int[3];
delete[](arr5[2]);
delete[](arr5[1]);
delete[](arr5[0]);
delete[](arr5);

std::unique_ptr<std::unique_ptr<int[]>[]> arr6 = std::make_unique<std::unique_ptr<int[]>[]>(3);
arr6[0] = std::make_unique<int[]>(3);
arr6[1] = std::make_unique<int[]>(3);
arr6[2] = std::make_unique<int[]>(3);
```
## Dynamic List
```cpp
#include <algorithm>
#include <string>
#include <vector>

// Lambda for printing a vector
auto print_vec = [](const std::vector<int>& v)
{
    std::for_each(v.cbegin(), v.cend(), [](const auto& elem) {
        printf("%d ", elem);
    });
    printf("\n");
};

// Create a vector of 10 default initialized elements
std::vector<int> vec(10);

// Add element at the end
vec.push_back(10);

// Adds an element through placement-new (prefer this)
vec.emplace_back(10);

// Get element at index 0 (throws if size() is zero)
vec.at(0);

// Erase the element at index zero, returns an iterator pointing to the next element
// O(n)
// Iterator passed to erase must be valid and dereferencable
auto itr = vec.erase(vec.begin());

// Finds an element and returns an iterator to it
// Note: Take care with comparison here
auto itr2 = std::find(vec.cbegin(), vec.cend(), 10);

// Returns the count of elements in the list
auto size = vec.size();

// Insert elements from array BEFORE the given iterator
// The below appends { 1, 2, 3 } to the end of the list
int arr[] = { 1, 2, 3 };
vec.insert(vec.cend(), arr, arr + std::size(arr));

// Sort vector (not stable, use stable_sort() if needed)
std::sort(vec.begin(), vec.end());

// Test if a sorted vector has an element
bool contains = std::binary_search(vec.begin(), vec.end(), 3);

// Get an iterator in O(log(n)) for element into a sorted vector
auto itr3 = std::lower_bound(vec.cbegin(), vec.cend(), 3);
printf("Index of 3 is: %td\n", std::distance(vec.cbegin(), itr3));

// Find the first instance of an element (0) at or after a given index (3)
auto itr4 = std::find(std::next(vec.cbegin(), 3), vec.cend(), 0);
printf("Index of 0 is: %td\n", std::distance(vec.cbegin(), itr4));

// Insert an element before the passed iterator (index 2 below)
vec.insert(std::next(vec.begin(), 2), 5);

// Empties the list
vec.clear();
```
## Linked List
```cpp
#include <algorithm>
#include <string>
#include <list>

// Lambda for printing a list
auto print_list = [](const std::list<std::string>& v)
{
    std::for_each(v.cbegin(), v.cend(), [](const auto& elem) {
        printf("%s ", elem.c_str());
    });
    printf("\n");
};

// Create a linked list from an array
std::string_view arr[] = { "abc", "def", "ghi" };
auto words = std::list<std::string>(arr, arr + std::size(arr));
print_list(words);

// Push an element to the front of the list O(1), prefer to push_front
words.emplace_front("xyz");

// Pop the front element and push it on the back
std::string front = *words.begin();
words.pop_front();
words.emplace_back(front);

// Remove the last element
words.pop_back();

// Remove an element from the end and push it on the front
std::string back = *words.rbegin();
words.pop_back();
words.push_front(back);

// Find the first instance of string ("def")
// To find the last instance of string, use rbegin to rend as range
auto itr1 = std::find(words.cbegin(), words.cend(), "def");
printf("%td, %s\n", std::distance(words.cbegin(), itr1), (*itr1).c_str());

// Insert four strings after the first element (before begin + 1, or index 1)
words.insert(std::next(words.begin()), { "aaa", "aaa", "bbb", "bbb" });

// Erase the element pointed to by iterator
words.erase(words.begin());

// Erase all elements with value "bbb"
words.remove("bbb");

// Erase the first instance of "aaa"
words.erase(std::find(words.begin(), words.end(), "aaa"));
print_list(words);

// Copy to vector
auto vec = std::vector<std::string>(words.begin(), words.end());

// Empty the list
words.clear();
```
## Queue
```cpp
#include <algorithm>
#include <string>
#include <deque>

// Note that cpp has both std::deque and std::queue. The latter is a wrapper and hides some of deque functionality

// Lambda for printing a queue
auto print_queue = [](const std::deque<std::string>& v)
{
    std::for_each(v.cbegin(), v.cend(), [](const auto& elem) {
        printf("%s ", elem.c_str());
    });
    printf("\n");
};

// Insert element into the queue (can also use emplace_front) 
auto q = std::deque<std::string>();
q.emplace_back("aaa");
q.emplace_back("bbb");

// Peek the front element
std::string_view front = q.front();
printf("%.*s\n", static_cast<int>(front.size()), front.data());

// Pop the front element
q.pop_front();
print_queue(q);

// Copy contents to another queue
auto q2 = std::deque<std::string>(q.begin(), q.end());

// Check if queue contains element
auto itr = std::find(q2.cbegin(), q2.cend(), "bbb");
if(itr != q2.cend())
{
    // Do stuff
}

// Clear the queue
q2.clear();
```
## Stack
```cpp
#include <string>
#include <stack>

std::stack<std::string> s;
s.emplace("aaa");

// Cannot print a stack, use std::deque if needed
auto str = s.top();
s.pop();

// Get stack size
s.size();

// Check if empty
s.empty();
```
## Dictionary
```cpp
struct complex
{
    int a;
    int b;

    bool operator==(const complex &other) const
    {
        return (a == other.a
                && b == other.b);
    }
};

template <>
struct std::hash<complex>
{
    std::size_t operator()( const complex& k ) const
    {
        std::size_t res = res * 31 + hash<int>()( k.a );
        res = res * 31 + hash<int>()( k.b );
        return res;
    }
};

// ... snip ... 

// Print all K/V pairs in the map
auto print_map = [](const auto& m)
{
    std::for_each(m.cbegin(), m.end(), [](const auto& pair) {
        printf("%d: %s\n", pair.first, pair.second.c_str());
    });
};

// Create a map (Note: they key must be trivially hashable and comparable via ==, or you have to provide your own)
std::unordered_map<int, std::string> map1;
map1.emplace(1, "abc");

// Using a custom hash function, and defining a custom == operator
std::unordered_map<complex, std::string, std::hash<complex>> map2;
map2.emplace(complex { .a = 5, .b = 7 }, "abc");

// Attempting to insert an already existing element fails (.second of returned pair is false)
auto [itr, success] = map1.emplace(1, "abc");

// Using std::tie for return values is useful too
decltype(map1)::key_type key;
decltype(map1)::mapped_type value;
std::tie(key, value) = (*map1.begin());

// Loop over keys
for(const auto& [key, value] : map1)
{
    printf("%d\n", key);
}

// Get map size
printf("%d\n", (uint32_t)map1.size());

// Remove a kvp
std::size_t num_erased = map1.erase(1);
printf("%d\n", (uint32_t)num_erased);

// Clear the map
map1.clear();

// Get a key or return a default value if it doesnt exist
// See https://stackoverflow.com/questions/40159732/return-other-value-if-key-not-found-in-the-map
```

## Sorted Set
```cpp
template<typename C>
void print(C c)
{
    for(const auto& k : c)
    {
        std::cout << k << " ";
    }
    std::cout << std::endl;
}

int main()
{
    std::set<std::string> sorted_set1;
    std::set<std::string> sorted_set2;

    sorted_set1.emplace("a");
    sorted_set1.emplace("b");
    sorted_set1.emplace("c");

    sorted_set2.emplace("d");
    sorted_set2.emplace("e");
    sorted_set2.emplace("f");

    // Merge two sets into one
    sorted_set1.merge(sorted_set2);
    print(sorted_set1); // a b c d e f
    print(sorted_set2); // <empty>

    // Swap two sets
    sorted_set2.swap(sorted_set1);
    print(sorted_set1); // <empty>
    print(sorted_set2); // a b c d e f

    // Get size
    printf("%zd\n", sorted_set2.size());

    // Union (OR) two sets (only works for sorted set)
    // There are equivalent operations in <algorithm> for difference (subtract), intersection (AND), symmetric_difference (XOR), and includes (subset)
    decltype(sorted_set1) output_set;
    sorted_set1.emplace("a");
    sorted_set1.emplace("h");
    std::set_union(sorted_set1.begin(), sorted_set1.end(), sorted_set2.begin(), sorted_set2.end(), std::inserter(output_set, output_set.begin()));
    print(output_set); // a b c d e f h

    // Clears the set
    output_set.clear();
}
```

## Unsorted Set
```cpp
template<typename C>
void print(C c)
{
    for(const auto& k : c)
    {
        std::cout << k << " ";
    }
    std::cout << std::endl;
}

int main()
{
    std::unordered_set<int> unsorted_set;
    std::multiset<std::string> multi_set;

    unsorted_set.emplace(4);
    unsorted_set.emplace(1);
    unsorted_set.emplace(2);
    unsorted_set.emplace(3);
    unsorted_set.emplace(4);
    print(unsorted_set); // 4 1 2 3

    // Remove an element
    unsorted_set.erase(4);
    print(unsorted_set); // 1 2 3

    // Returns an iterator to the element, or unsorted_set.end() if the element is not found
    // Used for 'contains'. You can also use unsorted_set.count(key) == 0 or 1, or .contains(key) since C++20
    auto itr = unsorted_set.find(2);
    printf("%d\n", *itr);
}
```
## Bit Arrays
```cpp
// Fixed size. For variable size, you can use the template specialization for std::vector<bool> which
// guarantees that each element is one bit.

std::bitset<20> s;
s[5] = 1;
s[10] = 1;
printf("%d\n", s.all()); // 0
printf("%d\n", s.any()); // 1
printf("%d\n", s.none()); // 0
printf("%zd\n", s.count()); // 2
printf("%d\n", s.test(5)); // Tests 5th bit, 1
printf("%d\n", s.test(6)); // Tests 5th bit, 0
s.flip(7); // Flip a single bit
s.flip(); // Flip all the bits
printf("%s\n", s.to_string().c_str()); // 11111111101101011111, note that bit 0 is last (lsb)
printf("%llu\n", s.to_ullong()); // 1047391 == 11111111101101011111, note that bit 0 is last (lsb)
s.set(11); // Set bit 11 to true
s.set(11, false); // Sets bit 11 to false
s.reset(); // Set all bits to zero

// Supports binary AND (&), OR (|), XOR (^) and NOT (!)
// Supports shift left and shift right (<< and >>)
```
## Heaps
```cpp
#include <queue>

// Creates a min heap
priority_queue <int, vector<int>, greater<int> > pq; 
pq.push(5); 
pq.push(1); 
pq.push(10); 
pq.push(30); 
pq.push(20);

// Creates a max heap
priority_queue <int, vector<int>> pq2;

// Note that pq does not know how to re-heapify when an internal element is modified
```
## Collection Utils
## Threading
```cpp
std::vector<uint8_t> written;
std::vector<uint8_t> read;
BinaryStream b(256, 100);

// Create two suspended threads that are passed the arguments as shown as references
std::jthread t1(WriteFunc, std::ref(b), std::ref(written));
std::jthread t2(ReadFunc, std::ref(b), std::ref(read));

// Wait on the threads to exit
t1.join();
t2.join();

// You can also do cancellation with jthreads (request a stop and then wait for join)
std::jthread sleepy_worker([](std::stop_token stoken)
{
    for (int i = 10; i; --i)
    {
        std::this_thread::sleep_for(300ms);
        if (stoken.stop_requested())
        {
            std::cout << "Sleepy worker is requested to stop\n";
            return;
        }
        std::cout << "Sleepy worker goes back to sleep\n";
    }
});

sleepy_worker.request_stop();
sleepy_worker.join();

// There is no thread pool built-in to standard library, but you can use something like https://github.com/bshoshany/thread-pool
```

```cpp
// For thread safety, you can use mutexes + locks
#include <mutex>

// A mutex that can be taken recursively by a thread
std::recursive_mutex _mutex;

// A unique RAII lock that will release once it goes out of scope
std::unique_lock<std::recursive_mutex> _lock(_mutex);
```

## Enumeration
### Spans
```cpp
#include <span>

// Make a span from an array starting at position total_writte_bytes and being of length of the remaining data past total_remaining bytes
std::span(data + total_written_bytes, std::size(data) - total_written_bytes)

// Function which accepts a span
uint32_t Write(std::span<uint8_t> data, uint32_t start_pos)

// Spans have two members, the data and the size
const uint8* d = data.data()
const size_t s = data.size()
```
## Random
```cpp
#include <random>
std::random_device r;
std::default_random_engine e1(r()); // Usually Mersenne 19937
std::uniform_int_distribution<int> uniform_dist(0, std::numeric_limits<uint8_t>::max());
int x = uniform_dist(e1);

// TODO: Add various distribution types

```
## Sleeping
```cpp
#include <chrono>
std::this_thread::sleep_for(std::chrono::milliseconds(10));
```
## Async
## Testing Framework
## Object Comparison
## Asserts
```cpp
#include <cassert> // For C-style assert

// Depends on NDEBUG macro
assert(1 == 1, "This should never fail");

// Prefer this in C++ as it is not a macro and thus has less quirks
static_assert(1 == 1, "This should never fail");
```
## Additional Language Specific Topics
### Function pointer syntax



### Packing



### Type Slicing
### Operator Overloads
See [Operator Overloading Signatures](/languages/CPP_operator_overloads.md)
### Templates

#### Function Template
Function templates allow you to create functions that can operate with different data types. Here's a simple example of a function template to find the maximum of two values:

```cpp
template<typename T>
T max(T x, T y) {
    return (x > y) ? x : y;
}
// Usage:
// max<int>(3, 5);
// max<double>(3.5, 2.5);
```

#### Class Template
Class templates are useful for defining classes that can handle data of any type. Here's an example of a generic `Box` class that can store a value of any type:

```cpp
template<typename T>
class Box {
public:
    T value;
    Box(T val) : value(val) {}
    T getValue() { return value; }
};
// Usage:
// Box<int> intBox(10);
// Box<double> doubleBox(3.14);
```

#### Variadic Template
Variadic templates allow functions to accept any number of arguments. Here's an example that prints all given arguments:

```cpp
template<typename... Args>
void printer(Args... args) {
    (std::cout << ... << args) << std::endl;
}
// Usage:
// printer(1, 2, 3, "Hello", 3.14);
```

#### Template Specialization
Template specialization allows you to define a specific implementation of a template for a particular data type. Here's an example of specializing a `min` function for `const char*`:

```cpp
template<typename T>
T min(T x, T y) {
    return (x < y) ? x : y;
}

template<>
const char* min<const char*>(const char* x, const char* y) {
    return strcmp(x, y) < 0 ? x : y;
}
// Usage:
// min<int>(2, 3);
// min<const char*>("abc", "def");
```

#### Template Template Parameter
Template template parameters allow you to pass a template as a parameter to another template. Here's an example using a container class:

```cpp
template<template<typename> class Container, typename T>
class MyClass {
    Container<T> data;
};
// Usage with a template class like std::vector:
// MyClass<std::vector, int> myClassInstance;
```

Each of these examples demonstrates different aspects of C++ templates, highlighting their flexibility and power in generic programming. Templates are central to writing efficient and reusable code in C++.

### Moving and additional constructors
#### Additional Constructors
```cpp
// Copy
BinaryBuffer(const BinaryBuffer& other) = delete; // Can also be default

// Move
BinaryBuffer(BinaryBuffer&& other) = delete; // Can also be default
```
#### Moving
### Virtual functions and VFTs
### Numeric limits
| Type                                                    | Availability    |
|---------------------------------------------------------|-----------------|
|   ```template<> class numeric_limits<bool>;```               |                 |
|   ```template<> class numeric_limits<char>;```             |                 |
|   ```template<> class numeric_limits<signed char>;```        |                 |
|   ```template<> class numeric_limits<unsigned char>;```      |                 |
|   ```template<> class numeric_limits<wchar_t>;```          |                 |
|   ```template<> class numeric_limits<char8_t>;```          |  (since C++20)  |
|   ```template<> class numeric_limits<char16_t>;```         |  (since C++11)  |
|   ```template<> class numeric_limits<char32_t>;```         |  (since C++11)  |
|   ```template<> class numeric_limits<short>;```            |                 |
|   ```template<> class numeric_limits<unsigned short>;```     |                 |
|   ```template<> class numeric_limits<int>;```              |                 |
|   ```template<> class numeric_limits<unsigned int>;```       |                 |
|   ```template<> class numeric_limits<long>;```             |                 |
|   ```template<> class numeric_limits<unsigned long>;```      |                 |
|   ```template<> class numeric_limits<long long>;```          |  (since C++11)  |
|   ```template<> class numeric_limits<unsigned long long>;``` |  (since C++11)  |
|   ```template<> class numeric_limits<float>;```            |                 |
|   ```template<> class numeric_limits<double>;```           |                 |
|   ```template<> class numeric_limits<long double>;```        |                 |

For example, to find the max value, you can use:

```cpp
int max_value = std::numeric_limits<int>::max;
```

### Printf
#### Format Specifiers
| Specifier | Type                               |
|-----------|------------------------------------|
| %c        | character                          |
| %d        | decimal (integer) number (base 10) |
| %e        | exponential floating-point number  |
| %f        | floating-point number              |
| %i        | integer (base 10)                  |
| %o        | octal number (base 8)              |
| %s        | a string of characters             |
| %u        | unsigned decimal (integer) number  |
| %x        | number in hexadecimal (base 16)    |
| %%        | print a percent sign               |
| \%        | print a percent sign               |

### Decltype
### Constexpr
### Noexcept
### PIMPL
### Concepts