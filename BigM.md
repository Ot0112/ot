# Big M Method (MATLAB)

```matlab
clc;
clear;

M = 1e5;

C = [3 2 0 -M -M];

A = [1 1 -1 1 0;
     2 1  0 0 1];

B = [4;5];

nv = 2;
bv = [4 5];

A = [A B];
C = [C 0];

Zc = C(bv)*A - C;

simplex_table = [A; Zc];
disp(array2table(simplex_table, ...
    'VariableNames', {'x1','x2','s1','a1','a2','sol'}, ...
    'RowNames', {'B1','B2','Zj-Cj'}));

run = true;

while run
    
    ZjCj = Zc(1:end-1);

    if any(ZjCj < 0)
        
        [min_zc, pvtcol] = min(ZjCj);
        
        col = A(:, pvtcol);
        sol = A(:, end);

        if all(col <= 0)
            error('Solution is unbounded');
        end

        ratio = inf(size(A,1),1);

        for i = 1:size(A,1)
            if col(i) > 0
                ratio(i) = sol(i)/col(i);
            end
        end

        [minratio, pvtrow] = min(ratio);

        bv(pvtrow) = pvtcol;

        pvtkey = A(pvtrow, pvtcol);

        A(pvtrow, :) = A(pvtrow, :) / pvtkey;

        for i = 1:size(A,1)
            if i ~= pvtrow
                A(i,:) = A(i,:) - A(i,pvtcol)*A(pvtrow,:);
            end
        end

        Zc = C(bv)*A - C;

        next_table = [A; Zc];
        disp(array2table(next_table, ...
            'VariableNames', {'x1','x2','s1','a1','a2','sol'}, ...
            'RowNames', {'B1','B2','Zj-Cj'}));

    else
        
        run = false;

        fprintf('\nOptimal value = %f\n', Zc(end));

        if any(ismember(bv, [4 5]))
            warning('Artificial variable still in basis → No feasible solution');
        else
            disp('Feasible optimal solution found');
        end
    end
end
````

```
```
