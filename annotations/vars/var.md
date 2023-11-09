# Var
Vars são usados para usar a inferência de tipo do Java. 
Disponível a partir da versão 10.
Vars devem ser declaradas e atribuída valor para JVM conseguir inferir valor
Podem ser declaradas em blocos de métodos, construtores ou blocos de inicialização
Não podem ser declaradas em parâmetros de métodos, construtores e nem como fields de classes.


compila
```java
public class Teste{
    public static void main(String[] args) {
        var name = "Bob Dylan";
        var age = 55;
        var sexo = 'M';

        System.out.println(name);
        System.out.println(age);
        System.out.println(sexo);
    }
}
```

não compila
```java
public class Teste {
    private var name;
    
    public static void main(var[] args) {
        
    }
    
    public void method(var param) {
        // codeBlock
    }
}
```
