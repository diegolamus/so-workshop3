### Taller 3
**Universidad ICESI**  
**Curso:** Sistemas Operativos  
**Estudiante:** Diego Lamus.  
**Código:** A00320776  

### Objetivos
* Conocer y explicar la función de las llamadas al sistema en un sistema operativo

## Solucion
**1.** execve() : esta llamada al sistema permite ejecutar un programa. Para que esta llamada ejecute un programa, este debe ser un binario o un script que inicie con  "#! interpreter [arg]".   

      parametros:  
            1. filename: nombre del archivo que se va a ejecutar.  
            2. args: es un arreglo de strings. La primera posición por lo general recibe el nombre del archivo que se va a ejetcutar dentro del archivo que se esta ejecutando.  
            3. envp: es un arreglo de estring en la forma Key=value; se usa para inicializar las variables de entorno del programa.
            
![](/A00320776/imagenes/execve.png?)
            
**2.** getuid() : esta llamada al sistema retorna la ID real del usuario que esta ejecutando el proceso.

![](/A00320776/imagenes/getuid.png)

**3.** mmap(): crea un mapeo en el espacio de direcciones virtuales del proceso.

      parametros:  
            1. addr: la dirección d inicio para el nuevo mapeo, Si se deja en null el kernel elige donde poner el mapeo.
            2. length: especifica el largo del mapeo.
            3. prot: describe la seguridad de la memoria del mapeo. recibe los siguientes valores:  
                PROT_EXEC  Las páginas pueden ser ejecutadas.  
                PROT_READ  Las páginas pueden ser leidas.  
                PROT_WRITE Las páginas pueden ser escritas.  
                PROT_NONE  Las páginas no tienen acceso.
            4. flags: determina si las actualizaciones en el mapeo son visibles a otros procesos mapeando la misma region.
            5. fd: file descriptor.
            6. offset: starting point of the file.
    
![](/A00320776/imagenes/mmap.png)    
    
**4.** close(): cierra y libera un file descriptor, para que no pueda ser usado por por ningun archivo y pueda ser reusado. Cualquier tipo de lock que tuviera el archivo asociado al file descriptor se libera, asi como tambien se libera el archivo al cual hacia referencia.  

      parameros:  
            1. fd: file descriptor: numero que identifica un archivo o un proceso.  
 
![](/A00320776/imagenes/close.png) 
 
**5.** read(): intenta leer cierta cantidad de bytes de un archivo que permite busqueda identificado por un file descriptor.  
      
      parametros:
            1. fd: identifica el archivo que se va a leer.
            2. buf: identifica el punto de inicio del buffer al que se va a introducir la lectura.
            3. count: cuenta cuantos bytes se van a leer desde el offset del archivo.  
            
![](/A00320776/imagenes/read.png)


**6.** Al compilar el programa y hacerle strace se observan las siguientes llamadas al sistemas:

![](/A00320776/imagenes/curlsyscalls.png)  


En las llamadas al sistema en la lista del programa curl no se encuentran syscalls utilizadas para envier o recivir datos en la red. Algunas de las llamadas al sistema para enviar o recibir datos en la red son las siguientes:  


**a.**  send()  -- enviar  (solo cuando hay un socket  en estado de conexion)

      parametros: 
      1. sockfd: file descriptor del socket de envio.
      2. buf: mensaje
      3. len: largo del mensaje
      4. flags: banderas para indicar cosas  necesarias.
     
**b.**  sendto()  -- enviar

      parametros: 
      1. sockfd: file descriptor del socket de envio.
      2. buf: mensaje
      3. len: largo del mensaje
      4. flags: banderas para indicar cosas  necesarias.  
      5. dest_addr: direccion de destino (se ignora en modo conexion)  
      6. addrlen: largo de la direccion de destino (se ignora en modo conexion)  
       
**c.**  sendmsg()  -- enviar

      parametros: 
      1. sockfd: file descriptor del socket de envio.
      2. msg: mensaje najo la estructura de msghdr
      3. flags  
      
**c.**  srecv()  -- recibir

      parametros: 
      1. sockfd: file descriptor del socket del que se recibe.
      2. buf: buffer de destino del mensaje
      3. len: largo del mensaje
      4. flags
      
## Referencias

* http://man7.org/linux/man-pages/man2/syscalls.2.html  
* https://jvns.ca/blog/2014/09/18/you-can-be-a-kernel-hacker/
