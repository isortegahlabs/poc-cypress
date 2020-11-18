# POC CYPRESS

## Motivación

Cypress es una herramienta de testing de última generación construida para la web moderna. Con este framework podemos probar cualquier cosa que funcione en un navegador. Es un **"todo en uno"** ya que incluye librerias de aserciones, mocks y prueba e2e sin utilizar "Selenium". No utiliza Selenium porque consta de una nueva arquitectura, construida desde cero, que ejecuta los comandos en el mismo ciclo de ejecución que la aplicación.

Nos presenta una interfaz gráfica que muestra el proceso de la ejecución de las pruebas como lo realizaría un usuario desde su navegador, y mientras corren las pruebas, nos permite obtener `insights` de todo lo que ocurre, además de poder interactuar y detenerte para ver el por qué de las fallas, regresar a cada paso realizado durante la ejecución para ver como era la `UI` en ese punto del tiempo y ver elementos en consola.

Cypress ejecuta un proceso Node que permanentemente se comunica, sincroniza y ejecuta tareas, teniendo acceso tanto a la parte `frontend` como a la parte `backend` de la aplicación y respondiendo a los eventos en tiempo real.

Está diseñado para manejar frameworks de JavaScript modernos como: React, Angular, Vue, Elm, etc. Pero, también funciona igual de bien en páginas o aplicaciones renderizadas en servidor.

|  Características	| Cypress 	|
|-	|-	|
| Lenguaje 	    | JavaScript 	|
|Entorno de ejecución| NodeJS|
| Navegadores   | Chrome , Firefox    	|
| Test Runner   | Mocha         |   
| Navegador embebido | Si|
|Consola Ejecución| Si|
|Ejecución headless| Si|
|Open Source|Si|


## Features

* Time Travel: Cypress toma snapshots mientras se ejecutan las pruebas. Al colocar el cursor sobre los comandos en el `Command Log` podemos ver exactamente qué sucedió en cada paso.

* Debuggability: No se requiere adivinar por qué fallan las pruebas. Podemos depurar directamente como con las herramientas de desarrollo. Los errores serán legibles y con formato de `stack traces` lo que hacen que la depuración sea muy rápida.

* Automatic Waiting: No se requiere agregar `waits` o `sleeps` a las pruebas. Cypress espera automáticamente los `commands` y las `assertions` antes de continuar. No más dolores de cabeza con las funciones asíncronas.

* Spies, Stubs, and Clocks: Podemos verificar y controlar el comportamiento de las funciones, las respuestas del servidor o los temporizadores. La misma funcionalidad de las pruebas unitarias está al alcance de nuestras manos.

* Network Traffic Control: Se puede controlar, resguardar y probar casos extremos muy fácilmente sin involucrar a su servidor. Puede bloquear el tráfico de la red como deseemos.

* Consistent Results: La arquitectura no utiliza Selenium ni WebDriver. Se da la bienvenida a las pruebas rápidas, consistentes y confiables que no tienen `flake-free`.

* Screenshots and Videos: Capturas de pantalla tomadas automáticamente en caso de falla, o videos de todo su conjunto de pruebas cuando se ejecuta desde la CLI.

* Cross browser Testing: Ejecución de pruebas dentro de los navegadores de la familia Firefox y Chrome (incluidos Edge y Electron) de manera local y óptima en un `Pipeline` de integración continua.

El navegador headless tiene estas principales ventajas:

* Es más rápido, ya que corre en memoria y no requiere de toda la preparación que tienen los navegadores gráficos.
* Se pueden tomar screenshots o vídeos como si fuera una prueba automatizada normal.
* Cuando se trabaja con una herramienta de integración continua y entrega continua, como Jenkins, nos permite correr las pruebas e2e sin necesidad de tener un navegador instalado.

