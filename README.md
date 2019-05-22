# Data-Compresion

```
% Huffman coding m file:
clc;
clear all;
close all;
symbols = 1:15
p = 1*rand(15,1);
p = p'/sum(p)
dict = huffmandict(symbols,p)
sig = randsrc(15,1,[symbols; p])
comp = huffmanenco(sig,dict)
%End of m file
```

Output:   
symbols =    
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15   
p =  
Columns 1 through 7:  
0.105671 0.068952 0.109873 0.091431 0.044652 0.072219 0.106946   
Columns 8 through 14:  
0.011521 0.091896 0.057962 0.020089 0.047533 0.052772 0.030945  
Column 15:  
0.087537  
dict =  
{  
[1,1] =  
1 1 0  
[1,2] =  
0 1 0 0  
[1,3] =  
1 0 0  
[1,4] =  
0 0 0 1  
[1,5] =  
1 1 1 1  
[1,6] =  
0 0 1 1  
[1,7] =    
1 0 1    
[1,8] =    
0 1 0 1 0 1    
[1,9] =    
0 0 0 0    
[1,10] =    
0 1 1 0    
[1,11] =    
0 1 0 1 0 0    
[1,12] =    
1 1 1 0    
[1,13] =    
0 1 1 1    
[1,14] =    
0 1 0 1 1    
[1,15] =    
0 0 1 0    
}    
sig =    
8    
14    
10    
1    
15    
12    
13    
10    
9    
3    
9    
5    
4    
9    
4    
comp =    
Columns 1 through 20:    
0 1 0 1 0 1 0 1 0 1 1 0 1 1 0 1 1 0 0 0    
Columns 21 through 40:    
1 0 1 1 1 0 0 1 1 1 0 1 1 0 0 0 0 0 1 0    
Columns 41 through 60:    
0 0 0 0 0 1 1 1 1 0 0 0 1 0 0 0 0 0 0 0    
Column 61:    
1    

```
%Shano Fano coding m file:
clc;
clear all;
close all;
m=15;
z=[];
h=0;l=0;
p = 1*rand(15,1);
p = p'/sum(p);
%Finding each alpha values
a(1)=0;
for j=2:m;
a(j)=a(j-1)+p(j-1);
end
fprintf('\n Alpha Matrix');
display(a);
%Finding each code length
for i=1:m
n(i)= ceil(-1*(log2(p(i))));
end
fprintf('\nCode length matrix is');
display(n);
%Computing each code
for i=1:m
int=a(i);
for j=1:n(i)
frac=int*2;
c=floor(frac);
frac=frac-c;
z=[z c];
int=frac;
end
fprintf('Codeword %d :',i);
display(z);
z=[];
end
%Computing Avg. Code Length & Entropy

fprintf('Avg. Code Length');
for i=1:m
x=p(i)*n(i);
l=l+x;
x=p(i)*log2(1/p(i));
h=h+x;
end
display(l);
fprintf('Entropy');
display(h);
%Computing Efficiency
fprintf('Efficiency');
display(100*h/l);
fprintf('Redundancy');
display(100-(100*h/l));
```

Output:    
Alpha Matrix Columns 1 through 8:    
0.00000 0.00942 0.12256 0.12628 0.13257 0.22648 0.36009 0.44274    
Columns 9 through 15:    
0.50312 0.54757 0.63873 0.68106 0.68232 0.80726 0.94644    
Code length matrix is 7 4 9 8 4 3 4 5 5 4 5 10 4 3 5    
Codeword 1 : 0 0 0 0 0 0 0    
Codeword 2 : 0 0 0 0    
Codeword 3 : 0 0 0 1 1 1 1 1 0    
Codeword 4 : 0 0 1 0 0 0 0 0    
Codeword 5 : 0 0 1 0    
Codeword 6 : 0 0 1    
Codeword 7 : 0 1 0 1    
Codeword 8 : 0 1 1 1 0    
Codeword 9 : 1 0 0 0 0    
Codeword 10 : 1 0 0 0        
Codeword 11 : 1 0 1 0 0    
Codeword 12 : 1 0 1 0 1 1 1 0 0 1    
Codeword 13 : 1 0 1 0    
Codeword 14 : 1 1 0    
Codeword 15 : 1 1 1 1 0    
Avg. Code Length 4.0075    
Entropy 3.4623    
Efficiency 86.396    
Redundancy 13.604    


