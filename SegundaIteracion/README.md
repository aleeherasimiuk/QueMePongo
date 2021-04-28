# ¿Qué me pongo? Segunda Iteración

Para continuar con la segunda iteración de QMP, empecé por corregir algunos problemas de la entrega anterior. Por ejemplo, refactoricé en términos de mayor robustez tanto la categoriía, como el tipo de la prenda, como el material; siendo ahora todos éstos un Enum, con opciones finitas, pero validadas por el programador. En cambio la implementación con String, era más flexible pero menos robusta.

----

### 1er Requerimiento


>Especificar qué trama tiene la tela de una prenda (lisa, rayada, con lunares, a cuadros o un estampado).

Para resolverlo basta con con un Enum, siendo consistentes con decisiones anteriores, y con mucho sentido ya que es un conjunto finito de opciones:

```
enum Trama{
  LISA,
  RAYADA,
  LUNARES,
  CUADROS,
  ESTAMPADO
}
```
----

### 2do Requerimiento

> Crear una prenda especificando primero de qué tipo es

Para ello es necesario refactorizar lo hecho en la entrega anterior. Para poder cumplir con ésto, el constructor de Prenda sólo debe recibir el `tipoPrenda` y todo lo demás debe asignarse mediante setters o bien un único método con los atributos faltantes.


### 3er Requerimiento:

>Crear una prenda especificando en segundo lugar los aspectos relacionados a su material (colores, material, trama, etc) para evitar elegir materiales inconsistentes con el tipo de prenda.

Hay una pequeña ambigüedad con respecto a la palabra material. ¿Los colores y la trama dependen del tipo de prenda o bien del material? Suponiendo que dependen del tipo de prenda, el segundo y tercer requerimiento se ven plasmados de la siguiente manera


### 5to Requerimiento

>Poder no indicar ninguna trama para una tela, y que por defecto ésta sea lisa.

Puede validarse por `!= null` en el setter de trama.
Asumo que `LISA` es válida para todo tipo de prenda


```
class Prenda{

  var tipoPrenda
  var material
  var colorPrimario
  var colorSecundario
  var trama

  constructor(tipoPrenda)


  method setMaterial(material) {

    if(!tipoPrenda.materialValido(material))
      lanzarExcepción()

    this.material = material
    
  }

  method setColorPrimario(colorPrimario){

    if(!tipoPrenda.colorPrimarioValido(colorPrimario))
      lanzarExcepción()

    this.colorPrimario = colorPrimario
  }

  method setColorSecundario(colorSecundario){

    if(!tipoPrenda.colorSecundarioValido(colorSecundario))
      lanzarExcepción()

    this.colorSecundario = colorSecundario
  }


  method setTrama(trama){

    if(trama == null){
      trama = Trama.LISA
    } else if(!tipoPrenda.tramaValida(trama)){
      lanzarExcepción()
    }

    this.trama = trama

  }
}

```

----

### 4to Requerimiento

>Guardar un borrador de la la última prenda que empecé a cargar para continuar después

### 6to Requerimiento

> Poder guardar una prenda solamente si esta es válida.


Para estos requerimiento, creé la clase Vestuario, quien será la responsable de validar si una prenda es válida para ser guardada,así como para guardar el borrador de una prenda. El enunciado aclara que es el borrador de la **última** prenda, con lo cual se trata de una variable de tipo `Prenda`.

```
class Vestuario{

  borrador
  prendas[]

  method validarYAgregarPrenda(unaPrenda){

    if(!esPrendaValida(unaPrenda))
      lanzarExcepcion()

    prendas.add(unaPrenda)

  }

  method guardarBorrador(unaPrenda){
    this.borrador = unaPrenda
  }


  method esPrendaValida(unaPrenda){

    //TODO
  
  }
}
```
---




