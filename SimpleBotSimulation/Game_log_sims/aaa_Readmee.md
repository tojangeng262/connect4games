in this folder is the result of my simulation. it have the JSON extention. it was the result of 6000 games play between 4 of my bot. every game contains list of the move that have something like this

    {
    "metadata": {
            "bot1": "bot1name",
            "bot2": "bot2name",
            "game_number": "number of the game that play between bot1 and bot2(int)",
            "ordering": "("normal" or "reversed")",
            "result": "botwinner"
            },
  
    "move_log": [
          {
              "move_number": "number of the move(int)",
              "player": "1 or 2",
              "column": "position of the column that player play",
              "row": "position of the row that player play",
              "timestamp": "timestamp of the move"
          },
  
          ##**...till the game end..**
  
          {
              "move_number": "number of the move(int)",
              "player": "1 or 2",
              "column": "position of the column that player play",
              "row": "position of the row that player play",
              "timestamp": "timestamp of the move"
          }
      ]
    }
