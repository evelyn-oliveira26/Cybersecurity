# Escola de Segurança Cibernética - RED (picoCTF)

> Solved by @evelyn-oliveira26
>
>> This is a CTF about Steganography

## Desafio: RED (Esteganografia)

**Introdução**

"RED" é um desafio da plataforma picoCTF - plataforma na qual oferece exercícios e competições voltados para segurança cibernética. Este desafio envolve assuntos como esteganografia - significa a prática de esconder uma informação dentro de outra, de modo que a existência da informação secreta passe despercebida. Este desafio também envolve a modificação dos bits menos significativos e codificação Base64. No entanto, o objetivo do desafio é mostrar como mensagens secretas podem ser escondidas em arquivos de imagem usando esteganografia.

* [Página do Desafio](https://play.picoctf.org/practice/challenge/460)

Essa questão consiste em treinar o uso de ferramentas para detectar e extrair dados de uma imagem fornecida, codificado em Base64. Ao decodificá-lo é possível obter a flag.

**Análise Inicial**

Quando começamos a resolver o desafio obtemos a seguinte descrição e a seguinte imagem:

>RED, RED, RED, RED

[![red1.jpg](https://i.postimg.cc/KvFNp3Tv/red1.jpg)](https://postimg.cc/NLJm5MbW)

Também possuimos algumas dicas que a própria questão traz:

>The picture seems pure, but is it though?

>Red?Ged?Bed?Aed

>Check whatever Facebook is called now.

**Interpretação das Dicas e Solução da Questão**

Analisando a primeira dica, como só temos uma única imagem conosco, isso nos leva a um único caminho lógico: checar os dados da imagem. Nesse sentido, importamos a imagem no [Notepad++](https://notepad-plus-plus.org/downloads/) - editor de texto e de código-fonte que oferece recursos avançados em comparação com o Bloco de Notas padrão. Assim que importamos, obtemos o seguinte poema:

[![red2.jpg](https://i.postimg.cc/4y9wjjvD/red2.jpg)](https://postimg.cc/q6p83b5w)

O poema particularmente é fofo, mas foquem nas letras maiúsculas do poema. Cada começo de verso possui letras maiúsculas, e se juntarmos elas montamos a seguinte frase: **CHECK LSB**.

Seguindo tal lógica, vamos procurar por dados ocultos nos bits menos significativos (LSB). Para executarmos tal comando, entraremos no site [CyberChef](https://gchq.github.io/CyberChef/) - ferramenta multifuncional on-line, criada para facilitar a análise e a decodificação de dados.

Assim que entramos no site, encontramos no canto esquerdo a aba **Operations**, nela, iremos pesquisar por *Extract LSB*.

[![red4.jpg](https://i.postimg.cc/YqqFm6gg/red4.jpg)](https://postimg.cc/qgSqPC1M)

Em seguida, na aba *Recipe*, obtemos a seguinte tabela:

[![red5.jpg](https://i.postimg.cc/dVhT5J5V/red5.jpg)](https://postimg.cc/Mn8TTJkC)

Analisando essa tabela a fundo, remetemos-a à segunda dica da questão: *"Red?Ged?Bed?Aed"*. As iniciais de cada palavra dessa dica serão nossos comandos para preencher o **Colour Pattern** - ele indica qual canal de cor e qual ordem de bits foram usados para esconder os dados. 

Assim que colocamos os comandos corretos, o site nos mostra que os LSBs do canal vermelho carregavam diversas strings idênticas em Base64 - um jeito de codificar dados binários em texto.

[![red6.jpg](https://i.postimg.cc/vZMXSq4K/red6.jpg)](https://postimg.cc/1fCp8Kc0)

 Logo, copiamos uma das diversas strings idênticas que estão no site, que já é o suficiente para decodificarmos. Optei por utilizar o site [base64decode.org](https://www.base64decode.org/pt/) para realizarmos a decodificação (o próprio CyberChef é capaz de realizar essa conversão, porém estou mais familiarizada com o base64decode):

[![red7.jpg](https://i.postimg.cc/PrRCpBds/red7.jpg)](https://postimg.cc/rK5V7ZdQ)
 

Por fim, encontramos a flag! O site já nos mostra a flag sem muitas enrolações, o que é ótimo para quem busca processos automatizados.

**Conclusão**

Flag:

>picoCTF{r3d_1s_th3_ult1m4t3_cur3_f0r_54dn355_}

Este desafio foi muito importante porque mostrou, na prática, como informações aparentemente ocultas podem estar escondidas em arquivos comuns, como imagens. 

Ele reforçou o conceito de esteganografia e a utilidade de ferramentas forenses (como Notepad++ e CyberChef) para identificar e decodificar dados escondidos. Além disso, nos mostrou que um arquivo visualmente inofensivo pode carregar conteúdo sensível em seus bits.
