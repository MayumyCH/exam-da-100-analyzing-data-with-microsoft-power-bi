# Get data in Power BI

## Introduction
Como la mayoría de nosotros, usted trabaja para una empresa en la que debe crear informes de Microsoft Power BI. 

Los datos residen en varias bases de datos y archivos diferentes. Estos repositorios de datos son diferentes entre sí, algunos están en Microsoft SQL Server, algunos están en Microsoft Excel, pero todos los datos están relacionados.

En el escenario de este módulo, usted trabaja para **Tailwind Traders**. El liderazgo senior le ha encomendado la tarea de crear un conjunto de informes que dependan de los datos en varias ubicaciones diferentes:
- La base de datos que rastrea las transacciones de ventas está en SQL Server, una base de datos relacional que contiene qué artículos compró cada cliente y cuándo. También rastrea qué empleado realizó la venta, junto con el nombre y la identificación del empleado. 
- Para obtenerla fecha de contratación del empleado, su título o quién es su gerente, debe acceder a los archivos que Recursos Humanos mantiene en Excel. Siempre ha estado solicitando que utilicen una base de datos SQL, pero aún no han tenido la oportunidad de implementarla.
- El envío de articulos se registra en la aplicación de almacenamiento, que es nueva para la empresa. Los desarrolladores optaron por almacenar datos en CosmosDB, como un conjunto de documentos JSON.
- La aplicación que ayuda con las proyecciones financieras, para que puedan predecir cuáles serán sus ventas en los meses y años futuros, basándose en las tendencias pasadas se almacenan en Microsoft Azure Analysis Services. 

A continuación, se muestra una vista de las numerosas fuentes de datos de las que se le solicita que combine datos. 

<img src="https://docs.microsoft.com/en-us/learn/modules/get-data/media/1-data-source-scenario-c.png#lightbox" alt="descargar" border="0" width=600px>

Una vez que haya aprendido los detalles de cada sistema (como extraer la data), puede **usar Power Query** (el motor de consulta utilizado por Power BI y Excel) para ayudarlo a **limpiar los datos**, como cambiar el nombre de las columnas, reemplazar valores, eliminar errores y combinar los resultados de la consulta.

Una vez que los datos se hayan limpiado y organizado, estará listo para crear informes en Power BI. 

Finalmente, publicará su conjunto de datos e informes combinados en Power BI service (PBIS). A partir de ahí, otras personas pueden utilizar su conjunto de datos y crear sus propios informes o pueden utilizar los informes que ya ha creado.

Este módulo se centrará en el primer paso, obtener los datos de las diferentes fuentes de datos e importarlos a Power BI mediante Power Query.

Al final de este módulo, podrá:

- Identificar y conectarse a una fuente de datos
- Obtenga datos de una base de datos relacional, como Microsoft SQL Server
- Obtener datos de un archivo, como Microsoft Excel
- Obtener datos de aplicaciones
- Obtenga datos de Azure Analysis Services
- Seleccione un modo de almacenamiento
- Solucionar problemas de rendimiento
- Resolver errores de importación de datos 

## Get data from files
_Obtener datos de archivos_

Un archivo plano es un tipo de archivo que tiene solo una tabla de datos y cada fila de datos está en la misma estructura. El archivo no contiene jerarquías. Probablemente, esté familiarizado con los tipos más comunes de archivos planos, que son archivos de valores separados por comas (.csv), archivos de texto delimitado (.txt) y archivos de ancho fijo. Otro tipo de archivo serían los archivos de salida de diferentes aplicaciones, como los libros de trabajo de Microsoft Excel (.xlsx). 

Power BI Desktop le permite obtener datos de muchos tipos de archivos. Puede encontrar una lista de las opciones disponibles cuando usa la característica Obtener datos en Power BI Desktop. Las siguientes secciones explican cómo puede importar datos de un archivo de Excel que está almacenado en una computadora local. 

### Scenario

