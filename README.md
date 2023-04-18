# Rust

É uma linguagem de programação para sistemas feita pela mozilla marcada por defender três coisas:
    - Segurança garantida em tempo de compilação
    - Concorrência
    - Velocidade
Fizeram isso porque estavam cansados do C++, que é uma linguagem pouco segura, fácil de cometer erros. Com isso, o firefox conseguiu ficar duas vezes mais rápido e com menos bugs.

 ## Cargo

Cargo é o gerenciador de pacotes para a linguagem Rust. Além disso, é onde o build é feito, onde rodam os testes e onde a documentação é gerada.

 - Para criar um projeto
~~~~rust

    cargo new NOME DO PROJETO

~~~~

 - Para rodar compilar e executar o projeto

~~~rust
    cargo run
~~~

 ## Variáveis

A linguagem é fortemente tipada, mas, apesar disso ela consegue descobrir o tipo caso você não declare ele. Além disso, podemos declarar mais de uma variável por vez com a sintaxe de desestruturação:

~~~rust

    fn main() {
        let (bunnies, carrots) = (1,56);
    }
~~~

Algo diferente do Rust das demais linguagens é o fato de que NÃO É POSSÍVEL ALTERAR VALOR DE UMA VARIÁVEL, o que permite mais segurança, concorrência e velocidade.

~~~rust

    fn main() {
        let bunnies = 16;
        bunnies = 2; //ERRO!!
    }
~~~

Para isso funcionar devemos declarar ela mutável

~~~rust

    fn main() {
        let mut bunnies = 16;
        bunnies = 2; //OK
    }
~~~

Para usar uma variável global, devemos declará-la constante explicitamente, obrigatoriamente falar seu tipo e usar um valor que pode ser descoberto em tempo de compilação como um valor fixo, além de, por convenção, usar o nome da variável em upper case. Isso permite grande velocidade.

~~~rust

    fn main() {
        const BUNNIES: f64 = 16.6;
    }
~~~

## Escopo

No exemplo a seguir, a variável *x* pode ser usada tanto no main, quanto entre as chaves dentro da main, que representa uma função, enquanto o y, só pode ser usado dentro das chaves, depois dela, graças ao garbage collector da linguagem, não pode ser usada mais, caso contrário, ocorrerá um erro em tempo de compilação, portanto, nós saberemos resolver.

~~~rust
    fn main(){
        let x = 5;
        {
            let y  = 99;
            println!("{}, {}", x, y);
        }
        println!("{},{}", x, y);
    }
~~~

## Segurança de memória (memory safety)

Variáveis precisam ser INICIALIZADAS antes de serem usadas

~~~rust

fn main(){
    let engima: i32;
    if true{
        enigma = 42;
    }
    println!("enigma is {}", enigma);
}

~~~

O código acima não funciona, porque o compilador não sabe dizer se a variável *enigma* vai ser inicializada ou não.

~~~rust

fn main(){
    let engima: i32;
    if true{
        enigma = 42;
    } else{
        enigma = 7;
    }
    println!("enigma is {}", enigma);
}


~~~

Por outro lado, o código acima funciona, já que, em tempo de compilação, sabemos que a variável enigma vai assumir algum valor.

## Funções

Definidas com *fn* seguida do nome da função definida em snake-case separada por underscore do tipo

~~~rust

    fn do_stuff(){

    }

~~~

Em rust não precisamos escrever o corpo da função antes da chamada dela, o que permite que o main fique no topo do código. Os parâmetros da função são passados como *nome: tipo* separados por vírgula e o retorno é passado depois dos parenteses como *-> tipo*. O retorno é usado como * return algo * ou basta deixarmos a última linha sem ponto e vírgula (tail expression).

~~~rust

    fn do_stuff(qty: f64, oz: f64) -> f64{
        return qty*oz;
    }

~~~

ou

~~~rust

    fn do_stuff(qty: f64, oz: f64) -> f64{
        qty*oz
    }

~~~

Uma função em Rust não suporta número variável de argumentos ou diferentes tipos pra um mesmo argumento. Para isso, preciramos de macros, como o println!. Todo macro termina em exclamação.

## Sistema de módulos

Em rust, você pode criar uma biblioteca .rs e importar em determinado arquivo .rs com 

~~~rust

use NOME_PROJETO::FUNCAO_CRIADA_QUE_QUERO_USAR;
use std; //biblioteca padrão

~~~

Podemos procurar o que há na biblioteca padrão em https://doc.rust-lang.org/std/index.html#primitives. Fora da bibliteca padrão, temos o *crates.io*, onde acharemos o resto (pacotes em geral). Para adicionar um pacotes do crates.io devemos em no arquivo Cargo.toml e adicionar o nome do pacote seguido de igual e da versão, como o exemplo a seguir para números randômicos.

~~~rust

[dependencies]
rand = "0.6.5" 

~~~
