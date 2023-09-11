```python
# CLIENTE DNS
import socket

# criando o socket com protocolo udp
client_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

# escolhendo o serviço
message = input('Digite o serviço desejado: ')
client_socket.sendto(message.encode(), ('127.0.0.1', 11111))

# imprimindo nova porta existente
data, server_address = client_socket.recvfrom(1024)
new_port = data.decode()
print(new_port)

if new_port != 'Not found, server não encontrado!':

    # escolhendo UDP ou TCP
    data, server_address = client_socket.recvfrom(1024)
    protocolo_escolhido = input(data.decode())
    client_socket.sendto(protocolo_escolhido.encode(), server_address)

    # recebendo resposta
    resposta, server_address = client_socket.recvfrom(1024)
    print(resposta.decode())

# fechando a conexao
client_socket.close()

```
