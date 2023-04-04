# Introducción a Rust
----------

El ecosistema de Rust esta compuesto:

- **rustc**: Es el compilar de rust, que combierte los .rs en archivos binarios
<br>

- **cargo**: Es el gestor de dependencias de Rust, descarga las dependencias que se encuentran en <a>https://crates.io</a> y se las enviara a `rustc` cuando contruyes tu proyecto. `cargo` trae incorporado un proceso de test embebido para ejecutar test unitarios
<br>

- **rustup**: herramienta de rust que se usa para instalar y actualizar `rustc` y `cargo` cuando salen nuevas versiones, adicionalmente, tambien descarga la documentación de librerías estandar. Puedes tener varias versiones de rust y cambiar entre ellas con esta herramienta. Para consultar una pequeña introducción a rust puedes usar el siguiente comando `rustup docs --book`
<br>

#### Usando Cargo

Nuestra herramienta principal para trabajar sera cargo, su uso esta estandarizado por los desarrolladores ya que contiene las herramientas para trabajar con rust. 

> Para añadir dependencias a tu proyecto has de manipular el fichero Cargo.toml. Cuando ejecutes comandos `cargo` se descargaran automaticamente incluidas sus dependencias. 

Te enseño el uso de los comandos principales:

- **`cargo new <example_name>`** Crea un nuevo proyecto rust
<br>

- **`cargo run`** Compila y ejecuta el proyecto
<br>

- **`cargo check`** Comprobara rápidamente si tu proyecto contiene algún tipo de error
<br>

- **`cargo build`** Compilara sin ejecutar el proyecto. Encontraras el fichero compilado en `target/debug/` en una compilación normal en debug. Si quieres construir una version optimizada para producción del proyecto deberas usar el comando `cargo build --release`, este fichero compilado se encontrara en la carpeta `target/release/`
<br>



## Sintaxis básica de Rust
 
#### Anatomía de un programa Rust
----------

- La función `main` es especial, es lo primero que se ejecuta en cualquier programa de Rust, puedes añadir parámetros insertándolos en los `()`.
- Las funciones se crean usando `fn`.
- Los bloques de código se cierran usando `;`.
- Los Strings de Rust son de codificación UTF-8 y pueden contener cualquier carácter Unicode.
<br>

Veamos un ejemplo usando estos conceptos escribiendo un clásico, ¡Hola, mundo!

```rust:
    fn main() {
        println!("¡Hola, mundo!")
    }
```

hemos añadido un nuevo concepto es esta linea que es `println!()`, esta es la encargada de pintar en nuestra consola aquello que le insertemos, ahora expliquemos unas cosas importantes.

1. las identaciones en rust usan 4 espacios, no un tab.
2. `println!()` llama a una **macro**, si se hubiera llamado a una función hubieramos usado `println()` sin el uso de `!`, de momento no explicaremos que es una **macro de rust** hasta mas adelante, pero quedate con que si usamos `!` estamos llamando a una macro en vez de una función, las **macros** no siempre siguen las mismas reglas que las funciones
3. Veras `¡Hola, mundo!` string, pasamos este string como argumento a `println!()` y este es pintado en pantalla
<br>

#### Hola Cargo
----------

`cargo` es un gestor de paquetes embebido dentro de rust. Muchos Rustaceans usan este herramienta para manipular sus proyectos ya que `cargo` gestiona muchas tareas por ti, ya sean construir tu código, descargar librerías en los que tu código dependa y construir estas librerías. (llamamos librerías a todo aquello que tu código dependa)

Vamos a crear un nuevo proyecto rust usando el comando `cargo new <example_name>`

```cmd:
$ cargo new hello_cargo
$ cd hello_cargo
```

Al ejecutar esos comandos, hemos creado un proyecto rust y hemos entrado en el, una vez dentro podremos ver 2 ficheros y un directorio.
<br>

