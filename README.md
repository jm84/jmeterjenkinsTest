# jmeterjenkinsTest

** se le pone https en el http request se pasa el ${__property(URL)} y se hace la petición pasando la url sin https:// con el siguiente comando:

jmeter -n -t C:\ruta\testfakeapi.jmx -JURL=fakeapi.net -l C:\ruta\resultados.jtl