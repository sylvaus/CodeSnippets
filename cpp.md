# Cpp Snippets

### Time code
```
#include <chrono>
#include <iostream>
auto start = std::chrono::high_resolution_clock::now();
// Code to be timed
auto finish = std::chrono::high_resolution_clock::now();
std::chrono::duration<double> elapsed = finish - start;
std::cout << "Code ran for " << elapsed.count() << "s\n";
```
