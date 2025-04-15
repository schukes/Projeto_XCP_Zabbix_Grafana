# ✅ Projeto: Instalação Completa de um Servidor de Monitoramento com XCP-ng, Xen Orchestra, Zabbix e Grafana

## 1. 📥 Download e Criação do Boot com XCP-ng

- Acesse o site oficial:  
  👉 [XCP-ng](https://xcp-ng.org/)  
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

- Baixe: 👉 [XCP-ng Center](https://github.com/xcp-ng/xenadmin/releases)  
- Adicione o host via IP e senha root.

---

## 5. 📦 Upload da ISO do Ubuntu no XCP-ng

- Baixe o Ubuntu Server 22.04.5:  
  👉 [Ubuntu Server](https://ubuntu.com/download/server)  
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

  - sudo apt update && sudo apt upgrade -y
  - apt install apache2 php libapache2-mod-php mysql-server unzip curl wget gnupg2 software-properties-common openssh-  -     -  server -y

---

## 8. 📊 Instalação do Zabbix
  - Acesse: Zabbix Download
  - Escolha:
  - Distribuição: Ubuntu 22.04
  - Versão: 7.0 LTS (ou a mais recente)
  - Banco de dados: MySQL
  - Instalação exemplo: (site com tutorial oficial https://www.zabbix.com/br/download)

  - wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_7.0-1+ubuntu22.04_all.deb
  - sudo dpkg -i zabbix-release_7.0-1+ubuntu22.04_all.deb
  - sudo apt update
  - sudo apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent -y

  - Configure o banco de dados:
  - CREATE USER zabbix@localhost IDENTIFIED BY 'Zabbix@123';
  - Finalize a instalação via navegador.

## 9. 📈 Instalação do Grafana

  - sudo apt install -y software-properties-common
  - sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
  - wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
  - sudo apt update
  - sudo apt install grafana -y
  - sudo systemctl start grafana-server
  - sudo systemctl enable grafana-server
  - Acesse: http://IP_DA_VM:3000
  - Usuário: admin
  - Senha: Admin@123

##10. 🔄 Integração Zabbix + Grafana

  - Em Configuration > Data Sources, adicione o Zabbix como fonte de dados.

##11. 🖥️ Instalação do Agente Zabbix

  - Download do agente no site oficial https://www.zabbix.com/br/download

  - Windows
  - Salve os arquivos em:
  - C:\Users\Usuario\Documents\agente_zabbix (tente manter um padrão pode salvar em outra pasta também)

  - Instalação:
  - zabbix_agentd.exe -i -c "C:\Users\Usuario\Documents\agente_zabbix\zabbix_agentd.win.conf"
  - Remoção:
  - zabbix_agentd.exe -d -c "C:\Users\Usuario\Documents\agente_zabbix\zabbix_agentd.win.conf"

  - Após instalar, inicie o serviço do Zabbix.

Linux
  - sudo apt update
  - sudo apt install -y gnupg
  - wget https://repo.zabbix.com/zabbix-official-repo.gpg
  - sudo apt-key add zabbix-official-repo.gpg
  - echo "deb https://repo.zabbix.com/zabbix/7.0/ubuntu stable main" | sudo tee /etc/apt/sources.list.d/zabbix.list
  - sudo apt update
  - sudo apt install zabbix-agent -y
  - sudo nano /etc/zabbix/zabbix_agentd.conf
  - sudo systemctl restart zabbix-agent
  - sudo systemctl status zabbix-agent

## 12. 👤 Credenciais de Acesso (Exemplos)

  - Sistema	Usuário	Senha
  - Ubuntu Server	monitor	Senha@123
  - Zabbix Frontend	Admin	Zabbix@123
  - Grafana	Admin	Grafana@123
  - Xen Orchestra	root	Xoa@123

## 13. ✅ Conclusão
  - Você terá um ambiente de monitoramento completo com:
  - 🧩 XCP-ng como hipervisor
  - 🎛️ Xen Orchestra para gerenciamento
  - 🐧 Ubuntu Server como base
  - 📡 Zabbix para monitoramento
  - 📊 Grafana para dashboards visuais
