#  **♨️ Exercício de introdução a Orientação a Objetos com Java**

Esse é um exercício em Java para treinar alguns dos conceitos basicos de *Orientação a Objetos*.

Com esse Exercício abordei os pontos Construtores, `Sobrecarga`, `Encapsulamento` e também um pouco de `Modificadores de Acesso`.

### 🔠  Enunciando e contexto do Exercício

>Em um banco, para se cadatrar uma conta bancária é necessário informar o núemro da conta e o nome do titular da conta, e o valor do depósito inicial que o titular depositou na conta. Este valor de depósito inicial, entretando, é opicional, ou seja: se o titular não tiver dinheiro a depositar no momento de abrir sua conta, o depósito inicial não será feito e o saldo inicial da conta será, naturalmente, zero.
>
>Importante: Uma vez que uma conta bacária foi aberta, o núemro da conta nunca poderá ser alterado. Já o nome do titular pode ser alterado.
>
>Por fim, o saldo da conta não pode ser alterado livremente. É preciso haver um mecanismo para proteger isso. O saldo só aumenta mediante a depósitos, e só diminui por meio de saques. Para cada saque realizado, o banco cobra uma taxa de $5,00. Nota: a conta pode ficar com saldo negativo se o saldo não for suficiente para realizar o saque e/ou pagar a taxa.

## __📑 Arquivo Class.java__

### __1️⃣ Definindo variáveis__


  Primeiramente vamos definir as variáveis que iremos utilizar. Vamos definir essa variáveis como privadas, para que só possam ser acessadas dentro da classe em que foram definidas, impedindo assim que elas seja definidas ou alteradas diretamente.

~~~java

private String name;
private int accountNumber;
private double balance;

~~~~

Essas serão as variáveis principais, durante o desenvolvimento usaremos outras variáveis mas não terão a mesma importância.

Agora com as variáveis definidas, podemos continuar nosso desenvovimento. Agora criaremos o contrutor para receber e instanciar as variáveis que criamos. Como as variáveis que criamos foram do tipo **private**  precisaremos definir um método (Construtor) para as variáveis.

###  __2️⃣ Definindo o Contrutor__

~~~Java
public Class(Sring name, int accountNumber, double balance){
  this.name = name;
  this.accountNumber = accountNumber;
  this.balance = balance;
}
~~~

Nosso contrutor recebeu o nome genérico de Class, nele vamos passar os seguintes parametros: ```name```, ```accountNumber``` e ```balance```. Esse construtor diferente das variáveis que criamos anteriormente, recebe `public` como modificador de acesso, então nesse caso vamos conseguir acessa-lo em outras classes e outros arquivos.
Note que usamos `this` no construtor, esse *this* faz referência ao objeto, então `this.name` faz referência a variavel criada anteriormente, e o `name` é o parametro do contrutor. Então de umas forma simples a *variavel name* está recebendo o *parametro name*.

Com o construtor definido vamos agora criar os getters e setter do nosso app, pois como descrito no enunciado algumas informações podem ser alteradas(setters) e também vamos precisar acessar as variáveis privadas então vamos usar o método get para retornar o resultado.


### __3️⃣ Criando Getters e Setters__

~~~java

// Alterando o nome
public void setName(newName){
  this.name = newName;
}
//Retornado o nome
public String getName(){
  return name;
}

// retornado o número da conta
public int getAccountNumber(){
  return accountNumber;
}

// retornando o Saldo da conta
public double getBalance{
  return balance;
}
~~~

Repare que apenas o nome tem um Setter, isso porque no enunciado diz que apenas o nome pode ser alterado, já o número da conta nunca pode ser alterado e o saldo só pode ser alterado mediante saque ou depósito.

### __4️⃣ Criando métodos de depósito e de saque__

Já que o saldo só pode ser alterado mediante a saque ou depósito vamos criar os metodos propostos, lembrando que existe uma taxa de saque de $5,00 para cada operação.

~~~java

//MÉTODO DE DEPÓSITO
public void deposit(deposit){
  balance += deposit;
}

// MÉTODO DE SAQUE
public void withdraw(withdraw){
  balance -= (withdraw + 5);
}
~~~

Agora que já temos nosso médoto de depósito, podemos alterar nosso construtor, pois lá o saldo inicial está sendo definido diretamente e é uma boa prática usar o método que foi criado para essa função e também poque se houver alguma alteração na política de depositos da empresa será necessário alterar em apenas um lugar.

Vamos substituir o ```this.balance = balance``` por ```deposit(initialDeposit)``` fazendo o construtor ficar assim:
~~~java
public Class(String name, int accountNumber, double initialDeposit){
  this.name = name;
  this.accountNumber = accountNumber;
  deposit(initialDeposit);
}
~~~

## __📑 Arquivo App.java__

Aqui no App vamos apenas instanciar as variáveis e imprimir na tela o que fizemos no outro arquivo, note que todas os métodos estão no arquivo `Class.java`, isso acontece porque estamos usando o conceito de responsabilidade.

~~~java
import java.util.Scanner;

public class App {
    public static void main(String[] args) throws Exception {

        Scanner scan = new Scanner(System.in);

        //RECEBENDO O NOME DO TITULAR
        System.out.print("Nome: ");
        String name = scan.nextLine();
        //RECEBENDO O NÚMERO DA CONTA
        System.out.print("Conta: ");
        int conta = scan.nextInt();
        // CONDICIONAL DO DEPOSITO INICIAL
        System.out.print("Deseja fazer um depósito inicial (Y/N) ? ");
        scan.nextLine();
        char answer = scan.next().charAt(0);
        double deposit = 0;


        if(answer == 'y'){
            System.out.print("Qual o valor do dopósito? ");
            deposit = scan.nextDouble();

        }
        System.out.println();
        
        Class data = new Class(name, conta, deposit);
        
        System.out.printf("Olá %s, sua conta é a %d, e seu saldo é %.2f%n",data.getName(),data.getAccountNumber(),data.getBalance());
        System.out.println();   

        System.out.print("Qual o valor do seu saque? ");
        double withdraw = scan.nextDouble();
        data.withdraw(withdraw);
        System.out.println(); 

        System.out.printf("Seu saldo atualizado é: %.2f%n",data.getBalance());
        System.out.println();        
        
        System.out.print("Qual o valor do seu Depósito? ");
        double add = scan.nextDouble();
        data.deposit(add);
        System.out.println(); 
        System.out.printf("Seu saldo atualizado é: %.2f%n",data.getBalance());
        
        scan.close();
    }
}
~~~
