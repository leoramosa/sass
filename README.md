# Practicando Sass

[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/M4M41O8NC)

`@import` sirve para importar otro archivos de sass (scss) en el archivo principal para que se refleje en el archivo final de style.css

####Variables
$ usando el signo de dolar podemos crear variables esto nos sirve para hacer una variable
y poder usarlo en nuestro proyecto varias veces, ejemplo:

	$color: red;
	$color1: blue;
	$color2: green;
---

	.div {
  	background-color: $color;
	}
>asi podemos usar $color sin poner el codigo del color 		varias veces


####Anidaciones
Con las Anidaciones podemos crear estilos dentro del estilo padre y asi cuando se compile saldra el estilo nombrado con el estilo padre ejemplo:

	.btn {
  	display: inline-block;
  	color: $buttoncolor;
  	background-color: $buttonbackgroundcolor;
  	.btn__icon{
    	font-size: 6em;
  	}
>`&` con este simbolo podemos nombrar al padre y ya no tendremos que escribirlo

	& &__icon{
   	 font-size: 6em;
  	}
  	.btn--info{
    	background-color: $color-info;
  	}
	}

El resultado sera el siguiente:

	.btn {
  	display: inline-block;
  	color: white;
  	background-color: #ea83ee;
  	line-height: 2.5;
  	border-radius: 4px;
  	font-size: 24px;
	}

	.btn .btn__icon {
  	font-size: 6em;
	}

	.btn .btn__icon {
  	font-size: 6em;
	}

	.btn .btn--info {
  	background-color: #42b8dd;
	}

##Mixins:
Los mixins nos permiten rehusar declaraciones e incluso Modificar el valor cuando la rehusamos explico un poco más una declaracion nos puede decir que un  color es igual a red, nosotros podemos  crear un mixins para que siempre color sea red pero más podemos modificar. Entonces vamos a ver un ejemplo de un mixins vamos a ir incrementando su funcionalidad para ver como hasta dónde podemos llegar con los mixes.

creamos un archivo _mixins.scss

escribimos:

-----
	@mixin max-width{
  	max-width: 800px;
  	margin-left: auto;
  	margin-right: auto;
	}

y en otro archivos des sasss ejemplo:  _layout.scss podemos utilizar lo que esta en mixins.scss para utilizarlo escribimos `@include` max-width:

	section {
  	@include max-width;
  	background-color: $color-lightgrey;
  	padding: $padding;
	}

Los mixins pueden ser parametricos, pueden ser parametros, ejemplo:

	@mixin max-width($maxwidth: $page-max-width){//son variables que funcionan en 	los mixins(unicamentes)
 	 //al 800px lo vamos a convertir en varible como practica para seguir usando sass
  	max-width: $maxwidth;
  	margin-left: auto;
  	margin-right: auto;
	}

####Constants
	$border-radius:4px;
	$padding:24px;
	$page-max-width:800px;

Uso de la directiva `content` (`block` en Stylus)
Una de las características que tienen los mixins es la directiva content.
Esta nos permite incluir un bloque de contenido dentro de un mixin.

##Extend
con ` %`  creamos placeholder en sass ejemplo:

	%max-width{
  	max-width:80%;
  	margin-right:0;
  	margin-left:0;
	}

El codigo anterior no se va a visualizar en css cuando lo compilemos para poder utilizrarlo debemos escribir el siguiente codigo de ejemplo:

	.section{
  	@extend %max-width;
	}

	.container{
  	@extend %max-width;
  	font-size:14px;
	}

asi podemos utilizar el ` @extend`  y el resultado en el css sera el siguiente:

	.container, .section {
  	max-width: 80%;
  	margin-right: 0;
  	margin-left: 0;
	}
-------
	.container {
  	font-size: 14px;
	}

###Funciones

Sass tiene muchas funciones que podemos usar cuando estamos modificando CSS.
Muchas de estas funciones son muy útiles como por ejemplo aclarar un color u oscurecerlo. Así hay muchísimas más, sin embargo hay algunas que no nos permiten hacer cambios visuales y que pueden parecer no tan útiles.

algunas funciones:

- darken
- lighten
- invert
-----
	$color-grey: #737373;
	$color-darkgrey: #4d4d4d;
>*esta funcione darken oscurece el color que esta en la variable*

	$color-darkgrey: darken($color-grey, 25%);
