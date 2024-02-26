# Pentesting con Metasploitable 2

## Instala un máquina virtual Metasploitable 2 y, mediante Kali Linux, intenta aprovechar las vulnerabilidades de los servicios FTP e IRC. Realiza un breve documento explicando los pasos y mostrando capturas que demuestren cómo has conseguido vulnerar los servicios.

# FTP---

Necesitams 2 makinas virtuales, una de kali y otra de metaspoitable las que debemos tener en la misma red.

![](metas.imgs/Captura%20de%20pantalla%202024-02-21%20111023.png)

Hacemos un scaneo con nmap -sV lo cual nos muestra los servicios y sus versiones de la ip correspondiente.

![](metas.imgs/Captura%20de%20pantalla%202024-02-21%20111632.png)

Ahora vamos a utilizar Metasploit Framework para buscar y explotar la vulnerabilidad que pueda tener este servicio.

![](metas.imgs/03.png)

Utilizamos el comando search vsftpd para ver las vulnerabilidades que tenemos dispnibles en ese servicio:

![](metas.imgs/04.png)


Como vemos en el nmap teniamos abierto el servicio ftp en el puerto 21 y encontramos la vulnerabilidad tambien.
Usaremos el comando exploit:

![](metas.imgs/05.png)

Configuramos la ip a la que atacaremos con 'set RHOSTS' y vemos que quedo bien:

![](metas.imgs/06.png)

Ahora ejecutamos el exploit y vemos que se crea una shell conectada a la otra maquina con permisos de root:

![](metas.imgs/07.png)


Viendo que ejecutando whoami para ver quien somos nos dice que somos root y por ende tenemos control sobre todo.

Tambien podemos ver los demas usuarios por lo que ya tambien podemos intentar hackear a cada usuario.

![](metas.imgs/08.png)



# IRC---

Volvemos a utilizar la maquina de kali para "hackear" el metasploitable fijandonos que esten en una misma red.

Comprovamos con un nmap -Sv los servicios y puerto abiertos 

![](metas.imgs/09.png)

Y ejecutamos la consola de metasploitable usando el modulo de urc:

![](metas.imgs/10.png)

Debemos configurar el host remoto y el host local:

    msf6 exploit(unix/irc/unreal_ircd_3281_backdoor) > set RHOSTS 192.168.55.19
    RHOSTS => 192.168.55.19


    msf6 exploit(unix/irc/unreal_ircd_3281_backdoor) > set lhost eth0
    lhost => eth0



Configuramos el payload:

![](metas.imgs/11.png)

Executamos el exploit y vemos que todo funciono bien y estamos dentro del sistema como root:

![](metas.imgs/12.png)


