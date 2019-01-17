package com.company;
import static com.company.ProjConstants.*;

public class ProjConstants {

    // ---------*---------*---------*---------*---------*
    // Integer Constants
    public static final int FULL = 3;
    public static final int HUNGRY = 2;
    public static final int STARVING = 1;
    public static final int DEAD = 0;



    // PRIVATE //

    // ---------*---------*---------*---------*---------*---------*---------*---------*
    // The caller references the constants using ProjConstants.MAXDATA,
    // and so on. So the caller should be prevented from constructing objects of
    // this class.
    // --> By declaring this private constructor for the class we accomplish this. <--
    //
    private ProjConstants() {
        //this prevents even the native class from calling this constructor as well
        throw new AssertionError();
    }
}

