```python
# TCP server
import socket

# para avisar o servidor DNS que o servidor tcp está funcionando
dns_server = ('127.0.0.1', 11111)
conectando = '1'
protocolo = 'TCP'

# Cria um socket para enviar o aviso
warning_dns = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
warning_dns.bind(('127.0.0.1', 9999))

# Envia a mensagem para o servidor DNS
warning_dns.sendto(conectando.encode(), (dns_server))
warning_dns.sendto(protocolo.encode(), (dns_server))

# Fechando o socket de aviso
warning_dns.close()

# Criação do socket TCP IPv4
server_TCP = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
print(f'Server >>>TCP<<< criado ...')

# definindo porta e escutando solicitaçao
server_TCP.bind(('127.0.0.1', 9999)) # sc.bind = definindo o ip e a porta que o socket estará vinculado
server_TCP.listen() # Colocar o servidor para escutar as solicitações de conexão
print('O server TCP está conectado e pronto para requisições')

# aceitando a conexão
client_TCP, clientAddr =  server_TCP.accept()

# recebendo pergunta
pergunta = client_TCP.recv(2048)
print(pergunta.decode())

# enviando mensagem avisando o que o serviço é capaz de fazer ao cliente
resposta = 'Retorno o quadrado de qualquer numero que voce pedir...'
print(resposta)
client_TCP.send(resposta.encode())

# Perguntando o número que o cliente gostaria de saber seu quadrado
pergunta = 'Digite o numero que voce gostaria de saber o quadrado dele:'
print(pergunta)
client_TCP.send(pergunta.encode())

# recebendo numero
data = client_TCP.recv(2048) 

# decodificando o numero recebido
num = int(data.decode())
print(f'>> {num}')

# Após receber, calcular e processar a requisição o servidor está apto para enviar uma resposta.
quadrado = num * num
answer2 = f'O quadrado do numero {num} é: {quadrado}'
print(answer2)
client_TCP.send(answer2.encode())

# fechando conexao
client_TCP.close()

# para avisar o DNS que o servidor será desligado
desconectando = '0'

# Cria um socket para enviar o aviso
warning_dns = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
warning_dns.bind(('127.0.0.1', 9999))

# Envia a mensagem para o servidor DNS
warning_dns.sendto(conectando.encode(), (dns_server))
warning_dns.sendto(protocolo.encode(), (dns_server))

# Fechando o socket de aviso
warning_dns.close()
```
