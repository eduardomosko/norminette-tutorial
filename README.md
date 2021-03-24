# O que a Norminette quer?

Aviso: Este não é um documento oficial da 42, foi escrito por um camper curioso que ficou testando o que a Normitte aceita ou não.

Licensa: [The Unlicense](https://unlicense.org/), escrito por Eduardo Mosko

A Norminette é o programa que vai checar nossos programas para garantir que eles se adequam a norma da 42. Toda a avaliação vai começar rodando ela e se ela identificar um errinho se quer, pode dar tchau pra sua nota nesse trabalho porque ela vai ser **zero**. Por isso fui entender exatamento o que ela aceita ou não e escrevi esse "guia" que tem exemplos e explica como entender e aplicar as mensagens de erro da Norminette.

Tem dois exemplos: um para [iniciantes](#Olá, Mundo) que tem bem pouco código e explora as mensagens de erro da Norminette e outro mais complexo pra quem já tem [experiência](#Exemplo mais complexo) e só quer saber como vai ter que escrever aqui na 42.

Se você percebeu alguma coisa que não foi incluida aqui sinta-se livre pra mandar mensagem que eu testo e adiciono a explicação aqui (meu nome na intra/discord é *emendes-*), ou pode mandar um pull-request direto com a alteração.


# Olá, Mundo

Vamos partir desse programa e fazer ele ser aceito pela Norminnete.

```c
#include <stdio.h>

int main() {
	printf("Hello, World!\n");
	return 0;
}
```

Rodando a Norminette temos os seguintes erros:

```bash
$ norminette olamundo.c 
Norme: ./olamundo.c
Error: 42 header not at top of the file
Error: file must end with a single empty line
Error (line 3): Space before function name
Error (line 3): missing void in function main
Error (line 3, col 11): no newline before block
Error (line 5, col 8): missing parentheses in return statement
Error (line 6, col 0): no newline after block
```

Em português (vai ter que usar o tradutor)

```
Erro: o cabeçalho 42 não está no topo do arquivo
Erro: o arquivo deve terminar com uma única linha vazia
Erro (linha 3): Espaço antes do nome da função
Erro (linha 3): falta vazio na função principal
Erro (linha 3, coluna 11): sem nova linha antes do bloco
Erro (linha 5, col 8): parênteses ausentes na declaração de retorno
Erro (linha 6, coluna 0): sem nova linha após o bloco 
```

Então vamos analisar erro por erro.

- Erro: o cabeçalho 42 não está no topo do arquivo

Colocar o cabeçalho pode ser feito com `f2` pelo vim ou `Ctrl+Alt+H` pelo editor normal. Uma coisa importante de saber é que se você não deixar uma linha em branco entre o cabeçalho e os includes, o editor vai deletar os conteúdos daquela linha sem te avisar.

- Erro: o arquivo deve terminar com uma única linha vazia
- Erro (linha 3, coluna 11): sem nova linha antes do bloco
- Erro (linha 6, coluna 0): sem nova linha após o bloco 

Vamos resolver esses três erros juntos por que eles são muito parecidos, todos eles falam pra colocar um `enter` extra em alguns lugares. O primeiro diz pra você colocar um no final do arquivo, o segundo fala pra colocar antes do bloco (um bloco é o espaço entre um `{` e `}`) e o último pra colocar depois do bloco. No caso, colocar uma linha no final do arquivo resolve os primeiro e o último, já é o mesmo lugar. Dá pra saber se existe ou não uma última linha em branco se tiver um último número seguido de espaço em branco no editor de texto. Tipo assim:

`Sem última linha`
```c
15  int main() {
16  	printf("Hello, World!\n");
17  	return 0;
18  }

```

`Com última linha`
```c
15  int main() {
16  	printf("Hello, World!\n");
17  	return 0;
18  }
19
```

Já o segundo erro pede um enter antes do `{`.

```c
int main()
{
	printf("Hello, World!\n");
	return 0;
}

```

- Erro (linha 3): Espaço antes do nome da função

Basta trocar o espaço por uma tabulação (tab) antes do nome da função e depois do tipo de retorno. Tome cuidado ao copiar o codigo direto daqui, tente sempre digitar, para evitar erros.

```c
int	main()
{
	printf("Hello, World!\n");
	return 0;
}

```

- Erro (linha 3): falta vazio na função principal

A tradução deixou essa meio estranha. O original fala que falta `void` no `main`. Void é uma palavra chave que indica ausência de tipos, ou ausência de argumentos pra uma função. Devemos coloca-lá para indicar que `main` não recebe parametros.

```c
int	main(void)
{
	printf("Hello, World!\n");
	return 0;
}

```

- Erro (linha 5, col 8): parênteses ausentes na declaração de retorno

Temos que colocar as variáveis/literais que queromos retornar de uma função entre parênteses.

```c
int	main(void)
{
	printf("Hello, World!\n");
	return (0);
}

```

Então o "Olá, Mundo" aprovado pela Norminette fica assim:

```c
/* ************************************************************************** */
/*                                                                            */
/*                                                        :::      ::::::::   */
/*   olamundo.c                                         :+:      :+:    :+:   */
/*                                                    +:+ +:+         +:+     */
/*   By: emendes- <emendes-@student.42sp.org.br>    +#+  +:+       +#+        */
/*                                                +#+#+#+#+#+   +#+           */
/*   Created: 2021/03/23 23:42:00 by emendes-          #+#    #+#             */
/*   Updated: 2021/03/24 00:31:07 by emendes-         ###   ########.fr       */
/*                                                                            */
/* ************************************************************************** */

#include <stdio.h>

int	main(void)
{
	printf("Hello, World!\n");
	return (0);
}

```

Podemos garantir que realmente arrumamos tudo checando mais uma vez.

```bash
$ norminette olamundo.c 
Norme: ./olamundo.c
```

E isso aí!

# Exemplo mais complexo

Esse exemplo é pra quem já têm alguma experiência com C e só quer ver os detalhes de como vai ter que escrever aqui na 42. Aqui tá o exemplo de código que fui usando pra testar a Norminette e assim que ele fica 100% aceito e no final tem uma lista das coisas que tem que ser feitas de um jeito especifico, mas esse jeito não é explicado na Norma.

Arquivo `test.h`
```c
/* ************************************************************************** */
/*                                                                            */
/*                                                        :::      ::::::::   */
/*   test.h                                             :+:      :+:    :+:   */
/*                                                    +:+ +:+         +:+     */
/*   By: emendes- <emendes-@student.42sp.org.br>    +#+  +:+       +#+        */
/*                                                +#+#+#+#+#+   +#+           */
/*   Created: 2021/03/23 22:43:29 by emendes-          #+#    #+#             */
/*   Updated: 2021/03/24 00:42:00 by emendes-         ###   ########.fr       */
/*                                                                            */
/* ************************************************************************** */

#ifndef TEST_H
# define TEST_H

typedef struct	s_struct
{
	int   i;
	char	c;
}				t_struct;

typedef enum	e_numeros
{
	UM = 1, DOIS, TRES
}				t_numeros;

typedef union	u_union
{
	t_numeros	n;
	t_struct	s;
}				t_union;

int	sum(int a, int b);

#endif

```

Arquivo `test.c`
```c
/* ************************************************************************** */
/*                                                                            */
/*                                                        :::      ::::::::   */
/*   test.c                                             :+:      :+:    :+:   */
/*                                                    +:+ +:+         +:+     */
/*   By: emendes- <emendes-@student.42sp.org.br>    +#+  +:+       +#+        */
/*                                                +#+#+#+#+#+   +#+           */
/*   Created: 2021/03/23 22:27:01 by emendes-          #+#    #+#             */
/*   Updated: 2021/03/23 23:31:07 by emendes-         ###   ########.fr       */
/*                                                                            */
/* ************************************************************************** */

#include <stdio.h>
#include "test.h"

int g_int;
char g_char;

int	main(void)
{
	int i;
	int j;

	g_int = 1;
	g_char = 'b';
	i = 0;
	while (i < 10)
	{
		printf("Hello, World!\n");
		i = sum(i, 1);
	}

	return (0);
}

/*
** Returns the sum of a and b
*/

int	sum(int a, int b)
{
	return (a + b);
}

```

# Funções
- Tem que colocar as coisas que você quer retornar dentre parênteses
- Tem que ser declarada desse jeito aí especificamente

## Comentários
- O comentário tem que comecar com ** em todas as linhas intermediarias
- O comentário tem que ter pelo menos uma linha intermediária
- Só pode escrever texto no comentário nas linhas intermediárias

## Structs, Enums e Unions

Essas coisas falam de structs, mas se aplicam à todos esses.

- Não pode declarar struct em um arquivo *.c, só pode em um *.h
- Tem que haver apenas tabs entre `struct` e o nome da struct
- Todos os nomes de membros da struct tem que estar alinhados usando tabs
- Se for fazer um typedef da struct, ele deve ter um nome que começa com t_ e está alinhado por tabs ao nome original
- No exemplo não parece que está alinhado, mas a Norma diz especificamente que o tab deve ter 4 colunas, mas o github usa 8

## Pre-processador
- Todas as diretivas de processador entre um #if (e equivalente) e #endif dever estar identados com um espaço entre o # e a diretiva.

# Arquivo .h
- Tem que ter o escopo global alinhado por tabs, ou seja o nome das funções, uniões, structs e tudo mais tem que estar alinhado.
