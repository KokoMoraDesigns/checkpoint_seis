# Python,  APIs &  bases de datos

## Clases de Python

Una clase consiste en una 'plantilla' para crear diferentes objetos que posean unos atributos y métodos determinados. 

<br>

**Sintaxis básica:**

    class Clase:
	    atributo1: ''
	    atributo2: ''
	    atributo3: ''
	    atributo4: ''
	    
	objeto = Clase()

 1. Definimos el nombre de la clase (Clase), la primera letra de la palabra en mayúsculas.
 2. Definimos los atributos de la clase.
 3. Creamos los objetos necesarios para almacenar  en ellos la clase.

**Por ejemplo:**


    class Ropa:
	    prenda = 'vestido'
	    talla = 48
	   
	    
	Ropa.prenda --> salida : 'vestido'
	Ropa.talla --> salida: 48
	
	prenda = Ropa.prenda
	talla = Ropa.talla
	
	
	def comprar():
		return f'quiero un(a) {prenda} rojo/a de la talla {talla}'
		
	comprar() --> salida: 'quiero un(a) vestido rojo/a de la talla 48'


En el ejemplo anterior hemos definido la clase Ropa, donde:

 - *Ropa* --> el nombre de la clase
 - *prenda*, *talla* --> los atributos de dicha clase
 
Después, hemos accedido a los atributos de la clase mediante *Ropa.prenda* y los hemos almacenado en dos variables diferentes (*prenda*, *talla*), para poder ser capaces de utilizarlos en la función *comprar()*.


Miremos ahora este **otro ejemplo**:

    Primero, definimos la clase, con la palabra reservada 'class' y el nombre que le queramos aplicar a la clase:
    
    class Ropa:
    
	    def __init__(self, prenda, talla):
		    self.prenda = prenda
		    self.talla = talla
	    
		def comprar(self):
			return f'quiero un(a) {self.prenda} rojo/a de la talla {self.talla}'
			
			
	
	Después, creamos un objeto de la clase:
	    
	    comprar_primero = Ropa('vestido', 48)
	    
	    
	    
	Y, finalmente, llamamos al método ('comprar') en el objeto ('comprar_primero'):
	    
	    comprar_primero.comprar()
	    
	    
	salida --> 'quiero un(a) vestido rojo/a de la talla 48'


	   
Podríamos haber creado un segundo objeto con los atributos  *'sudadera', '36'*, un tercero, y un cuarto, y un quinto... cada uno de ellos con diferentes atributos. 

Es decir, una clase puede derivar en diferentes objetos compuestos por atributos distintos, pero todos ellos tendrán en común la estructura con la que hayamos construido la clase. Esto nos permite crear un código ordenado y reutilizable.

<br>

### Herencia de clases

Consiste en crear una nueva clase basada en una clase que ya existe, es decir, heredando los atributos y los métodos de la clase ya existente. La clase original pasaría a llamarse 'clase base' o 'superclase' y la clase nueva se llamaría 'clase derivada' o 'subclase'.

**Sintaxis básica:**

    class ClaseBase:
	    def metodo_clase_base(self):
		    return 'operación del método'
		    
	class ClaseDerivada(ClaseBase):
		def metodo_clase_derivada(self):
			super().metodo_clase_base()
			return 'operación del método-subclase'


**Por ejemplo:**

    CLASE BASE:
    
    class Ropa:
    
	    def __init__(self, prenda, color, talla):
		    self.prenda = prenda
		    self.color = color
		    self.talla = talla
		    
	    
		def comprar(self):
			return f'quiero un(a) {self.prenda} {self.color} de la talla {self.talla}'
			
			
			
	CLASE DERIVADA:
	
	class PersonalShopper(Ropa):
				def __init__(self, prenda, color, talla, shopper, cliente):
					super().__init__(prenda, color, talla)
					self.shopper = shopper
					self.cliente = cliente
					
					
				def compra_confirmada(self):
				
					return f'Hola, {self.shopper}, cómprale a {self.cliente} un(a) {self.prenda} {self.color} de la talla {self.talla}, por favor. Muchas gracias.'
					
	ropa_uno = PersonalShopper('vestido', 'rojo', 48, 'persona uno', 'persona dos')
	
	ropa_uno.compra_confirmada()



