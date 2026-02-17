# Equipe de Segurança Cibernética - Sk1ttl3 Newspaper

> Solved by @evelyn-oliveira26
>
>> This is a CTF about Web Exploitation

## Desafio: Sk1ttl3 Newspaper (Exploração Web)

**Introdução**

"Sk1ttl3 Newspaper" é um desafio de exploração web que envolve comandos **SQL Injection**. No entanto, o objetivo do desafio é explorar essa vulnerabilidade da web, adquirindo conhecimento para avançar nos estudos de segurança cibernética.

* [Página do Desafio](https://snewspaper.discloud.app/)


**Processo**

Ao acessarmos a aplicação, nos deparamos com um jornal eletrônico, cuja as notícias são da cidade de *Night City*:

[![image.png](https://i.postimg.cc/mkTxX7NS/image.png)](https://postimg.cc/62b1T2P7)

E quando acessamos as notícias que estão destacadas em azul, somos redirecionados para outra página, por exemplo:

[![image.png](https://i.postimg.cc/hv8mgRdk/image.png)](https://postimg.cc/D4Z0dD56)

Note que o caminho da URL para essa notícia é **"/post.php?id=1"**. Logo, ao acessarmos cada notícia individualmente, veremos que cada uma das 5 notícias possui um número respectivo de **id's**, de 1 até 5.

A partir desses id's, testei se o servidor sanitiza o parâmetro como um texto simples ou se o concatena diretamente na consulta **SQL**, permitindo a execução de comandos no banco de dados:

[![image.png](https://i.postimg.cc/6QfnwsGX/image.png)](https://postimg.cc/8FsjB0HK)

Como mostrado na imagem, concluímos que o servidor executa comandos no banco de dados sem sanitização, pois ao testar a operação **"4-2"** na URL, a aplicação redireciona diretamente para a notícia cujo o id é de número 2.

Prosseguindo com o exercício, vamos olhar o código-fonte do exercício:

[![image.png](https://i.postimg.cc/1RG4fxmf/image.png)](https://postimg.cc/pydP66nH)

Notem que há um comentário em verde no final do código escrito:

>     <!-- admin.php -->

Seguindo tal lógica, podemos então raciocinar que existe uma parte da aplicação específica para o administrador. Logo, jogando o arquivo **"admin.php"** como caminho na URL:

[![image.png](https://i.postimg.cc/BZm9hNMn/image.png)](https://postimg.cc/Z0vMn8GG)

Somos redirecionados automaticamente para o caminho **"/login.php"**. 

Como havíamos testado, anteriormente, as operações matemáticas na URL e funcionado, podemos admitir que esta aplicação é favorável para injeção de comandos **SQL Injection**.

Dessa forma, um comando clássico de **SQL Injection** é o:

>     ' OR 1=1 --

 **' OR 1=1 --** é uma técnica de **SQL Injection** que insere uma condição matemática sempre verdadeira na consulta do banco de dados, forçando o sistema a aceitar o login sem uma senha válida e ignorando o restante do código original.

Assim, testando essa injeção de comando com o usuário **admin** e senha **' OR 1=1 --**, obtemos:

[![image.png](https://i.postimg.cc/MHnghJpm/image.png)](https://postimg.cc/kRdjbZ82)

Flag:

>    DUCK{SK1TTL3_N3W5_2077_SQL1NJ3CT10N_H45_B33N_H4CK3D}

**Vulnerabilidade**

A aplicação apresenta uma vulnerabilidade de **SQL Injection**.

 O problema ocorre porque os parâmetros recebidos na URL **(post.php?id=)** e no formulário de login são concatenados diretamente na consulta **SQL**, sem validação ou uso de consultas parametrizadas. 
 
 Isso foi confirmado quando a aplicação interpretou operações matemáticas (4-2) como expressão **SQL** válida, e quando o login foi burlado com o payload:

>     ' OR 1=1 --

 Esse comando transforma a consulta em uma condição sempre verdadeira, permitindo autenticação como administrador.

 **Mitigação de Risco**

Para corrigir a vulnerabilidade, as seguintes medidas devem ser aplicadas:


 **1. Consultas Parametrizadas:**

São a principal defesa contra **SQL Injection**, separando o código **SQL** dos dados de entrada do usuário. Ao usar marcadores de posição *(placeholders)*, o banco de dados trata a entrada estritamente como texto, não como comando executável, impedindo manipulações maliciosas como **' OR '1'='1**.

**2. Validação e Sanitização de Entrada:**

É o processo de verificar e tratar os dados recebidos do usuário para evitar informações maliciosas, inválidas ou indesejadas antes de processá-las.

A validação verifica se a entrada está no formato esperado (por exemplo: conferir se o campo idade contém apenas números).

A sanitização remove ou modifica caracteres perigosos (como ', ; ou --) para evitar que sejam interpretados como parte de um comando.

A validação bloqueia dados inválidos, e a sanitização remove caracteres perigosos, diminuindo as chances de exploração da aplicação.
