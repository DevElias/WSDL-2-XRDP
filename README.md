# Guia de Instalação WSL 2 + XRDP

 1. Etapa 1 – Habilitar o Subsistema do Windows para Linux
 
    1.1 - Digite em seu navegador: http://aka.ms/wsl para acessar a documentação da Microsoft WSL;
    1.2 - Abra o Power Shell como Administrador e execute o comando abaixo:
    
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    
    1.3 - Reiniciar o Computador
    
 2. Abrir a Store Microsft e baixar o sistema operacional desejado, neste exemplo baixei o Ubuntu 20.04 LTS

    ![image](https://user-images.githubusercontent.com/14336962/114484803-3db2b180-9be1-11eb-9661-3d3c83a9b89c.png)
    
 3. Configurar usuário e senha do Linux

 4.  Abra o Power Shell como Administrador, para habilitar o recurso de Máquina Virtual, digitando o seguinte código:

    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    
 5. Próximo passo é baixar o pacote de atualização do kernel do Linux:

    https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi
    
 6. Next e Finish para instalar o pacote;
 7. Abra o Power Shell como administrador e digite o comando
    
    wsl --list (para listar as distribuições instaladas no sistema);
    
  8. Agora você precisa definir a versão 2 do WSL na sua distribuição linux:

     wsl --set-version Ubuntu-20.04 2
     
  9. Caso você tenha tido algum problema ao setar a versão 2 do WSL, vc pode verificar a razão da falha utilizando o seguinte comando no power sheall:

     Systeminfo.exe
     
     ![image](https://user-images.githubusercontent.com/14336962/114486362-1d382680-9be4-11eb-8bc8-ec3f591b308b.png)
     
     9.1 - Nesse exemplo acima, tive problemas com a configuração de virtualização do windows, foi necessário habilitar a virtualização no firewall do windows;
     9.2 - Também tive que habilitar a virtualização direto na BIOS da minha placa mãe, essa configuração varia de modelo para modelo.
     9.3 - Para ter certeza estamos na v2 da WSL é necessário aparecer Conversão Concluída após rodar o comando -> wsl --set-version Ubuntu-20.04 2

     ![image](https://user-images.githubusercontent.com/14336962/114487715-743efb00-9be6-11eb-8a04-1ca722967dcf.png)
     
     9.4 - Por último para realmente verificar em que versão esta sua distribução linux, você pode executar o comando:
      
       wsl -l -v
       
       ![image](https://user-images.githubusercontent.com/14336962/114487864-b1a38880-9be6-11eb-89ed-2d9446fd7374.png)
       
    9.5 - Caso necessite reiniciar a instância em algum momento, execute o comando abaixo:

       wsl --shutdown
       
 # Guia de configuração para acessar o servidor remotamente com interface (xrdp)
 
 Passo 1 - Instalando xRDP
 
 sudo apt-get update
 sudo apt-get install xrdp
 
 Passo 2 - Instalando XFCE4
 
 sudo apt-get install xfce4
 
 Passo 3 - Instale o terminal XFCE4 e o pacote de icones
 
 sudo apt-get install xfce4-terminal
 
 sudo apt-get install gnome-icon-theme-full tango-icon-theme
 
 Passo 4 - Configura o xRDP
 
 echo xfce4-session >~/.xsession
 
 Passo 5 - Editar o arquivo
 
 nano /etc/xrdp/startwm.sh
 
 Adicione isso na última linha do arquivo: startxfce4
 
 ![image](https://user-images.githubusercontent.com/14336962/114904344-24328500-9dee-11eb-9463-c7ce9275768b.png)

  Passo 6 - Reiniciar o xRDP
  
  sudo service xrdp restart
  
  Passo 7 - Para verificar o IP de acesso:
  
  hostname -I
  
  Passo 8 - Abrir a conexão remota do windows ou mac e adicione o ip de conexão:
  
  ![image](https://user-images.githubusercontent.com/14336962/114904974-ceaaa800-9dee-11eb-8442-92a83738ac30.png)

  Passo 9 - Entre como session Xorg, seu usuario do linux e senha:
  
  ![image](https://user-images.githubusercontent.com/14336962/114905190-0d406280-9def-11eb-9afc-334687b1529a.png)
  
  * Comando para abrir google chrome vinculado a pastas: google-chrome --user-data-dir="tmp"
  
  Tutorial de apoio: https://www.tweaking4all.com/software/linux-software/use-xrdp-remote-access-ubuntu-14-04/