En este nuevo ejemplo, la clase derivada *PersonalShopper* tiene dos nuevos atributos (*shopper, cliente*) y un nuevo método (*compra_confirmada*), además, hemos traído el método de la clase base mediante la llamada *super().*, de esta manera, hemos sido capaces de heredar sus atributos.


<br>

### Otras herramientas para las clases de Python 

####  Método \__str()\__

Útil si deseas obtener una cadena que represente un objeto de manera más sencilla para un ojo no informático. 

Sin \__str()\__:

    class Presentacion:
	    def __init__(self, nombre, pasion):
		    self.nombre = nombre
		    self.pasion = pasion
		def presentarme(self): return f'Mi nombre: {self.nombre} y mi pasión: {self.pasion}'
			
			
	primera_persona = Presentacion('Amatxito', 'cocinar')
	
	print(primera_persona) --> salida --> <__main__.Presentacion object at 0x102c635c0>
		

Con  \__str()\__:

    class Presentacion:
	    def __init__(self, nombre, pasion):
		    self.nombre = nombre
		    self.pasion = pasion
		def __str__(self):
			return f'Mi nombre: {self.nombre} y mi pasión: {self.pasion}'
			
			
	primera_persona = Presentacion('Maite', 'leer')
	
	print(primera_persona) --> salida --> Mi nombre: Maite y mi pasión: leer

<br>

#### Método Dunder

Dunder equivale a *double underscore* ( '__') en inglés, y hace referencia a los métodos cuyos nombres empiezan y finalizan con dos guiones bajos, como, por ejemplo, *__init_\_* o *\_\_str\_\_*. Como ya hemos explicado anteriormente, estos métodos se ejecutan automáticamente. Veamos ahora otros métodos Dunder autoexplicativos:

***\_\_len\_\_***

    class Comida:
	    def __init__(self, alimentos):
		    self.alimentos = alimentos
		    
		def __len__(self):
			return len(self.alimentos)
			
			
	buffet = Comida(['croquetas', 'pizza', 'galletas', 'cookies', 'ensalada'])
	
	len(buffet) --> salida --> 5 --> es decir, calculamos la longitud de la lista


<br>

***\_\_getitem\_\_*** , ***\_\_setitem\_\_*** y ***\_\_delitem\_\_***

    class Comida:
	    def __init__(self):
		    self.alimentos = []
		    
		    
		def __getitem__(self, index):
			return self.alimentos[index]
			
		def __setitem__(self, index, value):
			self.alimentos[index] = value
			
		def __delitem__(self, index):
			del self.alimentos[index]
			
	nuestro_buffet = Comida()
	
	nuestro_buffet.alimentos = ['croquetas', 'pizza', 'galletas', 'cookies', 'ensalada']
	
	nuestro_buffet[4] --> getitem: salida --> 'ensalada'
	
	nuestro_buffet[4] = 'crema' --> setitem: salida de nuestro_buffet[4] --> 'crema'
	
	del nuestro_buffet[4] --> delitem: salida de nuestro_buffet.alimentos --> ['croquetas', 'pizza', 'galletas', 'cookies']
	
	Es decir, 'getitem' nos da la información de lo que está registrado bajo el índice que le pidamos, 'setitem' cambia el valor de ese índice, y 'delitem' elimina el registro.
	
	
<br>

 ***\_\_iter\_\_*** y ***\_\_next\_\_***

    class Malta:
    
		def __init__(self, min):
			self.min = min
			self.despensa = 7
			
		def __iter__(self):
			return self
			
		def __next__(self):
			if self.despensa > self.min:
				self.despensa -= 1
				return f'nos quedan {self.despensa} maltas, mami'
			else:
				raise StopIteration
				
	despensa = Malta(5)
	
	for malta in despensa:
		print(malta) --> salida --> nos quedan 6 maltas, mami
									nos quedan 5 maltas, mami
									--> es decir, iteramos sobre la colección
			
