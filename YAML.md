# YAML Syntax 

### WICHTIG: Alles was Code ist, ist schon mit Leerzeichen eingerückt und kann so 1 zu 1 in das YAML-File kopiert werden. Zum Schluss dieser Dokumentation folgt ein kompletter YAML-Code. Dieser ist ebenfalls richtig eingerückt. (von Herr Lux)

### version: 
```
version: "3.8" 
```
Mit "version:" wird in einem YAML-File die Docker Version angegeben. Die aktuellste Version ist 3.8. Den Wert, also in dem Fall 3.8 muss in "" und somit als String geschrieben werden. Die Version muss jedoch nicht unbedingt angegeben werden.


### service:
```
service:
 wordpress:
```
Mit "service:" kann man einen Dienst definieren. Zum Beispiel "Worpress". Nach dem Service folgen dann die Konfigurationen eines Dienstes. Man kann zum Beispiel ein YAML File erstellen und darin dann 2 verschiedene Services definieren (z.B Wordpress, Mariadb). Zu jedem Service folgen dann alle möglichen Angaben.


### image:
```
  image: wordpress
```
Mit "image:" wird das Standard Image angegeben. Hier ist es das Image "Wordpress", welches auf Dockerhub zu finden ist. Mit den nachfolgenden Schlüsseln/Angaben wird dann der Container definiert. Als Beispiel kann hier auch "mariadb" angegeben werden, wenn ein MariaDB Container erstellt werden soll.


### links:
```
  links:
   - mariadb:mysql
 ```
Mit "links:" können zwei Container miteinander verlinkt werden. Wenn man dieses Kommando benutzt, dann wird der Wert also das was miteinander verlinkt wird, unterhalb und einmal eingerückt mit einem " - " (also einer Auflistung) definiert.


### environment:
```
  environment:
   - WORDPRESS_DB_PASSWORD= xxx
   - WORDPRESS_DB_USER= xxx
```
Das Komanndo/Schlüssel "environment" ersetzt -e im "docker run" Command. Es wird benutzt um den Dienst also z.B Wordpress zu konfigurieren. Also hier legt man bei der Wordpress-Datenbank den User und sein Passwort fest.
Alle Angaben müssen darunter und einmal eingerückt mit einem " - " (Auflistung) angegeben werden.


### ports:
```
  ports:
   - "127.0.0.1:80:80" (IP Muss diejenige des PC sein)
```
oder 
```
  ports:
   - "8000:80"
```
Mit den Kommando "ports:" legt man fest welcher Port für die Anwengung/Service/Container genutzt wird. Die beiden oben gezeigten Optionen kann man verwenden.
Wenn man möchte, kann man auch mehrere Ports angeben, in dem man einfach darunter nochmals mit " - " einen neuen Port definiert.

### volumes:
```
  volumes:
   - ./Ordner/Auf/VM:/ordner/auf/container
 ```
Mit "volumes" kann man zwei Dateipfade miteinander verknüpfen. Es ersetzt das -v in einem "docker run" Command. Nice To know: ./ gibt das aktuelle Verzeichnis an, ohne dass man dne kompletten Pfad beschreiben muss. Alles was nach dem " / " folgt, ist das Zielverzeichnis/Datei

## Vollständiger YAML-Code:

```
services:
 wordpress:
  image: wordpress
  links:
   - mariadb:mysql
  environment:
   - WORDPRESS_DB_PASSWORD=geheim
   - WORDPRESS_DB_USER=root
  ports:
   - "127.0.0.1:80:80"
  volumes:
   - ./html:/var/www/html

 mariadb:
  image: mariadb
  environment:
   - MYSQL_ROOT_PASSWORD=geheim
   - MYSQL_DATABASE=wordpress
  volumes:
   - ./database:/var/lib/mysql
```
