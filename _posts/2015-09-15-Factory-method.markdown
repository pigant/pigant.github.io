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

De esta manera si queremos crear un arma (producto) y sabemos que lo tiene que
crear un herrero (factoria), pero el arma puede tener variaciones de diferente
indole, se puede aplicar este patrón.

## Cuando utilizar ##

* Cuando una clase no puede anticipar que tipo de objeto debe crear
* Cuando se quiere que la clase no especifique como crear objetos, si no que lo
  hagan sus subclases

