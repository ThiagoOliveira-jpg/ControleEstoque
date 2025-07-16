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



