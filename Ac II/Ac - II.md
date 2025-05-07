[[Resumo de Assembly (ate o momento 06-maio)]] explica melhor
# Assembly

instruções dadas ate o momento:

- ULA
``` Assembly

	add $rd $rf1 $rf2
	sub $rd $rf1 $rf2
	
```

#### **Arquitetura de von Neumann** ? (o que e)

### MIPS
(uma maquina de 32 bits)
``` opcode (6) | rs (5) | rt (5) | immediate (16) ```


```Assembly
addi $rd, $rf, imediato # rd = nf + imediato
```

Imediato -> n˚ na base 10
|          		   n˚ hexa => Ox... 
|        		   +, -
|_ 16 bits, ou seja ele tem que estar no intervalo \[-32768, 32767]

Exemplo:

faça com x= 100.000
```Assembly
x -> $S0
addi $t0, $zero, 30.000 # t0 = 0 + 30.000
add $t0, $t0, $t0 # t0 = 60.000
add $t0, $t0, $t0 # t0 = 120.000
addi $t0, $zero, -20.000 # t0 = 0 + 30.000
```

``` Assembly
or $rd, $rf1, $rf2 # rd = rf1 | rf2
and $rd, $rf1, $ft2 # rd - rf1 & rf2
```

mas levando em conta que a aquitetura de von Neumann tbm se aplica a ela;

``` Assembly
ori $rd, $rf, imediato #lembrando que o imediato tem 16 bits de                                espaco
andi $rd, $rf, imediato
```

### Shift ou Deslocamento

#### Deslocamento para a esquerda 

```Assembly
sll $destino, $origem, quantidade
```
lembrando que o deslocamento e feito em bit a bit

#### Deslocamento para a direita

```Assembly
srl $t0, $t1, 2   # $t0 = $t1 >> 2 (desloca $t1 dois bits para a direita, inserindo 0s à esquerda)
```

Comparação:
```

| Instrução | Nome                     | Direção | Sinal preservado? |
|-----------|--------------------------|---------|-------------------|
| `sll`     | Shift Left Logical       | ←       | Não               |
| `srl`     | Shift Right Logical      | →       | Não               |
| `sra`     | Shift Right Arithmetic   | →       | Sim               |
```

