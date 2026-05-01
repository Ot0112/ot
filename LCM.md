# Least Cost Method (LCM) - Transportation Problem (MATLAB)

```matlab
clc;
clear;

s=[5,8,7,16];
d=[7,9,18];
c=[2,7,4;3,3,1;5,5,4;1,6,2];

m = size(c,1);
n = size(c,2);

if sum(s)==sum(d)
    fprintf("P is balanced\n");
else
    if sum(s) > sum(d)
        dummy=zeros(m,1);
        diff=sum(s)-sum(d);
        c = [c,dummy];
        d = [d diff];
    else
        dummy=zeros(1,n);
        diff=sum(d)-sum(s);
        c = [c;dummy];
        s = [s diff];
    end
end

m = size(c,1);
n = size(c,2);

x=zeros(m,n);
ini_c=c;

for i=1:m
    for j=1:n
        mc=min(c(:));
        [mc_r,mc_c]=find(c==mc);

        x11=min(s(mc_r),d(mc_c));
        [alloc_val,ind]=max(x11);

        p=mc_r(ind);
        q=mc_c(ind);

        x(p,q)=alloc_val;

        s(p)=s(p)-alloc_val;
        d(q)=d(q)-alloc_val;

        if s(p)==0
            c(p,:)=inf;
        end
        if d(q)==0
            c(:,q)=inf;
        end
    end
end

tc=sum(sum(ini_c.*x));
fprintf('Transportation cost is %f\n',tc);
````

```
```

