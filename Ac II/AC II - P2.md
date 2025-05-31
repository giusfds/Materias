Começo -> [[Ac - II]]

### SLL & SRL
- Shift Logical Left - SLL
- Shift Logical Right - SRL
----------
- sao operadores de deslocamento (shift) usados para mover os bits de um registradir oara a esquerda(sll) ou diretia(srl)

``` asm
SLL $t0, t01, 2
```
- Isso desloca os bits de $t1 2 posições para a esquerda, e armazena o resultado em $t0

Exemplo:
```asm
Supondo valores $t1 = 0000 0000 0000 0000 0000 0000 0000 0011
```
apos o sll, o valor obtido em t0 sera de 
```asm
$t0 = 0000 0000 0000 0000 0000 0000 0000 1100
```

A Mesma coisa ocorre com o SRL, porem de forma em sentidos opostos.

### **Tipos de Instrução**

  
Antes de mais nada:

- **Tipo R (Register):** opera apenas entre registradores.
- **Tipo I (Immediate):** opera entre registrador e valor imediato (constante).

---

### **Instruções Tipo R**

Formato: instr rd, rs, rt

> A operação acontece entre rs e rt, e o resultado vai para rd.

| **Instrução** | **Tipo** | **Descrição**                                                      |
| ------------- | -------- | ------------------------------------------------------------------ |
| add           | R        | Soma: rd = rs + rt                                                 |
| sub           | R        | Subtração: rd = rs - rt                                            |
| and           | R        | E lógico: rd = rs & rt                                             |
| or            | R        | OU lógico: `rd = rs                                                |
| sll           | R        | Shift lógico à esquerda: rd = rt << shamt (multiplica por 2^shamt) |
| srl           | R        | Shift lógico à direita: rd = rt >> shamt (divide por 2^shamt)      |
> shamt é o número de bits que você quer deslocar. Ex: sll $t0, $t1, 2 desloca $t1 2 bits à esquerda e armazena em $t0.

### **Instruções Tipo I**
Formato: instr rt, rs, immediate
> A operação é entre o registrador rs e um valor imediato (constante). O resultado vai para rt.

| **Instrução** | **Tipo** | **Descrição**                                                                           |
| ------------- | -------- | --------------------------------------------------------------------------------------- |
| addi          | I        | Soma com imediato: rt = rs + imm                                                        |
| andi          | I        | E lógico com imediato: rt = rs & imm                                                    |
| ori           | I        | OU lógico com imediato: `rt = rs                                                        |
| lui           | I        | Load Upper Immediate: carrega os 16 bits superiores do registrador com o valor imediato |

-------------
# Exemplos praticos

## **Registradores básicos usados nos exemplos**

| **Nome**      | **Finalidade**                                 |
| ------------- | ---------------------------------------------- |
| $t0, $t1, $t2 | Temporários (podem ser usados livremente)      |
| $s0, $s1      | Salvos (mantêm valor entre chamadas de função) |
### **Instruções Tipo R (entre registradores)**

##### **add $t0, $t1, $t2**
```asm
$t0 = $t1 + $t2
```
Se $t1 = 5 e $t2 = 3, então $t0 vai receber 8.

##### **sub $t0, $t1, $t2**
```asm
$t0 = $t1 - $t2
```
Se $t1 = 10 e $t2 = 4, então $t0 = 6.

##### **and $t0, $t1, $t2**
```asm
$t0 = $t1 AND $t2
```

📌 Bit a bit. Ex:
- $t1 = 0b1100
- $t2 = 0b1010
- $t0 = 0b1000

##### **or $t0, $t1, $t2**
```asm
$t0 = $t1 OR $t2
```

📌 Ex:
- $t1 = 0b1100
- $t2 = 0b1010
- $t0 = 0b1110

##### **sll $t0, $t1, 2**
```asm
$t0 = $t1 << 2
```
Desloca os bits de $t1 duas casas à esquerda. Isso equivale a multiplicar por 4.
Se $t1 = 3, então $t0 = 12.

##### **srl $t0, $t1, 1**
```asm
$t0 = $t1 >> 1
```
Desloca os bits de $t1 uma casa à direita. Equivale a dividir por 2 (inteira).
Se $t1 = 8, então $t0 = 4.

### **Instruções Tipo I (com constantes)**

##### **addi $t0, $t1, 10**
```asm
$t0 = $t1 + 10
```
Se $t1 = 5, então $t0 = 15.

##### **andi $t0, $t1, 0x0F**
```asm
$t0 = $t1 & 0x0F
```
Faz um “AND” bit a bit entre $t1 e 00001111.
Isso extrai os 4 bits menos significativos.

##### **ori $t0, $t1, 0xF0**
```asm
$t0 = $t1 | 0xF0
```
Faz “OR” entre $t1 e 11110000, forçando os 4 bits mais altos a 1.

##### **lui $t0, 0x1234**
```asm
$t0 = 0x12340000
```
Carrega 0x1234 nos 16 bits superiores de $t0, e preenche os inferiores com zeros.


#### **Resumo de Instruções da ULA (MIPS)**
| **Instrução** | **Tipo** | **Descrição**                           | **Exemplo**         | **Resultado**    |
| ------------- | -------- | --------------------------------------- | ------------------- | ---------------- |
| add           | R        | Soma entre registradores                | add $t0, $t1, $t2   | $t0 = $t1 + $t2  |
| sub           | R        | Subtração entre registradores           | sub $t0, $t1, $t2   | $t0 = $t1 - $t2  |
| and           | R        | AND lógico (bit a bit)                  | and $t0, $t1, $t2   | $t0 = $t1 & $t2  |
| or            | R        | OR lógico (bit a bit)                   | or $t0, $t1, $t2    | `$t0 = $t1       |
| sll           | R        | Shift lógico à esquerda                 | sll $t0, $t1, 2     | $t0 = $t1 << 2   |
| srl           | R        | Shift lógico à direita                  | srl $t0, $t1, 1     | $t0 = $t1 >> 1   |
| addi          | I        | Soma com imediato                       | addi $t0, $t1, 10   | $t0 = $t1 + 10   |
| andi          | I        | AND com imediato                        | andi $t0, $t1, 0x0F | $t0 = $t1 & 0x0F |
| ori           | I        | OR com imediato                         | ori $t0, $t1, 0xF0  | `$t0 = $t1       |
| lui           | I        | Carrega imediato nos 16 bits superiores | lui $t0, 0x1234     | $t0 = 0x12340000 |
#### **Observações rápidas**
- **Tipo R:** usa 3 registradores: rd, rs, rt
- **Tipo I:** usa 2 registradores + um número: rt, rs, imediato
- **sll e srl** usam o campo de _shift_ (shamt, quantidade de bits para deslocar)

#### Dicas Rápidas
- `sll $t0, $t1, 2` → equivale a multiplicar `$t1` por 4  
- `srl $t0, $t1, 1` → equivale a dividir `$t1` por 2 (parte inteira)  
- `lui` é muito usado junto com `ori` para montar números de 32 b