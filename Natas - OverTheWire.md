# CTF - Natas (OverTheWire):

###### solved by @evelyn-oliveira26
> this is a Room about Web Security / Web Hacking.

[![image.png](https://i.postimg.cc/q7xMVM3n/image.png)](https://postimg.cc/nsMtqxTc)

Link: [Natas - OverTheWire](https://overthewire.org/wargames/natas/) 

### **Introdução**

A trilha *Natas*, do *OverTheWire*, é uma sequência de desafios focados em segurança web, projetados para ensinar, na prática, os fundamentos por trás de ataques e defesas em aplicações online. Nesta caminhada, que vai do level 0 ao level 15, cada etapa apresenta um conceito novo — desde inspeção básica de HTML até injeção SQL real, passando por manipulação de requisições HTTP, autenticação, filtros, encoding e exploração de comportamentos inesperados no servidor.

O progresso é construído de forma gradual: primeiro aprendemos a observar; depois, a entender; e finalmente, a explorar com precisão. Cada *level* esconde uma senha que só pode ser obtida analisando a página, quebrando proteções ou aproveitando vulnerabilidades específicas.

Esta trilha documenta minha jornada completa pelos *levels* 0 a 15, explicando cada solução, ferramentas usadas, erros cometidos e o aprendizado tirado de cada desafio. O objetivo é compartilhar conhecimento e mostrar que segurança web se aprende praticando.

---
## Natas Level 0

*Natas Level 0* é o primeiro desafio dessa trilha que iremos trabalhar! Como este é um desafio introdutório, não atinge tamanha complexidade ao resolvê-lo. Bom, quando acessamos a URL que o site do *Natas* nos deixou, nos deparamos com a seguinte frase: 

> You can find the password for the next level on this page.

Seguindo a lógica da dica fornecida, iremos inspecionar a página nas *DevTools* → *F12* no teclado, e ao inspecionar um pouco já encontramos a nossa senha para a próxima fase:

> The password for natas1 is 0nzCigAq7t2iALyvU9xcHlYN4MlkIwlq


[![image.png](https://i.postimg.cc/xCXVkjbG/image.png)](https://postimg.cc/mzW5Jsjh)


### Perguntas a serem feitas:

* **Onde isso é útil em testes de segurança reais?**

    **Resposta:** Na análise inicial de aplicações web, procurando vazamento de senhas, chaves ou informações escondidas.

* **O que isso ensina sobre práticas inseguras?**

    **Resposta:** Ensina que nunca se deve colocar informações importantes no código-fonte, mesmo que não apareça na página.

---
## Natas Level 1
O segundo desafio não se diferencia muito do primeiro. Agora ao entrarmos na página do desafio, nos deparamos com essa frase:

> You can find the password for the next level on this page, but rightclicking has been blocked!

No desafio anterior, poderíamos ter resolvido o desafio clicando com o **botão direito** do *mouse*, e inspecionar a página. No entanto, nesse exercício o site bloqueou o clique direito para não irmos por esse atalho. 

**Resolução:** Os atalhos existentes no computador não foram bloqueados, e um deles é o **Ctrl + U**, que ao pressionarmos essas teclas, elas irão nos levar direto para o código-fonte do site. Logo, quando analisamos o código-fonte do site, mais uma vez a senha para o próximo nível está lá:

> The password for natas2 is TguMNxKo1DSa1tujBLuZJnDUlCcUAPlI

### Perguntas a serem feitas:

* **O que o bloqueio de funções básicas prova para o atacante?**

    **Resposta:** Que existem outros atalhos (e vulnerabilidades) a serem explorados.

---
## Natas Level 2

Bom, neste desafio nos deparamos com a seguinte frase:

> There is nothing on this page.

A princípio, iremos inspecionar o código-fonte da página. Ao apertarmos **Ctrl + U**, podemos ver nas linhas finais do código o seguinte arquivo:

[![image.png](https://i.postimg.cc/5yynbgvg/image.png)](https://postimg.cc/9w3GBGLw)

Logo quando abrimos-o, nos deparamos com uma imagem preta, que também ao inspecionarmos, não nos leva a nada, porém quando abrimos a imagem que nos leva a uma tela preta, o nosso link de site acaba mudando para este:

[![image.png](https://i.postimg.cc/Rh28Yy89/image.png)](https://postimg.cc/FkgDdWNn)

Analisando este link, logo após o **".org"**, possuímos o seguinte caminho de diretórios: **/files/pixel.png**. Seguindo a lógica do caminho de diretórios, se assumirmos que **/pixel.png** seria a imagem da tela preta, ao apagarmos-a e ficarmos apenas com **/files**, poderíamos acessar os arquivos importantes do site.

[![image.png](https://i.postimg.cc/ZRsKWYBZ/image.png)](https://postimg.cc/Hc5CKg9P)

Dito e feito! Encontramos as vulnerabilidades desse site. E ao acessarmos o arquivo **users.txt**, a senha para a próxima fase do *Natas* está exposta junto ao arquivo.

> natas3: 3gqisGdR0pjm6tpkDKdIWO2hSvchLeYH

### Perguntas a serem feitas:
* **Qual é a lição de segurança aprendida neste nível?**

    **Resposta:** Exposição de diretórios e arquivos acaba sendo uma vulnerabilidade severa.

---
## Natas Level 3
Nesta fase, nos deparamos com a mesma frase do nível anterior:

> There is nothing on this page.

A princípio, poderíamos inspecionar a página para irmos em busca de alguma pista, porém ao inspecionar a página ou exibir o código-fonte dela, não encontramos nada muito útil. 
No entanto, possuímos uma ferramenta chamada ***robots.txt*** - um arquivo usado por sites para indicar aos rastreadores da web e outros robôs visitantes quais partes do site eles têm permissão para acessar.

Ao implementarmos o ***robots.txt*** no diretório do site, nos deparamos com a seguinte imagem:

[![image.png](https://i.postimg.cc/2SNHs4H7/image.png)](https://postimg.cc/7fXM7Tr5)

Essa nova página já nos fornece o **caminho** para explorarmos as vulnerabilidades cada vez mais. Ao adicionarmos junto ao link do site, obtemos:

[![image.png](https://i.postimg.cc/597yKgty/image.png)](https://postimg.cc/4ncXmzVR)

Encontramos mais um arquivo **".txt"**, e ao acessá-lo descobrimos a senha para o próximo nível do *Natas*:

> natas4: QryZXc2e0zahULdHrtHxzyYkj59kUxLQ

### Perguntas a serem feitas:

* **O que esse nível nos ensina sobre o uso do "robots.txt"?**

    **Resposta:** Ele mostra que o **robots.txt** serve para orientar robôs de busca, mas não para proteger conteúdos. Ou seja, ele não impede ninguém de acessar os caminhos listados nele.

---
## Natas Level 4

No nível 4 do *Natas*, obtemos a seguinte frase:

> Access disallowed. You are visiting from "http://natas4.natas.labs.overthewire.org/index.php" while authorized users should come only from "http://natas5.natas.labs.overthewire.org/".

Quando inspecionamos o código-fonte da página, não conseguimos achar nada muito interessante. Por isso, iremos usar uma ferramenta poderosíssima em segurança cibernética, o **Burp Suite** - um software desenvolvido em Java  para a realização de testes de segurança em aplicações web. Ele está insataldo juntamente a **Kali Linux** - uma distribuição Linux de código aberto, ela permite aos usuários realizar testes de penetração avançados e auditorias de segurança.

Logo, iremos acessar o **Burp Suite** na máquina da virtual e procuraremos por informações importantes (gostaria de dizer que não consegui obter imagens/prints dentro da **Kali**, meu computador apenas tira capturas de tela de sua  interface própria, tentei tirar fotos pelo celular, porém as fotos estão pixeladas, quando você tira foto de uma tela mesmo, sabe? Mas irei descrever o passo a passo da questão).

Ao acessarmos o **Burp Suite**, iremos ir na aba **Proxy** → **Intercept** → **Intercept is on**. Isso começará a interceptação do tráfego de rede. Logo, iremos acessar a URL do *Natas4* no navegador dentro da **Kali**, e assim, os dados daquele site serão capturados. No entanto, podemos editar esses dados para explorar cada vez mais as vulnerabilidades: ao clicarmos com o **botão direito do mouse** na URL que o **Burp Suite** capturou, e clicar em **Send to Repeater**, esses dados capturados irão para a aba **Repeater** - aba onde podemos editar esses dados.

Se formos analisar os dados, podemos perceber que há um com o cabeçalho **Host:** e outro com o cabeçalho **Referer:**, o **Host** armazena a URL original do Natas4 e o **Referer** também, porém com os caminhos  *index.php* adicionados a URL, que indica o endereço da página web anterior de onde o link para a página atual foi clicado. Esses dois cabeçalhos possuem certa ligação, como expliquei acima. Seguindo tal lógica, não poderíamos modificar o **Host** já que ele é o domínio original do site, mas podemos alterar o **Referer** para burlar o controle de acesso.

Quando alteramos o **Referer** para "http://natas5.natas.labs.overthewire.org/" que é justamente a URL que a própria questão nos fornece no início dela, e clicamos em  **Send**,  iremos obter acesso a resposta:

> Access granted. The password for natas5 is 0n35PkggAPm2zbEpOU802c0x0Msn1ToK

### Perguntas a serem feitas:

* **Qual é o propósito do Burp Suite em testes de segurança e por que ele é útil neste desafio?**

    **Resposta:** O **Burp Suite** serve para interceptar e alterar requisições enviadas ao servidor, permitindo analisar como a aplicação trata cada cabeçalho. No *Natas Level 4*, ele é útil porque nos deixa modificar o **Referer**, testando se o site realmente depende desse valor para liberar o acesso - o que confirma a vulnerabilidade.

---
## Natas Level 5
No início do *Natas 5*, obtemos a seguinte frase:

> Access disallowed. You are not logged in.

O primeiro pensamento sempre, sempre será inspecionar a página, logo, iremos inspecioná-la em busca de mais informações. Enquanto inspecionamos, na aba **Sources**, dentro do código possui esta linha:

> This stuff in the header has nothing to do with the level.

Como o próprio *Natas* diz... então não está na aba **Sources**.

Ao fazermos uma longa busca, na aba **Application** → **Cookies**, obtemos a seguinte imagem:

[![image.png](https://i.postimg.cc/vBVXXn5T/image.png)](https://postimg.cc/5Yfw267W)

Possuímos três *Cookies* do próprio site - *Cookies* são pequenos arquivos de texto que um servidor web envia para o seu navegador quando você visita um site - porém, repare no terceiro *Cookie*, ele se chama **loggedin** e possui valor **0**. Se seguirmos a lógica das matérias de Eletrônica Digital, nela, o **0** significa **False**, e **1** significa **True**, então se alterarmos o valor do *Cookie* para **1** e atualizarmos a página:
 
 > Access granted. The password for natas6 is 0RoJwHdSKWFTYR5WuiAewauSuNaBXned.

 Pronto, conseguimos a senha para a próxima fase!

 ### **Perguntas a serem feitas:**

* **Por que analisar cookies é um passo importante no estudo de segurança web?**

    **Resposta:** Porque cookies podem armazenar informações de autenticação e, se forem mal configurados, permitem que alguém altere o estado de login ou acesso apenas mudando seus valores.

---
## Natas Level 6

Chegando ao nível 6  do *Natas*, temos a seguinte imagem:

[![image.png](https://i.postimg.cc/xT2NF4wV/image.png)](https://postimg.cc/Hj6LrBW6)

A imagem nos diz para digitarmos algo como uma chave secreta, e ao lado inferior direito, temos a frase **"View sourcecode"**. Ao clicarmos, somos redirecionados para o código-fonte da página:

[![image.png](https://i.postimg.cc/76HQV9qz/image.png)](https://postimg.cc/PL74fmpf)

Como podemos ver ali em cima novamente, temos a seguinte frase para o primeiro cabeçalho:

> This stuff in the header has nothing to do with the level.

Bom, então se não está por ali, acredito que por ser bem intuitivo, está na parte colorida do código. Quando lemos o código colorido, podemos ver que a resposta se encontra nesta parte mesmo, agora só nos falta manipular este código para conseguirmos a chave secreta.

Se repararmos bem na primeira linha do código colorido, ela possui a sentença:

> include "includes/secret.inc";

A parte **"secret.inc"** do código possui uma **/** **(barra)** depois de **"includes"**, que é exatamente o que usamos para determinar caminhos em URL's de sites. Então, **"secret.inc"** seria um arquivo dentro do arquivo **"includes"**, e ao colocarmos este caminho na URL, obtemos:

[![image.png](https://i.postimg.cc/L8sWLN6p/image.png)](https://postimg.cc/xcWgSGzx)

Achamos a chave secreta! Vamos voltar para a página inicial e digitarmos essa chave.


Quando digitamos essa chave, obtemos nossa senha para o *Natas 7*:

> Access granted. The password for natas7 is bmg8SvU1LizuWjx3y7xkNERkHxGre0GS

### **Perguntas a serem feitas:**

 *  **Por que entender a estrutura de diretórios de um site é útil ao analisar vulnerabilidades?**

    **Resposta:** Porque a organização de pastas revela onde arquivos importantes podem estar guardados. Se o servidor não protege esses diretórios, basta acessar o caminho diretamente pela URL para obter informações confidenciais, como chaves, senhas ou configurações.

---
## Natas Level 7
Nesta fase, ao ingressarmos nela, obtemos a seguinte imagem:


[![image.png](https://i.postimg.cc/50MbSqW2/image.png)](https://postimg.cc/nsTyHmLy)

[![image.png](https://i.postimg.cc/fRrbm9bH/image.png)](https://postimg.cc/LJjRMhLf)

A principal frase dessas imagens é a **"Home About"** que são duas palavras separadas e clicáveis, quando clicamos em cada uma separadamente, obtemos frases diferentes, como podemos ver. Ali embaixo irei explicar sobre elas.

Inicialmente, iremos inspecionar a página. Ao executar as **Dev Tools**, encontramos uma pista escondida em forma de comentário:

>  hint: password for webuser natas8 is in /etc/natas_webpass/natas8

Bom, ao que tudo indica parece ser um caminho para adicionarmos na URL, porém ao adicionarmos este caminho a nossa URL, caímos direto no **erro 404** (quando a página está fora do ar, ou não encontrada), logo, voltamos à estaca zero.

De acordo com algumas pesquisas, pude perceber que **/etc/** não é um caminho válido em URLs, porque **/etc** é um diretório interno do **Linux**, não do site, e nenhum servidor web expõe diretórios do sistema pela URL. Logo, descartamos a possibilidade dessa dica ser um **caminho**.

No entanto, ao avaliarmos esta dica, ela pode não ser o caminho real para onde queremos chegar, porém podemos confirmar que esta dica tem alguma coisa a ver com isso, apenas pelo formato. Logo, ao pesquisarmos o conceito mesmo de uma URL e suas partes, obtemos diversos resultados, porém achei uma imagem boa para ilustrar:

[![image.png](https://i.postimg.cc/QC3zz0fT/image.png)](https://postimg.cc/VrK4rBQf)

Esta imagem vem do site [tecnoblog.net](https://tecnoblog.net/responde/o-que-e-url/)!

Ao observarmos a imagem acima, percebemos que uma URL pode carregar não apenas o caminho de um arquivo, mas também parâmetros enviados ao servidor, geralmente após o símbolo **"?"**. Esses parâmetros são usados para solicitar informações específicas ao servidor, como páginas internas, conteúdos dinâmicos ou resultados de consultas.

Com isso, voltamos ao *Natas 7* e notamos que ao clicar nos botões **Home** e **About**, o resto da URL muda para algo como:

> page=home

> page=about


Se compararmos com a da imagem, conseguimos perceber que **page** é a **chave** do parâmetro do site! E se o código estiver usando o **page** dentro de uma função que lê arquivos, então poderíamos substituir o **valor** original (**"home”** e **“about"**) por esse caminho que a dica nos trouxe:

> ?page=/etc/natas_webpass/natas8


Ao substituirmos, aqui está a senha para o *Natas 8*:

> xcoXLmzMkoIP9D7hlgPlh9XD7OgLAe5Q

### **Perguntas a serem feitas:**

* **Como o formato de uma dica pode indicar que ela é um caminho interno e não uma rota acessível?**

    **Resposta:** Caminhos iniciados por “/” e contendo diretórios típicos de Linux, como /etc/, mostram que o arquivo está no sistema, não na estrutura pública da aplicação.

---
## Natas Level 8
Chegamos ao nível 8 do *Natas*! Nesta fase, a página inicial nos mostra:

[![image.png](https://i.postimg.cc/5N92XVJb/image.png)](https://postimg.cc/7bckRjbW)

Podemos ver que é igual à página inicial do nível 6. Logo, vamos clicar em **"View sourcecode"** para inspecionarmos o código-fonte da página.

Como de costume, o código-fonte nos deixou um comentário sobre o cabeçalho inicial:

>  This stuff in the header has nothing to do with the level.

Então, iremos ignorar essa parte. 

Um pouco abaixo desse cabeçalho, temos um código colorido novamente, que ao lermos, já nos indica que a resposta está por ali.

[![image.png](https://i.postimg.cc/K82S17B3/image.png)](https://postimg.cc/vc3SjVPG)

E ao analisarmos, é um código que possui uma função chamada **encodeSecret**, que retorna:

> bin2hex(strrev(base64_encode($secret)))

No **return** percebemos que a **senha secreta** passa por três transformações, nesta ordem:

* **base64_encode()**
* **strrev()** (inverte a string)
* **bin2hex()**

Para decriptografar, começamos de fora para dentro, como se estivéssemos abrindo um presente mesmo, já que não há sentido em abrir um presente pelo meio.

A função **bin2hex()**, apesar do nome, não converte binário real para hexadecimal. Na verdade, ela pega cada byte da string original e o transforma em sua representação hexadecimal. Por isso, ao desfazer essa etapa, precisamos converter a chave que recebemos em **hexadecimal**, de volta para **string** para continuar o processo.

 Com decodificadores online, conseguimos fazer todo o trabalho. Ao decodificar a primeira parte de **hexadecimal** → **string**, obtemos:

 > ==QcCtmMml1ViV3b 

Certo, agora passamos para o comando **strrev**, que seria o **String Reverse**:

> b3ViV1lmMmtCcQ==

Ao reverter essa string, agora só falta a codificação **Base64**. Ao decodificá-la, obtemos:.

> oubWYf2kBq

Essa é a nossa chave secreta que precisamos colocar na página inicial do desafio. Ao colocarmos esta chave, obtemos:

> ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t
 
 E *voilà*! Conseguimos a senha para o *Natas 9*!

 ### **Perguntas a serem feitas:**

* **Por que o processo de descriptografia é feito de fora para dentro?**

    **Resposta:** Porque a função original aplica as transformações de dentro para fora; portanto, para desfazer o efeito, precisamos inverter a ordem.
---
## Natas Level 9
No *Natas Nível 9*, a página inicial nos mostra a seguinte imagem:

[![image.png](https://i.postimg.cc/xCBPwTYt/image.png)](https://postimg.cc/PpzZZHCw)

A frase nos diz: **"Ache palavras contendo: "**, vamos digitar qualquer coisa para ver o que aparece:

[![image.png](https://i.postimg.cc/VLs6yyLj/image.png)](https://postimg.cc/nM5Z7Pmz)

Se eu digito **"ing"**, o site me mostra as palavras contendo essa parte, nesse caso, tinha mais palavras para baixo, pois no inglês existe inúmeras palavras contendo **"ing"**, mas usei esse exemplo para mostrar que o site nos retorna tipo um dicionário.

Se inspecionarmos o código-fonte da página, podemos ver este código colorido, que acredito que ajudará na busca da senha para o *Natas 10*.

[![image.png](https://i.postimg.cc/SKPT4phR/image.png)](https://postimg.cc/LqzBkwhF)

Pesquisando a fundo, vemos que este é um código em **PHP** - linguagem de programação. Vamos entender o que esse código está fazendo:

Dentro do primeiro *if*, o código verifica se existe um parâmetro chamado **"needle"**. Se existir, ele é atribuído à variável **$key**:

Já no segundo *if*,  se **$key** não estiver vazia, executa o comando:

>     passthru("grep -i $key dictionary.txt");

Ao pesquisarmos o que exatamente este comando faz, consegui uma resposta interessante no site [oreilly](https://www.oreilly.com/library/view/php-in-a/0596100671/re72.html)!

> The `passthru()` function runs an external program, specified in the first parameter. It prints everything output by that program to the screen.

Que em português seria:

> A função `passthru()` executa um programa externo, especificado no primeiro parâmetro. Ela imprime na tela tudo o que for produzido por esse programa.

Aí que entra o grande perigo: o código utiliza a função **passthru()** para executar um comando **grep** no sistema operacional. 

**grep** é um comando de processamento de texto usado para procurar linhas que contêm uma palavra-chave específica em um arquivo.

Aí junta esses dois comandos + algo digitado pelo usuário, e como não há validação nenhuma, é possível **injetar comandos adicionais** diretamente na entrada de dados da página inicial.

Andei pesquisando, e existem muitos comandos possíveis para testar em injeções com **grep**, mas nem todos funcionam, porém um padrão muito conhecido é o uso do **ponto e vírgula (;)**.
 O **ponto e vírgula** no terminal **Linux** é um operador de controle que permite executar vários comandos em sequência na mesma linha.

Ou seja, vamos analisar essa parte novamente do código em **PHP**:

 > grep -i $key dictionary.txt

Se onde está **$key** for qualquer coisa que o usuário digitar, e o usuário injetar um comando para assumir o valor de **$key**, ele poderá obter informações muito importantes. Há um comando conhecido, que se chama **ls -al** - ele lista todos os arquivos do diretório atual com detalhes, e isso é muito importante para explorarmos as vulnerabilidades do site.

Se eu entrar com esses comandos juntos: **"; ls -al"**, obtemos isso:

[![image.png](https://i.postimg.cc/SKnzznnH/image.png)](https://postimg.cc/PLkqgrzM)

Certo, mas ainda não é isso que estamos procurando, existe outra injeção de comando que é **../../../**, esses dois pontos e uma barra é uma técnica que permite que um atacante se mova pelos diretórios do sistema de arquivos de um servidor, acessando arquivos e diretórios que não deveriam estar disponíveis. Ao aplicar juntamente com o **"; ls"**, obtemos:

[![image.png](https://i.postimg.cc/XvWYnXwd/image.png)](https://postimg.cc/Xr2b8j1Y)

O **ls** sozinho é um comando usado para listar arquivos e diretórios em um diretório. Então se eu combinar o **";"** com o **"ls"** e com o **"../../../"** , eu executo todo esse comando na mesma linha.

Se lembram do nível 7 do *Natas*, em que conseguimos analisar as informações para a senha, a partir do diretório **"etc"**, bom, aqui ele aparece novamente, então vamos utilizar esse diretório juntamente com as informações necessárias para acessarmos a senha do *Natas 10*, porém ao invés de só listar arquivos, iremos rodar um comando para ler o conteúdo do arquivo. O comando é o:

>     ; cat /etc/natas_webpass/natas10

Ao digitarmos isso na entrada de dados conseguimos achar a senha para o *Natas 10*:

> t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu

### **Perguntas a serem feitas:**

* **O que permitiu a injeção de comandos no Natas 9?**

    **Resposta:** A ausência de validação no parâmetro **needle**, que foi passado diretamente para o **grep** dentro de **passthru()**.

---
## Natas Level 10

O *Natas 10* é um nível muito parecido com o *Natas 9*, só que agora ele é assim:

[![image.png](https://i.postimg.cc/0j0MD37W/image.png)](https://postimg.cc/gLr2PgS8)

Agora, eles adicionaram a frase que diz: **"Por questões de segurança, agora nós filtramos em certos caracteres"**. E realmente, ao inspecionarmos o código-fonte da página, podemos ver o seguinte código:

[![image.png](https://i.postimg.cc/bYgw017v/image.png)](https://postimg.cc/DmWhn4yV)

Ele é bem parecido com o código do nível anterior, porém agora dentro do segundo *if*, possuímos um outro *if*, que contém o comando **preg_match** - esse comando realiza uma correspondência global de expressão regular, as famosas **REGEX**. Ao conferirmos o que o **preg_match** está procurando, podemos ver que são os caracteres:

 >     /[;|&]/
 
 E se o comando encontrar esses caracteres, iremos obter a saída:

>     Input contains an illegal character!

Logo, percebemos que não conseguimos seguir o caminho anterior, no qual injetamos comandos com os caracteres especiais, então precisamos achar outra solução para esse problema.

Vamos pensar, se o site sempre nos retorna correspondências de palavras que estão armazenadas naquele dicionário, então a senha para o *Natas 11*, está dentro deste grande dicionário. Anteriormente ao digitarmos "(comando) **/etc/natas_webpass/natas10**", de cara encontrávamos a senha para o próximo nível, mas como não podemos digitar caracteres especiais para utilizar as injeções de comando, podemos ao menos, testar aleatoriamente qualquer letra que possivelmente estaria dentro da senha, para assim, caso essa letra esteja contida na senha, o site nos liberaria a resposta.

Ao fazermos o teste com a letra **"a"**, o *Natas* já nos libera a senha para o próximo nível! A senha no caso, tinha a correspodência para o **"A" (maiúsculo**), porém o que faz o site acabar liberando a senha é por conta do **grep -i** no código - ele ignora diferença entre maiúsculas e minúsculas.

E se tivéssemos colocado algum número para teste e tivessem encontrado uma correspondência para aquele número, teria dado certo também!

[![image.png](https://i.postimg.cc/cLR9679c/image.png)](https://postimg.cc/CRKHQ8VZ)

> natas11: UJdqkK1pTu6VLt9UHWAgRZz6sVUZ3lEk

### **Perguntas a serem feitas:**
* **Qual é a lição principal de segurança que o *Natas Level 10* quer ensinar?**

    **Resposta:** Bloquear caracteres não impede que informações sensíveis sejam expostas se a lógica principal do sistema permitir acessos indevidos.
---
## Natas Level 11
Chegamos ao **Natas Nível 11*! Nele contém a seguinte página inicial:

[![image.png](https://i.postimg.cc/L808GfR6/image.png)](https://postimg.cc/k2KCb2Bk)

Como a própria frase menciona sobre os **Cookies**, vamos inspecioná-los:

[![image.png](https://i.postimg.cc/tg4n0y88/image.png)](https://postimg.cc/75jZ0vHN)

Bom, obtemos **3 cookies** diferentes, mas o que realmente vai importar é aquele em que contém o nome: **data** e o domínio: **natas11...**

Quando conferimos o valor desse cookie, ele está assim:

> HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyIxTRg%3D

Se clicarmos em **Show URL-decoded**, na parte inferior, o valor do **cookie** altera para:

> HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyIxTRg=

O que realmente altera é o **"%3D"** para **"="**. A princípio, vou conferir o código-fonte da página para ver se há alguma pista escondida dessa criptografização.

[![image.png](https://i.postimg.cc/W4y6pXLS/image.png)](https://postimg.cc/3ygDnjwD)

Ao lermos essa linha, percebemos que se retrata aos **cookies** que estávamos olhando:

>     $tempdata = json_decode(xor_encrypt(base64_decode($_COOKIE["data"])), true);

E que estão codificados em **Base64**. 

Seguindo tal lógica, se decriptografarmos a chave que possuímos, obtemos: 

[![image.png](https://i.postimg.cc/5ybmDjWg/image.png)](https://postimg.cc/0MXmwkQK)
 
 É um monte de caracter estranho, mas olhando novamente na linha do código, percebemos que **xor_encrypt()** precede **base64_decode()**  .

 Então, vamos dar uma olhada na criptografia **XOR**:

 No site da [Wikipedia](https://en.wikipedia.org/wiki/XOR_cipher), pude pesquisar mais a fundo. A criptografia **XOR** utiliza de três parâmetros: 
 * **Texto Simples (Plaintext):** é a mensagem original, legível, que se deseja criptografar.
 * **Chave (Key):** É um valor secreto, geralmente uma sequência de bits, usado em conjunto com o Texto Simples para realizar a operação XOR.
 * **Texto Cifrado (Ciphertext):** É o resultado da operação XOR bit a bit entre o Texto Simples e a Chave. É a mensagem ilegível que é transmitida.

E ao analisarmos o código **PHP** novamente, percebemos que já temos o **Texto Simples** e o **Texto Cifrado**, nos falta só a **Chave**.

>     Texto Simples: "showpassword"=>"no", "bgcolor"=>"#ffffff"
>     Chave: ???
>     Texto Cifrado: HmYkBwozJw4WNyAAFyB1VUcqOE1JZjUIBis7ABdmbU1GIjEJAyIxTRg%3D

Para descobrirmos a chave, faremos bom proveito das informações que já possuímos. Se entrarmos no site [CyberChef](https://gchq.github.io/CyberChef/), e utilizarmos as funções **XOR** e **From Base64**, conseguimos a **chave**. 

Detalhe: Tanto o **xor_encrypt**, quanto o **base64_decode**, vêm depois do comando **json_decode**, então no caso o **texto simples** para usarmos no **CyberChef** seria:

>     {"showpassword":"no","bgcolor":"#ffffff"}

Que está codificado em **JSON** - um formato de texto leve para intercâmbio de dados estruturados, amplamente usado para comunicação entre servidores e aplicações web.


[![image.png](https://i.postimg.cc/J4NZXRJF/image.png)](https://postimg.cc/VdNJQQK9)

Ao utilizarmos o **CyberChef**, obtemos o que seria a nossa chave, repetidas vezes:

>     eDWo

Por fim, ainda no **CyberChef**, trocamos a parte **"Key"** para a chave em que acabamos de encontrar, e o **"Input"** para:

>     {"showpassword":"yes","bgcolor":"#ffffff"}

que é o comando que vimos no final do código.

[![image.png](https://i.postimg.cc/XJn1FsDn/image.png)](https://postimg.cc/1gYK1rQd)

Se clicarmos em **Bake**, obteremos o real valor do **cookie** que precisamos para garantir acesso ao *Natas 12*.

[![image.png](https://i.postimg.cc/13cp6yxV/image.png)](https://postimg.cc/hXvzRWtK)

Logo, é só trocar o valor original do **cookie** para o valor que acabamos de encontrar em **Base64**.

[![image.png](https://i.postimg.cc/gJK5BCLQ/image.png)](https://postimg.cc/S2JDntrf)

*Finalmenteeeee!* Encontramos a senha para o *Natas 12*.

> natas12: yZdkjAYZRd3R7tq7T5kXMjMJlOIkzDeB

### **Perguntas a serem feitas:**

* **O que é o algoritmo XOR e por que ele é usado em desafios como o Natas 11?**

    **Resposta:** XOR é uma operação lógica que compara dois bits e retorna 1 apenas quando eles são diferentes. É usado porque é simétrico e reversível:

>     A XOR B = C
>     C XOR B = A
>     C XOR A = B

Embora seja muito fraco quando a chave é reutilizada.

---
## Natas Level 12
Vamos agora para o *Natas Nível 12*, nele, a página inicial nos mostra:

[![image.png](https://i.postimg.cc/bwYFmF3r/image.png)](https://postimg.cc/zVMjBpmY)

Ela pede para carregarmos um arquivo **JPEG** - um formato de arquivo de imagem - de no máximo 1 KB (kilobyte).

Então, ao seguirmos as instruções e colocarmos uma imagem aleatória de no máximo 1 KB, obtemos isso:

[![image.png](https://i.postimg.cc/YqPmPvxf/image.png)](https://postimg.cc/bsQJDNWs)

E ao clicarmos nesse link, é a imagem que carregamos para o site. Porém podemos perceber que o nome do arquivo mudou para um nome aleatório.

É melhor darmos uma olhada no código-fonte da página.

[![image.png](https://i.postimg.cc/0Q3LFgVP/image.png)](https://postimg.cc/gXVSL79T)

Esse código é escrito em **PHP**, e tem como principal objetivo receber e salvar um arquivo enviado pelo usuário, garantindo que o arquivo salvo tenha um nome único e aleatório dentro de um diretório específico, que foi o que aconteceu no meu *upload* ali em cima.

Bom, podemos carregar diferentes imagens e o código nos mostrará diversas frases (condições dos *if* finais), mas não iremos chegar em algum lugar.

 Nós precisamos realizar um **ataque de *upload* de arquivos**. Esse ataque consiste em carregarmos alguma coisa com a habilidade de executar comandos ao mesmo tempo. E, seguindo tal lógica, como o site está escrito em **PHP**, então devemos carregar um arquivo em **PHP**, para conseguirmos enganar o servidor e ele entender que o arquivo que implementei faz parte do código.

 Para realizarmos esse tipo de ataque, precisamos ter essas 3 condições:

* O site deve permitir upload;
* O diretório de upload deve ser conhecido, porque mesmo que enviamos um arquivo malicioso para o servidor, precisamos encontrá-lo e acessá-lo;
* O servidor deve processar o arquivo malicioso como PHP. 

Bom, então o próximo passo será escrever o arquivo **PHP** para carregar no site.

Ao pesquisar um pouco sobre comandos **PHP**, achei esse bem interessante:

>     <?php echo file_get_contents('nome_do_arquivo.extensão'); ?>

A função **file_get_contents()** é usada para ler todo o conteúdo de um arquivo ou de uma URL e retornar esse conteúdo como uma única string. Então, podemos adicionar o diretório para o *Natas 13*, que são aqueles diretórios que usamos nos níveis anteriores. Ficaria algo mais ou menos assim:

>     <?php echo file_get_contents('/etc/natas_webpass/natas13'); ?>

Essa será o nosso comando malicioso para injetarmos no site, porém não é simplesmente só enviar esse arquivo, pois ao enviarmos, mesmo com a extensão **PHP**, o site interpretou como **JPG**.

[![image.png](https://i.postimg.cc/Rh84XqDY/image.png)](https://postimg.cc/WqMB4pjm)

Logo, uma ferramenta poderosíssima, cujo qual podemos alterar o código-fonte do código, é o **Burp Suite** -  ele me permite fazer alterações e manipular dados que estão sendo enviados ao servidor (como expliquei no *Natas 4*).

Como havia mencionado anteriormente, não consigo fazer capturas de tela na **Kali**, então vou narrar os passos.

Ao entrar no **Burp Suite** pela **Kali Linux**, iremos na aba **Proxy** → **Intercept** → **Open Browser**. Quando abrimos o navegador, iremos digitar a URL para ingressar no *Natas 12*, e ao ingressarmos, fazemos *upload* de uma imagem aleatória mesmo, como no começo do nível.

Voltando ao **Burp Suite**, vamos em **Proxy** → **HTTP history**, e lá conseguimos ver que o **Burp** já captou a URL do *Natas*. Agora, para alterarmos o código, clicamos com o **botão direito** na URL que desejamos, e em seguida **Send to Repeater**. Por fim, vamos até a aba **Repeater** para fazermos as alterações.

Parte do meu código original estava assim:

> Content-Disposition: form-data; name="filename"

> t8slbfnxcm.jpg

Então, irei mudar onde está **jpg** para **php**, e no fim do código injetar aquele comando para ler conteúdo de arquivos, como havia mencionado.

Agora, ao ler o código-fonte da página o arquivo de **"upload/emsvlu0ppz.php"** estará disponível para colocarmos como caminho do site.

E conseguimos! Esta é a senha para o *Natas 13*:

> trbs5pCjCrkuSknBBKHhaBxq6Wm1j3LC

### **Perguntas a serem feitas:**
*  **Por que o navegador não permite trocar a extensão, mas o Burp Suite permite?**

    **Resposta:** Porque o navegador segue o formulário HTML rigidamente, enquanto o Burp permite interceptar e editar manualmente a requisição HTTP antes do envio.

---
## Natas Level 13

O *Natas 13* é um nível muito parecido com o anterior! Vamos dar uma olhada. 

[![image.png](https://i.postimg.cc/jS6rBR3D/image.png)](https://postimg.cc/dh0XycYF)

Agora, eles dizem que por razões de segurança, aceitam somente arquivos de imagem. E isso fica explicíto no código-fonte da página:

[![image.png](https://i.postimg.cc/0jpsxx5d/image.png)](https://postimg.cc/q6MYXP3z)

Nessa parte, em específico:

[![image.png](https://i.postimg.cc/SNk08BNH/image.png)](https://postimg.cc/BtYwfwFC)

Esse nível utiliza praticamente da mesma dinâmica do *Natas 12*, precisamos novamente tentar alterar o código-fonte da página, para injetarmos comandos e conseguir a senha.

O comando que iremos injetar será o mesmo, porém agora para o *Natas 14*, e faremos tudo isso no **Burp Suite**:

>     <?php echo file_get_contents('/etc/natas_webpass/natas14'); ?>

Novamente, entramos no **Burp Suite**, vamos em **Proxy** → **Intercept** → **Open Browser**. Quando abrimos o navegador, iremos digitar a URL para ingressar no *Natas 13* e fazemos algum *upload* de imagem aleatório.

Voltando ao **Burp Suite**, vamos em **Proxy** → **HTTP history**, e lá conseguimos ver que o **Burp** já captou a URL do *Natas*. Agora, para alterarmos o código, clicamos com o **botão direito** na URL que desejamos, e em seguida **Send to Repeater**. Por fim, vamos até a aba **Repeater** para fazermos as alterações.

Bom, parte do meu arquivo está assim:

>phfsdrsg10.jpg

>------WebKitFormBoundaryUSmFSzemzibzgG1s

>Content-Disposition: form-data; name="uploadedfile"; filename="png-clipart-julia-high-level-programming-language-dynamic-programming-language-computer-programming-julie-text-logo_11zon_11zon.jpg"
Content-Type: image/jpeg

> ÿØÿà...

Notem esse **"ÿØÿà"**, ao pesquisarmos sobre ele, descobrimos que **"ÿØÿà"** são bytes mágicos do arquivo **JPEG** que contém informações essenciais do cabeçalho da imagem. Não consegui copiar o que vem após o **"ÿØÿà"**, mas é o cabeçalho para confirmar que aquilo é um arquivo em **JPEG**.

Como o *Natas 13* valida apenas o início do arquivo - verificando os **bytes mágicos** de **JPEG** - podemos usufruir dessa característica: mantemos os **bytes mágicos** e no lugar do cabeçãho **JPEG**, injetamos o comando em **PHP**.

Também não podemos esquecer de mudar:

>phfsdrsg10.jpg

Para:

>phfsdrsg10.php

Isso vai enganar o mecanismo de *upload*, que vai acreditar estar recebendo uma imagem válida.

Ao clicarmos em **Send**, podemos ver o novo código-fonte, que nos mostra o caminho para adicionarmos a URL do *Natas 13*.

> upload/j3495vzmar.php

E ao colarmos esse caminho na URL, e atualizar a página, encontramos a senha para o *Natas 14*!

> z3UYcr4v4uBpeX8f7EZbMHlzK4UR2XtQ

### **Perguntas a serem feitas:**

* **Quais são os magic bytes característicos de um arquivo JPEG?**

    **Resposta:** Um arquivo JPEG começa com:

    **FF D8** (representado como ÿØ)

    seguido por **FF E0** (representado como ÿà)

Esses bytes indicam ao sistema que o arquivo é, de fato, uma imagem **JPEG**.

---
## Natas Level 14
Bom, o penúltimo nível da nossa trilha - *Natas 14* - nos mostra a seguinte página inicial:

[![image.png](https://i.postimg.cc/RFgV3Kjs/image.png)](https://postimg.cc/DJbKHJfL)

Ela nos pede o nome de um usuário e sua senha, respectivamente. O problema é, qual seria o usuário e a senha corretas? Para isso, vamos dar uma olhada no código-fonte do site:

[![image.png](https://i.postimg.cc/7h9yfkjy/image.png)](https://postimg.cc/dZhfxzqW)

O código está escrito em **PHP** e, ao lermos, podemos perceber que este código foi projetado para interagir com o banco de dados **MySQL**. Porém, atente-se à essa parte:

[![image.png](https://i.postimg.cc/8zDyPYV0/image.png)](https://postimg.cc/BXY5mMbT)

Esta é a parte da **vulnerabilidade** do sistema. O servidor cria uma consulta **SQL** baseada diretamente nos valores que o usuário envia em **"username"** e **"password"**. 

Esses dados são obtidos por meio da variável **$_REQUEST** - ela permite acesso à informações de diferentes métodos de requisição em um único array. Ou seja, tudo o que o usuário digita é inserido diretamente na consulta do banco de dados.

Como toda entrada é válida pelo servidor, podemos executar um ataque muito famoso conhecido por **SQL Injection**.

O site [w3schools](https://www.w3schools.com/sql/sql_injection.aspo) possui uma ótima explicação sobre o que é de fato **SQL Injection**, e quais são seus comandos. Nele, pude observar o seguinte comando:

>     Username:
>     " or ""="

>     Password:
>     " or ""="

O próprio site nos diz a seguinte frase:

> A hacker might get access to user names and passwords in a database by simply inserting " OR ""=" into the user name or password text box.

Que em português seria:

>Um hacker pode obter acesso a nomes de usuário e senhas em um banco de dados simplesmente inserindo " OU ""=" na caixa de texto do nome de usuário ou da senha:

Logo, vamos testar essa condição na página inicial do *Natas 14*:

[![image.png](https://i.postimg.cc/BnkGzsFh/image.png)](https://postimg.cc/cvRjKpXY)

Conseguimos a senha para o *Natas 15!!!*

> natas 15: SdqIqBsFcz3yotlNYErZSZwblkm0lrvx

### **Perguntas a serem feitas:**

* **Como a consulta SQL é montada e por que isso representa um risco?**

   **Resposta:** Ela é montada por concatenação de *strings*, misturando texto da aplicação com valores fornecidos pelo usuário. Isso permite que partes de **SQL** sejam injetadas dentro da *query*.

*  **Por que o uso de $_REQUEST contribui para a vulnerabilidade presente no desafio?**

    **Resposta:** Porque **$_REQUEST** pode receber valores tanto de **GET** quanto de **POST** (métodos **HTTP** usados para enviar e receber dados entre um cliente e um servidor), o que facilita o controle completo da entrada pelo usuário. 

---
## Natas Level 15
Chegamos ao último desafio da nossa trilha *Natas - OverTheWire*! O nível 15 nos mostra a seguinte página inicial:

[![image.png](https://i.postimg.cc/prCxn9qC/image.png)](https://postimg.cc/xNXBwdrN)

Se eu digitar qualquer nome de usuário, e clicar em **"Check existence"**:

[![image.png](https://i.postimg.cc/RCsDqQT8/image.png)](https://postimg.cc/0rSfBSFd)

Irá nos mostrar:

[![image.png](https://i.postimg.cc/Z5kjyfvF/image.png)](https://postimg.cc/7fVSFnVf)

Então pela lógica, só serão aceitos usuários cadastrados no sistema. Vamos dar uma olhada no código-fonte:

[![image.png](https://i.postimg.cc/8cRddG6v/image.png)](https://postimg.cc/p5dnxgkV)


Novamente, é um código escrito em **PHP** e, projetado para interagir com o banco de dados **MySQL**. 

É muito parecido com o código anterior, porém agora temos aquela parte laranja. Ela mostra a estrutura da tabela **users**, com os campos **username** e **password**, ambos **VARCHAR(64)** - um tipo de dado em bancos de dados que armazena texto de comprimento variável, com um limite máximo de 64 caracteres.

E lendo o código, percebemos que diferente do anterior, esse código não nos retorna a senha de um usuário, ele apenas nos mostra se existe esse usuário, ou não (**True** ou **False**). Logo, desenvolvendo essa questão, percebemos que o ataque que se trata aqui é o **SQL Injection: Boolean** - com ele, podemos abusar deste código para descobrir outros dados do banco de dados, fornecendo ao aplicativo comandos **True** ou **False**.

Este ataque utiliza um comando bastante interessante:

>     " OR substring(username,1,1) = 'a' -- 

Esse comando verifica se a primeira letra (1,1) do nome do usuário é **‘a’**. No caso, posso testar diversos caracteres, e ampliar até onde vai pegar a correspondência.

Ao testar com a letra 'a', obtemos a seguinte resposta:

[![image.png](https://i.postimg.cc/NF1pjmGD/image.png)](https://postimg.cc/m1gQdcH1)

Poderíamos tentar testar manualmente cada caractere, mas isso não seria eficiente nem confiável. O comando **" OR substring(username,1,1)='a' --**, não verifica a senha, apenas checa se algum usuário no banco começa com aquela letra.

Por isso, a melhor solução é automatizar o processo. No entanto, criar um script que realize os testes de forma estruturada e filtre corretamente o usuário alvo é a melhor alternativa. Com isso, pedi para a IA gerar um código em **Python** que executasse o ataque automaticamente.

Aqui está o código:

[![image.png](https://i.postimg.cc/ZY6hVkn5/image.png)](https://postimg.cc/bdYMwB17)

Ele foi testado no **Google Colab**. E ao executarmos, obtemos:

[![image.png](https://i.postimg.cc/cLbjdTCP/image.png)](https://postimg.cc/tsFD53hz)

[![image.png](https://i.postimg.cc/13fC76BT/image.png)](https://postimg.cc/SnbfJnw7)

Obtemos o resultado final da  nossa senha para o *Natas 16*!!

> natas16: hpkjkyvilqctew33qmuxl6edvfmw4sgo

### **Perguntas a serem feitas:**

* **Que tipo de ataque o Natas 15 ilustra?**

   **Resposta:**  Ilustra **Blind Boolean SQL Injection**, onde se testa condições lógicas que retornam um resultado.
  
---

### **Conclusão:**

Finalizar os levels 0 a 15 do *Natas* representa mais do que apenas resolver desafios — é entender a mentalidade de quem desenvolve, testa e explora aplicações web. Ao longo dessa trilha, conceitos essenciais de segurança são aprendidos: como o servidor interpreta input do usuário, como cookies e autenticação funcionam, como filtros falham e como vulnerabilidades simples podem abrir portas enormes.

Com isso, concluo minha caminhada pelos primeiros 15 níveis do *Natas*. O aprendizado aqui acumulado serve como base sólida para avançar aos próximos levels, onde a exploração se torna ainda mais técnica e desafiadora. Obrigada a todos que puderam acompanhar essa jornada!
