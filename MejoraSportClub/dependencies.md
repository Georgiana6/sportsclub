## 2. Dependencias

1. La creación del archivo "dependabot.yml" dentro de la carpeta "github" en el respositorio:

![alt text](image-20.png)

### Configuración archivo
2. Aplicar la configuración necesaria dentro del archivo: 

![alt text](image-21.png)

- Se activa Despendabot para Python, con el pip, revisando "requirements.txt" y "requirements-dev.txt", donde este busca nuevas versiones, las vulnerabilidades en el caso de que haya y si se encuentran dependencias inseguras.

- Activate the Dependabot for GitHub Actions

- Se va ha realizar cada semana 

- You will also have to create PRS atomically, in the event that you find necessary updates or vulnerabilities.

### Subida GitHub

Para poder hacer la subidad del archivo de dependencias creado se va ha ejecutar los siguenten desde la terminal: 

    git add .github/dependabot.yml
    git commit -m "Dependabot"
    git push
![alt text](image-22.png)

Se puede comprobar que recientemente se hizo la subida:

![alt text](image-23.png)

Revisando el apratado de seguridad se ve que detectado el yml creado y se ha activado manualmente.

![alt text](image-24.png)

Al ir a la opción "Pull requests" que se ver ver en el munu superior se ha podido comprobar que enuentra en funcionamiento.

![alt text](image-25.png)
Como se peude ver en al imagen superior aparece varias Pull requests en total 8.

![alt text](image-26.png)
Cuando nos encntamos dentro de una, se puede la vulenerabilida detallada en detalles y la modificación que se recomienda. En este primer caso se trata de Augmemtar acciones / caché de 4 a 5. Y con simplemente darle a concidir se aplica el cambio de manera automatica.

![alt text](image-28.png)
Todavia aprecen problemas dentro del repositorio, exactamente en pip-audit y line.

![alt text](image-27.png)
Tambien decir que se puede ver con exactitud sobre e cambio que se quiere hacer y la ubicación de este en el propio archivo.

![alt text](image-32.png)
Para poder aplicarlo únicmanete se le tendria que dar a "Solicitar de extracción de función" y luego en "Confirmar funsión"

![alt text](image-33.png)

Y si se ha llegado aplicar correctamente no aparecerá un mensaje de confirmación de la misma manera que se puede observar en la siguiente imagen

![alt text](image-34.png)
![alt text](image-31.png)
![alt text](image-35.png)

Recalling the previous problems, I came to see the motorcycle that did not pass all the tests: due to the issue of a space and the existence of detected vulnerabilities.

![alt text](image-30.png)
Se peuede ver una linia en blanco entrando en conflicto con los tets

![alt text](image-36.png)
Also when uploading the changes made to the repository, there is a need to use a "pull" 

![alt text](image-38.png)
Y se puede ver la exitencias de enimerable ejecuciones tato fallidad como correcta producidos a partir de los pasos anteriores.

![alt text](image-39.png)

I continue with the requested corrections of the failed tests, the enums.py has been modified
![alt text](image-29.png)

Pero al hacer "ruff check" se ha visto que aunque se corrida de manera malnual no se esta aplicado, por lo que se ha usado ""
![alt text](image-42.png)
--> La eliminación de sys porque no se esta usa
![alt text](image-43.png)
![alt text](image-41.png)
Since making the changes manually, it continues to give problems so in the end it has been left to use "--fix"

![alt text](image-44.png)
Y ciertamente se ha podido actualizar bien con los formato correcto

![alt text](image-45.png)
Tambie habia el problema con la versió actual de Django, por lo qeu segun lo recomendado se cambio 6.0 a 6.0.

![alt text](image-47.png)
Y al volver ha ejecutar el .in para generar limpiamente otro .txt y como se puede confirmar que si se ha hablidado el cambio y sin problemas aparentes.

![alt text](image-48.png)
![alt text](image-49.png)
--> rewrite dependencies
![alt text](image-50.png)
-->
![alt text](image-51.png)
Al volver a GitHub se puede ver que se ha solucionado uno de los test, pero todavia falta line

