---
layout: post
title:  "Patrón Abstract-factory"
date:   2015-09-17 13:23:06
categories: jekyll update
excerpt: 
hide: 0
---
## Intención ##

>Provee una interfaz para crear familias de objetos sin especificar sus clases
>concretas.
>

Es una extensión del metodo [factory-method][factory-method-post], en el que, en vez de entregarnos
una clase (producto), nos entrega otra factoria (creador), de esa manera las 
distintas factorias nos entregan diversos productos.

![Abstract-factory]({{ site.url }}/assets/abstract-factory_1.png "Abstract-factory")
Fuente de la imagen: [https://github.com/iluwatar/java-design-patterns][java-design]

Siguiendo el ejemplo de la imagen, con este patrón podemos crear los productos
Rey, Castillo y Armada, dependiendo de la raza a la que pertenezca. Y gracias a
que hay una interfaz para definir lo que es un reino, podemos hacer que los
reinos que implementen esta interfaz, puedan crear su reinado.

## Cuando utilizar ##

* Cuando un sistema debe ser independiente de como sus productos son creados,
  compuestos y representados.
* Cuando un sistema debe ser configurado con uno o mas familias de productos.
* Cuando una familia de productos esta diseñada para ser usadas juntas, y es
  necesario remarcar este hecho.
* Cuando se quiere entregar una librería de productos, y solo se quiera dar sus
  interfaces, no sus implementaciones.

## Caso de estudio ##

Supongamos que estamos en un invernadero y tenemos que programar el riego
automático y la inyección de CO2 dentro de este. Pero en el invernadero tiene
varios sectores con diferentes plantas, las cuales necesitan una cantidad
distinta de agua y de CO2. Podemas aplicar el modelo abstract factory, para
representar cada sección que necesitemos, y manejarlas todas por igual.

![Caso estudio Abstract-Factory]({{ site.url }}/assets/abstract-factory-caso-estudio.png "Caso de estudio")

En donde InvernaderoFactory es la interfaz para crear los diferentes lugares, y
Riego y CO2 (Clases que controlaran como funciona el invernadero) son nuestros
productos abstractos.

Si lo vemos en código Java:

{% highlight java %}
public interface Riego {
	public void regar();
}
{% endhighlight %}
{% highlight java %}
public interface CO2 {
	public void inyectar();
}
{% endhighlight %}
{% highlight java %}
public class RiegoSeccionN implements Riego{
    @Override
    public void regar(){
        System.out.println("Estoy regando la seccion N");
    }
}
{% endhighlight %}
{% highlight java %}
public class CO2SeccionN implements CO2{
    @Override
    public void inyectar() {
        System.out.println("Estoy inyectando CO2 a la sección N");
    }
}
{% endhighlight %}
{% highlight java %}
public interface InvernaderoFactory {
    public Riego crearRiego();
    public CO2 crearCO2();
}
{% endhighlight %}
{% highlight java %}
public class SeccionN implements InvernaderoFactory {
    @Override
    public Riego crearRiego() {
        return new Riego();
    }
    @Override
    public Riego crearCO2() {
        return new CO2();
    }
}
{% endhighlight %}
{% highlight java %}
public class EjemploAbstractFactory {
    public static void main(String[] args) {
        InvernaderoFactory iff = new SeccionN();
        Riego r = iff.crearRiego();
        r.regar();
    }
}
{% endhighlight %}

[factory-method-post]: http://pigant.github.io/jekyll/update/2015/09/15/Factory-method.html
[java-design]:  https://github.com/iluwatar/java-design-patterns
