# CONECTANDO O PERTA A NUVEM

### Introdução
No capítulo anterior, criamos nossa primeira interface de usuário, porém os dados ainda estão estáticos. Nesse capítulo, veremos como integrar nosso app internet usando a API do PerTA para pegar locais baseados na localização do usuário.

### API do PerTA
Vamos deixar nosso aplicativo 10x melhor usando dados reais da API do PerTA. Ela fornece locais próximo a um determinando local. Veja mais em http://sites.ecomp.uefs.br/perta/descricao-do-projeto/comunicacao-entre-interface-e-servidor-1.

A API é bastante simples, sendo necessário apenas uma requisição GET para conseguir os dados. A requisição pode ser feita para o seguinte URL:

	http://adam.uefs.br/perta/api/geocode/json?query=museu&lat=-12.967925402533108&lgt=-38.50484848022461&k=3&raio=1000

Parâmetros:

- **query**: ponto de interesse do usuário, pode ser um local especifico, uma categoria ou pode deixar vazio.
-  **lat** e **lgt**: é a latitude e longitude do local de referência
-  **k**: quantidade locais que será retornado
-  **raio:** distância máxima entre o ponto de referência e os locais de busca

Colocando a URL anterior no navegador, obtemos o seguinte resultado:

```json
[
	{"name":"Solar do FerrÃ£o","lgt":-38.5082721,"id":8966,"pageid":"1892020","category":"tourism","subcategory":"museum","lat":-12.9725383},
	{"name":"Museu Afro-Brasileiro","lgt":-38.509838,"id":8368,"pageid":"13782","category":"tourism","subcategory":"museum","lat":-12.972785},
	{"name":"Arena Fonte Nova","lgt":-38.50416666666667,"id":1914063,"pageid":"3014418","category":"","subcategory":"categoria nÃ£o informada","lat":-12.97861111111111}
]
```
Nosso próximo passo é integrar a nossa aplicação com a API do PerTA.

### Definindo um Ponto de Referência

Como vimos, para usarmos a API do PerTA precisamos definir um ponto de referência de busca. Esse ponto é dado pela latitude e longitude decimais de um local, por enquanto vamos usar um valor fixo, mas depois veremos como pegar a localização atual do usuário. Então abra a classe `MainActivity` e coloque as variáveis abaixo dentro do método `onCreate()`:

```java
double lat = -12.54667; //latitude
double lgt = -38.71194; // longitude
```
Está são as coordenadas de Santo Amaro, Bahia. Para outras coordenadas http://www.mbi.com.br/mbi/biblioteca/utilidades/dddcepba/.

### Adicionando método de Requisição

Agora que temos nosso ponto de referência, vamos fazer código que vai fazer requisição ao nosso servidor. 

1. Adicione o seguinte método a classe `MainActivity`:
```java
private String request(double lat, double lgt){
    // Esses dois precisam ser declarados antes do try/catch
    // para serem fechados no finnaly.
    HttpURLConnection urlConnection = null;
    BufferedReader reader = null;

    // Recebe o arquivo JSON em formato de String.
    String placesJsonStr = null;

    try {
        // Constroi a URL da requisição
        URL url = new URL("http://adam.uefs.br/perta/api/geocode/json" +
                "?query=&lat=" + lat + "&lgt=" + lgt + "&k=20&raio=1000");

        // Cria a requisição com o PerTA API e abri uma conexão
        urlConnection = (HttpURLConnection) url.openConnection();
        urlConnection.setRequestMethod("GET");
        urlConnection.connect();

        // Ler o input stream
        InputStream inputStream = urlConnection.getInputStream();
        if (inputStream == null) {
            // Não tem nada
            return null;
        }
        reader = new BufferedReader(new InputStreamReader(inputStream));

        // Guarda as linhas do JSON
        String line;
        placesJsonStr = "";
        while ((line = reader.readLine()) != null) {
            placesJsonStr += line + "\n";
        }

        return placesJsonStr;
    } catch (IOException e) {
        Log.e("PlaceholderFragment", "Error ", e);
        // Executa cada dê algum erro
    } finally{
        if (urlConnection != null) {
            urlConnection.disconnect();
        }
        if (reader != null) {
            try {
                reader.close();
            } catch (final IOException e) {
                Log.e("PlaceholderFragment", "Error closing stream", e);
            }
        }
    }

    return null;
}
```
2.	Chame o método adicionado depois da array places usando as variáveis criadas anteriormente
```java
...
String [] places = {
	...
};

double lat = -12.54667; //latitude
double lgt = -38.71194; // longitude
request(lat, lgt);
...
```

 3. Execute o app 
 
> Nota: ocorrerá um erro no aplicativo, falaremos disso logo mais

### Mensagens de LOG

