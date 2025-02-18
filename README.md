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
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

Sol:
There are 3 recursive calls, each of which have an input size of n/3 so the time spent there is:
    $'3T(n/3)'$
Then there are 3 nested loops:

 The most inner loop runs n*n times 
 
 The middle loop runs n times 
 
 The outer loop runs n*n times
 
The total work done in these loops is $O(n^2 * n * n^2) = O(n^5)$

This leaves the recurrence relation to be 
    $T(n) = 3T(n/3) + n^5$ 

*Note: there cannot be an asymptotic expression in a recurrence relation*
    
    
Looking at [This page in Geeks for Geeks](https://www.geeksforgeeks.org/recurrence-relations-a-complete-guide/) and using the Master Theorem which is a systematic way of solving recurrence relations with the form: $'T(n) = aT(n/b) + f(n)'$ The page gives an example similar to the relation of our mystery function: $T(n) = 3T(n/2) + n^2

a = 3, b = 2, k = 2, p = 0 

b^k = 4. So, a < b^k and p = 0 [Case 3.(a)] 

T(n) = O(n^k log^pn) 

T(n) = O(n^2)$ 

In our case, a = 3, b = 3, and k = 5 so, a tight big $O$ bound would be: $O(n^5)$

I used Geeks for Geeks as a reference otherwise: "I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice."
This was my submission from last semester
