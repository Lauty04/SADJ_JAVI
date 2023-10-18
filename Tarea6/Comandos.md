### Para generar el par de claves se utiliza :

    gpg --gen-key

### listar las claves con el comando :

    gpg --list-keys
    
### Exportar clave publica

    gpg -a --export -o fichero.pub 'usuario'

Ese fichero ya lo podremos enviar a la persona con quien queramos comunicarnos.

### Importamos la clave publica de Javi

    gpg --import nombre_fichero
    gpg --import Descargas/ClavePublicaJD.pub 

### Para encriptar fichero con clave publica de otra persona

    gpg -v -a -o ruta/mensaje.cifrado --encrypt --recipient usuario fichero 
    gpg -v -a -o punto5.cifrado --encrypt --recipient 'Javi Daroqui' punto5.txt

### Par descifrar con nuestra clave privada si nos los encriptan con nuestra clave publica

    gpg --decrypt mensaje.cifrado
    gpg --decrypt MensajeLautaro.txt.asc

### Crear huella

    gpg -a --detach-sign nombre_fichero

### Vrificar firma de la otra persona 

       gpg --verify nombre_fichero.ascç

### enviar tanto el mensaje como la firma en el mismo fichero y cifrado, podemos utilizar el comando siguiente:

    gpg -a --sign nombre_fichero
Esta vez tendremos un fichero llamado nombre_fichero.asc que contendrá tanto el contenido del fichero original como la firma y, además, estará cifrado con nuestra clave privada

### Para comrobar que un mensaje no a sido modificado tras firmarlo

    gpg --verify ficherooriginal ficheroacomprobar





