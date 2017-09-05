------------------------------------------------------Conta Interface Texto--------------------------------------------------
import java.util.Scanner;
public class ContaInterfaceTexto
{
 
      public void QueriaSerMainMasNaoPode()
      {
         Scanner teclado = new Scanner(System.in);
         String c;
         String n;       
         int x;
         ContaDB db = new ContaDB();
         while(1==1){
            System.out.printf ("Digite 1 para Inclusao de registro.\n");
            System.out.printf ("Digite 2 para Exclusao de registro.\n");
            System.out.printf ("Digite 3 para Consulta de registro.\n");
            System.out.printf ("Digite 4 para Alteracao de registro.\n");
            System.out.printf ("Digite 5 para Lista de registro.\n");
            System.out.printf ("Digite 9 para Sair;\n");
            System.out.printf ("Insira funcao desejada: ");
            switch ( Integer.parseInt ( teclado.nextLine())){  
               case 1: // Incluir
               db.incluir();
               System.out.printf("Registro Incluido!\n");
               break;
               case 2: // Exclusao
               db.excluir();
               break;
               case 3: // Consulta
               db.consultar();
               System.out.printf("Done!\n");
               break;
               case 4: // Alterar
               db.alterar();
               break;
               case 5: // Listar
               db.listar();
               System.out.printf("Done!\n");
               break;
               case 9: // Sair
               System.exit(0);
               break;
               default:
               System.out.printf("Opção inválida");
               break;
            }
         }
}
-------------------------------------------------------------------------Conta DB--------------------------------------------------
import java.util.Scanner;
public class ContaDB
{
   Scanner teclado = new Scanner(System.in);
   Conta K[] = new Conta[10];
   PessoaDB db2 = new PessoaDB();

 //---------------------------------------
   public void incluir(){
    for (int x=0; K[x]!=null;x++);
      if (x==10){
         System.out.printf ("Nao ha mais espaco para novos registros.\n Por favor apague um registro e tente novamente");
      }
      String c = db2.consultar();
      if (cpf==null || cpf=="")
      {
         System.out.printf ("CPF nao encontrado!\n");
         return;
      }
      System.out.printf ("Insira o Numero para conta: ");
      String n = teclado.nextLine();     
      System.out.printf ("Insira o saldo da conta: ");
      float s = teclado.nextLine();
      while (s<0)
      {
          System.out.printf ("Saldo invalido! Insira saldo POSITIVO: ");
          s = teclado.nextLine();
      }
      K[x] = new Conta(c,n,s);
   }//Fim Inlcuir
//---------------------------------------------  
  public void excluir(){
      System.out.printf ("Insira o CPF para exclusao: ");
      String ex = teclado.nextLine();
      for(int y=0;y<K.length; y++){
         if (K[y]!=null && K[y].getCpf().equals(ex)){
            K[y] = null;
            System.out.printf ("Registro Apagado!\n");
            break;
         }//end if
      }//end for
   }//end excluir
//---------------------------------------------
   public void listar(){
      for(int y=0;y<K.length; y++){
         while(K[y]==null&&y<K.length-1){
            y++;
            //System.out.printf ("Pulando registro %d",y);
         }
         if(K[y]==null){
            break;
         }
         K[y].imprime();
      }//end if
   }//end mostrar todos
//--------------------------------------------- 
   public void consultar(){
   System.out.printf ("Insira o CPF para consulta: ");
      String ex = teclado.nextLine();
      for(int y=0;K[y]!=null&&y<K.length; y++){
          if (K[y].getCpf().equals(ex)){
            K[y].imprime();
            return;
         }//end if
      }//end for
      System.out.printf ("Registro Nao Encontrado!\n ");
   }//end consulta
//---------------------------------------------  
   public void alterar(){
     
      System.out.printf ("Insira o CPF para alteracao: ");
      String ex = teclado.nextLine();
      for(int y=0;K[y]!=null && y<K.length; y++){
        String a = K[y].getCpf();
         if (K[y].getCpf().equals(ex)){
            System.out.printf ("Digite 1 para alterar CPF e 2 para alterar Nome:  ");
            int alt = teclado.nextInt();
            teclado.nextLine();
            if (alt==1){
               System.out.printf ("Insira novo CPF: ");
               String c = teclado.nextLine();
               K[y].setCpf(c);
               System.out.printf("Regstro Alterado!\n");
            }
            else if (alt==2){
               System.out.printf ("Insira novo nome: ");
               String n = teclado.nextLine();
               K[y].setNome(n);
               System.out.printf("Regstro Alterado!\n");
            }
            else System.out.printf ("Opcao invalida!");
            K[y].imprime();
            break;
         }//end if
      }//end for
   }//end alterar
//---------------------------------------------
}
--------------------------------------------------------------------------Conta--------------------------------------------------
public class Conta 
{
  private String cpfConta;  // atributo
  private String numConta; // atributo
  private float saldo;
  
