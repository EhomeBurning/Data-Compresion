# Data-Compresion

* Assuming 15 symble 
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

```
%Shano Fano coding m file:
clc;
clear all;
close all;
m=["The recent development of various methods of modulation such as PCM and PPM which exchange bandwidth for signal-to-noise ratio has intensified the interest in a general theory of communication. A basis for such a theory is contained in the important papers of Nyquist and Hartley on this subject. In the present paper we will extend the theory to include a number of new factors, in particular the effect of noise in the channel, and the savings possible due to the statistical structure of the original message and due to the nature of the final destination of the information."];
len=578
z=[];
h=0;l=0;
p = 1*rand(len,1);
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

Alpha Matrixa =      

 Columns 1 through 8:     

   0.00000   0.00158   0.00308   0.00468   0.00633   0.00922   0.01001   0.01116     

 Columns 9 through 16:     

   0.01453   0.01726   0.01737   0.01744   0.02064   0.02110   0.02308   0.02474     

 Columns 17 through 24:     

   0.02776   0.02996   0.03086   0.03226   0.03533   0.03651   0.03734   0.03886     

 Columns 25 through 32:     

   0.04187   0.04418   0.04708   0.04787   0.04881   0.05053   0.05269   0.05289     

 Columns 33 through 40:     

   0.05570   0.05880   0.06046   0.06146   0.06205   0.06396   0.06399   0.06509     

 Columns 41 through 48:     

   0.06586   0.06907   0.07227   0.07384   0.07453   0.07621   0.07822   0.07875     

 Columns 49 through 56:     

   0.08142   0.08486   0.08529   0.08802   0.09092   0.09393   0.09448   0.09457     

 Columns 57 through 64:     

   0.09489   0.09628   0.09653   0.09958   0.10202   0.10382   0.10543   0.10876     

 Columns 65 through 72:     
     
   0.11150   0.11152   0.11154   0.11222   0.11361   0.11608   0.11702   0.11705     

 Columns 73 through 80:     

   0.11778   0.12040   0.12087   0.12378   0.12694   0.13008   0.13152   0.13298     

 Columns 81 through 84:     

   0.13594   0.13600   0.13648   0.13956     


Code length matrix isn =     

 Columns 1 through 16:     

   10   10   10   10    9   11   10    9    9   14   14    9   12    9   10    9     

 Columns 17 through 32:     

    9   11   10    9   10   11   10    9    9    9   11   11   10    9   13    9     

 Columns 33 through 48:     

    9   10   10   11   10   16   10   11    9    9   10   11   10    9   11    9     

 Columns 49 through 64:

    9   12    9    9    9   11   14   12   10   12    9    9   10   10    9    9     

 Columns 65 through 80:     

   16   16   11   10    9   11   16   11    9   12    9    9    9   10   10    9     

 Columns 81 through 84:     

   15   12    9   10     
     
Codeword 1 :z =     

   0   0   0   0   0   0   0   0   0   0     

Codeword 2 :z =

   0   0   0   0   0   0   0   0   0   1     

Codeword 3 :z =

   0   0   0   0   0   0   0   0   1   1     

Codeword 4 :z =

   0   0   0   0   0   0   0   1   0   0

Codeword 5 :z =     

   0   0   0   0   0   0   0   1   1     

Codeword 6 :z =     

   0   0   0   0   0   0   1   0   0   1   0     

Codeword 7 :z =     

   0   0   0   0   0   0   1   0   1   0     

Codeword 8 :z =          

   0   0   0   0   0   0   1   0   1     

Codeword 9 :z =     

   0   0   0   0   0   0   1   1   1     

Codeword 10 :z =     

   0   0   0   0   0   1   0   0   0   1   1   0   1   0     

Codeword 11 :z =     

   0   0   0   0   0   1   0   0   0   1   1   1   0   0     

Codeword 12 :z =     

   0   0   0   0   0   1   0   0   0     

Codeword 13 :z =     

   0   0   0   0   0   1   0   1   0   1   0   0     

Codeword 14 :z =     
     
   0   0   0   0   0   1   0   1   0     

Codeword 15 :z =     

   0   0   0   0   0   1   0   1   1   1     

Codeword 16 :z =     

   0   0   0   0   0   1   1   0   0     

Codeword 17 :z =     

   0   0   0   0   0   1   1   1   0     

Codeword 18 :z =     

   0   0   0   0   0   1   1   1   1   0   1     

Codeword 19 :z =     

   0   0   0   0   0   1   1   1   1   1     

Codeword 20 :z =     

   0   0   0   0   1   0   0   0   0     

Codeword 21 :z =     

   0   0   0   0   1   0   0   1   0   0     

Codeword 22 :z =     

   0   0   0   0   1   0   0   1   0   1   0     

Codeword 23 :z =     

   0   0   0   0   1   0   0   1   1   0     

Codeword 24 :z =     

   0   0   0   0   1   0   0   1   1     

Codeword 25 :z =     

   0   0   0   0   1   0   1   0   1     

Codeword 26 :z =     

   0   0   0   0   1   0   1   1   0

Codeword 27 :z =

   0   0   0   0   1   1   0   0   0   0   0

Codeword 28 :z =

   0   0   0   0   1   1   0   0   0   1   0

Codeword 29 :z =

   0   0   0   0   1   1   0   0   0   1

Codeword 30 :z =

   0   0   0   0   1   1   0   0   1

Codeword 31 :z =

   0   0   0   0   1   1   0   1   0   1   1   1   1

Codeword 32 :z =

   0   0   0   0   1   1   0   1   1

Codeword 33 :z =

   0   0   0   0   1   1   1   0   0

Codeword 34 :z =

   0   0   0   0   1   1   1   1   0   0

Codeword 35 :z =

   0   0   0   0   1   1   1   1   0   1

Codeword 36 :z =

   0   0   0   0   1   1   1   1   1   0   1

Codeword 37 :z =

   0   0   0   0   1   1   1   1   1   1

Codeword 38 :z =

   0   0   0   1   0   0   0   0   0   1   0   1   1   1   1   1

Codeword 39 :z =

   0   0   0   1   0   0   0   0   0   1

Codeword 40 :z =

   0   0   0   1   0   0   0   0   1   0   1

Codeword 41 :z =

   0   0   0   1   0   0   0   0   1

Codeword 42 :z =

   0   0   0   1   0   0   0   1   1

Codeword 43 :z =

   0   0   0   1   0   0   1   0   1   0

Codeword 44 :z =

   0   0   0   1   0   0   1   0   1   1   1

Codeword 45 :z =

   0   0   0   1   0   0   1   1   0   0

Codeword 46 :z =

   0   0   0   1   0   0   1   1   1

Codeword 47 :z =

   0   0   0   1   0   1   0   0   0   0   0

Codeword 48 :z =

   0   0   0   1   0   1   0   0   0

Codeword 49 :z =

   0   0   0   1   0   1   0   0   1

Codeword 50 :z =

   0   0   0   1   0   1   0   1   1   0   1   1

Codeword 51 :z =

   0   0   0   1   0   1   0   1   1

Codeword 52 :z =

   0   0   0   1   0   1   1   0   1

Codeword 53 :z =

   0   0   0   1   0   1   1   1   0

Codeword 54 :z =

   0   0   0   1   1   0   0   0   0   0   0

Codeword 55 :z =

   0   0   0   1   1   0   0   0   0   0   1   0   1   1

Codeword 56 :z =

   0   0   0   1   1   0   0   0   0   0   1   1

Codeword 57 :z =

   0   0   0   1   1   0   0   0   0   1

Codeword 58 :z =

   0   0   0   1   1   0   0   0   1   0   1   0

Codeword 59 :z =

   0   0   0   1   1   0   0   0   1

Codeword 60 :z =

   0   0   0   1   1   0   0   1   0

Codeword 61 :z =

   0   0   0   1   1   0   1   0   0   0

Codeword 62 :z =

   0   0   0   1   1   0   1   0   1   0

Codeword 63 :z =

   0   0   0   1   1   0   1   0   1

Codeword 64 :z =

   0   0   0   1   1   0   1   1   1

Codeword 65 :z =

   0   0   0   1   1   1   0   0   1   0   0   0   1   0   1   1

Codeword 66 :z =

   0   0   0   1   1   1   0   0   1   0   0   0   1   1   0   0

Codeword 67 :z =

   0   0   0   1   1   1   0   0   1   0   0

Codeword 68 :z =

   0   0   0   1   1   1   0   0   1   0

Codeword 69 :z =

   0   0   0   1   1   1   0   1   0

Codeword 70 :z =

   0   0   0   1   1   1   0   1   1   0   1

Codeword 71 :z =

   0   0   0   1   1   1   0   1   1   1   1   1   0   1   0   1

Codeword 72 :z =

   0   0   0   1   1   1   0   1   1   1   1

Codeword 73 :z =

   0   0   0   1   1   1   1   0   0

Codeword 74 :z =

   0   0   0   1   1   1   1   0   1   1   0   1

Codeword 75 :z =

   0   0   0   1   1   1   1   0   1

Codeword 76 :z =

   0   0   0   1   1   1   1   1   1

Codeword 77 :z =

   0   0   1   0   0   0   0   0   0

Codeword 78 :z =

   0   0   1   0   0   0   0   1   0   1

Codeword 79 :z =

   0   0   1   0   0   0   0   1   1   0

Codeword 80 :z =

   0   0   1   0   0   0   1   0   0

Codeword 81 :z =

   0   0   1   0   0   0   1   0   1   1   0   0   1   1   0

Codeword 82 :z =

   0   0   1   0   0   0   1   0   1   1   0   1

Codeword 83 :z =

   0   0   1   0   0   0   1   0   1

Codeword 84 :z =

   0   0   1   0   0   0   1   1   1   0

Avg. Code Lengthl =  1.3303     
Entropyh =  1.2486     
Efficiency 93.855     
Redundancy 6.1453     