![alt text](image-52.png)
Volviendo a ver la causa se ha visto que la mejor opciones es usar "format --check"  y "formar . se ha aplicado bien de 88 archivos a 89.
![alt text](image-53.png)
Junto con la subida al GitHub
![alt text](image-54.png)
![alt text](image-55.png)

Como se puede llegar ha ver todos los test ha ido bien y no hay problemas actaules.

## 3 Herramientas Dependabot
### OWASP Dependency‑Check
![alt text](image-56.png)
#### Qué és
Es una herramienta de codigo abierto desarrollado para la comunidad OWASP (unas de las comunidades de seguridad mñas grandes o conocidas), teniendo en cuenta que su objetivo es analizar las dependencies por ejemplo de un proyecto, junto con la detección de vulnerabilidades, que además son comprobadas con una base de datos como por ejemplo NVD, que puede ser facilmente usada en auditórias de seguridad.

#### Pros y contras
Principalmente uno de sus pros es que se trata de open-source, facil de utilizar, con detecciones de vulnerabilidades del día a día, sin la necesidad de tener que usar GitHub por lo que nos aporta más libertat de uso, sin mencionar su alta compatiblidad con los diversos lenguajes.

Por otra lado hay que decir que puede llegar a tadar en su analisis sobretodo si se tarta de la primera vez.También decir que usar la interfaz HTML no esta tan intuitiva, sin dejar de lado que se tiene que instalar localmente o tambien en un servidor propio.

#### Cómo se instala

A la hora de querer hacer la instalación de esta primera herramienta, es necesario ejecutar el siguiente comando:
    
    choco install dependency-check
(Tambien se puede descargar ek archivo zip desde la página oficial).



