# BFS Method (Basic Feasible Solution)

## Problem
Maximize:  
Z = 6x₁ + 5x₂  

Subject to (Standard Form):  
x₁ + x₂ + s₁ = 5  
3x₁ + 2x₂ + s₂ = 12  
x₁, x₂, s₁, s₂ ≥ 0  

---

## MATLAB Code

```matlab
clc
clear

% Objective
C = [6 5 0 0];

% Constraints
A = [1 1 1 0;
     3 2 0 1];
b = [5; 12];

z = @(x) C*x;

[m,n] = size(A);

basicsol = [];
bfsol = [];

comb = nchoosek(1:n,m);

% Generate basic solutions
for i = 1:size(comb,1)
    idx = comb(i,:);
    x = zeros(n,1);
    B = A(:,idx);
    
    if det(B) ~= 0
        sol = B\b;
        x(idx) = sol;
        
        basicsol = [basicsol x];
        
        if all(sol >= 0)
            bfsol = [bfsol x];
        end
    end
end

disp(bfsol)

% Optimal solution
cost = z(bfsol);

[opt_val, index] = max(cost);
opt_sol = bfsol(:,index);

disp(opt_val)
disp(opt_sol)
