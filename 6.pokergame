code
====

public class Card implements Comparable<Card>{
	
    private int suit; // use integers 1-4 to encode the suit
    private int value; // use integers 1-13 to encode the value
	
    public Card(int s, int v){
        suit = s;
	value = v;
    }

    public int compareTo(Card c){
	int answer = this.value - c.value;
	if (answer == 0)
	    answer = this.suit - c.suit;
	return answer;
    }
	
    public String reportValue(){
        if (value==1)
	    return "Ace of ";
	else if (1<value && value<11)
	    return (value + " of ");
	else if (value==11)
	    return "Jack of ";
	else if (value==12)
	    return "Queen of ";
	else return "King of ";	
    }
	
    public String reportSuit(){
	if (suit==1)
	    return "clubs";
	else if (suit==2)
	    return "diamonds";
	else if (suit==3)
	    return "hearts";
	else return "spades";
    }
	
    public String toString(){
	String theSuit = this.reportSuit();
	String theValue = this.reportValue();
	return (theValue + theSuit);
    }
	
    public int getSuit(){
	return this.suit;
    }
	
    public int getValue(){
	return this.value;
    }

}

====

public class Deck {

    private Card[] theDeck;
    private int top; // the index of the top of the deck
	
    public Deck(){
	//creates a new deck
	theDeck = new Card[52];
	int counter = 0;
	for (int i=1; i<5; i++) {
	    for (int j=1; j<14; j++) {
	        Card addedCard = new Card(i,j);
	        theDeck[counter] = addedCard;
	        counter++;
	    }
	}
	top = -1;
    }
	
    public void shuffle(){
	//interchanges two random cards 100 times
	for (int i=0; i<100; i++) {
	    int randomNum = (int)(Math.random()*51);
	    int randomNum2 = (int)(Math.random()*51);
	    while (randomNum2 == randomNum) {
		randomNum2 = (int)(Math.random()*51);
	    }
	    Card temp = theDeck[randomNum];
	    theDeck[randomNum] = theDeck[randomNum2];
	    theDeck[randomNum2] = temp;
	}
    }
	
    public Card deal(){
        // deal the top card in the deck
	top++;
	if (top<52)
	    return theDeck[top];
	else return null;
    }

}

====

import java.util.*;

public class Game {
	
    private static Player p;
    private Deck cards;
    private ArrayList<Card> hand;
    private boolean testMode;
    private int rejectCounter;
    private int tokens;
    private Scanner input;
    private boolean onePair;
    private boolean twoPair;
    private boolean threeKind;
    private boolean straight;
    private boolean flush;
    private boolean fullHouse;
    private boolean fourKind;
    private boolean straightFlush;
    private boolean royal;
    private ArrayList<Integer> suit;
    private ArrayList<Integer> value;
    private ArrayList<Card> inputHand;
	
    public Game(String[] testHand){
	
	//turn testMode boolean on
	testMode ^= true;
        suit = new ArrayList<Integer>();
        value = new ArrayList<Integer>();
	inputHand = new ArrayList<Card>();
	
	//fill suit ArrayList	
	for (int i=0; i<5; i++){
	    char s = testHand[i].charAt(0);
	    if (s == 'c')
	        suit.add(1);
	    if (s == 'd')
		suit.add(2);
	    if (s == 'h')
	        suit.add(3);
	    if (s == 's')
		suit.add(4);
	}

	//fill value ArrayList	
	for (int i=0; i<5; i++) {
    	    if (testHand[i].length() == 2) {
		int v = (int) testHand[i].charAt(1);
		value.add(v);
	    }
	    if (testHand[i].length() == 3) {
		int v = (int) testHand[i].charAt(2);
		v += 10;
		value.add(v);
	    }		
	}
		
	//merge suit and value ArrayLists
	//to make an Array of Cards, inputHand
	p = new Player();
	for (int i=0; i<5; i++) {
	    Card addedCard = new Card(suit.get(i),value.get(i));
	    inputHand.add(addedCard);
	    p.addCard(inputHand.get(i));
	}

    }
	
    public Game(){
	p = new Player();
    }

