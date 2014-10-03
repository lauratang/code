code
====

/* Laura Tang (lt2510)
 * COMS W3134
 * Homework 1
 * Problem 2: Exercise 2.7b
 * Main Class
*/

import java.util.*;

public class Problem2 {
	
    private long startTime, endTime, elapsedTime;
    private int sum;
    private TimeInterval time;
	
    public static void main(String[] args) {
		
	//SET N VALUES HERE
	//note that bigger values of n may
	//cause the code to operate slowly
	int[] n = {1, 2, 4, 8, 16};
	
	//loop that iterates through codes for values of n
	for (int i = 0; i<=n.length-1; i++) {
	    System.out.println("N = " + n[i] + " for code 1"
				+ ": " + one(n[i]));
	    System.out.println("N = " + n[i] + " for code 2"
				+ ": " + two(n[i]));
	    System.out.println("N = " + n[i] + " for code 3"
				+ ": " + three(n[i]));
	    System.out.println("N = " + n[i] + " for code 4"
				+ ": " + four(n[i]));
 	    System.out.println("N = " + n[i] + " for code 5"
				+ ": " + five(n[i]));
	    System.out.println("N = " + n[i] + " for code 6"
				+ ": " + six(n[i]));
	    System.out.println();
	}
    }

    //code in separate methods below	
    public static double one(int n) {
	TimeInterval time = new TimeInterval();
	time.startTiming();
	int sum = 0;
        for( int i = 0; i < n; i++ ) {
            sum = sum + (int) Math.random();
        }
        time.endTiming();
        return (time.getElapsedTime());
    }
	
    public static double two(int n) {
	TimeInterval time = new TimeInterval();
	time.startTiming();
	int sum = 0;
        for( int i = 0; i < n; i++ ) {
            for( int j = 0; j < n; j++ ) {
                sum = sum + (int) Math.random();
            }
        }
        time.endTiming();
        return (time.getElapsedTime());
    }
	
    public static double three(int n) {
	TimeInterval time = new TimeInterval();
	time.startTiming();
	int sum = 0;
        for( int i = 0; i < n; i++ ) {
            for( int j = 0; j < (n * n); j++ ) {
        	sum = sum + (int) Math.random();
            }
        }
        time.endTiming();
        return (time.getElapsedTime());
    }
	
    public static double four(int n) {
	TimeInterval time = new TimeInterval();
	time.startTiming();
	int sum = 0;
        for( int i = 0; i < n; i++ ) {
            for( int j = 0; j < i; j++ ) {
        	sum = sum + (int) Math.random();
            }
        }
        time.endTiming();
        return (time.getElapsedTime());
    }
	
    public static double five(int n) {
	TimeInterval time = new TimeInterval();
	time.startTiming();
	int sum = 0;
        for( int i = 0; i < n; i++ ) {
            for( int j = 0; j < i * i; j++ ) {
        	for( int k = 0; k < j; k++ ) {
        	    sum = sum + (int) Math.random();
        	}
            }
        }
        time.endTiming();
        return (time.getElapsedTime());
    }
	
    public static double six(int n) {
	TimeInterval time = new TimeInterval();
	time.startTiming();
	int sum = 0;
        for( int i = 1; i < n; i++ ) {
            for( int j = 1; j < i * i; j++ ) {
                if ( j % i == 0) {
        	    for( int k = 0; k < j; k++ ) {
        		sum = sum + (int) Math.random();
            	    }
        	}
            }
        }
        time.endTiming();
        return (time.getElapsedTime());
    }
	
}

====

public class TimeInterval {
	
   private long startTime, endTime;
   private long elapsedTime; // Time Interval in milliseconds

   public void startTiming() {
      elapsedTime = 0;
      startTime = System.currentTimeMillis();
   }

   public void endTiming() {
      endTime = System.currentTimeMillis();
      elapsedTime = endTime - startTime;
   }

   public double getElapsedTime() {
      return (double) elapsedTime / 1000.0;
   }

}