<br>



***__add_\_***						

    class Libros:
	    def __init__(self, titulo):
		    self.titulo = titulo
		    
		def __add__(self, nuevo_titulo):
			return Libros(self.titulo + nuevo_titulo.titulo)
			
		def __repr__(self):
			return f"En nuestra librería privada de momento están los libros {self.titulo}."
			
			
	coleccion_uno = Libros('Pirómanas')
	
    añadir = Libros(', Suavidad')
    
    coleccion_definitiva = coleccion_uno + añadir
    
    
    coleccion_definitiva --> salida --> En nuestra librería privada de momento están los libros Pirómanas, Suavidad. 
    --> es decir, nos da la posibilidad de añadir nuevos elementos (o de efectuar sumas numéricas, por ejemplo)


   <br>

#### Llamar a métodos sobre un objeto

Podemos sacar un objeto de una clase, y, a ese objeto, le aplicamos el método que hemos creado. Por ejemplo:

    class Triangulo:
	    def __init__(self, base, altura):
		    self.base = base
		    self.altura = altura
		    
		def area(self):
			return self.base / 2 * self.altura
		
			
	primer_triangulo = Triangulo(7)
	
	area = primer_triangulo.area()
	
	print(f'área: {area}')

<br>

#### Cambiar las propiedades de objetos

Mediante el signo '.' podemos llegar a un atributo en concreto y actualizar su valor, por ejemplo:

    class Aula:
	    def __init__(self, nombre, edad):
		    self.nombre = nombre
		    self.edad = edad
		def saludo(self):
			return f'Mi nombre es {self.nombre} y tengo {self.edad} años'
			
			
	primera_persona = Aula('Koko', 27)
	primera_persona.nombre = 'Maite'

	    
	
Y si utilizamos la palabra clave *del*, eliminamos la propiedad del objeto. Por ejemplo:

    del primera_persona.nombre


<br>

#### Polimorfismo

El *poly*(muchos)*-morf*(forma)*-ismo* hace referencia a los objetos que pueden adoptar diferentes formas, es decir, crea la posibilidad de utilizar objetos que provengan de diferentes clases como si vinieran de una misma superclase, creando contextos diferentes para un mismo objeto. 

**Ejemplo básico:**
    
    class Brioche:
	    def desayuno(self):
		    return 'me gustaría desayunar brioche'
	
		    
	class Tortilla:
		def desayuno(self):
			return 'me gustaría desayunar una tortilla francesa'
			
	def Hambre(alimento):
		return alimento.desayuno()
		
	brioche = Brioche()
	tortilla = Tortilla()
	
	Hambre(brioche) --> salida --> 'me gustaría desayunar brioche'
	Hambre(tortilla) --> salida --> 'me gustaría desayunar una tortilla francesa'

<br>




#### Decorador

Consiste en una función que modifica o amplifica el comportamiento de la función original, pero sin alterar su código.  Para ello, escribimos: '@nombre_del_decorador'.

**Ejemplo básico:**

    *tenemos la función inicial*
    
    def formato_canciones(titulo):
		def canciones():
			tit = titulo()
			titulo_formateado = tit.title()
			return titulo_formateado
		return canciones
			

	*y ahora creamos el decorador, para aplicar la función a otra función, creando (funcionalmente hablando) una tercera función: *

	@formato_canciones
	def primera_cancion():
		return 'de maravisha'
	
	primera_cancion() --> salida --> 'De Maravisha'

<br>

> **OBSERVACIÓN**
> Podemos tener varios decoradores en una misma función. Por ejemplo, si por alguna razón razón quisiéramos separar el título con comas ('De, Maravisha'), podríamos crear otra función con el método *split* y a primera_cancion() pasarle:
> 

     @formato_canciones
     @separar_comas
     def primera_cancion():
    	    return 'de maravisha'


    
<br>

### Método de instancia & método constructor