  public Conta (String c, String n, float s){
     setCpfConta(c);
     setNumConta(n);
     setSaldo(s);
  } 
 
  public void setNumConta(String n){numConta = n;}
  public String getNumConta(){return numConta;}
 
  public void setCpfConta(String c){cpfConta = c;}
  public String getCpfConta(){return cpfConta;}
  
  public void setSaldo(float s){saldo = s;}
  public float getSaldo(){return saldo;}
  
  public void imprime(){ System.out.printf ( "cpf = %s\nnumero = %s\n saldo = %f\n\n",cpfConta,numConta,saldo); } // fim do método imprime

} // fim da classe
------------------------------------------------------------------MenuGeral--------------------------------------------------
import java.util.Scanner;
public class MenuGeral
{
   public static void main (String args[])
   {
      Scanner teclado = new Scanner(System.in);
      ContaInterfaceTexto CC = new ContaInterfaceTexto();
      PessoaInterface CP = new PessoaInterface();
      System.out.printf ("Digite 1 para Cadastro de Pessoas.\n");
      System.out.printf ("Digite 2 para Cadastro de Conta Corrente.\n");
      System.out.printf ("Digite 9 para Sair.\n");
      System.out.printf ("Insira funcao desejada: ");
      switch ( Integer.parseInt ( teclado.nextLine())){  
               case 1: // Cadastro Pessoas
               CP.TambemQueriaSerMain();
               break;
               case 2: // Cadastro CC
               CC.QueriaSerMainMasNaoPode();
               break;
               case 9: // Sair
               System.exit(0);
               break;
               default:
               System.out.printf("Opção inválida");
               break;
      }
   }
}
-----------------------------------------------------------------pessoa--------------------------------------------------
public class Pessoa 
{
  private String cpf;  // atributo
  private String nome; // atributo
  
  public Pessoa (String c, String n){
     setCpf(c);
     setNome(n);
  } 
 
  public void setNome(String n){nome = n;}
  public String getNome(){return nome;}
 
  public void setCpf(String c){cpf = c;}
  public String getCpf(){return cpf;}
  
  public void imprime(){ System.out.printf ( "cpf = %s\nnome = %s\n\n",cpf,nome); } // fim do método imprime

} // fim da classe

----------------------------------------------------------------Pessoa DB--------------------------------------------------
import java.util.Scanner;
public class PessoaDB
{
   Scanner teclado = new Scanner(System.in);
   Pessoa Q[] = new Pessoa[10];

