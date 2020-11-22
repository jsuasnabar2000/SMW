# Clase 5

### POO

- **Programación basada en prototipos**

>La programación basada en prototipos es un estilo de programación orientada a objetos en la que las clases no están presentes y la reutilización de comportamiento (conocido como herencia en lenguajes basados en clases) se lleva a cabo a través de un proceso de decoración de objetos existentes que sirven de prototipos. Este modelo también se conoce como programación sin clases, orientada a prototipos o basada en ejemplos.
>[Mozilla developer network](https://developer.mozilla.org/es/docs/Web/JavaScript/Introducci%C3%B3n_a_JavaScript_orientado_a_objetos)


- **Terminología**

> 
- Clase
	- Define las características del Objeto.
- Objeto
	- Una instancia de una Clase.
- Propiedad
	- Una característica del Objeto, como el color.
- Método
	- Una capacidad del Objeto, como caminar.
- Constructor
	- Es un método llamado en el momento de la creación de instancias.
- Herencia
	- Una Clase puede heredar características de otra Clase.
- Encapsulamiento
	- Una Clase sólo define las características del Objeto, un Método sólo define cómo se ejecuta el Método.
- Abstracción
	- La conjunción de herencia compleja, métodos, propiedades que un objeto debe ser capaz de simular en un modelo de la realidad.
- Polimorfismo
	- Diferentes Clases podrían definir el mismo método o propiedad.
> - [Mozilla developer network](https://developer.mozilla.org/es/docs/Web/JavaScript/Introducci%C3%B3n_a_JavaScript_orientado_a_objetos)


- Entendiendo los objetos:
```javascript
	/*
	[Objeto]{
	    [ Propiedad = Variables (no funciónes) ]
	    [ Método = Solo funciónes ]
	}
	*/
```


- Constructor de Objetos:
```javascript
	var coche = function (parametros) {
	    /* Codigo*/
	};
```


- Propiedades del Objeto:
```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad
	    this.color = color;
	    this.tipo = tipo;
	};
```

### Métodos

- En el Constructor
```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	    this.detalles = function(){
	      console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
	    }
	};

	var miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
	miCoche.detalles();
```


- Extensión del prototipo
```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	};

	coche.prototype.detalles = function(){
	  console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
	}

	var miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
	miCoche.detalles();
```


- Vinculación Externa
```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	    this.detalles = dameDetalles;
	};

	function dameDetalles(){
	  console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
	}

	var miCoche = new coche ("Seat", "Panda", 20, "azul", "turismo");
	miCoche.detalles();
```

### Herencia

- Herencia:
```javascript
	var coche = function (marca, modelo, antiguedad, color, tipo) {
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	    this.detalles = dameDetalles;
	};

	var furgon = function (taraMinima, cargaUtil, volumenCarga) {
	    this.taraMinima = taraMinima;
	    this.cargaUtil = cargaUtil;
	    this.volumenCarga = volumenCarga;
	    this.detallesTecnicos = detallesTecnicos;
	};


	function dameDetalles(){
	  console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años, clase "+this.tipo+" y color "+this.color);
	}

	function detallesTecnicos(){
	  console.warn("Tu coche tiene una Tara mínima de "+this.taraMinima+". Carga útil de "+this.cargaUtil+" y un volumen de carga de "+this.volumenCarga+"m3");
	}

	var miPickup = new coche ("Land Rover", "Santana Aníbal", 35, "Marrón tierra", "4x4");
	miPickup.prototype = new furgon (1200, 768, 4.5);


	miPickup.detalles();
	miPickup.prototype.detallesTecnicos();
```

- Herencia (simplificada):
```javascript
	var perro  = function () {
	    this.patas = 4;
	    this.ojos = 2;
	};

	var pastorAleman = function () {
	    this.colorLengua = "negra";
	    this.colorOjos = "marrón";
	    this.capacidadTrabajo = true;
	    this.especialidad = "Pastoreo";
	};

	pastorAleman.prototype = new perro();

	var miPerro = new pastorAleman();
	console.log("Número patas: "+miPerro.patas+"\n Número ojos: "+miPerro.ojos+"\n Color Lengua: "+miPerro.colorLengua+"\n Color ojos: "+miPerro.colorOjos+"\n Capacidad de trabajo: "+miPerro.capacidadTrabajo+"\n Especialidad: "+miPerro.especialidad);
```

### POO en detalle

- Privado y público:
```javascript
	var cocheEmpresa = function (marca, modelo, antiguedad, color, tipo) {
	    // públicas
	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	    
	    // privadas
	    var ITVPasada = true;
	    var ITVfrecuencia = "Cada año";
	    var seguroEnRegla = true;
	    var companySeguros = "SegurExpress";
	    var tipoSeguro = "a terceros";
		
		// Público
		this.dameDetalles = function () {
			console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años, clase "+tipo+" y color "+color);
	    }
		
		// Privadas
	    function datosPrivados() {
	        if (ITVPasada && seguroEnRegla)
	            console.info("INFO: Todo en Regla, tienes que pasar la ITV "+ITVfrecuencia+". Tienes un seguro "+tipoSeguro+" con "+companySeguros);
	        else{
	            console.error("ALERTA! El coche no puede usarse. El seguro o la ITV no esta en regla.");
	        }
	    }

	    datosPrivados();
	    this.dameDetalles();
	};

	var miCoche = new cocheEmpresa ("Audi", "S8", 2, "negro", "Berlina");
	var miCoche2 = new cocheEmpresa ("Audi", "S4", 2, "Rojo", "Compacto");
```

- Datos opcionales:
```javascript
	var cocheEmpresa = function (marca, modelo, antiguedad, color) {

	    this.marca = marca || "Seat";
	    this.modelo = modelo || "Ibiza";
	    this.antiguedad = antiguedad || 6;
	    this.color = color || "Azul Corporativo";

		this.dameDetalles = function () {
			console.log("Tu coche es un "+this.marca+" "+this.modelo+" con "+this.antiguedad+" años y color "+this.color);
	    }
		
	    this.dameDetalles();
	};

	var miCoche = new cocheEmpresa ("Audi", "S8", 2, "negro", "Berlina");
	var miCoche2 = new cocheEmpresa ();
	var otroCoche = new cocheEmpresa ("Seat", "Leon");
```


- Creando un ID:
```javascript

	var contador = 0;
	var cocheEmpresa = function (marca, modelo, antiguedad, color, tipo) {

	    this.marca = marca;
	    this.modelo = modelo;
	    this.antiguedad = antiguedad;
	    this.color = color;
	    this.tipo = tipo;
	   	this.id = contador++;
	    	    
	    var ITVPasada = true;
	    var ITVfrecuencia = "Cada año";
	    var seguroEnRegla = true;
	    var companySeguros = "SegurExpress";
	    var tipoSeguro = "a terceros";
		
		this.dameDetalles = function () {
			console.log("Tu coche es un "+marca+" "+modelo+" con "+antiguedad+" años, clase "+tipo+" y color "+color);
	    }
		
	    function datosPrivados() {
	        if (ITVPasada && seguroEnRegla)
	            console.info("INFO: Todo en Regla, tienes que pasar la ITV "+ITVfrecuencia+". Tienes un seguro "+tipoSeguro+" con "+companySeguros);
	        else{
	            console.error("ALERTA! El coche no puede usarse. El seguro o la ITV no esta en regla.");
	        }
	    }

	    function identificador(){
	        console.warn("Recuerda! Tu coche esta identificado como coche numero "+contador);
	    }
		
		
	    datosPrivados();
	    this.dameDetalles();
	    identificador();
	};

	var miCoche = new cocheEmpresa ("Audi", "S8", 2, "negro", "Berlina");
	var otroCoche = new cocheEmpresa ("Audi", "A8", 5, "gris", "Berlina");
	var miCoche2 = new cocheEmpresa ("Seat", "Ibiza", 9, "rojo", "Utilitario");
	console.info("Total de coches de empresa hasta el momento "+contador);
```


- Extensión de objetos nativos (usando prototipos):
```javascript
	Array.prototype.coincidencias = function(palabra) {
	    var coincidencias = 0;
	    for (var i=0; i<this.length; i++) {
	        if (this[i] == palabra) {
	            coincidencias++;
	        }
	    }
	    console.warn("Se encontraron "+coincidencias+" coincidencia(s) de la palabra");
	};


	var amigos = ["Charlie", "Marco", "Luis", "Jose", "Miguel", "Jose", "Luis", "Oscar"];
	amigos.coincidencias("Jose");
```


### POO Avanzado

- Dominando los Contextos de *this*: 
    - Window:
    ```javascript
        console.log( this === window );
         
        function prueba(){
          console.log( this === window);
        }
         
        prueba();
    ```
    - Otro Contexto:
    ```javascript
        var usuario = {
          nombre : 'Yo',
          apellido : 'Mismo',
          nombreCompleto : this.name + this.lastName,
          metodoNombre: function(){
            return this.nombre + " " + this.apellido
          },
          valorThis: function (){
            console.log(this);
          }
        }
        // ERROR - Undefined  -> this=window
        console.log( usuario.nombreCompleto);
        
        // FUNCIONA - this=usuario
        console.log(usuario.metodoNombre());
        
        // FUNCIONA - this=usuario
        usuario.valorThis();
    ```

- Usando this:
	```javascript
	var objeto = {
	    valor: 0,
	    incrementar: function(incremento){
	       this.valor += incremento;
	    }
	};

	objeto.incrementar(6);
	
	// objeto.valor
	```


- Alternado el valor de this:
	- ERROR!:
	```javascript
	var objeto = {
	    valor: 0,
	    incrementar: function(incremento){
	       function otraFuncion(unValor){
	           this.valor += unValor;
	       }
	       otraFuncion(incremento);
	    }
	};

	objeto.incrementar(6);
	
	// objeto.valor
	```

	- CORRECTO:
	```javascript
	var objeto = {
	    valor: 0,
	    incrementar: function(incremento){
	       var esto = this;
	       function otraFuncion(unValor){
	           esto.valor += unValor;
	       }
	       otraFuncion(incremento);
	    }
	};

	objeto.incrementar(6);
	
	// objeto.valor
	```


- Usando this en Constructor:
	```javascript
	var fabricaPersonas = function(){
	    this.nombre = 'Pepe';
	};

	fabricaPersonas.prototype.mostrarNombre = function(){
	    console.log(this.nombre);
	};

	var miPersona = new fabricaPersonas();
	miPersona.mostrarNombre();
	```


- Usando *.apply()* para modificar el contexto del *this*:
	```javascript
	var fabricaPersonas  = function(){
	    this.nombre = 'Pepe';
	};

	fabricaPersonas.prototype.mostrarNombre = function(){
	    console.log(this.nombre);
	};

	var otroObjeto = {
	    nombre: 'Oscar'
	};

	var miPersona = new fabricaPersonas();
	miPersona.mostrarNombre();
	miPersona.mostrarNombre.apply(otroObjeto);
	```

- Modificación de contexto
    - con *.call()*:
    	```javascript
    	var objeto = {
    	  multiplicador: 2,
    	  sumatorio: function(num1, num2){
    	     return (num1 + num2) * this.multiplicador;
    	  }
    	};
    
    	var resultado = objeto.sumatorio(2,2);
    	console.log(resultado);
    
    
    	var cambio = {
    	  multiplicador: 5
    	};
    
    	var resultado = objeto.sumatorio.call(cambio, 5, 5);
    	console.log(resultado);
    	```
    
    
    - con *.apply()*:
    	```javascript
    	var objeto = {
    	  multiplicador: 2,
    	  sumatorio: function(num1, num2){
    	     return (num1 + num2) * this.multiplicador;
    	  }
    	};
    
    	var resultado = objeto.sumatorio(2,2);
    	console.log(resultado);
    
    
    	var cambio = {
    	  multiplicador: 5
    	};
    
    	var resultado = objeto.sumatorio.apply(cambio, [5,5]);
    	console.log(resultado);
    	```
    
    
    - con *.bind()*:
    	```javascript
    	var objeto = {
    	  multiplicador: 2,
    	  sumatorio: function(num1, num2){
    	     return (num1 + num2) * this.multiplicador;
    	  }
    	};
    
    	var resultado = objeto.sumatorio(2,2);
    	console.log(resultado);
    
    	var cambio = {
    	  multiplicador: 5
    	};
    
    	var cambiandoFuncion = objeto.sumatorio.bind(cambio);
    	var resultado = cambiandoFuncion(5, 5);
    	console.log(resultado);
    
    	```


### Trabajando con prototipos

- .create():
	```javascript
	var coche = {
	    marca: "Seat",
	    modelo: "Panda",
	    antiguedad: 20,
	    color: "azul",
	    tipo: "turismo"
	};

	var clonCoche = Object.create(coche);

	console.log(clonCoche.marca+" "+clonCoche.modelo);
	```


- .isPrototypeOf():
	```javascript
	console.log(coche.isPrototypeOf(clonCoche));
	```


- .constructor():
	```javascript
	function arbol (nombre) {
	   this.nombre = nombre;
	}

	var miArbol = new arbol( "Pino" );
	console.log( "miArbol.constructor es " + miArbol.constructor );
	```


- .toString():
	```javascript
	function Perro(nombre, criadero, color, sexo) {
	   this.nombre=nombre;
	   this.criadero=criadero;
	   this.color=color;
	   this.sexo=sexo;
	}

	var elPerro = new Perro("Gabby","Laboratorio","chocolate","femenino");

	elPerro.toString();

	Perro.prototype.toString = function perroToString() {
	  var retorno = "Perro " + this.nombre + " es " + this.sexo + " " + this.color + " " + this.criadero;
	  return retorno;
	};

	elPerro.toString();
	```


### Ejercicios

> Vamos a crear un sistema acuapónico en nuestra oficina. Nuestro objetivo será desarrollar una aplicación para gestionarlo todo. Con este ejercicio nos centraremos en la POO y los prototipos

![Ilustración del sistema](http://www.cualtimexico.info/uploads/5/7/4/7/5747467/8636915.jpg)


**1 -** (Usando Constructores). Vamos a instalar un sistema acuapónico en una granja.
Nuestro primer paso será definir el equipamiento. Necesitaremos al menos dos constructores. 
Uno para el tanque de los peces y otro para la cama (recipiente para vegetales).

- Características Tanque:
 - capacidad: 40 Litros
 - dimensiones: 51 cm x 25.5 de ancho x 30.5 de alto
 - color: Gris Claro
 - Nivel agua Máximo: 29 cm

- Características Cama:
 - capacidad: 10 Litros
 - dimensiones: 51 cm x 25.5 de ancho x 10 de alto
 - color: Rojo
 - Nivel agua Máximo: 5 cm
 - Sustrato: Piedra volcánica

Nota: No usar herencia

```javascript
    var acuApp = {};

    // Constructores
    acuApp.constructorTanque = function (capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo) {
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho *largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.dimensionesMedida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
    };

    acuApp.constructorCama = function (capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo, sustrato) {
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho *largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.medida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.sustrato = sustrato;
    };

	// Pruebas
    acuApp["tanque principal"] = new acuApp.constructorTanque(40, "Litros", 30.5, 25.5, 51, "Cm", "Gris Claro", 2);
    acuApp["cama principal"] = new acuApp.constructorCama(10, "Litros", 10, 25.5, 51, "Cm", "Rojo", 5, "Piedra volcánica");
```



**2 -** El siguiente paso en nuestra fabrica será añadir los métodos y propiedades que nos permitan añadir y controlar el agua

- Características del sistema:
    - Métodos para añadir y quitar agua, incluyendo los litros deseados.
    - Comprobación del nivel agua para evitar desbordamientos.
    - En caso de desbordamiento debe activarse el desagüe para eliminar el exceso de agua.

```javascript
    var debugMode = true;

    function chivato (tipo, mensaje) {
        if (debugMode) {
            if(tipo == "warn"){
                console.warn(mensaje);
            } else {
                console.log(mensaje);
            }
        }
    }

    var acuApp = {};
    
    // Constructores
    acuApp.constructores = {
      constructorTanque: function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo) {
        this.nombre = nombre;
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho * largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.dimensionesMedida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.desagueFuncionando = false;
        this.nivelAgua = 0;
        /* Funciones */

        this.agregarAgua = function(litros){
            this.nivelAgua = this.nivelAgua + litros;
            if(this.nivelAgua >= this.nivelAguaMaximo){
                if(!this.desagueFuncionando){
                    this.desagueFuncionando = true;
                    chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
                }
                chivato("log", "nivel actual: "+this.nivelAgua);
                this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
            }
        };
        this.quitarAgua = function(litros){
            this.nivelAgua = this.nivelAgua-litros;
            if(this.desagueFuncionando){
                this.desagueFuncionando = false;
                chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
            }
            chivato("log", "nivel actual: "+this.nivelAgua);
        };
    },
      constructorCama: function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo, sustrato) {
        this.nombre = nombre;
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho *largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.medida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.sustrato = sustrato;
        this.desagueFuncionando = false;
        this.nivelAgua = 0;
        /* Funciones */

        this.agregarAgua = function(litros){
            this.nivelAgua = this.nivelAgua + litros;
            if(this.nivelAgua >= this.nivelAguaMaximo){
                if(!this.desagueFuncionando){
                    this.desagueFuncionando = true;
                    chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
                }
                chivato("log", "nivel actual: "+this.nivelAgua);
                this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
            }
        };
        this.quitarAgua = function(litros){
            this.nivelAgua = this.nivelAgua-litros;
            if(this.desagueFuncionando){
                this.desagueFuncionando = false;
                chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
            }
            chivato("log", "nivel actual: "+this.nivelAgua);
        };
    	}
    };

	// Pruebas
    acuApp.tanque1 = new acuApp.constructores.constructorTanque("Tanque principal",40, "Litros", 30.5, 25.5, 51, "Cm", "Gris Claro", 2);
    acuApp.cama1 = new acuApp.constructores.constructorCama("Cama principal", 10, "Litros", 10, 25.5, 51, "Cm", "Rojo", 5, "Piedra volcánica");
    acuApp.cama1.agregarAgua(100);
    acuApp.tanque1.agregarAgua(987);

```


**3 -** Con el sistema ya instalado... y todo el entorno acuático funcionando. Es hora de incluir los métodos para controlar a nuestros peces y plantas.

- En el constructor de Camas:
    - Añadir un nuevo método para agregar peces que permita definir nombre y clase
    - Agregar un nuevo método para retirar peces (sin perderlos)

- En el constructor de Tanques:
    - Añadir un nuevo método para agregar plantas que permita definir nombre y clase
    - Agregar un nuevo método para retirar plantas (sin perderlas)

```javascript
    var debugMode = true;

    function chivato (tipo, mensaje) {
        if (debugMode) {
            if(tipo == "warn"){
                console.warn(mensaje);
            } else {
                console.log(mensaje)
            }
        }
    };

    var acuApp = acuApp || {};

    // Constructores
    var constructorTanque = function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo) {
        this.nombre = nombre;
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho * largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.dimensionesMedida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.desagueFuncionando = false;
        this.nivelAgua = 0;
        this.peces = {};
        /* Funciones */
        this.agregarPez = function (nombre, clase, peso, espacio, lugar) {
            this.peces[nombre] = {
                tipo:"pez",
                clase: clase,
                peso: peso || 100,
                pesoMedida: "gramos",
                espacio: espacio || 0.05,
                espacioMedida: "m3",
                lugar: lugar || "Tanque principal"
            };
        };

        this.quitarPez = function (nombre) {
            var temp = this.peces[nombre];
            delete this.peces[nombre];
            return temp;
        };

        this.agregarAgua = function(litros){
            this.nivelAgua = this.nivelAgua + litros;
            if(this.nivelAgua >= this.nivelAguaMaximo){
                if(!this.desagueFuncionando){
                    this.desagueFuncionando = true;
                    chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
                }
                chivato("log", "nivel actual: "+this.nivelAgua);
                this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
            }
        };

        this.quitarAgua = function(litros){
            this.nivelAgua = this.nivelAgua-litros;
            if(this.desagueFuncionando){
                this.desagueFuncionando = false;
                chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
            }
            chivato("log", "nivel actual: "+this.nivelAgua);
        };
    };

    var constructorCama = function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo, sustrato) {
        this.nombre = nombre;
        this.capacidad = capacidad;
        this.capacidadMedida = capacidadMedida;
        this.dimensiones = alto * ancho *largo;
        this.alto = alto;
        this.ancho = ancho;
        this.largo = largo;
        this.medida = dimensionesMedida;
        this.color = color;
        this.nivelAguaMaximo = nivelAguaMaximo;
        this.sustrato = sustrato;
        this.desagueFuncionando = false;
        this.nivelAgua = 0;
        this.plantas = {};
        /* Funciones */

        this.agregarPlanta = function (nombre, clase, frutosDisponibles, estadoActual, espacio, lugar) {
        this.plantas[nombre] = {
            nombre: nombre,
            tipo: "planta",
            clase: clase,
            frutosDisponibles: frutosDisponibles,
            estadoActual: estadoActual,
            espacio: espacio || 0.05,
            espacioMedida: "m3",
            lugar: lugar || "Cama principal"
            };
        };

        this.quitarPlanta = function (nombre) {
            var temp = this.plantas[nombre];
            delete this.plantas[nombre];
            return temp;
        };

        this.agregarAgua = function(litros){
            this.nivelAgua = this.nivelAgua + litros;
            if(this.nivelAgua >= this.nivelAguaMaximo){
                if(!this.desagueFuncionando){
                    this.desagueFuncionando = true;
                    chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
                }
                chivato("log", "nivel actual: "+this.nivelAgua);
                this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
            }
        };
        this.quitarAgua = function(litros){
            this.nivelAgua = this.nivelAgua-litros;
            if(this.desagueFuncionando){
                this.desagueFuncionando = false;
                chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
            }
            chivato("log", "nivel actual: "+this.nivelAgua);
        };
    };

	// Pruebas
    acuApp.tanque1 = new constructorTanque("Tanque principal",40, "Litros", 30.5, 25.5, 51, "Cm", "Gris Claro", 2);
    acuApp.cama1 = new constructorCama("Cama principal", 10, "Litros", 10, 25.5, 51, "Cm", "Rojo", 5, "Piedra volcánica");
    acuApp.cama1.agregarPlanta("zanahoria1", "hortaliza", false, "planton");
    acuApp.cama1.agregarPlanta("zanahoria2", "hortaliza", true, "cosechable");
    acuApp.cama1.agregarPlanta("zanahoria3", "hortaliza", false, "semilla");
    acuApp.cama1.agregarPlanta("zanahoria4", "hortaliza", false, "semilla");
    var zanahoriaDescartada = acuApp.cama1.quitarPlanta("zanahoria4");
    acuApp.tanque1.agregarPez("Koi1", "aguas fria", 200);
    acuApp.tanque1.agregarPez("Koi2", "aguas fria", 200);
    acuApp.tanque1.agregarPez("pleco", "invasora", 400, 0.5);
    acuApp.tanque1.agregarPez("pleco2", "invasora", 1000, 1.5);
    var plecoDescartado = acuApp.tanque1.quitarPez("pleco2"); 
```

**4 -** Con todo el sistema en funcionamiento es hora de realizar mediciones para garantizar el correcto desarrollo.
Necesitamos mejorar el método de agregar agua para poder incluir como parámetros opcionales las propiedades del agua.
- Propiedades del agua: 
	- Nitratos(NO3 mg/l)
	- Nitritos (NO2 mg/l)
	- Dureza Sales (GH)
	- Carbonatos (KH)
	- Ph (Ph)
	- Cloro (CL2 mg/l)

Ademas... queremos saber el estados de cada tanque y cama usando un método que nos facilite toda la información por consola. 
Incluyendo:
- Estado del agua incluyendo cantidad y parámetros
- total de peces y total por tipo (solo en tanques)
- total de hortalizas y total por tipo (solo en camas)

Nota: *For... in* te resultará de gran utilidad.

- Ejemplo Cama
```
================================
Estado del Agua (Cama principal)
================================
Agua disponible: 5/5l
Nitratos(NO3): 10mg/l
Nitritos(NO2): 0.5mg/l
Dureza de sales(GH): >7ºd
Carbonatos(KH): 6ºd
Ph(PH): 7.2
Cloro(CL2): 0.2mg/l
================================
Estado de las Plantas
================================
Total Hortalizas: 3
```

- Ejemplo Tanque
```
================================
Estado del Agua (Tanque principal)
================================
Agua disponible: 2/2l
Nitratos(NO3): 25mg/l
Nitritos(NO2): 0.5mg/l
Dureza de sales(GH): >14ºd
Carbonatos(KH): 3ºd
Ph(PH): 8
Cloro(CL2): 0.4mg/l
================================
Estado de los Peces
================================
Total de Agua Fria: 2
Total de Invasores: 1
================================
```

```javascript
    var debugMode = true;

	function chivato (tipo, mensaje) {
	    if (debugMode) {
	        if(tipo == "warn"){
	            console.warn(mensaje);
	        } else {
	            console.log(mensaje);
	        }
	    }
	}

	var acuApp = acuApp || {};

	// Constructores
	var constructorTanque = function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo) {
	    this.nombre = nombre;
	    this.capacidad = capacidad;
	    this.capacidadMedida = capacidadMedida;
	    this.dimensiones = alto * ancho * largo;
	    this.alto = alto;
	    this.ancho = ancho;
	    this.largo = largo;
	    this.dimensionesMedida = dimensionesMedida;
	    this.color = color;
	    this.nivelAguaMaximo = nivelAguaMaximo;
	    this.desagueFuncionando = false;
	    this.nivelAgua = 0;
	    this.peces = {};
	    /* Funciones */
	    this.agregarPez = function (nombre, clase, peso, espacio, lugar) {
	        this.peces[nombre] = {
	            tipo:"pez",
	            clase: clase,
	            peso: peso || 100,
	            pesoMedida: "gramos",
	            espacio: espacio || 0.05,
	            espacioMedida: "m3",
	            lugar: lugar || "Tanque principal"
	        };
	    };

	    this.quitarPez = function (nombre) {
	        var temp = this.peces[nombre];
	        delete this.peces[nombre];
	        return temp;
	    };

	    this.agregarAgua = function(litros, nitratos, nitritos, durezaSales, carbonatos, ph, cloro){
	        this.calidadAgua = this.calidadAgua || {};
	        // Nitratos
	        this.calidadAgua["nitratos"] = this.calidadAgua["nitratos"] || {};
	        this.calidadAgua["nitratos"]["valor"] = nitratos || 10;
	        this.calidadAgua["nitratos"]["medida"] = "mg/l";
	        this.calidadAgua["nitratos"]["simbolo"] = "NO3";
	        // Nitritos
	        this.calidadAgua["nitritos"] = this.calidadAgua["nitritos"] || {};
	        this.calidadAgua["nitritos"]["valor"] = nitritos || 0.5;
	        this.calidadAgua["nitritos"]["medida"] = "mg/l";
	        this.calidadAgua["nitritos"]["simbolo"] = "NO2";
	        // Dureza de Sales
	        this.calidadAgua["dureza de sales"] = this.calidadAgua["dureza de sales"] || {};
	        this.calidadAgua["dureza de sales"]["valor"] = durezaSales || ">7ºd";
	        this.calidadAgua["dureza de sales"]["medida"] = "N/A";
	        this.calidadAgua["dureza de sales"]["simbolo"] = "GH";
	        // Carbonatos
	        this.calidadAgua["carbonatos"] = this.calidadAgua["carbonatos"] || {};
	        this.calidadAgua["carbonatos"]["valor"] = carbonatos || "6ºd";
	        this.calidadAgua["carbonatos"]["medida"] = "N/A";
	        this.calidadAgua["carbonatos"]["simbolo"] = "KH";
	        // PH
	        this.calidadAgua["ph"] = this.calidadAgua["ph"] || {};
	        this.calidadAgua["ph"]["valor"] = ph || 7.2;
	        this.calidadAgua["ph"]["medida"] = "N/A";
	        this.calidadAgua["ph"]["simbolo"] = "PH";
	        // Cloro (CL2 mg/l)
	        this.calidadAgua["cloro"] = this.calidadAgua["cloro"] || {};
	        this.calidadAgua["cloro"]["valor"] = cloro || 0.2;
	        this.calidadAgua["cloro"]["medida"] = "mg/l";
	        this.calidadAgua["cloro"]["simbolo"] = "CL2";
	        // Manejo de caudal
	        this.nivelAgua += litros;
	        if(this.nivelAgua >= this.nivelAguaMaximo){
	            if(!this.desagueFuncionando){
	                this.desagueFuncionando = true;
	                chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
	            }
	            chivato("log", "nivel actual: "+this.nivelAgua);
	            this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
	        }
	    };

	    this.quitarAgua = function(litros){
	        this.nivelAgua = this.nivelAgua-litros;
	        if(this.desagueFuncionando){
	            this.desagueFuncionando = false;
	            chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
	        }
	        chivato("log", "nivel actual: "+this.nivelAgua);
	    };

	    this.calcularFrios = function(){
	        var numero = 0;
	        for (var key in this.peces){
	            if(this.peces[key].clase == "aguas fria"){
	                numero++;
	            }
	        }
	        this.peces["total aguas fria"] = numero;
	    };    

	    this.calcularInvasores = function(){
	        var numero = 0;
	        for (var key in this.peces){
	            if(this.peces[key].clase == "invasora"){
	                numero++;
	            }
	        }
	        this.peces["total invasora"] = numero;
	    };

	    this.estadoGeneral = function(){

	        this.calcularInvasores();    
	        this.calcularFrios();

	        var resumenGeneral = "================================\n";
	        resumenGeneral += "Estado del Agua ("+this.nombre+")\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Agua disponible: "+this.nivelAgua+"/"+nivelAguaMaximo+"l\n";
	        resumenGeneral += "Nitratos("+this.calidadAgua["nitratos"]["simbolo"]+"): "+this.calidadAgua["nitratos"]["valor"]+this.calidadAgua["nitratos"]["medida"]+"\n";
	        resumenGeneral += "Nitritos("+this.calidadAgua["nitritos"]["simbolo"]+"): "+this.calidadAgua["nitritos"]["valor"]+this.calidadAgua["nitritos"]["medida"]+"\n";
	        resumenGeneral += "Dureza de sales("+this.calidadAgua["dureza de sales"]["simbolo"]+"): "+this.calidadAgua["dureza de sales"]["valor"]+"\n";
	        resumenGeneral += "Carbonatos("+this.calidadAgua["carbonatos"]["simbolo"]+"): "+this.calidadAgua["carbonatos"]["valor"]+"\n";
	        resumenGeneral += "Ph("+this.calidadAgua["ph"]["simbolo"]+"): "+this.calidadAgua["ph"]["valor"]+"\n";
	        resumenGeneral += "Cloro("+this.calidadAgua["cloro"]["simbolo"]+"): "+this.calidadAgua["cloro"]["valor"]+this.calidadAgua["cloro"]["medida"]+"\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Estado de los Peces\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Total de Agua Fria: "+this.peces["total aguas fria"]+"\n";
	        resumenGeneral += "Total de Invasores: "+this.peces["total invasora"]+"\n";
	        resumenGeneral += "================================\n";

	        console.log(resumenGeneral);
	    };
	};

	var constructorCama = function (nombre, capacidad, capacidadMedida, alto, ancho, largo, dimensionesMedida, color, nivelAguaMaximo, sustrato) {
	    this.nombre = nombre;
	    this.capacidad = capacidad;
	    this.capacidadMedida = capacidadMedida;
	    this.dimensiones = alto * ancho *largo;
	    this.alto = alto;
	    this.ancho = ancho;
	    this.largo = largo;
	    this.medida = dimensionesMedida;
	    this.color = color;
	    this.nivelAguaMaximo = nivelAguaMaximo;
	    this.sustrato = sustrato;
	    this.desagueFuncionando = false;
	    this.nivelAgua = 0;
	    this.plantas = {};
	    /* Funciones */

	    this.agregarPlanta = function (nombre, clase, frutosDisponibles, estadoActual, espacio, lugar) {
	    this.plantas[nombre] = {
	        nombre: nombre,
	        tipo: "planta",
	        clase: clase,
	        frutosDisponibles: frutosDisponibles,
	        estadoActual: estadoActual,
	        espacio: espacio || 0.05,
	        espacioMedida: "m3",
	        lugar: lugar || "Cama principal"
	        };
	    };

	    this.quitarPlanta = function (nombre) {
	        var temp = this.plantas[nombre];
	        delete this.plantas[nombre];
	        return temp;
	    };

	    this.agregarAgua = function(litros, nitratos, nitritos, durezaSales, carbonatos, ph, cloro){
	        this.calidadAgua = this.calidadAgua || {};
	        // Nitratos
	        this.calidadAgua["nitratos"] = this.calidadAgua["nitratos"] || {};
	        this.calidadAgua["nitratos"]["valor"] = nitratos || 10;
	        this.calidadAgua["nitratos"]["medida"] = "mg/l";
	        this.calidadAgua["nitratos"]["simbolo"] = "NO3";
	        // Nitritos
	        this.calidadAgua["nitritos"] = this.calidadAgua["nitritos"] || {};
	        this.calidadAgua["nitritos"]["valor"] = nitritos || 0.5;
	        this.calidadAgua["nitritos"]["medida"] = "mg/l";
	        this.calidadAgua["nitritos"]["simbolo"] = "NO2";
	        // Dureza de Sales
	        this.calidadAgua["dureza de sales"] = this.calidadAgua["dureza de sales"] || {};
	        this.calidadAgua["dureza de sales"]["valor"] = durezaSales || ">7ºd";
	        this.calidadAgua["dureza de sales"]["medida"] = "N/A";
	        this.calidadAgua["dureza de sales"]["simbolo"] = "GH";
	        // Carbonatos
	        this.calidadAgua["carbonatos"] = this.calidadAgua["carbonatos"] || {};
	        this.calidadAgua["carbonatos"]["valor"] = carbonatos || "6ºd";
	        this.calidadAgua["carbonatos"]["medida"] = "N/A";
	        this.calidadAgua["carbonatos"]["simbolo"] = "KH";
	        // PH
	        this.calidadAgua["ph"] = this.calidadAgua["ph"] || {};
	        this.calidadAgua["ph"]["valor"] = ph || 7.2;
	        this.calidadAgua["ph"]["medida"] = "N/A";
	        this.calidadAgua["ph"]["simbolo"] = "PH";
	        // Cloro (CL2 mg/l)
	        this.calidadAgua["cloro"] = this.calidadAgua["cloro"] || {};
	        this.calidadAgua["cloro"]["valor"] = cloro || 0.2;
	        this.calidadAgua["cloro"]["medida"] = "mg/l";
	        this.calidadAgua["cloro"]["simbolo"] = "CL2";
	        // Manejo de caudal
	        this.nivelAgua = this.nivelAgua + litros;
	        if(this.nivelAgua >= this.nivelAguaMaximo){
	            if(!this.desagueFuncionando){
	                this.desagueFuncionando = true;
	                chivato("warn", "Se activó el sistema de desagüe de emergencia en "+this.nombre);
	            }
	            chivato("log", "nivel actual: "+this.nivelAgua);
	            this.quitarAgua(this.nivelAgua-this.nivelAguaMaximo);
	        }
	    };
	    this.quitarAgua = function(litros){
	        this.nivelAgua = this.nivelAgua-litros;
	        if(this.desagueFuncionando){
	            this.desagueFuncionando = false;
	            chivato("log", "Se desactivo el sistema de desagüe de emergencia en "+this.nombre);
	        }
	        chivato("log", "nivel actual: "+this.nivelAgua);
	    };

	    this.calcularHortalizas = function(){
	        var numero = 0;
	        for (var key in this.plantas){
	            if(this.plantas[key].clase == "hortaliza"){
	                numero++;
	            }
	        }
	        this.plantas["total hortalizas"] = numero;
	    };

	    this.estadoGeneral = function(){

	        this.calcularHortalizas();

	        var resumenGeneral = "================================\n";
	        resumenGeneral += "Estado del Agua ("+this.nombre+")\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Agua disponible: "+this.nivelAgua+"/"+nivelAguaMaximo+"l\n";
	        resumenGeneral += "Nitratos("+this.calidadAgua["nitratos"]["simbolo"]+"): "+this.calidadAgua["nitratos"]["valor"]+this.calidadAgua["nitratos"]["medida"]+"\n";
	        resumenGeneral += "Nitritos("+this.calidadAgua["nitritos"]["simbolo"]+"): "+this.calidadAgua["nitritos"]["valor"]+this.calidadAgua["nitritos"]["medida"]+"\n";
	        resumenGeneral += "Dureza de sales("+this.calidadAgua["dureza de sales"]["simbolo"]+"): "+this.calidadAgua["dureza de sales"]["valor"]+"\n";
	        resumenGeneral += "Carbonatos("+this.calidadAgua["carbonatos"]["simbolo"]+"): "+this.calidadAgua["carbonatos"]["valor"]+"\n";
	        resumenGeneral += "Ph("+this.calidadAgua["ph"]["simbolo"]+"): "+this.calidadAgua["ph"]["valor"]+"\n";
	        resumenGeneral += "Cloro("+this.calidadAgua["cloro"]["simbolo"]+"): "+this.calidadAgua["cloro"]["valor"]+this.calidadAgua["cloro"]["medida"]+"\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Estado de las Plantas\n";
	        resumenGeneral += "================================\n";
	        resumenGeneral += "Total Hortalizas: "+this.plantas["total hortalizas"]+"\n";

	        console.log(resumenGeneral);
	    };
	};

	// Pruebas
	acuApp.tanque1 = new constructorTanque("Tanque principal",40, "Litros", 30.5, 25.5, 51, "Cm", "Gris Claro", 2);
	acuApp.cama1 = new constructorCama("Cama principal", 10, "Litros", 10, 25.5, 51, "Cm", "Rojo", 5, "Piedra volcánica");
	acuApp.cama1.agregarPlanta("zanahoria1", "hortaliza", false, "planton");
	acuApp.cama1.agregarPlanta("zanahoria2", "hortaliza", true, "cosechable");
	acuApp.cama1.agregarPlanta("zanahoria3", "hortaliza", false, "semilla");
	acuApp.cama1.agregarPlanta("zanahoria4", "hortaliza", false, "semilla");
	var zanahoriaDescartada = acuApp.cama1.quitarPlanta("zanahoria4");
	acuApp.tanque1.agregarPez("Koi1", "aguas fria", 200);
	acuApp.tanque1.agregarPez("Koi2", "aguas fria", 200);
	acuApp.tanque1.agregarPez("pleco", "invasora", 400, 0.5);
	acuApp.tanque1.agregarPez("pleco2", "invasora", 1000, 1.5);
	var plecoDescartado = acuApp.tanque1.quitarPez("pleco2");
	acuApp.cama1.agregarAgua(100);
	acuApp.tanque1.agregarAgua(987, 25, 0.5, ">14ºd", "3ºd", 8.0, 0.4);
	acuApp.tanque1.estadoGeneral();
	acuApp.cama1.estadoGeneral();
```