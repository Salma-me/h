# C++ Programs to Find the Nth Term of the Fibonacci Sequence.
### *What is Fibonacci sequence?*
The Fibonacci sequence is a set of integers that follows the rule that each number is equal to the sum of the preceding two numbers. It starts commonly with a zero, followed by a one, then by another one, and then by a series of steadily increasing numbers. 
The next few values in the sequence are shown below:

![picture of Fibonacci series](https://media.geeksforgeeks.org/wp-content/uploads/20211212213411/fib2-660x256.png)

Considering that each number is a **term**, the Fibonacci sequence can be
defined by the following three equations:
* F(0)  =  0 (applies only to the first integer).
* F(1)  =  1 (applies only to the second integer).
* F(N)  =  F(N-1) + F(N-2) (applies to all other integers).

**Here is different methods to find the Nth term of the Fibonacci series using C++:**

### *Method 1: Using Recursion*

```r
//Fibonacci Series using Recursion
#include <iostream>
using namespace std;
int fib(int N) {
    if (N <= 1)
        return N;
    return fib(N - 1) + fib(N - 2);
}
 
int main() {
    int N;
    cout << "Enter an integer number"<<endl;
    cin >> N;
    cout << fib(N);
    return 0;
}
```

##### **Time complexity**: It's O(2^n), or *exponential*, since each function call calls itself twice. That means for example if n = 6 the algorithm will have to go approximately through 64 computing steps to get the 6th Fibonacci number. For n = 20 or 30 and so on the computing steps greatly increases.   
##### **Space complexity**: O(n), or *Linear*, as the number of calls increases the call stack size increases because every previous call will be waiting for the next one to execute and these calls should be interlinked together at the same time.

### *Method 2: Using Dynamic Programming*

```r
#include <iostream>
using namespace std;
class calc {
public:
int fib(int n) {     
    // Declare an array to store Fibonacci numbers.
    // 1 extra to handle case, n = 0
    int f[n+1];
    int i;
    // 0th and 1st number of the series are 0 and 1
    f[0] = 0;
    f[1] = 1;
    for(i = 2; i <= n; i++) {
       //Add the previous 2 numbers in the series and store it
       f[i] = f[i - 1] + f[i - 2];
    }
    return f[n];
    }
};
 int main () {
     calc v;
     int n;
     cout <<"Enter an integer number"<<endl;
     cin >> n;
    cout << v.fib(n);
    return 0;
}
```

To avoid recursively repeating function calls, dynamic Programming is a strategy to store the output of these function calls (with specific input ) so the one can easily lookup into the stored values when needed again.

##### **Time complexity**: O(n)
##### **Space complexity**: O(n)

### *Method 3: Using Space Optimization*

```r
// Fibonacci Series using Space Optimized Method
#include <iostream>
using namespace std;
int F(int N) {
    int a = 0, b = 1, c, i;
    if( N == 0)
        return a;
    for(i = 2; i <= N; i++)
    {
       c = a + b;
       a = b;
       b = c;
    }
    return b;
}
 int main() {
    int N;
    cout << "Entr an integer number"<<endl;
    cin >> N;
    cout << F(N);
    return 0;
}
```

##### **Time complexity**: O(n).To find nth Fibonacci number, nth iterations are performed.
##### **Space complexity**: O(1). It is a method with an effective use of space since all we need to get the next Fibonacci number is the previous two numbers.

### *Method 4: Using Matrix Multiplication*

```r
#include <iostream>
using namespace std;
// Helper function that multiplies 2 matrices F and M of size 2*2, and puts the multiplication result back to F[][]
void multiply(int F[2][2], int M[2][2]);
// Helper function that calculates F[][] raise to the power n and puts the result in F[][]
// Note that this function is designed only for fib() and will not work as general power function
void power(int F[2][2], int n);
int fib(int n) {
    int F[2][2] = { { 1, 1 }, { 1, 0 } };
    if (n == 0)
        return 0;
    power(F, n - 1);
    return F[0][0];
}
void multiply(int F[2][2], int M[2][2]) {
    int x = F[0][0] * M[0][0] + F[0][1] * M[1][0];
    int y = F[0][0] * M[0][1] + F[0][1] * M[1][1];
    int z = F[1][0] * M[0][0] + F[1][1] * M[1][0];
    int w = F[1][0] * M[0][1] + F[1][1] * M[1][1];
    F[0][0] = x;
    F[0][1] = y;
    F[1][0] = z;
    F[1][1] = w;
}
void power(int F[2][2], int n) {
    int i;
    int M[2][2] = { { 1, 1 }, { 1, 0 } };
    // n - 1 times multiply the matrix to [(1,0),(0,1)]
    for(i = 2; i <= n; i++)
        multiply(F, M);
}
int main() {
    int n ;
     cout << "Enter an integer number"<<endl;
     cin >> n;
    cout << fib(n);
    return 0;
}
```

The formula for finding the Nth element of a Fibonacci series using matrix multiplication is shown below. It states that if we multiply the matrix M by itself n times, the element in the first row and column in the resulting matrix is the (n+1)th Fibonacci number. Since we want the nth Fibonacci number we only need to multiply matrix M by itself (n-1) times, in another way M^(n-1).

![Formula for Finding the Nth Element of a Fibonacci series using Matrix Multiplication.](https://prepinsta.com/wp-content/uploads/2022/01/CodeCogsEqn-1.webp)

##### **Time complexity**: O(n)
##### **Space complexity**: O(1), the program has a constant space allocation.

### *Method 5: Using Binet's Formula*

Fn = {[(sqrt(5) + 1)/2] ^ n} / sqrt(5)

Above Formula gives correct result only upto for n<71. Because as we move forward from n>=71, rounding error becomes significantly large. Although, using floor function instead of round function will give correct result for n=71. But after from n=72, it also fails. For further information about Binet's Formula click [here](https://r-knott.surrey.ac.uk/Fibonacci/fibFormula.html#section1).

```r
// C++ Program to find nth fibonacci Number
#include<iostream>
#include<cmath>
using namespace std;
int fib(int n) {
  double phi = (1 + sqrt(5)) / 2;
  return round(pow(phi, n) / sqrt(5));
  // the round function gives the nearest integer to its argument.
  //As n gets larger, the value of Phi^n/sqrt(5) is almost an integer.
}
int main () {
  int n ;
  cout << "Enter an integer number"<<endl;
  cin >> n;
  cout << fib(n);
  return 0;
}
```

##### **Time complexity**: O(log(n)). Calling pow() function to calculate nth power of phi takes O(log(n)) time.
##### **Space complexity**: O(1). No operation uses auxiliary space.

#### ***To summarize here is a table of all methods and its time and space complexity described in Big O Notation:***

| | Method | Time complexity | Space complexity |
|:--:|:-------|:---------------:|:----------------:|
|1| Using Recursion | O(2^n) | O(n) |
|2|Using Dynamic Programming | O(n) | O(n) |
|3|Using Space Optimization | O(n) | O(1) |
|4|Using Matrix Multiplication | O(n) | O(1) |
|5|Using Binet's Formula | O(log(n)) | O(1) |

#### *References:*
- https://en.wikipedia.org/wiki/Fibonacci_number.
- https://prepinsta.com/cpp-program/finding-the-nth-term-of-the-fibonacci-series/.
- https://pages.cs.wisc.edu/~vernon/cs367/notes/3.COMPLEXITY.html#application.
- https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/.

> This page was built by Salma Ashraf Ahmed Fathy.
> section 1, bench number 31.
