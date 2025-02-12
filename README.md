# Convolución, correlación y transformación
## Introducción
A continuación se presenta la señal resultante de la convolución de dos sistemas y dos señales discretas, calculada mediante sumatorias, junto con su representación gráfica y secuencial realizada manualmente, así mismo se incluye el código en Python que automatiza este proceso.
Por otra parte, a partir del código que puede encontrar en el repositorio "Statistical analysis of a signal" se realizaron modificaciones para realizar la transformada de Fourier, la gráfica de la transformada y de la densidad espectral de una señal de electromiografía con neuropatías sacada del banco ATM de pyshionet.

## Resultados
### Parte manual 
El primer sistema que se determinó fue 1034777850 junto con la primera señal discreta 5600765, con lo anterior se realizó la convolución de manera matricial, para oprimizar el proceso, se obtuvo el siguiente resultado
<div align="center">
<img src="https://i.postimg.cc/28kn53TH/P1.png"width="400" height="400">
<img src="https://i.postimg.cc/jqPGdZvh/P2.png"width="700" height="400">
</div>
Una vez obtenido lo anterior se realizaron las gráficas correspondientes a la señal, el sistema y su convolución:
<div align="center">
<img src="https://i.postimg.cc/fL2k3MM6/P3.png"width="600" height="400">
<img src="https://i.postimg.cc/R0bNhMS2/P4.png"width="600" height="400">
</div>
Posteriormente se realizó el mismo proceso con el segundo sistema y segunda señal, obteniendo lo siguiente
<div align="center">
<img src="https://i.postimg.cc/rFtCLPJ8/C1.png"width="400" height="400">
<img src="https://i.postimg.cc/nc7R1zNY/C2.png"width="700" height="400">
<img src="https://github.com/user-attachments/assets/d69cff42-7993-4f5d-a8fd-cda7f29ee9a5"width="600" height="400">
<img src="https://github.com/user-attachments/assets/3ca5e2a8-d025-4052-a284-b24be00a8fb1"width="600" height="400">
</div>

### Código en Python 
1. Se definen las señales y sistemas que se van a utilizar. Posteriormente se realiza la convolución discreta entre las señales con sus respectivos sistemas haciendo uso de la función np.convolve obteniendo así una tercera señal y las gráficas que se ven a continuación.
   
```python
# Señales discretas y sistemas proporcionados
SD1 = np.array([1, 0, 3, 4, 7, 7, 7, 8, 5])  # Señal discreta 1
sistema1 = np.array([5, 6, 0, 0, 7, 0, 7, 6, 7])  # Sistema 1

SD2 = np.array([1, 0, 3, 4, 7, 7, 7, 8, 5])  # Señal discreta 2
sistema2 = np.array([5, 6, 0, 0, 7, 0, 7, 6, 7])  # Sistema 2

# Convolución entre las señales y sistemas proporcionados
y1 = np.convolve(SD1, sistema1, mode='full')
y2 = np.convolve(SD2, sistema2, mode='full')

# Gráficos de señales y sistemas con su convolución
plt.figure(figsize=(12, 8))
plt.subplot(3, 2, 1)
plt.stem(n, SD1, label="Señal 1", linefmt='b', markerfmt='bo', basefmt=" ")
plt.stem(n, sistema1, label="Sistema 1", linefmt='g', markerfmt='go', basefmt=" ")
plt.title("Señal 1 y Sistema 1")
plt.legend()

plt.subplot(3, 2, 2)
plt.stem(n, SD2, label="Señal 2", linefmt='r', markerfmt='ro', basefmt=" ")
plt.stem(n, sistema2, label="Sistema 2", linefmt='m', markerfmt='mo', basefmt=" ")
plt.title("Señal 2 y Sistema 2")
plt.legend()

plt.subplot(3, 2, 3)
plt.stem(np.arange(len(y1)), y1, label="Convolución Señal 1", linefmt='c', markerfmt='co', basefmt=" ")
plt.title("Convolución Señal 1 y Sistema 1")
plt.legend()

plt.subplot(3, 2, 4)
plt.stem(np.arange(len(y2)), y2, label="Convolución Señal 2", linefmt='y', markerfmt='yo', basefmt=" ")
plt.title("Convolución Señal 2 y Sistema 2")
plt.legend()

plt.tight_layout()
plt.show()
```
<div align="center">
<img src="https://i.postimg.cc/FKKwGvyr/Se-ales-y-sistemas.png"width="400" height="400">
</div>
2.  Se definen los valores del tiempo de muestreo y el rango para que así las señales estén correctamente muestreadas y representadas. Además, se realiza la correlación de las mismas con ayuda de la función np.correlate, lo cual permite observar la similitud que hay entre ambas señales.

