code
====

public class BullsAndCows {

    public static void main(String[] args){
        Game g = new Game();
        g.play();
    }   
}

====

import java.util.ArrayList;
import java.util.Scanner;

public class Game{
	
    //instance variables
    private Scanner input = new Scanner(System.in);
    private ArrayList<Integer> scoreCount = new ArrayList<Integer>();
    private int turns;
    private int best;
    private int worst;
    private double avg;
    boolean userChoice;
    String guess;

    public Game() {
        //instantiate variables
        turns = 0;
        best = 0;
        worst = 0;
        avg = 0;
        userChoice = true;
        guess = "";
    }

    public void play(){
        System.out.println("Bulls and Cows! Let's play!");
        
        outerloop:
    	while (userChoice == true) {
            Oracle computer = new Oracle();
    	    String solution = computer.run();
    	    //do loop to run plays with the same secret number
    	    do {
    	        System.out.print("Please enter 4 unique digits "
                                + "from 0-9 (####): ");
                guess = input.next();
    		int b = computer.findBulls(guess,solution);
    		int c = computer.findCows(guess,solution);
    		turns++;
    		
    		if (b!=4) {
    		    //report number of bulls & cows for this round
    	            System.out.println(b +" bull(s) and " + c + " cow(s)");
                    //offer user a chance to quit the game
    		    System.out.println("Would you like to "
   		                      + "continue guessing? (yes/no)");
    		    if (input.next().equals("no")) {
    		        userChoice = !userChoice;
    			System.out.println("Thanks for playing!");
    			break outerloop;
    		    }
    		}
    	    } while (computer.findBulls(guess,solution)!=4);
    	
    	    //user finally guesses correctly	
    	    if (computer.findBulls(guess,solution)==4) {
    	        System.out.println("Moo! 4 bulls! You guessed the "
    				  + "secret number!");
		System.out.println("It took you " + turns + " attempts.");
    	        //add result to arraylist of game play results
    		scoreCount.add(turns);
    		//update best and worst scores
                if (best==0 || turns<best) {
    		    best = turns;
    		}	
    		if (worst==0 || turns>worst) {
    		    worst = turns;
    		}
    	        turns = 0;
    	    }
    	
    	    //implement do loop for a newly generated secret number
    	    System.out.println("Would you like to play "
    			      + "another round? (yes/no)");
    	    if (input.next().equals("no")) {
    	        userChoice = !userChoice;
    		System.out.println("Thanks for playing!");
    		break outerloop;
    	    }
    	}
   
    	//calculate avg score
	double sum = 0.0;
	for(int w = 0; w < scoreCount.size(); w++) {
	    sum += scoreCount.get(w);
	}
	avg = (sum / (scoreCount.size()));
	
        //print out results
	System.out.println("End of session. Total stats:");
	System.out.println("You played " + scoreCount.size() + " rounds" );
	System.out.println("Best score: " + best);
	System.out.println("Worst score: " + worst);
	System.out.println("Average score: " + avg);	
    	
    }
}

====

public class Oracle {
    
    //initialize variables
    private int bulls;
    private int cows;

    public Oracle() {
        //instantiate variables
        bulls = 0;
        cows = 0;
    }
    
    public String run() {
        //generate secret number with no repeat digits
        //by using an array
        int[] secretNumber = new int[4];  	
        secretNumber[0] = (int)(Math.random() * 10);
	do {
	    secretNumber[1] = (int)(Math.random() * 10);
	} while (secretNumber[1] == secretNumber[0]);
	do {
	    secretNumber[2] = (int)(Math.random() * 10);
	} while (secretNumber[2] == secretNumber[1] ||
	         secretNumber[2] == secretNumber[0]);
	do {
	    secretNumber[3] = (int)(Math.random() * 10);
	} while (secretNumber[3] == secretNumber[0] ||
		 secretNumber[3] == secretNumber[1] ||
		 secretNumber[3] == secretNumber[2]);

        //initialize the secret number, turn into string
        StringBuilder sb = new StringBuilder(secretNumber.length);
	for (int i : secretNumber) {
	    sb.append(i);
	}
	String solution = sb.toString();
	return solution;
    }
   
    public int findBulls(String guess, String solution) {	
    	//compare each guess number
    	//with corresponding secret number
    	bulls = 0;
    	for (int i=0; i<=3; i++) {
    	    char a = guess.charAt(i);
    	    char b = solution.charAt(i);
    	    if (a==b) {
    	        bulls++;
    	    }	
    	}
    	return bulls;
    }

    public int findCows(String guess, String solution) {		
    	//compare each guess number
    	//with all secret numbers, except corresponding
    	cows = 0;
    	
        //outerloop sets conditions to evaluate user input value
        outerloop:
    	for (int i=0; i<=3; i++) {
    	    //first eliminate accidental repeat cows
    	    //if the user disobeys and enters repeating numbers
    	    if (i==1) {
    	        int k=0;
    		if (guess.charAt(k)==guess.charAt(i)) {
    		    i++;
    		}
    	    }
    	    if (i==2) {
    		int k=1;
    		if (guess.charAt(k)==guess.charAt(i) ||
    		    guess.charAt(k-1)==guess.charAt(i)) {
    		    i++;
    		}	
    	    }
    	    if (i==3) {
    		int k=2;
    		if (guess.charAt(k)==guess.charAt(i) ||
    		    guess.charAt(k-1)==guess.charAt(i) ||
    		    guess.charAt(k-2)==guess.charAt(i)) {
    		    break outerloop; //if the last number is a repeat
    			  //there's no need to continue counting cows
    		    }	
    	    }
    	    char a = guess.charAt(i);
    	
            //compare to secret number
    	    for (int j=0; j<=3; j++) {
                char b = solution.charAt(j);
    		if (a==b) {
    		    cows++;
		    if (guess.charAt(j)==solution.charAt(j)) {
			cows--; //eliminate double counting bulls and cows
		    }
    		}
    	    }	
    	}
    	return cows;
    
    }    
} 
