# Estimación de Parámetros de un sistema
A continuación se presenta el procedimeinto para la estimación de parámetros estáticos de un sistema utilizando datos de entrada y salida. El proceso se realiza a partir de la optimizacióin de la respuesta iterando diferentes valores de parámetros hasta encontrar los óptimos.
Simulink / Matlab tiene una herramienta para llevar a cabo este proceso y de esta manera poder obtener un modelo de simulación Simscape, función de transferencia o espacio de estados
## Motor que se quiere modelar
Se presenta un ejemplo donde se pretende obtener los parámetros internos de un motor DC (inductancia, resistencia, constantes de transformación, etc.). El motor utilizado es el Moog C23L33W10

![Motor DC marca moog](images/motorDC.png)

Los parámetros que presenta el fabricante están dados en terminos del torque y la velocidad que puede alcanzar el motor en vacío y a plena carga

![Datasheet Motor DC marca moog](images/data_MotorDC.png)

De la figura anterior se puede observar que el fabricante no entrega parámetros internos como la inductancia y resistencia de armadura, o las constantes de conversión de energías necesarias si se quiere obtener un modelo por corriente de armadura o corriente de campo.

A este motor Moog C23L33W10 se le realizan pruebas en lazo abierto, de tal manera que se pueda obtener información de la dinámica del motor y a partir de esto llegar a un modelo aproximado al comportamiento real.

## Metodología de Uso de herramienta de estimación de prámetros
Para realizar la estimación de parámetros de cualquier sistema es posible reducir el procedimiento a los siguientes pasos:

* Recopilar los datos de entrada y salida del sistema por medio de una tarjeta de adquisición de datos, un osciloscopio o un microcontrolador+Simulink
* Crear un modelo en simulink que represente el sistema del que no se conocen todos los parámetros
* Declarar los parámetros que se quieren estimar como variables simbólicas y configura aquellos parámteros que son conocidos en el modelo Simulink
* Abrir la herramienta de estimación de parámetros y verificar que los parámetros que se van a estimar están configurados
* Ejecutar la herramienta para que corra el algoritmo de optimización

## Datos recopilados del motor DC Moog C23L33W10

Se configuró el motor en lazo abierto, con su respectivo puente H y se le aplico una señal de tren de pulsos para repetir su dinámica varias veces de manera periódica. La figura muestra la señal de entrada que se aplica y la respuesta del motor en terminos de velocidad en RPM.

Teniendo los datos de la prueba almacenados en una estructura de matlab que tiene la siguiente ruta:
* Para la entrada 'MotorDC{2}.Values.Data' y 'MotorDC{2}.Values.Time' para la base de tiempo
* Para la respuesta de la velocidad en RPM 'MotorDC{1}.Values.Data' y 'MotorDC{1}.Values.Time' para la base de tiempo

El código en Matlab para graficar la entrada y salida a partir de los datos almacenados en las estructuras anteriormente mencionadas puede escribirse asi:
```
>> subplot(2,1,1)
>> plot(MotorDC{2}.Values.Time, MotorDC{2}.Values.Data)
>> title('Entrada de pulsos')
>> ylabel('Voltaje (V)')
>> xlabel('Tiempo (s)')
>> axis([0 10 0 3.2])
>> subplot(2,1,2)
>> plot(MotorDC{1}.Values.Time, MotorDC{1}.Values.Data, "red")
>> title('Salida de motor')
>> ylabel('Velocidad (RPM)')
>> xlabel('Tiempo (s)')
>> axis([0 10 0 7300])
```
![Datos entrada y salida motorDC](images/DatosMotorDC.PNG)

## Creación de modelo Simulink
Para este caso se utilizará el paquete Simscape de Simulink, el cual cuenta con un modelo parametrizado de un motor DC, lo cual facilitará la creación del modelo. 

![Modelo Simulink MotorDC](images/Modelo_MotorDC.PNG)

En la imagen se observa bloques de paquete Simscape que representan el modelo matemático de un motor DC, conectado a un puente H como driver de potencia y un generador de PWM para conmutar los transistores del puente H. Los dos últimos son modelos ideales en los cuales no se configuró ningún parámetro.





