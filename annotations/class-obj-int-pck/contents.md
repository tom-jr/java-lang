# Objects, Classes, Interfaces, Packages, and Inheritance
## O que é objeto?

É o empacotamento de estados e comportamentos relacionados.

Estados são as características possíveis de um objeto.
Exemplo:
Um Objeto Bicycle tem estados:
Garupa, marcha, banco, etc.

Comportamentos são os comportamentos característicos do objeto em questão.
Exemplo:
Uma Bicycle pode (ação):
trocar macha, acelerar/reduzir velocidade, etc.

Alguns objetos são mais complexos do que outros, podendo ter mais estados e comportamentos e até conter
outros objetos dentro de si.

Objetos armazenam seus estados dentro de variáveis e os expõe por meio de métodos.

Métodos operam internamente sobre seus estados. São mecanismos primários na comunicação entre objetos.

Esconder os estados de um objeto e o expor a alterações apenas por meio de seus métodos é um conceito 
pilar da programação orientada a objeto, chamada **Encapsulamento**.

Encapsular estados permite um melhor monitoramento e regência dos estados de um objeto.
Exemplo:
Objeto Mp4 que tem o estado volume com range de amplitude entre 0 e 10.

**Vantagens do uso de Objetos**
- Modularidade: O código-fonte de um objeto fica independente de outros objetos.
- Ocultação de informações: limita ou restringe acesso a estados e comportamentos de um Objeto permitindo
acesso apenas por meio de métodos públicos.
- Reuso de código: Caso exista outro trecho do sistema que necessita de um agrupamento de estado e 
comportamento que ja exista como objeto, podemos o reutilizá-lo.
- Plugabilidade: Se um objeto não atende bem a necessidade. podemos removê-lo e plugar outro.

## O que é uma class?

São as pantas(moldes) no qual, a partir delas os Objetos são criados.
A instância de um classe gera um objeto.
Ex de uma classe em java:

```java
public class Bicycle {
    String name;
    String model;
    Ing gear;

    public changeGear(Int newValue) {
        this.gear = newValue;
    }
}
```
Geralmente a class não terá um método main.

Exemplo da instanciação da class para se obter um objeto:

```java
public class Main {
    public static void main(String[] args) {
        Bicycle b1 = new Bicycle();
        b1.name = "bike_name";
        b1.model = "Model_01";
        b1.gear = 1;

        b1.changeGear(2);
    }
}
```

## O que é uma interface
Em sua forma mais comum, **interface** é um ou um conjunto de métodos vazios.

```java
public interface Bicycle {
    void changeGear();
    void slowDown();
}
```
Quando uma class implementa essa interface ela pode ter um corpo único para os métodos que 
obrigatoriamente irá implementar. Exemplo:

```java
public class BicycleClass implements Bicycle {
    private Integer gear;
    private Integer speed;

    @Override
    public void getGear() {
        return gear++;
    }
    @Override
    public void slowDown() {
        return speed--;
    }
}
```
