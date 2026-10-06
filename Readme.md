# VRBox1

Projeto experimental desenvolvido em **Unity 6.4** para estudar o desenvolvimento de experiências de **Realidade Virtual (VR) em smartphones**, utilizando o **Google Cardboard XR Plugin** e dispositivos do tipo **VR Box**.

O primeiro objetivo do projeto é construir uma experiência VR extremamente simples, utilizando apenas **Gaze** (retícula/pontinho no centro da visão) como mecanismo de interação.

---

## 1. Objetivo atual

A primeira versão do projeto utiliza o exemplo oficial **HelloCardboard**, fornecido pelo Google Cardboard XR Plugin for Unity.

O experimento permite:

* visualizar uma cena 3D em modo estereoscópico;
* movimentar a cabeça e observar a câmera acompanhar o movimento;
* utilizar a retícula central (**Gaze**) para apontar para objetos;
* detectar quando um objeto está sob a retícula;
* modificar visualmente o objeto quando ele é observado.

A ideia é utilizar este projeto como base para, posteriormente, desenvolver um **jogo educacional para smartphones usados em VR Box**.

---

# 2. Ambiente utilizado

## Software

* **Unity 6.4**
* **Google Cardboard XR Plugin for Unity 1.35.0**
* Android Build Support instalado no Unity
* Git
* GitHub

## Hardware utilizado nos testes

### Computador

O projeto foi desenvolvido e configurado em um computador Windows capaz de executar o Unity 6.4 e gerar builds Android.

### Smartphone de teste

* **POCO M4 Pro 5G**
* Modelo: **21091116AG**
* Android: **13**
* Possui giroscópio

Esse aparelho foi utilizado para o primeiro teste real de VR.

> Outros smartphones Android também podem funcionar, desde que sejam compatíveis com o Cardboard e possuam os sensores necessários para rastreamento de movimento. A compatibilidade pode variar conforme o aparelho.

### Headset

* VR Box / dispositivo semelhante compatível com smartphones
* Smartphone instalado fisicamente no visor

---

# 3. Criando o projeto

Criar um projeto 3D novo no Unity.

Depois de abrir o projeto:

**Window → Package Manager**

Clique no botão:

**+ → Add package from git URL**

Utilizar o Google Cardboard XR Plugin:

```text
https://github.com/googlevr/cardboard-xr-plugin.git
```

A versão utilizada neste projeto é:

```text
1.35.0
```

Depois que o pacote for instalado:

1. Localizar **Google Cardboard XR Plugin for Unity** no Package Manager.
2. Na seção **Samples**, importar o sample **Hello Cardboard**.

Os arquivos do sample serão importados para uma estrutura semelhante a:

```text
Assets/
└── Samples/
    └── Google Cardboard/
        └── 1.35.0/
            └── Hello Cardboard/
```

---

# 4. Cena utilizada

Abrir:

```text
Assets/Samples/Google Cardboard/1.35.0/Hello Cardboard/Scenes/HelloCardboard
```

Essa é a cena principal utilizada neste primeiro experimento.

No Build Profile Android, essa cena deve estar incluída no build.

**Atenção:** inicialmente o Unity pode deixar `SampleScene` como a cena incluída no build. Neste projeto, deve ser utilizada a cena:

```text
HelloCardboard
```

---

# 5. Configuração do XR Plug-in Management

Abrir:

**Edit → Project Settings → XR Plug-in Management**

Selecionar a plataforma **Android**.

Deixar:

```text
☑ Cardboard XR Plugin
```

Não é necessário habilitar:

```text
☐ Google ARCore
☐ Mock HMD
```

Para este projeto, o único XR Provider necessário no Android é:

```text
Cardboard XR Plugin
```

---

# 6. Configuração da interação Gaze

A cena HelloCardboard já possui uma retícula central.

Na Hierarchy existe um objeto semelhante a:

```text
Player
└── Camera
    └── CardboardReticlePointer
```

