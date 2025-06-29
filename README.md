# jmeterjenkinsTest

# **Guía para la ejecución del test plan en JMeter**

## **Configuración del HTTP Request**
- En el campo **HTTP Request**, utiliza la variable `${__property(URL)}` para configurar la URL de la petición.
- La URL que se pasa al test plan **no debe incluir el esquema `https://`**. Por ejemplo:

fakeapi.net


## **Ejecutar el test plan desde la línea de comandos**
Utiliza el siguiente comando para ejecutar el test plan desde la terminal:

```bash
jmeter -n -t C:\ruta\testfakeapi.jmx -JURL=fakeapi.net -l C:\ruta\resultados.jtl
```
Detalles del comando:
-n: Ejecuta JMeter en modo no gráfico.
-t: Especifica la ruta del archivo .jmx del test plan.
-JURL: Define la propiedad URL que será utilizada en el test plan.
-l: Especifica la ruta donde se guardarán los resultados de la ejecución.
Prioridad de las variables
Si utilizas Build with Parameters en Jenkins para pasar la URL, el valor proporcionado en el parámetro tendrá prioridad sobre el valor configurado en el Jenkinsfile.
Ejecución según el sistema operativo
Linux: Usa el comando sh para ejecutar scripts en la terminal.
Windows: Usa el comando bat para ejecutar scripts en la línea de comandos.


## **Configuración del Pipeline en jenkins**
- Agregar plugins en jenkins: Performance plugin, github.
- Crear un new item tipo pipeline.
- Selecciona This project is parameterized
```
- nombre ENVIRONMENT
- choice: dev
uat
- Descripcion: Selecciona el ambiente para la ejecución del test plan
```
- Definicion del pipeline Script from SCM
```
- Git
- url del repo en git
- Credenciales si es privado o sin credenciales si es publico
- seleccionar rama principal : */main
- Apply y luego Save
```

