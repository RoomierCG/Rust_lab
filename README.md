# Introducción a Rust

El ecosistema de Rust está compuesto:

- **rustc**: Es el compilar de rust, que convierte .rs en archivos binarios
<br>

- **cargo**: Es el gestor de dependencias de Rust, descarga las dependencias que se encuentran en <a>https://crates.io</a> y se las enviara a `rustc` cuando construyes tu proyecto. `cargo` trae incorporado un proceso de test embebido para ejecutar test unitarios
<br>

- **rustup**: herramienta de rust que se usa para instalar y actualizar `rustc` y `cargo` cuando salen nuevas versiones, adicionalmente, también descarga la documentación de librerías estándar. Puedes tener varias versiones de rust y cambiar entre ellas con esta herramienta. Para consultar una pequeña introducción a rust puedes usar el siguiente comando `rustup docs --book`
<br>

## Usando Cargo
----------

Nuestra herramienta principal para trabajar será cargo, su uso está estandarizado por los desarrolladores, ya que contiene las herramientas para trabajar con rust. 

> Para añadir dependencias a tu proyecto has de manipular el fichero Cargo.toml. Cuando ejecutes comandos `cargo` se descargaran automáticamente incluidas sus dependencias. 

Te enseño el uso de los comandos principales:

- **`cargo new <example_name>`** Crea un nuevo proyecto rust
<br>

- **`cargo run`** Compila y ejecuta el proyecto
<br>

- **`cargo check`** Comprobara rápidamente si tu proyecto contiene algún tipo de error
<br>

- **`cargo build`** Compilara sin ejecutar el proyecto. Encontrarás el fichero compilado en `target/debug/` en una compilación normal en debug. Si quieres construir una version optimizada para producción del proyecto deberás usar el comando `cargo build --release`, este fichero compilado se encontrara en la carpeta `target/release/`
<br>



## Sintaxis básica de Rust
 
### Anatomía de un programa Rust
----------

- La función `main` es especial, es lo primero que se ejecuta en cualquier programa de Rust, puedes añadir parámetros insertándolos en los `()`.
- Las funciones se crean usando `fn`.
- Los bloques de código se cierran usando `;`.
- Los Strings de Rust son de codificación UTF-8 y pueden contener cualquier carácter Unicode.
<br>

Veamos un ejemplo usando estos conceptos escribiendo un clásico, ¡Hola, mundo!

```rust
fn main() {
    println!("¡Hola, mundo!")
}
```

Hemos añadido un nuevo concepto es esta línea que es `println!()`, esta es la encargada de pintar en nuestra consola aquello que le insertemos, ahora expliquemos unas cosas importantes.

1. las indentaciones en rust usan 4 espacios, no un tab.
2. `println!()` llama a una **macro**, si se hubiera llamado a una función hubiéramos usado `println()` sin el uso de `!`, de momento no explicaremos que es una **macro de rust** hasta más adelante, pero quédate con que si usamos `!` estamos llamando a una macro en vez de una función, las **macros** no siempre siguen las mismas reglas que las funciones
3. Verás `¡Hola, mundo!` string, pasamos este string como argumento a `println!()` y este es pintado en pantalla
<br>

### Hola Cargo
----------

`cargo` es un gestor de paquetes embebido dentro de rust. Muchos Rustaceans usan esta herramienta para manipular sus proyectos, ya que `cargo` gestiona muchas tareas por ti, ya sean construir tu código, descargar librerías en los que tu código dependa y construir estas librerías. (llamamos librerías a todo aquello que tu código dependa)

Vamos a crear un nuevo proyecto rust usando el comando `cargo new <example_name>`

```text
$ cargo new hello_cargo
$ cd hello_cargo
```

Al ejecutar esos comandos, hemos creado un proyecto rust y hemos entrado en él, una vez dentro podremos ver 2 ficheros y un directorio.
<br>

