# Event Loop
Node.js es una "aplicación de un solo subproceso", pero admite la concurrencia a través del concepto de evento y devoluciones de llamada. Como cada API de Node.js son asíncronas y siendo un solo hilo, usa la funcción **async** que llama a mantener la concurrencia. Node usa un patrón de observación. el hilo deNode, mantiene un ciclo de eventos y siempre que cualquier tarea se complete, lanza el evento correspondiente que señala la función detector de eventos para ser ejecutado

### Programación de evento conducido
Node.js utiliza eventos en gran medida y es una ded las razones por qué Node.js es bastante rápido en comparación a otras tecnologias similares. En cuanto Node inicia el servidor, simplemente inicializa las variables, declara funciones y luego simplemente espera a que ocurra un evento

En una aplicación de evento conducido, hay generalmente un ciclo principal que escucha por eventos, y entonces activa una funcion de devolución de llamada cuando uno de esos eventos es detectado
![Image](http://www.tutorialspoint.com/nodejs/images/event_loop.jpg)
Mientras los eventos parecen similares a los que son las devoluciones de llamada, la diferencia esta en el hecho de que las devoluciones son funciones que son llamadas cuando una función asíncrona regresa su resultado, cuando los manejadores de eventos trabajan en el patrón de obvervación. La función que escucha al evento actua como observador. Siempre que un evento es lanzado, su función de detección se ejecuta. Node.js tiene múltiple eventos incluidos disponibles mediante modulos de **evento** y la clase **EventEmitter** la cuál es usada para enlazar eventos y detectores de eventos de la siguiente manera:
```javascript
// Import events module
var events = require('events');
// Create an eventEmitter object
var eventEmitter = new events.EventEmitter();
```
Aquí la sintaxis para enlazar un manejador de evento con un evento
```javascript
// Bind event and even handler as follows
eventEmitter.on('eventName', eventHandler);
```
Y lanzamos el evento como:
```javascript
// Fire an event 
eventEmitter.emit('eventName');
```
Ejemplo:
```javascript
// Import events module
var events = require('events');
// Create an eventEmitter object
var eventEmitter = new events.EventEmitter();

// Create an event handler as follows
var connectHandler = function connected() {
   console.log('connection succesful.');
  
   // Fire the data_received event 
   eventEmitter.emit('data_received');
}

// Bind the connection event with the handler
eventEmitter.on('connection', connectHandler);
 
// Bind the data_received event with the anonymous function
eventEmitter.on('data_received', function(){
   console.log('data received succesfully.');
});

// Fire the connection event 
eventEmitter.emit('connection');

console.log("Program Ended.");
```
El cúal dara como resultado:
```sh
connection succesful.
data received succesfully.
Program Ended.
```