El equipo de Recursos Humanos (RR.HH.) de Tailwind Traders ha preparado un archivo plano que contiene algunos de los datos de los empleados de su organización, como el nombre del empleado, la fecha de contratación, el puesto y el gerente. Han solicitado que cree informes de Power BI utilizando estos datos y los datos que se encuentran en varios otros orígenes de datos.

**Ubicación de archivo plano**

Sus archivos de Excel pueden existir en una de las siguientes ubicaciones:

1. **Local**: El archivo no se mueve a Power BI. En su lugar, se crea un nuevo conjunto de datos en Power BI y los datos del archivo de Excel se cargan en él. En consecuencia, los cambios en el archivo de Excel original no se reflejan en su conjunto de datos de Power BI.

2. **OneDrive para la empresa**: puede extraer datos de OneDrive para la empresa en Power BI. Este método es eficaz para mantener sincronizados un archivo de Excel y su conjunto de datos, informes y paneles en Power BI. Si se encuentran cambios, su conjunto de datos, informes y paneles se actualizan automáticamente.

3. **OneDrive - Personal**: puede usar datos de archivos en una cuenta personal de OneDrive y obtener muchos de los mismos beneficios que obtendría con OneDrive para la Empresa. Sin embargo, deberá iniciar sesión con su cuenta personal de OneDrive y seleccionar la opción Mantener la sesión iniciada.

4. **SharePoint Team Sites**: guardar sus archivos de Power BI Desktop en sitios de grupo de SharePoint es similar a guardar en OneDrive para la empresa. La principal diferencia es cómo se conecta al archivo de Power BI. Puede especificar una URL o conectarse a la carpeta raíz. 

> El uso de una opción en la nube como OneDrive o SharePoint Team Sites es la forma más eficaz de mantener sincronizados su archivo y su conjunto de datos, informes y paneles en Power BI. Sin embargo, si sus datos no cambian con regularidad, guardar archivos en una computadora local es una opción adecuada. 

Como cargar un archivo
> Inicio -> Obtener datos -> Escoger origen de la data (Excel)

**Change the source file**
_Cambiar el archivo fuente_

Para mantener sus informes actualizados, si su archivo fuente se cambio de origen uested deberá actualizar sus rutas de conexión de archivos en Power BI.
Power Query proporciona varias formas de realizar esta tarea, de modo que pueda realizar este tipo de cambio cuando sea necesario.

- Configuración de la fuente de datos
- Configuración de la consulta
- Editor avanzado

> Power query -> Inicio -> configuración de la fuente de datos

> Power bi -> Inicio -> Transformar datos -> Configuracion de origen de datos

## Get data from relational data sources

_Obtener datos de fuentes de datos relacionales_

Si su organización usa una base de datos relacional conectar Power BI a la base de datos le ayudará a supervisar el progreso de su negocio e identificar tendencias, para que pueda pronosticar cifras de ventas, planificar presupuestos y establecer indicadores y objetivos de rendimiento. 

**Power BI Desktop** puede **conectarse** a muchas **bases de datos relacionales** que se encuentran en la nube o local.

### Scenario

> Inicio -> Obtener datos -> SQL Server

Se tendra 3 opciones
Data Connecty mode

- **Import** - Mas recomendable
- **DirectQuery**
- **Advanced options**
```
    SELECT
    ID
    , NAME
    , SALESAMOUNT
    FROM
    SALES
    WHERE
    OrderDate >= ‘1/1/2020’
```

<img src="https://i.ibb.co/MPwCG5X/sql-power-bi.png" alt="descargar" border="0" width=600px>

> Es una práctica recomendada evitar hacerlo directamente en Power BI. En su lugar, considere la posibilidad de escribir una consulta como esta en una vista. 
Una vista es un objeto de una base de datos relacional, similar a una tabla. Las vistas tienen filas y columnas y pueden contener casi todos los operadores del lenguaje SQL. Si Power BI usa una vista, cuando recupera datos, participa en el plegado de consultas, una característica de Power Query.
Power Query optimizará la recuperación de datos de acuerdo con cómo se usan los datos más adelante.



