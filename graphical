# Graphical Method (Linear Programming)

## Problem
Maximize:  
Z = 3x₁ + 4x₂  

Subject to:  
x₁ + x₂ ≤ 10  
2x₁ + x₂ ≤ 15  
x₁ + 2x₂ ≤ 16  
x₁, x₂ ≥ 0  

---

## MATLAB Code

```matlab
clc
clear
close all

% Objective
c = [3 4];
A = [1 1; 2 1; 1 2];
b = [10; 15; 16];

Z = @(x1,x2) c(1)*x1 + c(2)*x2;

[m,n] = size(A);

% Plot constraints
x1 = 0:0.1:max(b./A(:,1));

figure
hold on
for i = 1:m
    x2 = (b(i) - A(i,1)*x1)/A(i,2);
    plot(x1,x2,'LineWidth',1.5)
end

% Add x1>=0, x2>=0
A_ext = [A; eye(2)];
b_ext = [b; 0; 0];

pt = [];

% Intersection points
for i = 1:size(A_ext,1)
    for j = i+1:size(A_ext,1)
        M = [A_ext(i,:); A_ext(j,:)];
        if det(M) ~= 0
            sol = M \ [b_ext(i); b_ext(j)];
            pt = [pt sol];
        end
    end
end

pt = unique(pt','rows')';

% Feasible points
FP = [];
Zval = [];

for i = 1:size(pt,2)
    if all(A*pt(:,i) <= b) && all(pt(:,i) >= 0)
        FP = [FP pt(:,i)];
        plot(pt(1,i),pt(2,i),'r*')
        Zval = [Zval Z(pt(1,i),pt(2,i))];
    end
end

% Optimal solution
[opt_val, idx] = max(Zval);
opt_sol = FP(:,idx);

disp(FP)
disp(opt_val)
disp(opt_sol)
