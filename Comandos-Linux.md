# Comandos de Linux



*  #### dsquery
(busqueda/consulta del AD)
```
dsquery server domainroot (lista todos los controladores de dominio)

dsquery computer OU=Sales,DC=Contoso,DC=Com (busca todos los equipo de esa OU)

dsquery computer domainroot -name ServFichero* (busca en el dominio actual todas las maquinas cuyo nombre comience con "ServFichero")

dsquery user domainroot -name *smith -inactive 3 (muestra a todos los usuarios cuyo nombre termina en "smith" y que lleven más de 3 semanas de inactividad)

dsquery user ... -disabled (que las cuenta este desactivada)
dsquery user ... --stalepwd 30 (que no haya cambiado la password desde hace al menos 30 dias)
```





*  #### pwd
(Lista directorio actual)

*  #### whoami
(Lista usuario actual)

*  #### exec <comando>
(ejecuta el comando y te saca de SHELL "como si hicieras exit")

*  #### time <comando>
(Lista el tiempo (real, de usuario, de sistema) que ha tardado en ejecutarse <comando>)

*  #### history
(Lista los últimos comandos tecleados)
```
  ~/.bash_history
```

*  #### touch
(Crea un fichero vacío (con los permisos de la máscara actual umask)
```
permiso = permiso_base AND NOT (umask) *
  
  *  permiso base fichero -- 666
     permiso base direct -- 777
```

*  #### ls
(Listar contenido de un directorio)

```
-a (mostrar los ocultos)
-l (listado largo)
-F (añade marca al final)
-R (recursivo de todos los subdirectorios)
```

*  #### cp
(Copiar)
```
-u (copia, si el origen está mas actualizado que el destino)
-r (copia recursiva)
```

*  #### mv
(Mueve y renombra)
```
-i (pregunta antes de sobreescribir)
```

*  #### rm
(Elimina)
```

-i (pregunta)
-r (recursiva)
```

*  #### touch
(Crea ficheros vación)
```

-a (solo modifica fecha de acceso)
-m (solo modifica fecha de modificación)
-c (no crea fichero si este no existe)
```  
  
*  #### tar
(Empaquetar/Desempaquetar)
```

tar cvfz /media/copia.tgz ~/my-work
tar xvfz /media/copia.tgz
    
    c/x - crear un archivo/extraer archivo
    v - ver
    f - empaquetar contenido de archivos
    z - gzip
``` 

*  #### dd
(copia entre dispositivos)
```
dd if=/dar/zero of=empty.img bs=1024 count=720
dd if=dev/cdrom of=/media/imagenCD.iso
dd if=/dev/hda of=/media/mbr bs=512 count=1
```

*  #### mkdir
(Crea subdirectorios)
```
-p (crea todos los subdirectorios necesarios)
```

*  #### rmdir
(Eliminar un directorio)
```
-p (el arbol entero)
```

*  #### chown
(Permite cambiar el propietario de un archivo)
```
-R (recursivo)
  .chown user:group file (solo puede root!!)
```

*  #### chgrp
(Cambia el grupo owner)
  
*  #### chmod
(Cambiar los permisos de acceso de un fichero o directorio)

*  #### find
(Buscar ficheros en el sistema)
 ```
-type d
-name cadena
-perm 777
-exec
-user uid
-atime +-/n
-size +50mb
  
  
Comandos opciones {} \ ;
```

*  #### ln
(Enlaces)
```
  
-d (a directorios)
-s (simbolico)(por defecto si no es HARD*)

*HARD-link (todos los enlaces son los mismos inodo. Comparten TODO) Son "copias" del fichero" (si se borra el original, no pasa nada)
```

*  #### split
(Genera ficheros de trozos)
```

x bytes
x filas
```

*  #### tr
(Pasa de mayusculas a minusculas)
```

ABC...abc... < fichero.txt
```

*  #### uniq
(Elimina lineas duplicadas)
                          
*  #### nl
(Como el comando cat pero imprime los num de lineas)
```

-b a (numera tambien las lineas vacias)
```

*  #### head/tail
(Ver las primeras o ultimas filas N lineas)
```

tail -zoo f fichero.log (mantiene el fichero abierto u nos muestra las 1er lineas nuevas que se van cambiando del fichero)
```
                          
*  #### more/less
(Informacion paginada)


*  #### cut
(Corta en vertical)
```

-b (por bytes)
-f (por campos)
-c (por caracteres)
```

*  #### wc
(Word Count)
```

-l (cuenta lineas)
-w (cuenta palabras)
-m (cuenta caracteres)
-c (por caracter)
```

*  #### grep
(Busquedas)                     
*  #### egrep
(Soporta expr regulares)                        
*  #### fgrep
(NO soporta expr regulares)
```

Expresiones regulares
+ (1 o mas)
* (0 o mas)
? (0 o 1)
. (cualquier caracter, pero solo 1)
\ (escapar simbolos con significado especial)
1 (inicio linea)
$ (fin linea)
[a-z] (rango)
[abcd] (1 solo caracter)
| (opcionalidad)
[1, ...] (no coincidencia)
() (agrupacion)
{N} (num de ocurrencias)
{M} (1 o mas ocurrencias)
```                         