Essa retícula é o ponto/crosshair que permanece no centro da visão.

## Criar a Layer Interactive

Na barra superior do Unity:

**Layer → Edit Layers...**

Criar uma nova Layer chamada:

```text
Interactive
```

## Configurar o objeto Treasure

Selecionar o objeto:

```text
Treasure
```

No Inspector, alterar sua Layer para:

```text
Interactive
```

Se o Unity perguntar se a mudança também deve ser aplicada aos objetos filhos, escolher:

```text
Yes, change children
```

## Configurar o CardboardReticlePointer

Selecionar:

```text
Player
└── Camera
    └── CardboardReticlePointer
```

No componente **Cardboard Reticle Pointer**, localizar:

```text
Reticle Interaction Layer Mask
```

Selecionar:

```text
Interactive
```

---

# 7. Configuração do Android

No Unity 6.4:

**File → Build Profiles**

Selecionar:

```text
Android
```

Caso necessário:

```text
Switch Platform
```

---

# 8. Player Settings

Abrir:

**Edit → Project Settings → Player**

Selecionar a plataforma Android.

---

## 8.1 Resolution and Presentation

Ir para:

```text
Player
└── Resolution and Presentation
```

Configurações utilizadas:

### Default Orientation

```text
Landscape Left
```

Também seria possível utilizar `Landscape Right`.

O importante é utilizar uma orientação horizontal.

### Optimized Frame Pacing

```text
OFF
```

---

# 9. Player → Other Settings

Abrir:

```text
Player
└── Other Settings
```

Configurações utilizadas:

| Opção                   | Valor                      |
| ----------------------- | -------------------------- |
| Graphics APIs           | OpenGLES3                  |
| Minimum API Level       | Android 8.0 / API 26       |
| Target API Level        | API 35 ou superior         |
| Scripting Backend       | IL2CPP                     |
| Target Architecture     | ARM64                      |
| Internet Access         | Require                    |
| Active Input Handling   | Input System Package (New) |
| Application Entry Point | Activity                   |
| GameActivity            | Desabilitado               |

## Graphics API

Neste projeto foi utilizado:

```text
OpenGLES3
```

O Vulkan não foi utilizado neste primeiro teste.

---

# 10. Target API

O Google Cardboard atualmente exige:

```text
Minimum API Level: 26
Target API Level: 35 ou superior
```

Durante o desenvolvimento deste projeto, o Unity informou:

```text
Selected target SDK version (37) is higher than the latest installed SDK version (36).
Setting target SDK version to 36.
```

Isso não impediu a geração do APK.

Assim, no computador utilizado para este projeto, o build acabou sendo realizado utilizando o SDK/API 36.

---

# 11. Scripting Backend

Em:

```text
Player → Other Settings
```

utilizar:

```text
Scripting Backend:
IL2CPP
```

Não utilizar Mono para este projeto.

---

# 12. Arquitetura Android

Em:

```text
Target Architectures
```

utilizar:

```text
☑ ARM64
```

Neste primeiro projeto foi utilizado somente ARM64.

---

# 13. Input System

Em:

```text
Active Input Handling
```

utilizar:

```text
Input System Package (New)
```

---

# 14. Application Entry Point

Em:

```text
Application Entry Point
```

utilizar:

```text
☑ Activity
☐ GameActivity
```

---

# 15. Publishing Settings

Abrir:

```text
Player
└── Publishing Settings
```

Na seção **Build**, habilitar:

```text
☑ Custom Main Gradle Template
☑ Custom Gradle Properties Template
```

---

# 16. mainTemplate.gradle

O arquivo será criado em:

```text
Assets/Plugins/Android/mainTemplate.gradle
```

Na seção de dependências, utilizar:

```gradle
implementation 'androidx.appcompat:appcompat:1.6.1'
implementation 'com.google.android.gms:play-services-vision:20.1.3'
implementation 'com.google.android.material:material:1.12.0'
implementation 'com.google.protobuf:protobuf-javalite:3.19.4'
```

