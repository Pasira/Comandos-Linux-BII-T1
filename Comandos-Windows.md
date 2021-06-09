# Comandos de Windows

* #### gpedit.msc
(editor de GPO's o directivas de de grupo locales)

* #### gpresult
(mostrar las GPO's de usuario y/o computadora que están siendo aplicadas)
```
gpresult /r (resumen tando del USER como del COMPUTER)
gpresult /r /scope USER
gpresult /r /scope COMPUTER
gpresult /z (informacion super detallada)
gpresult /h informe_fichero.html
gpresult /x informe_fichero.xml
gpresult /s remote-pc-name
```

* #### gpupdate
(actualiza las directivas locales y del dominio en el equipo local)
```
gpupdate /force (forzamos la actualizacion)
gpupdate /boot (reinicia despues de la actualizacion)
gpupdate /logoff (cierra la sesion despues de la actualizacion)
gpupdate /target USER (solo se actualizan las directivas del usuario)
gpupdate /target COMPUTER (solo se actualizan las directivas del equipo)
```

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

* #### dsget,dsadd,dsmod,dsmove,dsrm
(visualizar, añadir, modificar, mover y borrar objetos del AD)
```
dsquery user –samid "username" | dsget user -email (obtener el email de un determinado usuario)

dsquery user -samid "username" | dsget user -memberof -expand (obtener todos los grupos de un usuario, incluidos los anidados)

dsquery group -samid "DEVELOPERS" | dsget group -members -expand  | dsget user -samid (obtener los miembros de un grupo)

-------------------------------------------------------------------------

dsget user ... -effectivepso (obtener las PSO=Politicas de sobre la configuración de las contraseñas)
dsget user ... -acctexpires (obtener la fecha de expiracion de la cuenta)
dsget user ... -disabled (si o no está desactivada)
dsget user ... -mustchpwd (si o no el usuario debe cambiar la contraseña en el siguiente inicio de sesion)
dsquery computer -inactive 4 | dsmod computer -disabled yes (deshabilita todos los equipos que hayan estado inactivos durante 4 o mas semanas)

-------------------------------------------------------------------------

dsadd user "CN=Carlos,OU=Marketing,DC=ruinosa,DC=com" (añade un usuario en una OU)
dsadd computer "CN=SALESWKSTN1,OU=Ventas,DC=ruinosa,DC=com" (alta de un equipo en una OU)
dsmod group "CN=Marketing Users,CN=users,DC=ruinosa,DC=com" -addmbr "CN=Sara,OU=Marketing,DC=ruinosa,DC=com" (añade usuario a un grupo)
dsmod user "CN=Pepe,OU=Ventas,DC=ibm,Dc=com" -pwd Abcd123 -mustchpwd yes (cambia la password+politica a un usuario)

-------------------------------------------------------------------------

dsrm -subtree -noprompt -c "OU=Marketing,DC=ruinosa,DC=com" (borra toda una OU)
```

* #### net
(administrar recursos compartidos, usuarios, grupos, servicios, etc)
```
net user (muestra usuarios locales creados en la maquina)
net user pepe (muestra info del usuario pepe)

Ej: Ultimo cambio de password, si la contraseña expira, ultima sesion iniciada, grupos locales a los que pertenece, directorio principal, etc)

net user juan 1234 /add (alta del usuario local juan)
net user juan 1234 /add /domain (alta del usuario juan en el dominio)
net user fer * (con esto podemos cambiar la password del usuario)

otras opciones interesantes:

/passwordreq:yes/no (si es obligatorio tener password para esa cuenta)
/passwordchg:yes/no (si el usuario puede cambiar la contraseña)
/expires:fecha/never (expiracion de la cuenta)
/active:yes/no (activa o desactiva la cuenta)
/times:momentos en los que se puede usar la computadora/hacer login
/workstations:lista de equipos desde donde puede hacer login

-------------------------------------------------------------------------

net accounts (modifica politicas de cuentas y password)
net accounts /MINPWLEN:longitudMinimaDeLaPassword
net accounts /MAXPWAGE:maximoDeDiasQueLaPasswordEsValida
net accounts /UNIQUEPW:numeroDePasswordUnicasCuandoSeCambia
(con /DOMAIN estos comandos afectan al dominio en lugar de la maquina local)

-------------------------------------------------------------------------

net computer \\equipo /add o /del (añade o borra una maquina al dominio)

-------------------------------------------------------------------------

net session \\servidorNominas (listado con los usuarios y desde que maquinas están conectados al servidorNominas)

-------------------------------------------------------------------------

net print \\equipo (muestra las colas de impresion compartidas)
net print \\equipo\ShareName (muestra la cola de impresion de ese share)
net print \\equipo NumeroDeJob (gestion de un job particular)

otras opciones interesantes: 

/hold o /release --> retrasa/retiene o libera el job
/delete --> borra el job

-------------------------------------------------------------------------

net share (gestion de recursos compartidos, sin parametros muestra los que hay actualmente creados)

net share DataCompartido=c:\Data (comparte el directorio c:\Data con el nombre publico DataCompartido)

otra opciones interesantes:

/users:numeroMaximoUsuariosSimultaneos
/delete (borrar el recurso compartido)

-------------------------------------------------------------------------

net group desarrolladores /add (añade grupo al dominio)
net localgroup desarrolladores /add (añade grupo local a la maquina)
net group desarrolladores pepe luis /add (añade usuarios al grupo)

-------------------------------------------------------------------------

net view (muestra la lista de maquinas del dominio actual o con /domain el que tu especifiques)
net view \\equipo /ALL (muestra todos los recursos compartidos del equipo. El $ en el nombre del recurso indica que son ocultos)

-------------------------------------------------------------------------

net use (gestión de unidades hacia --> recursos compartidos)
net use e: \\financiero\cartas (en la maquina "cliente" vamos a poder engancharnos contra el share creado en el servidor \\financiero)
net use [LPTx:] \\ComputerName\printer_share /persistent:yes

otras opciones interesantes:

/delete (borrar el mapeo de unidad)
/persistent:yes (para que se realice el mapeo en cada inicio de sesion)
/user:usuario password (mapeo con credenciales concretas)

-------------------------------------------------------------------------

net config server /autodisconnect:minutos (cierra sesiones inactivas al pasar x minutos)

-------------------------------------------------------------------------

net start/stop/pause/continue nombreDelServicio (gestión de servicios)

-------------------------------------------------------------------------

net time /domain[:dominio] /set (sincroniza la hora del equipo con la del dominio)
net time /rstdomain[:dominio] /set (idem pero contra un servidor de tiempos)
```

* #### netsh (contexto) (subcontexto) comando
(utilidad de configuracion de red)

```
netsh advfirewall set currentprofile state on (activar el firewall)

netsh advfirewall firewall add rule name="Open Port 80" dir=in action=allow protocol=TCP localport=80 (regla para abrir el puerto 80 de entrada)

netsh advfirewall firewall set rule group="remote desktop" new enable=Yes (activar el servicio de RDP)

netsh interface ip show config (muestra configuracion TCP/IP)

netsh interface ip delete arpcache (borra la cache de ARP)

netsh interface ip set address name="Local Area Connection" source=static addr=192.168.0.10 mask=255.255.255.0 gateway=192.168.0.1 gwmetric=1 (configuracion IP estatica)

netsh interface ip set address name="Local Area Connection" source=dhcp (configuracion IP dinamica)

netsh interface ip add dnsservers "Local Area Connection" 10.0.0.1 (añadir servidor de DNS)

netsh set machine servidorNominas (trabajar contra ese servidor)

netsh wlan add filter permission=block ssid=”WLAN name” networktype=infrastructure (bloquea la WIFI por SSID)

netsh http add iplisten address=1.1.1.1 (publicar nueva IP de escucha)
netsh http add sslcert ipport=1.1.1.1:443 certhash=0102030405060708090A0B0C0D0E0F1011121314 appid={00112233-4455-6677-8899-AABBCCDDEEFF} (asocia un certificado con una determinada IP+Puerto)

netsh dump > copia_configuracion.txt (copia de seguridad de la configuracion)
netsh exec copia_configuracion.txt (restauracion de la configuracion)
```

* #### robocopy (origen) (destino)
(copia/backup de ficheros)
```
/S (copia subcarpetas)
/E (copia subcarpetas incluso VACIAS)
/MIR (modo espejo, copia de forma recursiva pero al terminar se eliminan los archivos en el destino que ya no existen en el origen)
/MOV (mueve archivos y los elimina del origen después de ser copiados)
/MOVE (mueve archivos y carpetas y los elimina del origen después de ser copiados)
/L (hace una SIMULACION)
/MAX:bytes o /MIN:bytes (de un determinado tamaño)
/MAXAGE:dias o /MINAGE:dias (de una determinada antiguedad)
/Z (modo REINICIABLE)
/SEC(conservar permisos) o /COPYALL
/R:numeroReintentos
/XF patron (excluye los archivos indicados)
```

* #### arp
(gestión de la tabla/cache ARP)
```
-a (muestra las entradas de la tabla)
-d direccion_ip (elimina el host especificado o todos si se usa *)
-s direccion_ip direccion_mac (agrega una entrada a la tabla)
```

* #### ipconfig
(configuracion de interfaces)
```
/displaydns (muestra las resoluciones DNS de la cache)
/flushdns (borra la cache del DNS)
/renew (renueva la direccion IP)
/release (libera conexiones)
```

* #### getmac
(obtener la dirección fisica/MAC de una serie de interfaces de red)

* #### route
(administración de la tabla de enrutamiento)

* #### tracert / pathping
(muestra la ruta que siguen los datagramas IP entre dos extremos)
```
-d (no convierte direcciones en nombres de host)
-h (numero maximo de saltos en la busqueda)
-w milisegundos (tiempo para esperar cada respuesta)
-6 (forzar usando IPv6)
```

* #### netstat
(conexiones TCP/UDP)
```
-a (muestra todas las conexiones y puertos de escucha)
-p protocolo (filtra por TCP,UDP)
-r (muestra el contenido de la tabla de rutas)
-o (muestra el PID del proceso asociado	)
-n (muestra los puertos y las direcciones en formato numerico)
```

* #### nslookup
(resolucion de peticiones DNS)
```
nslookup -querytype=TXT -timeout=10 inap.es 8.8.8.8 (consulta de los registros de tipo TXT de inap.es usando GoogleDNS)
nslookup -type=TXT -timeout=10 inap.es 8.8.8.8 (consulta de los registros de tipo TXT de inap.es usando GoogleDNS)
```

* #### certutil
(gestión de certificados digitales)
```
certutil.exe -addstore Root MyCert.cer (importa una CA al almacen raiz)
certutil.exe -p MyPassword -importpfx MyCert.pfx (importa el pfx)
certutil -user -store MY (muestra todos los certificados del almacen personal)
```

* #### sc
(gestión de servicios)
```
sc create NewService binpath= c:\...\NewServ.exe type= share start= auto
sc query type= service/driver/... state=active/inactive
sc /start/stop/delete nombreDelServicio
```

* #### whoami
(muestra información del usuario)
```
/user (nombre de usuario + SID)
/groups (grupos a los que pertenece)
/priv (privilegios de seguridad)
```

* #### ntdsutil
(herramienta de administración del fichero/bbdd del AD - )

* #### mstsc (microsoft terminal server connection)
(arranca el cliente de escritorio remoto)

* #### convert
(convertir de fat16/32 a NTFS) 

* #### powercfg
(configuración de opciones de energia)

* #### tasklist / taskkill
(gestión de tareas/procesos)

* #### msconfig
(configuración del sistema)

* #### msinfo32
(información del sistema)

* #### bcdedit
(gestión del arranque de windows)

* #### runas
(ejecutar un comando como otro user)

* #### msg
(enviar mensaje a otro usuario)

* #### pushd/popd (push directory / pop directory)
(guarda y restaura el directorio actual generalmente usados en un script)



















