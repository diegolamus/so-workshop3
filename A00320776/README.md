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
            
**2.** getuid() : esta llamada al sistema retorna la ID real del usuario que esta ejecutando el proceso.

**3.** nmap(): crea un mapeo en el espacio de direcciones virtuales del proceso.

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
    
**4.** close(): cierra y libera un file descriptor, para que no pueda ser usado por por ningun archivo y pueda ser reusado. Cualquier tipo de lock que tuviera el archivo asociado al file descriptor se libera, asi como tambien se libera el archivo al cual hacia referencia.  

      parameros:  
            1. fd: file descriptor: numero que identifica un archivo o un proceso.  
            
**5.** read(): intenta leer cierta cantidad de bytes de un archivo que permite busqueda identificado por un file descriptor.  
      
      parametros:
            1. fd: identifica el archivo que se va a leer.
            2. buf: identifica el punto de inicio del buffer al que se va a introducir la lectura.
            3. count: cuenta cuantos bytes se van a leer desde el offset del archivo.  
            


### Actividades

1. Empleando el aplicativo **strace** obtenga 5 llamadas al sistema para uno o varios comandos de linux. Explique por qué los comandos seleccionados emplean las llamadas al sistema encontradas, para ello debe emplear los manuales de Linux en Internet o del sistema operativo (comando **man**). Debe incluir la explicación de los parámetros que reciben las llamadas al sistema encontradas. Consigne capturas de pantalla donde muestre las llamadas al sistema obtenidas (sugerencia: emplear -etrace para filtrar los resultados)

2. Realice la compilación del código fuente adjunto y su ejecución empleando el aplicativo **strace**. Identifique las llamadas al sistema encargadas de enviar y recibir datos a través de la red. A partir de los manuales de Linux en Internet o del sistema operativo explique las llamadas al sistema encontradas y sus parámetros.

**Nota:** Cuando compile programas tenga en cuenta que estos pueden necesitar la instalación de librerías para su compilación y ejecución.

**Debian**
```
# apt-get install libcurl4-openssl-dev
$ gcc -o curl curl.c -lcurl
```
**CentOS**
```
# yum install libcurl-devel
$ gcc -o curl curl.c -lcurl
```

### Nota

El informe debe ser entregado en formato README.md y debe ser subido a un repositorio de github. El repositorio de github debe ser un fork de https://github.com/ICESI-Training/so-workshop3 y para la entrega deberá hacer un Pull Request (PR) respetando la estructura definida. El código fuente y la url de github deben incluirse en el informe.  

## Referencias

* http://man7.org/linux/man-pages/man2/syscalls.2.html  
* https://jvns.ca/blog/2014/09/18/you-can-be-a-kernel-hacker/
