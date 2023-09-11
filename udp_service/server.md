```python
# SERVER UDP
import socket

# Criação do socket TCP IPv4
server_UDP = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
print(f'Server >>>UDP<<< criado ...')

# definindo porta e escutando solicitaçao
server_UDP.bind(('127.0.0.1', 999)) # sc.bind = set do ip e a porta que o socket estará vinculado
print('The UDP server is ready to receive')

# avisando ao dns que o udp esta funcionado
dns_server = ('127.0.0.1', 11111)
conectando = '1'
protocolo = 'UDP'

# Envia a mensagem para o servidor DNS
server_UDP.sendto(conectando.encode(), dns_server)
server_UDP.sendto(protocolo.encode(), dns_server)

# recebendo pergunta
pergunta, client_addr = server_UDP.recvfrom(2048) 
print(f'{pergunta.decode()}')

# enviando mensagem avisando o que o serviço é capaz de fazer ao cliente
resposta = 'Retorno o quadrado de qualquer numero que voce pedir...'
print(resposta)
server_UDP.sendto(resposta.encode(), client_addr)

# Perguntando o número que o cliente gostaria de saber seu quadrado
pergunta = 'Digite o numero que voce gostaria de saber o quadrado dele:'
print(pergunta)
server_UDP.sendto(pergunta.encode(), client_addr)

# recebendo numero
data, client_addr= server_UDP.recvfrom(2048) 

# decodificando o numero recebido
num = int(data.decode())
print(f'>> {num}')

# Após receber, calcular e processar a requisição o servidor está apto para enviar uma resposta.
quadrado = num * num
answer2 = f'O quadrado do numero {num} é: {quadrado}'
print(answer2)
server_UDP.sendto(answer2.encode(), client_addr)

# fechando conexao
server_UDP.close()

# avisando ao dns que o udp esta fechando
desconectando = '0'
server_UDP.sendto(desconectando.encode(), dns_server)
```
