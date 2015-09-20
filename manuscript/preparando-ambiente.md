# Preparando o Ambiente

Para começarmos a desenvolver nossos aplicativos Android é necessário termos um ambiente de desenvolvimento mínimo em nossos computadores, assim, precisamos ter o **JDK** e o **Android SDK** instalados. Como essa apostila vai trabalhar com **Android Studio**, também vamos instala-lo, mas saiba que também é possível trabalhar usando editor de texto mais linha de comando para desenvolver seus app.

## Instalando JDK

O JDK é fundamental para o desenvolvimento Android, sendo necessário ter a versão 7 instalada para iniciar a contrução do apps, é aconselhável usar o Kit da Oracle, mas não tem problema caso quera usar outros Kit como o OpenJDk.

### Instalando Oracle JDK no Linux (Ubuntu/Linux Mint/Debian)

**No Terminal**

1. Instale as dependências com os seguintes comandos:

	```bash
	sudo apt-get install python-software-properties
	sudo add-apt-repository ppa:webupd8team/java
	sudo apt-get update
	```
2. Execute o comando para instalar o Oracle JDK 7:

	```bash
	sudo apt-get install oracle-java7-installer
	```
3. Se tiver outra versão de JDK instalada, execute o seguinte comando para escolher a versão:

	```bash
	sudo update-alternatives --config java
	```
	Algo assim será exibido:
	<center>
	![terminal](http://3.bp.blogspot.com/-dS3f2MOzSLs/Vfr_MKaMUDI/AAAAAAAAAdA/pBgudChqIUw/s400/img1.png)
	</center>
	Escolha o número da versão de sua preferência e faça o mesmo com `javac`, o compilador java, usando o comando:
	```bash
	sudo update-alternatives --config javac
	```
	Também escolha o número da versão, igual feito anteriormente.
4.  Para definir a variável `JAVA_HOME` execute o comando:
	```bash
	sudo update-alternatives --config java
	```
	Será retornado algo como:
	<center>
	![terminal](http://3.bp.blogspot.com/-dS3f2MOzSLs/Vfr_MKaMUDI/AAAAAAAAAdA/pBgudChqIUw/s400/img1.png)
	</center>
	O caminho de instalação para cada um é (nesse caso):
		* `/usr/lib/jvm/java-7-oracle/`
		* `/usr/lib/jvm/java-7-openjdk-amd64/`
		* `/usr/lib/jvm/java-7-oracle/`
	Copie o caminho escolhido anteriormente e edite o arquivo `/etc/environment`
	```bash
	sudo nano /etc/environment
	```
	Adicione no fim do arquivo:
	```bash
	JAVA_HOME="CAMINHO_ESCOLHIDO"
	```
	E execute o comando no terminal:
	```bash
	source /etc/environment
	```
	
5. Pronto!

### Instalando Oracle JDK no Windows

1. Baixe o arquivo de instalação em http://www.oracle.com/technetwork/pt/java/javase/downloads/jdk7-downloads-1880260.html
2. Execute o arquivo .exe baixado
3. No assistente, clique em Next em todas as telas até concluir a instalação

	<center>![Instalação](http://luizricardo.org/wordpress/wp-content/upload-files/2013/11/02_instalar_jdk.png)</center>
4. Acesse as **"Configurações Avançadas do Sistema"** (Ctrl + pause) e na aba Avançado, clique em variáveis de sistema

	<center>![Variáveis](http://luizricardo.org/wordpress/wp-content/upload-files/2013/11/05_configurar_var_amb.png)</center>
5. Em **"variáveis do sistema"** clique em **"Novo..."** e crie uma variável chamada `JAVA_HOME` com o valor igual ao caminho que você instalou o Java, nomalmente é `C:\Arquivos de Programas (X86)\Java\jdk-versão`

	<center>![Java Home](http://luizricardo.org/wordpress/wp-content/upload-files/2013/11/06_configurar_java_home.png)</center>
6.  Em **"variáveis do sistema"** edite a variável Path acrescentando `;%JAVA_HOME%\bin` ao final do valor

	<center>![Path](http://luizricardo.org/wordpress/wp-content/upload-files/2013/11/07_configurar_path.png)</center>
7. Pronto!

## Instalando Android Studio

### Instalação no Linux

**No terminal**

1. Adicione o repositório e atualize o APT

	```bash
	sudo apt-add-repository ppa:paolorotolo/android-studio
	sudo apt-get update
	```
2. Instale-o com o comando

	```bash
	sudo apt-get install android-studio
	```
3. Abra o Android Studio. Se for a primeira vez que estiver instalando, aperecerá a janela seguinte, marque a segunda opção e clique em **ok**

	<center>![janela](http://3.bp.blogspot.com/-gOwqAC8x15c/Vf7BTjcW7hI/AAAAAAAAAdU/WvLlcYp6zXo/s400/0.png) </center>
4. Vai abrir a janela de Boas Vindas, clique em **Next**

	<center>![janela](http://2.bp.blogspot.com/-CBlVNqagZtA/Vf7BSW_HdbI/AAAAAAAAAdM/WGa6MsOrRz0/s400/1.png) </center>
5. Na próxima janela, deixe **Standard** marcado e clique em **Next**

    <center>![janela](http://4.bp.blogspot.com/-6S41kQqTWFc/Vf7BUw3vxxI/AAAAAAAAAdo/J3PYomAYI28/s400/2.png) </center>
6. Clique em **Next** na janela **Emulator Settings**

    <center>![janela](http://1.bp.blogspot.com/-q0P-tmBlCgg/Vf7BVvkTIGI/AAAAAAAAAds/lUVc6fNi9Mc/s400/3.png) </center>
7. Vai aparecer a janela que mostra os pacotes para serem instalados, clique em **Next**

    <center>![janela](http://2.bp.blogspot.com/-J-kY73E2llY/Vf7BUJEt6dI/AAAAAAAAAdY/nxw4mm9St_4/s400/4.png) </center>
8. Aguarde o assistente baixar os pacotes nescessários

	<center>![janela](http://2.bp.blogspot.com/-gKN-GNfbvdk/Vf7BUzU_uXI/AAAAAAAAAdg/UN5pJRx9teo/s400/5.png) </center>
9. Depois que baixar todos os arquivos, clique em **Finish**

	<center>![janela](http://3.bp.blogspot.com/-CZ0VZ_3SIMs/Vf76fgiR_9I/AAAAAAAAAeA/dKfHgckCO5k/s400/6.png) </center>
10. Pronto! A tela inicial será exibida

	<center>![janela](http://1.bp.blogspot.com/--StoPYJUzB0/Vf76f96KVLI/AAAAAAAAAeE/38ndKeQyQHI/s400/7.png) </center>
### Instalando no Windows

1. Baixe o Android Studio em https://developer.android.com/sdk/index.html
2. Instale o arquivo baixado (clique em **Next** em tudo)
3. Pronto!


## Instalando Pacotes necessários (Android SDK)

1. Abra o Android Studio e clique em **Configure**

	<center>![Studio](http://1.bp.blogspot.com/--StoPYJUzB0/Vf76f96KVLI/AAAAAAAAAeE/38ndKeQyQHI/s400/7.png)</center>
2. Clique em **SDK Manager**

	<center>![Studio](http://1.bp.blogspot.com/-ih4p4QRtn8k/Vf8HTxZBc_I/AAAAAAAAAeU/YtHKuI3K0HA/s400/8.png)</center>
3. Vai abrir uma janela. Vá em *Extra* e marque **Android Support Library** e **Google Play Services** e clique em **Install 2 packages**

	<center>![Studio](http://1.bp.blogspot.com/-k3-w0rJUxcQ/Vf8HUQeyQdI/AAAAAAAAAeg/sHtdQwQxcEs/s400/9.png)</center>
4. Aceite os termos e clique em **Install**

	<center>![Studio](http://2.bp.blogspot.com/-OW6oA_att54/Vf8HT3Sb1jI/AAAAAAAAAeY/Y-fwF3SYKFc/s400/10.png)</center>
5. Espere baixar e pronto! Pode sair do **SDK Manager**

	<center>![Studio](http://2.bp.blogspot.com/-guSFiaj-M6c/Vf8HT3p_cJI/AAAAAAAAAec/QaUZlSWvAKA/s400/11.png)</center>

## Ativando Modo de Depuração no Celular

Durante a criação dos nossos aplicativos, vamos precisar roda-los várias vezes para ver os resultados, para isso será necessário o uso de um emulador ou de um dispositivo com Android. Quando instalamos o Android Studio, ele automaticamente cria uma maquina virtual para a gente, porém para rodar os app em nossos dispositivos é necessário que ative o **modo Depuração**.

* Em dispositivos com Android 3.2 ou mais inferior, você deve ir em **Configurações > Aplicativos > Desenvolvimento** e marcar **Depuração USB**
	<center>![Debug](http://www.escolaandroid.com/wp-content/uploads/2014/01/depuracao-usb-1.png)</center>	

* Em dispositivos com Android 4.0 ou superior, vá em **Configurações > Opções de Desenvolvedor** ou **Configurações > Programador** e marque **Depuração USB**
	<center>![Debug](http://www.escolaandroid.com/wp-content/uploads/2014/01/depuracao-usb-2.png)</center>	
	
