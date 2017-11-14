# Print Fibonacci

F0=0，F1=1，Fn=F(n-1)+F(n-2)

---
Return a number
```py
def f(n):
    a, b = 0, 1
    for i in range(0, n):
        a, b = b, a + b
    return a
```

---
Return a list

```py
def fib(n):
    if n == 1:
        return [1]
    if n == 2:
        return [1, 1]
    fibs = [1, 1]
    for i in range(2, n):
        fibs.append(fibs[-1] + fibs[-2])
    return fibs
```