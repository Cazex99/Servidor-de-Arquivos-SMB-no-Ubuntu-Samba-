##  1. Atualizar o sistema (OBRIGATÓRIO)

Antes de qualquer configuração, atualize o sistema:

```bash
sudo apt update && sudo apt upgrade -y

```
Isso garante segurança e evita problemas de dependência.

## 2.Criar o usuário Linux

```bash
sudo adduser teste


```
Defina a senha e conclua o cadastro.

```bash
sudo apt update && sudo apt upgrade -y

```

## 3. Criar a pasta compartilhada
Crie o diretório dentro do /home do usuário:
```bash
mkdir /home/teste/arquivos

```


## 4. Ajuste dono e permissões:
```bash
sudo chown -R teste:teste /home/teste/arquivos
chmod 775 /home/teste/arquivos

```


## 5. Instalar o Samba (SMB)
Instale o serviço SMB:
```bash
sudo apt install samba -y


```
## 6. Verifique a instalação:

```bash
smbd --version

```


## 07. Criar senha do Samba
A senha do Samba não é a mesma do usuário Linux.
```bash
sudo smbpasswd -a teste
sudo smbpasswd -e teste

```


## 8. Configurar o compartilhamento
Edite o arquivo de configuração do Samba:
```bash
sudo nano /etc/samba/smb.conf

```


## 9. Configurar o compartilhamento parte dois
NÃO apague o conteúdo existente.

Role até o final do arquivo e adicione:
```bash
[Arquivos]
path = /home/teste/arquivos
browseable = yes
writable = yes
valid users = teste
create mask = 0664
directory mask = 0775

```
Salve:

Ctrl + O → Enter

Ctrl + X

## 10. Reiniciar o Samba

```bash
sudo systemctl restart smbd
sudo systemctl enable smbd

```


## 11. Verifique o status:

```bash
systemctl status smbd

```


## 12. Teste de acesso Windows.
Windows+r (para abrir o executar)

Coloque \\IP_DO_UBUNTU\Arquivos ou somente o IP.

Usuário: teste
Senha: senha configurada no smbpasswd

## 13. Teste de acessi Linux.
Abra explorador de arquivos do linux e vá em Outro locais:
<img width="881" height="546" alt="Captura de tela 2025-12-19 020322" src="https://github.com/user-attachments/assets/dce5d9b2-6914-4887-8f4b-7ca80090d658" />
e digite, smb://IP_DO_UBUNTU + nome da pasta compartilhada.

Usuário: teste
Senha: senha configurada no smbpasswd
