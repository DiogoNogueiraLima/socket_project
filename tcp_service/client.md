```python
# TCP client
import socket
import time

# começando a contar o tempo no inicio do programa
start_time = time.time()

# Criação do socket TCP IPv4
client_TCP = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
print(f'Client >>>TCP<<< criado ...')

# Solicitando conexao no ip e porta do server
client_TCP.connect(('localhost', 9999))
print('cliente conectado')

# perguntando para o server qual o serviço que ele provê
what_service = 'Qual seu serviço?'
print(what_service)
client_TCP.send(what_service.encode())

# Recebendo resposta do serviço do servidor.
service = client_TCP.recv(2048)
print(f'{service.decode()}')

# Recebendo pergunta feita pelo server querendo saber o numero escolhido
pergunta = client_TCP.recv(2048)
print(f'{pergunta.decode()}')

# enviando o numero escolhido pelo usuario
input_time = time.time()
num = str(input())

# desconsiderando o tempo que o usuario demorou para escrever o numero no teclado
final_input_time = time.time()
result_input_time = final_input_time - input_time

# calculando o tempo de envio da resposta TCP
initial_send_time = time.time()
client_TCP.send(num.encode())
final_send_time = time.time()

# imprimindo resposta do tempo que levou para o envio da mensagem
send_time = final_send_time - initial_send_time
print(f'O tempo de envio dessa operaçao foi de: {send_time} milisegundos')

# Recebendo as respostas do servidor.
quadrado = client_TCP.recv(2048)
reply = quadrado.decode()
print(reply)

# finalizando conexão
client_TCP.close()

# terminando o cronometro
end_time = time.time()
total_time = end_time - start_time
total_time -= result_input_time
print(f'O tempo total de execuçao do programa TCP foi de: {total_time} milisegundos')
```
