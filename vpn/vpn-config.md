# Configuração de VPN - MikroTik

## 📌 Objetivo
Permitir acesso remoto seguro à rede corporativa entre empresa: Matriz - Filial. 

## 🔧 Configuração

- Tipo: WIREGUARD
- Estilo: Site to Site
- Pool de IP para redes VPN

## 📡 Exemplo

```bash
/interface pptp-server server set enabled=yes
/ip pool add name=vpn-pool ranges= 10.100.10.1/30 - 10.100.10.2/30

## 🏷️ 𝐏𝐫𝐞𝐜𝐞𝐝𝐢𝐦𝐞𝐧𝐭𝐨𝐬/𝐍𝐨𝐦𝐞𝐜𝐥𝐚𝐭𝐮𝐫𝐚𝐬

### 𝐓𝐢𝐩𝐨𝐬:

Site to Site.
Client to Site.

## ⚙️ 𝐌é𝐭𝐨𝐝𝐨𝐬

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
** o - Tunel. 1 - Rede 1. 2 - Rede 2. 3 - Broadcast**
- - - - - - - - - -
3 - Criar o Peer - Com quem a VPN vai se conectar/comunicar
                           \/
                   WIREGUARD - PEERS - MATRIZ
                           \/
CRIAR INTERFACE DE ONDE SERÁ CONECTADO PARA GERAR A PUBLIC KEY DA MATRIZ
                           \/
                     WINBOX - MATRIZ
                           \/
                        WIREGUARD
                           \/
    **PODE COLOCAR A MESMA PORTA QUE A JA CRIADA PARA PADRONIZAR** 
                 **GERAR CHAVE PUBLIC KEY**
                           \/
     COLOCAR A CHAVE CRIADA NO PEERS PARA FAZER A CONEXÃO - (QUANDO FIZER O PEERS DA FILIAL1)
                           \/
                        ENDPOINT
**CASO TENHA UM  IP FIXO É MELHOR, MAS SE NÃO TIVER DEIXA EM BRANCO**
                           \/
                      ENDPOINT PORT
              **PORTA CRIADA NO WIREGUARD**

** O RESTANTE VAMOS PREENCHENDO COM O**

#### 🚨 IMPORTANTE!!
VAMOS FAZER AGORA ESSE MESMO PREENCHIMENTO DO OUTRO LADO, PARA CONECTAR TUDO DE VEZ.
- - - - - - - - - - - 
##🌐 𝐈𝐏 𝐂𝐨𝐧𝐟𝐢𝐠𝐮𝐫𝐚çã𝐨

Importante entender que o wareguard é uma interface, então como as outras é necessário estabelecer o IP para que funcione, e estabelecer a porta (Wireguard). Da qual precisa ser criada. 

            WIREGUARD
               \/
CRIAR INTERFACE COM MTU E SETAR A PORTA

** Com isso, é gerada a interface para setar no ip que será criado**

        IP ADDRESS
            \ /
             +
            \ /
 SELECIONAR INTERFACE WAREGUARD
            \ /
 CRIAR BLOCO DE IP NOVO (USANDO .1 E .2)

** Como exemplo já citado, usando /30 ou /32**
Exemplo: 10.100.10.1/30 - Matriz
Exemplo: 10.100.10.2/30 - Filial 1
- - - - - - - - - - -
##🖇️ 𝐏𝐞𝐞𝐫𝐬

** A configuração do peers é simples, basta ter a porta, public key e interface para conectar**
** Para a public key ser gerada, precisamos criar uma interface na filial, igual se faz na matriz**
**Lembrando que iremos preencher o peers da matriz primeiro, por isso precisamos da key da filial1**
** Campo de "Preshare key" podemos deixar em auto, ou se tiver um IP fixo também podemos colocar**
** Na configuração de Peers da FILIAL, o "ENDPOINT" é primordial. Ele é o IP da matriz, no caso, o IP da WAN que está cadatrado na interface da matriz**
- - - - - - - - - - - 
** Nesse momento já se deve ter conexão e comunicação**
- - - - - - - - - - -
##🤖 𝐎𝐒𝐏𝐅

ROUTING
\/
OSPF
\/
INSTANCIA



## 💬 Comentários

A configuração de VPN em ambientes corporativos permite acesso remoto seguro à rede interna, sendo amplamente utilizada para administração de sistemas e suporte técnico.

A escolha do protocolo, autenticação e controle de acesso deve ser feita considerando segurança, desempenho e compatibilidade com o ambiente.

 RESUMO DESSA PARTE: Criar o wireguard padrão, criar um IP novo, mas sempre setando .1 e .2, para organizar. No peers, usamos a chave publica para a comunicação de ambos os lados. Preenchemos "interface", "Public key", "Endpoint" e "Endpoint port". (Lembrando que a mesma port nos 2 lados).


