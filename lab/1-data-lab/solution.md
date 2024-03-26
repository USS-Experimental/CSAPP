# Solution to CSAPP lab1: data lab

1. **bitXor**  

> bitXor - x^y using only ~ and &
> Example: bitXor(4, 5) = 1  
> Legal ops: ~ &  
> Max ops: 14  
> Rating: 1  

We knows that $x \oplus y = x \overline{y} + \overline{x} y$, in c operator, `x^y = (x & (~y)) | ((~x) & y)`. And we can only use `~`, which is NOT($\overline{x}$), and `&`, which is AND($\cdot$). So we must change the `|` operator, which is OR($+$), to the combination of upper two operation. 

It seems to be little tricky without the knowledge of Boolean Algebra. But it only requires a single trick calls De Morgan's laws.

> $\lnot(p \land q) \equiv (\lnot p) \lor (\lnot q)$  
> $\lnot(p \lor q) \equiv (\lnot p) \land (\lnot q)$  
> or  
> $x + y = \overline{\overline{x} \cdot \overline{y}}$  
> $x \cdot y = \overline{\overline{x} + \overline{y}}$  

It is quite clear right now, $x \overline{y} + \overline{x} y$ is equivalent to $\overline{\overline{x \overline{y}} \cdot \overline{\overline{x} y}}$, so `x^y = (x & (~y)) | ((~x) & y)` now equivalent to `x^y = ~((x & (~y)) & ((~x) & y))`. And this is our solution.