package com.company;

/**
 * Created by 13549lac on 17/01/2019.
 */
import static com.company.ProjConstants.*;

public class Philosophers implements Philosopher {

        // Declare Class Variables

           private int  phil_num = INVALID;

           private int phil_state = INVALID;

           private int totalPhil = INVALID;

        int  int_arr_phil[][] = new int [11][3];




   /*
    public  Philosophers (int index, int state) {

        phil_num = index;
        phil_state = state;

    }
     */


    public int totalPhil (String arr_phil[][], int index){
        boolean invalid = false;

         while (!invalid){
             for (int i=0; i<11;i++){

                 if (arr_phil [i][index] != null) {

                      totalPhil = i;

                 } else {

                     invalid = true;

                     break;
                 }

            }// end for
        } //end while
        return totalPhil;
    }

    public void transferArray (String arr_phil[][], int index){

        for (int i=1; i < 10; i++){

            if (arr_phil[i][index] != null){

                int_arr_phil [i-1][0] = i;
                int_arr_phil [i-1][1] = 0;
                int_arr_phil [i-1][2] = FULL;

            } else {
                int_arr_phil[i-1][0] = INVALID;
                int_arr_phil[i-1][1]= INVALID;
                int_arr_phil[i-1][1]= INVALID;
            }

        }
        
    }









    // set int total number of philosophers (String arr_philosopers [][], int index)
    //boolean null = false;
    // while (null=false){
    // for (int i=0; i<11;i++){
    // if (arr_philosopers [i][index] == null){
    // int totalPhil = i;
    // break;
    // }
    // } end while
    // return totalPhil



    // get fork number {


// int setState ( int philosopherNumb , int state ) {
//  get Randomnumbs
// if philopsopher has two forks
// state-1;
// } else {
// state = FULL )
//
//



}