## Get data from a NoSQL database
_Obtenga datos de una base de datos NoSQL_

Algunas organizaciones no usan una base de datos relacional, sino que usan una base de datos NoSQL. Una base de datos NoSQL (también denominada no SQL, no solo SQL o no relacional) es un tipo flexible de base de datos que no utiliza tablas para almacenar datos.

### Scenario
Los desarrolladores de software de Tailwind Traders crearon una aplicación para administrar los productos de envío y seguimiento desde sus almacenes que utiliza CosmosDB, una base de datos NoSQL, como repositorio de datos. Esta aplicación utiliza Cosmos DB para almacenar documentos JSON, que son formatos de archivo estándar abiertos que se utilizan principalmente para transmitir datos entre un servidor y una aplicación web. Debe importar estos datos en un modelo de datos de Power BI para la generación de informes.

**Conectarse a una base de datos NoSQL (Azure Cosmos DB)**

> Inicio -> Obtener datos -> Más... -> Azure ->  Azure Cosmos DB

<img src="https://docs.microsoft.com/en-us/learn/modules/get-data/media/4-get-data-cosmos-ssm.png#lightbox" alt="descargar" border="0" width=600px>

**Importar un archivo JSON**
Los registros de tipo JSON deben extraerse y normalizarse para poder informar sobre ellos, por lo que debe transformar los datos antes de cargarlos en Power BI Desktop

## Get data from online services
_Obtenga datos de servicios en línea_

Para admitir sus operaciones diarias, las organizaciones suelen usar una serie de aplicaciones de software, como SharePoint, OneDrive, Dynamics 365, Google Analytics, etc. Estas aplicaciones producen sus propios datos. Power BI puede combinar los datos de varias aplicaciones para generar información e informes más significativos.

### Scenario

Tailwind Traders usa SharePoint para colaborar y almacenar datos de ventas. 
El formulario que usa el liderazgo existe en SharePoint. Debe establecer una conexión a estos datos, de modo que los objetivos de ventas se puedan usar junto con otros datos de ventas para determinar el estado de la canalización de ventas.

En las secciones siguientes se examina cómo usar la característica Obtener datos de Power BI Desktop para conectarse a orígenes de datos generados por aplicaciones externas. 

Para ilustrar este proceso, se proporciona un ejemplo que muestra cómo conectarse a un sitio de SharePoint e importar datos de una lista en línea.

**Conéctese a los datos de una aplicación**

> Inicio -> Obtener datos -> Más... -> Servicios en linea -> Lista en línea de SharePoint.

## Select a storage mode
_Seleccione un modo de almacenamiento_

La forma más popular de usar datos en Power BI es importarlos a un conjunto de datos de Power BI. Importar los datos significa que los datos se almacenan en el archivo de Power BI y se publican junto con los informes de Power BI.

En el caso en el que importar los datos no es un método ideal se debe crear los conjuntos de datos en Power BI para que pueda crear objetos visuales y otros elementos de informe. 
Por ejemplo el departamento de ventas tiene muchos conjuntos de datos diferentes de diferentes tamaños. 
Por motivos de seguridad, no se le permite importar copias locales de los datos en los informes, por lo que la importación directa de datos ya no es una opción. 

Por lo tanto, debe crear una conexión directa con el origen de datos del departamento de ventas.
Sin embargo, a veces puede haber requisitos de seguridad alrededor de los datos que hacen imposible importar directamente una copia. O es posible que los conjuntos de datos simplemente sean demasiado grandes y tarden demasiado tiempo en cargarse en Power BI y que desee evitar crear un cuello de botella de rendimiento. 

Power BI resuelve estos problemas mediante el **_modo de almacenamiento de DirectQuery_**, que le permite consultar los datos del origen de datos directamente y no importar una copia en Power BI. 

> DirectQuery es útil porque garantiza que siempre está viendo la versión más reciente de los datos.

Los tres tipos diferentes de modos de almacenamiento que puede elegir:
- importación
- DirectQuery
- Dual (compuesto)


