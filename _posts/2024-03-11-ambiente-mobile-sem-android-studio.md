---
title: Ambiente Mobile sem Android Studio
date: 2024-03-11 18:50:00 -300
categories: [Code, Mobile, flutter]
tags: [code]
lang: pt-br
---

*Método de 18/07/2020 e originalmente postado no meu [Dev.to](https://dev.to/pedrohti/flutter-sem-android-studio-54nl) durante estudos mobiles*

![](/assets/img/drake_androidstudio.png "Meme Drake rejeita Android Studio")

Apesar do mobile estar em alta, demorei para procurar sobre esse mundo. Tenho uma pequena base de React Native mas só agora resolvi estudar Flutter e conhecer essa nova plataforma que tem a "mãozinha" da Google envolvida.
Mas logo de cara me deparei com um sério problema: preparar o ambiente **SEM** o Android Studio.

E pensando nisso criei esse post com os passos que segui para conseguir fazer funcionar o ambiente mobile sem o Android Studio e receber os checks✔️ do flutter doctor.

OBS:* Nada contra ao Android Studio, acredito que ele seja uma ótima ferramenta, mas prefiro algo mais leve e "moldável", digamos.

&nbsp;

**Índice**

<!-- 1. [Ambiente Android](#p1)
2. [Flutter](#p2)
3. [Variáveis de Ambiente](#p3)
   1. [Android](#p31)
   2. [Path](#p32)
4. [Android SDK](#p4)
5. [Licenças do Android](#p5)
6. [Configurar SDK no Flutter](#p6)
7. [Emulador](#p7)
8. [VSCode](#p8)
9.  [Hora da Verdade](#p9)
10. [Resultado](#resultado)
11. [Fim](#fim) -->

&nbsp;

**Vamos lá!**

## 1º Passo - Ambiente Android

Baixe o pacote com o SDK e o OpenJDK [Google Drive](https://drive.google.com/file/d/1Ew_TVBn1IX_yGgszbx3j2hjGVQjg6oDs/view)

Crie a pasta Android na raiz da unidade que queira instalar o ambiente e dentro dela as pastas do OpenJDK e SDK

```
F:\Android\openjdk
F:\Android\sdk 
```

Extraia o pacote nas suas respectivas pastas.

## 2º Passo - Flutter

Instale o flutter de acordo com o seu sistema operacional [Flutter](https://flutter.dev/docs/get-started/install)

No meu caso estou utilizando Windows<br>
Criei a pasta ``Flutter`` e extraia os arquivos baixados nesta pasta.

```
F:\Flutter
```

## 3º Passo - Variáveis de Ambiente

Defina as variáveis de ambiente e o path do windows apontando para a pasta do Flutter e do Android

```
Iniciar > Sistema > Alterar Configurações > Avançado > Variáveis de Ambiente
```
ou
```
Tecla do Windows + PauseBreak > Alterar Configurações > Avançado > Variáveis de Ambiente
```

Eu defini todas as minhas variáveis na parte de baixo, ou seja, são Variáveis de Sistema e não só do Usuário, mas fique a seu critério.

Clique em "novo" e defina:

#### Android

```
ANDROID_HOME=F:\Android\
ANDROID_SDK_ROOT=F:\Android\sdk
```

![](/assets/img/variaveis_ambiente1.png "Criar variável de ambiente ANDROID_HOME")

### Path

Só clicar em Novo e adicionar as linhas separadamente

```
F:\Flutter\bin
F:\Android\sdk
F:\Android\sdk\bin
F:\Android\sdk\tools\bin
F:\Android\sdk\emulator
```
ls
![](/assets/img/variaveis_ambiente2.png "Adicionar novas variáveis")

## 4º Passo - Android SDK

Baixe o que falta do SDK (system images, platform tools, build tools, platforms e o emulator) através dos comandos abaixo:

```
sdkmanager system-images;android-28;google_apis;x86_64
sdkmanager platform-tools
sdkmanager build-tools;28.0.3
sdkmanager platforms;android-28
sdkmanager emulator
```

No dia desta postagem a versão mais recente era 30. Mas acredito que o suporte da versão 28 seja mais ampla.

Caso queira a lista das versões disponíveis utilize:
```
sdkmanager --list
```

### 5º Passo - Licenças Android

Aceite as lincenças do Android

```
sdkmanager --licenses
```

digite ``y`` e aperte ``enter`` para cada licença

## 6º Passo - Configurar SDK no Flutter

Faça com que o Flutter enxergue o Android SDK

```
flutter config — -android-sdk F:\Android\
```

## 7º Passo - Emulador

Crie o emulador com o nome que deseja, basta substituir o ``nexus``

```
avdmanager -s create avd -n nexus -k system-images;android-28;google_apis;x86_64
```

Se preferir, pode criar baseado em um dispositivo real. Eu gosto do Pixel XL, pois quando utilizei com React Native funcionou numa boa (e está melhor)

**Pixel XL**

```
avdmanager -s create avd -n PixelXL -k system-images;android-28;google_apis;x86_64 -d 19
```

**Execute o dispositivo emulado**

```
emulator.exe -avd PixelXl
```

ou

```
flutter emulators --launch PixelXl
```

A princípio, a diferença entre esses dois comandos é que pelo flutter você não precisa ficar "preso" a um cmd aberto.

**Para ver os emuladores criados utilize:**

```
avdmanager list avd
```

**Para ver a lista de dispositivos disponiveis utilize:**

```
avdmanager list device
```

**Caso queira deletar um emulador criado utilize:**
```
avdmanager delete avd -n PixelXl
```


## 8º Passo - VSCode

Instale a extensão do Flutter no seu VSC

[Dart Code Flutter VSC](https://marketplace.visualstudio.com/items?itemName=Dart-Code.flutter)

![](/assets/img/vsc_flutter.png "Instalar extensão FLutter VSC")

## 9º Passo - Hora da Verdade

Rode o ``doctor`` e veja se está tudo correto

```
flutter doctor
```

ou

```
flutter doctor -v
```

![Done](/assets/img/flutter_doctor.png "Resultado Doctor")



## Resultado

![](/assets/img/resultado.png "Emulador")


## Fim

Ficou um pouco extenso, mas é exatamente com estes passos que consegui instalar e emular de maneira mais promissora após muito tempo tentando e sempre ter algum problema. Agora está tudo certo!<br> Não sou nenhum expert e nem sou um desenvolvedor mobile, mas espero que tenha ajudado de alguma forma.

Até logo! 👋