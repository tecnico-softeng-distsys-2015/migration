## Passos:

* Substituir o ficheiro pom.xml na root do repositório por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/pom.xml).
* Substituir o ficheiro pom.xml na pasta bubbledocs-appserver por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/bubbledocs-appserver-pom.xml).
* Substituir o ficheiro pom.xml na pasta sd-id por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/sd-id-pom.xml).
* No ficheiro pom.xml substituido, definir nas properties, o fully classified name da classe main que correr o servidor sd-id na seguinte propriedade:
	```
	<main.exec.classname></main.exec.classname>
	```
* Substituir o ficheiro pom.xml na pasta sd-store por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/sd-store-pom.xml).
* No ficheiro pom.xml substituido, definir nas properties, o fully classified name da classe main que correr o servidor sd-store na seguinte propriedade:
	```
	<main.exec.classname></main.exec.classname>
	```
* Substituir o ficheiro pom.xml na pasta sd-id-cli por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/sd-id-cli-pom.xml).
* No ficheiro pom.xml substituido, definir nas properties, o fully classified name da classe main que correr o cliente sd-id-cli na seguinte propriedade:
	```
	<main.exec.classname></main.exec.classname>
	```
* Substituir o ficheiro pom.xml na pasta sd-store-cli por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/sd-store-cli-pom.xml).
* No ficheiro pom.xml substituido, definir nas properties, o fully classified name da classe main que correr o cliente sd-id-cli na seguinte propriedade:
	```
	<main.exec.classname></main.exec.classname>
	```
* Descomprime o ficheiro [uddi-naming.zip](http://disciplinas.tecnico.ulisboa.pt/leic-sod/2014-2015/labs/06-ws2/uddi-naming.zip) para a root do projecto. Garante que na root do projecto existe uma pasta chamada uddi-naming e que lá dentro existe um ficheiro pom.xml e uma pasta src.
* Descomprime o ficheiro [juddi-server.zip](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/juddi-server.zip) para a root do projecto. Garante que na root do projecto existe uma pasta chamada juddi-server e que lá dentro existe um ficheiro pom.xml e uma pasta src.
* Descomprime o ficheiro [ws-handlers.zip](http://disciplinas.tecnico.ulisboa.pt/leic-sod/2014-2015/labs/10-ws4/ws-handlers.zip) para a root do projecto. Garante que na root do projecto existe uma pasta chamada ws-handlers e que lá dentro existe um ficheiro pom.xml e uma pasta src.
* Garante que na root do projecto tens as seguintes pastas e ficheiros:
	* /bubbledocs-appserver
	* /sd-id
	* /sd-id-cli
	* /sd-store
	* /sd-store-cli
	* /uddi-naming
	* /ws-handlers
	* /juddi-server
	* /info
	* pom.xml
	* README.md

#### Para correr o servidor UDDI

1. Abrir uma nova consola.
2. Ir para a pasta do juddi-server
3. Correr o seguinte comando:
```
mvn clean tomcat7:run
```

Após invocar o comando Maven, o servidor UDDI irá arrancar e ficar bloqueado.
Para terminar o servidor UDDI, deve usar a combinação de teclas: `CTRL+C`

#### Para correr o servidor SD-X (em que X é ID ou Store)

1. Abrir uma nova consola.
2. Ir para a pasta sd-x (em que x é id ou store)
3. Correr o seguinte comando: mvn clean compile exec:java

Após invocar o comando Maven, o servidor SD-X irá arrancar e ficar bloqueado.
Para terminar o servidor SD-X, deve carregar em qualquer tecla.

#### Para correr o bubble-docs

1. Abrir uma nova consola.
2. Entrar na pasta bubbledocs-appserver.
3. Correr testes de unidade:
	* Correr apenas os testes de unidade locais:
	```
	mvn clean test
	```
	* Correr apenas uma classe de testes de unidade local:
	```
	mvn -Dtest=NomeDaClasseTest test
	```
	* Correr apenas um método de uma classe de testes de unidade local:
	```
	mvn -Dtest=NomeDaClasseTest#nomeDoMetodoTest test
	```
4. Correr testes de sistema:
	* Correr apenas os testes de sistema remoto:
	```
	mvn clean verify -DskipUnitTests
	```
	* Correr apenas uma classe de testes de sistema remoto:
	```
	mvn clean -Dit.test=NomeDaClasseIT verify -DskipUnitTests
	```
	* Correr apenas um método de uma classe de testes de sistema remoto:
	```
	mvn clean -Dit.test=NomeDaClasseIT#nomeDoMetodo verify -DskipUnitTests
	```
5. Correr todos os testes:
	* Correr tudo (testes de unidade e de sistema):
	```
	mvn clean verify
	```
