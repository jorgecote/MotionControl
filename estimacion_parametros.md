# Estimación de Parámetros de un sistema
A continuación se presenta el procedimeinto para la estimación de parámetros estáticos de un sistema utilizando datos de entrada y salida. EL proceso se realiza a partir de la optimizacióin de la respuesta iterando diferentes valores de parámetros hasta encontrar los óptimos.
Simulink / Matlab tiene una herramienta para llevar a cabo este proceso y de esta manera poder obtener un modelo de simulación Simscape, función de transferencia o espacio de estados
## Procedimiento para el uso del estimador de parámetros Simulinkb / Matlab
Se presenta un ejemplo donde se pretende obtener los parámetros internos de un motor DC (inductancia, resistencia, constantes de transformación, etc.). El motor utilizado es el Moog C23L33W10

![Motor DC marca mooc](images/motorDC.png){width='100px'}
