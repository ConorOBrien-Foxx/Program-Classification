# Program Classification
A repo for some definitions of certain classes of programs.

## 0: Preamble
This is a document containing the definitions for classes of programs--that is, a program can be described as belonging to a class if and only if it satisfies the described requirements.

A program is said to solve a problem `X` if that is its purpose. For example, the following ruby program solves the task of printing "Hello, World!":

```ruby
puts "Hello, World!"
```

### 0.1: definitions

 1. A program `P` _yields_ a value(s) `v` by returning it as the return result of a function, printing to STDOUT, etc. All of the following yield `42` in JavaScript:
    ```javascript
    x => 42;
    console.log(42);

 2. A concatenation of two programs `P` and `Q` is the simple appending of the source code of `Q` to the end of `P`, and is represented as `P + Q`, or `PQ` when clear.

 3. A program `P` is a subset of a program `Q` if and only if one can insert characters into `P` to transform it make it equal to `Q`. To illustrate this, observe the following two programs. The first is a subset of the second one.

    ```javascript
    f = x => x * x
    ```

    ```javascript
    f = (x) => x * x;
    ```

 4. `#P` is the cardinality or "size" of `p`. The cardinality of the following program is `37`.

    ```python
    print("Python 3 is better than 2...")
    ```

### 0.2: types of programs
    
A quine is a program `P` that yields its own source code, that is, `P`. These are some quines implemented in various languages.

 * JavaScript (ES6)
    ```javascript
    f=_=>`f=${f}`
    ```
 * Ruby
    ```ruby
    a="a=%p;puts a%%a";puts a%a
    ```
 * [J](http://codegolf.stackexchange.com/questions/69/golf-you-a-quine-for-great-good/26324#26324)
    ```J
    ',~@,~u:39',~@,~u:39
    ```
    

## 1: `N`-fragile programs

**Variables:**

 - `P` - the program
 - `X` - the problem it solves
 - `N` - the degree of fragality of the program.

**Formula:** `F_N(P,X)`

Program `P` is `N`-fragile if and only if all subsets of `P` of length `#P - N` error.

For example, the following is a 1-fragile quine in JavaScript:

```javascript
f=(n=b=`f=${f}`)=>(a=(n)==`f=${f}`,n=0,a)&(n!=b)?b:q
```

I verified it using this program:

```javascript
const oneFragile = (s) => {
    for(let i = 0; i < s.length; i++){
        try {
            let prog = s.slice(0, i) + s.slice(i + 1);
            eval(prog)();
            return prog;
        } catch(e){}
    }
    return true;
}
```