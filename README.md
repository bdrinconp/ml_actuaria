# Proyecto: Chain Ladder

## 1. Contexto
### 1.1 ¿Qúe es Chain Ladder? 
Chain Ladder es una técnica utilizada con frecuencia en la industria aseguradora. Esta metodología se emplea para **prever** la cantidad de dinero que una compañía de seguros necesitará reservar para cubrir futuras reclamaciones, basándose en el comportamiento histórico de los datos disponibles relacionados con **reclamaciones pasadas**.

Como descripción general de la técnica, Chain Ladder toma como referencia los datos asociados a reclamaciones de períodos anteriores. Con base en estos datos, se realiza la estimación (o predicción) de las reclamaciones futuras que podrían surgir. Es importante tener en cuenta que estas reclamaciones futuras pueden provenir de dos fuentes:

1. Siniestros incurridos pero no reportados (Incurred But Not Reported, IBNR): En este caso, se intenta estimar las pérdidas asociadas a siniestros que ya han ocurrido pero que aún no han sido reportados a la compañía aseguradora.

3. Siniestros que aún no se han resuelto: Corresponde a siniestros que ya están bajo el dominio de la compañía aseguradora, pero que, debido a su complejidad, aún se encuentran en estudio y eventualmente se deberá incurrir en pagos futuros.

La esencia de la metodología Chain Ladder está fundamentada en la idea de que las reclamaciones de un año en particular suelen desarrollarse de forma similar a las de años anteriores.

