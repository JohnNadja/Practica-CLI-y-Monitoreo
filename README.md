# Práctica sobre el uso de *Azure CLI* y servicios de monitoreo.

## Índice

### [Introducción](#introducción)
### [Requisitos](#requisitos)

### [Práctica Azure CLI](#practica-azure-cli) ![climini](/images/climini.svg)
### [Práctica Azure Service Health](#práctica-azure-service-health) ![healthmini](/images/healthmini.svg)
### [Práctica Azure Monitor](#práctica-azure-monitor) ![monitormini](/images/monitormini.svg)
### [Práctica Azure Resource Manager](#práctica-azure-resource-manager) ![armmini](/images/armmini.svg)
----
### Introducción

#### Azure CLI
![Azure CLI](/images/Azure-CLI.png)

Azure CLI (*Command Line Interface*) es un programa que permite tener una forma de manipular y administrar a través de una línea de comandos los recursos del entorno de Azure. Éste se puede instalar instalar en Windows, Linux, Mac, o ejecutarlo en contenedores [Docker](https://www.docker.com/); pero no en una Chromebook. Para instalarlo, se puede usar el siguiente [enlace](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) (dependiendo del tipo de Sistema Operativo en el que se tenga) y se siguen los pasos del instalado.

#### Azure Service Health
![AzureHealth](/images/Azurehealth.png)

Service Health es un servicio que permite monitorear el estado de los servicios de Azure. Es decir, se puede verificar si un servicio está funcionando correctamente o no.
Es un servicio tipo [**SaaS**](https://azure.microsoft.com/es-mx/overview/what-is-saas/). Es decir, es un servicio que se puede usar desde cualquier lugar (y no rquiere de programación). Es un *médico* de los servicios que requieran mantenimiento. Más información [aquí](https://azure.microsoft.com/es-mx/features/service-health/).
Para revisar la *salud* de los servicios de Azure, Se puede consultar el siguiente sitio [sitio](https://status.azure.com/es-es/status).


#### Azure Monitor
![Azure Monitor](/images/Azuremonitor.png)

Es un servicio que permite monitorear los recursos de Azure. Es decir, supervisa el rendimiento de las aplicaciones o soluciones. Es un servicio tipo [**SaaS**](https://azure.microsoft.com/es-mx/overview/what-is-saas/). Es decir, es un servicio que se puede usar desde cualquier lugar (y no rquiere de programación). Azure Monitor permite hacer un seguimiento de [SLA](https://azure.microsoft.com/es-es/support/legal/sla/summary/) de los recursos ocupados. Más información [aquí](https://azure.microsoft.com/es-mx/services/monitor/).


#### Azure Advisor
![Azure Advisor](/images/Azureadvisor.png)

Es un servicio **asesor** que sugiere posibles mejoras de nuestras implementaciones en Azure. Es un servicio tipo [**SaaS**](https://azure.microsoft.com/es-mx/overview/what-is-saas/). Es decir, es un servicio que se puede usar desde cualquier lugar (y no rquiere de programación). Puede realizar recomendaciones de seguridad, rendimiento o reducir costos con ayuda de IA. Más información [aquí](https://azure.microsoft.com/es-mx/services/advisor/).

### Azure Resource Manager (ARM)
![ARM](/images/ARM.png)

ARM es un servicio que permite volver a implementar recursos o grupo de recursos dentro de una suscripción de Azure. Más información [aquí](https://azure.microsoft.com/es-mx/features/resource-manager/).


----
### Requisitos
 - Tener una cuenta de Azure para realizar la práctica en su [*Portal*](https://portal.azure.com/#home) (si aún no se cuenta con alguna, se puede hacer el registro en el siguiente [*enlace*](https://azure.microsoft.com/es-mx/free/)). 
 - Contar con una suscripción activa de Azure para poder realizar la práctica (en el enlace anterior se muestra como se puede hacer).
 - Contar con **[Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)** instalado en su sistema operativo.


----
### Práctica Azure CLI ![climini](/images/climini.svg)
1. Como primera instancia, se debe abrir el programa **CMD** o **PowerShell** y ejecutar el siguiente comando (para poder iniciar sesión en Azure): `az login`
    - Una vez ejecutado, se debe verificar que se haya iniciado sesión correctamente. Esto se hace cuando se muestra una ventana de inicio de sesión en el portal de Azure con un mensaje de confirmación.
    ![resNavegador](/images/resNavegador.png)
    - En la línea de comandos, se mostrará que todo ha ido bien (a veces se requiere presionar la tecla *Intro* o *Enter* para que se muestre correctamente):
    ![resCMD](/images/resCMD.png)
    - Si se quiere saber la lista de comandos de Azure, se puede ejecutar el siguiente comando:`az`

2. Para crear una nueva práctica (en realidad, un grupo de recursos), se debe ejecutar el siguiente comando:
    ```
    az group create --location westus --resource-group practicaCLI
    ```
    
    - Group create crea un grupo de recursos en Azure.
    - Location westus indica que se creará en la ubicación central de EU en Azure.
    - Resource group practicaCLI indica el nombre del grupo de recursos que se creará.
        - Esperarmos a que se cree el recurso.
    ![GroupCreate](/images/GroupCreate.gif)

3. Para corroborar que se ha creado correctamente, se debe revisar la plataforma del [Portal de Azure](https://portal.azure.com/#home) y verificar que el grupo de recursos se ha creado correctamente en la sección de **Grupos de Recursos**.
![GroupView](/images/GroupView.gif)

##### Hemos creado un grupo de recursos en Azure con Azure CLI.

[⚠](#importante)
[Regresar a índice](#índice)

----
### Práctica Azure Service Health ![healthmini](/images/healthmini.svg)

1. Usando el mismo grupo de recursos que hemos creado anteriormente, se puede crear un nuevo recurso de tipo *Service Health* en Azure. Éste se encuentra buscando *Azure Service Health* en el [Portal de Azure](https://portal.azure.com/#home). Este recurso no genera ningún costo.
    - Dentro del recurso, se puede observar una interfaz simple que muestren los estados de los servicios de Azure.
    ![problemasServicio](/images/problemasServicio.gif)

2. Para saber cúando hay alguna falla en alguno de los servicios de Azure, se debe presionar el botón **Añadir  alerta de Service Health**.
    - En la pantalla que se muestra, se debe de configurar sobre qué queremos recibir notificaciones.
    - En condiciones:
        |Condición|valor|
        |---|---|
        Suscripción|Seleccionar la suscripción activa que se desea utilizar|
        Servicio|Seleccionar el servicio que se desea tener notificación. Ejemplo: **App Service**|
        | Regiones | Seleccionar la region que se desea tener notificación (puede ser *Global*)|
        | Tipo de evento | Es el tipo de error que se notificacrá.|
        
    ![addAlerta](/images/addAlerta.gif)

    - En acciones se debe **seleccionar un grupo de acciones**
        - Al pulsar el botón **Crear un grupo de acciones** nos dirigirá a una nueva página.
            - En datos básicos:
                |Campo|valor|
                |---|---|
                | suscripción | Seleccionar la suscripción en la que estamos realizando la práctica|
                | Grupo de recursos | Seleccionar el grupo de recursos en el que estamos realizando la práctica|
                | Nombre | Asinar un nombre al grupo de acciones|
            
            - En Notificaciones:
                |Campo|valor|
                |---|---|
                | Tipo de notificación | Seleccionar el tipo de notificación que se desea utilizar. En esta ocasión será **Correo electrónico/Mensaje SMS/Insertar/Voz**|
                | Nombre | Asignar un nombre a la notificación. Ejemplo: "Notificación de falla"|

            - Al seleccionar la opción de Correo, se muestra un panel a la derecha. Marcamos la casilla de **correo electrónico** y escribimos el correo electrónico que recibirá las notificaciones.
            - Pulsamos los botones **Aceptar**, **Revisar y crear** y **Crear**.
        ![grupoAcciones](/images/grupoAcciones.gif)

        - Si pulsamos el botón **Grupo de acciones de prueba** y el grupo de acciones creadom nos mostrará una ventana donde haremos clic en un botón similar (Grupo de acciones de prueba) y podemos mandar una alerta tipo test al correo que ingresamos. Por ejemplo: *Alerta de estado de servicio*.
        - Recibiremos un correo con el mensaje de prueba.
        ![testGrupoAcciones](/images/testGrupoAcciones.gif)

3. Regresamos a la sección de **Crear una regla de alertas**.
    - En detalles de la regla de alertas:
        |Campo|valor|
        |---|---|
        | Nombre de la regla de alertas | Asignar un nombre a la regla de alertas.|
        | Descripción | (Opcional) Asignar una descripción a la regla de alertas.|
        | Grupo de recursos | Seleccionar el grupo de recursos en la que se está realizando la práctica|
    - Aceptamos los cambios con **Crear regla de alertas**.
    ![reglaAlertas1](/images/reglaAlertas1.gif)


##### Ahora contamos con una regla de alertas de Service Health en Azure.

[⚠](#importante)
[Regresar a índice](#índice)

------------


### Práctica Azure Monitor ![monitormini](/images/monitormini.svg)

*Para poder realizar ésta práctica, se necesitará contar con una Máquina Virtual en Azure.* 
Podemos optar para crear una con el siguiente [enlace](https://github.com/JohnNadja/Practica-VM-dentro-de-VM#requisitos).


1. Crearemos un recurso en el grupo de recursos que hemos creado anteriormente. Este recurso se encuentra buscando *Azure Monitor* en el [Portal de Azure](https://portal.azure.com/#home). Este recurso no genera ningún costo**.
 
- Dentro del recurso, se puede observar desde el inicio la **Información general** que muestran *subservicios* de monitoreo.
- En **Registro de Actividad** se desglosa la actividad de recursos creados.
- En **Alertas** podemos crear y consultar alertas como de seguridad, rendimiento, etc.
- En **Métricas** se puede observar las métricas de algún recurso a seleccionar y qué tanto se está usando.
- En **Registros** muestra qué se ha hecho en algún recurso específico.
- **Libros** son la unión de todos los registros para poder revisar lo que se hace en Azure. Habitualmente, se trabajan con IA.
![monitorMuestra](/images/monitorMuestra.gif)

2. Una vez [conectados a la VM](https://github.com/JohnNadja/Practica-VM-dentro-de-VM#acceso-a-las-m%C3%A1quinas-virtuales), podemos acceder a **Métricas**.
    - En **Métricas**, seleccionamos el recurso de la VM y las diferentes métricas que se pueden observar.
    ![metricasVM](/images/metricasVM.gif)

    - En **Alertas**, crearemos una alerta de tipo *Regla de alertas*. (** Nota, las alertas ***sí*** tienen costo)
        - Seleccionamos el recurso (la Máquina Virtual) y aceptamos.
        - En **Condición** buscamos la que se llame (por ejemplo) **Percentage CPU**. y desplegará unas opciones adicionales. 
            - Nos interesa el ***Valor del umbral***, es decir, el porcentaje de uso de CPU que se desea que se detecte.y la ***Granulidad de agregación*** (periodo de acutalización). Podemos seleccionar el tiempo que nos permitan como opciones.
        - En **Acciones** seleccionamos el grupo de acciones que queremos que se ejecute cuando se detecte el umbral. Queremos que sea por medio de un **correo electrónico**.
        - En **Detalles** buscamos el apartado de:
            |Parámetro | Valor|
            |----|-----|
            | Gravedad | Se esoge la gravedad de la alerta. En esta ocasión será **Crítico**.|
            |Nombre de la alerta |le asignamos un nombre a esta alerta.|
            | Descripción | Le asignamos una descripción a esta alerta.|
            | Habilitar tras la creación | Marcamos la casilla.|
            |Resolver alertas automáticamente | Marcamos la casilla.|
        
        - Aceptamos la configuración con **Crear**.
        ![alertamonitor](/images/alertaMonitor.gif)

3. Para ver las métricas, ingresamos a la VM
    -  Debería llegar un correo de aviso por el porcentaje de CPU de límita para notificar que se está usando más de lo "establecido".
    ![correoMonitor](/images/correoMonitor.png)

##### Ahora contamos con una regla de alertas de Monitor en Azure.

[⚠](#importante)
[Regresar a índice](#índice)

----
### Práctica Azure Advisor ![advisormini](/images/advisormini.svg)

*Para poder realizar ésta práctica, se necesitará contar con una Máquina Virtual en Azure.* 
Podemos optar para crear una con el siguiente [enlace](https://github.com/JohnNadja/Practica-VM-dentro-de-VM#requisitos).

1. Crearemos un recurso en el grupo de recursos que hemos creado anteriormente. Este recurso se encuentra buscando *Azure Advisor* en el [Portal de Azure](https://portal.azure.com/#home). Este recurso no genera ningún costo.

    - Dentro de éste recurso, nos dará al inicio (en ***Puntuación de Adivsor***) una puntuación en forma de porcentaje de los recursos que se están impelementando. Además, muestra por categoría porcentajes sobre los recursos en forma general.
    - En ***Excelencia Operativa***, mostrará información de la nube y qué es posible para mejorar. Sin embargo, requiere de tiempo para que se consiga la información y sus recomendaciones.
    ![advisorMuestra](/images/advisorMuestra.gif)

    - En ***Alertas***, podemos crear y consultar alertas:
        |Parámetro | Descripción |
        |----|-----|
        | Grupo de recursos | El grupo de recursos que se desea monitorizar.|
        | Configurado por | Categoría y nivel de impacto, o Tipo de recomendación. Elegimos en esta ocasión la primera|
        | Categoría | Es el tipo de alerta que será notificado. Existe **Costo**, **Rendimiento**, **Confiabilidad**, **Excelencia Operativa**. Usaremos ésta vez **Costo**.|
        | Nivel de impacto | (Opcional) Es el nivel de impacto que se desea que se detecte. Elegimos en esta ocasión **Bajo**.|
        | Grupo de acciones | (Opcional) Es el grupo de acciones que se desea que se ejecute cuando se detecte la alerta. Elegimos en esta ocasión **Correo electrónico** (de acuerdo con las anteriores prácticas para crear el grupo de acciones).|
        | Nombre de la regla de alerta | Es el nombre de la regla de alerta.|
        | Descripción | Es la descripción de la regla de alerta.|

        - Creamos la alerta
        ![alertaAdvisor](/images/alertaAdvisor.gif)
        
        

##### Ahora contamos con una regla de alertas de Advisor en Azure.

[⚠](#importante)
[Regresar a índice](#índice)

----
### Práctica Azure Resource Manager ![armmini](/images/armmini.svg)
*Para poder realizar ésta práctica, se necesitará contar con un grupo de recursos o un recurso (como una [VM de Azure](https://github.com/JohnNadja/Practica-VM-dentro-de-VM#requisitos)).*

Hay 2 formas (en esta ocasión) para hacer plantillas ARM:

#### Conseguir plantilla a través de un grupo de recursos (con un recurso).
1. Ingresamos al grupo de recursos que hemos creado anteriormente. Dentro, buscaremos en el panel izquierdo una opción que se llame *Exportar plantilla*. Esa opción se encuentra en la sección **Automation**.
    - Mostrará una plantilla en formato JSON. para poder crear un *clon* del recurso o grupo de recursos.
    - Se puede **Descargar**, **Agregar**, **Implementar**o **Ver** la plantilla.
    ![ARM1](/images/ARM1.gif)

#### Crear una plantilla en un editor de texto (Como [Visual Studio Code](https://code.visualstudio.com/)).
    
##### Requisito para crear una plantilla:
- [Visual Studio Code](https://code.visualstudio.com/)
- Extensión de [ARM](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools) y [Bicep](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-bicep) instalada en el editor.
    
1. Crearemos un archivo de tipo *JSON* en el directorio que decidamos para nuestro proyecto. Este archivo se llamará **azuredeploy.json**.

2. Usar el siguiente código para crear una plantilla (esta es una plantilla vacía):
    ```json
    {
        "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "resources": []
    }
    ```

3. Para subirla, se necesita de **Azure CLI**. Se abre el explorador de archivos donde se encuentre el archivo **azuredeploy.json**. Se necesita tener iniciada una sesión de Azure (`az login`).

    - Ejecutamos el comando (los paramétros en *mayúscula* serán reemplazados por los valores reales): 
        ```bash
        az deployment group create --name NOMBRE_PLANTILLA --resource-group NOMBRE_GRUPO_RECURSOS --template-file DIRECCION_ARCHIVO_PLANTILLA
        ```

        - Ejemplo:
            ```bash
            az deployment group create --name mi-plantilla --resource-group practicaCLI --template-file azuredeploy.json
            ```
        - Esperamos a que se muestre el mensje de confirmación: `Running`
        - Buscamos en el grupo de recursos en el que se implementó la plantilla.
        ![ARM2subir](/images/ARM2subir.gif)
        ![buscarARM2](/images/buscarARM2.gif)

4. Para editar la plantilla, simplemente se codifica en el editor de texto el archivo **azuredeploy.json**. Por ejemplo, agregar una *Cuenta de almacenamiento*: 
    ```json
    {
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2021-09-01",
            "name": "micuentadealmacenamiento",
            "location": "Central US",
            "sku": {
                "name": "Standard_LRS"
            },
            "kind": "StorageV2",
            "properties": {
                "supportsHttpsTrafficOnly": true
            }
        }
    ]
    }
    ```
    
    - Ejecutamos el mismo comando:
        ```bash
        az deployment group create --name mi-plantilla --resource-group practicaCLI --template-file azuredeploy.json
        ```
    - Esperamos a que se muestre el mensje de confirmación: `Running`
    
    ![ARM2edit](/images/ARM2edit.gif)

    - Buscamos de nuevo en el grupo de recursos en el que se implementó la plantilla para ver los cambios afectados.
    ![ARM2vista](/images/ARM2vista.gif)


##### Ahora contamos con dos maneras de crear plantillas ARM en Azure.

[⚠](#importante)
[Regresar a índice](#índice)

---- 
# **⚠Importante⚠** 
### Recordar eliminar el grupo de recursos que se creó en Azure para evitar costos extras no deseados en caso de no ocupar el servicio.
Se puede hacer desde el panel de Azure en inicio y buscando el tipo de recurso que se llama **Grupo de Recursos**.
###### <sub>[Volver al índice](#índice)<sub>

## Hasta aquí la finalización de la práctica.