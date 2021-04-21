# Speedmeter-a-Stegano-Crackers (Actualizado)
Ya pasado un tiempo de realizado este blog, tocó actualizarlo con una excelente noticia para todos los CTFteros que buscan optimizar su velocidad de resolución.

El rey ha muerto, larga vida al rey.

Stegcracker, el ganador de la revisión que había hecho ya hace casi un año ha sido derrocado.
El nuevo campeón de steganografía ahora se llama Stegseek.

Tiene a su favor la no despreciable reputación de recorrer el archivo rockyou.txt en 2 segundos.
su trabajo ha sido arduo y en el control de versiones se puede identificar cada uno de los pasos que han llevado a los desarrolladores a la mejora.
según dice su documentación, es más rápido que los demás por que sólo lee una vez el archivo, a diferencia de los otros sistemas que leer una vez por palabra.

para instalarlo no es más que descargar la última versión liberada y dar sudo apt install ./stegseek_0.6-1.deb
(https://github.com/RickdeJager/stegseek/releases)

El uso es similar a stegcracker
stegseek <imagen> <wordlist>
   
Los invito a probar uds. mismos la velocidad de esta nueva herramienta con alguno de los desafíos que ya han tenido en su pasado y adoptar esta genial mejora en los desafíos de steganografía.

Saludos.

-------------------------------------------------------------------

Pruebas de velocidad de cada aplicación de crackeo esteganográfica

Existen varias herramientas de fuerza bruta para resolver steganografía en archivos de imagen.

un programa puede medir su calidad desde diferentes aspectos. En los relacionados con Crackers necesitamos:

1. Eficacia: que logre hacer lo que se pide.. es decir que no tenga falsos positivos o negativos, y que termine al momento de encontrar la palabra clave.

   - 1.1 diccionario que contenga la palabra correcta
  
   - 1.2 un software que revise correctamente cada palabra y detectando el éxito.


2. Eficiencia: que logre hacerlo en el mínimo de tiempo.
 Que logre resolver un desafío en el menos tiempo posible dependerá de varios factores:

   - 2.1 Rendimiento de la máquina donde corre el aplicativo (capacidad de cómputo)

   - 2.2 Un código que logre realizar la tarea de la forma más directa sin desperdiciar tiempo de procesador.
 
En un escenario donde la máquina no varía, el único factor a considerar será el rendimiento del código (2.2)
Aquí pondré una tabla comparativa de las pruebas de velocidad que realicé con el fin de lograr identificar cual herramienta usar de forma más permanente, basándose en las mejores formas de ejecutar el aplicativo sobre una maquina standard sin GPU. (unidad de procesamiento gráfico especializado)

El laboratorio se realiza poniendo intencionadamente una contraseña que no está en el diccionario.
De esta forma recorreremos en todos los casos la totalidad de las palabras en casa una de las pruebas.

Cantidad de palabras en el diccionario 100.000

| Nombre del programa | Comando Ejecutado |  Segundos | velocidad (palabras por segundo) | Observaciones |
| ------------- | ------------- | ------------- | ------------- | ------------- |  
stegcracker	| stegcracker file.jpg dict		| 433	| 231 |	|
steg_brute.py | sudo python steg_brute -b -d dict -f file.jpg		| 514 |	195	| cayó con syntax error (;'!)|
stegbreak	| stegbreak -f dict file.jpg	| | | caida por desbordamiento |
pybrute.py |	pybrute.py -f file -w dict steghide	| 546 |	183	| indica que usa 10 hilos (threads)|

### notas:

Steg_brute.py no logró administrar palabras que contenían comillas simples, lo que provocaba que la aplicación se detuvieran.
para ejectuar correctamente la intrucción se debió filtrar:

`tr "\'" ""`

stegbreak luego de unos 10 segundos tras la ejecución caía por Fragmentation Fault. Hasta el momento no he logrado identificar la causa (se descartó que fuera a raíz de las comillas simples)

pybrute.py indica que corre 10 hilos simultaneamente, pero en mediciones, esa modificación no significó mejora apreciable.

Entendiendo que la prueba fue realizada sólo con 100 mil palabras y considerando que `rockyou.txt` tiene 14.3 millones, esta diferencia de tiempo entre una herramienta y otra puede significar horas menos de espera.


Como podrán notar, `stegcracker` superó la velocidad promedio del resto, por lo que queda por el momento seleccionada como mi herramienta favorita.

# Links
Stegcracker: https://pypi.org/project/stegcracker/

steg_brute.py: https://github.com/Va5c0/Steghide-Brute-Force-Tool

stegbreak: https://github.com/s-fiebig/stegdetect-stegbreak

pybrute.py: https://github.com/DominicBreuker/stego-toolkit/tree/master/scripts
