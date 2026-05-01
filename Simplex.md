# Simplex Method (MATLAB)

```matlab
clc
clear

A = [3,1,1,0; 1,2,0,1];
B = [7;12];
C = [-3,4,0,0];
nv = 2;
bv = nv+1 : size(A,2);

A = [A B];
C = [C 0];

Zc = C(bv)*A - C;
simplex_table = [A ; Zc];

array2table(simplex_table, 'VariableNames',{'x1','x2','s1','s2','sol'}, 'RowNames',{'B1','B2','Zj-Cj'})

run = true;

while run
    ZjCj = Zc(1:end-1);
    
    if any(ZjCj < 0)
        [min_Zc , pvt_col]= min(ZjCj);
        sol = A(:,end);
        col = A(:, pvt_col);
        
        if all(col <= 0)
            fprintf('Solution is unbounded\n')
            break
        else
            ratio = zeros(size(A,1),1);
            for i = 1:size(A,1)
                if col(i) > 0
                    ratio(i) = sol(i)./ col(i);
                else
                    ratio(i) = inf;
                end
            end
            [min_ratio, pvt_row]= min(ratio);
        end
        
        bv(pvt_row) = pvt_col;
        pvt_key = A(pvt_row, pvt_col);
        A(pvt_row,:) = A(pvt_row,:)./ pvt_key;
        
        for i = 1:size(A,1)
            if i~= pvt_row
                A(i,:) = A(i,:) - A(i,pvt_col)* A(pvt_row,:);
            end
        end
        
        Zc = C(bv)*A - C;
        next_simplex_table = [A; Zc];
        
        array2table(next_simplex_table, 'VariableNames',{'x1','x2','s1','s2','sol'}, 'RowNames',{'B1','B2','Zj-Cj'})
    else
        run = false;
        fprintf('Final optimal has been obtained and its value is %f \n', Zc(end))
    end
end
````

```
```
