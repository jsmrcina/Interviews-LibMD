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
printf("%d\n", *itr2);

// Returns the count of elements in the list
auto size = vec.size();

// Insert elements from array BEFORE the given iterator
// The below appends { 1, 2, 3 } to the end of the list
int arr[] = { 1, 2, 3 };
vec.insert(vec.cend(), arr, arr + std::size(arr));
print_vec(vec);

// Sort vector (not stable, use stable_sort() if needed)
std::sort(vec.begin(), vec.end());
print_vec(vec);

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
print_vec(vec);

// Empties the list
vec.clear();
```

# Linked List
# Queue
# Stack
# Dictionary
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
# Templates