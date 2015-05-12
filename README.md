## Disclaimer

Este guia visa ajudar os alunos de ES+SD a configurar a integração entre os projectos de ambas as cadeiras. Neste guia, são enunciados passos que assumem que não houve definições de novos módulos e respectivas dependências dos restantes módulos. Ou seja, caso o grupo tenha definido um novo módulo e colocado o mesmo como dependência de outro, então ao seguir o passo de alteração da pom que contém essa dependência, a mesma deve ser adicionada à pom fornecida neste guia. O mesmo se aplica a dependências de bibliotecas externas (jodatime, jdom2, etc...).

Caso existam módulos adicionais criados pelos alunos, a parent pom (ficheiro pom que está na root do projecto) no final do guia, deve ser também alterada no elemento `modules`, onde devem indicar a pasta desse módulo, para que este seja considerado na instalação. O maven irá calcular o grafo de dependências e compilar e instalar as dependências primeiro.

Caso tenham problemas com o guia, devem contactar o corpo docente via email, e/ou aparecer num horário de dúvidas para garantir que a migração foi feita sem problemas.


## Racional da Migração

O projecto de ES+SD é constituído por diversos módulos, em que alguns deles dependem uns dos outros (ex: bubbledocs-appserver depende dos clientes de SD-ID e SD-STORE). Este guia visa ajudar os alunos na configuração do projecto para que sua codebase esteja enquadrada com a ferramenta maven. Desta forma, os alunos podem executar:

### Testes Unitários
Testes unitários são aqueles que correm sempre localmente no módulo onde pertencem, ou seja, todas as entidades externas que seja necessário invocar deverão ser mocked. Estes testes devem ser colocados em qualquer package do directório `src/test/java` e terminarem o filename do teste com `Test.java`. Quando o comando `mvn clean test` é executado, o maven irá correr apenas esses testes, não sendo necessário nenhum serviço externo estar a correr, pois são apenas usados mocks dos mesmos.

### Testes de Integração
Outro tipos de testes são aqueles que necessitam de um servidor externo a correr. Esses testes chama-se testes de integração e devem ser também colocados em qualquer package dentro de `src/test/java`, terminando o filename do teste com `IT.java`. Quando for invocado o comando `mvn clean verify` a configuração fornecida neste guia vai correr esses testes, tendo os alunos que garantir que todos os serviços externos (ex: UDDI-server, SD-ID, SD-Store) estejam a correr.

## Passos:

* Substituir o ficheiro pom.xml na root do repositório por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/pom.xml).
* Substituir o ficheiro pom.xml na pasta bubbledocs-appserver por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/bubbledocs-appserver-pom.xml).
* Substituir o ficheiro pom.xml na pasta sd-id por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/sd-id-pom.xml).
* No ficheiro pom.xml substituido, definir nas properties, o fully classified name da classe main que corre o servidor sd-id na seguinte propriedade:
```
<main.exec.classname> </main.exec.classname>
```
* Substituir o ficheiro pom.xml na pasta sd-store por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/sd-store-pom.xml).
* No ficheiro pom.xml substituido, definir nas properties, o fully classified name da classe main que corre o servidor sd-store na seguinte propriedade:
```
<main.exec.classname> </main.exec.classname>
```
* Substituir o ficheiro pom.xml na pasta sd-id-cli por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/sd-id-cli-pom.xml).
* No ficheiro pom.xml substituído, definir nas properties, o fully classified name da classe main que corre o cliente sd-id-cli na seguinte propriedade:
```
<main.exec.classname></main.exec.classname>
```
* Substituir o ficheiro pom.xml na pasta sd-store-cli por este ficheiro [pom.xml](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/sd-store-cli-pom.xml).
* No ficheiro pom.xml substituido, definir nas properties, o fully classified name da classe main que correr o cliente sd-id-cli na seguinte propriedade:
```
<main.exec.classname></main.exec.classname>
```
* Descomprime o ficheiro [uddi-naming.zip](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets//uddi-naming.zip) para a root do projecto. Garante que na root do projecto existe uma pasta chamada uddi-naming e que lá dentro existe um ficheiro pom.xml e uma pasta src.
* Descomprime o ficheiro [juddi-server.zip](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/juddi-server.zip) para a root do projecto. Garante que na root do projecto existe uma pasta chamada juddi-server e que lá dentro existe um ficheiro pom.xml e uma pasta src.
* Descomprime o ficheiro [ws-handlers.zip](https://github.com/tecnico-softeng-distsys-2015/migration/raw/master/assets/ws-handlers.zip) para a root do projecto. Garante que na root do projecto existe uma pasta chamada ws-handlers e que lá dentro existe um ficheiro pom.xml e uma pasta src.
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
* Instala os projectos localmente correndo o seguinte comando na root do repositório:
```
mvn clean install -Dmaven.test.skip=true
```


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
