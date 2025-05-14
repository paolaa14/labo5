A. Fundamento teórico;

Para la practica de laboratorio, fue necesario realizar una invertigación teórica acerca de los siguientes términos:

- En cuanto al sistema autónomo (SNA) es el encargado de controlar funciones involuntarias del cuerpo como la frecuencia cardíaca, la digestión y la respiración. De la misma manera, es importante mencionar que este se divide en simpático (se activa en situaciones de peligro o huida, donde se aumenta la frecuencia cardiaca, se dilatan las pupilas y se reduce la digestión para ahorrar energía, también se redirige la sangre a los músculos, preparándonos para la acción) y el parasimpático (es la parte encargada del descanso, donde, se incrementa la digestión, se contraen las pupilas y se disminuye la frecuencia cardiaca).

- La variabilidad del ritmo cardíaco (VRC) mide cómo fluctúa el tiempo entre cada latido del corazón, mostrando qué tan bien se adapta el sistema nervioso autónomo a diversas situaciones del cuerpo; además, las frecuencias importantes en la VRC son: Frecuencia baja (0. 04 - 0. 15 Hz): Revela la acción conjunta de los sistemas simpático y parasimpático, ligada al control de la presión y otros procesos más pausados. Frecuencia alta (0. 15 - 0. 4 Hz): Vinculada al sistema parasimpático y a la respiración, afectando al ritmo cardíaco en ciclos de respiración acelerada. 
Una VRC alta casi siempre indica buena capacidad de adaptación del sistema autónomo, pero una VRC baja podría sugerir estrés, cansancio o problemas del corazón.

- La transformada wavelet es un método matemático que divide una señal en distintas escalas o frecuencias, facilitando el análisis tanto en el tiempo como en la frecuencia. A diferencia de la transformada de Fourier, que mira frecuencias globales, la transformada wavelet deja ver cómo varían las frecuencias con el tiempo. Aplicaciones en señales biológicas: En ECG, EEG y VRC, ayuda a detectar cambios en la actividad a distintas frecuencias, permitiendo examinar cómo reacciona el cuerpo a estímulos o detectar irregularidades. Tipos de wavelet en señales biológicas: Morlet: Extensa, ideal para señales biológicas como ECG y EEG, ya que posibilita analizar frecuencia y tiempo al mismo tiempo.



