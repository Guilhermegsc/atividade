# atividade/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package atividadepi.guilhermegomesdasilva;

import java.util.Scanner;

/**
 *
 * @author Guilherme Gomes da Silva
 */
public class AtividadePIGuilhermeGomesDaSilva {

    static Scanner sc = new Scanner(System.in);

    /**
     * @param args the command line arguments
     */
    static int procuraPosicao(String[] nome) {
        int posicaoDesoculpada = -1;
        for (int contador = 0; contador < 10; contador++) {
            if (nome[contador] == null) {
                posicaoDesoculpada = contador;
                break;
            }

        }
        return posicaoDesoculpada;
    }

    static int procuraPosicoes(String[] nome) {
        int contador = 0;
        int posicoesLivres = 0;
        while (contador < 10) {
            if (nome[contador] == null) {
                posicoesLivres++;
            }
            contador++;
        }

        return posicoesLivres;
    }

    static String[] adicionaContato(String nome[], String telefone[], int posicaoDesoculpada) {
        System.out.print("Nome: ");
        nome[posicaoDesoculpada] = sc.next();
        System.out.print("Telefone: ");
        telefone[posicaoDesoculpada] = sc.next();

        int posicoesLivres = procuraPosicoes(nome);
        System.out.println("Contato salvo com sucesso. Ainda podem ser cadastrados " + posicoesLivres + "contatos.");

        return nome;
    }
    

    static void apresentaNome(String nome[], int posicoesOcupadas[]) {
        for (int contador = 0; contador < posicoesOcupadas[0]; contador++) {
            System.out.println(nome[contador]);

        }

    }

    static int pesquisaContato(String nome[]) {
        System.out.println("Nome a ser pesquisado: ");
        String nomePesquisa = sc.next();
        
        int encontrado = -1;
        for (int contador = 0; contador < 10; contador++) {
            if (nome[contador].equalsIgnoreCase(nomePesquisa)) {
                encontrado = contador;
            }

        }
        return encontrado;
    }

    static String[] removeNome(String nome[], int posicoesOcupadas[], String remova) {
        // Já que deve haver uma nova pesquisa se o nome está na lista então essa função irá chamar a anterior.
        int posicao = pesquisaNome(nome, posicoesOcupadas, remova);
        if (posicao != -1) {
            for (int contador = posicao; contador < posicoesOcupadas[0]; contador++) {
                nome[contador] = nome[contador + 1];
            }
            posicoesOcupadas[0]--;
        } else {
            System.out.println("O nome não foi encontrado.");
        }
        return nome;
    }

    public static void main(String[] args) {
        // TODO code application logic here

        String[] nome = new String[10];
        String[] telefone = new String[10];

        int opcao = 1;

        while (opcao != 0) {
            System.out.println("1 - Incluir um contato.");
            System.out.println("2 - Alterar os dados.");
            System.out.println("3 - Pesquisar um contato.");
            System.out.println("4 - Remover um contato.");
            System.out.println("5 - Listar todos os contatos.");
            System.out.println("0 - Sair da agenda.");

            opcao = sc.nextInt();

            switch (opcao) {
                case 1:
                    int posicaoDesoculpada = procuraPosicao(nome);
                    if (posicaoDesoculpada == -1) {
                        System.out.println("A lista de contatos ja esta completa.");
                    } else {
                        adicionaContato(nome, telefone, posicaoDesoculpada);
                    }
                    break;
                case 2:
                    int encontrado = pesquisaContato(nome);
                    if(encontrado == -1){
                        System.out.println("Nome não encontrado.");
                    }
                    else{
                    adicionaContato(nome, telefone, encontrado);
                    }
                case 3:
                    if (posicoesOcupadas[0] == 0) {
                        System.out.println("A lisa esta vazia.");
                    } else {
                        apresentaNome(nome, posicoesOcupadas);
                    }
                    break;
                case 3:
                    System.out.println("Digite o nome a ser pesquisado.");
                    String nomePesquisa = sc.next();
                    int encontrado = pesquisaNome(nome, posicoesOcupadas, nomePesquisa);
                    // Se encontrado estiver com o valor diferente de que foi inicializado estará 
                    // com o valor onde foi encontrado.
                    if (encontrado != -1) {
                        System.out.println("Encontrado na posicao: " + encontrado);

                    } else {
                        System.out.println("O nome não foi encontrado.");
                    }
                    break;
                case 4:
                    System.out.println("Digite o nome a ser removido.");
                    String remova = sc.next();
                    removeNome(nome, posicoesOcupadas, remova);
            }

        }

    }

}
