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


DAT_140003000, DAT_140003020 확인하고 역연산한다.


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

회전 연산임을 알 수 있고, shift와 carry bit을 이용해 rolfunction 함수를 구현할 수 다. 주어진 조건이 맞을 경우 result에 더하여 flag를 구할 수 있다.

```python

def rolfunction(x, n):
    shift = x << n
    shift &= 255
    carry = x >> 8 - n
    return shift | carry


flag = [0x52, 0xDF, 0xB3, 0x60, 0xF1, 0x8B, 0x1C, 0xB5, 0x57, 0xD1, 0x9F, 0x38, 0x4B, 0x29, 0xD9, 0x26, 
0x7F, 0xC9, 0xA3, 0xE9, 0x53, 0x18, 0x4F, 0xB8, 0x6A, 0xCB, 0x87, 0x58, 0x5B, 0x39, 0x1E]

result = ''

for i in range(0, 31):
    for j in range(33, 128):
        if rolfunction(j, (i & 7))^i == flag[i]:
            result += chr(j)
            break


print(result)


```

`Roll_the_left!_Roll_the_right!`



## chall9


```C
sVar2 = strlen(param_1);
iVar1 = (int)sVar2 + 1;
uVar4 = iVar1 >> 0x1f & 7;
if ((iVar1 + uVar4 & 7) == uVar4) {
    for (local_18 = 0; local_18 < (int)sVar2 + 1; local_18 = local_18 + 8) {
        FUN_1400010a0((byte *)(param_1 + local_18));
    }
    iVar1 = memcmp(param_1,&DAT_140004000,0x19);
    if (iVar1 == 0) uVar3 = 1;
    else uVar3 = 0;
}
```
```C
local_28 = DAT_140004128 ^ (ulonglong)local_48;
pbVar2 = (byte *)"I_am_KEY";
pbVar3 = local_38;
for (lVar1 = 9; lVar1 != 0; lVar1 = lVar1 + -1) {
    *pbVar3 = *pbVar2;
    pbVar2 = pbVar2 + 1;
    pbVar3 = pbVar3 + 1;
}
local_48[0] = *param_1;
for (local_40 = 0; local_40 < 0x10; local_40 = local_40 + 1) {
    for (local_44 = 0; local_44 < 8; local_44 = local_44 + 1) {
        local_48[0] = (byte)((&DAT_140004020)[(int)(uint)(local_48[0] ^ local_38[local_44])] +
                          param_1[(int)(local_44 + 1U & 7)]) >> 5 |
                    ((&DAT_140004020)[(int)(uint)(local_48[0] ^ local_38[local_44])] +
        param_1[(int)(local_44 + 1U & 7)]) * '\b';
        param_1[(int)(local_44 + 1U & 7)] = local_48[0];
    }
}
```

블록 암호 문제인 것으로 보이고, s_box를 찾고 c 배열의 값을 찾을 수 있다. 회전 연산 함수를 만들어서 입력값을 구할 수 있다.
8bytes씩 연산이 진행되므로 암호화된 배열을 3개로(8개씩) 나누어서 계산하고, xor, s_box 연산 이후의 값, lor 연산 이후의 암호화 값을 계산하여(예외 처리 해야 함) rotate 계산을 진행할 수 있다. 16번의 round를 진행하면 flag을 얻을 수 있다.


