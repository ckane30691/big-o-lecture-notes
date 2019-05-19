# Big-O Analysis

---
* Constant
* Logarithmic
* Square Root
* Linear
* Log-Linear
* Quadratic
* Polynomial
* Exponential
* Factorial

---

It's all a matter of counting!

---


```ruby
def example1(n)
  n = 3n + 2
  n += 40n
  n**5
end
```

Note:
O(1) because it takes the same number of operations to raise 2^2 as it does to raise 10^2.  Remember it's all about how does the number of operations grow as the input size grows.

---
```ruby
def example2(n)
  n.times { |i| p i }
end
```

Note:
O(n) because as n grows in size the number of times this program has to loop will increase linearly with n.

---
```ruby
def example3(n)
  t = 0
  n.times do
    n.times do  
      t += 1
    end
  end
  p t
end
```

Note:
O(n^2) because for every iteration of the original n, we have to do an additional n operations.
---

```ruby
def example4(n)
  t = 0
  (1..n).each do |i|
    i.times do  
      t += 1
    end
  end
  p t
end
```
Note:
O(n^2) Typical pattern. The number of things to do each time is not always n, so it is less than `n^2` in total, right? Sort of...

If you count it all out, we are adding up from `1..n`. This results in `n(n+1)/2`, which is still `n^2`.
---

```ruby
def example5(n)
  while n > 0
    n /= 2
  end
end
```

Note:
Typical of logarithmic time complexity. Reducing the data set by a factor each time. Remember MergeSort?

Why was it `O(nlogn)`?  Any time we reduce our search space or iteration in half that's going to be typical of a logarithmic time complexity.  Said another way, as our search space doubles, our number of iterations only increase by 1.

---

```ruby
def example6(n)
  return 1 if n == 0
  example6(n-1)
end
```
Note:
O(n) time and O(n) space due to the recursive call stack.

---

```ruby
def example7(n)
  return 1 if n.even? || n < 0
  example7(n-2)
end
```

Note:
Best Case: Constant
Worst Case: Linear

---

```ruby
def example8(n)
  return 1 if n == 0
  example8(n-1) * example8(n-1)
end
```

Note:
This is a branching recursive tree. Since each call results in two more calls, we multiply by two for each level of the tree.

If we input 5, the total number of calls is `2^(n+1) - 1` => `O(2^n)`

---

```ruby
def example9(n)
  return 1 if n == 0
  n.times { p n } if n.odd?
  example9(n-1) * example9(n-1)
end
```

Note:
 Example 9 is a branching tree which gives us a lower bound of `O(2^n)`

 However, there is extra stuff going on. Sometimes we do extra stuff that depends on `n`. Here is where you should mention upper bounding.

 If there were `n` things going on for each recursive call, then our time complexity would be `O(n*2^n)` NB: May be ```O(n + 2^n)```. This is the upper bound

 Counting up exactly how much stuff is going on, given that only odd numbers result in extra work, is outside the scope of what you should expect to be able to do. It is a fun math challenge to try though!

---
```ruby
def example10(n)
  t = 0
  n.times do
    n.times do  
      t.to_s.split('').each { |el| p el }
      t += 1
    end
  end
  p t
end
```

Note:
The key question here is: What is contained in the double loop?

For each iteration we do extra work equal to the number of digits of the current number. Do you see that?

The number of digits is roughly equal to `log10(n)`

If we count everything up we get

```
Sum from i=1 to n^2 of:
log10(i)
```

This should give us a Time Complexity of around `O(n^2 * log10n^2)`; once we normalize the base of the logarithm and discard the constant factor this is `O(n^2 * logn)`.

For `n=100` the total number of prints is 38,890;


---

```ruby
def example11(n)
  n.times do |i|
    j = i
    while j < n
      j *= 2
    end
  end
end
```

---
`Sum from i=1 to n of:
1 + log(n/i)`

`O(n)`

Understanding why the summation results in linear time is not very important. In fact, you wouldn't be expected to know that. However, being about to say that some constant stuff plus something logarithmic is happening `n` times is important. Furthermore, you should be able to notice that it is **better** than `log(n)` each time because the starting point of `j` increases and thus multiplies more rapidly.
---

```ruby
def example12(n)
  p n
  n.times do
    example11(n-1)
  end
end
```

---
Factorial: `n=5` results in 4 more calls, each of which results in 3 more calls...etc.
