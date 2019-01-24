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



        // USE PARAMERATIZED CONSTRUCTOR THAT DEFAULTS THE OBJECTS IN THE STRING ARRAY AS A HEALTHY STATE



            ///  - generate random number for which philosopher will go first. That philosopher is garrunteed two forks/
              - using a method similar to the prime number program (looping through indexes by a certain amount and returning to the
              beginning if that goes over the max index taking the remainder as the new starting number and continuing) determine
              which of he philosophers will pick up next
              - the forks that a philosopher has available depends on the surrounding philosophers on either side of the array.
               (e. if the two philosophers on either side of them have picked up the forks they cannot pick them up).
              - philopsophers will pick up all forks available to them (the ones on either side of them) when it is their turn
              - once all the philosophers have attempted to pickup forks the imer moves to the next round and a new random philosopher
              starts.



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

        String arr_philosophers[][] = new String [11][100];



        String battleName;

        System.out.println("");
        System.out.println("Please type in the file name\n");

        //create a variable s of type scanner to process input from "System.in"
        Scanner scanSystemIn = new Scanner(System.in);

        // Use the Scanner "s" to get the "next" input from "System.in"
        userFileName = scanSystemIn.next();

        // Display the user input now stored in "userInput"
        System.out.println("\nThe user input: " + userFileName);

        System.out.println("\n==================================================\n");


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

                //System.out.println(" START " );

                line = scanUserFile.nextLine();

                //System.out.println(" line: " + line);


                String[] temp = line.split(" ");
                //System.out.println(" --------------- " + temp.length);


                for (int i=0; i < 10; i++){

                    if (i < temp.length) {
                        arr_philosophers[i][counter] = temp[i];
                        //System.out.print(" counter " + counter + " i " + i + " " + arr_philosophers[i][counter] + " ");
                        System.out.print(arr_philosophers[i][counter] + " ");

                    } else {
                        if(scanUserFile.hasNextLine()) {
                            counter +=1;
                        }

                        break;
                    }


                }

                // ---------------------------------------------
                System.out.println("\n==================================================\n");




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

        int numbDead = 0;

        for (int i=0; i < 11; i++){

            // change the column number depending on which battle

            if (i==0){
                battleName =  arr_philosophers[i][0];
                System.out.println("Battle Name:" + battleName + "\n");

            } else if (arr_philosophers[i][0]!= null){

                // Philosophers PI = new Philosophers(i,FULL);



                // this is when the philosophers class is called to run all of the states
                // call to run timer method
                //

            }

        }


        Philosophers P = new Philosophers();

        int totalPhil = P.totalPhil(arr_philosophers,0);
        System.out.println("total number of philosophers: " + totalPhil);

        P.transferArray(arr_philosophers,0);
        int random = (int )(Math.random() * totalPhil + 1);
        System.out.println ("first philosopher to eat: " + random);

       int nextPrime =  P.findNextPrime(P.totalPhil(arr_philosophers,0));
       System.out.println( "next prime " + nextPrime );


        P.setState(random, nextPrime);
        // P.setState();

        for (int i=1; i <= totalPhil; i++){
            System.out.println("---------------");
            //System.out.println(" i " + i + " " + P.getState(i));

            switch (P.getState(i)){

                case FULL: {
                    System.out.println("Name: " + arr_philosophers[i][0]+ "State: " + "Full");

                    break;
                }

                case HUNGRY: {

                    System.out.println("Name: " + arr_philosophers[i][0]+ "State: " + "Hungry");

                    break;
                }

                case STARVING: {

                    System.out.println("Name: " + arr_philosophers[i][0]+ "State: " + "Starving");

                    break;
                }

                case DEAD: {

                    System.out.println("Name: " + arr_philosophers[i][0]+ "State: " + "Dead");
                    // remove philosopher from array by setting the value to null or invalid
                    // you will have to remake your methods so it skips over "dead" or moves everything down one in the array
                    break;
                }


            }


        }

        // send philosopher and state to the philosophers class
        // create temp int array with each of the philosophers number and in the second column their state (FULL,HUNGRY
        // STARVING or DEAD)















    }// end main method
}// end main class



