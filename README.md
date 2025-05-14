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

codigo arduino: 
void setup() {
  // Iniciar comunicación serial
  Serial.begin(9600);
}

void loop() {
  
 Serial.println(analogRead(A0));
 delay(4);
}




Señal ECG original de la matriz;
<img width="857" alt="Figure 2025-05-13 193406 (0)" src="https://github.com/user-attachments/assets/8f98d940-118a-43f4-adc0-19c9d13ca0cf" />


Señal ECG filtrada (pasa alta y pasa bajo):
<img width="857" alt="Figure 2025-05-13 193406 (1)" src="https://github.com/user-attachments/assets/ce944648-55a5-406a-8d6e-7ddef2d8ddf2" />



Señal ECG filtrada con picos R:
<img width="857" alt="Figure 2025-05-13 193406 (2)" src="https://github.com/user-attachments/assets/12fb9ba7-4171-486a-9b19-c8079ea1dda7" />


Espectrrograma de HVR en baja frecuencia(0.04 -0.15 Hz); 
<img width="798" alt="Figure 2025-05-13 193406 (5)" src="https://github.com/user-attachments/assets/46987aef-fb3c-47a5-85a2-b8b859a67458" />


Espectrograma de HVR en alta frecuencia (0.15 - 0.4 Hz):
<img width="804" alt="Figure 2025-05-13 193406 (6)" src="https://github.com/user-attachments/assets/d0b175db-341f-4bbe-9aa2-c06aec434239" />

Índice de intervalo R-R:
<img width="506" alt="Captura de pantalla 2025-05-13 a la(s) 7 36 18 p m" src="https://github.com/user-attachments/assets/dca8f1bf-2bf1-4a4a-b7b5-1bd1535a4975" />
