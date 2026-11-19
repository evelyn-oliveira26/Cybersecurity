# Relatório de Análise de Vulnerabilidade - PHP2Shell

**Nome:** Evelyn Maria de Oliveira Silva

## Introdução

No dia 21 de outubro de 2026, foram divulgadas duas vulnerabilidades críticas no PHP, conhecidas em conjunto como PHP2Shell.

PHP é uma linguagem de script de código aberto, usada no desenvolvimento web. Seu código é executado no servidor e está presente em plataformas como WordPress, Moodle, Joomla e Drupal.

Essas vulnerabilidades podem permitir que um invasor execute código no servidor sem precisar de uma conta ou fazer login. Isso pode causar vazamento de informações, alteração de dados e interrupção de serviços.

O objetivo deste relatório é explicar como essas falhas funcionam e quais medidas podem ser tomadas para reduzir os riscos e corrigi-las. 

## Funcionamento da vulnerabilidade

O PHP2Shell envolve duas falhas no gerenciamento de memória do próprio PHP. Por isso, um site pode ser afetado mesmo que a vulnerabilidade não esteja no código desenvolvido para ele.

As falhas são identificadas como **CVE-2026-109618** e **CVE-2026-109619**. CVE significa *Common Vulnerabilities and Exposures* e funciona como um código de identificação para cada vulnerabilidade.

Nesses códigos, **2026** indica o ano de atribuição ou reserva do identificador. Já **109618** e **109619** são os números que identificam cada falha naquele ano e não representam sua gravidade.

As duas receberam nota **9,2 no CVSS v4.0**, sendo classificadas como críticas. O CVSS é um sistema que avalia a gravidade técnica de uma vulnerabilidade, usando notas de 0 a 10.

### CVE-2026-109618

A primeira falha é chamada de *out-of-memory (OOM) corruption* e está relacionada ao tratamento de erros de falta de memória.

Durante o processamento de uma requisição, o PHP pode ficar sem memória e interromper uma operação antes que seus dados internos estejam completamente preparados. Depois, ao fazer a limpeza da requisição, pode usar esses dados incompletos como se estivessem corretos.

A exploração dessa falha pode permitir que o invasor execute código com as permissões do **worker do PHP**, que é o processo responsável por executar o PHP e atender às requisições.

Por exemplo, se esse processo tiver permissão para ler ou alterar determinados arquivos, o código do invasor também poderá fazer isso. Porém, isso não significa que ele terá automaticamente acesso de administrador.

### CVE-2026-109619

A segunda falha é chamada de *stale global state across requests*. Ela ocorre quando o PHP mantém referências a dados de uma requisição mesmo depois que a memória usada por eles já foi liberada.

Quando o mesmo worker atende a uma nova requisição, ele pode acabar usando essas referências antigas.

Isso pode causar um **use-after-free**, que significa acessar uma região de memória depois que ela foi liberada. Dependendo da exploração, o invasor pode obter informações da memória do processo ou executar código.

## Mitigação e correção

A principal forma de corrigir o PHP2Shell é atualizar o PHP para uma versão que contenha as correções de segurança.

As primeiras versões corrigidas de cada linha foram:

| Linha do PHP | Primeira versão corrigida |
|---|---|
| 8.2 | 8.2.35 |
| 8.3 | 8.3.36 |
| 8.4 | 8.4.27 |
| 8.5 | 8.5.12 |

Depois da atualização, é necessário reiniciar os serviços e os workers para que utilizem a versão corrigida.

Quando não for possível atualizar imediatamente, algumas medidas temporárias podem reduzir os caminhos de exploração:

- **Limitar o tamanho das requisições e dos uploads:** ajuda a reduzir algumas formas de provocar consumo excessivo de memória. Esses limites precisam considerar o funcionamento normal do site.

- **Desativar o acompanhamento de uploads na sessão:** o parâmetro `session.upload_progress.enabled` permite acompanhar o andamento do envio de arquivos. Configurá-lo como `0`, na configuração do PHP ou do servidor antes do processamento das requisições, e reiniciar os workers bloqueia alguns caminhos relacionados a sessões. Isso desativa o acompanhamento, mas não impede o envio dos arquivos.

- **Desativar o rastreamento de erros fatais no PHP 8.5:** o parâmetro `fatal_error_backtraces` registra a sequência de chamadas de funções que levou a um erro fatal. Configurá-lo como `0` e reiniciar os workers bloqueia um caminho conhecido de exploração. Essa medida não impede que os erros aconteçam.

Essas mitigações são parciais. Elas reduzem alguns riscos, mas não substituem a atualização do PHP.

## Conclusão

O PHP2Shell mostra que a segurança de um site também depende dos componentes usados no servidor. Mesmo que o código da aplicação não tenha essas falhas, uma versão vulnerável do PHP pode colocar o sistema em risco.

A atualização é a principal forma de corrigir o problema. As mitigações podem ajudar enquanto isso não é possível, mas não oferecem proteção completa.

Por isso, é importante acompanhar os avisos de segurança, manter o servidor atualizado e dar aos processos apenas as permissões necessárias para seu funcionamento.
