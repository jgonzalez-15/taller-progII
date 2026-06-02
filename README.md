# Conceptos útiles para el Obligatorio
## Índice
- [Git y Github](#git-y-github)
- [Enums](#enums)
- [Comparable](#comparable)
- [Logs](#logs)
- [Manejo de archivos en Java](#manejo-de-archivos-en-java)

## Git y Github
### Git vs Github
Git es el sistema de control de versiones, Github es una plataforma en la nube de almacenamiento de código.

### Concepto de versiones
Git trabaja con versiones del código, es decir, almacena qué cambios se hicieron en cada actualización del código, con lo que podemos navegar fácilmente entre distintas versiones.
Por ejemplo supongamos que tengo mi código:
```java
//Versión 1
int a = 10;
System.out.print(a);
```
Esta sería la primera versión

Luego si agrego más código y genero una segunda versión:
```java
//Versión 2
int a = 10;
int b = 1;
int c = a + b;
System.out.print(c);
```
Git sabrá cual era el código en cada momento y puedo volver a la primera versión fácilmente.

### Commits
La forma de crear una nueva versión en git es mediante un commit, esto es en definitiva una forma de confirmar los cambios hechos en el código. Si no hacemos commit git no guardará los cambios como una versión nueva, por lo que podemos perderlos.

En el ejemplo anterior, cuando agregamos las líneas nuevas, debimos haber hecho un commit para que git genere la segunda versión.

### Branches
Para organizar el trabajo y no editar el mismo código, git permite el uso de branches (ramas). Estas son "versiones paralelas" del mismo código, por ejemplo, supongamos que partimos del código anterior:

```java
//Rama 1
int a = 10;
System.out.print(a);
```

Podríamos crear una nueva rama a partir de esta (digámosle Rama 2). Como la creamos a partir de la Rama 1, tendrá el mismo código:
```java
//Rama 1
int a = 10;
System.out.print(a);

//Rama 2
int a = 10;
System.out.print(a);
```

Luego alguien podría hacer el cambio de antes en la Rama 2 y hacer commit, esto genera un cambio sólo sobre la Rama 2, generando el siguiente resultado:

```java
//Rama 1
int a = 10;
System.out.print(a);

//Rama 2
int a = 10;
int b = 1;
int c = a + b;
System.out.print(c);
```

### Merge
Para unificar el trabajo de distintas ramas existe el merge, esta acción junta los cambios de ambas ramas.

Supongamos que estamos en la Rama 1 de nuestro ejemplo, si hacemos un merge de la Rama 2 traeremos los cambios de la misma, dando el siguiente resultado:
```java
//Rama 1
int a = 10;
int b = 1;
int c = a + b;
System.out.print(c);

//Rama 2
int a = 10;
int b = 1;
int c = a + b;
System.out.print(c);
```
Si estuvieramos en la Rama 2 e hicieramos merge de la Rama 1 no haría cambios, pues la Rama 1 no tuvo cambios desde que se creó la Rama 2.

### Merge conficts
Debemos tener cuidado al trabajar en distintas ramas ya que, si ambias hacen un cambio sobre la misma línea, no sabrá cual utilizar.
Por ejemplo en las ramas de antes:

```java
//Rama 1
int a = 10;
System.out.print(a);

//Rama 2
int a = 10;
System.out.print(a);
```
Si en la Rama 1 se cambia el nombre de *a* por *b*, mientras que en la Rama 2 se cambia *a* por *c*
```java
//Rama 1
int b = 10;
System.out.print(b);

//Rama 2
int c = 10;
System.out.print(c);
```

Al intentar hacer merge Git no sabrá con qué versión quedarse, lo que genera problemas. En estos casos Git te obligará a elegir una de las dos versiones, o cancelar el merge y editar el código antes de reintentar.

### Origin y Local
Como GitHub almacena código en la nube, existe una diferencia entre lo que hay online (origin) y lo que tenemos en nuestra computadora (local).

Por esto, cuando hacemos un commit en nuestra computadora (local), debemos hacer **push** para que el cambio se reflejé online (origin). De la misma manera, si tenemos cambios de alguien más en origin, debemos utilizar **pull** para traerlos a local.

### Organización en Git
Cuando se hacen proyectos de a varias personas, existen varias formas de organizarse, algunas más "formales" que otras
- Ramas por persona (cada uno crea su rama y trabaja en ella)
- Ramas por sección de código (backend/frontend)
- Ramas por feature (login / página principal / carrito / ...)

Lo fundamental en todas estas es que nadie trabaja sobre la rama principal (**main**), esta rama se deja sólo para cambios testeados y funcionales, así nadie que ejecute o cree una rama desde main encontrará errores.

## Enums
Los enums son una entidad de Java que sirve para "definir variables personalizadas". 

Por ejemplo, supongamos que queremos una variable color que pueda ser azul, rojo o amarillo; normalmente podríamos definir un *int color* que tome valores 0, 1 y 2 y recordar "0 es azul", "1 es rojo" y "2 es amarillo".

En lugar de esto podemos crear un Enum, en este podemos definir las variables (azul, rojo, amarrilo) y dejar que java se encarga de guardarlo e interpretarlo como quiera (en general es similar al ejemplo anterior). Este ejemplo se vería de la siguiente manera:
```java
public enum Color {
  ROJO,
  AZUL,
  AMARILLO
}
```
Luego podemos acceder a él mediante Color.*color* o incluso agregarlo a una clase:
```java
public class Auto {
  String marca;
  Sting modelo;
  Color color;

  public Auto(String marca, Srting modelo, Color color){
    this.marca = marca;
    this.modelo = modelo;
    this.color = color;
  }
}

Auto auto1 = new Auto("Renault", "Swift", Color.ROJO);
```

## Comparable
Existen algoritmos y TADs que necesitan comparar objetos, por ejemplo un heap.
Sin embargo, cuando tenemos un objeto complejo java no sabe cuál es mayor y cuál menor, por ejemplo supongamos una persona:
```java
public class Persona {
  String nombre;
  int edad;
  int altura;

  //SUpongamos que tiene constructor
}

Persona ana = new Persona("Ana", 20, 172);
Persona beto = new Persona("Beto", 18, 172);
```
¿En este caso se cumple *Ana > Beto* o *Beto < Ana*? Tal vez incluso sea *Ana = Beto*.

Para esto existe Comparable, una interfaz de java que indica que una clase se puede comparar utilizando la función *compareTo()*.

En el caso de Ana y Beto, podemos compararlos por edad, por altura, o por cualquier otra cosa que queramos. Lo que sea que elijamos como forma de comparación, debe calcularse en *compareTo()*

*Ana.compareTo(Beto)* devolverá: 1 si Ana > Beto, 0 si Ana = Beto, -1 si Ana < Beto.
```java
public class Persona implements Comparable<Persona> {
  String nombre;
  int edad;
  int altura;

  //Supongamos que tiene constructor

  //Si comparamos por edad sería
``@Override
``public int compareTo(Product other) {
    if (this.edad > other.edad){
      return 1;
    }
    else if (this.edad == other.edad){
      return 0;
    } else {
      return -1;
    }

    //También podemos aprovechar que java ya sabe comparar ints y usar directamente
    return this.edad.compareTo(other.edad);
}

Persona ana = new Persona("Ana", 20, 172);
Persona beto = new Persona("Beto", 18, 172);
ana.compareTo(beto); //Devuelve 1 pues Ana es mayor a Beto en edad.
```

## Logs
Supongamos que trabajamos para una empresa y tenemos un programa de análisis de datos que dejamos ejecutando todas las noches mientras dormimos.

Puede suceder que un día el programa falle y se cierre a media noche, en este caso al levantarnos no tendríamos forma de saber qué pasó, ni que datos procesamos y cuales quedaron sin procesar.

Para esto se usa un log, es decir, un archivo de texto plano donde el programa anota las cosas que hace a medida que ejecuta, así podemos saber todo lo que hizo después.

Un ejemplo básico podría verse así:
```txt
[23:59] Se cargó el dato con Id 1
[00:04] Se terminó de procesar el dato con Id 1
[00:05] Se cargó el dato con Id 2
```

Si el log terminara ahí y el programa falló, podemos suponer que hubo un error al procesar el dato con Id 2 pues no se terminó de procesar nunca.  

En resumen, los logs son una herramienta para que un desarrollador pueda saber qué sucedió con el código a través de un archivo que se guarda incluso cuando el programa cierra. No tienen un formato específico, sino que se elige qué escribir según qué información consideramos útil.

Para el programa es simplemente una escritura, no necesita leer el log nunca.

## Manejo de archivos en Java

Java cuenta con librerías propias para trabajar con archivos de texto.

### Escribir (y crear) un archivo
Para escribir texto, usamos *FileWriter* envuelto en un *BufferedWriter* (que lo hace más eficiente). Si el archivo no existe, Java lo crea automáticamente.
```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class EscritorDeArchivos {
    public static void main(String[] args) {
        String nombreArchivo = "ejemplo.txt";
        try (BufferedWriter escritor = new BufferedWriter(new FileWriter(nombreArchivo))) {
            escritor.write("Linea de texto 1");
            escritor.newLine(); // Pasamos de línea
            escritor.write("Segunda línea");
        } catch (IOException e) {}
    }
}
```

El archivo resultante *ejemplo.txt* sería:
```txt
Linea de texto 1
Segunda línea
```

### Leer un archivo
Para leer, usamos *FileReader* envuelto en un *BufferedReader*, parecido al caso anterior.
```java
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class MLectorDeArchivos {
    public static void main(String[] args) {
        String nombreArchivo = "ejemplo.txt";
        try (BufferedReader lector = new BufferedReader(new FileReader(nombreArchivo))) {
            String linea;
            // Leemos línea por línea hasta que el resultado sea null (fin del archivo)
            while ((linea = lector.readLine()) != null) {
                System.out.println(linea); //línea será un String con un renglón del archivo en cada iteración, por lo que lo podemos modificar como queramos
            }
        } catch (IOException e) {}
    }
}
```

### Cierre automático
Siempre hay que cerrar los archivos al terminar. Usando *try (...)*, Java cierra el archivo automáticamente, incluso si lanza algún error.