#### **Cargo.toml**
Este fichero es una pieza cable de nuestro proyecto. Este fichero está escrito en el formato TOML (Tom’s Obvious, Minimal Language), que es el formato de configuraciones de cargos, abre este fichero para ver que contiene.

- `[package]` Es la primera sección que nos encontramos y esta indica que es un paquete de configuración, mientras más información añadamos, se añadirán mas secciones.
<br>

- Las siguientes tres líneas índicas la configuración de cargo que necesita para compilar: el nombre del proyecto, las version y la `edición` de Rust que usamos. Hablaremos de la `edición` más adelante
<br>

- La última línea es `[dependencies]`, es el comienzo de las listas de cualquier dependencia que añadas al proyecto. En rust, los paquetes de código son llamados crates.
<br>


 
#### **src/main.rs**
Cargo ha creado un programa "¡"Hola, mundo!", como tal cual vimos en una explicación anterior.

Cargo espera que todo el código fuente viva dentro de la carpeta `src/`. La raíz del proyecto está reservada para ficheros como README, licencias, ficheros de configuración y todo aquello no relacionado con el código.

Si has empezado un proyecto rust que no usa Cargo, puedes convertirlo en uno que lo usa, simplemente tienes que mover el código fuente al directorio `src/` y crear un `Cargo.toml` apropiado a la configuración 
<br>

> Contenido del fichero generado por el comando `cargo new hello_cargo`

```rust
fn main() {
    println!("Hello, World!")
}
```
<br>

#### Building and Running de un proyecto Cargo

Vamos a explicar la diferencia entre `build` y `run`, para ello vamos a usar el proyecto hello_cargo que creamos antes, vamos a ejecutar el siguiente comando para construir el proyecto:
```text
$ cargo build
   Compiling hello_cargo v0.1.0 (C:/projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```

Este comando crear un fichero ejecutable en la siguiente en la ruta `target/debug/hello_cargo` (en windows genera `target\debug\hello_cargo.exe`) donde hayas generado el proyecto. Por defecto cargo genera un `debug build`, puedes ejecutar el archivo compilado usando este comando:

```text
$ ./target/debug/hello_cargo # or .\target\debug\hello_cargo.exe on Windows
Hello, world!
```
<br>

Si todo va bien, debería pintar por pantalla "Hello, world!", ejecutar `cargo build` por primera vez hace que `cargo` genere un fichero en la raíz llamado `Cargo.lock`. Este fichero sirve para llevar un seguimiento de las versiones de las dependencias que tenemos instaladas, este fichero se actualiza automáticamente cada vez que el proyecto es compilado y no es necesario su manipulación. 

Hay otra manera más rápida de conseguir el output del proyecto, usando el siguiente comando:

```text
$ cargo run
   Compiling hello_cargo v0.1.0 (C:/projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.33 secs
     Running `target/debug/hello_cargo`
Hello, world!
```
<br>

Cargo también nos proporciona el comando `cargo check`. Este comando comprueba que se pueda compilar el código perfectamente y crear un ejecutable del mismo:

```text
$ cargo check
   Checking hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.32 secs
```

`cargo check` aveces, este comando en mucho más rápido que `cargo build` ya que nos saltamos el paso de crear el binario, y podemos comprobar que el estado del código es correcto. Usar `cargo check` a medida que vamos desarrollando nuestro código es una buena manera de saber si nuestro proyecto sigue compilando tras los cambios añadidos, muchos Rustaceans usan este comando como buena práctica.

> Por añadir, los comandos de cargo son los mismos independientemente del SO en el que estes desarrollando el código.
>
> Podemos acceder a documentación de las dependencias que hemos descargado mediante el comando 
>`cargo doc --open`

<br>

## Conceptos comunes de la programación

En esta sección se cubrirán conceptos que aparecen en casi todos los lenguajes de programación y como estos funcionan en Rust. Muchos lenguajes de programación tienen en común su núcleo. Ninguno de estos conceptos presentes en esta sección son únicos de Rust, pero hablaremos de ellos más adelante y los usos alrededor de estos mismos.