![alt text](<Captura de pantalla 2026-02-04 201913.png>)

    Set-ExecutionPolicy Bypass -Scope Process -Force; `
    [System.Net.ServicePointManager]::SecurityProtocol = `
    [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; `
    iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))

![alt text](image-58.png)
   
    choco --version

![alt text](image-57.png)

As there have been several problems because you need "choco" in advance to be able to use it and as it was manually by command it did not work or errors appeared, it has been obtained by downloading the zip. 

Tambien no decia que nniamos que tener actualizado java, por lo que se hizo con la descarga de u msi y por lo tanto a la ejecución.
![alt text](image-59.png)
De la misma manera que se puede ver en la siguientes imagenes:
![alt text](image-60.png)

![alt text](image-61.png)
#### Cómo se ejecuta

Para poder ejecutar la OWASP se realiza de la próxima manera:

    dependency-check --scan . --format HTML --out report
Con el comando anterior se haria estando dentro del repositorio, pero en mi caso se ha hecho el comando mostrado en el próxima imagen:

![alt text](image-62.png)

As mentioned above, the first start will take several minutes.

![alt text](image-63.png)

#### Resultado del escaneo

![alt text](image-64.png)
Eecución del reporte.
![alt text](image-65.png)
El HTML generado:
![alt text](image-66.png)
No ha vulnerabilidades detectadas
![alt text](image-67.png)

Como se puede ver en la imagen anterior no se ha detectado nunguna vulnerabilidad actualmente, pero hay que tener en cuenta que en los pasos anterores ha solcionado, por lo que no es extranos que no den resultados de vulnerabilidades detctado por lo que es una buena señal.

Significando de esta maner que tanto el "requirements.txt" como la actualización de Django estan correctamente.

Hay que decir que tambien menciona las dependencias scaneadas, “Dependencies Scanned: 120 (115 unique)” que seria una afirmación de que Dependency-Check ha analizado todos los archivos del repositorio. Tambien decir el uso de dependencias reales y archivos auxiliares por lo que normal que el número sea alto y tambien hay que no són reales pero es normal por el hecho de que se trate de un proyecto web.

"Aviso del .NET Analyzer" donde se puede ver el mensaje "Could not execute .NET AssemblyAnalyzer, is the dotnet 8.0 runtime or sdk installed?", como el proyecto es con Python y no .NET no afecta, por el hecho de que intenta analizar cualquier .dll o .exe pero como no se usa .NET 8 se nuesta este aviso, pero no afecta al aálisi de dependencias de Python.


### Snyk
#### Qué es
Sobre esta segunda herramienta, de plataforma SaaS, enfocada primeramente en la seguridad de aplicaciones, como tambien en analisis de dependencias, los contenedores, infraestructuras de codigo o como en nuestro caso las vulnerabilidades dentro de un repositorio.

#### Pros y contras

Hay que decir que se tiene una intefeaz muy intuitiva y facil de manejar, con la posibilidad de detectar varias vulnerabilidades en diferentes ecocistemas. Tambien se puede integrar con GitHub, junto con el ofrecimiento de alertas automáticas y PRs de actualizaciones, donde tambien afrece un CLI muy potente.

Por otro lado dentro de las puntos negativos se puede decir que no se trata de una herramienta completamente de codigo abierto, se necesita crearse una cuenta en la plataforma, la versióm gratis tiene varias limitaciones y depende de un servicio externo, por lo que no es ideal en entornos privados o que no tengan internet.


#### Comunidad

Su comunidad es muy activa, con un aplio soporye empresarial, junto con una documentación muy extensa y además la integración con IDEs como por ejemplo VSCode.

#### Cómo se hace la instalación

Antes de hacer la instalación es necesario tener Node.js y se puede realizar con el sisguiente comando:

    npm install -g snyk

Después hay que auntenticarse ejecutando lo próximo:

    snyk auth
    
- El escaneo de vulnerabilidades 

        snyk test
- Para monitorizar un proyecto y recibir alertas: 

        snyk monitor
 

#### ¿Por qué no lo elegí para instalar? 
Hay que decir que es una herramienta muy potente, pero el hecho de que tenga algunas limitaciones y que no se pueda usar libremente dentro de un entono local como por ejemplo si OWASP.

### Renovate
#### Qué es
A diferencia a las anteriores herramientas Renovate esta se trata de un bot automatizado que analiza los repositorios y que crea pull requests para mantener las dependencias actaualizadas. Siendo también una alernativa de codigo abierto, donde su objetivo principal no es simplemente detectar vulnerabilidades, sino que mantener las versiones al día, lo que indirectamente mejora la seguridad.

#### Pros y contras
Los puntos positivos es que es de codigo abierto, muy facil de configurar, sin importar el lenguaje, las agrupaciones de actualizacione separa evitar ruido, funciona con GitHub y además se puede ejecutar como contenedor Docker en entornos privados.

Mencionado tambien que esta no analiza vulnerabilidades directamente, se requiere una configuración avanzada, los archivos "renovate.json", puede llegar a generar muchas PRs llegando a molestar en el caso de que no se llegue a configurar bien.
 
#### Comunidad
En relación a su comunidad hay que decir que es muy activa, mantenido por Mend.io, la documentación externa y es muy usada por empresa grandes que necesitan automatzaciones avanzadas.

#### Cómo se usa
- Hay que instalar la GitHub App de Renovate en el repositorio
- Para añadir un archivo de configura de manera muy básic

        { "extends":      ["config:base"]
        }
- Ya deberia empezar a crear PRs (como por ejemplo para Actualizar Django, analizar dependencias de Note, etc. )

#### Por qué no lo elegí para instalar
Renovate es una herramienta muy potente para automatizar actualizaciones de dependencias, pero no fue seleccionada porque su objetivo principal no es analizar vulnerabilidades, sino mantener versiones al día. Además no es tan paractica y facil de usar en comparación a la primera herramienta explicada.

## Enlaces
Fork del repositorio:  
https://github.com/Georgiana6/sportsclub

requirements.txt  mejorado:  
https://github.com/Georgiana6/sportsclub/blob/main/requirements.txt

requirements.md:  
https://github.com/Georgiana6/sportsclub/blob/main/requirements.md

dependencies.md:  
https://github.com/Georgiana6/sportsclub/blob/main/dependencies.md

Workflow CI/CD modificado:  
https://github.com/Georgiana6/sportsclub/blob/main/.github/workflows/ci.yml