---

# 17. gradleTemplate.properties

Arquivo:

```text
Assets/Plugins/Android/gradleTemplate.properties
```

Adicionar:

```properties
android.enableJetifier=true
android.useAndroidX=true
```

---

# 18. Build Profile

Voltar para:

**File → Build Profiles → Android**

Adicionar a cena:

```text
HelloCardboard
```

Utilizar **Add Open Scenes** com a cena HelloCardboard aberta para evitar esquecer de adicioná-la.

Antes do build, conferir se a lista contém a cena correta.

---

# 19. Gerando o APK

Existem duas opções principais.

## Build

Gera somente o arquivo APK.

Exemplo:

```text
Builds/VRBox1.apk
```

## Build And Run

Compila o projeto, instala o APK no smartphone conectado por USB e tenta executar o aplicativo automaticamente.

Para desenvolvimento e testes, utilizar:

```text
Build And Run
```

---

# 20. Configuração do smartphone Android

O procedimento abaixo utiliza como referência o **POCO M4 Pro 5G (21091116AG)**.

Outros aparelhos Android podem possuir menus diferentes.

---

## 20.1 Ativar modo desenvolvedor

No smartphone:

```text
Configurações
→ Sobre o telefone
```

Localizar o campo relacionado à versão do sistema/build.

Tocar aproximadamente **7 vezes** até o Android informar que as opções de desenvolvedor foram ativadas.

---

# 21. Ativar Depuração USB

Abrir:

```text
Configurações
→ Configurações adicionais
→ Opções do desenvolvedor
```

Ativar:

```text
Depuração USB
```

---

# 22. Ativar instalação via USB no POCO

No POCO, também é necessário permitir instalação de aplicativos através do USB.

Em:

```text
Opções do desenvolvedor
```

ativar:

```text
Instalar via USB
```

O nome exato pode variar conforme a versão da MIUI/Android.

Essa configuração foi necessária neste projeto.

Quando ela estava desabilitada, a Unity apresentou:

```text
INSTALL_FAILED_USER_RESTRICTED:
Install canceled by user
```

Depois de habilitar a instalação via USB, o APK pôde ser instalado normalmente.

---

# 23. Conectar o smartphone ao computador

Conectar o POCO ao computador usando um cabo USB capaz de transmitir dados.

Deixar o telefone desbloqueado.

Quando o Android perguntar:

```text
Permitir depuração USB?
```

aceitar.

Pode-se marcar:

```text
Sempre permitir deste computador
```

---

# 24. Executar o projeto diretamente no smartphone

No Unity:

```text
File
→ Build Profiles
→ Android
```

Em:

```text
Run Device
```

selecionar o smartphone conectado.

Depois:

```text
Build And Run
```

O fluxo será:

```text
Unity
  ↓
Compilação
  ↓
APK
  ↓
ADB
  ↓
Instalação no smartphone
  ↓
Execução do aplicativo
```

---

# 25. Teste dentro do VR Box

Depois que o aplicativo abrir:

1. Confirmar que a experiência está em modo estereoscópico.
2. Colocar o smartphone no VR Box.
3. Colocar o VR Box no rosto.
4. Movimentar lentamente a cabeça.
5. Observar se a câmera acompanha a direção da cabeça.
6. Utilizar a retícula central para mirar no objeto.
7. Verificar a mudança de comportamento do objeto quando ele entra na mira.

O teste real de head tracking deve ser realizado no smartphone.

---

# 26. Teste do Gaze no Editor

Também é possível testar parte da interação no próprio Unity utilizando:

```text
Play
```

No Editor, a retícula pode ser observada e a lógica de interação pode ser testada.

Entretanto, o Editor não substitui completamente o teste em um smartphone real.

O funcionamento que interessa no dispositivo é:

```text
Giroscópio do smartphone
        ↓
Head Tracking
        ↓
Movimento da câmera
        ↓
Direção da visão
        ↓
Retícula Gaze
        ↓
Interação com o objeto
```

