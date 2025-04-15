# ✅ Projeto: Instalação Completa de um Servidor de Monitoramento com XCP-ng, Xen Orchestra, Zabbix e Grafana

## 1. 📥 Download e Criação do Boot com XCP-ng

- Acesse o site oficial:  
  👉 https://xcp-ng.org/  
- Baixe a ISO mais recente do XCP-ng.
- Crie um pendrive bootável com [Rufus](https://rufus.ie/):
  - Selecione a ISO e o pendrive.
  - Escolha o modo “MBR” (ou UEFI, dependendo do hardware).
  - Clique em **Iniciar**.

## 2. 💻 Instalação do XCP-ng no Servidor

- Dê boot com o pendrive.
- Siga as instruções de instalação:
  - Selecione disco.
  - Configure senha de root.
  - Defina IP fixo, se necessário.
  - Escolha a fonte de repositório (internet/local).
- Reinicie após a instalação.

## 3. 🌐 Acesso à Internet (Firewall)

Se você usa firewall (ex: Fortigate), **libere o acesso à internet para o IP do servidor XCP-ng** durante a instalação.

## 4. ⚙️ Gerenciamento do XCP-ng

**Opção 1 – Xen Orchestra (Recomendado):**

- Acesse via navegador: `http://IP_DO_SERVIDOR`
- Clique em "Xen Orchestra" e siga as instruções.

**Opção 2 – XCP-ng Center (Windows):**

- Baixe: 👉 https://github.com/xcp-ng/xenadmin/releases  
- Adicione o host via IP e senha root.

---

## 5. 📦 Upload da ISO do Ubuntu no XCP-ng

- Baixe o Ubuntu Server 22.04.5:  
  👉 https://ubuntu.com/download/server  
- Crie um **Storage Repository (SR)** para armazenar a ISO.

## 6. 🖥️ Criação da Máquina Virtual Ubuntu

- Crie uma VM com:
  - **Sistema:** Linux / Ubuntu 64-bit
  - **Disco:** 50 GB
  - **RAM:** 2 GB+
  - **vCPUs:** 2+
- Configure:
  - IP fixo
  - Nome de host
  - Usuário: `monitor`
  - Senha: `Senha@123`
  - Instale o OpenSSH Server (se quiser acesso remoto)

---

## 7. 🧰 Pós-instalação do Ubuntu

sudo apt update && sudo apt upgrade -y
sudo apt install apache2 php libapache2-mod-php mysql-server unzip curl wget gnupg2 software-properties-common openssh-server -y
