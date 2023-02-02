#Exploring of Cairo 1.

Here are some simple examples to show you how Cairo 1 works. As I continue to develop Cairo 1, I will add more examples.
To run the examples, use the following command:

```bash
cargo run --bin cairo-run -- -p ./<path_file> 
```

Here's an example:
```bash
cargo run --bin cairo-run -- -p ./src/var/var_1.cairo 
```

Note: The Cairo 1 version is still in alpha, so it's very likely that the syntax will change.
The base template is from the people at Extropy. You can see it [here](https://github.com/ExtropyIO/cairo-1-template).
To make these examples, I based them on the repositories.
* [Cairo Examples](https://github.com/starkware-libs/cairo/tree/main/examples)
* [Quaireaux](https://github.com/keep-starknet-strange/quaireaux)

### Contents
- Variables
    - [Let](#let)
    - [Mut](#mut)
    - [Ref](#ref)
    - [Constant](#constant)
    - [Bool](#bool)
- [Debugging](#debugging)
    - [Print felt](#print-felt)
- [Conditional Statements](#conditional)
    - [Equality Operator (==)](#operator)
    - [Comparison Operators (< > <= >=)](#operators)
    - [AND Operator](#and)
    - [OR Operator](#or)
    - [Negation Operator (!)](#negation)
- [Arrays](#arrays)
    - [Creating, Appending, and Accessing Elements](#new)
    - [Length (len)](#len)
    - [Pop Front](#pop)
- [Enumerations](#enum)
- [Match Expressions](#match)

## Variable

<a id="let"></a>
#### Let
Declaring a Variable. Once a value is assigned, it cannot be changed. It becomes a constant.
```rust
fn main() -> felt {
    let a = 1;
    a
}
```

<a id="mut"></a>
#### Mut
Declaring a Mutable Variable. Otherwise, the value cannot be modified again.
```rust
fn main() -> felt {
    let mut b = 2;
    b = 3
    b
}
```
<a id="ref"></a>
#### Ref
Modifying a Variable That is Passed as a Reference.
```rust
fn main() -> felt {
    let mut n = 1;
    b(ref n);
    n
}

fn b(ref n: felt){
    n = 1;
}
```
<a id="constant"></a>
#### Constant
Declaring global constant.
```rust
const NUM: felt = 15;
fn main() -> felt {
    NUM
}
```

<a id="bool"></a>
#### Bool
```rust
fn main() -> bool {
    let a = 25;
    if a == 15 {
        return bool::True(());
    } else {
        return bool::False(());
    }
}
```

<a id="debugging"></a>
## Debugging

<a id="print-felt"></a>
#### Print felt
```rust
fn main() -> felt {
    let a = 15;
    debug::print_felt('a: ');
    debug::print_felt(a);
    a
}
```

<a id="conditional"></a>
## Conditional Statements

<a id="operator"></a>
#### Equality Operator (==)
```rust
fn main() {
    let x = 25;
    if x == 0 {
        debug::print_felt('x is equal to 0');
    } else if x == 1 {
        debug::print_felt('x is equal to 1');
    } else {
        debug::print_felt('x is not equal to 0 or 1');
    }
}
```

<a id="operators"></a>
#### Comparison Operators (< > <= >=)
```rust
fn main() {
    let x = 10;
    let y = 20;
    if x < y {
        debug::print_felt('x is less than y');
    }
    if x <= y {
        debug::print_felt('x is less than or equal to y');
    }
    if x > y {
        debug::print_felt('x is greater than y');
    }
    if x >= y {
        debug::print_felt('x is greater than or equal to y');
    }
}
```
<a id="and"></a>
#### AND Operator
```rust
fn main() {
    let x = 25;
    if x != 0 & x >= 25 {
        debug::print_felt('x is not equal to 0');
        debug::print_felt('and');
        debug::print_felt('x is greater than or equal to 25');
    } else {
        debug::print_felt('x is equal to 0');
    }
}
```

<a id="or"></a>
#### OR Operator
```rust
fn main() {
    let x = 0;
    if x != 0 | x >= 25 {
        debug::print_felt('x is not equal to 0');
        debug::print_felt('or');
        debug::print_felt('x is greater than or equal to 25');
    } else {
        debug::print_felt('x is equal to 0');
        debug::print_felt('or');
        debug::print_felt('x is less than 25');
    }
}
```
<a id="negation"></a>
#### Negation Operator (!)
A function can be called in the conditional if
```rust
fn main() {
    let age = 15;
    if !is_greater(age) {
        debug::print_felt('is less');
    } else {
        debug::print_felt('is greater');
    } 
}

fn is_greater(age: felt) -> bool {
    age >= 18
}
```

<a id="arrays"></a>
## Arrays

<a id="new"></a>
#### Creating, Appending, and Accessing Elements
```rust
use array::ArrayTrait;

fn main() {
    let mut arr = ArrayTrait::new();
    arr.append(10);
    arr.append(11);
    arr.append(12);
    let pos2 = arr.at(2_usize);
    debug::print_felt(pos2);
}
```
<a id="len"></a>
#### Length (len)
```rust
use array::ArrayTrait;

fn main() -> usize {
    let mut arr = ArrayTrait::new();
    arr.append(10);
    arr.append(11);
    arr.append(12);
    arr.len()
}
```

<a id="pop"></a>
#### Pop Front
```rust
use array::ArrayTrait;

fn main() {
    let mut arr = ArrayTrait::new();
    arr.append(10);
    arr.append(11);
    arr.append(12);
    
    match arr.pop_front() {
        Option::Some(x) => {
            debug::print_felt(x);    
        },
        Option::None(_) => {
            debug::print_felt('None');
        },
    };
}
```

<a id="enum"></a>
## Enumerations

```rust
enum MyEnumShort {
    a: felt,
    b: felt
}

fn main() -> felt {
    let es0 = MyEnumShort::a(10);
    match_short(es0)
}

fn match_short(e: MyEnumShort) -> felt {
    match e {
        MyEnumShort::a(x) => {
            x
        },
        MyEnumShort::b(x) => {
            x * 2
        },
    }
}
```

<a id="match"></a>
## Match Expressions
Match with a non-zero value is not supported.
```rust
fn main() -> felt {
    let a = 25;
    match_test(a)
}

fn match_test(a: felt) -> felt {
    match a {
        0 => 15, 
        _ => 0,
    }
}
```