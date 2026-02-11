# Java-Functional-Interfaces
A way to study functional paradigm because I get no chill in all Java interviews when I get asked about this @"#$"#$"# topic, gosh...

En al menos 4 entrevistas que he tenido de Java, últimamente tienden a preguntar mucho sobre las functional interfaces. Y si he de
ser sincero, no he querido profundizarlas por pereza, porque no es común encontrarte ese paradigma... pero veo que en versiones
de java si se tiende a aplicar mucho!.

Así que para no quedarnos tan deprecados tendremos así como con el tópico de los hilos, checar este tema
y estudiarlo. Y para el repo del día de hoy haremos eso:

Los lambdas son una forma de reducir tus expresiones, en ciertas funciones. El antepasado de los lambdas
eran las clases anónimas, que eran clases que declarabas dentro de x método instanciado. Ahora
es solamente seguir el patrón {(param)->param transformed and returnes}, si te das cuenta es parecido a un callback
en javascript.

Si investigas algunos ejemplos, te podrás dar cuenta que hay ciertas clases como los Comparator<?> que puedes
implementar en clases, un comparator te ayuda a no crear muchas entidades para temas así.

El lambda viene implicito con los streams. También está el concepto de los reduce, que en resumidas
es la manera de invocar clases como System.out::println de una manera static. 

Si quieres hacer un reduce, en un stream, crear una clase:

````main.java
class Example{
  public static getRetirementPercentagePayment(float salary){
      return salary*0.45;
  }
}

/*... y en tu lambda lo invocas asi...*/

salarys.stream().map(Example::getRetirementPercentagePayment); /*Y asaí continuas haciendo tu stream pipe*/
````

Esto, el estático con :: es un reduce, al ser método se categoriza como una lambda implicita.

Las functional interfaces son métodos que no tienen nombre definido, son anónimos. 

````main.java
ArrayList < String> milista = new ArrayList < String > ();
milista.add("Miguel");
milista.add("Alicia");

/**Aqui usamos reducers, el método estático se vuelve un lambda implicito, ya que los consumers
no devuelven nada, y el print es un método void totalmente compatible**/
milista.forEach(System.out::println);

milista.forEach((e)->{System.out.println(e)}); // la manera anónima pero declarativa dentro de otro método.

/**Forma desglosada: hay lambdas implicitos por defecto en java, tienen sus tipos, esta
es la forma declarativa, forEach usa lambdas de tipo consumer, solo declaras el tipo de valor
del input pero no declaras el output*/

 Consumer<String> opt = (e)->System.out.println(e);
milista.forEach(System.out::println);
````

Tipos de functional interfaces:

Los lambdas por defecto en java están categorizados, los exploraremos:

*Function*
Defines tipo de datos en input y output
````main.java
/*Devuelve string a mayusculas*/
Function<String,String> optFunc = (s1)-> s1.toUpperCase();
System.out.println(optFunc.apply("pruebamin"));

/*Los functional también te permiten hacer chaining de métodos, es como patrón de diseño*/
Function<String,String> optFunc = (s1)-> s1.toUpperCase();
optFunc = optFunc.andThen((e)->e.repeat(5));
````

*Functional interfaces by @FunctionalInterface*
Una manera de declarar @FunctionalInterfaces es por medio de una interfaz

````main.java
@FunctionalInterface
  interface clasBy{
      int appP(int a);
      int appB(int c);
  }

/*Si añades dos elementos el ide te marcara error, los functional interfaces solo pueden tener un método.*/



interface clasBy{
    int appP(int a);
    int appB(int c);
}
````

*Tipos de functional interfaces*

*Function* => Ya explicado arriba

*Consumer*=> También explicado arriba

*Predicate*=> Functional interface que solo acepta su parametro de entrada, crea un booleano de acuerdo a lo que evalua

````main.java
Predicate<Integer> numberHigher = (number)-> number>100;

/*También existen predicados por función*/
for (int i = 0; i < 100; i++) {
    System.out.println(prueba(i, (c)->c % 2 !=0 ));
}

public static boolean prueba(int number,Predicate<Integer> evaluatorHigherThan){
    return evaluatorHigherThan.test(number) ? true : false;
}

/*Puedes aplicar and o or, como compuertas*/
public static boolean prueba(int number,Predicate<Integer> evaluatorHigherThan){
    return evaluatorHigherThan.and((Integer numberRange)->numberRange >10).test(number) ? true : false;
}
````

*Supplier*
Los suppliers son funciones que no toman inputs y devuelven outputs... no muy necesarios...

Y eso es todo, los functional interfaces básicos, también los Comparator y comparable son functional interfaces.

La diferencia radica en que comparator se aplica en cualquier lista, tiene los métodos reverseOrder() & naturalOrder(), y
para lógicas más customizadas usas un lambda, En Comparable, tienes que implementarlo en una clase. ADEMÁS, comparator te permite
también hacer  lo mismo que comparable pero con más campos.


Y eso es todo, es Supplier, Consumer, Predicate y Function, y @FunctionalInterface.
Existen otros más pero no es muy frecuente usarlos.

https://www.geeksforgeeks.org/java/java-functional-interfaces/

Ahora a estudiar cosas más importantes.

