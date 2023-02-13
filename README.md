# MIAD-VyS
David Ruiz repository for MIAD courses
Visualización y Storytelling - MIAD
Tablero de control: Diversidad de salarios
David Mauricio Ruiz Ayala

1. Fenómeno
Con la intención de conocer información sobre el dinero que ganan las personas a lo largo del mundo, en la página www.askamanager.org se creó un formulario abierto que permite a las personas responder algunas preguntas sobre el ingreso que obtienen por su trabajo y algunas variables relacionadas con el mismo:
https://www.askamanager.org/2021/04/how-much-money-do-you-make-4.html
De la misma manera, los resultados se pueden obtener de forma libre en el siguiente enlace:
https://docs.google.com/spreadsheets/d/1IPS5dBSGtwYVbjsfbaMCYIWnOuRmJcbequohNxCyGVw/edit?resourcekey#gid=1625408792

2. Datos crudos
Inicialmente, se descargó la base de datos crudos del enlace mencionado. Se descargó en dos formatos: una versión .xlsx y una versión .csv. Inicialmente trabajamos en Excel con la versión xlsx ya que nos permite observar con relativa facilidad el tipo de variables, la cantidad y el estilo de los registros en cada variable. Al revisar la base en formato .xlsx encontramos un total de 27.936 registros y 17 variables, a saber:
Nombre	Tipo	Descripción	Registros vacíos
1. How old are you?	Categórico –
Intervalo numérico	Los encuestados pueden elegir un intervalo en el que se encuentra su edad, en años. (< 18, 18 a 24, 25 a 34, 35 a 44, 45 a 54, 55 a 64 y 65+).	0
2. What industry do you work in?	Texto libre	Los encuestados pueden escribir de manera libre el sector en el que trabajan, por lo que es posible encontrar respuestas con distintos niveles de generalidad.	70
3. Job title	Texto libre	Los encuestados describen el título de su trabajo de manera libre, por lo que se tiene más de 10.000 respuestas distintas.	0
4. If your job title needs additional context, please clarify here	Texto libre	Los encuestados pueden complementar la respuesta a la anterior pregunta. Es posible que esta variable no se considere en la fase de modelado por tener tantos datos vacíos.
	20.708
5. What is your annual salary?	Numérico –
Moneda	Los encuestados escriben su salario anual en términos nominales (sin incluir la moneda en la que reciben el salario).	0
6. How much additional monetary compensation do you get, if any	Numérico – Moneda	Los encuestados escriben las compensaciones adicionales al salario que reciben de manera anual.	7.251
7. Please indicate the currency	Categórico –
Texto	Los encuestados indican la moneda en la que reciben su salario y sus compensaciones. No hay registros vacíos, pero si hay 156 registros “Other”, registros que posiblemente no se tengan en cuenta en el modelado.	0
8. If "Other," please indicate the currency here	Texto libre	Los encuestados que eligen “Other” en la pregunta anterior pueden escribir el tipo de moneda en el que reciben su salario y sus compensaciones.	27.732
9. If your income needs additional context, please provide it here	Texto libre	Los encuestados pueden escribir información adicional como complemento de la respuesta brindada en la variable 6.	24.893
10. What country do you work in?	Texto libre – 
Geográfico	Los encuestados pueden escribir libremente el país en el que trabajan. No hay registros vacíos, pero se observan algunas respuestas incoherentes.
	0
11. If you're in the U.S., what state do you work in?	Texto libre – Geográfico
	Los encuestados que eligieron Estados Unidos (en sus distintas versiones de escritura) pueden escribir el estado en el que trabajan.	4.400
12. What city do you work in?	Texto libre – 
Geográfico	Los encuestados pueden escribir la ciudad en la que trabajan.	9
13. How many years of professional work experience do you have overall?	Categórico –
Intervalo numérico
	Los encuestados pueden elegir el intervalo en el que se ubica el número de años de experiencia profesional total (1 año o menos, 2 a 4 años, 5 a 7 años, 8 a 10 años, 11 a 20 años, 21 a 30 años, 31 a 40 años, 41 años o más).	0
