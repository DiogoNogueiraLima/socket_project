
# Captura do Wireshark:

Para demonstrar a funcionalidade do serviço e capturar o tráfego de rede relacionado a ele, foi realizada uma série de etapas usando o Wireshark:

### 1. Inicialização do Servidor DNS:
Primeiramente, o servidor DNS foi iniciado. O DNS (Domain Name System) é um sistema que traduz nomes de domínio em endereços IP. A ideia da nossa aplicação é que ao cliente fazer uma requisição de serviço, o servidor DNS retorna o IP e a porta ao qual esse serviço esteja funcionando.

### 2. Inicialização do Servidor UDP:
Após a inicialização do servidor DNS, o servidor UDP (User Datagram Protocol) foi inicializado. Enviando assim, uma mensagem para o servidor DNS avisando a o IP e a porta ao qual o servidor UDP estará funcionando a partir daquele momento. Após o envio da mensagem, o servidor DNS cadastrou o servidor UDP na sua lista de servidores disponíveis para conexão.

### 3. Inicialização do Servidor TCP:
Em seguida, o servidor TCP (Transmission Control Protocol) foi inicializado. Enviando assim, uma mensagem para o servidor DNS avisando a o IP e a porta ao qual o servidor TCP estará funcionando a partir daquele momento. Após o envio da mensagem, o servidor DNS cadastrou o servidor TCP na sua lista de servidores disponíveis para conexão.

### 4. Utilização do Cliente DNS:
Depois de configurar os servidores DNS, UDP e TCP, um cliente DNS foi utilizado para buscar onde estava funcionando o serviço de retornar o quadrado no servidor UDP. Em seguida, outro cliente DNS foi iniciado para perguntar ao servidor DNS onde estava hospedado o serviço que retorna o quadrado utilizando o servidor TCP. Nas duas ocasiões o servidor DNS conseguiu retornar com exatidão onde estavam hospedados os servidores UDP e TCP. Assim que o cliente solicita um serviço que não seja cadastrar-se ou ser removido do servidor de nomes, o servidor DNS criará uma novas portas efêmeras para tratar cada solicitação que estiver chegando, Dessa forma o servidor não ficará sobrecarregado e poderá responder a várias solicitações ao mesmo tempo.

### 5. Utilização do Cliente TCP:
Após localizar o serviço do servidor TCP, um cliente TCP foi usado para estabelecer uma conexão com o servidor TCP e acessar o serviço. Neste caso, o serviço é calcular o quadrado de um número. Após a consulta feita e o resultado obtido pelo cliente, o servidor TCP foi encerrado e removido da lista de servidores disponíveis no servidor DNS.

### 6. Utilização do Cliente UDP:
De maneira semelhante ao cliente TCP, um cliente UDP foi utilizado para estabelecer uma conexão com o servidor UDP e acessar seu serviço. Também neste caso, o serviço é calcular o quadrado de um número. Após a consulta feita e o resultado obtido pelo cliente, o servidor UDP foi encerrado e removido da lista de servidores disponíveis no servidor DNS.

### 7. Finalização do Servidor DNS:
Por fim, o servidor DNS foi encerrado, concluindo assim o teste e a captura de tráfego relacionados ao serviço desenvolvido.

### Conclusão
A captura do Wireshark registrou o tráfego de rede gerado durante essas etapas, incluindo consultas DNS, conexões TCP e UDP, bem como as respostas do servidor. Esta análise do tráfego foi fundamental para entender como a comunicação ocorre entre os componentes do sistema e pode ser valiosa para fins de depuração e otimização.

