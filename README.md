<h1>std.js is JavaScript standard</h1>
<p>std.js es un proyecto de c�digo abierto que he comenzado por mi cuenta, con el �nico fin de reunir una serie de funciones utilizadas frecuentemente con diferentes fines. De esta manera std.js propone funciones para:</p>

<ul>
	<li>atajos (getElement) y ejecuci�n (ready) del DOM</li>
	<li>Manejo de estilos</li>
	<li>Comunicaciones AJAX</li>
	<li>Soporte a JSON (IE 7)</li>
	<li>Efectos y animaciones</li>
	<li>Manejador de eventos</li>
	<li>Compatibilidad con frameworks js</li>
</ul>
<p>�Por qu� no utilizar una de las tantas librer�as JavaScript del mercado, si est�n tan bien documentadas y son tan funcionales? tengo varias razones para utilizar y mantener este trabajo, tal vez algunas de ellas sean muy egoc�ntricas y otras m�s carezcan de sentido, pero son mis razones y estas son: rapidez de ejecuci�n (hasta 80% m�s r�pido que algunos frameworks populares), control absoluto del c�digo, simplicidad y porque realmente amo a JavaScript como es, con sus virtudes y defectos.</p>

<h2>Premisas de std.js</h2>
<ul>
	<li>
		<b>Promover la simplicidad:</b> Keep It Simple, Stupid! de hecho soy un eterno creyente que el camino m�s sencillo casi siempre es el m�s efectivo.
	</li>
	<li>
		<b>Ocupar poco espacio:</b> Espero no llegar a pasar los 20k, de momento la librer�a pesa menos de 10k y no podr�a estar m�s contento de ello.
	</li>
	<li>
		<b>Dar prioridad a lo nativo:</b> Siempre es mejor usar las cosas nativas del lenguaje, en caso de las animaciones existe CSS y aunque no sea soportado por algunos navegadores, si es una animaci�n est�tica es mucho mejor pasar de JavaScript.
	</li>
	<li>
		<b>Continuar la legac�a IE:</b> Hasta donde sea posible claro est�, tampoco vamos a dar soporte a IE 6, pues ya ni Microsoft lo da.
	</li>
	<li>
		<b>Modificar lo menos posible la sintaxis JavaScript:</b> A�n que tal vez muchos no compartan m� opini�n, para m� JavaScript es hermoso tal cual es y quiero mantenerlo as�.
	</li>
</ul>

<h2>Consideraciones</h2>
<p>L�gicamente std.js no ha sido testeado infinidad de veces como lo hacen "fameworks" m�s populares y por lo tanto es MUY posible que este plagado de errores y asuntos a�n no resueltos, seg�n he ido testeando el funcionamiento de la librer�a he observado que algunos errores son debido a algunas consideraciones que se deben tener en cuenta.</p>

<h3>Pru�balo en un servidor</h3>
<p>Para realizar las pruebas AJAX se deben tener los archivos directamente en alg�n servidor, esta misma consideraci�n debe ser tomada en cuenta para la utilizaci�n de hojas de estilos en Chrome, pues si se prueba de manera stand alone, puede presentar inconvenientes.</p>

<h3>T� eres primero</h3>
<p>Si vas a usar hojas de estilos o scripts ajenos a t� servidor (caso de redes sociales) no olvides que estas deben ser enlazadas al final del documento, esto se debe principalmente al modo como std recorre las hojas de estilos externas.</p>

<h2>M�dulos externos</h2>
<p>A partir de la versi�n 0.0.9 de la librer�a se acepta la inclusi�n de m�dulos externos (tambi�n conocidos como plugins), gracias a esta nueva caracter�stica se ha podido separar el m�dulo encargado de generar las ventanas speudomodales y su inclusi�n a la librer�a es opcional. La manera de crear m�dulos externos para la librer�a es la siguiente:</p>

```javascript
(function($, window, undefined) {
	/*#module*/
})(std, window);
```

<p>Se usa std y no el alias, ya que std siempre va a estar apuntando inmodificable a la librer�a as� se use cmode, gracias a esto se pueden encerrar funcionalidades en un solo �mbito que use la librer�a, de esta manera se evitan futuros problemas de incompatibilidad entre frameworks y std.</p>

<p>La estructura interna del m�dulo se puede dividir en tres bloques: la declaraci�n de variables globales, las funciones internas y la exportaci�n, la exportaci�n del m�dulo se puede hacer por medio de $.extend en cuyo caso se debe extender el objeto std $ con el nuevo m�dulo que se ha creado, otra manera es usar $.dom.ready o su alias para que al momento de cargar el DOM y dependiendo de los atributos de algunos elementos se ejecuten las funciones dadas.</p>

```javascript
(function($, window, undefined) {
	// declaraci�n de variables globales
	var FALSE = false,
		TRUE = true,
		NULL = null,
		document = window.document,
		core = {
			/*#code*/
		};

	//funciones intenarnas
	function fn (e) {
		/*#code*/
	}

	//Exportaci�n del m�dulo por $.extend, $.dom.ready o ambas
	$ (function () {
		/*#code*/
	})

	$.extend($, {module: core});
})(std, window);
```