-----
	$color-lightgrey: #bfbfbf;

>*esta funcione lighten aclara el color que esta en la variable*

	$color-lightgrey: lighten($color-grey, 25%);
----
	$color-error: rgb(218,79,73);
----
>*esta funcione invierte el color*

	$color-invert: invert($color-error);


##Directiva
Las funciones nos permiten directamente modificar el valor de ciertas propiedades. 
Para crear una función vamos a usar el @function.

	@function suma($numero-uno, $numero-dos){
  	@return $numero-uno + $numero-dos;
	}
----
	.div{
  	padding: suma(10px, 5px);
	}

Resultado en el css:

	div{
		padding:15px;
	}

Ejemplos de funciones

Las funciones también puede ser extraer valores de un array.
Una función puede utilizar arrays que son más parecidas a listas.
Para Sass es más un mapa. Podemos aprender a usar mapas con los posibles tipos de fuentes que hayan.

Nos sirve para fuentes, tamaños, colores, etc.

	$fs: (
  	big:24px,
  	normal:16px,
  	small:14px,
  	x-small:12px,
	);
----
	p{
  	font-size: map-get($fs, normal);
	}

se visualizara asi en el css:

	p {
  	font-size: 16px;
	}

####Listas y directiva @each

De ahora en adelante veremos varias directivas de control de flujo dentro de Sass. Por eso en esta clase vamos a hablar sobre cómo usar la directiva each y cómo manejar listas dentro de Sass.

para usar @each usamos el siguiente codigo:
>*Con each podemos hacer varios estilos pero con 	la misma propiedades pero con el valor diferente*

	@each $font in (normal, bold, italic){ 
  	.#{$font} {font-weight: $font;}
	}

resultado en el css:

	.normal {
  	font-weight: normal;
	}

	.bold {
  	font-weight: bold;
	}

	.italic {
  	font-weight: italic;
	}

ahora para seguir usando terminos de sass vamos hacer una lista para utilizar el codigo anterior ya escrito:

>*creacion de la lista* para hacer una lista solo demos separarlas por un espacio

	$font-weights: normal bold italic;
	@each $font in ($font-weights){
  	.#{$font} {font-weight: $font;}
	}

Resutaldo:

	.normal {
  	font-weight: normal;
	}

	.bold {
  	font-weight: bold;
	}

	.italic {
  	font-weight: italic;
	}

###Ciclos FOR/EACH
Por medio de la directiva each ustedes van a crear las clases usando el ciclo each.
La directiva for se parece mucho a la directiva each.

con el termino `@for` podemos crear el sigueinte codigo:

	@for $i from 1 to 5 {
  	.class {
    	&:before {
    	content: $i;
    	}
  	}
	}

El resutlado en el css es el siguiente:

	.class:before {
  	content: 1;
	}

	.class:before {
  	content: 2;
	}

	.class:before {
  	content: 3;
	}

	.class:before {
  	content: 4;
	}

otro ejemplo:

>al usar #{} dentro de una variable podemos escaparla es decir podemos usar la variables en la propiedad y valor de un estilos y el resultado va hacer el mismo solo con algunos cambios que los puedes ver a la hora de compilar el codigo de abajo.

	@for $i from 1 to 5 {
  	.class-#{$i} {
    	&:before {
    	content: "#{$i}";
    	}
  	}
	}

###Directiva @if Condicionales

Si definimos una variable con un valor:

	$background-color:black;

Podemos usar la directiva @if para darle una condicion a esa variable y dentro podemos escribir selector agremos su propidad y su valor, si la condicion es verdadera podemos visualizarlo en a la hora de compilar el css porque si no cumple no se va mostrar, para eso tambien podemos usar la directiva @else para asignarle una varialbe con un selector si se requiere o tambien podemos omitir la directa @else si se requiere.

	@if $background-color == black{
  	p {
    	text-color: white;
  	}
	}

y el resultado en css sera el siguiente:

	p {
  	text-color: white;
	}

Aparte podemos usar la cascada si p ya tiene un valor:

	p {
  	text-color: black
	}

y ejecutamos el codigo anterior esto nos serviria para cambiar los valores dinamicamente con las Condicionales el resultado seria el sigueinte en el css:

	p {
  	text-color: black;
	}

	p {
  	text-color: white;
	}

[![ko-fi](https://www.ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/M4M41O8NC)
