```python
# CLIENTE UDP
import socket
import time

# começando a contar o tempo
start_time = time.time()

# Criação do socket UDP IPv4
client_UDP = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
print(f'Client >>>UDP<<< criado ...')

# conectando no ip e porta
server_UDP_addrs = (('localhost', 999))

# perguntando para o server qual o serviço que ele provê
what_service = 'Qual seu serviço?'
print(what_service)
client_UDP.sendto(what_service.encode(), server_UDP_addrs)

# Recebendo resposta do serviço do servidor.
service, server_UDP_addrs = client_UDP.recvfrom(2048)
print(f'{service.decode()}')

# Recebendo pergunta feita pelo server querendo saber o numero escolhido
pergunta, server_UDP_addrs = client_UDP.recvfrom(2048)
print(f'{pergunta.decode()}')

# enviando o numero escolhido pelo usuario
input_time = time.time()
num = str(input())

# desconsiderando o tempo que o usuario demorou para escrever o numero no teclado
final_input_time = time.time()
result_input_time = final_input_time - input_time

# calculando o tempo de envio da resposta TCP
initial_send_time = time.time()
client_UDP.sendto(num.encode(), server_UDP_addrs)
final_send_time = time.time()

# imprimindo resposta do tempo que levou para o envio da mensagem
send_time = final_send_time - initial_send_time
print(f'O tempo de envio dessa operaçao foi de: {send_time} milisegundos')

# Recebendo as respostas do servidor.
quadrado, server_UDP_addrs = client_UDP.recvfrom(2048)
reply = quadrado.decode()
print(reply)

# finalizando conexao
client_UDP.close()

# terminando o cronometro
end_time = time.time()
total_time = end_time - start_time
total_time -= result_input_time
print(f'O tempo total de execução do programa UCP foi de: {total_time} milisegundos')
```
