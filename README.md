using System;
using System.Linq;

namespace MyApp
{
    class Program
    {
        static void Main(string[] args)
        {

//____________________________________________________________________________________________________________________

        //Storing ASCII art in an array
        string[] listOfImages;
        listOfImages = new string[] {
        "________________\n | \n |\n |\n |\n |\n |\n |\n |\n================", 
        "_______________\n | \n | \n |    (0_0) \n | \n | \n | \n | \n | \n================",
        "_______________\n | \n | \n |  \\ (0_0) \n |   \\__| \n | \n | \n | \n | \n================",
        "_______________\n | \n | \n |  \\ (0_0) / \n |   \\__|__/ \n | \n | \n | \n | \n================",
        "_______________\n | \n | \n |  \\ (0_0) / \n |   \\__|__/ \n |      | \n |      | \n | \n | \n================",
        "_______________\n | \n | \n |  \\ (0_0) / \n |   \\__|__/ \n |      | \n |      | \n |     / \n |    / \n================",
        "_______________\n | \n | \n |  \\ (*_*) / \n |   \\__|__/ \n |      |      -+ GAME +- \n |      |      -+ OVER +- \n |     / \\ \n |    /   \\ \n================"
        };

//____________________________________________________________________________________________________________________

            //Prints out the game introduction
            Console.WriteLine("Welcome to Hangman, C# edition!");

            //Gets the first letter of the user's name and converts it to uppercase
            Console.WriteLine("P1, enter your name");
            string p1Name = Console.ReadLine();
            char p1firstLetter = (Char.ToUpper(p1Name[0]));

            //Gets the word for Hangman
            Console.WriteLine("Enter word");
            string p1Word = (Console.ReadLine()).ToLower();
            

            //Sets up the the possible guesses
            int numberOfLetters = p1Word.Length;
            string[] arrayOfLetters;
            arrayOfLetters = new string[numberOfLetters];
            
            //Creates the array where each letter of the response is stored
            char[] wordToGuess;
            wordToGuess = new char[numberOfLetters];

            //Creates an array to store correct guesses in
            int[] correctLetters;
            correctLetters = new int[numberOfLetters];
      
            //Puts each Char of the responses into its corresponding array slot
            for(int letters = 0; letters < numberOfLetters; letters++)
            {
                wordToGuess.SetValue(Convert.ToChar(p1Word[letters]), letters); 
            }
            
//____________________________________________________________________________________________________________________

            //Intro for P2
            Console.Clear(); 
            Console.WriteLine("Welcome Player 2! Enter in your name");
            string p2Name = Console.ReadLine();
            char p2FirstLetter = Char.ToUpper(p2Name[0]);

            Console.WriteLine($"The word you have to guess is {Convert.ToString(numberOfLetters)} letters long");
            Console.WriteLine(listOfImages[0]);

            //Sets up the guesses
            for(int guesses = 0; guesses <= 5;)
            {

                //Gets P2's first guess
                Console.WriteLine("Guess a letter in P1's word");
                char guess = Convert.ToChar(Console.ReadLine());
            
//__________________________________________________________________________________________________________________________

                //Checks if guess matches 
                if (Array.IndexOf(wordToGuess, guess) > -1)
                {
                    Console.WriteLine("Congratulations!");
                    Console.WriteLine($"\n {listOfImages[guesses]}");

                    //Loop to manage the guesses
                    Console.WriteLine("\n");
                    for(int starting = 0; starting < numberOfLetters; starting++) 
                    {

                        //Sets all correct guesses into an array
                        if (Array.IndexOf(wordToGuess, guess, starting, (numberOfLetters-starting)) > -1)
                        {
                            correctLetters.SetValue(1, Array.IndexOf(wordToGuess, guess, starting, (numberOfLetters-starting)));

                            //Checks if all the letters have been guessed
                            if(correctLetters.Contains(0) == false)
                            {
                                //Win code
                                Console.WriteLine(listOfImages[guesses]);
                                Console.WriteLine($"{p2Name} wins!!");
                                Console.WriteLine($"The word was +{p1Word}+");
                                return;
                            }

                        }

                    }

                }
 
                //Executes if guess is incorrect    
                else
                {
                    //Print out a message and increments guesses
                    Console.WriteLine("Sorry thats not one of them");
                    guesses++;
                }
    
                //Prints out the correct guesses
                for(int starting = 0; starting < numberOfLetters; starting ++)
                {

                    //Prints correct letters
                    if (correctLetters[starting] == 1)
                    {
                        Console.Write(wordToGuess[starting]);

                    }

                    //Prints blanks
                    else
                    {
                        Console.Write("_");

                    }
                }

                //Prints out the hangman and how many guesses are left
                Console.WriteLine(listOfImages[guesses]);
                Console.WriteLine($"You have {6- guesses} guesses left");

                }

            }
         
    }

}
