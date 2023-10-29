# Realizar la instalación de Maven en el SO
# Ruben Abreu Gonzalez

- [Instalar Apache Maven con apt](#instalar-apache-maven-con-apt)
- [Instalar una versión concreta de Apache Maven](#instalar-una-versión-concreta-de-apache-maven)
- [Verificar la instalación](#verificar-la-instalación)

## Instalar Apache Maven con apt
- Instalar Maven en Ubuntu usando apt es un proceso simple y directo.
- Actualice el índice del paquete e instale Maven ingresando los siguientes comandos:
- sudo apt update
<details>
<summary>salida</summary>

```code
[sudo] contraseña para rabgonzalez:      	 
Obj:1 http://archive.ubuntu.com/ubuntu jammy InRelease
Obj:2 http://archive.ubuntu.com/ubuntu jammy-updates InRelease            	 
Obj:3 http://archive.ubuntu.com/ubuntu jammy-backports InRelease          	 
Ign:4 http://packages.linuxmint.com victoria InRelease                    	 
Obj:5 http://packages.linuxmint.com victoria Release  
Obj:7 http://security.ubuntu.com/ubuntu jammy-security InRelease
Leyendo lista de paquetes... Hecho
Creando árbol de dependencias... Hecho
Leyendo la información de estado... Hecho
Se pueden actualizar 218 paquetes. Ejecute «apt list --upgradable» para verlos.
```
</details>

- sudo apt install maven
<details>
<summary>salida</summary>

```code
Leyendo lista de paquetes... Hecho
Creando árbol de dependencias... Hecho
Leyendo la información de estado... Hecho
maven ya está en su versión más reciente (3.6.3-5).
0 actualizados, 0 nuevos se instalarán, 0 para eliminar y 218 no actualizados.
```
</details>


- Para verificar la instalación, ejecute mvn -version:
- mvn -version
<details>
<summary>salida</summary>

```code
Apache Maven 3.6.3
Maven home: /usr/share/maven
Java version: 11.0.20.1, vendor: Ubuntu, runtime: /usr/lib/jvm/java-11-openjdk-amd64
Default locale: es_ES, platform encoding: UTF-8
OS name: "linux", version: "5.15.0-76-generic", arch: "amd64", family: "unix"
```
</details>

## Instalar una versión concreta de Apache Maven
- En el momento de escribir este artículo, es la última versión de Apache Maven 3.8.6. Antes de continuar con el siguiente paso, visite la página de descarga de Maven para ver si hay una versión más nueva disponible.
- Descargue Apache Maven en el directorio /tmp:
- wget https://www.apache.org/dist/maven/maven-3/3.9.5/binaries/apache-maven-3.9.5-bin.tar.gz -P /tmp
<details>
<summary>salida</summary>

```code
--2023-10-29 15:40:15--  https://www.apache.org/dist/maven/maven-3/3.9.5/binaries/apache-maven-3.9.5-bin.tar.gz
Resolviendo www.apache.org (www.apache.org)... 151.101.2.132
Conectando con www.apache.org (www.apache.org)[151.101.2.132]:443... conectado.
Petición HTTP enviada, esperando respuesta... 302 Found
Ubicación: https://downloads.apache.org/maven/maven-3/3.9.5/binaries/apache-maven-3.9.5-bin.tar.gz [siguiente]
--2023-10-29 15:40:15--  https://downloads.apache.org/maven/maven-3/3.9.5/binaries/apache-maven-3.9.5-bin.tar.gz
Resolviendo downloads.apache.org (downloads.apache.org)... 88.99.95.219, 135.181.214.104
Conectando con downloads.apache.org (downloads.apache.org)[88.99.95.219]:443... conectado.
Petición HTTP enviada, esperando respuesta... 200 OK
Longitud: 9359994 (8,9M) [application/x-gzip]
Guardando como: ‘/tmp/apache-maven-3.9.5-bin.tar.gz’

apache-maven-3.9.5- 100%[===================>]   8,93M  7,61MB/s	en 1,2s    

2023-10-29 15:40:17 (7,61 MB/s) - ‘/tmp/apache-maven-3.9.5-bin.tar.gz’ guardado [9359994/9359994]
```
</details>

> Nota: Al visitar la página de descargas de Maven había una versión más moderna, por lo que descargue la 3.9.5 en lugar de la 3.8.6

- Una vez que se complete la descarga, extraiga el archivo en el directorio /opt
sudo tar xf /tmp/apache-maven-*.tar.gz -C /opt
<details>
<summary>salida</summary>

```
```
</details>

- Para tener más control sobre las versiones y actualizaciones de Maven, que a crear un maven enlace simbólico que apunte al directorio de instalación de Maven:
- sudo ln -s /opt/apache-maven-3.9.5 /opt/maven
<details>
<summary>salida</summary>

```
```
</details>

- Cuando se lanza una nueva versión, puede actualizar su instalación de Maven desempaquetando la última versión y cambiando el enlace simbólico para señalarla.
- Establecer variables de entorno A continuación, necesitaremos establecer las variables de entorno. - Para hacer esto, abra su editor de texto y cree un nuevo archivo llamado mavenenv.sh en el directorio /etc/profile.d/
- sudo nano /etc/profile.d/maven.sh
- Pega el siguiente código:
export M2_HOME=/opt/maven
export MAVEN_HOME=/opt/maven
export PATH=${M2_HOME}/bin:${PATH}
<details>
<summary>salida</summary>

```
```
</details>

- Guarde y cierre el archivo. Este script se utilizará al iniciar el shell.
- Haga que el script sea ejecutable con chmod:
- sudo chmod +x /etc/profile.d/maven.sh
<details>
<summary>salida</summary>

```
```
</details>

- Finalmente, cargue las variables de entorno usando el comando de source
- source /etc/profile.d/maven.sh
<details>
<summary>salida</summary>

```
```
</details>

## Verificar la instalación
- Para verificar que Maven está instalado, use el mvn -version que imprimirá la versión de Maven:
- mvn -version
<details>
<summary>salida</summary>

```code
    Apache Maven 3.6.3
    Maven home: /usr/share/maven
    Java version: 11.0.20.1, vendor: Ubuntu, runtime: /usr/lib/jvm/java-11-openjdk-amd64
    Default locale: es_ES, platform encoding: UTF-8
    OS name: "linux", version: "5.15.0-76-generic", arch: "amd64", family: "unix"
```
</details>

> Nota: Al final me debería salir “Apache Maven 3.9.5” pero habré cometido algún fallo en los apartados anteriores por lo que no me aparece la última versión.
