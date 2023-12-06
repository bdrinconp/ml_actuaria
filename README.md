# Chain Ladder
## 0. Video

[Video](https://www.youtube.com/watch?v=h-_AM0u9L0E)

## 1. Contexto

Históricamente, los seguros han acompañado el desarrollo de la humanidad. Los primeros surgieron en la antigüedad, cuando pequeños grupos de personas se unían para protegerse colectivamente de eventos fortuitos e inesperados. Con el tiempo, los seguros han evolucionado y se han convertido en herramientas que ofrecen protección frente a una amplia variedad de riesgos en distintos contextos.

Este avance ha sido impulsado por el desarrollo de la estadística y las matemáticas, lo que permite que los seguros sean objeto de estudios rigurosos. Esta rigurosidad confiere a los seguros un carácter formal y sólido, aspectos especialmente importantes dada su relevancia global. Este nivel de análisis riguroso posibilita que las compañías aseguradoras mantengan la solidez financiera y dispongan de los recursos necesarios para cubrir pérdidas o siniestros, aspectos que tienen un impacto directo en sus asegurados.

Con este contexto en mente, el presente proyecto busca estudiar y proponer una metodología alternativa a la técnica Chain-Ladder. El objetivo de este enfoque es estimar los flujos futuros de dinero necesarios para cubrir pérdidas que han ocurrido, pero aún no se han reportado a la compañía aseguradora.

### 1.1	Sector asegurador

Es importante entender que el sector asegurador está compuesto por diferentes entidades, entre las cuales se encuentran las compañías aseguradoras, los reguladores y otros organismos que participan de forma directa o indirecta en el mercado asegurador, como por ejemplo los reaseguradores. Para cada una de estas entidades, es crucial contar con solidez financiera para cubrir futuras pérdidas. Además, es fundamental conocer la solidez financiera de los otros actores involucrados, ya que la falta de solidez en alguno de ellos podría tener un efecto negativo en toda la red financiera del sector asegurador.

Por otro lado, es importante considerar la estructura interna de las compañías aseguradoras, la cual se organiza en lo que se conoce como 'ramos'. Un ramo es un conjunto de seguros que agrupa riesgos de características similares. Algunos ejemplos de ramos son: ramo de vida, ramo de automóviles, ramo de terremoto o ramo de responsabilidad civil.
En particular este proyecto se concentra en estudiar y analizar las perdidas del ramo de responsabilidad civil (Liability). 

### 1.2 Responsabilidad civil

Los seguros de responsabilidad civil permiten a una persona, conocida como tomador, trasladar a otra entidad, en este caso la aseguradora, el riesgo de ser considerada responsable civilmente por causar daños a un tercero. Por ejemplo, el dueño de una vivienda sería responsable de los daños causados por objetos que pudieran caer o ser arrojados desde la vivienda al exterior, en caso de que esto ocurra el riesgo es cubierto por la compañía aseguradora. 

Desde el enfoque del proyecto, un aspecto importante a considerar en el ramo de responsabilidad civil es expuesto por Nieto y Tamayo (2018), donde se indica: 'En particular, en negocios como vida individual, gastos médicos, responsabilidad civil, etc., la evolución del reporte de los siniestros es estacional'. Teniendo en cuenta esta característica de estacionalidad, es importante considerar aplicar técnicas y modelos que permitan capturar de forma precisa estos patrones estacionales, con el fin de realizar estimaciones más acertadas de las futuras pérdidas.


### 1.3 Metodología Chain-Ladder
Chain Ladder es una técnica utilizada con frecuencia en la industria aseguradora. Esta metodología se emplea para **prever** la cantidad de dinero que una compañía de seguros necesitará reservar para cubrir futuras reclamaciones, basándose en el comportamiento histórico de los datos disponibles relacionados con **reclamaciones pasadas**.

Como descripción general de la técnica, Chain Ladder toma como referencia los datos asociados a reclamaciones de períodos anteriores. Con base en estos datos, se realiza la estimación (o predicción) de las reclamaciones futuras que podrían surgir. Es importante tener en cuenta que estas reclamaciones futuras pueden provenir de dos fuentes:

1. Siniestros incurridos pero no reportados (Incurred But Not Reported, IBNR): En este caso, se intenta estimar las pérdidas asociadas a siniestros que ya han ocurrido pero que aún no han sido reportados a la compañía aseguradora.

3. Siniestros que aún no se han resuelto: Corresponde a siniestros que ya están bajo el dominio de la compañía aseguradora, pero que, debido a su complejidad, aún se encuentran en estudio y eventualmente se deberá incurrir en pagos futuros.

La esencia de la metodología Chain Ladder está fundamentada en la idea de que las reclamaciones de un año en particular suelen desarrollarse de forma similar a las de años anteriores.

**Pasos básisos para aplicar Chain Ladder:**
**- Crear un triángulo de pérdidas:** Los datos históricos se organizan en un triángulo en el que cada fila representa un año de origen de las reclamaciones, y cada columna representa un período de tiempo acumulativo desde ese año de origen.
  
![image](https://github.com/bdrinconp/ml_actuaria/assets/63571645/f8346d7a-3bbd-4c8f-88af-28299d511124)


**- Calcular factores de desarrollo:** Para cada par de años consecutivos dentro de una fila, se calcula un factor de desarrollo, que es la razón entre las pérdidas acumuladas en el año más reciente y las pérdidas acumuladas en el año anterior.

![image](https://github.com/bdrinconp/ml_actuaria/assets/63571645/d11fc7e2-9d70-4e55-a948-1593e47f321f)

**- Promediar factores de desarrollo:** Se toma un promedio de los factores de desarrollo para cada columna con el fin de estimar cómo se desarrollarán las pérdidas en el futuro.

**- Proyectar pérdidas futuras:** Utilizando los factores de desarrollo promedio, se proyectan las pérdidas futuras para cada año de origen y se suman para obtener el total de la reserva necesaria.

La metodología Chain Ladder es popular y está ampliamente adoptada por compañías aseguradoras; sin embargo, tiene ciertas limitaciones. Por ejemplo, asume que los patrones de desarrollo de las pérdidas en el pasado son un buen predictor de los patrones futuros, lo cual no es necesariamente correcto. Además, es sensible a variaciones en los datos, lo que puede afectar las estimaciones.

## Recursos y referencias
1. [Chain Ladder Method and Example](https://www.bppacted.com/docs/textbook/CAA%20M4%20Textbook%20extract.pdf)
2. [Explained Chain Ladder](https://www.shmoop.com/finance-glossary/chain-ladder-method-clm.html)
3. [Nieto y Tamayo 2018](http://gfnun.unal.edu.co/fileadmin/content/eventos/simposioestadistica/documentos/Simposio_2018/memorias_2018/poster/Comparacion_de_modelos_estocasticos_para_el_calculo_de_la_reserva_IBNR_en_seguros_de_no_vida_-_Maria_Camila_Nieto.pdf)
4. [Aplicación de los métodos Chain-Ladder](https://repositorio.uasb.edu.ec/bitstream/10644/8595/1/T3757-MGFARF-Machado-Aplicacion.pdf)
6. [Liability Definition](https://www.spanish-translator-services.com/espanol/diccionarios/seguro-ingles-espanol/l/Liability_insurance.html)
