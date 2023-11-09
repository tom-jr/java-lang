# Why use

- Checking preciso em tempo de compilação
- Elimina uso de casting

Sem uso de generics

```java
public class Teste {
    public static void main(String[] args) {
        List list01 = new ArrayList();
        list01.add("Hello World!");

        /* É necessário fazer casting para o tipo String, e mesmo assim tem riscos de dar erro em 
                Com o generics podemos tirar a necessidade de casting e evitar erros de runtime
         * */
        String content001 = (String) list01.get(0);
        System.out.println(content001);

    }
}
```

Com uso de generics

```java
public class Teste {
    public static void main(String[] args) {
        // podemos remover o Type do Array list, o compilador vai inferir pelo List<String>
//        List<String> list01 = new ArrayList<String>(); 
        List<String> list01 = new ArrayList<>();

        list01.add("Hello World!");

        /* É necessário fazer casting para o tipo String, e mesmo assim tem riscos de dar erro em 
                Com o generics podemos tirar a necessidade de casting e evitar erros de runtime
         * */
        String content001 = list01.get(0);
        System.out.println(content001);

    }
}
```

## Tipo Simples de Generics

Usa uma única letra maiúscula para representar o Type
Podemos ter vários Types declarados

        class name<T1, T2, ..., Tn> { /* ... */ }

```java
public class Box<T> {
    private T t;

    public T getT() {
        return t;
    }

    public void setT(T t) {
        this.t = t;
    }
}
```

## Invocando a class Box

```java
public class Teste {
    public static void main(String[] args) {

        Box<Integer> box1 = new Box<Integer>(); // ou new Box<>();
        Box<String> box2 = new Box<Integer>(); // ou new Box<>();
        Box<Long> box3 = new Box<Integer>(); // ou new Box<>();
    }
}
```

## Multiple Type

```java
public interface Pair<K, V> {
    K getKey();

    V getValue();
}

public class OrderPair<K, V> implements Pair<K, V> {

    private K key;
    private V value;
    
    public OrderPair(K key, V value) {
        this.key = key;
        this.value = value;
    }
    
    @java.lang.Override
    public K getKey() {
        return this.key;
    }

    @java.lang.Override
    public V getValue() {
        return this.value;
    }
}

public class Teste {
    public static void main(String[] args) {
        OrderPair<Integer, String> pair = new OrderPair<Integer, String>(1, "Luffy"); // ou OrderPair<>();
        
//        Podemos passar como type um tipo que seja parametrizado com um tipo
        OrderPair<Integer,List<String>> pair2;
    }
}
```
## Raw type (Tipo Bruto)
Os Raw types não checam os tipos. Existe devido necessidade de compatibilidade com legacy codes
```java
public class Teste {
    public static void main(String[] args) {
        Box<Integer> box = new Box<>(); //Generic
        Box box = new Box(); //Row Type
    }
}
```

Recomendado que não se misture generic com row type.
```java
public class Teste {
    public static void main(String[] args) {
        Box<Integer> box = new Box<>(); //Generic
        Box boxR = box; //Row Type

        Box boxR2 = new Box(); //Row Type
        Box<String> box2 = boxR;
    }
}
```

## Métodos Genéricos

```java
public class Teste {
    public static<K> returnType typeMethod(Object<R> r, Object<X> x){
        //code block
    }
}
```

## Limitador de Type

Podemos limitar o type generic, para que o parameter type seja apenas aqueles que extends or implements
as classes ou interfaces declaradas

```java
public class Box<T extends A> {
    
    public static <R extends X> void method( R r) {
        
    }
}
```

múltiplos limitadores

    class Generic<X extends A & B & C> {}

pode ser misto com interface type, porem a class deve vim primeiro

```java
class A {}
interface B {}
interface C {}
class Generic<X extends A & B & C> {}
class Generic<X extends B & A & C> {} //throw error

```

## Métodos Genéricos e limitador de type

Um tipo não primitivo, não roda nesse método genérico devido ao operador '>' que se usa apenas com 
primitivo
```java
public class Teste {
    public static <T> int countGreaterThan(T[] anArray, T elem) {
        int count = 0;
        for (T e : anArray)
            if (e > elem)  // compiler error
                ++count;
        return count;
    }

}
```