    public void play(){
	//this constructor is to actually play a normal game
	//ignore if in testMode
	if (testMode == false) {

	System.out.println("");
	System.out.println("Welcome to VideoPoker!");
	System.out.println("Here are 50 tokens. "
			   +"You insert 1 token to play.");
	System.out.println("Type 0 when you want to quit.");
	tokens = 49;
	rejectCounter = 0;
	input = new Scanner(System.in);
	 	
	do {
	    //make and shuffle deck
	    cards = new Deck();
	    cards.shuffle();
	    
	    //deal 5 cards in normal game mode
	    if (testMode == false) {
	        for (int i=0; i<5; i++) {
	            p.addCard(cards.deal());
	        }	
	    }

	    //show hand to user
	    System.out.println("");
	    System.out.println("Your hand:");
  	    System.out.println("[" + revealHand(hand) + "]");
  	    
	    //reject card option
	    System.out.println("Please enter a number.");
     	    System.out.println("Would you like to reject "
	    + "none(1), some(2), or all(3) of your cards?");
	    
	    int request = input.nextInt();		
	    if (request == 3) { //all clear and re-deal
		p.clearHand();
		for (int i=0; i<5; i++) {
		    p.addCard(cards.deal());
		}
		System.out.println("");
                System.out.println("Your new hand: ");
                System.out.println("[" + revealHand(hand) + "]");
                System.out.println("");
	    }			
	    else if (request == 2) { //some removal re-deal
	        System.out.println("Enter cards you want to "
		+ "reject WITHOUT spaces in ascending positional order.");
		System.out.println("(1 for first card, etc).");
		//further user instruction for input format
		//only given the first time user rejects 'some' cards
		if (rejectCounter == 0){
		    System.out.println("(Number the cards "
		    + "1, 2, 3, 4, and 5 from left to right). ");
		    System.out.println("(ex: type '125' to throw"
		    + "out your first, second and fifth cards).");
		}
		int request2 = input.nextInt();
		while (request2 > 0){
		    int digit = request2 % 10;
		    request2 = request2 / 10;
		    p.removeCard(digit-1);
		    p.addCard(cards.deal());
		}
		rejectCounter++;
		System.out.println("");
                System.out.println("Your new hand: ");
                System.out.println("[" + revealHand(hand) + "]");
                System.out.println("");
	    }
	    else if (request == 0) { //player wants to quit
		System.out.println("");
		System.out.println("Thanks for playing VideoPoker!");
		System.out.println("Number of Tokens: " + tokens);
		System.exit(0);
 	    }
	
   	    //evaluate hand and give results
   	    System.out.println("Your result: " + checkHand(hand));
	    System.out.println("Current number of tokens: " + tokens);
	    System.out.println("Press 0 to quit "
	    + "or 1 to insert another token and continue.");
	    int in = input.nextInt();
	    if (in == 0){
	        System.out.println("");
		System.out.println("Thanks for playing VideoPoker!");
	        System.out.println("Number of Tokens: " + tokens);
		System.exit(0);
	    } else{
		p.clearHand();
		tokens--;
	    }
	} while (tokens != -1); //end of do-while loop
				//end when all tokens used
		
	if (tokens == -1){
	    System.out.println("");
	    System.out.println("You ran out of tokens :(");
	    System.out.println("Thanks for playing VideoPoker!");
            System.exit(0);
	}
	
	//if in testMode skip regular game procedures
	} else System.out.println("Your results: " + checkHand(hand));
    }
	
    public String checkHand(ArrayList<Card> hand){
        //order cards in ascending order
        p.sortHand();
        //run hand checks
	//account for duplicate hands
        checkStraightandFlush(hand);
        checkDuplicates(hand);
	
        //print results!
        if (onePair == true){
	    tokens++;
	    onePair ^= true;
	    return "one pair, 1 token";
        } else if (twoPair == true){
	    tokens += 2;
	    twoPair ^= true;
	    return "two pairs, 2 tokens";
        } else if (threeKind == true){
	    tokens += 3;
	    threeKind ^= true;
	    return "three of a kind, 3 tokens";
	} else if (straight == true){
	    tokens += 4;
	    straight ^= true;
	    return "straight, 4 tokens";
	} else if (flush == true){
	    tokens += 5;
	    flush ^= true;
	    return "flush, 5 tokens";
	} else if (fullHouse == true){
	    tokens += 6;
	    fullHouse ^= true;
	    return "full house, 6 tokens";
	} else if (fourKind == true){
	    tokens += 25;
	    fourKind ^= true;
	    return "four of a kind, 25 tokens";
        } else if (straightFlush == true){
	    tokens += 50;
	    straightFlush ^= true;
	    return "straight flush, 50 tokens";
        } else if (royal == true){
	    tokens += 250;
	    royal ^= true;
	    return "royal flush, 250 tokens";
        } else {
	    return "high card";
        }
    }
	