Puede acceder a los modos de almacenamiento cambiando a la vista Modelo, seleccionando una tabla de datos y en el panel Propiedades resultante, seleccionando qué modo desea usar en la lista desplegable Modo de almacenamiento, como se muestra en el siguiente objeto visual.

**Import mode**
El modo Importar le permite crear una copia local de Power BI de los conjuntos de datos desde el origen de datos. Sin embargo, las actualizaciones de datos deben realizarse manualmente. El modo de importación es el valor predeterminado para crear nuevos informes de Power BI.

**DirectQuery mode**

La opción DirectQuery es útil cuando no desea guardar copias locales de los datos porque los datos no se almacenarán en caché. 
En su lugar, puede consultar las tablas específicas que necesitará mediante **consultas nativas de Power BI** y los datos necesarios se recuperarán del origen de datos subyacente. Esencialmente, está creando una **conexión directa con el origen de datos**. El uso de este modelo garantiza que siempre esté viendo los datos más actualizados y que se cumplan todos los requisitos de seguridad. Además, este modo es adecuado para cuando tiene conjuntos de datos grandes de los que extraer datos. En lugar de ralentizar el rendimiento al tener que cargar grandes cantidades de datos en Power BI, también puede usar DirectQuery para crear una conexión con el origen, resolviendo también problemas de latencia de datos.


**Dual (modo compuesto)**

En el modo Dual, puede identificar algunos datos que se importarán directamente y otros datos que se deben consultar. Cualquier tabla que se trae al informe es un producto de los modos Import y DirectQuery. El uso del modo Dual permite a Power BI elegir la forma más eficiente de recuperación de datos.

