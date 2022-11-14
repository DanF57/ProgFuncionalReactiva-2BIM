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
## Semana 5
```scala
def is Even(k: Int) : Int = ( k % 2 ) match {
	case 0 => 1
	case _ => 0
}
def count Even (s: List[Int]): Int = s.map(isEven).sum

def countEven( s: List[Int] ) : Int = {
	def isEven(k: Int) : Int = (k%2) match {
	case 0 => 1
	case _ => 0
}
s.map(isEven).sum
```
Ejercicio de mapeo
- Ej1
```scala
val names = List( "Leo", "Cristiano", "Enner", "Felipe")
names.map(_.length())
```
- Ej2
```scala
val numbers = List(3, 4, 7, 11, 12)
val isPrime = (nro : Int) => ( 2 to nro -1 ).forall( nro % _ != 0 )
numbers.map(isPrime(_) match{
    case true => 1
    case false => 0
}).sum
```
Filtrar y truncar secuencias
- Ejemplos
```scala
val nums = List(6, 8, 7, 11, 28, 11)
nums.max
nums.min
nums.size
```
- exists filter takeWhile -> Predicados - función que devuelve valor lógico(boolean)
- Rangos
<br /> a to b => a<= x <=b
<br /> a until b => a<= x < b

Forall - Exists - TakeWhile - Filter
```scala
def isPrime(nro: Int) : Boolean = (2 until nro).forall(nro % _ != 0)
//forall devuelve true si todos los valores de la lista son true
```
```scala
def isPrime(nro: Int) : Boolean = !(2 until nro).exists(nro % _ == 0)
//exists devuelve true si uno de los valores de la lista es true
```
```scala
//filter -> devuelve una lista que únicamente contiene los valores que cumplen con el predicado
List( 1, 2, 3, 4, 5 ).filter( k => k % 3 != 0 )
```
```scala
//takeWhile -> trunca la lista hasta que encuentra el valor del predicado
List( 1, 2, 3, 4, 5 ).takeWhile( k => k % 3 != 0 )
```
Map/Reduce
  <br />transformar - map, filter, etc.
  <br />agregar - devuelve valor unico - sum, product, forall, max, etc.
- Ej1
```scala
val names = List( "Leo", "Cristiano", "Enner", "Felipe")
names.map(_.length())
```
- Ej2
```scala
val numbers = List(3, 4, 7, 11, 12)
val isPrime = (nro : Int) => ( 2 to nro -1 ).forall( nro % _ != 0 )
numbers.map(isPrime(_) match{
    case true => 1
    case false => 0
}).sum
```
Ejercicio Map y Filter
- Numeros perfectos
```scala
val divP = (n: Int) => (1 until n).filter(div => n % div == 0)
val sumDiv = (n: Int) => (1 until n).filter(div => n % div == 0).sum

nums.filter(nro => nro == sumDiv(nro)).size
nums.filter(nro => nro < sumDiv(nro)).size
nums.filter(nro => nro > sumDiv(nro)).size
```
Ejercicios en Clase
- Factorial escalonado n!! para enteros positivos 8!! = 384
```scala
def factorialEscalonado(n : Int ) : Int  = {
    n % 2 match {
        case 0 => (2 to n by 2).product
        case _ => (1 to n by 2).product
    }
}
factorialEscalonado(8) //res = 384
factorialEscalonado(9)
```
```scala
val numbers = (1 to 20).toList
```
- Contar Pares
```scala
numbers.filter( nro => nro % 2 == 0).size
numbers.count( nro => nro % 2 == 0)
```
- Contar Impares
```scala
numbers.filter( nro => nro % 2 != 0).size
numbers.count( nro => nro % 2 != 0)
```
- Contar Primos
```scala
def contarPrimos(nros : List[Int]) : Int = {
    val isPrime = (n : Int) => (2 until n).forall(n % _ != 0)
    //nros.filter(isPrime).size
    nros.count(isPrime)
}
contarPrimos(numbers)
```
- Presentar 3 factores
```scala
def tresFactores(nros : List[Int]) : List[Int] ={
    val factores = (n: Int) => (2 until n).filter(n % _ == 0)

    nros.filter(nro => factores(nro).size == 3)
}

tresFactores((1 to 1000).toList)
```