    public static String revealHand(ArrayList<Card> hand) {
        hand = p.getHand();
        ArrayList<String> s = new ArrayList<String>();
        for (int i=0; i<5; i++) {
	    p.getCard(i).reportValue();
	    p.getCard(i).reportSuit();
	    s.add(p.getCard(i).toString());
	}
	String print = "";
	for (int i=0; i<s.size(); i++){
	if (i==s.size()-1){
	    print += s.get(i);
	} else{
	    print += s.get(i)+", ";
	}
    }
    return print;
    }
	
    public void checkDuplicates(ArrayList<Card> hand){
        //check for any repeated cards
        //one or two pairs, three or four of a kind and full house
        int dupCounter = 0;
        for (int i=0; i<4; i++){
	    if (p.getCard(i).getValue() == p.getCard(i+1).getValue()){
	        dupCounter++;
	    }
        }
		
        if (dupCounter == 1 && flush == false){ //one pair only
  	    onePair ^= true;
        }
        if (dupCounter == 2 && flush == false){ //two pair, three kind
	    int threeCounter = 0;
	    for (int i=0; i<3; i++){
	        if (p.getCard(i).getValue() == p.getCard(i+2).getValue()){
	            threeCounter++;
	        }
	    }
	    if (threeCounter == 1){
	       threeKind ^= true;
	    } else if (threeCounter == 0){ 
	       twoPair ^= true;
	    }
        }		
        if (dupCounter == 3){ //full house or four of a kind
            int fourCounter = 0;
            for (int i=0; i<2; i++){
	        if (p.getCard(i).getValue() == p.getCard(i+3).getValue()){
	            fourCounter++;
	        }
	    }
	    if (fourCounter == 1){
                fourKind ^= true;
		if (flush == true) {
		    flush ^= true;
		}
            } else{
	        fullHouse ^= true;
	        if (flush == true) {
                    flush ^= true;
                }
	    }
	}
    }
	
    public void checkStraightandFlush(ArrayList<Card> hand){
	//find a flush
        int counter = 0;
        for (int i=0; i<4; i++){
            if (p.getCard(i).getSuit() == p.getCard(i+1).getSuit()){
    	        counter++;
	    }
	}
	if (counter == 4){
	    flush ^= true;
	}
	    
	//find a straight
	//accounts for 1, 2, 3, 4, 5
	//and 1, 10, 11, 12, 13 possibilities 
	int straightCounter = 0;
	for (int i=0; i<4; i++){
	    if (p.getCard(i).getValue() == (p.getCard(i+1).getValue())-1){
	        straightCounter++;
	    }
	}
	if (straightCounter == 4 || ((p.getCard(0).getValue()+12 ==
				    p.getCard(4).getValue()) &&
				    (p.getCard(3).getValue()+1 ==
                                    p.getCard(4).getValue()) &&
				    (p.getCard(2).getValue()+1 ==
                                    p.getCard(3).getValue()) &&
				    (straightCounter == 3))){
	    straight ^= true;
	}

	//find straight flush
	if (flush == true && straight != false) {
            straightFlush ^= true;
	    flush ^= true;
	    straight ^= true;
        }
		
	//find royal flush
	if ((straightFlush == true) && 
	    (p.getCard(0).getValue()+12 == p.getCard(4).getValue())) {
	    royal ^= true;
	    straightFlush ^= true;
	}
    }

}

====

import java.util.*;

public class Player {

    private ArrayList<Card> hand; // the player's cards
		
    public Player(){		
	hand = new ArrayList<Card>();
    }

    public ArrayList<Card> getHand(){
	return hand;
    }
	
    public void addCard(Card c){
        hand.add(c);
    }
	
    public void clearHand(){
        hand.clear();
    }
	
    public void removeCard(int i){
        hand.remove(i);		
    }
	
    public Card getCard(int i){
	return (hand.get(i));
    }
	
    public ArrayList<Card> sortHand(){
        //order cards in ascending order
	//by value and suit
	//using bubble sort
	for (int i=0; i<5; i++){
	    for (int j=4; j>i; j--){
		if (getCard(j).compareTo(getCard(j-1)) < 0){
		    Collections.swap(hand, j, j-1);
		}
	    }
	}
	return hand;
    }

}

====

public class PokerTest {
	//this class must remain unchanged
	public static void main(String[] args){
		if (args.length<1){
			Game g = new Game();
			g.play();
		}
		else{
			Game g = new Game(args);
			g.play();
		}
	}

}
