# Equipe de Segurança Cibernética - Super Serial (picoCTF)

> Solved by @evelyn-oliveira26
>
>> This is a CTF about Web Exploitation

## Desafio: Super Serial (Exploração Web)

**Introdução**

"Super Serial" é um desafio da plataforma picoCTF - plataforma na qual oferece exercícios e competições voltados para segurança cibernética. Este desafio envolve assuntos como codificação Base64, desserialização insegura em PHP e manipulação de cookies. No entanto, o objetivo do desafio é explorar essas vulnerabilidades da web, adquirindo conhecimento para avançar nos estudos de segurança cibernética.

* [Página do Desafio](https://play.picoctf.org/practice/challenge/180?page=1&search=super%20se)


**Análise Inicial**

Quando começamos a resolver o desafio obtemos a seguinte descrição:

>Try to recover the flag stored on this website.
Additional details will be available after launching your challenge instance.

E quando clicamos em ***Launch Instance***, a descrição nos libera o *link* para o site do desafio.


Também possuímos uma dica que a própria questão traz:

>The flag is at ../flag

**Interpretando a Dica**

Bom, ao estudarmos assuntos como **Path Traversal** - vulnerabilidade que permite que o atacante acesse arquivos e diretórios armazenados fora do diretório raiz da aplicação web. Há uma vulnerabilidade que o atacante pode manipular referências de arquivo para navegar pela estrutura de diretórios do servidor, que seria:

>     ../

Essa vulnerabilidade instrui o sistema a retroceder um nível de hierarquia. 

Então quando temos:

>     ../flag

Isso instrui o sistema a retroceder um diretório e procurar por um arquivo chamado "*flag*" (que estaria a nossa resposta).


**Solução da Questão**

Ao acessarmos o site, nos deparamos com um pedido de cadastro, típico de questão de CTF. 

[![image.png](https://i.postimg.cc/nVS9MbKH/image.png)](https://postimg.cc/s1Sg0L08)

Quando fazemos um teste para tentarmos acessar o site, recebemos a seguinte mensagem:

[![image.png](https://i.postimg.cc/SKbMq664/image.png)](https://postimg.cc/68z3fGbb)

O erro mostra que o site tenta abrir um banco de dados **SQLite** localizado em **../users.db**. Isso confirma que o sistema acessa arquivos fora do diretório público usando caminhos relativos. 

Uma ferramenta importante é a ***robots.txt*** - um arquivo usado por sites para indicar aos rastreadores da web e outros robôs visitantes quais partes do site eles têm permissão para acessar.

Ao implementarmos o ***robots.txt*** no diretório do site, nos deparamos com a seguinte imagem:

[![image.png](https://i.postimg.cc/vBV8mkbN/image.png)](https://postimg.cc/5YfW7PHB)

Descobrimos que há um caminho para este site! Porém, quando testamos este caminho, nos deparamos com página não encontrada.

Para constar, há diferença entre as extensões **".php"** e **".phps"**:
>     ".php" executa o código.

>     ".phps" exibe o código-fonte na tela.

Bom, mas como não deu certo pelo caminho anterior, vi que existe um outro caminho **(/index.php)** quando fiz o teste de login. Seguindo tal lógica, se existe um **/admin.phps**, então outros arquivos **PHP** também podem ter a versão **".phps"**. No caso, farei o teste usando **/index.phps**:

[![image.png](https://i.postimg.cc/bYFX53P6/image.png)](https://postimg.cc/8sWnJdjW)

Chegamos no código-fonte da imagem acima, porém, vamos dar uma atenção a mais para a parte do código em **PHP**:

[![image.png](https://i.postimg.cc/P5s7G7Rr/image.png)](https://postimg.cc/XpLLdsWT)

O código armazena conteúdo diretamente em um cookie após serialização e codificação. Como esse cookie pode ser controlado pelo usuário, a aplicação fica vulnerável e  um atacante pode manipular o conteúdo desse cookie para injetar objetos maliciosos.

Bom, na primeira linha temos:

>     require_once("cookie.php");

Analisando esta linha, é possível identificar que há um arquivo chamado **"cookie.php"** que vem através do **require_once**. Logo, como existe este arquivo, vamos testá-lo como caminho.

 O caminho com **"/cookie.php"** retorna uma página em branco, mas com **"/cookie.phps"**, retorna o código-fonte da página:

 [![image.png](https://i.postimg.cc/8CKYJztm/image.png)](https://postimg.cc/7Cz9jwv5)

 [![image.png](https://i.postimg.cc/FKRW4QNc/image.png)](https://postimg.cc/pmwYf49X)

 O código desserializa diretamente dados fornecidos pelo cliente através do cookie "login". Ele aplica decodificações (URLdecode e Base64) e executa a função ***"unserialize()"*** sem qualquer verificação de integridade, permitindo a manipulação dos dados.

Prosseguindo com o exercício, vemos também no código de **/index.phps** uma linha até que interessante:

>     header("Location: authentication.php");

Essa linha é executada após enviar as credenciais de login. Caso o usuário seja  **guest** ou **admin**, o sistema cria o cookie de autenticação e, em seguida, redireciona automaticamente para **/authentication.php**.

Logo, ao testar essa caminho diretamente, o site me retorna isto:

[![Whats-App-Image-2026-02-10-at-10-59-53.jpg](https://i.postimg.cc/NfSkZrLb/Whats-App-Image-2026-02-10-at-10-59-53.jpg)](https://postimg.cc/mt39HkYF)

Como vimos anteriormente, precisamos de um cookie "login", logo, irei criá-lo como teste a princípio:

[![Whats-App-Image-2026-02-10-at-14-05-16.jpg](https://i.postimg.cc/pdw6Y6Mn/Whats-App-Image-2026-02-10-at-14-05-16.jpg)](https://postimg.cc/LqVDmvXH)

Assim que atualizamos a página, obtemos:

[![Whats-App-Image-2026-02-10-at-17-54-54.jpg](https://i.postimg.cc/zXG0WrH7/Whats-App-Image-2026-02-10-at-17-54-54.jpg)](https://postimg.cc/YjT6KT3L)

Isso nos mostra que o site tentou fazer ***unserialize()*** (desserializar), e mostra que nós usuários conseguimos explorar isso. Logo, se o site consegue reconstruir qualquer valor que eu mandar, vamos mandar algum valor que mostraria a possível *flag*.

No caso, como não tem jeito de enviar código **PHP** como valor de cookie, precisamos fazer a serialização, que seria transformar o código **PHP** em formato de texto para usar como valor no cookie.

 Primeiramente, fui em **/authentication.phps** ver o código-fonte dessa página e nos deparamos com essa parte em **PHP**:

[![image.png](https://i.postimg.cc/TwnYCn8X/image.png)](https://postimg.cc/HcsgLcsS)

**Log** é um arquivo usado pelo sistema para registrar eventos e atividades. A classe **access_log** deveria manipular apenas esses registros,
porém como o caminho do arquivo não foi validado em **function read_log()**, é possível explorar a função
para ler arquivos sensíveis, como o arquivo da *flag*.

 serializando o código, assim, para que eu pudesse colocar o texto obtido como valor no cookie

A partir desse código, e retornando a **/authentication.php**, utilizei a inteligência artificial para gerar um script explorando essa falha de segurança. O objetivo foi serializar o código, permitindo usar o texto resultante como valor do cookie. Em seguida, executei o código no **PHP Sandbox**:

[![image.png](https://i.postimg.cc/KY6smMRd/image.png)](https://postimg.cc/cKccm67m)

Agora, temos nosso valor para inserir dentro do nosso cookie de login:

[![Whats-App-Image-2026-02-10-at-14-12-12.jpg](https://i.postimg.cc/DwbrnYLy/Whats-App-Image-2026-02-10-at-14-12-12.jpg)](https://postimg.cc/NKB9xDdW)

Atualizando a página conseguimos chegar na *flag*!!! 

[![image.png](https://i.postimg.cc/6qy7zyhr/image.png)](https://postimg.cc/p5MXLV4r)

**Conclusão**

Flag:

>picoCTF{1_c4nn0t_s33_y0u_2fba20fa}

O desafio mostrou como uma aplicação pode se tornar vulnerável ao confiar em dados controlados pelo usuário.
Ao aceitar informações vindas de um cookie sem validação adequada, o sistema permitiu a manipulação do seu funcionamento interno, resultando em acesso a arquivos que deveriam ser protegidos.

Assim, o desafio reforça que falhas no desenvolvimento podem abrir portas para ataques, e que validar, restringir e tratar corretamente os dados do usuário é essencial para proteger uma aplicação.
