# connect4games
i try to analyze how to be unbeatable in 4 connect games. i play it with my friend and it feels good if you can always win everytime right?

#Games_simulation
i using python to simulated the games many times. the code is on the connect4sims and the result is connect4_games10juta.csv

Here's my first approach for the data

First Question, From random simulation, is it player 1 and player 2 have a same chance to win the game?
![image](https://github.com/user-attachments/assets/d2723aa0-1003-4d55-b669-13e210a9f5d3)


The simulation of random game show that there are no huge difference in win rate of the player.

Second Question, Player one is the first player to move. is there an advantages that can draw from it?
![image](https://github.com/user-attachments/assets/7a275207-7f39-4e23-9489-5105e5da736b)


It look like that the Win rate of player one (which in this case the player that move first) falls higher toward the centre of the board. D tile have the best percentage of WR that hold by player one (55,06%). So, the answer that we can learn is as player one, we should always play D square
