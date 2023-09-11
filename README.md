# Contexto
Este é um projeto da disciplina de redes de computadores do terceiro semestre do curso de Sistemas de Informação - CIn - UFPE

# Serviço Desenvolvido:

O serviço desenvolvido consiste em uma aplicação de servidor que tem a capacidade de calcular o quadrado de qualquer valor que seja requisitado a ele. Ou seja, o cliente pode enviar um número para o servidor, e o servidor retornará o quadrado desse número como resposta. Primeiramente os servidores (tanto TCP quanto UDP) enviam uma mensagem para o servidor DNS avisando o IP e a porta que estarão funcionando. Logo em seguida, os servidores já estarão prontos para receber requisições. Depois, ele recebe uma pergunta do cliente querendo saber “Qual seu serviço?” e prontamente responde “Retorno o quadrado de qualquer número que voce pedir…”. Depois, o servidor envia: “Digite o numero que voce gostaria de saber o quadrado dele:” e em seguida, recebe o número digitado pelo usuário. Após calcular o quadrado do número requisitado, o servidor envia ao cliente a resposta e encerra a conexão com o cliente. Por fim, o servidor envia uma mensagem para o servidor DNS avisando que estará sendo desligado.

## Equipe
Diogo Nogueira Lima
Guilherme Lopes Rabello de Barros Correia
