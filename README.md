# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return; // 1
    else {
        mystery(n / 3);  // T(n/3)
        var count = 0;   // 1
        mystery(n / 3);  // T(n/3)
        for(var i = 0; i < n*n; i++) {   // n*n
            for(var j = 0; j < n; j++) {   // n
                for(var k = 0; k < n*n; k++) {  // n*n
                    count = count + 1;  // 1
                }
            }
        }
        mystery(n / 3);  // T(n/3)
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

Solution modeled after what we did in class:

After annotating the code with runtime, they add up as follows:

1 + T(n/3) + 1 + T(n/3) + (n*n * n * n*n * 1) + T(n/3) = 3T(n/3) + $n^5$ + 3

The base case runtime is T(n) if n <= 1

If n > 1 then T(n) = 3T(n/3) + n^5 + 3

Substituting for T(n/3):

    T(n/3) = 3T((n/3)/3) + (n/3)^5 + 3

    T(n/3) = 3T(n/(3)^2) + (n/3)^5 + 3

    Substituting again 

    T(n) = 3(3T(n/(3)^2) + (n/3)^5 + 3) + n^(5) + 3

    T(n) = 9T(n/9) + 3(n^(5)/3^(5)) + 9 + n^(5) + 3

    T(n) = 9T(n/9) + (n^(5)/3^(4)) + 9 + n^(5) + 3

Substituting for T(n/9)

    T(n/3) = 3T((n/9)/3) + (n/9)^(5) + 3

    T(n/3) = 3T(n/27) + (n^(5)/9^(5)) + 3

    Substituting again 

    T(n) = 9(3T(n/27)+ (n^(5)/9^(5)) + 3) + (n^(5)/3^(4)) + 9 + n^(5) + 3

    T(n) = 27T(n/27)+ 9(n^(5)/9^(5)) + 27 + (n^(5)/3^(4)) + 9 + n^(5) + 3

    T(n) = 27T(n/27)+ (n^(5)/9^(4)) + (n^(5)/3^(4)) + n^(5) + 3 + 9 + 27

27T(n/27) can be represented as 3^(k)T(n/3^(k))

(n^(5)/9^(4)) + (n^(5)/3^(4)) + n^(5) can be represented as $\sum_{i=0}^{k} (\frac{n^5}{3^{4(i-1)}})$

3 + 9 + 27 can be represented as $\sum_{i=0}^{k} (3^i)$

All together that's T(k) = 3^(k)T(n/3^(k)) + $\sum_{i=0}^{k} (\frac{n^5}{3^{4(i-1)}})$ + $\sum_{i=0}^{k} (3^i)$

To solve for base case we solve for k(n/3^(k)) = 1 

    n/3^(k) = 1

    log(base 3)n = k

Substituting k back in:

    T(n) = 3^(log(base 3)n)T(n/(3^(log(base 3)n))) + $n^(5)\sum_{i=0}^{log(base 3) (\frac{1}{3^4(i-1)}) + \sum_{i=0}^{log(base 3)} (3^i)$

Simplifies to T(n) = n(1) + n^(5)

Further simplifies to T(n) = n^(5)

"I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice."
