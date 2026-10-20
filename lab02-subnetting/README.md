# Lab 02 - Subnetting (/24 dividido em 4 sub-redes /26)

## 🎯 Objetivo
Dividir a rede 192.168.1.0/24 em 4 sub-redes e verificar na prática quais dispositivos se comunicam sem roteador.

## 🗺️ Topologia
![Topologia](topologia%202.png)

## 🔢 Plano de sub-redes (máscara 255.255.255.192)

| Sub-rede | Rede | Hosts utilizáveis | Broadcast |
| :--- | :--- | :--- | :--- |
| 1 | 192.168.1.0/26 | .1 até .62 | .63 |
| 2 | 192.168.1.64/26 | .65 até .126 | .127 |
| 3 | 192.168.1.128/26 | .129 até .190 | .191 |
| 4 | 192.168.1.192/26 | .193 até .254 | .255 |

## 🔢 Tabela de Endereçamento

| Dispositivo | IP | Máscara | Sub-rede |
| :--- | :--- | :--- | :--- |
| PC-A | 192.168.1.10 | 255.255.255.192 | 1 |
| PC-B | 192.168.1.20 | 255.255.255.192 | 1 |
| PC-C | 192.168.1.70 | 255.255.255.192 | 2 |

## ✅ Testes Realizados
- PC-A → PC-B (mesma sub-rede): 4 de 4 respostas
<img width="705" height="710" alt="image" src="https://github.com/user-attachments/assets/234bf7e9-4a58-481f-a185-cf1cca63c181" />


- PC-A → PC-C (sub-redes diferentes): 100% de perda (timeout)

<img width="696" height="709" alt="image" src="https://github.com/user-attachments/assets/851f6fba-aa9c-4f15-8e47-3d16d29e22c5" />


## 📚 O que aprendi
- Dispositivos na mesma sub-rede se comunicam direto, sem gateway.
- Sub-redes diferentes só se comunicam por meio de um roteador. Sem ele, o ping dá timeout, mesmo com cabos e switch funcionando.
- Dividir /24 em 4 sub-redes empresta 2 bits e resulta na máscara /26, com blocos de 64 endereços.
