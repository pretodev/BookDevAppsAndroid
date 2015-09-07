# INICIANDO PROJETO PERTA

### Criando um Projeto Android 
Para começar a desenvolver nossa aplicação android, primeiro temos que criar um projeto no Android Studio, nele teremos todos os arquivos necessário para construir um aplicativo completo. O passos seguintes ensinará como criar nosso projeto.
> Nota: Você já deve ter instalado o Android Studios, se não consulte o capitulo um deste modulo.

1. No Android Studio, crie um novo projeto
    * Se não possuir projeto aberto, clique em **Start a new Android Studio project**
    * Se possuir projeto aberto, vá em **file->New Project**
2.  Em **Configure your new project** preencha os campos
    * **Application Name** é o nome do aplicativo que vai ser mostrado para os usuários. Nesse projeto use o nome "PerTA".
    *  **Company Domain** defini um qualificador para o aplicativo que também será usado pelo Android Studio para criar os pacotes java. Coloque o valor "com.example".
    *  **Package Name** é o nome completo do qualificador do projeto (seguindo as mesma regras da nomeclatura de pacotes do java). Não altere nada.
    *  **Projection Location** é onde o projeto vai ficar no seu computador. Mude para onde quiser.
3. Em **Select the form factors your app will run on** você pode definir as plataformas e a versão minima do Android que o aplicativo vai rodar.
    * Marque apenas **Phone e Tablet** e selecione para **Minimum SDK** a API 10: Android 2.3.3(Gingerbread).
4. Em **Add an activity to Mobile** você defini o template base para sua primeira Tela.
    * Escolha **Blank Activity**
5. **Customize the Activity** defini algumas propriedades da tela:
    * **Activity Name**: nome da classe que vai ter a lógica da tela
    *  **Layout Name**: nome do arquivo xml que vai ter o layout da tela
    *  **Title**: titulo da tela. Coloque "PerTA"
    *  **Menu Resource Name**: nome do arquivo xml que possui todos itens do menu dessa tela
6. Clique em **Finish** para criar seu projeto.
##### Arquivos do Projeto
Após um tempo o projeto é criado e podemos ver varios arquivos e pastas criadas:
1. *app/manifest/AndroidManifest.xml*
    * Arquivo que descreve as caracteriscas fundamentais do projeto
2. *app/java/com.example.perta*
    * Pacote com classes Java do projeto
3. *app/res/layout*
    * Arquivos xml com os layouts do projeto
4. *app/res/menu* 
    * Arquivos xml com opções de todos os menu projeto
5. *app/res/values*
    * Arquivos xml com constantes do projetos
6. *app/res/mipmap*
    * Imagens usadas no projetos, exemplo icones
    
### Executando seu aplicativo
Quando criamos um projeto no Android Studio, ele gera um template inicial que já podemos executar e visiualizar em nossos dispositivos ou em emulador.
##### Executando o aplicativo em um Dispositivo Real
Se você possui um dispositivo com Android e quer rodar o aplicativo nele, faça os passos seguintes.
###### Configurando o Dispositivo
1. Conecte o dispositivo via USB ao seu PC. Se estiver usando Windows, você vai precisar instalar os drivers para o seu dispositivo.
2. Ative a Depuração USB em seu dispositivo
    * Para Android 3.2 ou inferior: **Configurações > Aplicações > Desenvolvedor**
    * Para Android 4.0 ou superior: **Configurações > Opções do Desenvolvedor**
    > Em dispositivos com Android 4.2 ou superior essa opção fica escondida, para liberar vá em **Configurações > Sobre** e clique 7 vezes em Número da versão.