Usamos el **método de instancia** cuando necesitamos 'que actúe sobre la instancia de una clase', es decir, cuando necesitamos acceder y/o actualizar un valor determinado de una instancia; la manera que tenemos de lograr este acceso es mediante el parámetro *self*. 

**Por ejemplo:**

    class Familia:
	    def __init__(self, nombre, raza):
		    self.nombre = nombre
		    self.raza = raza
		    
		def miembros(self):
			return f'sí, {self.nombre} es de raza {self.raza}'
			
			
		*creamos las instancias de Familia*
			
		miembra1 = Familia('Amatxito', 'humana')
		miembra2 = Familia ('Maite', 'humana')
		miembro3 = Familia ('Jam', 'Pitbull mezcla')
		miembro4 = Familia ('Jolie', 'Chihuahua')
		miembra5= Familia ('Suki', 'Dobermann')
	
		
		
		*llamamos al método de instancia*
		
		miembra2.miembros() --> 'sí, Maite es de raza humana'

El método de instancia sería *miembros()*, y utiliza *self* para acceder a los atributos *nombre* y *raza* de cada instancia.


Cuando creas una instancia de una clase, automáticamente se ejecuta el método constructor (*\__init\__*). 


**Sintaxis básica:**

    class Clase:

		*constructor que será llamado al crear un objeto*
		
	    def __init__(self, primer_atributo, segundo_atributo):
		    self.primer_atributo = primer_atributo
		    self.segundo_atributo = segundo_atributo
		
		
		*método definido en la clase*
		    
		def metodo(self):
			return f'el primer atributo es {self.primer_atributo} y el segundo atributo es {self.segundo_atributo}'