Dentro do método request exitem algumas classes chamadas `Log`, ela serve para mandar mensagens de LOG, essas mensagens podem ser vistas na caixa **Android** do Android Studio, ela fica localizada na parte inferior da IDE.
![LOG](http://3.bp.blogspot.com/-3mq4xBFfppg/VfUF84blTqI/AAAAAAAAAcc/77sYPAdnE7s/s640/erro.png)
Existem os seguintes tipos de mensagens:

```java
Log.v()   // Verboso
Log.d()   // Debug
Log.i()	  // Informação
Log.w()	  // Alerta
Log.e()   // Erro
```
Usaremos este recurso para mostrar informações em tempo de execução em nosso aplicativo.

### Trabalhando em plano fundo

Quando o aplicativo for executado no estado atual ele deve retornar um erro, isso ocorreu por causa da requisição que tentamos fazer. Android não permite que executamos operações que gaste tempo na Thread principal, isso porque essa thread é responsável por fazer todas as operações de renderização de componentes na tela, assim se formos fazer um requisição pode parar o aplicativo. 

Assim, precisaremos criar uma segunda Thread que rode em background no nosso app usando o `AsyncTask`. Essa classe possui o método `doInBackground()` que faz as operações em segundo plano. 

#### Criando um AsyncTask

1. Dentro de `MainActivity` crie a classe `FetchPlaceTask`
2. Faça a classe estender `AsyncTask<Void, Void, Void>`
3. Adicione o método `doInBackground()` à classe, use Ctrl + I
4. Mova o método `request()` para dentro de `FetchPlaceTask`
5. Adicione o seguinte código à `doInBackground()`
```java
double lat = -12.54667; //latitude
double lgt = -38.71194; //longitude
String placesJsonStr = request(lat, lgt);
Log.v("Places", placesJsonStr);
```

#### Executando o AsyncTask

Basta adicionar o seguinte código ao método `onCreate()`
```java
new FetchPlaceTask().execute();
```

Agora execute o app

### Permissões

Ocorreu novamente um erro em seu aplicativo, isso se deve pela falta de permissão para fazer operações com a internet. Várias das operações que você for fazer em um aplicativo, será necessário que possua uma permissão, como acesso a rede, monitoramento de rede, armazenamento de dados, câmera, etc. 

Para adicionar a permissão para acesso a rede, abra o arquivo **AndroidManifest.xml** e dentro de `<manifest ...></manifest>` adicione:

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

Execute e veja o resultado no LOG.

![Resultado](http://2.bp.blogspot.com/-rBDVNv0XQ9Q/VfUF8p139rI/AAAAAAAAAcY/YeDay2J2WXE/s640/log.png)

### Lendo JSON

Agora que temos a resposta do servidor, vamos ler o arquivo JSON (consulte http://json.org/) e pegar os dados que queremos, a principio só vamos precisar dos nomes dos locais.

1. Adicione o método seguinte à `FetchPlaceTask`:

```java
private String [] getPlacesDatafromJson(String placesJsonStr) throws JSONException {

    // nomes das chaves do JSON
    final String ITEM_ID = "id";
    final String ITEM_NAME = "name";
    final String ITEM_CATEGORY = "category";
    final String ITEM_SUBCATEGORY = "subcategory";
    final String ITEM_LAT = "lat";
    final String ITEM_LGT = "lgt";

    JSONArray placesJson = new JSONArray(placesJsonStr);

    String[] resultStrs = new String[placesJson.length()];

    for (int i = 0; i < placesJson.length(); i++){

        JSONObject place = placesJson.getJSONObject(i);

        int id = place.getInt(ITEM_ID);
        String name = place.getString(ITEM_NAME);
        String category = place.getString(ITEM_CATEGORY);
        String subcategory = place.getString(ITEM_SUBCATEGORY);

        double lat = place.getDouble(ITEM_LAT);
        double lgt = place.getDouble(ITEM_LGT);

        // verifica se o objeto possui nome
        if(name.length() > 0)
            resultStrs[i] = name;
        else
            resultStrs[i] = subcategory;
    }

    return resultStrs;
}
```

2. Mude o ultimo parâmetro de `FetchPlaceTask` para `String []`
```java
class FetchPlaceTask extends AsyncTask<Void, Void, String[]>{
	....
}
```

3. Deixe `doInBackground()` assim:
```java
@Override
protected String[] doInBackground(Void... params) {

    double lat = -12.54667; //latitude
    double lgt = -38.71194; //longitude
    String placesJsonStr = request(lat, lgt);

    try {
        return getPlacesDatafromJson(placesJsonStr);
    } catch (JSONException e) {
        e.printStackTrace();
    }

    return null;
}
```
4. Adicone o método `onPostExecute()`:
```java
@Override
protected void onPostExecute(String[] result) {
    if(result != null){
        for(String placeName : result){
            Log.v("Place", placeName);
        }
    }
}
```

Agora execute e veja a lista de lugares no LOG

![LOG](http://4.bp.blogspot.com/-ThwJlPVqsW0/VfZVUOrPK2I/AAAAAAAAAcs/mvxncEyWsIg/s640/places.png)

### Adicionando os locais na Lista

1. Transforme a variável `adapter` em uma propriedade da classe `MainActivity`
2. Apague a lista de locais fictícios e no lugar adicione uma `ArrayList`
```java
adapter = new ArrayAdapter<>(this,
	android.R.layout.simple_list_item_1, new ArrayList());
```
3. Deixe `onPostExecute()` assim:
```java
@Override
protected void onPostExecute(String[] result) {
    if(result != null){
        adapter.clear(); //limpa a lista
        for(String placeName : result){
            adapter.add(placeName); //adiciona novo local
        }
    }
}
```

Pronto!

![Resultado](http://1.bp.blogspot.com/-qQwwoLp5nw8/VfZVcXNuSEI/AAAAAAAAAc0/IUt6nHNs8uU/s400/Screenshot_2015-09-14-02-01-42_framed.png)

### Passando parâmetros para FetchPlaceTask

1. Mude o primeiro parâmetro da classe `FetchPlaceTask` para `Double`
```java
class FetchPlaceTask extends AsyncTask<Double, Void, String[]>{
	...
}
```
2. Mude `doInBackground()` para 
```java
protected String[] doInBackground(Double... params) {
	...
}
```
3. Faça `lat` e `lgt` receberem `params`
 ```java
double lat = params[0]; //latitude
double lgt = params[1]; //longitude
```
4. Modifique a chamada da Task para:
```java
double lat = -12.54667; //latitude
double lgt = -38.71194; //longitude
new FetchPlaceTask().execute(lat, lgt);
```
