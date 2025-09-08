# Escola de Segurança Cibernética - Flag Hunters (picoCTF)

> Solved by @evelyn-oliveira26
>
>> This is a CTF about Reverse Engineering

## Desafio: Flag Hunters (Engenharia Reversa)

**Introdução**  

*"Flag Hunters"* é um desafio da plataforma *picoCTF* - plataforma na qual oferece exercícios e competições voltados para segurança cibernética. Este desafio envolve assuntos como Engenharia Reversa e injeção de comandos. No entanto, o objetivo desse desafio é manipular o funcionamento do *script* (conjunto de instruções para que uma função seja executada) no terminal, para que ele revele a *flag* secreta.

* [Página do Desafio](https://play.picoctf.org/practice/challenge/472)

**Análise Inicial**

Quando começamos a resolver o desafio obtemos a seguinte descrição:

>*Lyrics jump from verses to the refrain kind of like a subroutine call. There's a hidden refrain this program doesn't print by default. Can you get it to print it? There might be something in it for you.*
*The program's source code can be downloaded here.
Additional details will be available after launching your challenge instance.*

Também possuímos algumas dicas que a própria questão traz:

>*This program can easily get into undefined states. Don't be shy about Ctrl-C.*

>*Unsanitized user input is always good, right?*

>*Is there any syntax that is ripe for subversion?*

**Interpretando a Dica**

Bom, ao meu ver, a segunda dica é a mais significativa da questão, logo, a interpretação dela foi a que consegui obter uma análise mais precisa e clara em cima do exercício.

*“Unsanitized input”* significa entrada do usuário sem validação. Esse é o cenário da vulnerabilidade: o programa não checa o que você digita, então você consegue injetar comandos que normalmente não deveria.

Isso é uma pista direta de que o programa sofre de injeção de código, e que você pode escrever algumas coisas para mudar o fluxo de execução.


**Solução da Questão**

Ao baixarmos o arquivo que a questão nos pede, notamos que o arquivo é um código em *Python*. Nesse sentido, abrimos o arquivo no ***Visual Studio Code*** para analisarmos-o.


# [![flaghunters.jpg](https://i.postimg.cc/DzCk0cP0/flaghunters.jpg)](https://postimg.cc/3yDbbm6Q) [![flaghunters2.jpg](https://i.postimg.cc/D0LMrQLq/flaghunters2.jpg)](https://postimg.cc/y36jBZfd) [![flaghunters3.jpg](https://i.postimg.cc/50ZrQKY4/flaghunters3.jpg)](https://postimg.cc/xJ35WR3h) 
# [![flaghunters4.jpg](https://i.postimg.cc/fL3FLQbq/flaghunters4.jpg)](https://postimg.cc/S2hVT5Cc)


Ao analisarmos com clareza, percebemos que no começo do código está armazenado o conteúdo de nossa *flag*.

[![flaghunters5.jpg](https://i.postimg.cc/fyPYR1JC/flaghunters5.jpg)](https://postimg.cc/n9vXdRK9)

No entanto, o ***"reader"*** (ou leitor)  começa a ler a partir do **VERSO 1**. Logo, precisamos achar uma maneira de ele começar a ler desde onde está armazenado o conteúdo de nossa *flag*.

[![flaghunters6.jpg](https://i.postimg.cc/hG0xdXXf/flaghunters6.jpg)](https://postimg.cc/d7LLMtmY)
[![flaghunters7.jpg](https://i.postimg.cc/rwXtZ1WD/flaghunters7.jpg)](https://postimg.cc/ZCHRCywm)


Um ponto importante, é que nas linhas 121 e 122, há um comando ***RETURN*** que pode ser usado para que o leitor seja forçado a ler qualquer linha específica.

[![flaghunters8.jpg](https://i.postimg.cc/Dz5JzRNG/flaghunters8.jpg)](https://postimg.cc/LqY6CQ24)

Quando clicamos em ***Launch Instance***, na página do desafio, ele nos libera um *link* para utilizarmos no terminal.

Seguindo tal lógica, abrimos o ***Webshell*** - *terminal do picoCTF*, e digitamos o *link* no terminal.

Ao pressionarmos *Enter*, o terminal irá nos mostrar a canção a partir do **VERSO 1**, como havíamos comentado.

[![flaghunters10.jpg](https://i.postimg.cc/HkNWPHFB/flaghunters10.jpg)](https://postimg.cc/VJjcJyfC)



Em uma parte do código, na parte do *"Crowd: "* acaba nos pedindo para inserir uma entrada de dados. 

Como havia dito anteriormente, lembram que na parte do código em que há um comando ***RETURN*** e um número, o leitor irá ler qualquer linha específica? Logo, iremos digitar **RETURN 0**  (já que força a função a terminar imediatamente e com sucesso, como no C/C++) para o *script* e ver o que ele nos mostra.

[![flag11.jpg](https://i.postimg.cc/X7wDzghh/flag11.jpg)](https://postimg.cc/Ln8TqjmB)

Podemos perceber que a saída nos mostra o **RETURN 0** em diversos trechos, tratando-o como uma *string* - sequência de caracteres. Para fazer o *script* interpretar o **RETURN 0** como um comando, precisamos ajustar nossa entrada de dados.

No código aberto no ***Visual Studio Code***, notamos que o programa separa seus comandos pelo ponto e vírgula **";"**. Isso significa que podemos escrever qualquer coisa antes, colocar um ponto e vírgula, para assim escrever  o comando em seguida que ele irá funcionar.

Voltando para o ***Webshell***, vamos fazer o teste:
 
[![flag12.jpg](https://i.postimg.cc/8kn1CTzD/flag12.jpg)](https://postimg.cc/BtHWY9Fw)

Com isso, o programa volta a imprimir desde a primeira linha, incluindo a *secret_intro*. Por fim, concluímos nossa missão. Encontramos a *flag*!

**Conclusão**

*Flag:*

>picoCTF{70637h3r_f0r3v3r_0099cf61}

Esse desafio nos mostrou, de forma simples e prática, como injeção de código funciona: ao manipular entradas em um programa, conseguimos alterar seu fluxo de execução para obter informações sensíveis.

A principal lição que podemos tirar é que a  validação de entrada é fundamental. Em sistemas reais, a falta dessa validação pode permitir ataques sérios como vazamento de dados ou até comprometimento completo do sistema.
