# Steepest Descent Method (MATLAB)

```matlab
clc
clear all

f=@(x1,x2) x1.^2+2*x2.^2;
grad_f=@(x1,x2) [2*x1 ; 4*x2];

x=[3;3];
max_iter=100;
alpha=0.1;
tol=1e-6;

for iter = 1:max_iter
    gradient=grad_f(x(1),x(2));
    if norm(gradient)<tol
        fprintf("Converged at iteration %d\n", iter);
        break;
    end
    x=x-alpha*gradient;
end

fprintf("Answer (minimum point):\n x1: %.6f \n x2: %.6f",x(1),x(2));
````

```
```
