# Lab 01 - Rede Básica com Switch e Endereçamento IPv4

## 🎯 Objetivo
Configurar uma topologia simples de rede local (LAN) conectando 2 hosts a um switch central, atribuindo IP estático e testando a conectividade de ponta a ponta.

## 🗺️ Topologia
![Topologia do Laboratório](topologia.png)

## 🔢 Tabela de Endereçamento

| Dispositivo | Interface | Endereço IP  | Máscara de Sub-rede | Gateway Padrão |
| :---        | :---      | :---         | :---                | :---           |
| PC-A        | FastEth0  | 192.168.1.10 | 255.255.255.0       | N/A            |
| PC-B        | FastEth0  | 192.168.1.20 | 255.255.255.0       | N/A            |
| Switch-01   | VLAN 1    | 192.168.1.2  | 255.255.255.0       | N/A            |

## 💻 Comandos Utilizados

### Configuração inicial do Switch (CLI)
```
enable
configure terminal
hostname Switch-01
interface vlan 1
 ip address 192.168.1.2 255.255.255.0
 no shutdown
end
write memory
```

## ✅ Testes Realizados
<img width="707" height="714" alt="image" src="https://github.com/user-attachments/assets/2a1d980f-3eb8-4514-993d-ca15c29212f6" />


- PC-A → PC-B:
- PC-A → Switch-01:
- PC-B → Switch-01:
- PC-A → PC-B: 4 de 4 respostas (0% de perda)
- PC1 → Switch-01: 3 de 4 respostas (o primeiro pacote falhou por causa do ARP)

## ❓ Perguntas
1. Por que não precisamos de gateway nesta topologia? O gateway é a “porta de saída” da rede local: o equipamento (um roteador) que leva os pacotes para outras redes. Aqui, PC-A, PC-B e Switch-01 estão todos na mesma rede (192.168.1.0), então conversam direto, sem sair dela. Por isso o gateway é N/A.
2. O que o switch faz com o endereço IP da VLAN 1? O switch encaminha o tráfego entre PC-A e PC-B usando o endereço MAC, e para isso não precisa de IP. O IP na VLAN 1 (uma interface virtual) serve para gerenciar o switch: dá para pingar, acessar por Telnet/SSH e configurar à distância. Foi por isso que ele respondeu ao seu ping.
3. O que significa a máscara /24? A máscara 255.255.255.0 é escrita como /24 porque tem 24 bits ligados. Esses 24 bits (os 3 primeiros números) identificam a rede, e o último número identifica o host. Rede: 192.168.1 | Host: .10 (PC-A), .20 (PC-B), .2 (switch) | Uma rede /24 tem 256 endereços, mas 254 utilizáveis: o .0 é o endereço da rede e o .255 é o broadcast.

## 📚 O que aprendi
- Não foi preciso configurar gateway, pois PC-A, PC-B e Switch-01 estão na mesma rede (192.168.1.0/24) e se comunicam diretamente.
- O primeiro ping pode falhar porque o dispositivo ainda precisa descobrir o MAC do destino via ARP. Os seguintes funcionam normalmente.
- O TTL mostra o tipo de equipamento: 128 no PC (Windows) e 255 no switch Cisco.
- Estar ligado ao mesmo switch não significa estar na mesma rede: quem define isso é o IP junto com a máscara.
