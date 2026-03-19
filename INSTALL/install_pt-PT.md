# Como Instalar o NVIDIA NemoClaw: Guia Passo a Passo

O NemoClaw é uma stack de código aberto da NVIDIA projetada para executar agentes de IA OpenClaw com segurança, adicionando controles de privacidade, sandboxing e barreiras de segurança.

Siga estes passos simples para configurar e executar seu agente de IA seguro.

## Pré-requisitos

Antes de começar, certifique-se de que seu sistema atende aos seguintes requisitos:

* **Sistema Operacional:** Linux (Ubuntu 22.04+ recomendado). macOS e Windows (via WSL2) são suportados, mas em fase experimental.
* **Hardware:** Pelo menos 8 GB de RAM (16 GB altamente recomendado) e cerca de 40 GB de espaço livre em disco.
* **Chave de API:** Uma Chave de API da NVIDIA (você pode obter uma gratuitamente em `build.nvidia.com`).

## Passo 1: Prepare o seu sistema

O NemoClaw requer a instalação do Docker e Node.js (versão 20 ou 22) para funcionar corretamente.

### 1. Verifique o Docker:

Certifique-se de que o Docker está instalado e que você tem as permissões corretas sem precisar usar `sudo` toda vez:

```bash
docker ps
```

(Se você receber um erro de permissão negada "permission denied", execute `sudo usermod -aG docker $USER`, faça logout e login novamente).

### 2. Instale o Node.js:

Execute os seguintes comandos para instalar o Node.js (versão 22):

```bash
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs
```

Verifique a instalação executando `node --version`.

## Passo 2: Instale o NemoClaw

A NVIDIA fornece um script de instalação simples que cuida do trabalho pesado.

Execute o seguinte comando no seu terminal:

```bash
curl -fsSL https://nvidia.com/nemoclaw.sh | bash
```

Nota: Dependendo da configuração do seu sistema, pode ser necessário executá-lo com `sudo bash` se encontrar erros de permissão.

## Passo 3: Configure o seu agente (Onboarding)

Após a conclusão da instalação, você precisará configurar o seu sandbox e as configurações de inferência.

Execute o assistente de configuração:

```bash
nemoclaw onboard
```

Durante este processo interativo:

* Dê um nome ao seu assistente (por exemplo, `my-assistant`).
* Insira sua Chave de API da NVIDIA quando solicitado.
* Aceite as configurações padrão para as políticas de segurança e a configuração do sandbox.

Nota: O script fará o download da imagem do sandbox (aprox. 2,4 GB). Isso pode levar alguns minutos.

## Passo 4: Conecte-se e converse!

Seu ambiente seguro agora está pronto. É hora de se conectar ao seu agente isolado.

### 1. Conecte-se ao sandbox:

Substitua `my-assistant` pelo nome que você escolheu no Passo 3.

```bash
nemoclaw my-assistant connect
```

### 2. Inicie a interface de chat:

Uma vez dentro do sandbox isolado, inicie a Interface de Usuário em Texto (TUI) do OpenClaw:

```bash
openclaw tui
```

Parabéns! Agora você pode digitar mensagens com segurança e interagir com seu agente de IA isolado.

## Dicas de Solução de Problemas

* **Erros de Falta de Memória (OOM):** Se a instalação falhar em uma máquina com 8 GB de RAM, tente adicionar espaço de troca (swap space) ao seu sistema.
* **Usuários do WSL2:** Se você estiver usando o Subsistema Windows para Linux e tiver problemas com a passagem de GPU (GPU passthrough) durante o `nemoclaw onboard`, pode ser necessário iniciar o gateway OpenShell manualmente sem a flag `--gpu`.
