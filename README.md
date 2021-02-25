# BlackJack
V1 of my blackjack game
#include <stdio.h>
#include <time.h>			//needed to generate different random cards

char cards[] = { '2', '3' , '4', '5' , '6', '7', '8', '9', 'J', 'Q', 'K', 'A' }; //initializing the possible "cards"

int value(char c) 
{
	int v;					//assigning cards a local variable to assign them a value and saving that value
	switch (c)
	{
	case '2': v = 2;
		break;
	case '3': v = 3;
		break;
	case '4': v = 4;
		break;
	case '5': v = 5;
		break;
	case '6': v = 6;
		break;
	case '7': v = 7;
		break;
	case '8': v = 8;
		break;
	case '9': v = 9;
		break;
	case 'J': v = 10;
		break;
	case 'Q': v = 10;
		break;
	case 'K': v = 10;
		break;
	case 'A': v = 11;
		break;
	}
	return v;
}


char draw_card()				//intitializes the draw card function
{

	int n = (rand() + 0) % 12;	//this is to limit to the 12 possibilities

	return cards[n];
}

int dealer_count = 0;			//for storing dealer and player count
int player_count = 0;

								//main funtion.
int main()
{
	srand(time(0));				//to stop rand function from generating same values

	char D, P;					//to store cards for dealer(D) and player(P)

	printf("\n-------------------------------------------------------------------------------------------------------\n");
	printf("                                WELCOME TO ISAAC'S BLACKJACK!                                         ");
	printf("\nTHE GOAL IS TO GET AS CLOSE TO 21 AS POSSIBLE WITHOUT GOING OVER. IF YOU GO OVER 21 YOU LOSE!\n");
	printf("\n                   ------------A=11, K=10, Q=10, J=10--------------\n");
	printf("-------------------------------------------------------------------------------------------------------\n");

	printf("\n------------ROUND 1--------------\n");

	D = draw_card();							//draws dealer card
	dealer_count += value(D);					//adds card to dealer count.
	printf("Dealer Card: %c", D);				//prints dealer card.

	P = draw_card();							//draws player card
	player_count += value(P);					//adds card to player count
	printf("\nPlayer card: %c", P);				//prints player card

	printf("\n\n------------ROUND 2--------------");

	D = draw_card();							//draws dealer card
	dealer_count += value(D);					//adds card to dealer count.
	printf("\nDealer Card: hidden");			//prints "hidden"

	P = draw_card();							//draws player card
	player_count += value(P);					//adds card to player count
	printf("\nPlayer card: %c", P);				//prints player card

												//if a player or dealer gets 21 then prints BLACKJACK!!

	if ((player_count == 21 && dealer_count != 21) || (player_count != 21 && dealer_count == 21))
		printf("\n\nBLACKJACK!!");
	else//else
	{
		char decision;												//decision to Hit or stay
		printf("\n\nWould you like to Hit or Stay (H/S)? ");
		scanf_s("%c", &decision);

		while (decision == 'H' && player_count <= 21)	//if decision is H and player count is lessthan or equal to 21 then the block code in while is executed
		{
			P = draw_card();										//draws card for player.
			player_count += value(P);
			printf("\nPlayer card: %c", P);

			printf("\n\nHit or Stay (H/S)? ");						//prompts player again
			scanf_s(" %c", &decision);
		}
	}
	
	printf("\nThe hidden dealer card was: %c", D);					//prints hidden card and total of both dealer and player
	printf("\nDealer sum = %d", dealer_count);
	printf("\nPlayer sum = %d", player_count);

	if ((player_count < dealer_count) && dealer_count <= 21)		//if else to decide if player or dealer won based on score and if one or the other busted
		printf("\nYou Lose!\n");
	else if (player_count > dealer_count && player_count <= 21)
		printf("\nYou Won!\n");
	else if (player_count == dealer_count)
		printf("\nIt's a draw!\n");
	else if (player_count <= 21)
		printf("\nYou Won!\n");
	else if (dealer_count <= 21)
		printf("\nYou Lose!\n");
	else printf("\nIt's a draw\n");

	return 0;														//ends code
}
