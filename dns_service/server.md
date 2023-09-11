```python
# SERVIDOR DNS
import socket

# funçao para achar nomes
def find_key_by_value(dictionary, value):
    find = False
    for key, val in dictionary.items():
        if val == value:
            find = True
            key = key
            break

    if find:
        resposta = (f"Server que possui o serviço Quadrado conectado em {key}")
    else:
        resposta = ('serviço nao disponivel no momento')

    print(resposta)
    new_server.sendto(resposta.encode(), client_address)
    return

# definindo a porta que o dns escutará
dns_server = ('127.0.0.1', 11111)

# dicionario de nomes dos serviços disponiveis
services = {}

# criando socket
server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
server_socket.bind(dns_server)

print(f"Server DNS conectado no endereço: {dns_server[0]}, porta: {dns_server[1]}")


while True:
    data, client_address = server_socket.recvfrom(1024)
    requisicao = data.decode()

    if requisicao == '0':
        del services[client_address]
        print(f"servidor: {client_address[0]}, porta: {client_address[1]} se desconectando")
    
    elif requisicao == '1':
        data, client_address = server_socket.recvfrom(1024)
        protocol = data.decode()
        services.update({client_address: protocol})
        print(f"servidor {protocol}: {client_address[0]}, porta: {client_address[1]} conectado ao servidor dns")

    else:
        print(f"Resposta recebida do endereço: {client_address[0]}, porta: {client_address[1]}, serviço pedido: {requisicao}")

        if requisicao.upper() == 'QUADRADO':

            #criando nova porta efêmera para tratar a solicitaçao
            new_server = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
            new_server.bind(('127.0.0.1', 0))

            new_solicitation = f'Sua solicitaçao será tratada na nova porta {new_server.getsockname()[1]}'
            print(new_solicitation)
            
            server_socket.sendto(new_solicitation.encode(), client_address)

            # perguntando o protocolo
            protocolo = 'Deseja se conectar via TCP ou UDP? '
            new_server.sendto(protocolo.encode(), client_address)

            # recebendo o protocolo escolhido
            data, client_address = new_server.recvfrom(1024)
            protocolo_escolhido = data.decode()

            if protocolo_escolhido.upper() == 'UDP':
                key = find_key_by_value(services, "UDP")

            elif protocolo_escolhido.upper() == 'TCP':
                key = find_key_by_value(services, "TCP")

            else:
                resposta = ('Protocolo nao existente para essa aplicaçao')
                print(resposta)
                new_server.sendto(resposta.encode(), client_address)

        else:
            print(f'serviço requerido: {requisicao}')
            print('Not found')
            server_socket.sendto('Not found, server não encontrado!'.encode(), client_address)

```
