Sistema de Controle de Estoque em Java, utilizando orientação a objetos, estrutura de listas e interação por console. Projeto acadêmico focado em lógica de programação e boas práticas de codificação.

# ControleEstoque
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Estoque estoque = new Estoque();

        int opcao;

        do {
            System.out.println("\n=== SISTEMA DE CONTROLE DE ESTOQUE ===");
            System.out.println("1 - Cadastrar produto");
            System.out.println("2 - Listar produtos");
            System.out.println("3 - Entrada de estoque");
            System.out.println("4 - Saída de estoque");
            System.out.println("5 - Valor total em estoque");
            System.out.println("0 - Sair");
            System.out.print("Escolha uma opção: ");
            opcao = sc.nextInt();

            switch (opcao) {
                case 1:
                    System.out.print("Nome: ");
                    sc.nextLine(); // consumir quebra de linha
                    String nome = sc.nextLine();
                    System.out.print("Código: ");
                    int codigo = sc.nextInt();
                    System.out.print("Quantidade inicial: ");
                    int qtd = sc.nextInt();
                    System.out.print("Preço unitário: ");
                    double preco = sc.nextDouble();
                    Produto p = new Produto(nome, codigo, qtd, preco);
                    estoque.adicionarProduto(p);
                    break;

                case 2:
                    estoque.listarProdutos();
                    break;

                case 3:
                    System.out.print("Código do produto: ");
                    int codEntrada = sc.nextInt();
                    Produto entrada = estoque.buscarPorCodigo(codEntrada);
                    if (entrada != null) {
                        System.out.print("Quantidade a adicionar: ");
                        int add = sc.nextInt();
                        entrada.adicionarEstoque(add);
                    } else {
                        System.out.println("Produto não encontrado.");
                    }
                    break;

                case 4:
                    System.out.print("Código do produto: ");
                    int codSaida = sc.nextInt();
                    Produto saida = estoque.buscarPorCodigo(codSaida);
                    if (saida != null) {
                        System.out.print("Quantidade a remover: ");
                        int rem = sc.nextInt();
                        saida.removerEstoque(rem);
                    } else {
                        System.out.println("Produto não encontrado.");
                    }
                    break;

                case 5:
                    double total = estoque.calcularValorTotal();
                    System.out.printf("Valor total em estoque: R$ %.2f%n", total);
                    break;

                case 0:
                    System.out.println("Encerrando o sistema.");
                    break;

                default:
                    System.out.println("Opção inválida.");
            }

        } while (opcao != 0);

        sc.close();
    }
}


New name file: Produto.Java
 
import java.util.ArrayList;

public class Produto {
    private String nome;
    private int codigo;
    private int quantidade;
    private double preco;

    public Produto(String nome, int codigo, int quantidade, double preco) {
        this.nome = nome;
        this.codigo = codigo;
        this.quantidade = quantidade;
        this.preco = preco;
    }

    public String getNome() {
        return nome;
    }

    public int getCodigo() {
        return codigo;
    }

    public int getQuantidade() {
        return quantidade;
    }

    public double getPreco() {
        return preco;
    }

    public void adicionarEstoque(int qtd) {
        this.quantidade += qtd;
    }

    public void removerEstoque(int qtd) {
        if (qtd <= this.quantidade) {
            this.quantidade -= qtd;
        } else {
            System.out.println("Erro: Estoque insuficiente.");
        }
    }

    public double valorTotal() {
        return this.quantidade * this.preco;
    }

    @Override
    public String toString() {
        return String.format("Código: %d | Nome: %s | Qtd: %d | Preço: R$ %.2f | Total: R$ %.2f",
                codigo, nome, quantidade, preco, valorTotal());
    }
}


New name file: Estoque.Java 


import java.util.ArrayList;
import java.util.Scanner;

public class Estoque {
    private ArrayList<Produto> produtos = new ArrayList<>();

    public void adicionarProduto(Produto p) {
        produtos.add(p);
    }

    public Produto buscarPorCodigo(int codigo) {
        for (Produto p : produtos) {
            if (p.getCodigo() == codigo) {
                return p;
            }
        }
        return null;
    }

    public void listarProdutos() {
        if (produtos.isEmpty()) {
            System.out.println("Nenhum produto cadastrado.");
        } else {
            for (Produto p : produtos) {
                System.out.println(p);
            }
        }
    }

    public double calcularValorTotal() {
        double total = 0;
        for (Produto p : produtos) {
            total += p.valorTotal();
        }
        return total;
    }
}