Para obtener más información sobre los modos de almacenamiento, consulte [Modos de almacenamiento](https://docs.microsoft.com/en-us/power-bi/transform-model/desktop-storage-mode/).

<img src="https://docs.microsoft.com/en-us/power-bi/transform-model/media/desktop-storage-mode/storage-mode-02.png" alt="descargar" border="0" width=600px>



## Get data from Azure Analysis Services
_Obtenga datos de Azure Analysis Services_

Azure Analysis Services Es un producto de Azure que le permite ingerir datos de varios orígenes de datos, crear relaciones entre los datos y crear cálculos en los datos. 
Los cálculos se crean mediante expresiones de análisis de datos (DAX). Azure Analysis Services Es similar a la tecnología de modelado y almacenamiento de datos de Power BI.

Tailwind Traders usa Azure Analysis Services para almacenar datos de proyección financiera. Se le ha pedido que compare estos datos con datos de ventas reales en una base de datos diferente. Obtener datos de cubos de Azure Analysis Services Es similar a obtener datos de SQL ServerSQL Server, ya que puede:

- Autentique al servidor.
- Elige el cubo que quieras usar.
- Seleccione las tablas que necesita.

Las diferencias notables entre los cubos de Azure Analysis Services y SQL ServerSQL Server son:

- Los cubos de Analysis ServicesAnalysis Services ya tienen cálculos en el cubo, que se discutirán con más detalle más adelante.
- Si no necesita una tabla completa, puede consultar los datos directamente. En lugar de usar Transact-SQLTransact-SQL (T-SQL) para consultar los datos, como lo haría en SQL ServerSQL Server, puede usar expresiones multidimensionales (MDX) o expresiones de análisis de datos (DAX).

**Connect to data in Azure Analysis Services**

Como se mencionó anteriormente, use la característica Obtener datos en Power BI Desktop. Al seleccionar Analysis ServicesAnalysis Services, se le pedirá la dirección del servidor y el nombre de la base de datos con dos opciones: Importar y conectar en vivo.

Conectar en vivo es una nueva opción en Azure Analysis Services. 
Azure Analysis Services Usa el modelo tabular y DAX para compilar cálculos, similares a Power BI. 
Estos modelos son compatibles entre sí.

El uso de la opción Conectar en vivo le ayuda a mantener los datos y los cálculos DAX en su ubicación original, sin tener que importarlos todos a Power BI. Azure Analysis Services puede tener una programación de actualización rápida, lo que significa que cuando los datos se actualizan en el servicio, los informes de Power BI se actualizarán inmediatamente, sin necesidad de iniciar una programación de actualización de Power BI. Este proceso puede mejorar la puntualidad de los datos del informe.

De forma similar a una base de datos relacional, puede elegir las tablas que desea usar. Si desea consultar directamente el modelo de Azure Analysis Services, puede usar DAX o MDX.

Es probable que importe los datos directamente en Power BI. Una alternativa aceptable es importar todos los demás datos que desee (desde Excel, SQL Server, etc.) en el modelo de Azure Analysis Services y, a continuación, usar una conexión en vivo. Con este enfoque, el modelado de datos y las medidas DAX se realizan en un solo lugar, y es una forma mucho más sencilla de mantener la solución.

Para obtener más información sobre cómo conectar Power BI a Azure Analysis Services, consulte La [documentación de Conectar con Power BI](https://docs.microsoft.com/en-us/azure/analysis-services/analysis-services-connect-pbi/).

## Fix performance issues
_Solucionar problemas de rendimiento_

Ocasionalmente, las organizaciones tendrán que abordar los problemas de rendimiento al ejecutar informes. Power BI proporciona la herramienta Analizador de rendimiento para ayudar a solucionar problemas y optimizar el proceso.

Tenga en cuenta el escenario en el que está creando informes para el equipo de ventas de la organización. Ha importado los datos, que se encuentran en varias tablas dentro de la base de datos SQL del equipo de ventas, creando una conexión de datos a la base de datos a través de DirectQuery. Al crear objetos visuales y filtros preliminares, observa que algunas tablas se consultan más rápido que otras y algunos filtros tardan más en procesarse en comparación con otras.

**Optimizar el rendimiento en Power Query**
El rendimiento de Power Query depende del rendimiento en el nivel de origen de datos. 
La variedad de orígenes de datos que ofrece Power Query es muy amplia y las técnicas de ajuste del rendimiento para cada origen son igualmente amplias. 

Por ejemplo, si extrae datos de un Microsoft SQL Server, debe seguir las directrices de ajuste del rendimiento del producto. Las buenas técnicas de ajuste del rendimiento de SQL ServerSQL Server incluyen creación de índices, actualizaciones de hardware, ajuste del plan de ejecución y compresión de datos. Estos temas están fuera del ámbito aquí y se tratan solo como un ejemplo para crear familiaridad con el origen de datos y cosechar las ventajas al usar Power BI y Power Query.

Power Query aprovecha un buen rendimiento en el origen de datos a través de una técnica denominada Plegado de consultas.

### **Plegado de consultas**
El plegado de consultas dentro del Editor de consultas de energía le ayuda a aumentar el rendimiento de los informes de Power BI. El plegado de consultas es el proceso mediante el cual se realiza el seguimiento de las transformaciones y ediciones que realice en power query editor como consultas nativas o instrucciones SQL selectas simples, mientras realiza transformaciones de forma activa. La razón para implementar este proceso es asegurarse de que estas transformaciones pueden tener lugar en el servidor de origen de datos original y no abrumar los recursos informáticos de Power BI.

Puede usar Power Query para cargar datos en Power BI. Con power query editor, puede realizar más transformaciones en los datos, como cambiar el nombre o eliminar columnas, anexar, analizar, filtrar o agrupar los datos.

Considere un escenario en el que ha cambiado el nombre de algunas columnas en los datos de ventas y ha combinado una columna de ciudad y estado en el formato "estado de la ciudad". Mientras tanto, la función de plegado de consultas realiza un seguimiento de esos cambios en las consultas nativas. A continuación, al cargar los datos, las transformaciones tienen lugar de forma independiente en el origen original, lo que garantiza que el rendimiento esté optimizado en Power BI.

Los beneficios para el plegado de consultas incluyen:

- Más eficiencia en las actualizaciones de datos y actualizaciones incrementales. Al importar tablas de datos mediante el plegado de consultas, Power BI puede asignar recursos y actualizar los datos más rápido porque Power BI no tiene que ejecutarse a través de cada transformación localmente.

- Compatibilidad automática con los modos de almacenamiento DirectQuery y Dual. Todos los orígenes de datos de modo de almacenamiento DirectQuery y Dual deben tener las capacidades de procesamiento del servidor back-end para crear una conexión directa, lo que significa que el plegado de consultas es una capacidad automática que puede usar. Si todas las transformaciones se pueden reducir a una sola instrucción Select, puede producirse el plegado de consultas.

En el siguiente escenario se muestra el plegado de consultas en acción. En este escenario, se aplica un conjunto de consultas a varias tablas. Después de agregar un nuevo origen de datos mediante Power Query y dirigirse al Editor de consultas de energía, vaya al panel Configuración de consulta y haga clic con el botón derecho en el último paso aplicado, como se muestra en la siguiente ilustración.

Una buena guía para recordar es que si puede traducir una transformación en una instrucción Select SQL, que incluye operadores y cláusulas como GROUP BY, SORT BY, WHERE, UNION ALL y JOIN, puede usar el plegado de consultas.

Aunque el plegado de consultas es una opción para optimizar el rendimiento al recuperar, importar y preparar datos, otra opción son los diagnósticos de consultas.

### **Diagnóstico de consultas**

Usar para estudiar el rendimiento de las consultas son los diagnósticos de consultas. 
Esta característica le permite determinar qué cuellos de botella (si los hay) existen al cargar y transformar los datos, actualizar los datos en Power Query, ejecutar instrucciones SQL en el Editor de consultas, etc.

Para acceder a los diagnósticos de consultas en el Editor de consultas de energía, vaya a Herramientas en la cinta de opciones Inicio. Cuando esté listo para comenzar a transformar los datos o realizar otras ediciones en power query editor, seleccione Iniciar diagnósticos en la pestaña Diagnósticos de sesión. Cuando haya terminado, asegúrese de seleccionar Detener diagnóstico.

<img src="https://docs.microsoft.com/en-us/learn/modules/get-data/media/8-navigating-query-diagnostics-ss.png#lightbox" alt="descargar" border="0" width=600px>

Al seleccionar Diagnosticar paso se muestra el tiempo que se tarda en ejecutar ese paso, como se muestra en la siguiente imagen. Esta selección puede indicarle si un paso tarda más en completarse que otros, lo que sirve como punto de partida para una investigación adicional.

Esta herramienta es útil cuando desea analizar el rendimiento en el lado de Power Query para tareas como cargar datasets, ejecutar actualizaciones de datos o ejecutar otras tareas transformadoras.

**Otras técnicas para optimizar el rendimiento**
Otras formas de optimizar el rendimiento de las consultas en Power BI incluyen:

- Procese tantos datos como sea posible en el origen de datos original. Power Query y Power Query Editor le permiten procesar los datos; sin embargo, la potencia de procesamiento necesaria para completar esta tarea podría reducir el rendimiento en otras áreas de los informes. Por lo general, una buena práctica es procesar, tanto como sea posible, en el origen de datos nativo.

- Use consultas SQL nativas. Cuando utilice DirectQuery para bases de datos SQL, como el caso de nuestro escenario, asegúrese de que no va a extraer datos de procedimientos almacenados o expresiones comunes de tabla (CTEs).

- Fecha y hora separadas, si están enlazadas. Si alguna de las tablas tiene columnas que combinan fecha y hora, asegúrese de separarlas en columnas distintas antes de importarlas a Power BI. Este enfoque aumentará las habilidades de compresión.

Para obtener más información, consulte [Guía de plegado de consultas](https://docs.microsoft.com/en-us/power-bi/guidance/power-query-folding/) y [Plegado de consultas](https://docs.microsoft.com/en-us/power-query/power-query-folding/).