> **Keywords o palabras reservadas**
> 
> Rust contiene keywords que están reservadas para solo el uso del propio lenguaje. Quédate en mente que estas keywords no se pueden usar como nombres de variables o funciones. Muchas de las keywords tienen un significado especial, y los usarás para realizar ciertas tareas en tus programas Rust, actualmente hay algunas keywords que no tiene funcionalidad, pero serán añadidas en un futuro.

<br>

### Variables y mutabilidad
----------

Por defecto las variables en rust son inmutables. Este es uno de los muchos empujones que Rust te da para que escribas tu código de forma que aproveches la seguridad y la fácil concurrencia que Rust ofrece.

Sin embargo, puedes crear tus variables mutables, vamos a explorar como y por qué Rust te anima a tener inmutabilidad. Cuando una variable es inmutable, una vez que su valor está asociado al nombre este no puede ser modificado. Para mostrar esto revisemos el siguiente código:

```rust
fn main() {
    let x = 5;
    println!("El valor de x es: {x}");
    x = 6;
    println!("El valor de x es: {x}");
}
```
<br>

Si guardas y ejecutas el programa usando `cargo run`. Deberías recibir un mensaje de error con respecto a un error de inmutabilidad, como se muestra en esta salida

```text
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
error[E0384]: cannot assign twice to immutable variable `x`
 --> src/main.rs:4:5
  |
2 |     let x = 5;
  |         -
  |         |
  |         first assignment to `x`
  |         help: consider making this binding mutable: `mut x`
3 |     println!("The value of x is: {x}");
4 |     x = 6;
  |     ^^^^^ cannot assign twice to immutable variable

For more information about this error, try `rustc --explain E0384`.
error: could not compile `variables` due to previous error
```
<br>

Este ejemplo muestra como el compilador te ayuda mostrándote el error. Los errores de compilación pueden ser frustrantes, pero en realidad lo que te significa es que tu programa no es lo suficientemente seguro sea lo que sea que estés creando.

Has recibido el mensaje `cannot assign twice to immutable variable x `, traducido esto seria `no se puede asignar dos veces x a una variable inmutable`, porque has intentado asignado un segundo valor a la variable inmutable x.

Es importante que recibamos errores en tiempo de compilación cuando intentamos cambiar un valor designado como inmutable, ya que esta situación puede causar errores. Si una parte de nuestro código opera bajo la suposición de que un valor nunca cambiará y otra parte de nuestro código cambia ese valor, es posible que la primera parte del código no haga lo que se diseñó para hacer. El compilador de Rust garantiza que cuando se declara que un valor no cambiará, realmente no cambiará. Su código es así más fácil de entender.

Pero la mutabilidad puede ser muy útil, y puede hacer que el código sea más cómodo de escribir. Aunque las variables sean inmutables por defecto, podemos hacerlas mutables añadiendo `mut` delante de la variable.

Cambiemos el anterior código para hacerlo funcionar:

```rust
fn main() {
    let mut x = 5;
    println!("The value of x is: {x}");
    x = 6;
    println!("The value of x is: {x}");
}
```
<br>

Si ejecutamos ahora el código obtendremos lo siguiente:

```text
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished dev [unoptimized + debuginfo] target(s) in 0.30s
     Running `target/debug/variables`
The value of x is: 5
The value of x is: 6
```
<br>

#### **Constantes**

Como las variables inmutables, las constantes son valores asignados que no están permitidos cambiar, existen unas diferencias entre constantes y variables.

Primero, no está permitido el uso de `mut` con las constantes. Las constantes no son inmutables por defecto, ellas siempre son inmutables. Para declarar constantes usas el keyword `const` en vez de `let`, y el tipo de dato tiene que ser declarado.