Nesse foi usado a interface Comparable<T> para 'limitar' o Type. Assim não será uma primitiva.
```java
public class Test{
    public static <T extends Comparable<T>> int countGreaterThan(T[] anArray, T elem) {
        int count = 0;
        for (T e : anArray)
            if (e.compareTo(elem) > 0)  // compiler error
                ++count;
        return count;
    }
}

```


1 - Cite duas vantagens do uso de generics
2 - Como criar e invocar uma class genérica?
3 - Como criar e invocar uma class genérica com múltiplos types?
4 - É possível passar tipos parametrizados como Type?
5 - O que são os Raw types
6 - Demostre a estrutura de um método genérico
7 - Crie um generic delimitando o tipo par number
8 - Demonstre e descreva sobre múltiplos delimitadores

R01: 
- Dispensa do uso de Casting
```java
public class Teste {
    public static void main(String[] args) {
         //Sem o uso de genérico esse trecho de código precisará de casting, pois não sabemos que tipo
         //vamos receber em 'el'. Com o Type informado em List o compilador iria ter a certeza que se tra-
         //ta de uma string e tirar a necessidade de casting e remover o risco de um erro em runtime devido
        // a tipagem
        List arr1 = new ArrayList<>();
        arr1.add("Element");
        String el = arr1.get(0); // não compila sem a declaração de um cast para string.

    }
}
```
- Da uma forte checking de tipo em tempo de compilação evitando diversos erros em runtime que poderiam disparar
```java
// Como exemplo, esse código não tem erro em compilação, mas em runtime ele gera um erro de casting, pois BigDecimal não
//pode ser casting a String.
// Com o Type param em List em compilação já seria informado que os elementos de List podem ser add em um tipo Especifico
public class Test{
    public static void main(String[] args) {
        List arr1 = new ArrayList<>();
        arr1.add(new BigDecimal(1));
        String el = arr1.get(0);
        
    }
}
```
- Habilita o programa a usar algoritmos genéricos.

R02:
- Criar
```java
public class Box<T> {
    private T t;

    public T getT() {
        return t;
    }

    public void setT(T t) {
        this.t = t;
    }
}
```
- Invocar
```java

public class Main {

    public static void main(String[] args) {
        Box<String> strBox = new Box<>();

        strBox.setT("Hello World!");

        System.out.println(strBox.getT());
    }
}

```

R03:
podendo add mais

        class Box<K,V,Z,Y ... N> {}
```java
class Box<K, V> {
    private K k;
    private V v;

    public K getK() {
        return k;
    }

    public V getV() {
        return v;
    }

    public void setK(K k) {
        this.k = k;
    }

    public void setV(V v) {
        this.v = v;
    }
}
```
R04:
 - Sim:
```java
public class Teste {
    public static void main(String[] args) {
        Box<List<String>> box = new Box<>();
    }
}
```

R05:
- Raw Types é quando instanciamos uma class genérica como um class genérica sem passar any param Type:

Essa instanciação bruta é possível devido compatibilidade com legacy code
```java
public class Box<T> {
    private T t;

    public Box() {
    }

    public Box(T t) {
        this.t = t;
    }

    public void setT(T t) {
        this.t = t;
    }

    public T getT() {
        return t;
    }
}

public class Teste {
    public static void main(String[] args) {
        Box box =  new Box(); // Aqui esta um raw type
    }
}
```
R06:
```java
public class Box<A> {
    public <B> void method(B b) {
        System.out.println(b.getClass().getName);
    }
}

public class Teste {
    public static void main(String[] args) {
        Box<Object> box = new Box<>();
        box.<BigDecimal>method(BigDecimal.TEN); // Podendo neste caso omitir o Type pois há inferência de tipo
    }
}
```

R07:

```java
public class BoxNumber<N extends Number> {
    private N n;

    public BoxNumber() {
        
    }
    public BoxNumber(N n) {
        this.n = n;
    }

    public N getN() {
        return n;
    }

    public void setN(N n) {
        this.n = n;
    }
}

public class Teste {
    public static void main(String[] args) {
        BoxNumber<Long> boxNumber =  new BoxNumber<Long>(1L); //se colocar qualquer type que não extends de Number não compilará
    }
}
```

R08:
uma type pode ser delimitado por mais de uma class ou interface

```java
// Onde o primeiro deve ser a class e os demais interfaces
public class Box<T extends U & V & X> {
    
}
```
