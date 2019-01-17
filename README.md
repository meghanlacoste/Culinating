# Culminating

package com.company;

import java.util.*;
import java.io.*;
import static com.company.ProjConstants.*;


public class Main {

    public static final int MAX_DATA= 1000;

    public static void main(String[] args) {
        // write your code here
        /*
   You are to write a Java program that implements many
  of the features required in the Dining Philosophers Problem (see Sections 2.3 - 2.5 from Tanenbaum's Modern
  Operating text). To perform this task you are to use timers, and perhaps randomly generated numbers to determine
  which philosopher is to try to "eat" next (note: you are not to use semaphores, or other mutual
  exclusion primitives). Your program must be able to function with a minimum of 2 philosophers, and a maximum
  of 10. Each of the philosophers should be a separate object that is created from a single class that implements
   an interface. The interface must have at a minimum the set and get methods for the philosophers health that
   can be in the following states: Full, Hungry, Starving, or Dead. With every timer firing, your program will
   generate a random number and this will be the first philosopher to try to "pick up" forks, and then you will
    generate additional random numbers to determine the next philosopher ... and continue this process until all
    "living" philosophers have tried to "pickup forks / eat". If a philosopher manages to pickup 2 forks then their
    state should be reset to "full" if not then his state should "degrade" by 1 i.e. Hungry -> starving.
     If a Philosopher "dies" then they will no longer be part of the Battle, and their associated fork is
     to be removed as well. The "Battle" will continue until only 1 Philosopher remains (wins) and all others are
        `"dead".

                User Input:
                - Name of file to be used, and each line will have multiple entries: <Number of Philosophers> <Battle Name 1> <Philosopher Name 1> .... <Philosopher Name "N">
                <Battle Name 2> <Philosopher Name 1> .... <Philosopher Name "N">
                <Battle Name 3> <Philosopher Name 1> .... <Philosopher Name "N">
                ....

                Screen Output:

                Battle Name 1
                ============
                Philosophers Timer Round: 1
                ---------------------------------------------
                <Philosopher Name> <Philosopher State>

                ... 2 Blank Lines ...

                Philosophers: Timer Round: 2
                -----------------------------------------------
                <Philosopher Name> <Philosopher State>

                ... 2 Blank Lines ...
                etc

                ***************************************************************************************
                ... 1 Blank Lines ...
                Battle Name 1
                ============
                Philosophers Timer Round: 1
                ---------------------------------------------
                <Philosopher Name> <Philosopher State>

                ... 2 Blank Lines ...

                Philosophers: Timer Round: 2
                -----------------------------------------------
                <Philosopher Name> <Philosopher State>

                ... 2 Blank Lines ...
                etc
                ***************************************************************************************
                ... 1 Blank Lines ...
                etc

                Additional Information:
                - Please skim read Sections 2.3 - 2.5 from Tanenbaum's Modern Operating systems section 2.5 contains a description of the problem.
         */

        String userFileName;

        String arr_philosophers[][] = new String [10][2];


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

                while (scanUserFile.hasNextLine()) {

                    String line = scanUserFile.nextLine();

                    for (int i = 0; i < 12; i++) {
                        if (scanUserFile.hasNext()) {

                            // sets 'n' - the dimensions of the 2D array to be the first value in the file
                            if (i == 0) {

                                battleName = scanUserFile.next();
                                System.out.print(" "+ battleName);

                            } else {

                                arr_philosophers[i][0]= scanUserFile.next();
                                System.out.print(" "+ arr_philosophers[i][0]);


                                // stores the values in the file in the 2D array

                            }

                        } else {
                        // ---------------------------------------------

                            System.out.println();
                            scanUserFile.nextLine();
                            break;


                    }// end for-loop

                }


                }

                // The scanner detected no other integers
                // - closes the scanner for the file
                // - breaks out of the for loop
                //
                System.out.print("\n\nDataFileFILE has been completely READ");
                scanUserFile.close();


            } catch (FileNotFoundException e) {
                System.out.println(e);
                e.printStackTrace();
            }







        }// end main method
    }// end main class