---

# 27. Mensagem de erro observada no Editor

Durante o Play Mode no Unity pode aparecer:

```text
Please initialize Cardboard XR loader before calling this function.
```

Essa mensagem apareceu durante os testes do HelloCardboard no Editor.

Ela não impediu a geração nem a execução do APK Android.

O teste real de Cardboard deve ser realizado no dispositivo Android.

---

# 28. O que deve ser enviado ao GitHub

Um projeto Unity não deve enviar ao GitHub todos os arquivos gerados pelo Editor.

## Manter

Principalmente:

```text
Assets/
Packages/
ProjectSettings/
```

Além dos arquivos próprios de configuração/versionamento do projeto.

## Não enviar

Normalmente não devem ser versionados:

```text
Library/
Temp/
Logs/
Obj/
UserSettings/
```

e outros diretórios temporários ou gerados automaticamente pelo Unity.

---

# 29. Pasta Builds

Neste projeto foi criada:

```text
Builds/
```

O build gerou vários arquivos e pastas auxiliares.

Não é necessário enviar todos eles ao GitHub.

Os seguintes diretórios podem ser removidos:

```text
VRBox1_BackUpThisFolder_ButDontShipItWithYourGame/
VRBox1_BurstDebugInformation_DoNotShip/
```

Para este projeto, o único arquivo que interessa manter como resultado do teste é:

```text
Builds/VRBox1.apk
```

O APK atualmente possui aproximadamente **37 MB**.

---

# 30. Sugestão de .gitignore para Builds

Como queremos manter o APK mas ignorar outros arquivos gerados dentro de `Builds`, pode ser utilizada a seguinte regra:

```gitignore
Builds/*
!Builds/*.apk
```

Assim:

```text
Builds/
├── VRBox1.apk                    ← mantém
├── VRBox1_BackUpThisFolder...    ← ignora
├── VRBox1_BurstDebugInformation... ← ignora
└── outros arquivos gerados       ← ignora
```

---

# 31. Sobre o aviso de arquivo grande do GitHub

Durante o primeiro `git push`, o GitHub apresentou um aviso relacionado ao arquivo:

```text
Packages/com.google.xr.cardboard/Runtime/iOS/GfxPluginCardboard.a
```

Esse arquivo possui aproximadamente **65 MB**.

O GitHub permite arquivos abaixo de 100 MiB, mas recomenda atenção a arquivos acima de 50 MiB e sugere Git LFS para arquivos grandes.

Esse aviso não impediu o `push`.

Por enquanto, o projeto continua funcional.

---

# 32. Versão funcional atual

Estado atual do projeto:

```text
Unity 6.4
        +
Google Cardboard XR Plugin 1.35.0
        +
HelloCardboard
        +
Android
        +
ARM64
        +
OpenGLES3
        +
POCO M4 Pro 5G
        +
VR Box
        ↓
Experiência VR funcional
```

O primeiro objetivo do projeto foi alcançado:

**executar uma experiência Google Cardboard real em um smartphone Android e utilizar Gaze como mecanismo básico de interação.**

---

# 33. Próximos passos

A próxima etapa do projeto será substituir gradualmente o exemplo HelloCardboard por uma experiência própria.

A ideia é utilizar os conhecimentos adquiridos neste protótipo para desenvolver um **jogo educacional simples, original e adequado para smartphones utilizados em VR Box**.

O projeto deverá priorizar:

* baixo custo computacional;
* controles simples;
* Gaze como principal mecanismo de interação;
* funcionamento em smartphones Android;
* facilidade de instalação;
* experiência adequada para iniciantes em VR;
* possibilidade de utilização em contexto educacional.

---

## Referências

As configurações deste projeto foram baseadas principalmente na documentação oficial do **Google Cardboard XR Plugin for Unity** e na documentação oficial do Unity sobre Android e Git Package Manager.
