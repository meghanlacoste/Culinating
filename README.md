# Culminating
package com.company;

import java.util.*;
import java.io.*;
import static com.company.ProjConstants.*;

public class Main {

    public static final int MAX_DATA= 100;

    public static void main(String[] args) {
        // write your code here


        String userFileName;

        String arr_philosophers[][] = new String [11][MAX_DATA];



        String battleName;

        System.out.println("");
        System.out.println("Please type in the file name\n");

        //create a variable s of type scanner to process input from "System.in"
        Scanner scanSystemIn = new Scanner(System.in);

        // Use the Scanner "s" to get the "next" input from "System.in"
        userFileName = scanSystemIn.next();

        // Display the user input now stored in "userInput"
        System.out.println("\nThe user input: " + userFileName);



        // ---------------------------------------------
        //  "try" to process the file
        //



        try {
            // --------------------------------
            // create file, and scanner objects
            // - file object is called tempfilenums.txt and is in your project directory
            //   that is the same folder as the iml file
            //

            File userFile = new File(userFileName);
            Scanner scanUserFile = new Scanner(userFile);


            // ---------------------------------------------
            // Reads in values from the file in a for loop
            //\

            int counter = 0;
            String line;

            while (scanUserFile.hasNextLine()) {


                line = scanUserFile.nextLine();

                String[] temp = line.split(" ");



                for (int i=0; i < 11; i++){

                    if (i < temp.length) {
                        arr_philosophers[i][counter] = temp[i];

                    } else {
                        if(scanUserFile.hasNextLine()) {
                            counter +=1;
                        }

                        break;
                    }


                }



            }


            // The scanner detected no other integers
            // - closes the scanner for the file
            // - breaks out of the for loop
            //
            System.out.print("\n\nDataFileFILE has been completely READ\n\n");
            scanUserFile.close();


        } catch (FileNotFoundException e) {
            System.out.println(e);
            e.printStackTrace();
        }


        int totalBattles = 0;

        // loops over the columns of the array, adding to the total number of battles
        // until a column with no valid input is reached

        for (int j=0; j < MAX_DATA; j++) {
            if (arr_philosophers[0][j]!=null){

                totalBattles +=1;

            } else {
                break;
            }

        }



        int counter = 0;
        while (counter < totalBattles) {


            battleName =  arr_philosophers[0][counter];
            System.out.println("    Battle Name " + battleName + "\n");
            System.out.println("    =================");


            Philosophers P = new Philosophers();

            int totalPhil = P.totalPhil(arr_philosophers,counter);
            System.out.println("total phil " + totalPhil);


            // if the total number of philosophers is below 2 or above 10, the string array cannot be transferred

            if (totalPhil>=2 && totalPhil <=10) {

                P.transferArray(arr_philosophers,counter);

            } else {

                System.out.print("ERROR: THE AMOUNT OF PHILOSOPHERS MUST BE BETWEEN 2 AND 10");
            }


            //creates new int array to store which philosophers have died each round
            int dead [] = new int[11];

            int round = 0;
            int numbDead = 0;

            while ((totalPhil-numbDead) > 1) {



               for (int i = 0; i < 11; i++){
                   dead [i] = INVALID;
               }



                round +=1;

                System.out.println("\n\n\tPhilosophers Timer Round: " + round); //
                System.out.println("total phil this round " + P.totalPhil(arr_philosophers,counter));
                System.out.println("\t----------------------------" );


                boolean validRandom = false;


                // while loop executes until the random number generated is the index position of an alive
                while (!validRandom) {

                    // generates random number within the bounds of the total number of philosophers within the array
                    int random = (int )(Math.random() * totalPhil + 1);



                    // checks that the philosopher is still alive
                    if (arr_philosophers[random][counter] != null){


                                System.out.println("random " + random);



                                // finds next prime number using the current total philosophers as an index
                                int nextPrime =  P.findNextPrime(P.totalPhil(arr_philosophers,counter));

                                System.out.println("next prime value" + nextPrime);

                                System.out.println("\t ************ "  + P.findNextPrime((P.totalPhil(arr_philosophers,counter))));



                                // calls on the philosopher class passing the random number and the next prime as
                                // an argument

                                P.setState(random, nextPrime);
                                validRandom=true;


                    }

                }// end while !validRandom


                int counter2 = 0;

                for (int i = 1; i <= totalPhil; i++){

                    if (arr_philosophers[i][counter]!=null) {

                        counter2++;

                       // System.out.println ("counter " + counter2);


                        System.out.println();

                        switch (P.getState(i)) {

                            case FULL: {

                                System.out.println("\t\t" + arr_philosophers[i][counter] + "  " + "Full");

                                break;
                            }

                            case HUNGRY: {

                                System.out.println("\t\t" + arr_philosophers[i][counter] + "  " + "Hungry");

                                break;
                            }

                            case STARVING: {

                                System.out.println("\t\t" + arr_philosophers[i][counter] + "  " + "Starving");

                                break;
                            }

                            case DEAD: {

                                System.out.println("\t\t" + arr_philosophers[i][counter] + "  " + "Dead");

                                arr_philosophers[i][counter] = null;


                                dead[i]= i;
                                //

                                P.removePhilosopher(i);

                                System.out.println(" ************* "  + P.totalPhil(arr_philosophers,counter));

                                numbDead += 1;

                                System.out.println("number dead " + numbDead);

                                break;
                            }

                            default:{

                            }

                        }// end switch statement (P.getState(i))


                    }// end if statement that checks whether the value is null


                }// end for loop

                /*
                 for (int i =0; i< 11; i++){
                    if (dead[i] != INVALID){
                        P.removePhilosopher(i);

                        System.out.println(" ************* "  + P.totalPhil(arr_philosophers,counter));

                        numbDead += 1;
                         System.out.println( " dead: " + i + " number dead " + numbDead);
                    }
                }
                 */




            }// end while

            counter +=1;

            System.out.println("\n\n***************************************************************************************\n");



        }














    }// end main method
}// end main class
