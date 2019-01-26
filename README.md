package com.company;

/**
 * Created by 13549lac on 17/01/2019.
 */
import java.awt.*;

import static com.company.ProjConstants.*;

public class Philosophers implements Philosopher {

    // Declare Class Variables

    private int phil_state = INVALID;

    private int totalPhil = 0;

    int int_arr_phil[][] = new int[11][3];

    int nextPrime = 2;


    // example of paramaterized constructor for another possible solution
   /*
    public  Philosophers (int index, int state) {

        phil_num = index;
        phil_state = state;

    }
     */

    // takes in 2d string array as a parameter
    // returns the total number of philosophers in the array (int value)
    public int totalPhil(String arr_phil[][], int index) {

        totalPhil = 0;

        // the index starts at 1 because the value at index 0 is the battle name
        for (int i = 1; i < 11; i++) {

            // counter increases if the value at the index is not null
            if (arr_phil[i][index] != null) {

                totalPhil += 1;

            }

        }// end for

        return totalPhil;
    }


    // this method transfers the index of each philosopher in
    // pre - conditions:
    // the value at the index is not null
    // if the value is null all values at that index are set to INVALID

    public void transferArray(String arr_phil[][], int index) {

        for (int i = 1; i < 11; i++) {

            if (arr_phil[i][index] != null) {

                int_arr_phil[i - 1][0] = i;
                int_arr_phil[i - 1][1] = 0;
                int_arr_phil[i - 1][2] = FULL;

            } else {
                int_arr_phil[i - 1][0] = INVALID;
                int_arr_phil[i - 1][1] = INVALID;
                int_arr_phil[i - 1][2] = INVALID;
            }


        }


    }


 void removePhilosopher(int deadPhilosopher) {

        int x = INVALID;
        for (int i=0; i< 11; i++){
            if (int_arr_phil[i][0]==deadPhilosopher){

                x=i;
                break;
            }
        }

        for(int i = x+1; i < 10; i++) {

            int_arr_phil[i-1][0] = int_arr_phil[i][0];
            int_arr_phil[i-1][1] = int_arr_phil [i][1];
            int_arr_phil[i-1][2] = int_arr_phil [i][2];
        }

    }





    // returns the first prime value
    // greater than the square root of the total number of philosophers.

    // special cases for 10 and 6 because they are divisible by the corresponding
    // next prime number larger than their square root. To avoid looping over the same
    //indexes repeatedly, different prime values are assigned.

    public int findNextPrime(int input){

        if (input == 10 || input == 4){

            nextPrime = 3;
            return nextPrime;

        } else if (input == 6) {

            nextPrime = 5;
            return nextPrime;


        } else {

            input = (int) Math.sqrt(input);

            int counter;
            input++;

            while(true){

                counter = 0;

                for(int i = 2; i <= Math.sqrt(input); i ++){
                    if(input % i == 0)  counter++;
                }
                if(counter == 0) {

                    nextPrime =input;
                    return nextPrime;

                }else{
                    input++;
                    continue;
                }
            }

        }

    }




    // method that takes in the random index of the first philosopher to eat, and the first prime value
    // greater than the square root of the total number of philosophers.
    //
    public void setState(int firstPhil , int primeValue) {

                int forks = totalPhil;

                for (int i=0; i< totalPhil; i++){
                    int_arr_phil[i][1]=0;
                }


                switch (totalPhil){

                    case 2: {

                        System.out.println("CASE 2");

                        for (int i=0; i < 11; i++) {
                            if (int_arr_phil[i][0] == firstPhil) {

                                    int_arr_phil[i][1] = 2;
                                    int_arr_phil[i][2] = FULL;

                            } else if (int_arr_phil[i][0]!=INVALID) {

                                    int_arr_phil[i][1] = 0;
                                    int_arr_phil[i][2] -= 1;


                            }
                        }

                        break;
                    }

                    default: {


                        int primeIndex=0;


                                // finds the matching index to the philosopher to eat first
                                for (int i=0; i < 11; i++ ) {

                                    if (int_arr_phil[i][0]== firstPhil) {

                                        int_arr_phil[i][1] = 2;

                                         primeIndex = i;
                                    }
                                }

                        for (int i = 0; i < totalPhil; i++){

                            // special case that checks if it is the first value in the array (in which case it will
                            // share a side with the last philosopher in the array

                                        if (primeIndex == 0 ) {

                                                    if ((int_arr_phil[1][1] == 0) && (int_arr_phil[totalPhil - 1][1] == 0) && (forks>=2)) {


                                                        int_arr_phil[0][1] = 2;
                                                        int_arr_phil[0][2] = FULL;
                                                        forks -= 2;


                                                    } else {

                                                        int_arr_phil[0][1] = 0;
                                                        int_arr_phil[0][2] -= 1;
                                                    }



                                         // special case that checks if it is the first value in the array (in which case it will
                                            //share a side with the last philosopher in the array

                                        } else if (primeIndex == totalPhil-1 ){


                                                    if ((int_arr_phil[primeIndex-1][1] == 0) && (int_arr_phil[0][1] == 0) && (forks>=2)){

                                                            int_arr_phil[primeIndex][1] = 2;
                                                            int_arr_phil[primeIndex][2] = FULL;

                                                            forks -= 2;

                                                    } else {

                                                            int_arr_phil[primeIndex][1] = 0;
                                                            int_arr_phil[primeIndex][2] -=1;
                                                        }


                                            // default case where the index does not fall on the edges of the array
                                        } else {



                                                    if ((int_arr_phil[primeIndex-1][1] == 0) && (int_arr_phil[primeIndex+1][1] == 0 ) && (forks>=2)){


                                                        int_arr_phil[primeIndex][1] = 2;
                                                        int_arr_phil[primeIndex][2] = FULL;

                                                        forks -=2;

                                                    } else {

                                                        int_arr_phil[primeIndex][1] = 0;
                                                        int_arr_phil[primeIndex][2] -=1;
                                                    }

                                        }



                            System.out.println( primeIndex + " " +   int_arr_phil[primeIndex][0] + " " + int_arr_phil[primeIndex][1] + " " + int_arr_phil[primeIndex][2]);




                            // Use the prime value and maximum number of data items to determine the next index

                            boolean valid = false;

                            int previousIndex = primeIndex;

                            // excecutes until alive philosopher index reached that is different from the previous index
                            while (!valid){

                                primeIndex = (primeIndex + primeValue) % (totalPhil);

                                // checks that the next index is that of an alive philosopher
                               if ((int_arr_phil[primeIndex][1]!= INVALID) && (int_arr_phil[primeIndex][2]!=0) && (primeIndex!= (previousIndex)) && (primeIndex!= previousIndex- primeValue)){

                                   valid = true;
                                }


                            }// end while !valid


                        }

                        break;


                    }//end case default


                }// end switch statement


    }


    // int parameter that represents the index number of the philosopher in the original array
    // returns int value of the state of the philosopher

    public int getState (int phil_num){

        for (int i = 0 ; i < 10; i ++ ){

            if (int_arr_phil[i][0] == phil_num){

                System.out.println( i + " " +  int_arr_phil[i][0] + " " + int_arr_phil[i][1] + " " + int_arr_phil[i][2]);

                phil_state = int_arr_phil[i][2];
                break;

            } else {

                System.out.println("&&&&&&&&&&&&& " + i + " " +  int_arr_phil[i][0] + " " + int_arr_phil[i][1] + " " + int_arr_phil[i][2]);
            }
        }

        return phil_state;
    }


}// end class


