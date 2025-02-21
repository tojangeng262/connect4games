# connect4games
i try to analyze how to be unbeatable in 4 connect games. i play it with my friend and it feels good if you can always win everytime right?

#Games_simulation
i using python to simulated the games many times. the code is on the connect4sims and the result is connect4_games10juta.csv

Here's my first approach for the data

First Question, From random simulation, is it player 1 and player 2 have a same chance to win the game?
![image](https://github.com/user-attachments/assets/e2082dc1-ae90-48ae-9dd8-f2b7bd893dfe)



The simulation of random game show that there are no huge difference in win rate of the player.

Second Question, Player one is the first player to move. is there an advantages that can draw from it?
![image](https://github.com/user-attachments/assets/873f35c6-58f5-4375-96de-5660aa3af1d0)





It look like that the Win rate of player one (which in this case the player that move first) falls higher toward the centre of the board. D tile have the best percentage of WR that hold by player one (55,06%). So, the answer that we first learn is as player one, we should always play D tiles
