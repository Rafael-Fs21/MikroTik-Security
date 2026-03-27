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

## 📊 𝐈𝐍𝐅𝐎𝐑𝐌𝐀ÇÕ𝐄𝐒 𝐅𝐈𝐑𝐄𝐖𝐀𝐋𝐋 - 𝐌𝐈𝐊𝐑𝐎𝐓𝐈𝐊

O Firewall do mikrotik funciona no modo "Default Accept", isso significa que ele por ádrão, aceita todos os pacotes, podendo mudar essa política através de regras.

As regras são lidas de forma individual, ou seja, não há interferencia em sua posição, visando canal para canal. Caso sejam regras do mesmo canal, exemplo: input, então há sim interferência na ordem.

As regras de firewall se comportam e atuam com regras "simples", sendo "se e então". Isso ou aquilo. 

    FIREWALL
      \/
  NEW FIREWALL
      \/
 GENERAL - ADVANCED - ACTION

É como se General fosse o "se" e o action o "então". Tendo essa visão, pode-se configurar regras do firewall, colocando o que ele deve ou não fazer, aprovar ou bloquear algo.

  TIPOS DE ADDRESS

Se tem o ADDRESS Src e o Dst.

- Src (Source Address) - Endereço de quem envia.
- Dst (Destination Address) - Endereço que recebe.

##Exemplo:

Bloquear o acesso ao endereço listado
Chain: forward
Dst. Address: 1.1.1.1
Protocol: tcp
Dst Port: 443
Action: Drop

Agora só falta definir em "action" o que será feito, como "drop", "accept".




## 🧱 𝐂𝐚𝐦𝐚𝐝𝐚𝐬 𝐝𝐞 𝐩𝐫𝐨𝐭𝐞çã𝐨

** Segurança de Mikrotik não se baseia somente na camada 3 e 4, Rede e porta, mas também na camada 2, que é super importante**

## 💬 Comentário

À partir do terminal no MikroTik, em "filter rules" e "address list", é possível verificar e configurar regras de proteção do firewall,
que podem variar desde a liberação específica de IPs até o bloqueio de portas e conexões.

As configurações são adaptadas conforme as necessidades do ambiente corporativo, garantindo maior controle e segurança da rede.




