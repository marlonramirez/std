<h1>std.js</h1>
<p><a href="http://std.mirdware.co.cc">Std.js</a> es un proyecto de c�digo abierto que he comenzado por mi cuenta, con el �nico fin de reunir una serie de funciones utilizadas frecuentemente con diferentes fines. De esta manera std.js posee funciones para:</p>
<ul>
	<li>atajos y ejecuci�n del DOM</li>
	<li>Manejo de estilos</li>
	<li>Comunicaciones AJAX</li>
	<li>Soporte a JSON (IE 7 y 8)</li>
	<li>Efectos y animaciones</li>
	<li>Manejador de eventos</li>
	<li>Compatibilidad con frameworks js</li>
</ul>
<p>�Por que no utilizar una de las tantas librer�as JavaScript del mercado, si est�n tan bien documentadas y son tan funcionales? tengo varias razones para utilizar y mantener este trabajo, tal vez algunas de ellas sean muy egocentricas y otras m�s carescan de sentido, dentro de estas razones estan: rapidez de ejecuci�n (hasta 80% m�s rapido que algunos frameworks populares), control absoluto del codigo, simplicidad y por que realmente amo a javascript como es, con sus virtudes y defectos.</p>
<h2>Consideraciones</h2>
<p>Logicamente std.js no ha sido testeado infinidad de veces como lo hacen "fameworks" m�s populares y por lo tanto es MUY posible que este pragado de errores y asuntos a�n no resueltos, seg�n he ido testeando el funcionamiento de la libreria he observado que algunos errores son debido a algunas consideraciones que se deben tener en cuenta.</p>
<h3>Pru�balo en un servidor</h3>
<p>Para realizar las pruebas AJAX se deben tener los archivos directamente en alg�n servidor, esta misma consideraci�n debe ser tomada en cuenta para la utilizaci�n de hojas de estilos en Chrome, pues si se prueba de manera stand alone, puede presentar inconvenientes.</p>
<h3>T� eres primero</h3>
<p>Si vas a usar hojas de estilos o scripts ajenos a t� servidor (caso de redes sociales) no olvides que estas deben ser enlazadas al final del documento, esto se debede principalmente al modo como std recorre las hojas de estilos externas.</p>
<h2>M�dulos externos</h2>
<p>A partir de la versi�n 0.0.9 de la librer�a se acepta la inclusi�n de m�dulos externos (tambi�n conocidos como plugins), gracias a esta nueva caracter�stica se ha podido separar el modulo encargado de generar las ventanas speudomodales y su inclusi�n a la librer�a es opcional. La manera de crear m�dulos externos para la librer�a es la siguiente:</p>
```javascript
	(function($, window, undefined) {
		//extiende std con el modulo externo
		$.extend($, {
			modulo: ...
		});
	})(std, window);
```
<p>Se usa std y no el alias, ya que std siempre va a estar apuntando inmodificable a la librer�a as� se use cmode, gracias a esto se pueden encerrar funcionalidades en un solo �mbito que use la librer�a, de esta manera se evitan futuros problemas de incompatibilidad entre frameworks y std.</p>
```javascript
	(function($, window, undefined) {
		// declaraci�n de variables globales
		var FALSE = false,
			TRUE = true,
			NULL = null,
			document = window.document;

		//domready
		$ (function () {

		})
	})(std, window);
```