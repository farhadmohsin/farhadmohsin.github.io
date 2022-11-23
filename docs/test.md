Here's something to check how code snippets and latex work at the same time.


The following code solves the Birthday paradox.
```python
import numpy as np
from matplotlib import pyplot as plt

p = np.zeros(len(range(2,200)))
for g in range(2,100):
    for gg,t in enumerate(range(10000)):
        x = np.zeros(365)
        flag = False
        for i in range(g):
            birthday = np.random.randint(365)
            if(x[birthday] == 1):
                flag = True
                break
            else:
                x[i] = 1
        if(flag):
            p[g] += 1
    print(g, p[g])
    
plt.plot(range(2,100),np.ones(len(range(2,100)))*0.5)
plt.plot(range(2,100),p[:len(range(2,100))]/10000)
plt.xlabel('# of people')
plt.ylabel('Probability that two of them had the same birthday')

plt.show()
```

The task is essentially to find how many people we need so that the probability that two of them had the same birthday is $\ge \frac{1}{2}$.
Let there be $k$ people. Let's check in how many ways everyone would have a unique birthday. That's kind of easy-
$C(n, k) = \frac{n!}{(n-k)!}$ where $n=365$, the total number of days.
So, the probability that at least two share a birthday is $\Pr(A_k) = 1 - \frac{C(n,k)}{n^k}$. The denominator is the total number of ways $k$ people can have birthdays.

Essentially, we're finding the $k$ for which $Pr(A_k) \ge \frac{1}{2}$.