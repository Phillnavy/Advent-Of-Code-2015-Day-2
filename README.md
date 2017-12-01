# Advent-Of-Code-2015-Day-2
This is Code in Java for Advent of code 2015 Day 2

import java.io.FileNotFoundException;
import java.util.ArrayList;
import java.util.Scanner;

import parser.InputParser;
public class AOC2015two {



	public static void main(String args[]) throws FileNotFoundException {

		int total = 0; //This is our answer and what it will be saved in
		int ribbon=0; //this is the ribbon exit

		InputParser parse = new InputParser("test_input.txt");
		parse.parseInput();

		ArrayList<String> input = parse.getInput(); 
		//Puts all inputs in an array list.
		ArrayList<int[]> pairs = new ArrayList<int[]>(); 
		//ArrayList<String[]> pairs = new ArrayList<String[]>(); 
		//Array list to separate inputs


		for( int x = 0; x < input.size(); x++) {
			//Goes through array

			int[] snums = new int[3];
			//Temporary place to store each number

			String s = input.get(x);
			//Saves all values to X

			//System.out.println(s); //Always good to test



			for(int q = 0; q < 2; q++) { 
				//Numbers will always only be 2 x's in each place

				int name = s.indexOf("x");
				//Gets location of "x"

				snums[q] = Integer.parseInt(s.substring(0,name));
				//Makes array have no "x"

				s = s.substring(name+1); 
			}


			snums[2] = Integer.parseInt(s);
			pairs.add(snums);   
			//Array that has numbers
		}

		////////////////////////////We will use these later/////////
		int hw = 0;
		int lh = 0;
		int l;
		int w;
		int h;
		//////////////////////////////////////////////////////////////////////////////////////////////////////////////


		for(int i = 0; i < pairs.size();  i++ ) {  //Loop that prints all numbers without the "x"


			lw = (pairs.get(i)[0] * pairs.get(i)[1]);
			hw = (pairs.get(i)[2] * pairs.get(i)[1]);
			lh = (pairs.get(i)[0] * pairs.get(i)[2]);
			//These multiply l*w, h*w, and l*h for us

			l=pairs.get(i)[0];
			w=pairs.get(i)[1];
			h=pairs.get(i)[2];
			//These tell us what our length, width, and height values are in integers.


//////////////////////////////////////////////////////////////////////////////////////////////////
			if(l<=w && l<=h) {
				if(w<=h) {
					ribbon += l + l + w + w;
					System.out.println("Ribon total: " + ribbon);
				}
				else //height is smaller
				{
					ribbon += l + l + h + h;
					System.out.println("Ribon total: " + ribbon);
				}
			}

			else if(w<=l && w<=h) {
				if(l<=h) {
					ribbon += w + w + l + l;
					System.out.println("Ribon total:" + ribbon);
				}
				else //height is smaller
				{
					ribbon += w + w + h + h;
					System.out.println("Ribon total: " + ribbon);
				}
			}
			else {
				if(w<=l) {
					ribbon += h + h + w + w;
					System.out.println("Ribon total: " + ribbon );
				}
				else //length is smaller
				{
					ribbon += h + h + l + l;
					System.out.println("Ribon total: " + ribbon);
				}
			}
			
			//All of these statements work for the ribbon.
			//They tell the smallest side we need to use for the length around.
/////////////////////////////////////////////////////////////////////////////////////////


			total += lw*2;
			total += hw*2;
			total += lh*2;
			//Used for the surface area formula
			
///////////////////////////////////////////////////////////////////////////////////////////////////////////////
			if(lw <= hw && lw <= lh) {
				total += lw;
				System.out.println("This is the total surface area so far " + total);

			}

			else if(hw <= lw && hw <= lh){
				total += hw;
				System.out.println("This is the total surface area so far" + total);

			}

			else {				
				total += lh;
				System.out.println("This is the total surface area so far" + total);

			}
			
			//These statements tell us what the smallest side 
			//for us to add back to the total is
////////////////////////////////////////////////////////////////////////////////
			ribbon += l*w*h; //Ribbon volume 

			
			System.out.println(("The inputs were: " + pairs.get(i)[0] + "x" + pairs.get(i)[1] + "x" + pairs.get(i)[2]));
			//This tells us our inputs we used
			
			System.out.println("----------------------------------------------------------------------------------");
			//Makes your console look prettier
		}
		
		System.out.println("The total surface area is: " + total);
		System.out.println("The total ribbon is: " + ribbon);
		//Our final outputs and what they are.
	}
}
