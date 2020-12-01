import numpy as np
from sympy import *
import math
x = symbols("x")
g = 1 / ( 1 + x)
dg = g.diff(x)
d2g = dg.diff(x)
d3g = d2g.diff(x)
d4g = d3g.diff(x)
dg = lambdify(x, dg)
d2g = lambdify(x, d2g)
d3g = lambdify(x, d3g)
d4g = lambdify(x, d4g)

def f(x):
    return 1 / ( 1 + x)

def trapezoidanlRule(a, b, n):
    c = [0] * (n + 1)
    h = (b - a) / n
    c[0] = a
    for i in range (1, n + 1):
        c[i] = a + i * h
        
    sum = f(c[0])
    for j in range(1, n):
        sum += 2 * f(c[j])

    sum += f(c[n])
    integration = sum * h / 2
    
    print(integration)
    M = d2g(c[0])
    
    for i in range (1, n+1):
        if (M < abs(d2g(c[i]))):
            M = d2g(c[i])
            
    epsilon = (M / 12) * (b-a) * math.pow(h, 2)
    print(M)
    print(epsilon)

def simpsonRule(a, b, n):
    c = [0] * (n + 1)
    h = (b - a) / n
    c[0] = a
    for i in range (1, n + 1):
        c[i] = a + i * h
    sum = f(c[0])
    for j in range(1, n):
       if(j % 2 != 0):
           sum += 4 * f(c[j])
       else:
           sum += 2 * f(c[j])

    sum += f(c[n])
    integration = sum * h / 3
    
    print(integration)
    M = d4g(c[0])
    
    for i in range (1, n+1):
        if (M < abs(d4g(c[i]))):
            M = d4g(c[i])
            
    epsilon = (M / 180) * (b-a) * math.pow(h, 4)
    print(M)
    print(epsilon)
    
    

if __name__ == "__main__":
    
      simpsonRule(0, 1, 10)
      trapezoidanlRule(0, 1, 100)