Imagen 1, plan de acción para cumplir con el objetivo:
![image](https://github.com/user-attachments/assets/c838b62a-ee88-413c-bdd7-79f4a346ffd9)


Imagen 2, diagrama de flujo que complementa el plan de acción:
se evidencia por partes para mejor visualización del contenido del mismo.

<img width="798![PHOTO-2025-05-13-17-18-06](https://github.com/user-attachments/assets/7093d273-0b0b-4d0c-9af4-df37c1cc0f61)
" alt="Captura de pantalla 2025-05-13 a la(s) 7 28 27 p m" src="https://github.com/user-attachments/assets/f2cc8e0c-6b94-46b4-968d-207af0b6c524" />

<img width="798" alt="Captura de pantalla 2025-05-13 a la(s) 7 28 38 p m" src="https://github.com/user-attachments/assets/fca0c6f4-782b-4a23-8146-a2f2b5713a92" />


<img width="797" alt="Captura de pantalla 2025-05-13 a la(s) 7 28 46 p m" src="https://github.com/user-attachments/assets/f32b8bb3-0a7c-4545-8136-e61d7bc1860d" />



B.Adquisición señal ECG;

Inicialmente, se seleccionó un sujeto de prueba, para medirle la señal electrocardiográfica, el cual no tiene ninguna patología que pueda afectar el resultado de la señal, en la imagen 3 se evidencia al sujeto y adicional la ubicación de los electrodos (el de referencia que esta en la parte inferior que es la parte baja del tórax y los de arriba):

Imagen 3, foto del sujeto: 
![Imagen de WhatsApp 2025-05-13 a las 17 18 06_8be3bb91](https://github.com/user-attachments/assets/96d86a0e-ce74-43e2-9b7e-fab7703eb361)

La señal se tomó durante 5 minutos en reposo, con el fin de evitar el ruido experimental causado por distintos factores como; ropa, cables rozando, etc.

Para leer continuamente la señal ECG, se implementa un código de arduino que llega al pin A0, este código permite enviar los datos al computador a través del puerto serial, el código mencionado es (teniendo en cuenta que es implementando arduino UNO y el sensor ECG);

El código arduino:

void setup() {
  // Iniciar comunicación serial
  Serial.begin(9600);
}

void loop() {
  
 Serial.println(analogRead(A0));
 delay(4);
}

La gráfica de la señal tomada directamente desde el arduino se evidencia a continuación;

Imagen 4, señal ECG original de la matriz;

<img width="857" alt="5min" src="https://github.com/user-attachments/assets/a752db1a-4a2d-4092-8a38-0b2a1d6755fd" />

La imagen 4 muestra la señal del corazón (ECG) tal cual, sacada del sistema antes de limpiarla digitalmente. El tiempo se mide en milisegundos (ms) en la línea horizontal, y la fuerza de la señal en milivoltios (mV) en la línea vertical. Se ven unos 3,5 segundos, mostrando varios latidos completos. 

La señal se ve como un ECG normal, con las partes QRS (sobre todo los picos R) claras y altas, de más de 600 mV, no obstante, también hay anomalías en la línea base y ruido rápido y lento, tal vez por: Movimientos o respiración que la ensucian (cosas lentas) o electricidad que molesta del entorno o del sistema (cosas rápidas). 

Esto es normal en una señal sin filtrar, y por eso hay que limpiarla con filtros digitales. Estos filtros quitan lo que no sirve y mejoran la señal, ayudando a encontrar los picos R y a estudiar cómo cambia el ritmo del corazón (HRV). Además, viendo cómo están los picos R, se puede decir que el corazón late a un ritmo constante, lo que ayuda a probar los programas que la analizan. Pero es clave usar filtros para encontrar bien lo importante. 


C. Pre procesamiento de la señal:

Es importante mencionar que el pre procesamiento de una señal es algo fundamental, ya que con este paso se mejora la calidad de la señal capturada y de esta forma identificar correctamente en nuestro caso la señal del corazón. A partir de esto, como se mencionó anteriormente se toma la señal en reposo del sujeto de prueba, que se encuentraa contaminada por distintos ruidos, y para lograr corregir esto se implementan filtros digitales que son diseñados para este tipo de señal. En particular, se utiliza un filtro de tipo IIR (respuesta infinita al impulso), el cual se diseña de acuerdo con las características espectrales del ECG y se implementa considerando condiciones iniciales en cero. Este filtro se compone de una etapa pasa alta, que elimina las componentes de muy baja frecuencia, y una etapa pasa baja, que suprime las frecuencias altas no deseadas. El resultado es una señal limpia, con mejor definición del complejo QRS, como se muestra en la Imagen 5.

Imagen 5, señal ECG filtrada (pasa alta y pasa bajo):

<img width="857" alt="5minfiltro" src="https://github.com/user-attachments/assets/be4ef1bc-3f2b-460b-9dc4-9c6c7e3d30b7" />

Esta gráfica muestra la señal de ECG después de haber sido procesada con filtros digitales de tipo pasa alta y pasa baja. El propósito de este paso es eliminar el ruido presente en la señal original, tanto de baja frecuencia (como el producido por movimientos corporales o la respiración) como de alta frecuencia (como interferencias eléctricas o artefactos del entorno). Este filtrado permite obtener una señal más limpia y estable, fundamental para su posterior análisis. La curva resultante muestra con claridad los ciclos cardíacos, especialmente el complejo QRS, dentro del cual el pico R es el más prominente. Este preprocesamiento es una etapa clave dentro del procesamiento digital de señales, ya que permite mejorar la calidad de la información útil y facilita la implementación de algoritmos para detección de eventos y análisis cuantitativos.


Después, lo que hacemos es encontrar los picos R, que vienen siendo los puntos más álgidos del complejo QRS y que señalan cuándo se contraen los ventrículos. Para dar con ellos, usamos la señal que ya habíamos limpiado antes, aplicando métodos sencillos para buscar los puntos más altos y así clavar dónde están los picos con exactitud. Una vez que tenemos los picos R bien ubicados, calculamos el tiempo que hay entre uno y otro, que se conoce como intervalo R-R, y con esto armamos una nueva señal basada en los tiempos entre cada latido. Esta info es clave para estudiar cómo varía la frecuencia cardiaca (HRV), porque nos deja ver cómo el sistema nervioso autónomo anda regulando el ritmo del corazón. En la Imagen 6 se puede ver cómo queda todo esto, con los picos R resaltados para que se note la regularidad de los latidos, dejando la señal lista para seguir analizándola ya sea mirando el tiempo, o usando técnicas como la transformada wavelet para ver el tiempo y la frecuencia a la vez, lo cual se evidencia en la imagen 6.

Imagen 6, señal ECG filtrada con picos R:

<img width="857" alt="5minpicos" src="https://github.com/user-attachments/assets/f6f8aa47-a15b-4d9e-ba7d-a3826bbb7450" />

Esta gráfica presenta la misma señal de ECG ya filtrada, pero con la detección de los picos R resaltada mediante marcadores visuales (cruces amarillas). Estos picos corresponden a los máximos de cada complejo QRS y su detección precisa es esencial para calcular los intervalos R-R, es decir, el tiempo entre un latido y el siguiente. Esta etapa forma parte del proceso de extracción de características y se realiza aplicando técnicas de procesamiento digital como la derivación, umbralización adaptativa o algoritmos como Pan-Tompkins, que permiten identificar automáticamente estos puntos clave dentro de la señal. La identificación de los picos R permite transformar una señal continua en un conjunto de eventos temporales discretos, que son la base para el análisis de la variabilidad de la frecuencia cardiaca (HRV), tanto en el dominio del tiempo como en el dominio tiempo-frecuencia. Esta extracción es imprescindible para interpretar la dinámica del sistema nervioso autónomo y llevar a cabo estudios clínicos o biomédicos más avanzados.




D. Análisis nde HVR en el dominio del tiempo:

El análisis de la variabilidad de la frecuencia cardíaca (HRV) en el dominio del tiempo, lo que hacemos es examinar cómo los espacios entre cada latido (los intervalos R-R) se modifican con el pasar del tiempo. Con este análisis, podemos entender mejor cómo funciona el sistema nervioso autónomo, ya que la VFC nos dice si hay equilibrio entre las ramas simpática y parasimpática. Para hacer esto, primero medimos los intervalos R-R detectando los picos R en la señal del ECG, una vez que la hemos limpiado de ruidos. Con estos intervalos en mano, calculamos cosas básicas como el promedio y la dispersión, que nos dan una idea de cuánta variabilidad hay y qué tan regular es el corazón. Es algo muy común en el análisis de señales del cuerpo, ya que nos permite interpretar lo que sucede en el cuerpo usando herramientas sencillas de procesamiento digital, como cálculos estadísticos aplicados a una señal que viene del ECG. 

 
Imagen 7, parámetros básicos de la HVR;
<img width="506" alt="Captura de pantalla 2025-05-13 a la(s) 7 36 18 p m" src="https://github.com/user-attachments/assets/dca8f1bf-2bf1-4a4a-b7b5-1bd1535a4975" />


En los datos que tenemos en la imagen 7, vemos una serie de 23 intervalos R-R expresados en segundos, con números que van desde cerca de 0. 064 hasta 0. 112 segundos. Con estos datos, calculamos un promedio de los intervalos R-R de 0. 0741 segundos, lo que quiere decir que, en general, el tiempo entre latidos en esta medición fue de 74. 1 milisegundos. La dispersión es de 0. 0097 segundos, lo que nos indica que hay una variabilidad moderada en los intervalos. Esto sugiere que el ritmo del corazón es bastante regular, pero con pequeños cambios naturales, algo normal en condiciones normales. Además, se muestran medidas como el MSE (error cuadrático medio) y el R-squared, que, aunque se usan más para ajustar modelos, pueden servir para ver cuán bien se reconstruye o predice la señal R-R en ciertos casos. También se muestran los promedios de intensidad en las bandas de baja y alta frecuencia, que nos preparan para el análisis espectral. 



Imagen 8 , coeficientes wavelet morlet; 
<img width="717" alt="Figure 2025-05-13 193406 (3)" src="https://github.com/user-attachments/assets/b8f15c32-b5b8-4378-81d5-8fc932b7d702" />


En la imagen 8 , vemos los coeficientes que salieron al usar la transformada wavelet continua con la wavelet de Morlet, que es una forma de mirar las señales en el tiempo y en la frecuencia a la vez. La gráfica nos deja ver cómo cambian las diferentes partes de la señal, cada una con su propia frecuencia, a medida que avanza el tiempo. En el eje vertical tenemos las frecuencias, medidas en hercios (Hz), y en el horizontal, el tiempo, medido en milisegundos. Los puntos donde la gráfica se ve más intensa, con colores más vivos, nos dicen que hay más energía o actividad en ciertas frecuencias y en ciertos momentos. Aquí, se ve claramente que la actividad se concentra en las frecuencias más bajas, más o menos entre 5 y 15 Hz, que suele ser normal en las señales del corazón y puede tener que ver con el sistema parasimpático. Esta forma de verlo ayuda mucho porque nos da más información que solo mirar la señal en el tiempo, y nos enseña cómo el ritmo del corazón va cambiando con el tiempo, cosa que no podríamos ver solo con números y estadísticas.





Espectrrograma de HVR en baja frecuencia(0.04 -0.15 Hz); 
<img width="798" alt="Figure 2025-05-13 193406 (5)" src="https://github.com/user-attachments/assets/46987aef-fb3c-47a5-85a2-b8b859a67458" />


Espectrograma de HVR en alta frecuencia (0.15 - 0.4 Hz):
<img width="804" alt="Figure 2025-05-13 193406 (6)" src="https://github.com/user-attachments/assets/d0b175db-341f-4bbe-9aa2-c06aec434239" />