 //---------------------------------------
   public void incluir(){
      String c;
      String n;
      int x;
      
      for (x=0; Q[x]!=null;x++);
      if (x==10){
         System.out.printf ("Nao ha mais espaco para novos registros.\n Por favor apague um registro e tente novamente");
      }
      System.out.printf ("Insira CPF: ");
      c = teclado.nextLine();
      System.out.printf ("Insira Nome: ");
      n = teclado.nextLine();
      Q[x] = new Pessoa(c,n);
   }//Fim Inlcuir
//---------------------------------------------  
  public void excluir(){
      System.out.printf ("Insira o CPF para exclusao: ");
      String ex = teclado.nextLine();
      for(int y=0;y<Q.length; y++){
         if (Q[y]!=null && Q[y].getCpf().equals(ex)){
            Q[y] = null;
            System.out.printf ("Registro Apagado!\n");
            break;
         }//end if
      }//end for
   }//end excluir
//---------------------------------------------
   public void listar(){
      for(int y=0;y<Q.length; y++){
         while(Q[y]==null&&y<Q.length-1){
            y++;
            //System.out.printf ("Pulando registro %d",y);
         }
         if(Q[y]==null){
            break;
         }
         Q[y].imprime();
      }//end if
   }//end mostrar todos
//--------------------------------------------- 
   public String consultar(){
   System.out.printf ("Insira o CPF: ");
      String ex = teclado.nextLine();
      for(int y=0;Q[y]!=null&&y<Q.length; y++){
          if (Q[y].getCpf().equals(ex)){
            Q[y].imprime();
            return (Q[y].getCpf());
         }//end if
      }//end for
      System.out.printf ("Registro Nao Encontrado!\n ");
      return ("0");
   }//end consulta
//---------------------------------------------  
   public void alterar(){
      System.out.printf ("Insira o CPF para alteracao: ");
      String ex = teclado.nextLine();
      for(int y=0;Q[y]!=null && y<Q.length; y++){
        String a = Q[y].getCpf();
         if (Q[y].getCpf().equals(ex)){
            System.out.printf ("Digite 1 para alterar CPF e 2 para alterar Nome:  ");
            int alt = teclado.nextInt();
            teclado.nextLine();
            if (alt==1){
               System.out.printf ("Insira novo CPF: ");
               String c = teclado.nextLine();
               Q[y].setCpf(c);
               System.out.printf("Regstro Alterado!\n");
            }
            else if (alt==2){
               System.out.printf ("Insira novo nome: ");
               String n = teclado.nextLine();
               Q[y].setNome(n);
               System.out.printf("Regstro Alterado!\n");
            }
            else System.out.printf ("Opcao invalida!");
            Q[y].imprime();
            break;
         }//end if
      }//end for
   }//end alterar
//---------------------------------------------
}
------------------------------------------------------------- Pessoa Interface--------------------------------------------------
import java.util.Scanner;
public class PessoaInterface
{
 
      public void  TambemQueriaSerMain()
      {
         Scanner teclado = new Scanner(System.in);
         String c;
         String n;       
         int x;
         PessoaDB db = new PessoaDB();
         while(1==1){
            System.out.printf ("Digite 1 para Inclusao de registro.\n");
            System.out.printf ("Digite 2 para Exclusao de registro.\n");
            System.out.printf ("Digite 3 para Consulta de registro.\n");
            System.out.printf ("Digite 4 para Alteracao de registro.\n");
            System.out.printf ("Digite 5 para Lista de registro.\n");
            System.out.printf ("Digite 9 para Sair;\n");
            System.out.printf ("Insira funcao desejada: ");
            switch ( Integer.parseInt ( teclado.nextLine())){  
               case 1: // Incluir
               db.incluir();
               System.out.printf("Registro Incluido!\n");
               break;
               case 2: // Exclusao
               db.excluir();
               break;
               case 3: // Consulta
               String TEMP = db.consultar();
               System.out.printf("Done!\n");
               break;
               case 4: // Alterar
               db.alterar();
               break;
               case 5: // Listar
               db.listar();
               System.out.printf("Done!\n");
               break;
               case 9: // Sair
               System.exit(0);
               break;
               default:
               System.out.printf("Opção inválida");
               break;
            }
         }
}

   
      
           
        
      }//fim metodo main

      
           
