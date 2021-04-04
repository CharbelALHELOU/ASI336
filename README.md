# Rapport ASI336
En ouvrant le fichier `ctf_1` avec Ghidra et en cherchant directement le main, c'est-a-dire l'entree du programme, on remarque assez rapidement les fonctions importantes à regarder : `check`, et les `check_char_[0-6]`.

## Analyse de <check_char_1>

CODE: _ _ _ _ _ _ _

```
bool check_char_1(char param_1)
{
  return (char)(param_1 * '\x0e') == -0x7e;
}
```

Il s'agit de resoudre

`param_1 * 14 = -126` => param_1 = -9;

avec `a = 'C'`, ça devrait marcher !



 


```
bool check_char_2(char param_1)

{
  return (char)((param_1 + '\x13') * '\f') == -0x60;
}




bool check_char_3(char param_1)

{
  puts("Going to sleep");
  sleep(100);
  return (char)(param_1 * '\v') == '\a';
}




bool check_char_4(char param_1)

{
  char cVar1;
  char cVar2;
  
  cVar2 = (param_1 + '\x01') * '\x1c';
  cVar1 = col(cVar2);
  if (cVar1 == '\x01' || cVar2 == '\0') {
    cVar2 = cVar2 + '\x12';
  }
  else {
    cVar2 = cVar2 + '2';
  }
  return cVar2 == -0x76;
}

undefined4 check_char_5(void)

{
  return 1;
}


bool check_char_6(char param_1)

{
  return param_1 == '[';
}


bool check_char_0(undefined param_1)

{
  undefined uVar1;
  char cVar2;
  
  uVar1 = eval(0xc9,param_1,2);
  uVar1 = eval(0xf0,uVar1,2);
  cVar2 = eval(0xc9,uVar1,10);
  return cVar2 == -0x42;
}

undefined4 check(char *param_1)

{
  int iVar1;
  
  iVar1 = check_char_0((int)*param_1);
  if (((((iVar1 != 0) && (iVar1 = check_char_1((int)param_1[1]), iVar1 != 0)) &&
       (iVar1 = check_char_2((int)param_1[2]), iVar1 != 0)) &&
      ((iVar1 = check_char_3((int)param_1[3]), iVar1 != 0 &&
       (iVar1 = check_char_4((int)param_1[4]), iVar1 != 0)))) &&
     ((iVar1 = check_char_5((int)param_1[5]), iVar1 != 0 &&
      ((iVar1 = check_char_6((int)param_1[6]), iVar1 != 0 &&
       (iVar1 = check_array(param_1 + 7,7), iVar1 != 0)))))) {
    return 1;
  }
  return 0;
}


void eval(int param_1,uint param_2,uint param_3)

{
  void *pvVar1;
  void *pvVar2;
  int unaff_EBP;
  int unaff_retaddr;
  uint in_stack_fffffff4;
  uint in_stack_fffffff8;
  
  pvVar1 = (void *)(param_2 & 0xff);
  pvVar2 = (void *)(param_3 & 0xff);
  if ((((param_1 != 0xf0) && (param_1 < 0xf1)) && (param_1 != 0xe3)) &&
     (((param_1 < 0xe4 && (param_1 != 0xd7)) &&
      ((param_1 < 0xd8 && ((param_1 != 0xc9 && (param_1 < 0xca)))))))) {
    if (param_1 == 0x77) {
      r(pvVar1,pvVar2,in_stack_fffffff4 & 0xffffff00 | (uint)pvVar2,
        (char *)(in_stack_fffffff8 & 0xffffff00 | (uint)pvVar1),unaff_EBP,unaff_retaddr);
    }
    else {
      if (((((param_1 < 0x78) && (param_1 != 0x69)) && (param_1 < 0x6a)) &&
          ((param_1 != 0x4c && (param_1 < 0x4d)))) && (param_1 == 0x45)) {
        l(pvVar1,pvVar2);
      }
    }
  }
  return;
}


byte col(byte param_1)

{
  int local_c;
  byte local_5;
  
  local_5 = param_1;
  local_c = 0;
  while ((local_c < 200 && (local_5 != 1))) {
    if ((local_5 & 1) == 0) {
      local_5 = local_5 >> 1;
    }
    else {
      local_5 = local_5 * '\x03' + 1;
    }
    local_c = local_c + 1;
  }
  return local_5;
}
```
