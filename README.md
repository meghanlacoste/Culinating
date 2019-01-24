package com.company;

/**
 * Created by 13549lac on 17/01/2019.
 */
import java.awt.*;

import static com.company.ProjConstants.*;

public class Philosophers implements Philosopher {

    // Declare Class Variables


    //private static int PRIMEVALUE = 5;

    private int phil_num = INVALID;

    private int phil_state = INVALID;

    private int totalPhil = 0;

    int int_arr_phil[][] = new int[11][3];

    int nextPrime = 2;



   /*
    public  Philosophers (int index, int state) {

        phil_num = index;
        phil_state = state;

    }
     */


    public int totalPhil(String arr_phil[][], int index) {
        boolean invalid = false;
        totalPhil = -1;

        while (!invalid) {
            for (int i = 0; i < 11; i++) {

                if (arr_phil[i][index] != null) {

                    totalPhil +=1;

                } else {

                    invalid = true;
                    break;
                }

            }// end for
        } //end while
        return totalPhil;
    }

    public void transferArray(String arr_phil[][], int index) {

        for (int i = 1; i < 10; i++) {

            if (arr_phil[i][index] != null) {

                int_arr_phil[i - 1][0] = i;
                int_arr_phil[i - 1][1] = 0;
                int_arr_phil[i - 1][2] = FULL;

            } else {
                int_arr_phil[i - 1][0] = INVALID;
                int_arr_phil[i - 1][1] = INVALID;
                int_arr_phil[i - 1][2] = INVALID;
            }

            System.out.println( i-1 + " " + i + " " +  int_arr_phil[i - 1][1] + " " + int_arr_phil[i - 1][2]);

        }


    }


    public int findNextPrime(int input){
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





    public void setState(int firstPhil , int PRIMEVALUE) {


        int_arr_phil[firstPhil-1][1] = 2;


        int forks = totalPhil;


        int primeIndex = firstPhil-1;

        for (int i = 0; i < totalPhil; i++){

            // Use the prime value and maximum number of data items to determine the next index
           // primeIndex = (PRIMEVALUE * i) % (totalPhil-1);
            System.out.println("********  " + int_arr_phil[primeIndex][0] );

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
                // share a side with the last philosopher in the array

            } else if (primeIndex == totalPhil-1 ){

                if ((int_arr_phil[primeIndex-1][1] == 0) && (int_arr_phil[0][1] == 0) && (forks>=2)){

                    int_arr_phil[primeIndex][1] = 2;
                    int_arr_phil[primeIndex][2] = FULL;
                    forks -= 2;

                } else {

                    int_arr_phil[primeIndex][1] = 0;
                    int_arr_phil[primeIndex][2] -=1;
                }

            } else {

                // default case where the index falls

                if ((int_arr_phil[primeIndex-1][1] == 0) && (int_arr_phil[primeIndex+1][1] == 0 && (forks>=2))){

                    int_arr_phil[primeIndex][1] = 2;
                    int_arr_phil[primeIndex][2] = FULL;

                    forks -=2;

                } else {

                    int_arr_phil[primeIndex][1] = 0;
                    int_arr_phil[primeIndex][2] -=1;
                }

            }

            // System.out.println (" i " + i + "primeIndex" +  primeIndex + " arr")
            System.out.println( primeIndex + " " +   int_arr_phil[primeIndex][0] + " " + int_arr_phil[primeIndex][1] + " " + int_arr_phil[primeIndex][2]);

            // Use the prime value and maximum number of data items to determine the next index
           // int sqrt = (int) Math.sqrt(totalPhil);
            primeIndex = (primeIndex + PRIMEVALUE) % (totalPhil);
           // System.out.println("&&&&&&&&&&&&&&&& " + primeIndex);

        }



    }




    public int getState (int phil_num){

        phil_state = int_arr_phil[phil_num - 1][2];

        return phil_state;
    }


}// end class