###### Cargo.toml
este fichero es una pieza cable de nuestro proyecto. Este fichero esta escrito en el formato TOML (Tom’s Obvious, Minimal Language),que es el formato de configuraciones de cargos, abre este fichero para ver que contiene.

- `[package]` Es la primera sección que nos encontramos y esta indica que es un paquete de configuración, mientras mas información añadamos, se añadirán mas secciones.
<br>

- Las siguientes tres lineas indicas la cofiguración de cargo que necesita para compilar: el nombre del proyecto, las version y la `edición` de Rust que usamos. Hablaremos de la `edición` más adelante
<br>

- La ultima linea es `[dependencies]`, es el comienzo de las lista de cualquier dependencia que añadas al proyecto. En rust, los paquetes de código son llamados crates.
<br>


 
###### src/main.rs
Cargo ha creado un programa "¡"Hola, mundo!" como tal cual vimos en una explicación anterior.

Cargo espero que todo el codigo fuente viva dentro de la carpeta `src/`. la raiz del proyecto esta reservada para ficheros como README, licencias, ficheros de configuración y todo aquello no relacionado al código.

Si has empezado un proyecto rust que no usa Cargo, puedes convertirlo en uno que lo usa, simplemente tienes que mover el código fuente al directorio `src/` y crear un `Cargo.toml` apropiado a la configuración 
<br>

> contenido del fichero generado por el comando `cargo new hello_cargo`

```rust:
    fn main() {
        println!("Hello, World!")
    }
```
<br>

###### Building and Running de un proyecto Cargo

Vamos a explicar la diferencia entre `build` y `run`, para ello vamos a usar el proyecto hello_cargo que creamos antes, vamos a ejecutar el siguiente comando para construir el proyecto:
```cmd:
$ cargo build
   Compiling hello_cargo v0.1.0 (C:/projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 2.85 secs
```

Este comando crear un fichero ejecutable en la siguiente en la ruta `target/debug/hello_cargo` (en windows genera `target\debug\hello_cargo.exe`) donde hayas generado el proyecto. Por defecto cargo genera un `debug build`, puedes ejecutar el archivo compilado usando este comando:

```cmd:
$ ./target/debug/hello_cargo # or .\target\debug\hello_cargo.exe on Windows
Hello, world!
```
<br>

Si todo va bien, debería pintar por pantalla "Hello, world!", ejecutar `cargo build` por primera vez hace que `cargo` genere un fichero en la raíz llamado `Cargo.lock`. Este fichero sirve para llevar un seguimiento de las versiones de las dependencias que tenemos instaladas, este fichero se actualiza automáticamente cada vez que el proyecto es compilado y no es necesario su manipulación. 

Hay otra manera más rápida de conseguir el output del proyecto, usando el siguiente comando:

```cmd:
$ cargo run
   Compiling hello_cargo v0.1.0 (C:/projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.33 secs
     Running `target/debug/hello_cargo`
Hello, world!
```
<br>

Cargo tambien nos proporciona el comando `cargo check`. Este comando comprueba que se pueda compilar el código perfectamente y crear un ejecutable del mismo:

```cmd:
$ cargo check
   Checking hello_cargo v0.1.0 (file:///projects/hello_cargo)
    Finished dev [unoptimized + debuginfo] target(s) in 0.32 secs
```

`cargo check` aveces, este comando en mucho mas rápido que `cargo build` ya que nos saltamos el paso de crear el binario, y podemos comprobar que el estado del código es correcto. Usar `cargo check` a medida que vamos desarrollando nuestro código es una buena manera de saber si nuestro proyecto sigue compilando tras los cambios añadidos, muchos Rustaceans usan este comando como buena practica.

> Por añadir, los comandos de cargo son los mismos independientemente del SO en el que este desarrollando el código.
>
> Podemos acceder a documentación de las dependencias que hemos descargado mediante el comando `cargo doc --open`

<br>

###### Build para producción