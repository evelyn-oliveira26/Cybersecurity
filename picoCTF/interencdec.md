# Escola de Segurança Cibernética - interencdec (picoCTF)

> Solved by @evelyn-oliveira26
>
>> This is a CTF about Cryptography

## Desafio: interencdec (Criptografia)

*Introdução*  

"interencdec" é um desafio da plataforma picoCTF - plataforma na qual oferece exercícios e competições voltados para segurança cibernética. Este desafio envolve assuntos como criptografia e vários processos de decodificação. Nele, veremos a codificação Base64 e a Cifra de César. No entanto, o objetivo do desafio é treinar a capacidade de reconhecer e decodificar dados encobertos em diversas camadas de codificação.

* [Página do Desafio](https://play.picoctf.org/practice/challenge/418)

Essa questão consiste em um exercício de codificação/decodificação de uma mensagem encriptada. Ao decodificá-la é possível obter a flag.

*Análise Inicial*

Quando começamos a resolver o desafio obtemos a seguinte descrição:

>*Can you get the real meaning from this file.
Download the file here.*

Também possuimos uma dica que a própria questão traz:

>Engaging in various decoding processes is of utmost importance

*Interpretando a Dica*

A dica recebida foi bem clara e objetiva, ela nos leva para apenas uma abordagem lógica: processos de decodificação.

*Solução da Questão*

Ao baixarmos o arquivo que a questão nos pede, abrimos-o no bloco de notas.

[![inter1.jpg](https://i.postimg.cc/X7h8g1nd/inter1.jpg)](https://postimg.cc/ykmc1Pg8)

Após abrirmos o arquivo, nos deparamos com uma mensagem encriptada.

[![inter2-1.jpg](https://i.postimg.cc/DZyLh127/inter2-1.jpg)](https://postimg.cc/qtSzXhhF)

Seguindo tal lógica, vamos procurar decodificar a tal mensagem encriptada. Para executarmos tal comando, entraremos no site [CyberChef](https://gchq.github.io/CyberChef/) - ferramenta multifuncional on-line, criada para facilitar a análise e a decodificação de dados.

Assim que entramos no site, encontramos no canto esquerdo a aba ***Operations***, nela, iremos pesquisar por *From Base64*, pois a mensagem que copiamos está no formato Base64 - método de codificação binário-texto que converte dados binários em uma sequência de caracteres imprimíveis seguros.

[![inter3.jpg](https://i.postimg.cc/25JbsMX7/inter3.jpg)](https://postimg.cc/t134PSbs)

Ao decodificarmos a mensagem encriptada, na aba **Output** recebemos outra mensagem também encriptada. Notem que ela começa com um " b' " e termina com " ' ", esses caracteres não fazem parte da mensagem, é um formato do site mostrar a resposta (padrão do Python), logo, iremos remover essa parte e deixar o que realmente nos interessa, que é o conteúdo dentro das aspas.
 
[![inter4.jpg](https://i.postimg.cc/76kDJNCy/inter4.jpg)](https://postimg.cc/mc8K0CNd)

Quando decodificamos a segunda mensagem, o **Output** nos mostra uma outra mensagem encriptada, essa nova mensagem está quaseeee legível, então iremos testar a nova decodificação pela Cifra de César -  método de criptografia que substitui cada letra do texto original por outra letra um número fixo de posições à frente no alfabeto.

Efetivamente, ainda no [CyberChef](https://gchq.github.io/CyberChef/), pesquisaremos em **Operations** por *ROT13* - ROT vem de Rotate, nesse caso ele utiliza a Cifra de César e "rotaciona" 13 posições à frente da letra correspondida. 

Ao adicionarmos esse método, colamos a segunda mensagem que acabamos de encontrar no **Input**.

[![inter6.jpg](https://i.postimg.cc/HWvKf2ps/inter6.jpg)](https://postimg.cc/vD93n5gp)

Porém ao testar com o número de posições ajustado para 13, encontramos mais uma mensagem encriptada, logo, fui ajustando o número de posições até obtermos a flag.

Quando ajustamos a aba **Amount** para 45 foi possível obter a flag!

[![inter8.jpg](https://i.postimg.cc/vm8kJS6T/inter8.jpg)](https://postimg.cc/qNY1nwwH)

Por fim, concluímos nossa missão! Encontramos a flag ao decorrer de vários processos de decodificação.

*Conclusão*

Flag:

>picoCTF{caesar_d3cr9pt3d_78250afc}

Esse exercício se mostrou importante porque reforçou a habilidade de identificar múltiplas camadas de codificação, um recurso bastante comum para quem atua na área de segurança da informação. Ele evidenciou que, ao encontrar uma sequência aparentemente ilegível, não basta decodificar uma vez, é necessário verificar se o resultado ainda contém outra forma de codificação.
