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

#### My Answer

I found the recurrence relation as $3T(n/3) + n^5$, because the mystery function makes three recurence calls, dividing the input by three for each one. The remainder of the code is then a set of three nested loops, iterating through the input n^2, n, and n^2 times, for a total of n^5, or a constant value time that can be ignored in asymptotic analysis. The base case would be $T(n)=1$ for n <= 1 because the function returns, constant time, for any input less than or equal to one. 

$T(n) = 1,  n <= 1$

$T(n) = 3T(n/3) + n^5,  n > 1$

$3T(n/3) + n^5$

$3(3T((n/3)/3) + (n/3)^5) + n^5$ = $9T(n/9) + 3(n/3)^5 + n^5$

$9(3T((n/9)/3) + (n/9)^5) + 3(n/3)^5 + n^5$ = $27T(n/27) + 9(n/9)^5 + 3(n/3)^5 + n^5$

$3^iT(n/3^i) +  \sum_{k=1}^i 3^{k-1}(n/3^{k-1})^5$

$n/3^i = 1$

$i = log_3(n)$

$nT(1) + \sum_{k=1}^{log_3(n)} 3^{k-1}(n/3^{k-1})^5$

$n + \sum_{k=1}^{log_3(n)} 3^{k-1}(n/3^{k-1})^5$ 

$n + n^5 + 3n^5/3^5 + 9n^5/9^5 + ... + (1/3)n(n^5/((1/3)n)^5)$ 

$n + n^5 + n^5/3^4 + n^5/9^4 + ... + n^5/(1/3)^4n^4$

$n + n^5 + n^5/3^4 + n^5/9^4 + ... + n/(1/3)^4$

No matter how the summation is expanded, the result is various $n^5$ terms multiplied by some constants summed together. The constants are ignored during asymptotic analysis, and only the fastest growing term is selected, which would be $n^5$. This is the dominant term no matter how the summation is expanded, as the remainder terms are all either less than or equal to n^5. Therefore the mystery function is an element of $O(n^5)$. 

### Sources and Plagiarism 

I certify that I have listed all sources used to complete this exercise, including the use of any Large Language Models. All of the work is my own, except where stated otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is suspected, charges may be filed against me without prior notice.

