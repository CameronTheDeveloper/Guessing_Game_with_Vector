# Guessing_Game_with_Vector
This Program allows user to guess a number between 0-250. User gets unlimited guesses until they guess the right number. A text file saves the lowest number of guesses to guess the right number (Best Score).

    #include <iostream>
    #include <string>
    #include <cstdlib> 	    
    #include <ctime>
    #include <vector>
    #include <fstream>

    using std::cout;
    using std::string;
    using std::endl;
    using std::cin;
    using std::getline;
    using std::vector;
    using std::ifstream;


    //Saves Best Score
    void save_score(int count)
    {
	ifstream infilevar("bestScore.txt");

	if(!infilevar.is_open())	//If input file isn't open
	{
	    cout << "Unable to read file\n";
	}

	int best_score;
	infilevar >> best_score;

	std::ofstream output("bestScore.txt");	
	if (count < best_score)
	{
	    output << "The best score is: " << count;
	}
	else
	{
	    output << "The best score is: " << best_score;
	}
    }


    void print_vector(vector<int> vector)		//Function to count guesses
    {
	cout << "Your guesses were: ";
	for (int i = 0; i < vector.size(); i++)
	{
	    cout << vector[i] << ",  ";
	}
	cout << endl;
    }

    void play_game()
    {
	int guess;			//User guesses number
	vector <int> guesses;	   	//Counts/stores guesses

	int count = 0;			//count counts how many guesses
	int random = rand() % 251;		

	cout << "You chose to play!\n";
	cout << "Guess a number: ";

	while(true)		//Indefinite loop (Ends manually)
	{
	    cin >> guess;		//cins for "Guess a number"
	    count++;	//Counts every guess
	    guesses.push_back(guess);		//Saves each guessed number

	    if (guess == random)
	    {
       		cout << "You guessed it correctly!\n";
		break;	//Ends while loop
	    }
	    else if (guess < random)
	    {
		cout << "Guess is too low! Guess again: ";
	    }
	    else
	    {
		cout << "Guess is too high! Guess again: ";
	    }
	}

	save_score(count);

	print_vector(guesses);	
    }



    int main()
    {
	//Menu to select games
	cout << "MENU OPTIONS:\n------------------------\n";
	cout << "0: Exit" << endl << "1: Play Game\n";

	int choice;
	srand(time(NULL));	//Seeds random number. Only needs to be done once

	//do while contains menu and switch statement
	do
	{
	    cout << "\nMENU OPTIONS:\n------------------------\n";
	    cout << "0: Quit" << endl << "1: Play Game\n";
	    cout << "\nENTER HERE: ";

	    cin >> choice;	//Gets user menu choice



	    switch(choice)
	    {
		case 0:
		    cout << "Goodbye! Thanks for playing!\n";
		    return 0;
		case 1:
		    play_game();
		    break;

	    }
	}
	while (choice != 0);
    }
