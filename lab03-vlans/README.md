# Lab 03 - VLANs

## 🎯 Objetivo
Criar duas VLANs em um switch e verificar na prática que dispositivos em VLANs diferentes não se comunicam, mesmo estando na mesma rede IP.

## 🗺️ Topologia
![Topologia](topologia-lab03.png)


## 🔢 Plano de VLANs

| VLAN | Nome | Portas | Dispositivos |
| :--- | :--- | :--- | :--- |
| 10 | FINANCEIRO | Fa0/1, Fa0/2 | PC-A, PC-B |
| 20 | TI | Fa0/3, Fa0/4 | PC-C, PC-D |

## 🔢 Tabela de Endereçamento (rede 192.168.1.0/24, sem gateway)

| Dispositivo | IP | Máscara | VLAN |
| :--- | :--- | :--- | :--- |
| PC-A | 192.168.1.10 | 255.255.255.0 | 10 |
| PC-B | 192.168.1.20 | 255.255.255.0 | 10 |
| PC-C | 192.168.1.30 | 255.255.255.0 | 20 |
| PC-D | 192.168.1.40 | 255.255.255.0 | 20 |

## 💻 Comandos Utilizados

```
enable
configure terminal
hostname Switch-03
vlan 10
 name FINANCEIRO
exit
vlan 20
 name TI
exit
interface range fastEthernet 0/1 - 2
 switchport mode access
 switchport access vlan 10
exit
interface range fastEthernet 0/3 - 4
 switchport mode access
 switchport access vlan 20
end
write memory
```

Verificação: `show vlan brief`

![show vlan brief](show-vlan.png)

## ✅ Testes Realizados

- PC-A → PC-B (mesma VLAN 10): respondeu

<img width="707" height="715" alt="Captura de tela 2026-10-19 215717" src="https://github.com/user-attachments/assets/021d1f91-7832-4dcc-9188-93f97db1205f" />


- PC-A → PC-C (VLANs diferentes): 100% de perda (timeout)

<img width="705" height="715" alt="Captura de tela 2026-10-19 215812" src="https://github.com/user-attachments/assets/bf475fb5-c0dd-40c0-bfa2-8304fe57ed2d" />


- Teste extra: movendo a porta Fa0/1 para a VLAN 20, o ping PC-A → PC-C passou a funcionar. Ao devolver a porta para a VLAN 10, o timeout voltou.

<img width="701" height="713" alt="Captura de tela 2026-10-19 225500" src="https://github.com/user-attachments/assets/8d68cef1-a7e3-44fc-b926-7f8ffda8c246" />
<img width="700" height="709" alt="Captura de tela 2026-10-19 225053" src="https://github.com/user-attachments/assets/7aa779b6-deb3-439c-911e-85ef8c0cf776" />


## 📚 O que aprendi
- VLAN divide o switch em redes virtuais isoladas.
- Dispositivos em VLANs diferentes não se comunicam, mesmo com IP e máscara compatíveis.
- Quem pertence a uma VLAN é a porta do switch. Para mudar um PC de VLAN, muda-se a porta.
- Timeout pode ter causas diferentes: no Lab 02 era endereçamento (sub-redes diferentes), aqui é isolamento no switch (VLANs diferentes).
- Para comunicar VLANs diferentes, é preciso um roteador (próximo laboratório).
