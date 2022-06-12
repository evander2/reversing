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


DAT_140003000, DAT_140003020 확인하고 역연산


```python

flag =['0','4D','51','50','EF','FB','C3','CF','92','45','4D','CF','F5','4','40','50',
'43','63']

key = ['63','7C','77','7B','F2','6B','6F','C5','30','1','67','2B','FE','D7','AB','76',
'CA','82','C9','7D','FA','59','47','F0','AD','D4','A2','AF','9C','A4','72','C0',
'B7','FD','93','26','36','3F','F7','CC','34','A5','E5','F1','71','D8','31','15',
'4','C7','23','C3','18','96','5','9A','7','12','80','E2','EB','27','B2','75',
'9','83','2C','1A','1B','6E','5A','A0','52','3B','D6','B3','29','E3','2F','84',
'53','D1','0','ED','20','FC','B1','5B','6A','CB','BE','39','4A','4C','58','CF',
'D0','EF','AA','FB','43','4D','33','85','45','F9','2','7F','50','3C','9F','A8',
'51','A3','40','8F','92','9D','38','F5','BC','B6','DA','21','10','FF','F3','D2',
'CD','0C','13','EC','5F','97','44','17','C4','A7','7E','3D','64','5D','19','73',
'60','81','4F','DC','22','2A','90','88','46','EE','B8','14','DE','5E','0B','DB',
'E0','32','3A','0A','49','6','24','5C','C2','D3','AC','62','91','95','E4','79',
'E7','C8','37','6D','8D','D5','4E','A9','6C','56','F4','EA','65','7A','AE','8',
'BA','78','25','2E','1C','A6','B4','C6','E8','DD','74','1F','4B','BD','8B','8A']

result = ''
for i in range(0, len(flag)):
    for j in range(0, len(key)):
        if flag[i] == key[j]:
            result += chr(j)

print(result)

```

`Replac3_the_w0rld`


## chall7

```C
byte bVar1;
uint local_18;
  
local_18 = 0;
while( true ) {
    if (0x1e < local_18) {
      return 1;
    }
    bVar1 = (byte)local_18 & 7;
    if (((byte)(*(byte *)(param_1 + (int)local_18) << bVar1 |
               *(byte *)(param_1 + (int)local_18) >> 8 - bVar1) ^ local_18) !=
        (uint)(byte)(&DAT_140003000)[(int)local_18]) break;
    local_18 = local_18 + 1;
}
return 0;
```


```python

flag = [0x52, 0xDF, 0xB3, 0x60, 0xF1, 0x8B, 0x1C, 0xB5, 0x57, 0xD1, 0x9F, 0x38, 0x4B, 0x29, 0xD9, 0x26, 
0x7F, 0xC9, 0xA3, 0xE9, 0x53, 0x18, 0x4F, 0xB8, 0x6A, 0xCB, 0x87, 0x58, 0x5B, 0x39, 0x1E, 0x00]

j = 0;

for i in range(0, 32):
    if j == 8:
        j=j-8
    fx[i]=i^ buf[i];
    tmp1 = fx[i] >> j;
    tmp2 = fx[i] << (8 - j);
    input[i] = tmp1 + tmp2;
    result += input(i)
    j=j+1
    
print(result)

```






## chall9





## easyarray





## ransome