14. How many years of professional work experience do you have in your field?	Categórico –
Intervalo numérico	Los encuestados pueden elegir el intervalo en el que se ubica el número de años de experiencia profesional en su campo (1 año o menos, 2 a 4 años, 5 a 7 años, 8 a 10 años, 11 a 20 años, 21 a 30 años, 31 a 40 años, 41 años o más).	0
15. What is your highest level of education completed?	Categórico –
Texto	Los encuestados pueden elegir la categoría del grado de educación formal completada más alto (College, Highschool, professional, Masters, PhD).	195
16. What is your gender?:	Categórico –
Texto	Los encuestados pueden elegir el género con el que se identifican (Man, Woman, Non-Binary, Other or prefer not answer).	156
17. What is your race? (Choose all that apply.):	Texto libre	Los encuestados pueden elegir la raza a la que pertenecen.	163

Modelado de datos
A partir de la base de datos original, y teniendo en cuenta que algunas variables ofrecen respuestas libres, realizaremos las siguientes transformaciones para obtener una base de datos acorde con los objetivos que queremos plantear para la fase del storytelling.
Paso 1. Para la variable 2 (What industry do you work in?), eliminaremos los 70 registros vacíos ya que representan una porción muy pequeña de la base (~0.25%).
Paso 2. Se elimina toda la variable 4 (If your job title needs additional context, please clarify here), relacionada con respuestas complementarias a la pregunta por el título del trabajo, porque alrededor del 78% de los registros son vacíos y no se planea realizar análisis sobre estas respuestas.
Paso 3. Eliminamos los registros que quedan con respuesta “Other” en la variable 7 (Please indicate the currency) pues la cantidad de registros es muy pequeña (~0.5%) por lo que no sería adecuado realizar inferencias o identificar tendencias con una cantidad tan pequeña de datos.
Paso 4. Eliminamos la variable 8, en la que se especificaba el tipo de moneda cuando se eligió en la pregunta anterior “Other”) pues como se mencionó, no se planea realizar análisis sobre estas monedas adicionales.
Paso 5. Se elimina toda la variable 9 (If your income needs additional context, please provide it here), relacionada con respuestas para complementar la respuesta de los ingresos (salario y compensaciones) pues alrededor del 89% de los registros son vacíos y no se planea realizar análisis sobre estas respuestas.
Paso 6. En este paso, el más importante de la fase de modelado, nos centraremos en unificar las respuestas a la pregunta de la variable 10 (What country do you work in?):
	Inicialmente eliminamos 64 registros que obedecen a respuestas incoherentes (valores numéricos, letras solas, continentes, etc).
	Ajustamos manualmente el nombre de países con múltiples escrituras o con errores de escritura (Australia, Canada, England, United States, Germany, Hong Kong, etc). Se decidió realizar el ajuste manualmente pues la cantidad de registros no es extremadamente alta y se puede analizar otras respuestas a preguntas distintas, p. ej. de la variable 12 (City),  para tomar una decisión de ajuste, análisis que sería más complejo de programar para que lo realice una máquina.
	Un caso particular que requirió un esfuerzo adicional fue la identificación del país (Country) para aquellos casos en los que la respuesta fue Reino Unido (United Kingdom) en cualquier de sus posibles versiones de escritura. La distinción entre Inglaterra (England), Escocia (Scotland), Irlanda (Ireland), Gales (Wales) e Irlanda del Norte (Northern Ireland) requirió analizar las respuestas a la pregunta de la variable 12 (City), en algunos casos de manera casi que individual.
