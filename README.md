# Expo common issues

Esse repositório contém uma série de erros (e suas soluções) que você pode ter com o Expo.

## Issues

  - [Expo command not found](#expo-command-not-found)
  - [Invalid Regular Expression](#invalid-regular-expression)
  - [Input is required, but Expo CLI is in non-interactive mode.](#input-is-required-but-expo-cli-is-in-non-interactive-mode)
  - [Network response timed out](#network-response-timed-out)
  - [The internet connection appears to be offline.](#the-internet-connection-appears-to-be-offline)
  - [Imagens não aparecendo no dispositivo físico](#imagens-n%c3%a3o-aparecendo-no-dispositivo-f%c3%adsico)
  - [Logo ou Texto aparecendo atrás das barra de status no Android](#logo-ou-texto-aparecendo-atr%c3%a1s-das-barra-de-status-no-android)
  - [ENOSPC: System limit for number of file watchers reached](#enospc-system-limit-for-number-of-file-watchers-reached)
  - [KeyboardAvoidingView não funciona no Android](#keyboardavoidingview-n%c3%a3o-funciona-no-android)


### **Expo command not found**

- Verifique se você instalou o `expo-cli` e se foi configurado corretamente no seu `$PATH`.

- Para mais informações sobre como instalar o `expo-cli` verifique [a documentação](https://docs.expo.io/versions/latest/introduction/installation/).

### **Invalid Regular Expression**

- Esse erro ocorre principalmente no Windows por conta de pastas que possuem espaços, pontos, acentos ou outros caracteres inválidos (ex: "Semana Omnistack" ou "C:\Users\João Pedro"). Para evitar esse erro, recomendamos que crie seu projeto na raíz do seu drive, por exemplo: "C:\SemanaOmnistack\".

- Esse erro também pode ser encontrado caso você esteja utilizando a versão 12+ do NodeJs, nesse caso, basta fazer o *downgrade* para a versão 10.

### **Input is required, but Expo CLI is in non-interactive mode.**

- Alguns terminais (git bash, por exemplo) podem bloquear a interatividade das CLIs. Inicie seu projeto com o comando: `expo init mobile --template blank`

### **Network response timed out**

- Verifique se seu computador e seu celular estão na mesma rede;
- Configurações de firewall podem influenciar:
  - Mude a configuração da sua rede de WiFi de "Pública" para "Privada" e inicie seu projeto do expo novamente;
  - Rode o comando `yarn start` ou `expo start` através do terminal do seu computador ao invés de usar o terminal embutido do VSCode;
- VMWare ou VirtualBox ou Docker podem influenciar na hora do Expo criar um endereço IP, se estiver com algum destes serviços rodando, altere a conexão de LAN para Tunnel;
- Altere a conexão de LAN pra Tunnel;

### **The internet connection appears to be offline.**

- Verifique método pelo qual você está tentando acessar aplicação. Caso opte pelo método **LAN**, verifique se o IP é no formato 192.x.x.x, se não, troque para esse formato e tente acessar a aplicação novamente. Exemplo: `exp://192.168.0.5:19000`. Se o erro persistir, opte pela conexão do tipo **Tunnel** lá na pagina do Expo e utilize a URL/QR Code disponibilizado.

### **Imagens não aparecendo no dispositivo físico**

- Altere o seguinte campo no seu Model de Spot para mostrar seu IP ao invés de localhost:
```js
SpotSchema.virtual('thumbnail_url').get(function() {
  return `http://IP_DA_SUA_REDE:3333/files/${this.thumbnail}`
})
```

### **Logo ou Texto aparecendo atrás das barra de status no Android**

- O Expo muda a cor da barra de status do Android para transparente por padrão, e isso faz com que o comportamento dos elementos funcione igual no iOS, porém a SafeAreaView não funciona no Android. A forma mais rápida de resolver isso é adicionando as seguintes linhas no seu arquivo `app.json`:
```js
{
  "expo": {
    ...
    //adicione as linhas abaixo
    "androidStatusBar": {
      "barStyle": "dark-content",
      "backgroundColor": "#ffffff"
    },
  }
}
```
- Após este processo, pare o processo do Metro Bundler do Expo apertando Ctrl + C no terminal que está rodando, e **inicie novamente**.

### **ENOSPC: System limit for number of file watchers reached**

- Em dispositivos Linux, o sistema pode ter uma certa limitação para o uso do live reload, o que ocasiona esse erro quando o diretório de algum projeto com a função ativada possui muitos arquivos. Execute o comando `echo fs.inotify.max_user_watches=524288 | sudo tee -a /etc sysctl.conf && sudo sysctl -p` em seu terminal e o problema será resolvido.

### **KeyboardAvoidingView não funciona no Android**

- Caso o componente **KeyboardAvoidingView** não tenha o comportamento esperado no _**Android**_, ajustar o _layout_ quando o teclado é exibido. Você pode tentar passar o parâmetro `behavior` como `null`, pois em dispositivos _Android_ ele se comportará melhor sem o `behavior`.

```js
import {KeyboardAvoidingView, Platform} from 'react-native';

<KeyboardAvoidingView behavior={Platform.OS === 'ios' ? 'padding' : null} >
  ... outros componentes ...
</KeyboardAvoidingView>;
```

### **expo.ps1 não pode ser carregado**

- No Windows ao executar expo init esse err ocorrerá caso o seu PowerShell não estiver habilitado para execução de scripts. Acesse o PowerShell como administrador e execute o comando abaixo para habilitar a execução.

```terminal
set-executionpolicy unrestricted 
```
