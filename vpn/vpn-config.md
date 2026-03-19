# Configuração de VPN - MikroTik

## 📌 Objetivo
Permitir acesso remoto seguro à rede corporativa.

## 🔧 Configuração

- Tipo: PPTP / L2TP / WIREGUARD
- Autenticação com usuário e senha
- Pool de IP para clientes VPN

## 📡 Exemplo

```bash
/interface pptp-server server set enabled=yes
/ppp secret add name=usuario password=senha service=pptp
/ip pool add name=vpn-pool ranges=192.168.10.2-192.168.10.10

## 🏷️ Procedimentos / Nomeclaturas

### Tipos:

Site to Site.
Client to Site.

## ⚙️ Métodos

1 - Criar Interface Wareguard - Criando túnel da VPN. 
     \/      \/        \/
 MTU (Unidade máxima de transmissão) // Indica a quantidade de transferência.
        \/       \/
     OVERHEAD/PAYLOAD
       FRAGMENTAÇÃO

MTU sempre menor que o valor suportado do dispositivo para ser possível a transferência do overhead e a fragmentação dos dados caso necessário.
           \/
Listen port - Porta da VPN
Recomendação: Alterar para evitar porta padrão.
- - - - - - - - - - 

2 - Definir IP da VPN
        \/
     INTERFACE
        \/
    NEW ADRRESS

Definir a interface da wireguard criada e o IP - IP NOVO.
Colocar /30 ou /32 é um método interessante, gerando 4 partições. 
- - - - - - - - - -
3 - Criar o Peer - Com quem a VPN vai se conectar/comunicar
                           \/
                   WIREGUARD - PEERS - FILIAL 1
                           \/
CRIAR INTERFACE DE ONDE SERÁ CONECTADO PARA GERAR A PUBLIC KEY NA FILIAL 2
                           \/
                     WINBOX - FILIAL 2
                           \/
                        WIREGUARD
                           \/
    **PODE COLOCAR A MESMA PORTA QUE A JA CRIADA PARA PADRONIZAR** 
                 **GERAR CHAVE PUBLIC KEY**
                           \/
     COLOCAR A CHAVE CRIADA NO PEERS PARA FAZER A CONEXÃO - FILIZAL 1
                           \/
                        ENDPOINT
**CASO TENHA UM  IP FIXO É MELHOR, MAS SE NÃO TIVER DEIXA EM BRANCO**
                           \/
                      ENDPOINT PORT
              **PORTA CRIADA NO WIREGUARD**

** O RESTANTE VAMOS PREENCHENDO COM O**



## 💬 Comentários

A configuração de VPN em ambientes corporativos permite acesso remoto seguro à rede interna, sendo amplamente utilizada para administração de sistemas e suporte técnico.

A escolha do protocolo, autenticação e controle de acesso deve ser feita considerando segurança, desempenho e compatibilidade com o ambiente.
