## Referência [Linuxize - How to install and configure samba on centos 7](https://linuxize.com/post/how-to-install-and-configure-samba-on-centos-7/)

### Grupos Criados no Servidor

| ID | Grupo |
| ----- | ------- |
| 2001 | sambashare |
| 2002 | gerencia |
| 2003 | rh |
| 2004 | financeiro |

### Usuários Criados no Servidor

| Usuários | Grupos |
| -------- | ------ |
| smbadmin | sambashare gerencia rh financeiro |
| gerencia | sambashare gerencia rh financeiro |
| rh | sambashare rh |
| financeiro | sambashare financeiro |
| normaluser | sambashare |

### Arquivo SMB Config

```
[global]
        workgroup = SAMBA
        security = user
        passdb backend = tdbsam
        printing = cups
        printcap name = cups
        load printers = yes
        cups options = raw
        map to guest = Bad User

[administrativo]
	path = /sambashares/administrativo
	browseable = yes
	read only = no
	create mask = 770
	force create mode = 770
	directory mask = 770
	force directory mode = 770
	inherit owner = yes
	force group = sambashare
	valid users = @sambashare
```

#### Observação

Pastas e arquivos que precisam ser restritos a algum grupo, basta mudar o ownership da pasta/arquivo para o grupo esperado.

**Ex.: chown -R smbadmin:gerencia ./RH/RESTRITO**

Os grupos dos usuários são muito importantes. São eles que definem as pastas com restrições