###### Rodando o Aplicativo
1. Selecione um modulo e clique **Run** ![Run](https://developer.android.com/images/tools/as-run.png) na barra de ferramentas ou use o atalho *Shift+F10*
2. Quando a janela **Choose Device** aparecer, selecione o dispositivo e aperte **OK**
3. Espere e veja o aplicativo em seu dispositivo

![Aplicativo Rodando no dispositivo](http://3.bp.blogspot.com/-bimu1b2K5QQ/Ve1Hbgv6PrI/AAAAAAAAAb4/80mZ_e7CQGs/s400/Screenshot_2015-09-06-23-01-19_framed.png)

Aplicativo Rodando em Dispositivo Android
##### Executando o aplicativo no Emulador
O Android SDK também permite que você emule um ou vários dispositivo Android em seu computador, isso permite que veja como seu aplicativo se comporta em dispositivos com configurações diferentes.
###### Criando Dispositivos Virtual
1.  Vá em **Tools > Android > AVD Manager**, ou clique no icone  ![AVD](https://developer.android.com/images/tools/avd-manager-studio.png) na barra de ferramenta
2.  Na tela do **AVD Manager**, clique em **Create Virtual Device**
3.  Em **Select Hardware**, selecione uma configuração de dispositivo, como Nexus 6, e clique em **Next**
4.  Selecione imagem com a versão do Android de sua preferência e clique em **Next**
5.  Verifique as configurações e aperte em **Finish**
###### Rodando o Aplicativo com Emulador
1. Selecione um modulo e clique **Run** ![Run](https://developer.android.com/images/tools/as-run.png) na barra de ferramentas ou use o atalho *Shift+F10*
2. Quando a janela **Choose Device** aparecer, clique em **Launch Emulator**
3. Selecione o Dispositivo Virtual e aperte **OK**
4. Espere e veja o aplicativo rodando

![Aplicativo Rodando no emulador](http://3.bp.blogspot.com/-21Zzv-SCjX4/Ve1EpnInnpI/AAAAAAAAAa0/hPd5Ia5hk4o/s640/emulador-launch.png)

Aplicativo Rodando em Dispositivo Android
### Criando Interface de Usuário
Agora que você já sabe criar e executar seus projetos, vamos começar a trabalhar em nosso projeto. Primeiro, vamos criar a interface gráfica do nosso projeto.
#### Introdução a Views
A interface gráfica de uma aplicação Android é construída usando uma hierarquia de objetos `Views` e `ViewGroups`. Views são componentes da interface de usuário como butões e campos de texto, já os ViewGroups são containeis invisiveis que define como os Views serão exibidos na tela, como Grades e Listas.

Android fornece varios elementos XML correspondente a subclasses de Views e ViewsGroups para ser usados para construção de hierarquias de elementos na interface de usuário.

![Hierarquia da Interface de usuário](https://developer.android.com/images/viewgroup.png)
#### Criando um FrameLayout
1. Vá para pasta *res/layout* e abra o arquivo *activity_main.xml*
    * Esse arquivo terá um `RelativeLayout` e um `TextView` porque escolhemos *BlankActivity* anteriormente, na construção do projeto
2. No painel de visualização que vai abrir, na parte inferior, clique em **Text**
    * Por padrão, o Android Studio abri o painel de visualização quando abrimos um layout, onde podemos editar elementos arrastando e largando, mas nessa aula iremos trabalhar diretamente com o XML
3. Delete o elemento `<TextView>`
4. Mude o `<RelativeLayout>` para `<FrameLayout>`
5. Remova os atributos `android:padding` e `tools:context`

O resultados deve ser esse:

*res/layout/activity_main.xml*
```xml
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">
</FrameLayout>
```
`FrameLayout` é um container (subclasse de `ViewGroup`) que serve para mostrar apenas um componente (`View`).

Os atributos `android:layout_width` e `android:layout_height` são obrigadores para qualquer componente elemento de layout, já que são eles que definem a altura e largura do componente. Como `FrameLayout` é o elemento raíz do nosso layout ele deve preencher toda a ela, por isso sua altura e largura devem ter o valor `match_parent`. Esse valor define que elemento deve preencher todas as dimenções dentro do elemento pai.

#### Adicionando uma Lista
1. No arquivo *activity_main.xml*, dentro de `<FrameLayout>`, adicione o elemento `<ListView>` com o atributo `id` definido como `@+id/listview_places`
2. Defina a largura e altura como `match_parent`

Seu layout deve ter ficado assim:
*res/layout/activity_main.xml*
```xml
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <ListView
        android:id="@+id/listview_places"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>

</FrameLayout>
```
O atributo `android:id` define um indentificador unico para o elemento, com isso podemos manipula-lo posteriormente.

### Adicionando Dados a lista
Agora que temos nosso layout pronto, vamos adicionar um pouco de código Java que vai adicionar dados a nossa lista. Vá em *java/com.example.perta* e abra a classe `MainActivity`, essa classe representa a tela Inicial da nossa aplicação.
#### Criando Dados estáticos
Dentro da classe `MainActivity` encontre o método `onCreate()` e coloco que no fim dele o array:
```java
String [] places = {
        "Santo Amaro",
        "Santo Antonio de Jesus",
        "São Francisco do Conde",
        "Cachoeira",
        "Bom Jesus",
        "Feira de Santa",
        "Amelia Rodrigues",
        "São Sebastião do Passé",
        "Birimbau",
        "Madre de Deus",
        "São Felix",
        "Candeia",
        "Muritiba",
        "Governador Mangabeira",
        "Saubara"
};
```
#### Buscando um View
Como foi dito anteriormente, todo layout é contruído com uma hierarqui de elementos, esses elementos podem ser encontrados dentro do layout para que possamos manipulalos a nosso gosto, para isso é necessário que os elementos de um layout tenha um *id*, onde podemos referencia-lo em nosso código Java. Veremos como pegar o `ListView` em nosso layout.

Dentro de `MainActivity`, no fim do método `onCreate()`, adicione o código seguinte:

```java
ListView listView = (ListView) findViewById(R.id.listview_places);
```
O metódo `findViewById()` busca um View em nosso Layout usando o *id* do elemento, esse id é referenciado pela classe `R`, essa classe é criada automaticamente pela a IDE para guardar todos os elementos da pasta *res* (IDs de elementos, layouts, strings, etc). 

Depois de encontrado o elemento, nós o armazenamos na variavel `listView`, como `ListView` é filha de `View` precisamos apenas de cast.

> Nota: Você deve estar se perguntando como a classe MainActivity sabe qual layout buscar o elemento. Quando a classe foi criada, ela recebeu o código `setContentView(R.layout.activity_main);` que define o layout da classe.

#### Criando um Adapter
Para que possamos colocar dados em um `ListView` é necessário haja um mediador nesse processo, para isso temos os `Adpaters`, a grosso modo, eles pega os elementos de um conjunto de dados e transforma cada elemento do conjunto em `View`, assim podendo ser usados tanto em listas quanto grades.

Para criar nosso `Adapter`, adicione o código seguinte ao fim do metódo `onCreate()`
```java
ArrayAdapter<String> adapter = new ArrayAdapter<String>(this,
    android.R.layout.simple_list_item_1, places);
```
Com isso, definimos um adapter que recebe `String`. O parametros que passamos foram:
* this: contexto da nossa aplicação, em outras palavras, um ponto de acesso a informações globais do sistema
* android.R.layout.simple_list_item_1: layout de elemento da lista
* places: dados da lista

#### Adicionando o Adapter a uma lista
Por fim temos que adicionar nosso Adapter a lista, isso é bem simples, basta adicionar ao fim de `onCreate()` o código:
```java
listView.setAdapter(adapter);
```

Pronto, rode e aplicação e veja o resultado.

![Aplicativo Rodando](http://3.bp.blogspot.com/-sTecoXVdBp0/Ve1Hbn-fqrI/AAAAAAAAAb8/lgkhRVJpM5M/s400/Screenshot_2015-09-07-04-52-15_framed.png)








