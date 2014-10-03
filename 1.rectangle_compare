code
====

/* Laura Tang (lt2510)
 * COMS W3134
 * Homework 1
 * Problem 1: Exercise 1.15
 * Main Class. Hardcode Rectangles to be compared here.
*/

import java.util.*;

public class Problem1 {
	
    private Rectangle r1;
    private Rectangle r2;
    private Rectangle r3;
    private Rectangle r4;
    private Rectangle maxArea;
    private Rectangle maxPerimeter;
	
    public static void main(String[] args) {
	//MANIPULATE RECTANGLES HERE
	Rectangle r1 = new Rectangle(4,3);
	Rectangle r2 = new Rectangle(9,9);
	Rectangle r3 = new Rectangle(1,18);
	Rectangle r4 = new Rectangle(2,5);
		
	//place them into an array
	Rectangle[] arr = {r1, r2, r3, r4};
		
	//use findMax method
	Rectangle maxArea = findMax(arr, new CompareArea());
	Rectangle maxPerimeter = findMax(arr, new ComparePerimeter());
			
	//print out results
	System.out.println("Rectangle of Max Area: "
			  + maxArea.getLength() + "x" 
			  + maxArea.getWidth());
	System.out.println("Rectangle of Max Perimeter: "
			  + maxPerimeter.getLength() + "x" 
			  + maxPerimeter.getWidth());
    }
    
    //findMax method
    //takes in Rectangle[] and Comparator as parameters
    public static <Rectangle>
    Rectangle findMax(Rectangle [] arr, Comparator<? super Rectangle> cmp) {
	int maxIndex = 0;
	for (int i = 1; i<arr.length; i++) {
	    if (cmp.compare(arr[i], arr[maxIndex]) > 0) {
		maxIndex = i;
	    }
	}
	return arr[maxIndex];
    }
	
}

====

class Rectangle {
    private int l;
    private int w;
	
    public Rectangle(int l, int w) { 
    //Rectangle constructor with two properties
	this.l = l; //length
	this.w = w; //width
    }
	
    public int getLength() { //method to get length
	return l;
    }

    public int getWidth() { //method to get width
	return w;
    }
	
}

====

import java.util.*;

public class CompareArea implements Comparator<Rectangle> {
	
    //implementation of Comparator for area
	
    public int compare(Rectangle r1, Rectangle r2) {
	int a = (r1.getLength()*r1.getWidth());
	int b = (r2.getLength()*r2.getWidth());
	if (a>b) {
   	    return 1;
	} else return -1;	
    }
	
}

====

import java.util.*;

public class ComparePerimeter implements Comparator<Rectangle> {
	
    //implementation of Comparator for Perimeter
	
    public int compare(Rectangle r1, Rectangle r2) {
	int a = 2*(r1.getLength()+r1.getWidth());
	int b = 2*(r2.getLength()+r2.getWidth());
	if (a>b) {
	    return 1;
	} else return -1;		
    }
	
}


