# reversing


## chall6


```C
uint local_18;
  
local_18 = 0;
while( true ) {
    if (0x11 < local_18) {
      return 1;
    }
    if ((&DAT_140003020)[*(byte *)(param_1 + (int)local_18)] != (&DAT_140003000)[(int)local_18])
    break;
    local_18 = local_18 + 1;
}
return 0;
```

DAT_140003020 : 63, 7C, 77, 7B, F2, 6B, 6F, C5, 30, 01, 67, 2B, FE, D7, AB, 76, CA
DAT_140003000 : 00, 4D, 51, 50, EF, FB, C3, CF, 92, 45, 4D, CF, F5, 04, 40, 50, 43,


```python

arr = [0x63, 0x7C, 0x77, 0x7B, 0xF2, 0x6B, 0x6F, 0xC5, 0x30, 0x01, 0x67, 0x2B, 0xFE, 0xD7, 0xAB, 0x76, 0xCA]

for i in arr:
    a = 


```



## chall7







## chall9





## easyarray





## ransome
