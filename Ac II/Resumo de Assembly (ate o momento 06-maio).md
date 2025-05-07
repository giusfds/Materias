
🔧 INSTRUÇÕES DA ULA (OPERAM COM REGISTRADORES)

    add $rd, $rf1, $rf2     # $rd = $rf1 + $rf2
    sub $rd, $rf1, $rf2     # $rd = $rf1 - $rf2

- $rd = registrador de destino (onde o resultado vai parar)
- $rf1 e $rf2 = registradores fonte
- Essas instruções não usam valores imediatos.


💾 INSTRUÇÃO COM IMEDIATO (USANDO NÚMERO DIRETO)

    addi $rd, $rf, imediato   # $rd = $rf + imediato

- Imediato é um valor inteiro em base decimal (positivo ou negativo).
- O valor do imediato deve estar no intervalo: [-32.768, 32.767] (porque são 16 bits com sinal).


⚙️ ARQUITETURA DE VON NEUMANN

- Mesma memória para instruções e dados.
- Processador de 32 bits (largura dos registradores e barramentos principais).
- O acesso à memória é sequencial, ou seja, mais lento que trabalhar diretamente com registradores.
- Por isso, sempre que possível, trabalhe com registradores ao invés de acessar a memória várias vezes.


💡 EXEMPLO DE COMO CONSTRUIR O NÚMERO 100.000 USANDO APENAS IMEDIATOS DE 16 BITS

Problema:
Imediato tem limite de 32.767 → não dá pra colocar 100.000 de uma vez com addi.

Solução (usando somas acumuladas):

    addi $t0, $zero, 30000     # $t0 = 30.000
    add  $t0, $t0, $t0         # $t0 = 60.000
    add  $t0, $t0, $t0         # $t0 = 120.000
    addi $t0, $t0, -20000      # $t0 = 100.000

Explicação:
- Carrega um valor válido (30.000).
- Dobra duas vezes: 30.000 → 60.000 → 120.000.
- Subtrai 20.000 com addi negativo: 120.000 - 20.000 = 100.000.


➕ COMPLEMENTOS ÚTEIS

📍 REGISTRADORES COMUNS (MIPS-LIKE)

    Registrador | Uso comum
    ------------|----------------------
    $zero       | Sempre vale 0
    $t0-$t7     | Temporários (uso geral)
    $s0-$s7     | Variáveis salvas
    $a0-$a3     | Argumentos (funções)
    $v0-$v1     | Retornos de funções


📌 DICAS PARA ASSEMBLY

- Sempre que for carregar um número grande: quebra com addi e add.
- Evita usar números fora do intervalo imediato sem montar eles passo a passo.
- Organize seus registradores: use $s0 a $s7 para guardar variáveis, e $t0 a $t7 para contas temporárias.