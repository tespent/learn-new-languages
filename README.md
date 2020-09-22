# learn-new-languages
Helpful self-assigned tasks &amp; reference implementation when learning programming languages

**Some of these tasks may exceed the limits of the language.**

## Container iteration

Construct and iterate over a container (list or vector) of structures using as less code as possible. For example, in C++ 17 ...

```c++
#include <iostream>
#include <vector>

struct person {
  std::string name;
  int age;
  char gender;
};

int main() {
  std::vector<person> group = {
    { "Alice", 20, 'F' },
    { "Bob", 21, 'M' },
    { "Cindy", 22, 'F' },
  };

  for (const auto &[name, age, gender] : group) {
    std::cout << name << " " << age << " " << gender << std::endl;
  }
}
```

... or in Rust ...

```rust
struct Person {
  name: std::string::String,
  age: i32,
  gender: char,
}

fn main() {
  let group = vec![
    Person {name: String::from("Alice"), age: 20, gender: 'F'},
    Person {name: String::from("Bob"), age: 21, gender: 'M'},
    Person {name: String::from("Cindy"), age: 22, gender: 'F'},
  ];
  for Person {name, age, gender} in group {
    println!("{} {} {}", name, age, gender)
  }
}
```

## Recursive fibonacci closure/function

Construct a closure that computes the n-th fibonacci number using recursive algorithm.

*Please note that, in some languages, recursive closure may not be posible.*

```c++
#include <iostream>
#include <functional>

int main() {
  std::function<int(int)> fib = [&fib](int i) -> int {
    return (i <= 2) ? 1 : fib(i - 1) + fib(i - 2);
  };
  for (int i = 1; i <= 10; i++) {
    std::cout << "fib(" << i << ")=" << fib(i) << std::endl;
  }
  return 0;
}
```

### Futher: anonymous recursion without Y combinator

```c++
#include <iostream>
#include <functional>

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
    std::cout << "fib(" << i << ")=" << fib(i) << std::endl;
  }
  return 0;
}
```