```python

# Definir Ts y el rango de n
Ts = 1.25e-3  # Tiempo de muestreo en segundos
n = np.arange(0, 9)  # Rango de n

# Definir las señales x1[n] y x2[n]
x1 = np.cos(2 * np.pi * 100 * n * Ts)  # Señal coseno
x2 = np.sin(2 * np.pi * 100 * n * Ts)  # Señal seno

# Correlación entre x1 y x2
correlacion = np.correlate(x1, x2, mode='full')
```
<div align="center">
<img src="https://i.postimg.cc/vTGKgdZw/Correlacion.png"width="700" height="400">
</div>

3. Por último se realiza la representación secuencial por medio de la creación de gráficos animados que muestran la evolución de las señales y sistemas punto a punto en el tiempo, como se puede observar en las siguientes gráficas:
```python
# Representación secuencial de x1 y x2
plt.figure(figsize=(8, 6))
for i in range(len(n)):
    plt.clf()
    plt.subplot(2, 1, 1)
    plt.stem(n[:i+1], x1[:i+1], linefmt='b', markerfmt='bo', basefmt=" ")
    plt.title("Evolución de x1[n]")
    
    plt.subplot(2, 1, 2)
    plt.stem(n[:i+1], x2[:i+1], linefmt='r', markerfmt='rs', basefmt=" ")
    plt.title("Evolución de x2[n]")
    
    plt.tight_layout()
    plt.pause(0.5)
plt.show()

# Representación secuencial de los sistemas
plt.figure(figsize=(8, 6))
for i in range(len(n)):
    plt.clf()
    plt.subplot(2, 1, 1)
    plt.stem(n[:i+1], sistema1[:i+1], linefmt='g', markerfmt='go', basefmt=" ")
    plt.title("Evolución del Sistema 1")
    
    plt.subplot(2, 1, 2)
    plt.stem(n[:i+1], sistema2[:i+1], linefmt='m', markerfmt='mo', basefmt=" ")
    plt.title("Evolución del Sistema 2")
    
    plt.tight_layout()
    plt.pause(0.5)
plt.show()
```
<div align="center">
<img src="https://i.postimg.cc/y6Sh9GSw/REPRESENTACI-N-SECUENCIAL.png"width="400" height="400">
<img src="https://i.postimg.cc/zGR118Lx/fin-fin.png"width="400" height="400">
</div>

## Representación secuencial

### Señal EMG 
A partir de la señal EMG, se obtuvo la sieguiente gráfica
<div align="center">
  <img src="https://github.com/user-attachments/assets/867b23ff-0963-4645-b1b3-7c63aea2e882" width="400" height="400">
</div>

Posteriormente se realizan los cálculos pertinentes para hallar su media, desviación estandandar y coeficiente de variación, los valores obtenidos son los siguientes:


