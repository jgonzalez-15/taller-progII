# Conceptos útiles para el Obligatorio
## Índice
- [Git y Github](#git-y-github)
- [Enums](#enums)
- [Comparable](#comparable)
- [Logs](#logs)
- [UML](#uml)
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

Al intentar hacer merge Git no sabrá con qué versión quedarse, lo que genera problemas.

### Origin y Local
Como GitHub almacena código en la nube, existe una diferencia entre lo que hay online (origin) y lo que tenemos en nuestra computadora (local).

Por esto, cuando hacemos un commit en nuestra computadora (local), debemos hacer **push** para que el cambio se reflejé online (origin). De la misma manera, si tenemos cambios de alguien más en origin, debemos utilizar **pull** para traerlos a local.

## Organización en Git
Cuando se hacen proyectos de a varias personas, existen varias formas de organizarse, algunas más "formales" que otras
- Ramas por persona (cada uno crea su rama y trabaja en ella)
- Ramas por sección de código (backend/frontend)
- Ramas por feature (login / página principal / carrito / ...)

Lo fundamental en todas estas es que nadie trabaja sobre la rama principal (**main**), esta rama se deja sólo para  


## Enums

## Comparable

## Logs

## UML

## Manejo de archivos en Java
