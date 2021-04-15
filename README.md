# analisis_distribuidores
Análisis integral del desempeño de un conjunto de distribuidores en base a diversas variables y utilizando diferentes técnicas.

Este trabajo es principalmente descriptivo/iferencial. Pero ha sido utilizado para tomar decisiones estratégicas sobre el potencial accionar futuro de diversos conjuntos de distribuidores. Por ende, aunque no incluye técnicas predictivas formales, podría decirse que sí implica un aspecto prospectivo. 

PASO 1: Los datos y la limpieza

Las fuentes de datos para este análisis son diversas y la mayoría permanece almacenada en hojas de cálculo. Algunas otras, aunque provienen de un sistema transaccional, fueron editadas tambien en Excel para un análisis previo, por lo que se utilizaron las mismas fuentes. La transformación y limpieza consiste simplemente en unificar las diversas fuentes (las que contienen información por transacción), y generar agregados priemro por clientes y luego por distribuidores. Para ello, además, se agregan diversos datos que caracterizan a los clientes o a los distribuidores, dependiendo el nivel de agregación necesario. La incorporación de atributos a nivel distribuidor incluye una variables de georreferenciación (latitud y longitud) que se calcula como la mediana de las coordenadas de los clientes que realizaron compras en cada distribuidor; para ello se utiliza la librería Geopy.

PASO 2: Clústers

Para conocer posibles agrupaciones "naturales" entre los diferentes distribuidores se construyeron clústers a partir de cinco variables: El volumen de ventas, el crecimiento interanual actual, un indicador de crecimiento histórico, el promedio de ventas por cliente (o ticket promedio) y la cantidad de clientes nuevos. Para ello se utilizó la metodología de Kmeans incluida en la librería sklearn.

PASO 3: Análisis Gráfico

La indagación a partir de gráficos resultó central para encontrar las primeras relaciones. Se generaron diagramas de dispersión (scatters) para encontrar posibles efectos de diversas variables sobre eldesempeño de los distribuidores. Además, se trató de diferenciar estos efectos según la zona de influencia de cada uno (la que podía ser grande (1) o pequeña (2) y por los clústers antes generados. 

PASO 4: Regresión lineal múltiple

Para formalizar ciertas relaciones encontradas y terminar de confirmar su existencia, se estimó una regresión lineal múltiple entre la variable dependiente (desempeño actual) y las independientes (desempeño pasado, promedio de ventas). Para esto se empleó el módulo linear_model dentro de sklearn.

PASO 5: la geografía

Para seguir indagando más efectos y relaciones potenciales, se incorporó el aspecto geográfico. Primeramente se graficaron todas las coordenadas medianas de cada distribuidor en un mapa y se observó alguna relación del desempeño con la latitud de dichos puntos. Para confirmar esta relación, se incorporó al modelo de regresión la variable latitud como explicativa, obteniendo resultados satisfactorios.

PASO 6: el desempeño pasado

Dado que el desempeño pasado de los distribuidores tenía un peso importante en la explicación del desempeño presente, se procedió a buscar alguna explicación de las disparidades pasadas. Para ello se recurrio a variables que incorporaran diversos porcentajes de clientes que tuviera cada distribuidor. En este caso, se encontraron relaciones con el porcentaje de clientes nuevos a los que hubieran accedido los distribuidores (relación postiva) y al porcentaje de clientes "históricos" (relación negativa)