Las constantes pueden ser declaradas en cualquier scope, incluso el global, lo que las hace útiles para almacenar valores que se usaran en varias piezas de código. La última diferencia es que las constantes solamente pueden fijarse a una expresión constante, no al resultado de un valor que solo podría calcularse en tiempo de ejecución.

Un ejemplo de ello es lo siguiente:
```rust
const TRES_HORAS_EN_SEGUNDOS: u32 = 60 * 60 * 3;
```
<br>

Fíjate en como se ha escrito el nombre de la variable `TRES_HORAS_EN_SEGUNDOS`, han de ir en mayúscula por convención. El compilador es capaz de evaluar un conjunto limitado de operaciones en tiempo de compilación, lo que nos permite elegir escribir este valor de una manera que sea más fácil de entender y verificar, en lugar de establecer esta constante al valor 10,800. 
<br>


#### **Shadowing**

En Rust puedes declarar una nueva variable con el mismo nombre de una existente, algo asi:

```rust
fn main() {
    let x = 5;
    let x = x + 1;
}
```

Los Rustaceans dicen que la primera variable ha sido shadowed por la segunda variable. Esto significa que la segunda variable es que el compilador verá cuando uses el nombre de la variable.

En efecto, la segunda variable eclipsa la primera, asumiendo cualquier uso del nombre de la variable hasta que ella misma sea eclipsada o el scope termine. Añadamos más cosas al código anterior:

```rust
fn main() {
    let x = 5;
    let x = x + 1;
    
    {
        let x = x * 2;
        println!("El valor de x dentro scope interno es: {x}");
    }

    println!("El valor de x es: {x}");
}
```
<br>

En este código el programa asigna a la variable `x` el valor `5`. Después crea otra vez una nueva variable con el nombre `x` repitiendo `let x =` y le asignamos el valor original sumándole `1` dejando que el valor de `x` sea `6`. Después dentro de scope interno usamos otra vez `let` que vuelve hacer shadow a la variable `x` y crea una nueva variable, multiplicando el valor que tenía anteriormente multiplicado por `2` dejando un el resultado de `x` en `12`. Cuando el scope interno termina, el shadowing interno termina dejando el valor de `x` en `6`. Cuando ejecutamos este programa, el output debería ser el siguiente:

```text
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
    Finished dev [unoptimized + debuginfo] target(s) in 0.31s
     Running `target/debug/variables`
El valor de x dentro scope interno es: 12
El valor de x es : 6
```
<br>

Shadowing es diferente a crear variable con la propiedad `mut` porque obtendremos un error de compilación si intentamos reasignar un nuevo valor si nos olvidamos de usar el keyword `let`. 
Usando `let` podemos crear una transformación en el valor de la variable siendo está inmutable después de haber sido transformada.

Otra diferencia con `mut` y shadowing es que estamos creando de una manera efectiva una nueva variable cuando usamos otra vez `let`, podemos cambiar el tipo de valor recusando el mismo nombre de la variable.
Por ejemplo, digamos que nuestro programa le pregunta al usuario que cuantos espacios que se añadan entre un texto introduciendo caracteres de espacio, y luego queremos guardar ese input como un número.

```rust
fn main() {
    let spaces = "    ";
    let spaces = spaces.len();
}
```
<br>

La primera variable `spaces` es de tipo String y la segunda variable `spaces` es de tipo número. Shadowing nos ahorramos tener que inventar nombres diferentes, como por ejemplo crear `spaces_str` y `spaces_num`; en vez de eso, podemos rehusar simplemente `spaces`. Pero si intentamos este mismo código pero usando el keyword `mut` no dará un error de compilación:

```rust
fn main() {
    let mut spaces = "    ";
    spaces = spaces.len();
}
```
<br>

El error que se nos notificara era que no está permitido mutar las variables de tipos:

