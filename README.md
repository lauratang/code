code
====

/* Laura Tang (lt2510)
 * COMS W3134
 * Homework 1
 * Problem 3: Binary Recursion
 * Problem3 Class
*/

import java.io.*;
import java.util.*;

public class Problem3 {
	
    public static void main(String[] args) throws IOException,
    FileNotFoundException, InputMismatchException {

	try {	
	    Problem3Tester test = new Problem3Tester("array.txt");
	    System.out.println("Press .5 anytime to quit");

	    boolean again = true;
	    while (again) {

		System.out.println("Please enter the search key:");
	        Scanner scan = new Scanner(System.in);
		double choice = scan.nextDouble();
		if (choice == .5) {
		    again = false;
		    break;
		}
		int userChoice = (int) choice; 
			    
		//recursive search
		Problem3BinSearch bin = new Problem3BinSearch();
		int ans = bin.binarySearch(test.a(), userChoice);
		if (ans == -1) {
		    System.out.println(userChoice + " is not found");
		} else {
		    System.out.println(userChoice + " is found at" 
					+ " index " + ans);
		}
	    
	    }
		    
	} catch (FileNotFoundException e) {
            System.out.println("Please check to see if the "
                    + "array text file exists");
            return;
	} catch (InputMismatchException e) {
	    System.out.println("Please enter the correct input");
	} catch (NoSuchElementException e) {
	    System.out.println("Please enter the correct input");
	}
    }
	
}

====

import java.io.*;
import java.util.*;

public class Problem3Tester {
	
    private File inFile;
    private Scanner input;
    private String fileName;
    private List<Integer> numArray;
	
    //constructor that takes the name of the dictionary file 
    //as the only parameter
    public Problem3Tester(String fileName) throws IOException {
        inFile = new File(fileName);
        input = new Scanner(inFile);
        numArray = new ArrayList<Integer>();
	
	//puts dictionary words from file into ArrayList
	while(input.hasNext()) {
	    int n = Integer.parseInt(input.next());
	    numArray.add(n);
	}
    }
    
    public int[] a() {
    	int[] a = new int[numArray.size()];
    	for (int i = 0; i < a.length; i++) {
    	    a[i] = numArray.get(i);
    	}
    	return a;
    }
    
}

====

public class Problem3BinSearch {
	
    //binary search for number
    //assuming sorted list
	
    //first search
    public int binarySearch(int[] a, int k) { 
	return binarySearch(a, k, 0, a.length - 1);
	//forward to recursive search below
    }
	  
    public int binarySearch(int[ ] a, int k, int low, int high) {
	if (low > high) { //we searched all of the list
	    return -1; 
	}
	int mid = (low + high)/2;
	if (k == a[mid]) {
	    return mid; //the middle is the number
	} else if (k > a[mid]) { //in the upper half
	    return binarySearch(a, k, mid+1, high);
	} else // last possibility: k < a[mid]
	    return binarySearch(a, k, low, mid-1);
    }
	
}
