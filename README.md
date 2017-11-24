   import java.util.*;
   import java.util.Scanner;
   public class ba{
      Scanner input = new Scanner(System.in);
      public static final boolean DEBUG = true;  
      public static void breakln()
      {
         System.out.println("_____________________________________");
         System.out.println("");
      }
      public static void createBoard(String[][] board)
      {
         for(int r = 0; r < board.length; r++)
         {
            for(int c = 0; c < board[0].length; c++)
            {
               board[r][c] = "0";
            }
         }
      }
      public static void showBoard(String[][] board)
      {
         breakln();
         for(int r = 0; r < board.length; r++)
         {
            if(DEBUG == true)
            {
               for(int c = 0; c < board[0].length; c++)
               {
                  System.out.print(" "+board[r][c]);
               }
               System.out.println("");
            }
            else
            {
               for(int c = 0; c < board[0].length; c++)
               {
                  if(board[r][c].equals("4"))
                  {
                     System.out.print(" "+"~");
                  }
                  else
                  {
                     System.out.print(" "+board[r][c]);
                  }
               }
               System.out.println("");
            }
         }
         breakln();
      }
      public static void createShip5(String[][] board,int size)
      {
         if(Math.random() < 0.5)
         {
            int col = (int)(Math.random()*5);
            int row = (int)(Math.random()*7);
            for(int i = 0; i<size; i++)
            {
               board[row][col+i] = "5";
            }
         }
         else
         {
            int col = (int)(Math.random()*7);
            int row = (int)(Math.random()*5);
            for(int i = 0; i<size; i++)
            {
               board[row+i][col] = "5";
            }
         }
      }
      public static void createShip4(String[][] board,int size)
      {  
         int tip = 0;
         while (tip < 2){
         if(Math.random() < 0.5)
         {
            int col = (int)(Math.random()*5);
            int row = (int)(Math.random()*7);
            for(int i = 0; i<size; i++)
            {
               board[row][col+i] = "4";
            }
         }
         else
         {
            int col = (int)(Math.random()*7);
            int row = (int)(Math.random()*5);
            for(int i = 0; i<size; i++)
            {
               board[row+i][col] = "4";
            }
         }
         tip++;
        }
      }
      public static void createShip3(String[][] board,int size)
      {  
         int tip = 0;
         while (tip < 3){
         if(Math.random() < 0.5)
         {
            int col = (int)(Math.random()*5);
            int row = (int)(Math.random()*7);
            for(int i = 0; i<size; i++)
            {
               board[row][col+i] = "3";
            }
         }
         else
         {
            int col = (int)(Math.random()*7);
            int row = (int)(Math.random()*5);
            for(int i = 0; i<size; i++)
            {
               board[row+i][col] = "3";
            }
         }
         tip++;
        }
      }    
      public static void createShip2(String[][] board,int size)
      {  
         int tip = 0;
         while (tip < 4){
         if(Math.random() < 0.5)
         {
            int col = (int)(Math.random()*5);
            int row = (int)(Math.random()*7);
            for(int i = 0; i<size; i++)
            {
               board[row][col+i] = "2";
            }
         }
         else
         {
            int col = (int)(Math.random()*7);
            int row = (int)(Math.random()*5);
            for(int i = 0; i<size; i++)
            {
               board[row+i][col] = "2";
            }
         }
         tip++;
        }
      }        
      public static int userFire(String[][] board, int hits, int torps)
      {
         Scanner input = new Scanner(System.in);
         int row;
         int col;
         System.out.println("¡Tienes: "+ torps +" torpedos disponibles!");
         System.out.println("Selecciona la fila que quieres disparar: ");
         row = input.nextInt();
         while(row > 10 || row < 1) // Error checking for row
         {
            System.out.println("Solo numeros validos entre 1 y 10");
            row = input.nextInt();
         }
         System.out.println("Selecciona la columna que quieres disparar: ");
         col = input.nextInt();
         while(col > 10 || col < 1) // Error checking for column
         {
            System.out.println("Solo numeros validos entre 1 y 10");
            col = input.nextInt();
         }         
         if(board[row-1][col-1].equals("5")){
            hits ++;
            torps ++;
            System.out.println("~~~~~~~ IMPACTO ~~~~~~~");
            board[row-1][col-1] = "0";
         }
         else if(board[row-1][col-1].equals("4")){       
              System.out.println("~~~~~~~ IMPACTO ~~~~~~~");
              board[row-1][col-1] = "0";
              torps ++;
              hits ++;
           }
           else if(board[row-1][col-1].equals("3")){
                System.out.println("~~~~~~~ IMPACTO ~~~~~~~");
                board[row-1][col-1] = "0";
                torps ++;
                hits ++;
               }
               else if(board[row-1][col-1].equals("2")){
                       System.out.println("~~~~~~~ IMPACTO ~~~~~~~");
                       board[row-1][col-1] = "0";
                       torps ++; 
                       hits ++;
                      }
         else{
          System.out.println("~~~~~~~ FALLASTE ~~~~~~~");
          board[row-1][col-1] = "M";
          torps --;     
         }
         return hits;
      }
      public static void finall(int hits, int torps)
      {
          Scanner input = new Scanner(System.in);
         if(hits < 4)
            System.out.println("Perdiste, no has hundido la flota.");
         if(torps < 1)
            System.out.println("Agotaste los torpedos");
         else
            if(hits >= 4)
            {
               System.out.println("Felicidades, has ganado, ¡gracias por jugar!");
            }
      }
      public static void main(String[] arg)
      {
        Scanner input = new Scanner(System.in);
        int again = 1;
        while(again==1){  
         String[][] board = new String[10][10];
         createBoard(board);
         createShip2(board, 2);
         createShip3(board, 3);
         createShip4(board, 4);
         createShip5(board, 5);
         int torps = 10;
         int hits = 0;
         while(torps > 0 && hits < 4)
         {
            showBoard(board);
            hits = userFire(board, hits, torps);
            torps--;
         }
         finall(hits, torps);
         do{
           System.out.println("Buen juego, ¿quieres jugar otra vez? (Si=1 No=2)");
           again = input.nextInt();
           }while(again >2 || again <0);
        }
      }
    }

  
   
