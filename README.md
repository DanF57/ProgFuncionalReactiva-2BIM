# ProgFuncionalReactiva-1BIM
## Semana 4
Paradgima Funcional
Valores inmutables
- Las cosas no deberían cambiar
```scala
val = cedula "1103353532"
cedula = "1103353533" //error (No se puede hacer reasignacion)
var = cedula "1103353531" //Var es mutable es una variable
```
Funciones de Orden Superior
- Una funcion que puede asignarse a un valor
```scala
f(x) = -x² + 8x - 12
(x: Double) => -Math.pow(x,2) + 8 * x - 12
val f1 = (x: Double) => -Math.pow(x,2) + 8 * x - 12
f1(12) * 9 / 8 + 3 //Invocacion
((x: Double) => -Math.pow(x,2) + 8 * x - 12)(12) //Funcion sin nombre
```
```scala
def integracion(a:Int, b:Int, f:Double => Double) = { //Recordatorio: la flecha indica que es una función
	 	val intermedio = ((a+b) /2.0)  	//Usar 2.0 para mayor presición
	 	val fa = f(a); 			//; es opcional
	 	val fi = f(intermedio)
		val fb = f(b)
	 	(b - a) *  (fa + 4 * fi + fb) / 6
}
```
- Una función que devuelve una función. 
 Ejem:
Calculadora para sumar números enteros
```scala
def select(option: Char) : (Int, Int) => Double = {
 option match{
	case '+' => (a: Int, b: Int) => a + b
	case '-' => (a: Int, b: Int) => a - b
	case '*' => (a: Int, b: Int) => a * b
	case '/' => (a: Int, b: Int) => a / b.toDouble
	case _ => (a: Int, b: Int) => 0 / (a+b)
	}
}
//Forma Directa
select('+')(2, 1) 
//Dos Pasos
val operation = select('+')
operation(2, 1)
```
- Obtener Datos de Secuencias 
<br />isEven funcion auxliar, ayudan a escribir fácilmente la función countEven
<br />En código sería:

```scala
//Op1 
val isEven = ( k: Int ) => if( k % 2 == 0) 1 else 0

//Op2 
def isEven ( k:Int ) : int = ( k % 2 ) match {
	 	case 0 => 1
	 	case _ => 0
	}

	def countEven( s : List[Int] ): Int = s.map( isEven ).sum
//----------------------------------------------------------------------------------------
	def countEven( s : List[Int] ): Int ={
		def isEven ( k:Int ) : int = ( k % 2 ) match {
	 	case 0 => 1
	 	case _ => 0
		}
	 s.map(isEven ).sum
	}
countEven(List(1,2,3,2,2,2,))
```
```scala
//En Scala se declara una Lista 
List[ Int ]
List( 1, 2, 3 )
List( 1, 2, 3 ).sum

List(1,2,3).map (x=> x * x + 100 * x)
//res1: List[Int] = List(101, 204, 309)

def func1( x: Int ) : Int = x * x + 100 * x
List(1,2,3).map(func1)
//res3: List[Int] = List(101 , 204, 309)

List(1,2,3) mao func1 //dotless infix
```

- Ejemplo
```scala
val nums = List(1, 2, 3)
nums.map(x => x + 1)

def add1(a : Int) : Int = a + 1
nums.map(add1)
nums.map(x => add1(x))
nums.map(add1(-))

val sumaDos = (a: Int, b: Int) => a + b
nums.map(sumaDos) //Error método sobrecargado
nums.map(x => sumaDos(x , x))
```
Ejercicios Propuestos Semana 4:
<br />Mapear una lista de cadenas de texto a lista de enteros que representan la longitud del texto
```scala
//Op1
val cadenas = List("utpl", "daniel", "git", "")
cadenas.map(x => x.length())
      // : List[Int] = List(4, 6, 3, 0)
//Op2
List("utpl", "daniel", "git", "").map(x => x.length())
      // : List[Int] = List(4, 6, 3, 0)
```
  <br />Dada una lista de numeros enteros, desarrorollar las funciones necesarias que le permitan contar cuandtos elementos
```scala
val nums = List(1, 3, 3, 4, 1, 10, 11)
nums.length //Int = 7
nums.size //Int = 7
nums.count(Int => true) //Int = 7
nums.count(_ == 3) //Int = 2
```
