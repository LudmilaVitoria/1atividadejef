import java.util.ArrayList;
import java.util.Scanner;

class Produto {
    int codigo;
    String descricao;
    double preco;
    String imagem;

    Produto(int codigo, String descricao, double preco, String imagem) {
    this.codigo = codigo;
    this.descricao = descricao;
    this.preco = preco;
    this.imagem = imagem;
    }

 @Override
    public String toString() {
    return "|Código: " + codigo +
          " | Descrição: " + descricao +
          " | Preço: R$ " + String.format("%.2f", preco) +
          " | Imagem: " + imagem;
    }
}

public class CadastroProdutos {
    static ArrayList<Produto> produtos = new ArrayList<>();
    static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
      
        produtos.add(new Produto(1, "Cachorro Quente", 4.00, "C:\\Users\l\udmi\\Downloads\\cachorro quente.jpg"));
        produtos.add(new Produto(2, "X-Salada", 4.50, "C:\\Users\\ludmi\\Downloads\\x-salada.jpg"));
        produtos.add(new Produto(3, "X-Bacon", 5.00, "C:\\Users\\ludmi\\Downloads\\x-bacon.jpg"));
        produtos.add(new Produto(4, "Torrada simples", 2.00, "C:\\Users\\ludmi\\Downloads\\torrada simples.jpg"));
        produtos.add(new Produto(5, "Refrigerante", 1.50, "C:\\Users\\ludmi\\Downloads\\refrigerante.jpg"));

        int opcao;
        do {
            System.out.println("\n-_____________);
            System.out.println("\n|====MENU ====|");
            System.out.println("  |1 - Cadastrar|");
            System.out.println("  |2 - Editar   | ");
            System.out.println("  |3 - Excluir  | ");
            System.out.println("  |4-  Listar   |");
            System.out.println("  |5 - Vender   |");
            System.out.println("  |0 - Sair     |");
            System.out.println("\n_______________");
            opcao = sc.nextInt();
            sc.nextLine();

            switch (opcao) {
                case 1 -> cadastrar();
                case 2 -> editar();
                case 3 -> excluir();
                case 4 -> listar();
                case 5 -> vender();
                case 0 -> System.out.println("Saindo...");
                default -> System.out.println("Opção inválida.");
            }
           } while (opcao != 0);
    }

     static void cadastrar() {
        System.out.print("Código do produto: ");
        int codigo = sc.nextInt();
        sc.nextLine();

        System.out.print("Descrição: ");
        String descricao = sc.nextLine();

        System.out.print("Preço: ");
        double preco = sc.nextDouble();
        sc.nextLine();

        System.out.print("Imagem: ");
        String imagem = sc.nextLine();

        produtos.add(new Produto(codigo, descricao, preco, imagem));
        System.out.println("Produto cadastrado com sucesso!");
    }

    static void editar() {
        System.out.print("Código do produto para editar: ");
        int codigo = sc.nextInt();
        sc.nextLine();

        for (Produto p : produtos) {
            if (p.codigo == codigo) {
                System.out.print("Nova descrição: ");
                p.descricao = sc.nextLine();
                System.out.print("Novo preço: ");
                p.preco = sc.nextDouble();
                sc.nextLine();
                System.out.print("Nova imagem: ");
                p.imagem = sc.nextLine();
                System.out.println("Produto atualizado!");
                return;
            }
        }
        System.out.println("Produto não encontrado.");
    }

    static void excluir() {
        System.out.print("Código do produto para excluir: ");
        int codigo = sc.nextInt();
        sc.nextLine();

        produtos.removeIf(p -> p.codigo == codigo);
        System.out.println("Produto removido (se existia).");
    }

    static void listar() {
        if (produtos.isEmpty()) {
            System.out.println("Nenhum produto cadastrado.");
            return;
        }
        for (Produto p : produtos) {
            System.out.println(p);
        }
    }

    static void vender() {
        System.out.print("Código do produto: ");
        int codigo = sc.nextInt();
        System.out.print("Quantidade: ");
        int qtd = sc.nextInt();

        for (Produto p : produtos) {
            if (p.codigo == codigo) {
                double total = p.preco * qtd;
                System.out.printf("Total: R$ %.2f%n", total);
                return;
            }
        }
        System.out.println("Produto não encontrado.");
    }
}
