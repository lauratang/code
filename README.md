code
====

public class MontyHallSimulator {

    //declare instance variables
    private int switchWin;
    private int originalWin;
    private int choiceDoor;
    private int shownDoor;

    //constructor accepts integer shownDoor as input
    //initializes the variables
    public MontyHallSimulator() {
    int shownDoor;
    int choiceDoor;
    int switchWin;
    int originalWin;
    }

    //method with algorithm
    public void run() {
        for(int plays = 0; plays < 1000; plays++) {
	    
	    //create array {0,0,0} where 0 is a goat, 1 is car
	    int[] threeDoors = new int[3];
	    //randomly change one of the 0's into a 1, placing a car
	    threeDoors[(int)(Math.random() * (3))] = 1;
	    //contestant chooses a random door
	    choiceDoor = (int)(Math.random() * (3));
	    //pick a random door for host to show
	    shownDoor = (int)(Math.random() * (3));
	    //while the door contains the car or is the contestant's door
	    //choose a random door to be shown again
	    while (threeDoors[shownDoor] == 1 || shownDoor == choiceDoor) {
		shownDoor = (int)(Math.random() * (3));
	    }

	    //deciding which strategy allows for a win
            if (threeDoors[choiceDoor] == 1) {
	        originalWin++;
	    } else {
		switchWin++;
	    }

	}
    }

    //accessor method strategy1
    public int strategy1() {
    return switchWin;
    }

    //accessor method strategy2
    public int strategy2() {
    return originalWin;
    }	

}

====

public class MontyHallTester {

    public static void main (String[]args) {

        //create a new object of MontyHallSimulator
        MontyHallSimulator simulator = new MontyHallSimulator();

        //determine and print the outcome
	simulator.run();
        int strategy1 = simulator.strategy1();
        int strategy2 = simulator.strategy2();
        System.out.println("Wins by switching your door choice: " + strategy1);
	System.out.println("Wins by keeping your door choice: " + strategy2);
    
    }

}
