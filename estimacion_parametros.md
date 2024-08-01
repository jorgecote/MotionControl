# Estimación de Parámetros de un sistema
A continuación se presenta el procedimeinto para la estimación de parámetros estáticos de un sistema utilizando datos de entrada y salida. EL proceso se realiza a partir de la optimizacióin de la respuesta iterando diferentes valores de parámetros hasta encontrar los óptimos.
Simulink / Matlab tiene una herramienta para llevar a cabo este proceso y de esta manera poder obtener un modelo de simulación Simscape, función de transferencia o espacio de estados
## Motor que se quiere modelar
Se presenta un ejemplo donde se pretende obtener los parámetros internos de un motor DC (inductancia, resistencia, constantes de transformación, etc.). El motor utilizado es el Moog C23L33W10

![Motor DC marca moog](images/motorDC.png)

Los parámetros que presenta el fabricante están dados en terminos del torque y la velocidad que puede alcanzar el motor en vacío y a plena carga

![Datasheet Motor DC marca moog](images/data_MotorDC.png)

De la figura anterior se puede observar que el fabricante no entrega parámetros internos como la inductancia y resistencia de armadura, o las constantes de conversión de energías necesarias si se quiere obtener un modelo por corriente de armadura o corriente de campo.

A este motor Moog C23L33W10 se le realizan pruebas en lazo abierto, de tal manera que se pueda obtener información de la dinámica del motor y a partir de esto llegar a un modelo aproximado al comportamiento real.

## Datos recopilados del motor DC Moog C23L33W10

Se configuró el motor en lazo abierto, con su respectivo puente H y se le aplico una señal de tren de pulsos para repetir su dinámica varias veces de manera periódica. La figura muestra la señal de entrada que se aplica y la respuesta del motor en terminos de velocidad en RPM.

Teniendo los datos de la prueba almacenados en una estructura de matlab que tiene la siguiente ruta:
* Para la entrada 'MotorDC{2}.Values.Data' y 'MotorDC{2}.Values.Time' para la base de tiempo
* Para la respuesta de la velocidad en RPM 'MotorDC{1}.Values.Data' y 'MotorDC{1}.Values.Time' para la base de tiempo

El código en Matlab para graficar la entrada y salida a partir de los datos almacenados en las estructuras anteriormente mencionadas puede escribirse asi:


