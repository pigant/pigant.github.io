---
layout: post
title:  "El patron Factory-method"
date:   2015-09-15 13:43:06
categories: jekyll update
excerpt: 
hide: 0
---
## Intención ##

>Definir una interfaz para crear objetos, dejando a las subclases decidir cual
clase instanciar. Permite que una clase delegue en sus subclases la creación de
objetos.
>

Consta de un creador abstracto y un producto abstracto, cuando queremos
generar un producto en particular o una familia relacionada a ese producto
abstracto(Por ejemplo algun comestible, donde puede ser pizza o arroz), 
heredamos de producto. Y cuando queramos crear algun producto especifico dentro
de una familia de productos, creamos un creador para este producto/s.

![factory-method]({{ site.url }}/assets/factory-method_1.png "opt title")
Fuente de la imagen: [https://github.com/iluwatar/java-design-patterns][java-design]

De esta manera si queremos crear un arma (producto) y sabemos que lo tiene que
crear un herrero (factoria), pero el arma puede tener variaciones de diferente
indole, se puede aplicar este patrón.

## Cuando utilizar ##

* Cuando una clase no puede anticipar que tipo de objeto debe crear
* Cuando se quiere que la clase no especifique como crear objetos, si no que lo
  hagan sus subclases

## Caso de estudio ##

Imaginemos que tenemos un juego, el en cual deseamos que, independiente del
control que utilicemos, podamos cargar el juego y jugarlo tranquilamente. En
ese caso, podemos identificar que tenemos una clase abstracta o una interfaz
llamada control, la que podra tener las subclases, teclado, mouse, joypad,
volante, etc. Para cargar alguno en especifico sin tener que realizar mucho
trabajo podemos tener una clase creadora, como en el patron Factory-method.

![Caso estudio Factory-method]({{ site.url }}/assets/factory-method-caso-estudio.png "Caso de estudio")

En donde Control es nuestra clase producto abstracto, y la clase ControlFactory
es nuestra clase creadora abstracta, y es con esas que nuestro programa
trabaja, la implementación del producto esta en Mouse, Teclado, Joypad y
volante, y la implementación del creador SeleccionControl.

Si lo vemos en código Java:

{% highlight java %}
public interface Control {
	public int obtenerBoton();
}
{% endhighlight %}
{% highlight java %}
public class Mouse implements Control{
	@Override
	public int obtenerBoton() {
		//Puede devolver algun boton presionado, a manera de ejemplo 
		//solo retorna un 1
		return 1;
	}
}
{% endhighlight %}
{% highlight java %}
public class Teclado implements Control{
	@Override
	public int obtenerBoton() {
		//Puede devolver algun boton presionado, a manera de ejemplo 
		//solo retorna un 1
		return 1;
	}
}
{% endhighlight %}
{% highlight java %}
public class Joypad implements Control{
	@Override
	public int obtenerBoton() {
		//Puede devolver algun boton presionado, a manera de ejemplo 
		//solo retorna un 1
		return 1;
	}
}
{% endhighlight %}
{% highlight java %}
public class Volante implements Control{
	@Override
	public int obtenerBoton() {
		//Puede devolver algun boton presionado, a manera de ejemplo 
		//solo retorna un 1
		return 1;
	}
}
{% endhighlight %}
{% highlight java %}
public interface ControlFactory {
	public Control obtenerControl();
}
{% endhighlight %}
{% highlight java %}
public class SeleccionControl implements ControlFactory {
	@Override
	public Control obtenerControl(String control) {
		switch(control){
			case "mouse":
				return new Mouse();
			case "teclado":
				return new Teclado();
			case "joypad":
				return new Joypad();
			case "volante":
				return new Volante();
			default:
				return new Teclado();
		}
	}
}
{% endhighlight %}
{% highlight java %}
public class EjemploFactoryMethod {
	public static void main(String[] args) {
		ControlFactory c = new SeleccionControl();
		//obtengo un objeto Control, con su implementacion en Mouse
		Control control = c.obtenerControl("mouse");
	}
}
{% endhighlight %}

[java-design]:  https://github.com/iluwatar/java-design-patterns
