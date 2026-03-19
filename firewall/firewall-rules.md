# Configuração de Firewall - MikroTik

## 📌 Objetivo
Garantir a segurança da rede, controlando acessos e bloqueando conexões indevidas.

## 🔧 Regras aplicadas

```bash
/ip firewall filter
add chain=input action=accept connection-state=established,related comment="Permitir conexões estabelecidas"
add chain=input action=drop connection-state=invalid comment="Descartar conexões inválidas"
add chain=input action=accept protocol=tcp port=8291 src-address=192.168.0.0/24 comment="Acesso Winbox interno"
add chain=input action=drop comment="Bloquear acessos externos não autorizados"

## 💬 Comentário

À partir do terminal no MikroTik, em "filter rules" e "address list", é possível verificar e configurar regras de proteção de firewall, que podem variar desde a liberação específica de IPs até o bloqueio de portas e conexões.

As configurações são adaptadas conforme as necessidades do ambiente corporativo, garantindo maior controle e segurança da rede.
