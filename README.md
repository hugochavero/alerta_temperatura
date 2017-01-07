# Alerta Temperatura

## Objetivo.
El archivo temp.py es un ejemplo de como implementar una alarma en weewx para determinado evento climatico o metereológico. 

## Implementación.
### Primer paso.
Agregue el siguiente código en su archivo de configuración weewx.conf:
```
[Alarm]
  expression = "outTemp < 40.0"
  time_wait = 3600
  smtp_host = smtp.mymailserver.com
  smtp_user = myusername
  smtp_password = mypassword
  mailto = auser@adomain.com, anotheruser@someplace.com
  from = me@mydomain.com
  subject = "Alarm message from weewx!"
```
### Segundo paso.
Configuracion personaliza. En este ejemplo, si la temperatura exterior cae debajo de los 40 F°, se enviara un correo electrónico
a la lista separada por comas especificada en la opcion "mailto", en este caso
auser@adomain.com, another@somewhere.com
El ejemplo asume que su servidor de correo SMTP se encuentra en smtp.mymailserver.com y
que utiliza un logeo seguro (secure logins). Si esto no fuera asi, deje libres las lines
para smtp_user y smtp_password y no se intentara ningun logeo de acceso.
La configuracion del remitente en el correo es opcional. Si Usted no brinda la misma, una de facto sera instroducida; pero
su servidor SMTP puede que no la acepte
La configuracion del valor "asunto" (subjet) en el correo electronico es opcional. Si Usted no brinda la misma, una de facto sera instroducida.
Para evitar una catarata de correos electrónicos, se configuró el valor time_wait para que mande uno cada 3600 segundos (una hora).

### Tercer paso.
Para especificar que este nuevo servicio se cargue y sea ejecutador, se debe agregar el mismo a la
configuración (weewx.conf) dentro de la seccion de configuración "report_services", localizada en la sub-sección [Engine][[Services]].
```
[Engine]
  [[Services]]
    ...
    report_services = weewx.engine.StdPrint, weewx.engine.StdReport, examples.alarm.MyAlarm
```
Si Usted desea usar a la vez este ejemplo de alerta y el ejemplo lowBattery.py, simplemente debera fusionar
las dos opciones de configuracion bajo [Alarm] y agregar los dos servicios a
report_services.