```text
$ cargo run
   Compiling variables v0.1.0 (file:///projects/variables)
error[E0308]: mismatched types
 --> src/main.rs:3:14
  |
2 |     let mut spaces = "   ";
  |                      ----- expected due to this value
3 |     spaces = spaces.len();
  |              ^^^^^^^^^^^^ expected `&str`, found `usize`

For more information about this error, try `rustc --explain E0308`.
error: could not compile `variables` due to previous error
```
<br>

### Tipos de datos
----------

Veremos dos subconjuntos de tipos de datos: scalar (escalares) y compound (compuestos), acuérdate de que Rust es un lenguaje de tipado estático, lo que significa que necesita saber todos los tipos de datos en tiempo de compilación. Rust puede deducir que tipo queremos usar basándonos en el valor asignado y como se use.

#### **Escalares**

Un tipo de datos escalar representa un **solo** valor, Rust tiene cuatro tipos escalares primarios: Integers, floating-point, numbers, Booleans y characters.

##### Tipo Integer

Un número entero es un número sin componente fraccionario. Tomemos por el ejemplo lo siguiente el tipo **u32**, la declaración de este tipo indica que el valor asociado deberá ser unsigned integer (los tipos signed integers empiezan por **i** en vez de **u**) que ocupa 32 bits de espacio. En la siguiente tabla mostraremos los tipos enteros incorporados en Rust. Podremos usar cualquiera de estas variaciones para declarar un integer.

<br>

| **Tamaño** | **Signed** | **Unsigned** |
|:----------:|:----------:|:------------:|
|   8-bits   |     i8     |      u8      |
|  16-bits   |    i16     |     u16      |
|  32-bits   |    i32     |     u32      |
|  64-bits   |    i64     |     u64      |
|  128-bits  |    i128    |     u128     |
|    arch    |   isize    |    usize     |

<br>

> Te voy a adjuntar los rangos de valores para cada tipo de integer:
>
>- **8 - bits**            
>   - **i8**  -128 a 127
>   - **u8**  0 a 255
>
>- **16 - bits**
>   - **i16**  -32,768 a 32,767
>   - **u16**  0 a 65,535
>
>- **32 - bits**
>   - **i32**  -2,147,483,648 a 2,147,483,647
>   - **u32**  0 a 4,294,967,295
>
>- **64 - bits**
>   - **i64**  -9,223,372,036,854,775,808 a 9,223,372,036,854,775,807
>   - **u64**  0 a 18,446,744,073,709,551,615
>
>- **128 - bits**
>   - **i128**  -170,141,183,460,469,231,731,687,303,715,884,105,728 a 170,141,183,460,469,231,731,687,303,715,884,105,727
>   - **u128**  0 a 340,282,366,920,938,463,463,374,607,431,768,211,455

<br>

Cada variación puede ser signed o unsigned y tienen un tamaño explícito, *signed* o *unsigned* hace referencia a que es exista la posibilidad de números negativos, en otras palabras, Si tus datos pueden ser tanto positivos como negativos entonces el tipo que usaras será **signed**, en cambio, si solo tienes positivos es **unsigned**.

Además, los tipos isize y usize dependen de la arquitectura del ordenador en el que se ejecuta el programa, que se indica en la tabla como "arch": 64 bits si estás en una arquitectura de 64 bits y 32 bits si estás en una arquitectura de 32 bits.

Puedes escribir integers de cualquier forma mostrada en la siguiente tabla. Es posible que desees especificar explícitamente el tipo de número que deseas utilizar. 

Para hacer esto, puedes agregar un "sufijo de tipo" al literal integer, por ejemplo `let number = 57u8`. Además, puedes usar _ como un separador visual para hacer el número más fácil de leer, por ejemplo `let number = 1_000` es lo mismo que `let number = 1000`

<br>

