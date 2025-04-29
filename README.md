# DS5100-FinalProject

# Monte Carlo Simulator

** Author: ** Molly Shand
** Project: ** Monte Carlo Simulator

## Synopsis
This project implements a Monte Carlo simulator using three main classes:
'Die'
'Game'
'Analyzer'
It allows users to simulate dice games and analyze the outcomes.

### Installation
To install the package:
```bash
pip install -e
```

### Demo
from montecarlo.montecarlo import Die, Game, Analyzer
import numpy as np

Step 1: Create your dice
```
faces = np.array([1, 2, 3, 4, 5, 6])
die1 = Die(faces)
die2 = Die(faces)
die3 = Die(faces)
```
Step 2: Play your game!
```
game = Game([die1, die2, die3])
game.play(100)
results = game.show('wide')
```

Step 3: Analyze your game
```
analyzer = Analyzer(game)
jackpot)count = analyzer.jackpot()
face_counts = analyzer.face_counts_per_roll()
combos = analyzer.combo_count()
perms = analyzer.permutation_count()
```

### API Description

Class Die: A die with n faces, each with a weight

  Attributes:
  - _df (DataFrame): Internal dataframe storing faces and weights
  Methods:
  
  - __init__: Initializes the die with a NumPy array of faces.
    
        Arguments:
            faces (np.ndarray): An array of unique face values (Can be numeric or string).
    
        Raises: 
            TypeError: If input is not a NumPy array.
            ValueError: If array elements are not unique.
  - change_weight(face, weight): Changes the weight of a specific face.
    
        Arguments:
            face: A face value in the die.
            weight: A numeric value.
    
        Raises:
            IndexError: If the face is not in the die.
            Type Error: If the weight is not numeric.
  - roll(n_rolls = 1): Rolls the die n times using the current weights.
    
        Arguments:
            n_rolls (int): Number of times to roll (default = 1).
        
        Returns:
            list: List of outcomes.
  - show(): Shows current faces and weights of the die.
    
        Returns:
            DataFrame: copy of internal state.

Class Game: A game consists of rolling one or more die objects.
  
  Attributes: 
    _dice (list): List of die objects.
    _results (DataFrame): Data frame storing results of the most recent play.

    Methods:
    - __init__ : Initializes a game with a list of die objects.
        
        Arguments:
            dice (list): list of die objects.
        
        Raises:
            TypeError: If elements in the list are not die objects.
    - play(n_rolls: int): Rolls all dice given a number of times and save the results.
        
        Arguments:
            n_rolls (int): Number of times to roll all dice. 
    - show(self, form = 'wide'): Returns the results of the most recent play.
        
        Arguments:
            form (str): 'wide' (default) or 'narrow' format.

Class Analyzer: An analyzer object takes the results of a single game and computes various descriptive statistical properties about it.
    
    Attributes:
        _game (Game): The game object to analyze.
        _face_counts_per_roll (DataFrame): Data frame of face counts per roll.

    Methods:
    - __init__(self, game): Initializes analyzer with a Game object.
        
        Arguments:
            game (Game): A game object that has been played
            
        Raises: 
            ValueError: If the provided object is not an instance of game.
    - jackpot(): Counts how many rolls had all dice showing the same face.
        
        Returns:
            int: Number of jackpots.
    - face_counts_per_roll(): Counts how many times each face appeared in each roll.
        
        Returns:
            DataFrame: Rolls are row numbers, columns are the face values, and the cells are             counts.
    - combo_count(): Computes counts of unique face combinations (order-independent).
        
        Returns:
            DataFrame: MultiIndex of combinations, with a column for their counts.
    - permutation_count():Computes counts of unique combinations (order-dependent).
        
        Returns: 
            DataFrame: MultiIndex of permutations, with a column for their counts.
      
