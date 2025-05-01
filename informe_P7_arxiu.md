# Informe Práctica 7
## Ejercicio Practico 1 reproducción desde memoria intern

###  Descripción de la salida por el puerto serie
Cuando se ejecuta el programa , si todo funciona bien , no se muestra nada mas que el mensaje de que el puerto serie se haya iniciado. Cuando el audio termina de reproducirse , aparece el mensaje :
 ```cpp
Sound Generator
```
 Este mensjae se repite cada segundo y se muestra cuando ya ha finalizado la reproducción del audio.


###  Explicación del funcionamiento
Este código reproduce un sonido que esta guardado en la ESP32, usando el protocolo del I2S para enviar la señal de audio a un amplificador externo (altavoz).

Lo que hace el código paso por paso es:
1. **Inicio del puerto serie**

2. **Carga del archivo de audio**
- AudioFileSourcePROGMEM
3. **Configuración de los componentes de audio**
- **AudioGeneratorAAC**: Descodifica el archivo 
- **AudioOutputI2S**: Manda la señal a través del protocolo I2S
- **SetPinout(20,21,47)**: Define los pines que se usan para la seál I2S 
4. **Inicio de reproducción**
- aac->begin(in, out)
5. **Bucle de reproducción**
En el loop () , el código revisa constantemente si el audio sigue reproduciéndose:
- Si es que sí, sigue llamando a aac->loop() para seguir con la reproducción
- Si es que no, detiene el audio con aac->stop() y muestra un mensaje en el puerto serie (ada segundo) que dice: Sound Generator
## Ejercicio Practico 2 reproducir un archivo WAVE en ESP32 desde una tarjeta SD externa
###  Descripción de la salida por el puerto serie
Para este codigo, si todo funciona correctamente, no aparece ningun mensaje en el puerto serie durante la reproducción del audio, ya que no tienen ninguna instrucción del tipo : Serial.print() . 

###  Explicación del funcionamiento
Este programa reproduce un archivo de audio guardado en una tarjeta SD, usando el protocolo I2S y con la ayuda de un módulo amplificador MAX98357A . Este módulo lo que haces es convertir la señal digital en una señal analógica para poder escucharla en el altavoz.

Lo que hace el código paso por paso es:
1. **Configuració Inicial**
- Definición de pines
2. **Inicio de la tarjeta SD**
-  SD.begin(SD_CS)
3.  **Configuraciónn de I2S**
- Configuración de pines del protocolo I2S
4. **Ajuste del volumen**
- audio.setVolume(10)
5. **Inicio de la reproducción**
- audio.connecttoFS(SD, "bass-wiggle-297877.wav")

