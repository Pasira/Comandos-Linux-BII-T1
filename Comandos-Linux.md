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





* #### pwd
(Lista directorio actual)

* #### whoami
(Lista usuario actual)

* #### exec <comando>
(ejecuta el comando y te saca de SHELL "como si hicieras exit")

*  #### time <comando>
(Lista el tiempo (real, de usuario, de sistema) que ha tardado en ejecutarse <comando>)

* #### history
(Lista los últimos comandos tecleados)
```
  ~/.bash_history
```

* #### touch
(Crea un fichero vacío (con los permisos de la máscara actual umask)
```
permiso = permiso_base AND NOT (umask) *
  
  *  permiso base fichero -- 666
     permiso base direct -- 777
```

* #### ls
(Listar contenido de un directorio)

```
-a (mostrar los ocultos)
-l (listado largo)
-F (añade marca al final)
-R (recursivo de todos los subdirectorios)
```

* #### cp
(Copiar)
```
-u (copia, si el origen está mas actualizado que el destino)
-r (copia recursiva)
```

* #### mv
(Mueve y renombra)
```
-i (pregunta antes de sobreescribir)
```

* #### rm
(Elimina)
```

-i (pregunta)
-r (recursiva)
```

* #### touch
(Crea ficheros vación)
```

-a (solo modifica fecha de acceso)
-m (solo modifica fecha de modificación)
-c (no crea fichero si este no existe)
```  
  
* #### tar
(Empaquetar/Desempaquetar)
```

tar cvfz /media/copia.tgz ~/my-work
tar xvfz /media/copia.tgz
    
    c/x - crear un archivo/extraer archivo
    v - ver
    f - empaquetar contenido de archivos
    z - gzip
``` 

* #### dd
(copia entre dispositivos)
```
dd if=/dar/zero of=empty.img bs=1024 count=720
dd if=dev/cdrom of=/media/imagenCD.iso
dd if=/dev/hda of=/media/mbr bs=512 count=1
```




