```C
#include <stdio.h>
#include <string.h>

const int s_box[16][16] = {
  {0x63, 0x7c, 0x77, 0x7b, 0xf2, 0x6b, 0x6f, 0xc5, 0x30, 0x01, 0x67, 0x2b, 0xfe, 0xd7, 0xab, 0x76},
  {0xca, 0x82, 0xc9, 0x7d, 0xfa, 0x59, 0x47, 0xf0, 0xad, 0xd4, 0xa2, 0xaf, 0x9c, 0xa4, 0x72, 0xc0},
  {0xb7, 0xfd, 0x93, 0x26, 0x36, 0x3f, 0xf7, 0xcc, 0x34, 0xa5, 0xe5, 0xf1, 0x71, 0xd8, 0x31, 0x15},
  {0x04, 0xc7, 0x23, 0xc3, 0x18, 0x96, 0x05, 0x9a, 0x07, 0x12, 0x80, 0xe2, 0xeb, 0x27, 0xb2, 0x75},
  {0x09, 0x83, 0x2c, 0x1a, 0x1b, 0x6e, 0x5a, 0xa0, 0x52, 0x3b, 0xd6, 0xb3, 0x29, 0xe3, 0x2f, 0x84},
  {0x53, 0xd1, 0x00, 0xed, 0x20, 0xfc, 0xb1, 0x5b, 0x6a, 0xcb, 0xbe, 0x39, 0x4a, 0x4c, 0x58, 0xcf},
  {0xd0, 0xef, 0xaa, 0xfb, 0x43, 0x4d, 0x33, 0x85, 0x45, 0xf9, 0x02, 0x7f, 0x50, 0x3c, 0x9f, 0xa8},
  {0x51, 0xa3, 0x40, 0x8f, 0x92, 0x9d, 0x38, 0xf5, 0xbc, 0xb6, 0xda, 0x21, 0x10, 0xff, 0xf3, 0xd2},
  {0xcd, 0x0c, 0x13, 0xec, 0x5f, 0x97, 0x44, 0x17, 0xc4, 0xa7, 0x7e, 0x3d, 0x64, 0x5d, 0x19, 0x73},
  {0x60, 0x81, 0x4f, 0xdc, 0x22, 0x2a, 0x90, 0x88, 0x46, 0xee, 0xb8, 0x14, 0xde, 0x5e, 0x0b, 0xdb},
  {0xe0, 0x32, 0x3a, 0x0a, 0x49, 0x06, 0x24, 0x5c, 0xc2, 0xd3, 0xac, 0x62, 0x91, 0x95, 0xe4, 0x79},
  {0xe7, 0xc8, 0x37, 0x6d, 0x8d, 0xd5, 0x4e, 0xa9, 0x6c, 0x56, 0xf4, 0xea, 0x65, 0x7a, 0xae, 0x08},
  {0xba, 0x78, 0x25, 0x2e, 0x1c, 0xa6, 0xb4, 0xc6, 0xe8, 0xdd, 0x74, 0x1f, 0x4b, 0xbd, 0x8b, 0x8a},
  {0x70, 0x3e, 0xb5, 0x66, 0x48, 0x03, 0xf6, 0x0e, 0x61, 0x35, 0x57, 0xb9, 0x86, 0xc1, 0x1d, 0x9e},
  {0xe1, 0xf8, 0x98, 0x11, 0x69, 0xd9, 0x8e, 0x94, 0x9b, 0x1e, 0x87, 0xe9, 0xce, 0x55, 0x28, 0xdf},
  {0x8c, 0xa1, 0x89, 0x0d, 0xbf, 0xe6, 0x42, 0x68, 0x41, 0x99, 0x2d, 0x0f, 0xb0, 0x54, 0xbb, 0x16}};

int c1[8] = {0x7d, 0x9a, 0x8b, 0x25, 0x2d, 0xd5, 0x3d, 0x7e};
int c2[8] = {0x2b, 0x38, 0x98, 0x27, 0x9f, 0x4f, 0xbc, 0x03};
int c3[8] = {0x79, 0x00, 0x7d, 0xc4, 0x2a, 0x4f, 0x58, 0x2a};

int in[8]={0,}, out[8]={0,};
int key[8] = {0x49, 0x5f, 0x61, 0x6d, 0x5f, 0x4b, 0x45, 0x59};

int sub(int a, int b){
    if(a>b) return b-a+256;
    else return b-a;
}

int lor(int n){
    int res = 0;
    res = n<<5;
    res += n>>3;
    res %= 256;
    return res;
}

void rotate(int c[]){
    int val = 0;
    for(int i=7; i>=0; i--{
        val = in[i]^key[i];
        val = s_box[val/16][val%16];
        out[i] = sub(val, lor(c[i]));
        if(i==7) in[0] = out[i];
    }
    memcpy(c, out, sizeof(out));
}


int main(){
    for(int i=0; i<16; i++){
        rotate(c1); rotate(c2); rotate(c3);
    }
    
    printf("%c", c1[7]);
    for(int i=0; i<7; i++) printfd("%c", c1[i]);
    printf("%c", c2[7]);
    for(int i=0; i<7; i++) printfd("%c", c2[i]);
    printf("%c", c3[7]);
    for(int i=0; i<7; i++) printfd("%c", c3[i]);
}


```

out[7]의 값이 in[0]의 값이고, 뺄셈 계산시 1바이트 연산을 해야 함을 기억하여 처리하고 출력하면 된다.


`Reverse__your__brain_;)`



## easyarray


```C
printf("input:",(undefined4 *)((longlong)puVar4 + 4));
scanf("%s");
lVar3 = mystrlen((char *)local_88);
if ((int)lVar3 != 0x1b) {
    puts("wrong input length");
    getch();
    exit(0);
}
local_1c = 0;
while( true ) {
    if (0x1a < local_1c) {
      puts("correct! input is your flag");
      getch();
      return 0;
    }
    if ((uint)*(byte *)((longlong)local_88 + (longlong)local_1c) !=
        *(uint *)(&table + (longlong)local_1c * 4)) break;
    local_1c = local_1c + 1;
}
puts("wrong flag");
getch();
```

input의 길이는 27이고, 역연산을 통해 flag를 구할 수 있다.


```python

table = [0x3a, 0xc0, 0x3c, 0xcf, 0xfb, 0x54, 0x12, 0xcf, 0x12, 0x7e, 0xc5, 0x31, 0xb4, 0xdc, 0x47, 0x27, 
0x59, 0xf0, 0xdc, 0x47, 0xdf, 0xb4, 0xb4, 0x59, 0xdc, 0x9c, 0x11]


result = ''

for i in range(0, len(table)):
    result += chr(i)
    
print(result)

```

` `


` `





## ransome










