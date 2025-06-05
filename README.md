# 🎬 Como Instalar o DaVinci Resolve com GPU AMD

Este repositório contém um passo a passo para configurar o **DaVinci Resolve** com placas de vídeo **AMD**. Também inclui dois scripts (`Davinci-Pre-Install-Fix.sh` e `Davinci-Pos-Install-Fix.sh`) que automatizam partes do processo.

<br>

### 👉🏼 Tutorial realizado no Fedora, mas os passos são semelhantes para outras distribuições Linux.
---

<br>

## 📦 Pré-requisitos

- Ambiente Linux instalado e atualizado  
- Placa de vídeo AMD compatível  

<br>

---

<br>

## 🚀 Passo a Passo

### 1. Instale as bibliotecas necessárias

Execute o script de pré-instalação `Davinci-Pre-Install-Fix.sh`:

<br>

Modo automático com script .sh:
```bash
chmod +x Davinci-Pre-Install-Fix.sh
./Davinci-Pre-Install-Fix.sh
```

<br>

Modo manual sem script .sh:
```bash
sudo dnf install libxcrypt-compat libcurl libcurl-devel mesa-libGLU
```

<br>

### 2. Baixe o instalador oficial

Acesse o site oficial da Blackmagic Design e baixe a versão mais recente do DaVinci Resolve:  
[https://www.blackmagicdesign.com/br/products/davinciresolve/](url)

<br>

### 3. Torne o instalador executável

Após o download, descompacte (se necessário) e dê permissão ao arquivo `.run`:

```bash
chmod +x ./DaVinci_Resolve_<versao>.run
```

<br>

### 4. Ignore a verificação de pacotes (zlib)

Se ocorrer um erro relacionado à biblioteca `zlib`, você pode ignorar a checagem de pacotes ao executar o instalador com a variável de ambiente `SKIP_PACKAGE_CHECK=1`:

```bash
SKIP_PACKAGE_CHECK=1 ./DaVinci_Resolve_<versao>.run
```

<br>

### 5. Remova bibliotecas conflitantes

Após a instalação do DaVinci Resolve, execute o script de pós-instalação para remover bibliotecas desnecessárias que podem impedir o programa de abrir corretamente:

<br>

Modo automático com script .sh:
```bash
chmod +x Davinci-Pos-Install-Fix.sh
./Davinci-Pos-Install-Fix.sh
```

<br>

Modo manual sem script .sh:
```bash
cd /opt/resolve/libs
sudo mkdir disabled-libraries
sudo mv libglib* disabled-libraries
sudo mv libgio* disabled-libraries
sudo mv libgmodule* disabled-libraries
```

<br>

### 6. Corrija o erro de GPU (AMD)

Se ao iniciar o DaVinci Resolve aparecer a mensagem de erro: `Unsupported GPU Processing Mode`  

<br>

Isso indica que o suporte à GPU AMD ainda não está configurado corretamente. Para resolver, instale o pacote rocm-opencl:  

```bash
sudo dnf install rocm-opencl
```

<br>
<br>


### 💡 Dica: Pacotes adicionais da ROCm
Caso o erro de GPU persista, experimente instalar os seguintes pacotes adicionais:

<br>

⚠️ Não precisa instalar todos. Teste um de cada vez (linha por linha) para verificar se irá resolver o erro de GPU do DaVinci Resolve.
```bash
sudo dnf install rocm
sudo dnf install rocminfo
sudo dnf install rocm-opencl
sudo dnf install rocm-clinfo
sudo dnf install rocm-hip
sudo dnf install rocm-runtime
```

🦎 Solução OpenSuse:
```bash
sudo zypper install Mesa-libOpenCL
```