Una vez obtenidos los datos anteriores se ontuvo su histograma y su función de probabilidad de manera manual y automática obteniendo lo siguiente:
<div align="center">
  <img src="https://github.com/user-attachments/assets/acd5e1d1-1acd-4852-abf7-348b8bdf8341" width="400" height="400">
  <img src="https://github.com/user-attachments/assets/9f92d611-f059-4cdd-86e5-748d3e09f632" width="400" height="400">
  <img src="https://github.com/user-attachments/assets/620ace93-208a-4176-a3f6-7858f78322ab" width="400" height="400">
  <img src="https://github.com/user-attachments/assets/26916ee6-aa85-4a9c-8727-80c8d0019fbd" width="400" height="400">
</div>

Al aplicar la transformada de Fourier de la señal y graficar su transformada y su densidad espectral, se btuvo lo siguiente:
<div align="center">
  <img src="https://github.com/user-attachments/assets/ab9286bb-75a5-4ee6-a39b-ed1df082806f" width="400" height="400">
  <img src="https://github.com/user-attachments/assets/cbdccfa2-7906-4d2a-b44e-f1e586a3d2b3" width="400" height="400">
</div>

A partir de la señal obtenida y de su representación en gráficos se observa que es una señal no determinística dado que no sigue un patrón matemático, lo que quiere decir que son variantes y dependientes de factores cambiantes. Así mismo estocástica por el hecho de que tiene un componente aleatorio lo que quiere decir que su comportamiento varía en el tiempo de manera impredecible

## Instrucciones 
## Señales EMG
Nota: A continuación se presentaron únicamente los cambios nuevos realizados sobre el código ya mencionado.

1. Para realizar la transformada de Fourier se utilizó scipy.fft.fft para calcularla la transformada rápida de Fourier dada su mayor facilidad, posteriormente se cálculo el espectro de la misma (magnitud) y se graficó para ver cómo se distribuyen las frecuencias de la señal, finalmente se calcula la densidad espectral de potencia (PSD), que muestra la distribuición de la potencia de la señal a lo largo de las frecuencias.
```python
# Realizar la Transformada Rápida de Fourier (FFT) de la señal EMG
frecuencia = np.fft.fftfreq(len(emg), d=ts)  # Generar el vector de frecuencias
fft_emg = np.fft.fft(emg)  # Calcular la FFT de la señal

# Calcular la magnitud de la FFT
magnitud_fft = np.abs(fft_emg)

# Graficar el espectro de la señal
plt.plot(frecuencia[:n//2], magnitud_fft[:n//2])  # parte positiva de la frecuencia
plt.title('Espectro de la Señal EMG')
plt.xlabel('Frecuencia (Hz)')
plt.ylabel('Magnitud')
plt.show()

# Calcular la densidad espectral de potencia (PSD)
from scipy.signal import welch
frequencias_psd, psd_emg = welch(emg, fs, nperseg=1024)

# Graficar la densidad espectral de potencia (PSD)
plt.semilogy(frequencias_psd, psd_emg)
plt.title('Densidad Espectral de Potencia de la Señal EMG')
plt.xlabel('Frecuencia (Hz)')
plt.ylabel('Densidad Espectral de Potencia (dB/Hz)')
plt.show()
```

## Requerimientos
1. Python 3.12
2. Librerias numpy, matplotlib, time
3. Señal electromigráfica en formato mat
   
## Referencias
1. Dominio de la Frecuencia | PySDR: A Guide to SDR and DSP using Python. (s. f.). https://pysdr.org/es/content-es/frequency_domain.html
2. Transformada rápida de Fourier (I). (s. f.). http://www.sc.ehu.es/sbweb/fisica3/datos/fourier/fourier_1.html#:~:text=La%20transformada%20r%C3%A1pida%20de%20Fourier,%2C%201024%2C%204096%2C%20etc.
3. PhysioBank ATM. (s. f.). https://archive.physionet.org/cgi-bin/atm/ATM
4. Dominio de la Frecuencia | PySDR: A Guide to SDR and DSP using Python. (s. f.). https://pysdr.org/es/content-es/frequency_domain.html
