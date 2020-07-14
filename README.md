# learn-new-languages
Helpful self-assigned tasks &amp; reference implementation when learning programming languages

**Some of these tasks may exceed the limits of the language.**

## Recursive fibonacci closure/function

Construct a closure that computes the n-th fibonacci number using recursive algorithm.

*Please note that, in some languages, recursive closure may not be posible.*

```c++
#include <iostream>
#include <functional>

using namespace std;

int main() {
  std::function<int(int)> fib = [&fib](int i) -> int {
    return (i <= 2) ? 1 : fib(i - 1) + fib(i - 2);
  };
  for (int i = 1; i <= 10; i++) {
    cout << "fib(" << i << ")=" << fib(i) << endl;
  }
  return 0;
}
```

### Futher: anonymous recursion without Y combinator

```c++
#include <iostream>
#include <functional>

using namespace std;

int main() {
  // this code can be simplified using the non-standard compound literals
  // however, compound-literals is forbidden by ISO C++
  struct fib_generator {
    int operator()(int n) {
      return (n < 2) ? n : (*this)(n-1) + (*this)(n-2);
    }
  };
  std::function<int(int)> fib = fib_generator {};
  for (int i = 1; i <= 10; i++) {
    cout << "fib(" << i << ")=" << fib(i) << endl;
  }
  return 0;
}
```