**Pasos básisos para aplicar Chain Ladder:**
- Crear un triángulo de pérdidas: Los datos históricos se organizan en un triángulo en el que cada fila representa un año de origen de las reclamaciones, y cada columna representa un período de tiempo acumulativo desde ese año de origen.
![image](https://github.com/bdrinconp/ml_actuaria/assets/63571645/60ea937c-0332-4616-b549-7623a4f454f1)

- Calcular factores de desarrollo: Para cada par de años consecutivos dentro de una fila, se calcula un factor de desarrollo, que es la razón entre las pérdidas acumuladas en el año más reciente y las pérdidas acumuladas en el año anterior.

![image](https://github.com/bdrinconp/ml_actuaria/assets/63571645/c9dc859b-f9f5-40c4-87ce-e83341c160a6)

- Promediar factores de desarrollo: Se toma un promedio de los factores de desarrollo para cada columna con el fin de estimar cómo se desarrollarán las pérdidas en el futuro.

- Proyectar pérdidas futuras: Utilizando los factores de desarrollo promedio, se proyectan las pérdidas futuras para cada año de origen y se suman para obtener el total de la reserva necesaria.

La metodología Chain Ladder es popular y está ampliamente adoptada por compañías aseguradoras; sin embargo, tiene ciertas limitaciones. Por ejemplo, asume que los patrones de desarrollo de las pérdidas en el pasado son un buen predictor de los patrones futuros, lo cual no es necesariamente correcto. Además, es sensible a variaciones en los datos, lo que puede afectar las estimaciones.

Con base en lo anterior, es importante explorar otras técnicas que permitan abordar de forma más robusta el problema asociado con la estimación de los factores de desarrollo. Esto es esencial para prever futuras pérdidas y, por ende, determinar la cantidad de dinero que la compañía de seguros debería reservar.

### 1.2 Chain Ladder y la industria aseguradora
Las compañías aseguradoras enfrentan diversos desafíos relacionados con la gestión de riesgos y la estimación de pasivos futuros, especialmente en seguros generales. Como se mencionaba anteriormente, uno de los principales retos está asociado con la determinación adecuada del dinero que se debe reservar para hacer frente a futuras reclamaciones o siniestros.

Los seguros generales se enfocan particularmente en seguros de propiedad, seguros patrimoniales, seguros de auto, cumplimiento y microseguros, entre otros. En muchos casos, estos seguros ofrecen cobertura a terceros que resulten afectados por las acciones del asegurado. Esto se conoce como cobertura o seguro de responsabilidad civil (liability). En general, las coberturas de responsabilidad civil poseen un desarrollo a largo plazo, dado que pueden tardar mucho tiempo en resolverse. Esto implica que hay un lapso importante de tiempo entre el momento en que ocurre el siniestro y cuando finalmente se resuelve o se paga. Debido a esta complejidad en la estimación de las reservas necesarias, Chain Ladder es frecuentemente utilizado para esta tarea.

### 1.3 Responsabilidad Civil 
Un aspecto importante a considerar en el ramo de responsabilidad civil se expone en Nieto y Tamayo (2018), donde se indica: "En particular, en negocios como vida individual, gastos médicos, responsabilidad civil, etc., la evolución del reporte de los siniestros es estacional". Teniendo en cuenta lo anterior, se podría pensar que bajo ciertos escenarios, la característica de estacionalidad es positiva y beneficia la implementación de Chain Ladder. Sin embargo, aunque la estacionalidad puede entenderse como un tipo de patrón, no necesariamente implica mejores condiciones para la implementación de Chain Ladder. Por lo tanto, puede requerirse el ajuste de modelos para capturar de forma precisa estos patrones estacionales.

## 2. Entendimiento de negocio
### 2.1 Objetivos de negocio
#### 2.1.1 Objetivo general
Optimizar la asignación de recursos financieros en la compañía aseguradora mediante la mejora de la precisión en la estimación de reservas para siniestros en el ramo de responsabilidad civil.
#### 2.1.2 Objetivos especificos
1. Identificar las limitaciones y áreas de mejora en el proceso actual de estimación de reservas, con el objetivo de reducir la incertidumbre y el riesgo financiero asociados.
2. Aumentar la eficiencia operativa en la gestión de siniestros a través de un sistema de estimación de reservas más preciso, que permita una asignación de capital más eficaz.
### 2.2 Evaluación de la situación (assess situation)
#### 2.2.1 Inventario de recursos
1. Datos disponibles: Historico de reclamaciones y sus caracteristicas (fechas, movimientos de dinero), detalle de las pólizas e información de los asegurados.
2. Talento humano: Actuarios y analistas de datos.
3. Tecnología: Software especializado para realizar los analisis.
#### 2.2.2 Requisitos, suposiciones y restricciones
1. Requisitos: Cumplimiento con los requerimientos del ente regulador.
2. Suposiciones: La metodologia Chain Ladder actual es suceptible a mejoras.
3. Restricciones: Confidencialidad de los datos.
#### 2.2.3 Terminos y definiciones
1. Reserva: Monto de dinero que la compañia de seguros debe guardar para cubrir siniestros futuros.
2. Siniestro: Reclamaciones que hacen los asegurados a la compañia aseguradora.
3. Ramo de responsabilidad civil (Liability): Tipo de seguro que cubre al asegurado contra reclamaciones de terceros. 
### 2.3 Objetivos de ciencia de datos (Data mining goals)
#### 2.3.1 Objetivo general
Desarrollar y validar un modelo machine learning que mejore la precisión del método Chain Ladder en la proyección de pagos futuros en el ramo de responsabilidad civil.
#### 2.3.2 Objetivos especificos
1.Examinar los datos históricos de siniestros para identificar patrones, correlaciones y posibles outliers que puedan afectar la proyección.
2. Utilizar técnicas de modelado estadístico y machine learning para crear modelos que proyecten con mayor precisión los pagos futuros de siniestros. 
3. Validar los modelos construidos mediante validación cruzada y comparar su rendimiento versus Chain Ladder.
### 2.4 Aproximación al plan del proyecto 
![image](https://github.com/bdrinconp/ml_actuaria/assets/63571645/84b6b539-77cf-4ef4-aa1c-915640cb538f)
#### Entendimiento de negocio
1. Revisar las documentación relacionada con la metodología Chain Ladder y su relación con el ramo de responsabilidad civil.
2. Definición de objetivos de negocio y ciencia de datos.
#### Entendimiento de los datos
1. Recolección de datos a traves de la información disponible en la [CAS](https://www.casact.org/publications-research/research/research-resources/loss-reserving-data-pulled-naic-schedule-p)
2. IDA - exploración inicial de datos
#### Modelado
1. Seleccionar algoritmos de machine laerning apropiados.
2. Definición de la estrategia de entrenamiento y optimización de hiperparametros.
3. Definición de la estrategia de validación.
#### Evaluación
1. Comparar el rendimiento de los modelos vs Chain Ladder
2. Validar cumplimiento de los objetivos de negocio y de ciencia de datos.
#### Implementación
1. Documentar el modelo y los entregables relacionados con los desarrollos.
2. Despliegue del modelo. 
## 3. Datos seleccionados
Los datos seleccionados corresponden a los datos disponibles en [CAS](https://www.casact.org/publications-research/research/research-resources/loss-reserving-data-pulled-naic-schedule-p) tomado como referecia el data set **Product Liability Data Set** y pueden ser consultados en este repositorio en la carpeta **data** archivo  junto con sus respectivos metadatos. 
![image](https://github.com/bdrinconp/ml_actuaria/assets/63571645/b7829ca2-8bc5-46da-812a-ffde5e1a96a3)

## Recursos y referencias
1. [Chain Ladder Method and Example](https://www.bppacted.com/docs/textbook/CAA%20M4%20Textbook%20extract.pdf)
2. [Explained Chain Ladder](https://www.shmoop.com/finance-glossary/chain-ladder-method-clm.html)
3. [Nieto y Tamayo 2018](http://gfnun.unal.edu.co/fileadmin/content/eventos/simposioestadistica/documentos/Simposio_2018/memorias_2018/poster/Comparacion_de_modelos_estocasticos_para_el_calculo_de_la_reserva_IBNR_en_seguros_de_no_vida_-_Maria_Camila_Nieto.pdf)
4. [Aplicación de los métodos Chain-Ladder](https://repositorio.uasb.edu.ec/bitstream/10644/8595/1/T3757-MGFARF-Machado-Aplicacion.pdf)
5. 
6. [Liability Definition](https://www.spanish-translator-services.com/espanol/diccionarios/seguro-ingles-espanol/l/Liability_insurance.html)
