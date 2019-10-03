# Expo common issues

Esse repositório contém uma série de erros (e suas soluções) que você pode ter com o Expo.

### **Expo command not found**

- Verifique se você instalou o `expo-cli` e se foi configurado corretamente no seu `$PATH`.

- Para mais informações sobre como instalar o `expo-cli` verifique [a documentação](https://docs.expo.io/versions/latest/introduction/installation/).

### **Network response timed out**

- Verifique se seu computador e seu celular estão na mesma rede;
- Configurações de firewall podem influenciar:
  - Mude a configuração da sua rede de WiFi de "Pública" para "Privada" e inicie seu projeto do expo novamente;
  - Rode o comando `yarn start` ou `expo start` através do terminal do seu computador ao invés de usar o terminal embutido do VSCode;
- VMWare ou VirtualBox ou Docker podem influenciar na hora do Expo criar um endereço IP, se estiver com algum destes serviços rodando, altere a conexão de LAN para Tunnel;
- Altere a conexão de LAN pra Tunnel;

### The internet connection appears to be offline.

- Verifique método pelo qual você está tentando acessar aplicação. Caso opte pelo método **LAN**, verifique se o IP é no formato 192.x.x.x, se não, troque para esse formato e tente acessar a aplicação novamente. Exemplo: `exp://192.168.0.5:19000`. Se o erro persistir, opte pela conexão do tipo **Tunnel** lá na pagina do Expo e utilize a URL/QR Code disponibilizado.