Al terminar este filtrado y ajuste a la respuesta de la variable 10 (Country), quedan 27.644 registros en la base.
Paso 7. Se decide unificar las respuestas de la variable 11 (If you're in the U.S., what state do you work in?) asociados a los estados en los que trabajan aquellas personas que respondieron Estados Unidos (United States) como país de trabajo (variable 10).
	Se verifica que hayan elegido Estados Unidos como respuesta.
	Se ajustan posibles respuestas similares para evitar distintos tipos de escritura.
	Se eliminan registros con respuestas múltiples, i.e, varios estados.
	Se diligencia el estado para aquellos registros vacíos que hayan respondido Estados Unidos utilizando la respuesta de la variable 12 (City) como guía.
En total, se eliminan 24 registros con respuestas múltiples que no permiten identificar el estado o con respuestas de Country distintas a Estados Unidos.
Paso 8. Se decide mantener la variable 12 (What city do you work in?) sin eliminar los registros vacíos, pues no representa una porción grande de los datos. Sin embargo, se considera poco probable que se realice un análisis de estas respuestas pues la limpieza de los datos podría tomar un tiempo prologando y recursos computacionales.
Paso 9. Se mantiene sin transformaciones las respuestas de las variables 13 (How many years of professional work experience do you have overall?) y 14 (How many years of professional work experience do you have in your field?).
Paso 10. Para la variable 15 (What is your highest level of education completed?), se eliminan los registros vacíos que corresponden aproximadamente al 0,5% de los registros totales.
Paso 11. Para las variables 16 (What is your gender?) y 17 (What is your race? (Choose all that apply.)) se decide mantener los registros vacíos, aun cuando es posible que no se realicen análisis para estas variables.
Paso 12. A continuación, se crean las siguientes variables:
	Salario COP: resultado de multiplicar la variable Annual Salary por el valor de la tasa de cambio del 12 de febrero de 2023, para cada uno de los distintos tipos de moneda, y convertir este valor a millones de pesos colombianos (COP).
	Compensaciones COP: resultado de multiplicar la variable Additional monetary compensation por el valor de la tasa de cambio del 12 de febrero de 2023, para cada uno de los distintos tipos de moneda, y convertir este valor a millones de pesos colombianos (COP).
	Ingresos COP: resultado de sumar las variables Salario COP y Compensaciones COP.
Nota 1: Para las 3 variables creadas anteriormente, la unidad de medida será millones de pesos colombianos con la intención de que la visualización sea más amigable.
Nota 2: Las tasas de cambio utilizadas para el 12 de febrero de 2023 son:
Moneda	Tasa de cambio
AUD/NZD	3288,42
CAD	3560,6
CHF	5143,81
EUR	5075,6
GBP	5732,42
HKD	605,51
JPY	36,15
SEK	454,97
USD	4753,4
ZAR	264,93

Paso 13. Como filtro final, se eliminarán los registros que tienen un valor menor o igual que 10 en la variable Ingresos COP, por ser valores extremadamente bajos para la realidad. Adicionalmente, se elimina un registro que aparece en USD pero parece estar originalmente en COP, generando un valor extremadamente alto en las 3 variables creadas. De esta manera, se eliminan 76 registros.
Después de realizar todas las transformaciones mencionadas, la base de datos final tendrá 27.334 registros y 17 variables. Las variables serán renombradas al español y quedarán así:
Nombre	Tipo	Descripción	Registros vacíos
1. Edad	Categórico –
Intervalo numérico	Los encuestados pueden elegir un intervalo en el que se encuentra su edad, en años. (< 18, 18 a 24, 25 a 34, 35 a 44, 45 a 54, 55 a 64 y 65+).	0
2. Industria	Texto libre	Los encuestados pueden escribir de manera libre el sector en el que trabajan, por lo que es posible encontrar respuestas con distintos niveles de generalidad.	0
3. Trabajo	Texto libre	Los encuestados describen el título de su trabajo de manera libre, por lo que se tiene más de 10.000 respuestas distintas.	0
4. Salario original	Numérico –
Moneda	Los encuestados escriben su salario anual en términos nominales (sin incluir la moneda en la que reciben el salario).	0
5. Compensaciones originales	Numérico –
Moneda	Los encuestados escriben las compensaciones adicionales al salario que reciben de manera anual.	7.036
6. Moneda	Categórico –
Texto	Los encuestados indican la moneda en la que reciben su salario y sus compensaciones.	0
7. País trabajo	Texto libre – 
Geográfico	Los encuestados pueden escribir libremente el país en el que trabajan	0
8. Estado trabajo	Texto libre – Geográfico	Los encuestados que eligieron Estados Unidos (en sus distintas versiones de escritura) pueden escribir el estado en el que trabajan.	4.580
9. Ciudad trabajo	Texto libre – 
Geográfico	Los encuestados pueden escribir la ciudad en la que trabajan.	9
10. Experiencia trabajo	Categórico –
Intervalo numérico
	Los encuestados pueden elegir el intervalo en el que se ubica el número de años de experiencia profesional total (1 año o menos, 2 a 4 años, 5 a 7 años, 8 a 10 años, 11 a 20 años, 21 a 30 años, 31 a 40 años, 41 años o más).	0
11. Experiencia campo	Categórico –
Intervalo numérico	Los encuestados pueden elegir el intervalo en el que se ubica el número de años de experiencia profesional en su campo (1 año o menos, 2 a 4 años, 5 a 7 años, 8 a 10 años, 11 a 20 años, 21 a 30 años, 31 a 40 años, 41 años o más).	0
12. Nivel educativo	Categórico –
Texto	Los encuestados pueden elegir la categoría del grado de educación formal completada más alto (College, Highschool, professional, Masters, PhD).	0
13. Género	Categórico –
Texto	Los encuestados pueden elegir el género con el que se identifican (Man, Woman, Non-Binary, Other or prefer not answer).	128
14. Raza	Texto libre	Los encuestados pueden elegir la raza a la que pertenecen.	121
15. Salario COP	Numérico – 
Moneda	A partir de las respuestas se calcula el salario que reciben los encuestados, en millones de pesos colombianos.	0
16. Compensaciones COP	Numérico – 
Moneda	A partir de las respuestas se calcula el dinero recibido como compensaciones que reciben los encuestados, en millones de pesos colombianos.	0
17. Ingresos COP	Numérico – 
Moneda	A partir de las variables Salario COP y Compensaciones COP, se suman para obtener la cantidad de ingresos, en millones de pesos colombianos, que reciben los encuestados por su trabajo.	0

Creación del tablero de control
Para crear el tablero de control que nos permita realizar una exploración de los datos que se han modelado, según la propuesta de Tukey, se realizó lo siguiente.
Paso 1. Se cargó la base de datos en formato .csv a Hojas de cálculo de Google con el nombre de IML_Ask A Manager Salary Survey 2021 (Responses)_ModeladoFinal_DR_MIAD.
Paso 2. Se creó un nuevo informe en Looker Studio, se cargó la hoja de cálculo del paso 1. El informe se nombró Diversidad de salarios - David Ruiz - VyS – MIAD.
Paso 3. Se ajustaron los tipos de variables según la tabla presentada en el apartado de Modelación de los datos (numéricas, geográficas, texto, etc.).
Paso 4. Para satisfacer las condiciones del tablero de control, se crearon 4 módulos:
	Módulo 1. Contador básico de respuestas.
Se incluyó un cuadro de resultados que contabiliza la cantidad total de registros que tiene la base de datos. Este contador se podrá ver afectado por los controles y filtros que se agregarán en los siguientes módulos.
Módulo 2. Mapa de burbujas por países.
Se incluyó un mapa de burbujas que permite identificar los países en los que hay mayor cantidad de encuestados. Las comparaciones se pueden realizar por tamaño de las burbujas y el contraste del color. Adicionalmente, se podrá seleccionar un país en particular para conocer el conteo total de encuestados de dicho país. Esta selección afectará los demás módulos construidos.
Módulo 3. Relación del salario promedio por industria.
Para poder hacer análisis exploratorio y buscar tendencias y relaciones entre el salario promedio y la industria a la que pertenecen los encuestados, se agregaron dos controles: Industria y País. De esta manera, podremos elegir las categorías de industrias que queremos analizar. Una vez elegidas las categorías, podremos observar el salario promedio, compensaciones promedio e ingresos promedio (en COP). De la misma manera, se podrá elegir un país para hacer el respectivo análisis.
Módulo 4. Otros análisis
Para analizar algunas de las otras variables de la base de datos considerada, se incluyó
	Una gráfica de tendencia que permite analizar la variación del ingreso promedio a medida que los encuestados tienen una mayor cantidad de años de experiencia en total. Se agregaron métricas opcionales (salario promedio, compensaciones promedio) para elegir aquella con la que se quieran hacer las comparaciones.
	Una gráfica de barras que permite analizar la variación del ingreso promedio según el nivel educativo alcanzado por los encuestados. Se agregaron métricas opcionales (salario promedio, compensaciones promedio) para elegir aquella con la que se quieran hacer las comparaciones.
	Una gráfica de rectángulos que permite comparar el ingreso promedio según el género de los encuestados. Se agregaron métricas opcionales (salario promedio, compensaciones promedio) para elegir aquella con la que se quieran hacer las comparaciones.

Notas adicionales
	La estética del tablero de control es básica, pues tiene como objetivo la comunicación a nosotros mismos, es decir, sirve para trabajo interno del equipo que realizará la fase de análisis exploratorio de los datos.
	El enlace al tablero de control es:
https://lookerstudio.google.com/reporting/a0f1749c-9a74-4909-a615-7301fa536435
	El enlace a la base de datos modelados es:

https://docs.google.com/spreadsheets/d/1UVMjgV-2M_Os6pKPOexGM0WG2cYCnebKTFnkrAN3sak/edit?usp=sharing



