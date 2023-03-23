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

- La función `main` es especial, es lo primero que se ejecuta en cualquier programa de Rust, puedes añadir parametros insertandolos en los `()`.
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