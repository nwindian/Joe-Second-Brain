#Computer-Science #Leetcode 

# XOR
12 =        00001100
25 =        00011001
_________________
12^25 =  00100101

Add two decimals with bitwise:
12 + 25
```
    int getSum(int a, int b) {
        unsigned int buff = INT_MIN;

        while(buff != 0){
            buff = a&b;
            a = a^b;
            b = buff << 1;
        }

        return a;
    }
```

a: 00001100 + b: 00011001
Iteration 1:
	buff = (a&b) =     00001000
	a = (a^b) =          00010101
	b = (buff << 1) = 00010000 

Iteration 2:
	buff = (a&b) =     00010000
	a = (a^b) =          00000101
	b = (buff << 1) = 00100000

Iteration 3:
	buff = (a&b) =     00000000
	a = (a^b) =          __00100101__
	b = (buff << 1) = 00000000