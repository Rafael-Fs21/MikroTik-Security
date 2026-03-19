# Configuração de VPN - MikroTik

## 📌 Objetivo
Permitir acesso remoto seguro à rede corporativa.

## 🔧 Configuração

- Tipo: PPTP / L2TP
- Autenticação com usuário e senha
- Pool de IP para clientes VPN

## 📡 Exemplo

```bash
/interface pptp-server server set enabled=yes
/ppp secret add name=usuario password=senha service=pptp
/ip pool add name=vpn-pool ranges=192.168.10.2-192.168.10.10
