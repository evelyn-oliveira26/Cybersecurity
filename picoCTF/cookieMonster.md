# Escola de Segurança Cibernética - Cookie Monster Secret Recipe (picoCTF)

> Solved by @evelyn-oliveira26
>
>> This is a CTF about Cookie Manipulation Vulnerability

## Desafio: Cookie Monster Secret Recipe (Vulnerabilidade de Manipulação de Cookies)

**Introdução**

"Cookie Monster Secret Recipe" é um desafio da plataforma picoCTF - plataforma na qual oferece exercícios e competições voltados para segurança cibernética. Este desafio envolve assuntos como manipulação de cookies, e codificação Base64. No entanto, o objetivo do desafio é ensinar conceitos fundamentais de segurança em aplicações web.

* [Página do Desafio](https://play.picoctf.org/practice/challenge/469)

Essa questão consiste em manipular um cookie codificado em Base64. Ao decodificá-lo é possível obter a flag.

**Análise Inicial**

Quando começamos a resolver o desafio obtemos o seguinte enunciado:

>*Cookie Monster has hidden his top-secret cookie recipe somewhere on his website. As an aspiring cookie detective, your mission is to uncover this delectable secret. Can you outsmart Cookie Monster and find the hidden recipe?
Additional details will be available after launching your challenge instance.*

Também possuimos algumas dicas que a própria questão traz:

>Sometimes, the most important information is hidden in plain sight. Have you checked all parts of the webpage?

>Cookies aren't just for eating - they're also used in web technologies!

>Web browsers often have tools that can help you inspect various aspects of a webpage, including things you can't see directly.

**Interpretando a Dica**

As dicas fornecidas nos levam a um único caminho lógico. 

Como a questão e as dicas mencionam muito a palavra **Cookie**, este exercício não escaparia dos famosos cookies de sites, que são pequenos arquivos de texto que um site envia para o navegador do utilizador, armazenando informações da sua visita.

**Solução**

A princípio, quando começamos a resolver o desafio você é redirecionado para esta página:

[![cookie1.jpg](https://i.postimg.cc/8PSSy4wJ/cookie1.jpg)](https://postimg.cc/grNQjvCm)

Nesta página você precisa tentar fazer login (eu usei como login e senha a palavra *test*).

Logo após, somos redirecionados para outra página, na qual nos diz que nosso acesso foi negado.

[![cookie3.jpg](https://i.postimg.cc/C5CWTyJZ/cookie3.jpg)](https://postimg.cc/jn58PFpK)

Porém o **Cookie Monster** nos deixou essa dica como está descrito na imagem. Como havíamos interpretado a dica anteriormente, estamos lidando com cookies de websites, logo, precisamos acessá-los.

Para acessar a parte onde podemos verificar os cookies de um site, precisamos entrar nas **DevTools**, quando clicamos **F12** no teclado.

Já na parte das **DevTools**, especificamente na aba **Application**, podemos ver no canto esquerdo um tópico chamado **Cookies**, neste tópico garantimos logo abaixo o domínio onde os cookies estão armazenados, e nessa lógica, precisamos decodificá-lo.

[![cookie4.jpg](https://i.postimg.cc/JzzSg2Xn/cookie4.jpg)](https://postimg.cc/D8RC45Bk)

Efetivamente, o  domínio (ou scope do cookie) está codificado em Base64 - um jeito de codificar dados binários em texto. Logo, usei o site [base64decode.org](https://www.base64decode.org/pt/) para realizar a decodificação.
 
[![cookie5.jpg](https://i.postimg.cc/VvzKtJB6/cookie5.jpg)](https://postimg.cc/bDF0cN5c)

Por fim, encontramos a flag! O site já nos mostra a flag sem muitas enrolações, o que é ótimo para quem busca processos automatizados.

**Conclusão**

Flag:

>picoCTF{c00k1e_m0nster_l0ves_c00kies_C430AE20}

Esse desafio foi muito importante para mostrar na prática como informações relevantes podem estar escondidas nos cookies de um site. Ele revelou que, muitas vezes, esses valores não estão protegidos de fato, mas apenas codificados em Base64, algo que qualquer pessoa consegue decodificar com ferramentas bem simples.

Além disso, o exercício foi útil para praticar a inspeção e manipulação de cookies no navegador, demonstrando como pequenas alterações podem afetar completamente o comportamento da aplicação. Isso evidencia que vulnerabilidades simples podem expor dados sensíveis e comprometer a segurança do sistema.