Para la parte de reportes podemos usar [mochawesome](https://github.com/adamgruber/mochawesome), lo he utilizado en el pasado y es muy bueno y fácil de modificar en caso de requerir agregar alguna característica.

## Pre requisitos

* Instalación del proyecto

```bash
    npm install
```


## Cypress Open

* El comando [`cypress open`](https://docs.cypress.io/guides/guides/command-line.html#cypress-open) nos lanzará una aplicación de escritorio que nos permite ejecutar nuestras pruebas, en caso de ejecutarse por primera vez, se inicializará una carpeta con nombre `cypress` que contiene dentro de sus subcarpetas la ruta `integration/examples` con varios ejemplos que nos permiten explorar las diferentes funciones disponibles.

```bash
npx cypress open
```

***Nota:*** Este comando nos permitiría inicializar el proyecto. Usa [Electron](https://www.electronjs.org/) para crear la aplicación de escritorio.


## Conclusión

Revisamos en primer instancia el framework por su uso para la automatización de pruebas e2e, pero al tener incluidos los frameworks Mocha, Chai y Sinon, se pueden realizar perfectamente pruebas unitarias y por supuesto pruebas de integración, tanto para `Frontend` como de `Backend`.

Cypress opera dentro de la aplicación, lo que permite realizar las siguientes acciones, que son muy útiles, tanto para test unitarios como para los test e2e:

* Realizar stubs de funciones para forzar ciertos comportamientos.
* Exponer data stores desde el código de los test.
* Testear las respuestas a errores modificando el status code de la respuesta del servidor a un 500.
* Evitar hacer siempre login gracias a comandos como cy.request() que envía directamente una petición HTTP.
* Puede ejecutar las pruebas sin la necesidad de tener un navegador instalado.

También opera en la capa de red leyendo y alterando el tráfico web sobre la marcha. Esto permite no solo modificar todo lo que entra y sale del navegador, sino también cambiar el código que puede interferir con su capacidad para automatizar el navegador.

Las pruebas tienen que estar escritas en Javascript (lo que no puede agradar a algunos)Dado que tiene acceso nativo a todos los elementos, desde elementos DOM y funciones, hasta la ventana o temporizadores, esto facilita de gran forma la automatización. 

Las características que son más sobresalientes y que debemos considerar a detalle son:

* Tasks (plugins)
* Custom Commands (support)
* fixture
* mocking server
* Ejecución en paralelo
* Documentación clara y completa
* Simplicidad en la creación de test
* Facilidad de instalar (nos olvidamos de las dependencias al estar todo integrado)
* Velocidad en la ejecución de pruebas
* Debug mode por console logs y videos
* Visual testing con [percy](https://docs.percy.io/docs/getting-started)
* Reutilizar el código en testunitarios
* viewports (redimensionar la view para simular dispositivos)
* Selector en la UI, para revisar que selector va a utilizar
* Selectores con chai
* Integración de [testing library](https://testing-library.com/docs/cypress-testing-library/intro/#docsNav)
* No Page Object
* No login UI necessary
* Real Visual testing
* Se puede integrar con el desarrollo por lo que en CI se podría ejecutar

Cabe destacar que estas la gran mayoría de estas funcionalidades podemos programarlas y utilizarlas en cualquier otro framework como `test cafe` o incluso `Selenium`, lo interesante aquí es saber el `que?`, el `como?` investigando un poco podríamos implementarlo.

El uso de este framework es recomendable para ser usado cuando se comienza a automatizar, nos facilita el camino de una forma impresionante y su arquitectura nos proporciona bastantes ideas además de que nos proporciona herramientas suficientes para poder programar lo que nuestra imaginación dicte y construir un framework bastante robusto para nuestros proyectos.

## Referencia

* [Cypress in a Nutshell](https://www.youtube.com/watch?v=LcGHiFnBh3Y)

* [Webinar: Problemas, ventajas y retos del Test end to end con Cypress.io](https://www.youtube.com/watch?v=rA_1fPa38Tg)
* [Why Cypress?](https://docs.cypress.io/)