> **Desbordamiento de Integer**
>
> El desbordamiento de Integer es cuando un número es demasiado grande para ser almacenado en un tipo de dato determinado. En Rust, si intentas asignar un valor fuera del rango permitido a una variable, como 256 en un tipo u8 que únicamente acepta valores entre 0 y 255, ocurrirá un desbordamiento de integer. Esto puede resultar en dos comportamientos diferentes, dependiendo del modo en que se compila el programa.
>
> Cuando se compila en modo depuración, Rust incluye verificaciones de desbordamiento de integer que provocan que el programa termine con un error. En cambio, cuando se compila en modo release con la bandera --release, Rust no incluye verificaciones de desbordamiento de integer y en su lugar aplica "two's complement wrapping", es decir, el valor mayor al máximo permitido "rebobina" y se establece como el valor mínimo permitido. Por ejemplo, en un tipo u8, el valor 256 se convierte en 0, el valor 257 en 1 y así sucesivamente.
>
> Es importante tener en cuenta que no se recomienda depender de este comportamiento de rebobinado para manejar el desbordamiento de integer. Para manejar explícitamente la posibilidad de desbordamiento, Rust proporciona varias familias de métodos en su biblioteca estándar para tipos numéricos primitivos:
>
> Wrapping_* métodos: para realizar un rebobinado de integers en todos los modos.
>
> Checked_* métodos: para devolver el valor None si hay desbordamiento.
>
> Overflowing_* métodos: para devolver el valor y un booleano que indica si hubo desbordamiento.
>
> Saturating_* métodos: para "saturar" el valor en los límites máximo y mínimo permitidos.

<br>

##### Tipo Floating-Point

Rust tiene dos tipos primitivos para números decimales llamados "Floating-Point Types": **f32** y **f64**, de 32 y 64 bits respectivamente. El tipo predeterminado es **f64** porque en las CPU modernas es casi tan rápido como **f32,** pero es más preciso. Todos los tipos de números decimales tienen signo y se representan según el estándar **IEEE-754**. **f32** es de precisión simple y **f64** es de doble precisión.

Ejemplo de Floating-points en código:

```rust
fn main() {
    let x := 2.0 //f64

    let y: f32 = 3.0 //f32
}
```

<br>

##### Operaciones numéricas

Rust es un lenguaje de programación que te permite realizar operaciones matemáticas básicas como suma, resta, multiplicación, división y obtener el resto de una división. Si divides dos números enteros, el resultado se trunca hacia cero, es decir, se redondea al número entero más cercano.

En Rust, cada operación matemática se representa mediante un operador y se evalúa como un único valor que se almacena en una variable.

Ejemplo de Operaciones numéricas:

```rust
fn main() {
    // suma
    let sum = 5 + 10; 

    // resta
    let difference = 95.5 - 4.3;

    // multiplicación
    let product = 4 * 30;

    // division 
    let quotient = 56.7 / 32.2;
    let truncated = -5 / 3; // el resultado es -1

    // resto
    let remainder = 43 % 5;
}
```

<br>

##### Tipo Booleano

En Rust, como en la mayoría de los lenguajes de programación, el tipo Booleano tiene dos valores posibles: `true` y `false`. Los valores Booleanos en Rust ocupan un byte de tamaño. Para especificar el tipo Booleano en Rust, se utiliza la palabra bool. Por ejemplo:

```rust
fn main() {
    let x = true;
    let z: bool = false; //Tiene explícitamente la anotación
}
```

<br>

##### Tipo Character

El tipo `char` de Rust es el tipo alfabético más primitivo del lenguaje. Estos son algunos ejemplos de declaración de valores `char`:

```rust
fn main() {
    let c = 'z';
    let z: char = 'ℤ'; // con anotación explícita de tipo
}
```

Debemos especificar literales de caracteres en Rust usando comillas simples, mientras que los literales de cadenas usan comillas dobles. El tipo `char` en Rust tiene un tamaño de cuatro bytes y representa un valor escalar Unicode, lo que significa que puede representar mucho más que solo ASCII. Letras acentuadas, caracteres chinos, japoneses y coreanos, emojis y espacios de ancho cero son valores válidos para `char` en Rust. Los valores escalares Unicode van desde `U+0000` hasta `U+D7FF` y desde `U+E000` hasta `U+10FFF`. Sin embargo, el concepto de "carácter" no existe realmente en Unicode, por lo que tu intuición humana puede no coincidir con la definición de `char` en Rust. Profundizaremos en este tema más adelante

