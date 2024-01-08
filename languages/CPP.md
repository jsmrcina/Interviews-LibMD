# C++
# Common Datatypes
# Math Utils
# Arrays
## 1D
```cpp
#include <memory>

int arr[20];
arr[0] = 1;

int* arr2 = new int[20];
delete[](arr2);

std::unique_ptr<int[]> arr3 = std::make_unique<int[]>(30);
arr3[1] = 0;
```
## 2D
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
# Dynamic List
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
# Linked List
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
# Queue
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
# Stack
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
# Dictionary
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
map1_type map1;
map1.emplace(1, "abc");

// Using a custom hash function, and defining a custom == operator
std::unordered_map<complex, std::string, std::hash<complex>> map2;
map2.emplace(complex { .a = 5, .b = 7 }, "abc");

// Attempting to insert an already existing element fails (.second of returned pair is false)
auto [itr, success] = map1.emplace(1, "abc");

// Using std::tie for return values is useful too
map1_type::key_type key;
map1_type::mapped_type value;
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

# Sorted Set
# Unsorted Set
# Bit Arrays
# Collection Utils
# Threading (Pools)
# Enumeration
# Async
# Testing Framework
# Object Comparison
# Additional Language Specific Topics
# Type Slicing
# Operator Overloads
# Templates