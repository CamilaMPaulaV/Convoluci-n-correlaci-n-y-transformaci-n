# Convolución, correlación y transformación
## Introducción
A continuación se presenta la señal resultante de la convolución de dos sistemas y dos señales discretas, calculada mediante sumatorias, junto con su representación gráfica y secuencial realizada manualmente, así mismo se incluye el código en Python que automatiza este proceso.
Por otra parte, a partir del código que puede encontrar en el repositorio "Statistical analysis of a signal" se realizaron modificaciones para realizar la transformada de Fourier, la gráfica de la transformada y de la densidad espectral de una señal de electromiografía con neuropatías sacada del banco ATM de pyshionet.

## Resultados
### Parte manual 
El primer sistema que se determinó fue 1034777850 junto con la primera señal discreta 5600765, con lo anterior se realizó la convolución de manera matricial, para oprimizar el proceso, se obtuvo el siguiente resultado
AQUÍ FOTO 1

Una vez obtenido lo anterior se realizaron las gráficas correspondientes a la señal, el sistema y su convolución:
GRÁFICAS 1

Posteriormente se realizó el mimso proceso con el segundo sistema y segunda señal, obteniendo lo siguiente
AQUÍ FOTO 2
AQUÍ GRÁFICA 2


### Código en Python 

### Señal EMG 
A partir de la señal EMG, se obtuvo la sieguiente gráfica
AQUÍ SEÑAL EMG

Posteriormente se realizan los cálculos pertinentes para hallar su media, desviación estandandar y coeficiente de variación, los valores obtenidos son los siguientes:
Coeficiente de variación: 101842.59095057225
SNR con Ruido Gaussiano Alta Frecuencia: 3.02 dB
SNR con Ruido Gaussiano Baja Frecuencia: 2.99 dB

Una vez obtenidos los datos anteriores se ontuvo su histograma y su función de probabilidad de manera manual y automática obteniendo lo siguiente:
AQUÍ GRÁFICAS

Al contaminar la señal con ruido Gaussiano, impulos y artefacto, se obutvo lo siguiente:
AQUÍ GRÁFICA


Al aplicar la transformada de Fourier de la señal y graficar su transformada y su densidad espectral, se btuvo lo siguiente:
AQUÍ FOTO


## Requerimientos
1. Python 3.12
2. Librerias numpy, matplotlib, time
3. Señal electromigráfica en formato mat