Cuando crees el nuevo objeto, accederás al constructor y este inicializará automáticamente los atributos que le hayas asignado inicialmente (*self*, que es la instancia primera de la clase, la que utilizas para acceder a los atributos y métodos de la clase. 

    *crear el objeto y definir sus valores (__init__ se ejecuta automáticamente*
    
    primer_objeto = Clase(7,7)
    
    (se ha asignado 7 al valor self.primer_atributo y 7 al valor self.segundo_atributo)


    *llamar al método en el objeto*
    
    salida = primer_objeto.metodo()
    
    
    *ya podemos usar el objeto en el programa*

<br>
<br>

 

> **OBSERVACIÓN:**
> 
>  Podemos colocar **atributos opcionales** , por ejemplo:
> 
>     class Libro:
>     
> 	    def __init__(self, titulo, persona_autora, editorial='kakao books'):
> 	    
> 		    self.titulo = titulo
> 		    self.persona_autora = persona_autora
> 		    self.editorial = editorial
> 		    
>     primer_libro = Libro(titulo1, persona1) 
>     
>     *si no especificamos una editorial, automáticamente se colocará la predeterminada: 'kakao books'.*

<br>

## APIs

Una Interfaz de Programación de Aplicaciones trabaja como intermediaria entre los distintos programas de software para intercambiar datos y funcionalidades, es decir, para comunicarse entre sí. De esta manera un desarrollador puede hacer uso de las utilidades de una aplicación externa sencillamente siguiendo un listado de instrucciones que se le haya proporcionado, sin tener por qué llegar a conocer sus engranajes internos.

<br>

> **PROCESO:** 
 > 1. La aplicación (en este contexto, se suele hacer referencia a ella bajo el término de **cliente**)  *envía una solicitud* a la API
 > 
 > 2. La API (en este contexto, se suele hacer referencia a ella bajo el término de **servidor**) sirve de *intermediaria*: acepta la solicitud y la
> procesa 
> 
> 3. La API *responde* la solicitud

<br>

Para la persona usuaria, la API es una parte invisible de las aplicaciones que utiliza diariamente (Instagram, Tik Tok, Twitter, Lively...), y sin embargo, fundamental, pues asegura las conexiones que sean necesarias para el buen funcionamiento de la aplicación (en el caso de Lively, por ejemplo, para recoger los datos de tu última menstruación; en el caso de Instagram, por ejemplo, para crear un nuevo post).

<br>

**Ejemplo desde la perspectiva de la persona usuaria:**

En un restaurante, te sientas en una mesa donde te servirán la comida, esa mesa se encuentra en un local, y ambos, tanto la mesa como el local, están funcional y estéticamente diseñados para alcanzar tu placer. Por otro lado, en una cocina de dicho local hay personas trabajando para crear tu comida. Y, como enlace entre esas personas y tu mesa, está trabajando el servicio de mesa (la API).

![api](https://media2.dev.to/dynamic/image/width=800,height=,fit=scale-down,gravity=auto,format=auto/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5fgs7e9ib9i8x7labxfh.png)

<br>

**Ejemplo desde la perspectiva de la persona desarrolladora:**

En un automóvil, los pedales, las palancas, los botones, y el volante (es decir, la API), hacen posible que la persona que lo conduce pueda hacerlo funcionar y manejarlo según su necesidad sin tener que conocer el funcionamiento del motor.

<br>

### Los tres verbos de API

Los verbos primarios de una API (llamados **verbos HTTP** o **métodos HTTP**) son GET, POST y PUT, aunque también vamos a hablar de DELETE, otro verbo muy importante e incluido en las operaciones CRUD (Create, Read, Update, Delete). Estos verbos señalan qué operación deseas aplicar sobre un recurso determinado en una API.

**GET** (read): es el verbo que usamos para sacar información del servidor. Por ejemplo, si en un blog consultamos todas las publicaciones que se han guardado bajo la etiqueta *comida*, estamos haciendo uso del verbo GET. Se considera que es una operación segura, o idempotente, porque usarla no genera ningún cambio en el servidor: no importa el número de veces que la apliquemos, el resultado siempre será el mismo.

**POST** (create): es el verbo que usamos para crear un nuevo recurso en el servidor. Por ejemplo, si administras un blog, le das a 'nueva publicación', escribes el contenido que deseas, y guardas esa nueva publicación, estás creando un nuevo recurso gracias a las utilidades del verbo POST. No es una operación idempotente / segura porque, cada vez que la utilizas, crea un nuevo registro en el servidor.

**PUT** / **PATCH** (update): son los verbos que usamos para actualizar un recurso que ya existe en el servidor. Hacemos uso de PUT para *reemplazar* un recurso entero, con todos sus atributos, y de PATCH para *modificar parcialmente* un recurso. Por ejemplo, si vuelves sobre un texto que publicaste el mes pasado y decides editarlo y cambiarle el título. También se la considera una operación no idempotente / no segura.

<br>

> **MEJORES PRÁCTICAS:**
> En algunas APIs, si el recurso al que haces referencia al usar el verbo PUT no existe, el servidor lo va a crear, es decir, va a actuar como si estuvieras usando el verbo POST.  No obstante, es recomendable que, si quieres crear un nuevo recurso, utilices POST.

<br>


**DELETE** (delete): es el verbo que usamos para eliminar un recurso del servidor. Por ejemplo, vuelves a esa publicación del mes pasado y decides que ya no deseas que forme parte de tu blog. También se la considera una operación no idempotente / no segura.

<br>

**Estructura básica:**

Para gestionar los verbos HTTP usarás una URL similar a la siguiente: 

`https://api.servidor.com/coleccion`

Donde *servidor*  equivale al servidor que estás utilizando (devcamp.space, por ejemplo), y *colección* al conjunto de recursos con el que estás trabajando (usuarios, portfolio, publicaciones... por ejemplo).

<br>



### Postman

Se trata de una aplicación que permite a los desarrolladores probar las aplicaciones o páginas web que estén creando y se conecten a APIs. Sus funciones se dividen en las siguientes:

**Solicitudes**:  permite simular las interacciones con una API al utilizar los verbos HTTP.

**Colecciones**: permite almacenar y organizar las solicitudes anteriores en diferentes conjuntos de solicitudes.

**Entornos**: permite configurar diversos entornos (prueba y producción, desarrollo...) y variar entre ellos, lo que posibilita el probar tu aplicación en contextos distintos sin tener que hacer ningún cambio manual de la configuración.

**Documentación de API**: por medio de la información que haya recibido a partir de las peticiones que hayas procesado y las descripciones que hayas incluido al procesarlas, Postman crea la documentación al respecto de forma automática, así como las instrucciones sobre cómo establecer las peticiones a la API según el lenguaje de programación. Muy útil para facilitarles la información sobre el uso de la API a otros desarrolladores en proyectos colaborativos, por ejemplo.

**Monitor**: permite realizar diversas pruebas automatizadas a tu código, y recibirás no solamente el resultado, sino también el tiempo de respuesta que ha sido necesario y el estado HTTP devuelto por el servidor. De esta manera, puedes captar los errores desde el comienzo.

<br>


## Bases de datos SQL y NoSQL

Cuando estás creando una aplicación contarás con una colección de datos (base de datos) que deberás organizar de alguna manera para poder aplicarla a la app. Por ejemplo, un listado de personas suscritas, con sus nombres de usuarios, contraseñas, localización e historial de compras. **SQL (Structured Query Language)** consiste en un sistema que organiza en tablas tu colección de datos (como si fuera la conocida hoja de cálculo Excel, con sus filas y columnas), permitiéndote no solo acceder a la base de datos para realizar consultas sobre ella y administrarla, sino también crear relaciones (por eso se le llama *base de datos relacional*) entre las distintas tablas (por ejemplo, una tabla de usuarios, otra de direcciones, otra de productos vendidos... unidas por el id de cada usuario).

El nombre de SQL indica que es un sistema de datos estructurados, es decir, tienes una tabla cuyas columnas indican los atributos de interés (id, nombre, apellido, información de contacto), y cuyas filas indican el valor de tales atributos. Si haces una consulta relacionándola con una segunda tabla cuyos atributos sean nombre del producto, categoría, etc., obtendrás una tercera tabla con los datos de quién ha comprado qué y cómo puedes contactarle.

![tabla de datos con SQL](https://s33046.pcdn.co/wp-content/uploads/2018/03/word-image-27.png)

Por el otro lado, una base de datos **No SQL** (**Not Only SQL** ) almacena y administra los datos de una manera distinta: no estructurada, no relacional, y más flexible. El Big Data y la exigencia de las nuevas aplicaciones de tener un sistema que permita el seguimiento de recursos en tiempo real ha derivado en la necesidad de procesar grandes cantidades de datos provenientes de diferentes fuentes, y con un tráfico constante. NoSQL nos permite almacenar todos estos datos, y en diferentes tipos de formatos, que incluyan, por ejemplo, imágenes y videos. Por ello, es un sistema más flexible que permite almacenar los datos, en lugar de solamente en tablas, en colecciones como pares de clave-valor o documentos. 

![base de datos con NoSQL](https://learn.microsoft.com/es-es/azure/architecture/data-guide/big-data/images/document.png)

Por ejemplo, si quieres guardar los trabajos que ha tenido un usuario, puedes hacer:

     { 
	     ..... 
	     'trabajos': ['x', 'y', 'z', 'a'] 
	     ..... 
	 }
	 
En una base de datos SQL tendrías que crear una nueva fila por cada tipo de empleo, lo que crearía repeticiones innecesarias y un resultado menos ordenado, heterogéneo, escalable, y eficiente. 

Las bases de datos NoSQL son las que le permiten a nuestros servicios de *streaming* que nos recomienden nuevas series o nuevas películas en función de cuánto hayamos disfrutado (o no) las que hemos visto anteriormente, que nos ordenen en una lista las producciones que tenemos pendientes, y que nos ordenen en otra lista las que ya hemos empezado a ver. También son las que hacen posible el alto tráfico diario de videos e imágenes que tienen aplicaciones como Tik Tok, Instagram, YouTube, o Snapchat sin afectar a la latencia.

La base de datos NoSQL más popular a día de hoy es *MongoDB*, mientras que la base de datos SQL más popular a día de hoy es *MySQL*.

<br>
<br>
<br>

> Written by     [Maite Ekhiñe Mora]


