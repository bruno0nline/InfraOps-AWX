# 🚀 InfraOps-AWX

![Ansible](https://img.shields.io/badge/Ansible-EE0000?style=flat&logo=ansible&logoColor=white)
![AWX](https://img.shields.io/badge/AWX-EE0000?style=flat&logo=ansible&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)

Projeto de automação de infraestrutura com **AWX/Ansible**, focado na padronização, provisionamento e gerenciamento centralizado de ambientes Linux e recursos de rede.

> 📚 Projeto desenvolvido durante curso de AWX para automação de infraestrutura

## 📋 Sobre o Projeto

Este repositório contém playbooks Ansible para automatizar tarefas comuns de infraestrutura, incluindo:

- ✅ Integração de servidores ao Active Directory (Join AD)
- ✅ Configuração de DHCP e registros DNS via Route 53
- ✅ Instalação de pacotes por distribuição (Debian e RedHat)
- ✅ Aplicação de atualizações de sistema
- ✅ Criação de usuários e permissões de acesso
- ✅ Instalação e configuração de serviços (Apache, etc)

**Objetivo:** Garantir agilidade, consistência e segurança nas operações de infraestrutura.

---

## 📁 Estrutura do Projeto

```
InfraOps-AWX/
├── README.md                      # Documentação principal
├── LICENSE                        # Licença MIT
├── CONTRIBUTING.md                # Guia de contribuição
├── INVENTORY_EXAMPLE.md           # Exemplos de inventário
├── .gitignore                     # Arquivos ignorados pelo Git
├── ansible.cfg.optimized          # Configuração otimizada do Ansible
│
├── adduser.yml                    # Criação de usuários
├── config_dhcp.yml                # Configuração DHCP
├── install-apache.yml             # Instalação Apache
├── install-packages.yml           # Instalação de pacotes (genérico)
├── install-packages-debian.yml    # Instalação de pacotes Debian
├── install-packages-redhat.yml    # Instalação de pacotes RedHat
├── join_ad.yml                    # Integração com Active Directory
├── linux-update.yml               # Atualização de sistemas Linux
├── ping.yml                       # Teste de conectividade
├── r53.yml                        # Gerenciamento Route 53 (AWS)
├── site.yml                       # Playbook principal de exemplo
├── tags.yml                       # Exemplo de uso de tags
├── windows_updates.yml            # Atualização de sistemas Windows
│
└── collections/
    └── requirements.yml           # Dependências de collections
```

---

## 🔧 Pré-requisitos

- **Ansible** 2.9+ ou **AWX** instalado
- Acesso SSH aos hosts gerenciados
- Credenciais apropriadas (AD, AWS, etc)
- Python 3.x nos hosts gerenciados

### Instalação de Collections

```bash
ansible-galaxy collection install -r collections/requirements.yml
```

---

## 🎯 Como Usar

### 1. Teste de Conectividade

```bash
ansible-playbook -i inventory ping.yml
```

### 2. Atualização de Sistemas Linux

```bash
ansible-playbook -i inventory linux-update.yml
```

### 3. Integração com Active Directory

```bash
ansible-playbook -i inventory join_ad.yml \
  -e "ad_user=admin" \
  -e "ad_password=SenhaSegura" \
  -e "ad_group=LinuxAdmins"
```

### 4. Instalação de Pacotes (Debian)

```bash
ansible-playbook -i inventory install-packages-debian.yml
```

### 5. Configuração Route 53 (AWS)

```bash
ansible-playbook -i inventory r53.yml
```

### 6. Criar Usuário

```bash
ansible-playbook -i inventory adduser.yml
```

---

## 🏷️ Uso de Tags

O playbook `tags.yml` demonstra o uso de tags para execução seletiva:

```bash
# Executar apenas tarefas com tag específica
ansible-playbook tags.yml --tags "install"

# Pular tarefas com tag específica
ansible-playbook tags.yml --skip-tags "config"
```

---

## 🔐 Segurança

⚠️ **Importante:** Nunca commite credenciais no repositório!

Recomendações:
- Use **Ansible Vault** para variáveis sensíveis
- Configure credenciais no AWX (Credentials)
- Use variáveis de ambiente ou arquivos externos

Exemplo com Ansible Vault:
```bash
ansible-vault create secrets.yml
ansible-playbook playbook.yml --ask-vault-pass
```

---

## 🌐 Integração com AWX

Para usar estes playbooks no AWX:

1. **Criar Projeto** no AWX apontando para este repositório
2. **Configurar Credenciais** (Machine, AWS, etc)
3. **Criar Inventário** com seus hosts
4. **Criar Job Templates** para cada playbook
5. **Executar** ou agendar as automações

---

## 📚 Playbooks Detalhados

### `join_ad.yml`
Integra servidores Linux ao Active Directory usando `realmd` e `sssd`.

**Variáveis necessárias:**
- `ad_user`: Usuário com permissão para join
- `ad_password`: Senha do usuário
- `ad_group`: Grupo AD para permissões sudo

### `linux-update.yml`
Atualiza pacotes do sistema (apt/yum) de forma idempotente.

### `r53.yml`
Gerencia registros DNS no AWS Route 53.

**Requer:** Collection `community.aws` e credenciais AWS configuradas.

### `config_dhcp.yml`
Configura servidor DHCP em sistemas Linux.

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para:

1. Fazer fork do projeto
2. Criar uma branch para sua feature (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona MinhaFeature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abrir um Pull Request

---

## 📝 Licença

Este projeto é de código aberto e está disponível para uso educacional e profissional.

---

## 👤 Autor

**Bruno** - [@bruno0nline](https://github.com/bruno0nline)

---

## 🎓 Sobre o Curso

Este projeto foi desenvolvido como parte de um curso de AWX focado em automação de infraestrutura, cobrindo:

- Fundamentos de Ansible e AWX
- Automação de tarefas de infraestrutura
- Integração com Active Directory
- Gerenciamento de recursos AWS
- Boas práticas de IaC (Infrastructure as Code)

---

## 📞 Suporte

Para dúvidas ou sugestões, abra uma [issue](https://github.com/bruno0nline/InfraOps-AWX/issues) no repositório.