<br>

#### **Compuestos**

Los tipos compuestos pueden agrupar múltiples valores en un solo tipo. Rust tiene dos tipos compuestos primitivos: tuplas y matrices.

##### Tipo Tupla

Una *tupla* es una forma general de agrupar varios valores con diferentes tipos en un solo tipo compuesto. Las tuplas tienen una longitud fija: una vez declaradas, no pueden aumentar ni disminuir de tamaño.

Creamos una tupla escribiendo una lista de valores separados por comas dentro de paréntesis. Cada posición en la tupla tiene un tipo, y los tipos de los diferentes valores en la tupla no tienen que ser iguales. En este ejemplo, hemos añadido anotaciones de tipo opcionales:

```rust
fn main() {
    let tup: (i32, f64, u8) = (500, 6.4, 1);
}
```

<br>

La variable `tup` se vincula a la tupla completa porque una tupla se considera un solo elemento compuesto. Para obtener los valores individuales de una tupla, podemos utilizar coincidencia de patrones (pattern matching) para desestructurar un valor de tupla, de esta manera:

```rust
fn main() {
    let tup = (500, 6.4, 1);

    let (x, y, z) = tup;

    println!("The valor de y es: {y}")
}
```

<br>

Este programa primero crea una tupla y la vincula a la variable `tup`. Luego, utiliza un patrón con `let` para convertir la tupla en tres variables separadas, `x`, `y`, `z`. Esto se llama desestructuración porque descompone la tupla en tres partes. Finalmente, el programa imprime el valor de `y`, que es `6.4.`

También podemos acceder a un elemento de la tupla directamente utilizando un punto (`.`) seguido del índice del valor que queremos acceder. Por ejemplo:

```rust
fn main() {
    let x: (i32, f64, u8) = (500, 6.4, 1);

    let quinientos = x.0;

    let seis_punto_cuatro = x.1;

    let uno = x.2;
}
```

<br>

Este programa crea la tupla `x` y luego accede a cada elemento de la tupla usando sus respectivos índices. Como en la mayoría de los lenguajes de programación, el primer índice en una tupla es 0.

La tupla sin valores tiene un nombre especial, unidad (unit). Este valor y su tipo correspondiente se escriben ambos como `()` y representan un valor vacío o un tipo de retorno vacío. Las expresiones devuelven implícitamente el valor de la unidad si no devuelven ningún otro valor.

<br>

##### Tipo Array

Otra forma de tener una colección de múltiples valores es con un *array* (array). A diferencia de una tupla, todos los elementos de un array deben tener el mismo tipo. A diferencia de los arrays en algunos otros lenguajes, los arrays en Rust tienen una longitud fija.

Escribimos los valores en un array como una lista separada por comas dentro de corchetes:

```rust
fn main() {
    let arr = [1, 2, 3, 4, 5];
}
```

<br>

Los arrays son útiles cuando deseas que tus datos se asignen en la stack (pila) en lugar del heap (montón) o cuando deseas asegurarte de tener siempre un número fijo de elementos. Un array no es tan flexible como el tipo vector, sin embargo. Un vector es un tipo de colección similar proporcionado por la biblioteca estándar que puede crecer o reducirse en tamaño. Si no estás seguro de si usar un array o un vector, lo más probable es que debas usar un vector.

Sin embargo, los arrays son más útiles cuando sabes que el número de elementos no necesitará cambiar. Por ejemplo, si estuvieras utilizando los nombres de los meses en un programa, probablemente usarías un array en lugar de un vector porque sabes que siempre contendrá 12 elementos:

