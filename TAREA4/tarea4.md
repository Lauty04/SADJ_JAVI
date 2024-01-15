# UD3 – Instalación y configuración de cortafuegos y proxies

## Tarea 4 – Conifguración proxy Squid

Vamos a instalar Squid en una máquina virtual Xubuntu

    lautaro@IAW:~$ sudo apt install squid

## Vamos a realizar unos ejemplos:

### 1- Bloquear accesos a páginas con ciertas palabras:
Editamos el archivo /etc/squid/squid.conf y añadimos :

    1 # NUEVAS REGLAS ACL BLOQUEO
    2 acl bloqueo url_regex as twitter
    3 http_access deny bloqueo

### 2- Permitir la navegación sólo a ciertas Ips de nuestra red:

    acl ips_permitidas src "/etc/squid/conf.d/lista_ips"
    http_access allow ips_permitidas

### 3- Denegar el acceso a sitios de cierto contenido:

    acl denegados url_regex /etc/squid/conf.d/lista_denegados
    http_access allow !denegados

    lautaro@IAW:/etc/squid/conf.d$ cat lista_denegados 
    youtube
    wikipedia

### 4- Permitir o denegar el acceso a ciertos dominios:

    acl permitidos dstdomain “/etc/squid/dominios”
    https_access allow permitidos

Habéis llegado a la conclusión de configurar un proxy con las siguientes características:

• Debe usar el puerto 8080

    http_port 8080

• Utilizará 1GB de memoria para caché y se almacenará en /var/cache/proxy

    cache_dir ufs /var/cache/proxy 1000 16 256


◦ Dirección debe poder entrar a cualquier página, así como el Departamento de
Informática y los servidores. 

    acl direccion src 192.168.101.1-192.168.101.20
    http_access allow direccion

    acl informática  src 192.168.101.31-192.168.101.50
    http_access allow informática

    acl servidores src 192.168.103.0/24
    http_access allow servidores

◦ El resto de direcciones tendrán prohibido el acceso a páginas web con el
siguiente contenido:
▪ Deportes
▪ Apuestas
▪ Juegos
▪ Viajes

    acl denegados url_regex /etc/squid/conf.d/lista_denegados
    http_access deny denegados

Habrá una excepción en caso de que los dominios de dichas webs sean .edu o .gov

    acl permitidos dstdomain “/etc/squid/dominios”
    https_access allow permitidos


FICHERO DE CONFIGURACION PERSONAL:

    acl bloqueo url_regex as twitter
    http_access deny bloqueo

    acl ips_permitidas src "/etc/squid/conf.d/lista_ips"
    http_access allow ips_permitidas

    acl dominios_permitidos dstdomain .edu .gov
    https_access allow dominios_permitidos

    acl permitidos dstdomain “/etc/squid/dominios”
    https_access allow permitidos

    acl denegados url_regex /etc/squid/conf.d/lista_denegados
    http_access deny denegados

    cache_dir ufs /var/cache/proxy 1000 16 256

    acl direccion src 192.168.101.1-192.168.101.20
    http_access allow direccion

    acl informática  src 192.168.101.31-192.168.101.50
    http_access allow informática

    acl servidores src 192.168.103.0/24
    http_access allow servidores

    cache_dir ufs /var/cache/proxy 1000 16 256

    http_access allow all


Fichero de acceso prohibido:

    lautaro@IAW:/etc/squid/conf.d$ cat /etc/squid/conf.d/lista_denegados
    youtube
    \.deportes\.
    \.apuestass\.
    \.juegos\.
    \.viajess\.  












