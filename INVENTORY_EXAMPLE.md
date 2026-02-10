# Exemplo de Inventário para AWX/Ansible

## Estrutura Recomendada

```
inventories/
├── production/
│   ├── hosts
│   └── group_vars/
│       └── all.yml
├── staging/
│   ├── hosts
│   └── group_vars/
│       └── all.yml
└── development/
    ├── hosts
    └── group_vars/
        └── all.yml
```

## Exemplo de hosts (INI format)

```ini
[webservers]
web1.example.com
web2.example.com

[databases]
db1.example.com
db2.example.com

[linux:children]
webservers
databases

[linux:vars]
ansible_user=admin
ansible_become=yes
```

## Exemplo de hosts (YAML format)

```yaml
all:
  children:
    webservers:
      hosts:
        web1.example.com:
        web2.example.com:
    databases:
      hosts:
        db1.example.com:
        db2.example.com:
  vars:
    ansible_user: admin
    ansible_become: yes
```

## Variáveis de Grupo (group_vars/all.yml)

```yaml
---
# Configurações gerais
ntp_server: ntp.example.com
dns_servers:
  - 8.8.8.8
  - 8.8.4.4

# Active Directory
ad_domain: maestriatec.local

# AWS
aws_region: us-east-1
```

## Uso no AWX

No AWX, configure o inventário apontando para este repositório ou crie inventários dinâmicos.