```rust
fn main() {
    let meses =  ["enero", "febrero", "marzo", "abril", "mayo", "junio", "julio",
        "agosto", "septiembre", "octubre", "noviembre", "diciembre"];
}
```

<br>

Escribes el tipo de un array usando corchetes con el tipo de cada elemento, un punto y coma, y luego el número de elementos en el array, de la siguiente manera:

```rust
fn main() {
    let arr: [i32; 5] = [1, 2, 3, 4, 5];
}
```

Aquí, i32 es el tipo de cada elemento. Después del punto y coma, el número 5 indica que el array contiene cinco elementos.

<br>

También puedes inicializar un array para que contenga el mismo valor para cada elemento especificando el valor inicial, seguido de un punto y coma, y luego la longitud del array entre corchetes, como se muestra aquí:

```rust
fn main () {
    let arr: [3:5];
}
```

El array llamado `arr` contendrá `5` elementos que inicialmente tendrán el valor 3. Esto es lo mismo que escribir `let a = [3, 3, 3, 3, 3];` pero de una manera más concisa.

###### Acceso a los elementos del array

Un array es un bloque único de memoria de un tamaño conocido y fijo que se puede asignar en el stack (pila). Puedes acceder a los elementos de un array utilizando indexación, de la siguiente manera:

```rust
fn main() {
    let arr = [1, 2, 3, 4, 5];
    
    let primero = arr[0];
    let segundo = arr[1];
}
```

En este ejemplo, la variable llamada `primero` obtendrá el valor `1` porque ese es el valor en el índice `[0]` del array. La variable llamada `segundo` obtendrá el valor `2` del índice `[1]` en el array.

<br>

###### Acceso invalidó a los datos

Veamos qué sucede si intentas acceder a un elemento de un array que está más allá del final del mismo. Supongamos que ejecutas este código, para obtener un índice de array del usuario:

```rust
use std::io;

fn main() {
    let arr = [1, 2, 3, 4, 5];

    println!("Introduzca un índice del array.");

    let mut index = String::new();

    io::stdin()
        .read_line(&mut index)
        .expect("Error al leer la linea");

    let index: usize = index
        .trim()
        .parse()
        .expect("El indice asignado no es número");

    let element = arr[index];

    println!("El valor del indice {}: {}", index, element);
}
```

<br>

Este código se compila correctamente. Si ejecutas este código usando `cargo run` e ingresas `0`, `1`, `2`, `3` o `4`, el programa imprimirá el valor correspondiente en ese índice del array. Sí, en cambio, ingresas un número que sobrepasa el final del array, como 10, verás una salida como esta:

```text
thread 'main' panicked at 'index out of bounds: the len is 5 but the index is 10', src/main.rs:19:19
note: run with RUST_BACKTRACE=1 environment variable to display a backtrace
```

<br>

El programa resultó en un error en tiempo de ejecución en el punto de usar un valor no válido en la operación de indexación. El programa salió con un mensaje de error y no ejecutó la declaración final println!. Cuando intentas acceder a un elemento usando indexación, Rust verificará que el índice que has especificado sea menor que la longitud del array. Si el índice es mayor o igual a la longitud, Rust entrará en pánico. Esta verificación debe realizarse en tiempo de ejecución, especialmente en este caso, porque el compilador no puede saber qué valor ingresará un usuario cuando ejecute el código más adelante.

Este es un ejemplo de los principios de seguridad de la memoria de Rust en acción. En muchos lenguajes de bajo nivel, este tipo de verificación no se realiza, y cuando proporcionas un índice incorrecto, se puede acceder a memoria no válida. Rust te protege contra este tipo de error al salir inmediatamente en lugar de permitir el acceso a la memoria y continuar. El Capítulo 9 analiza más sobre el manejo de errores en Rust y cómo puedes escribir código legible y seguro que no entre en pánico ni permita el acceso a memoria no válida.
