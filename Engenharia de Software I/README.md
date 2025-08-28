# bertoti

1. Engenharia de software implica mais na aplicação de conhecimentos teóricos de construçaõ de software do que a programação em si. Conforme o desenvolvimento de softwares evolui, devemos criar métodos e padrões de engenharia mais rigorosos para garantir a segurança e confiabilidade.

2. O parágrafo reflete sobre a engenharia de software, e apresennta princípios para garantir a organização dos códigos, sendo: <b>Tempo e Mudança:</b> Como o código precisará se adaptar ao longo de sua vida, <b>Escala e Crescimento:</b> Como a organização precisará se adaptar à medida que evolui, <b>Compensações e Custos:</b> Como a organização toma decisões, com base nas lições de Tempo e Mudança, e Escala e Crescimento.

3. a) Desempenho vs. Legibilidade do Código

Explicação: Melhorar o desempenho pode resultar em código mais difícil de entender, o que torna a manutenção mais difícil.

b) 2. Velocidade de Desenvolvimento vs. Qualidade do Código

Explicação: Entregar rapidamente pode sacrificar a qualidade do código, como testes e boas práticas, o que aumenta o risco de erros.

c) 3. Escalabilidade vs. Simplicidade

Explicação: Soluções escaláveis exigem mais complexidade, mas tornam o sistema mais preparado para crescer. Soluções simples podem não suportar o aumento de usuários ou dados.

4. Diagrama de Classes UML
<img src="https://github.com/DanielDPereira/bertoti/blob/main/Engenharia%20de%20Software%20I/diagramaClassesUML2808.png?raw=true"/>

6. Java:
```java
import java.util.ArrayList;
import java.util.List;
import java.text.SimpleDateFormat;
import java.util.Date;

public class SistemaBancario {

    // Classe Cliente
    static class Cliente {
        private String nome;
        private String cpf;
        private List<ContaBancaria> contas;

        public Cliente(String nome, String cpf) {
            this.nome = nome;
            this.cpf = cpf;
            this.contas = new ArrayList<>();
        }

        public void abrirConta(ContaBancaria conta) {
            contas.add(conta);
            System.out.println("Conta aberta para " + nome + " com sucesso.");
        }

        public void fecharConta(ContaBancaria conta) {
            if (contas.contains(conta)) {
                contas.remove(conta);
                System.out.println("Conta fechada com sucesso.");
            } else {
                System.out.println("Conta não encontrada.");
            }
        }

        public List<ContaBancaria> getContas() {
            return contas;
        }
    }

    // Classe ContaBancaria
    static class ContaBancaria {
        private String numeroConta;
        private double saldo;
        private String tipo;

        public ContaBancaria(String numeroConta, String tipo) {
            this.numeroConta = numeroConta;
            this.saldo = 0.0;
            this.tipo = tipo;
        }

        public void depositar(double valor) {
            if (valor > 0) {
                saldo += valor;
                System.out.println("Depósito de " + valor + " realizado com sucesso.");
            } else {
                System.out.println("Valor inválido para depósito.");
            }
        }

        public void sacar(double valor) {
            if (valor <= saldo && valor > 0) {
                saldo -= valor;
                System.out.println("Saque de " + valor + " realizado com sucesso.");
            } else {
                System.out.println("Saldo insuficiente ou valor inválido.");
            }
        }

        public void transferir(ContaBancaria contaDestino, double valor) {
            if (valor <= saldo && valor > 0) {
                this.saldo -= valor;
                contaDestino.depositar(valor);
                System.out.println("Transferência de " + valor + " realizada com sucesso.");
            } else {
                System.out.println("Saldo insuficiente ou valor inválido.");
            }
        }

        public double getSaldo() {
            return saldo;
        }

        public String getNumeroConta() {
            return numeroConta;
        }

        public String getTipo() {
            return tipo;
        }
    }

    // Classe Transacao
    static class Transacao {
        private String tipo;
        private double valor;
        private String data;
        private ContaBancaria contaOrigem;
        private ContaBancaria contaDestino;

        public Transacao(String tipo, double valor, ContaBancaria contaOrigem, ContaBancaria contaDestino) {
            this.tipo = tipo;
            this.valor = valor;
            this.contaOrigem = contaOrigem;
            this.contaDestino = contaDestino;
            this.data = new SimpleDateFormat("dd/MM/yyyy HH:mm:ss").format(new Date());
        }

        public void registrar() {
            System.out.println("Transação registrada: ");
            System.out.println("Tipo: " + tipo);
            System.out.println("Valor: " + valor);
            System.out.println("Data: " + data);
            if (contaOrigem != null) {
                System.out.println("Conta Origem: " + contaOrigem.getNumeroConta());
            }
            if (contaDestino != null) {
                System.out.println("Conta Destino: " + contaDestino.getNumeroConta());
            }
        }
    }

    // Método main para rodar o sistema
    public static void main(String[] args) {
        // Criando clientes
        Cliente cliente1 = new Cliente("João Silva", "123.456.789-00");

        // Criando contas bancárias
        ContaBancaria conta1 = new ContaBancaria("12345", "Corrente");
        ContaBancaria conta2 = new ContaBancaria("67890", "Poupança");

        // Abrindo contas para o cliente
        cliente1.abrirConta(conta1);
        cliente1.abrirConta(conta2);

        // Depositando dinheiro nas contas
        conta1.depositar(1000);
        conta2.depositar(500);

        // Realizando transações
        conta1.sacar(200);
        conta1.transferir(conta2, 300);

        // Registrando transações
        Transacao t1 = new Transacao("Saque", 200, conta1, null);
        t1.registrar();

        Transacao t2 = new Transacao("Transferência", 300, conta1, conta2);
        t2.registrar();
    }
}

```
