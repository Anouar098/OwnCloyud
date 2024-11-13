# Instal·lació d'Owncloud 

Aquesta es l'instalació i configuració d'owncloud.

## Instalació i actualització

Lo primer es instalar aquest .zip: https://download.owncloud.com/server/stable/owncloud-complete-20240724.zip

Com la versió que hi ha es 7.4 de PHP, l'hem d'actualitzar a Ubuntu 24.04.

# Actualització

Després d'instal·lar-ho haureu d'actualitzar-ho heu de posar les següents comandes a la terminal:
```bash
sudo apt install software-properties-common -y
```

Instal·la les eines necessàries per treballar amb els arxius de paquets personals (PPA).
```bash
LC_ALL=C.UTF-8 sudo add-apt-repository ppa:ondrej/php -y
```

Actualitza ara els repositoris:
```bash
sudo apt update
```

Instal·la les llibreries de PHP de la versió 7.4
```bash
sudo apt install php7.4 -y
```
```bash
sudo apt install -y php libapache2-mod-php7.4
```

```bash
sudo apt install -y php7.4-fpm php7.4-common php7.4-mbstring php7.4-xmlrpc php7.4-soap php7.4-gd php7.4-xml php7.4-intl php7.4-mysql php7.4-cli php7.4-ldap php7.4-zip php7.4-curl
```

Seleccioneu la versió de PHP que voleu:
```bash
sudo update-alternatives --config php
```

Activa els mòduls d'apache2 necessaris:
```bash
sudo a2enmod proxy_fcgi setenvif
```

```bash
sudo a2enconf php7.4-fpm
```

Reinicieu l'apache2:
```bash
sudo service apache2 restart
```
# Instalació

Ara passarem a la part d'instal·lació, si no et funciona algunes comandes del final, pot ser que sigui pel nom "owncloud" que no a tothom el surt el mateix, llavors haureu de canviar-ho pel nom que tingui el vostre .zip o la carpeta descompresa.

Per instal·lar-ho haureu de seguir els següents passos:
1. Actualització de la màquina.
```console
sudo apt update
```
```console
sudo apt upgrade
```

2. Instal·lació del servidor web **apache2**.
```console
sudo apt install -y apache2
```

3. Instal·lació del servidor de bases de dades **mysql-server**.
```console
sudo apt install -y mysql-server
```

4. Instal·lació d'algunes llibreries de **php**.
```console
sudo apt install -y php libapache2-mod-php
```
```console
sudo apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```

5. Reiniciem el servidor apache2
```console
sudo systemctl restart apache2
```

## Configuració de MySQL
### Accedim a la consola de MySQL
Des d'un terminal on siguem **root** hem d'executar la següent comanda:
```console
sudo mysql
```

T'haurá de sortir així:

<img src="/Terminal1.png" width="834" height="395" alt="Foto de la terminal MySQL"/>

### Creació de la base de dades:
Un cop dins la consola de MySQL executem les comandes per a crear la base de dades. En aquest cas estem creant una base de dades amb el nom **bbdd**.

```console
CREATE DATABASE bbdd;
```

### Creació d'un usuari
Tingueu en compte que s'haurà d'identificar la IP des de la qual s'accedirà a la base de dades, en aquest cas, **localhost**.

```console
CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```

### Donem privilegis a l'usuari:
```console
GRANT ALL ON bbdd.* to 'usuario'@'localhost';
```

### Sortim de la base de dades
```console
exit
```

Amb aquesta comanda tormarás al terminal normal

<img src="/Terminal2.png" width="355" height="99" alt="Foto de la terminal MySQL"/>

### Probem la connexió a la base de dades
Des d'un terminal amb un usuari sense privilegis hem de ser capaços de connectar introduïnt la nostra contrassenya.

```console
mysql -u usuario -p
```

## Descarreguem els fitxers de l'aplicació web
Anem al directori **/var/www/html** i descomprimim allà els fitxers de l'aplicació web.

```console
sudo cp ~/Descargas/owncloud.zip /var/www/html
```
Aneu al directori **/var/www/html**
```console
cd /var/www/html
```
Descomprimiu el fitxer que heu baixat
```console
sudo unzip owncloud.zip
```

Ara has fet unzip al .zip


Copieu els fitxers a la carpeta **/var/www/html**.
```console
sudo cp -R owncloud/. /var/www/html
```
Eliminem la carpeta creada quan hem fet l'**unzip**
```console
sudo rm -rf owncloud/
```

## Eliminem el fitxer **index.html** de l'**apache2**
```console
sudo rm -rf /var/www/html/index.html
```

## Aplicació de permisos a les nostres aplicacions web
Un cop descomprimits els fitxers de l'aplicació web al directori **/var/www/html**, apliquem els següents permisos al directori **/var/www/html**.

```console
cd /var/www/html
```
```console
sudo chmod -R 775 .
```
```console
sudo chown -R usuario:www-data .
```

Quan entres per primera vegada al terminal i intentes a posar una comanda, moltes vegades et posa això:

<img src="/Terminal3.png" width="424" height="59" alt="Foto de terminal contraseña"/>

Hauràs de posar **usuari** o **password**, si no et surt res a l'hora d'escriure la contrasenya no et preocupis, ja que si poses la contrasenya correcta i pitges enter entraràs igualment.

# Com entrar

Després d'acabar de fer-ho tot haureu d'entrar al link http://localhost per comprobar que ho has fet tot bé, i t'hauría de sortir així:

<img src="/Registrarse.jpg" width="425" height="700" alt="Foto de donde hay que poner toda la información"/>

L'informació que heu de posar per registrarse és la següent:

* **usuari:** usuario
* **contrasenya:** password
* **base de dades:** bbdd
* **domini:** localhost

## Inici de sessió i configuració

Ara comença la part d'iniciar sessió i conficurar tot dins de l'[Owncloud](https://github.com/josepb80/Owncloud/blob/main/Configuraci%C3%B3.md).
