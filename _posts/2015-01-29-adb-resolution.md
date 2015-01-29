---
layout: post
title: "Como cambiar la resolución de un dispositivo Android"
modified:
categories: Android
excerpt: "Cambia la resolución de tu dispositivo para probar tu aplicación."
tags: [Android, adb, trucos]
image:
  feature:
date: 2015-01-29T20:37:00+01:00
---

Si quieres probar tu aplicación en distintas resoluciones sin necesidad de disponer de varios dispositivos puedes ajustar la resolución de tu dispositivo mediante adb. Para ello tan solo necesitas enviar el comando *wm* al dispositivo de la siguiente forma:

{% highlight text %}
adb shell wm size <nuevo_ancho>x<nuevo_alto>
{% endhighlight %}

Y en el caso de querer simular otra densidad puedes hacerlo mediante:

{% highlight text %}
adb shell wm density <nueva_densidad>
{% endhighlight %}

Te recomiendo realizar los cambios con la pantalla apagada (bloqueada), ya que haciendolo mientras la pantalla está encendida me he encontrado con cosas curiosas como la desaparición de la barra de menús al establecer resoluciones menores que la nativa o tamaños de letra minúsculos en el caso de pasar a resoluciones mayores.

Por ejemplo para establecer una resolución de 600x800 y una densidad de 200 tendrías que ejecutar los siguientes comandos:

{% highlight text %}
adb shell wm size 600x800
adb shell wm density 200
{% endhighlight %}

<figure class="half">
    <a href="/images/resize_screen_720x1280.png"><img src="/images/resize_screen_720x1280.png"></a>
    <a href="/images/resize_screen_600x1000.png"><img src="/images/resize_screen_600x1000.png"></a>
    <figcaption>Capturas de un Moto G con resolución de 720x1280 y 600x1000 respectivamente.</figcaption>
</figure>

### Deshaciendo los cambios

Para volver a los valores por defecto tienes que utilizar *"reset"* como valor para la resolución o densidad:

{% highlight text %}
adb shell wm size reset
adb shell wm density reset
{% endhighlight %}

### Otras posibilidades

También puedes consultar los valores de tu dispositivo no indicando un nuevo valor, por ejemplo para saber cuál es la densidad de tu dispositivo puedes ejecutar:

{% highlight text %}
adb shell wm density
{% endhighlight %}

**NOTA**: En el caso de que tu dispositivo use una versión de Android anterior a la 4.3 deberás sustituir el comando *wm* por *am* y añadir *display-* antes de la opción que quieras modificar. Por ejemplo así modificarías la resolución:

{% highlight text %}
adb shell am display-size <nuevo_ancho>x<nuevo_alto>
{% endhighlight %}
