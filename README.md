# Game of Sticks

In the Game of Sticks there is a heap of sticks on a board. On their turn, each player picks up 1 to 3 sticks. The one who has to pick the final stick will be the loser.

The following is an example of the game of sticks.

- The game starts with 20 sticks on the board.
- Marvin takes 3 sticks, there are 17 sticks remaining.
- Gunther takes 2 sticks, there are 15 sticks remaining.
- Marvin takes 1 stick, there are 14 sticks remaining.
- Gunther takes 3 sticks, there are 11 sticks remaining.
- Marvin takes 2 sticks, there are 9 sticks remaining.
- Gunther takes 2 sticks, there are 7 sticks remaining.
- Marvin takes 3 sticks, there are 4 sticks remaining.
- Gunther takes 1 stick, there are 3 sticks remaining.
- Marvin takes 2 sticks, there is 1 stick remaining.
- Gunther has to take the final stick and loses.

This assignment is split into four parts:

1. Implementing the game as a two-player game.
2. Adding an AI that can be played against.
3. Adding an option for training the AI against another AI.
4. Performing mathematical analysis of the problem based on information gathered from the AI.

## Objectives
After completing this assignment, you will...

- Understand lists and tuples
- Be able to use functions effectively
- Be able to build a simple AI

## Deliverables
- A Git repo named game-of-sticks containing at least:
  - README.md file explaining how to run your project
  - An implementation of the game in at least one file named sticks.py.
  - A suite of tests for your project in at least one file named sticks_test.py.

## Normal Mode
### Player vs Player
Create a game where two players can play against each other. The two examples below demonstrate how the game behaves.

Example 1:

```
Welcome to the Game of Sticks!
How many sticks are there on the table initially (10-100)? 10

There are 10 sticks on the board.
Player 1: How many sticks do you take (1-3)? 3

There are 7 sticks on the board.
Player 2: How many sticks do you take (1-3)? 3

There are 4 sticks on the board.
Player 1: How many sticks do you take (1-3)? 3

There is 1 stick on the board.
Player 2: How many sticks do you take (1-3)? 1
Player 2, you lose.
```

Example 2:

```
Welcome to the Game of Sticks!
How many sticks are there on the table initially (10-100)? 500
Please enter a number between 10 and 100.
How many sticks are there on the table initially (10-100)? 3
Please enter a number between 10 and 100.
How many sticks are there on the table initially (10-100)? 50

There are 50 sticks on the board.
Player 1: How many sticks do you take (1-3)? 3

There are 47 sticks on the board.
Player 2: How many sticks do you take (1-3)? 55
Please enter a number between 1 and 3
Player 2: How many sticks do you take (1-3)? 3

There are 44 sticks on the board.
Player 1: How many sticks do you take (1-3)? 3
...

There is 1 stick on the board.
Player 1: How many sticks do you take (1-3)? 1
Player 1, you lose.
```

### Player vs AI
Let's create an artificial intelligence player for the Game of Sticks. Instead of creating an AI based off knowledge of the optimal strategy, we'll create an AI that can learn from games it wins and loses, and then we can look at it to figure out the best strategy.

Consider the functionality of the AI using the following description:

An AI has a number of hats, one hat for each possible amount of sticks on the table. Initially, each hat contains three balls that are numbered from 1 to 3.

At every step of the game that the AI plays, the AI takes a random ball out of the hat that matches the amount of sticks currently on the board. When the AI takes a ball out of a hat, it places it next to the hat for waiting, reads the number on the ball, and takes the amount of sticks that the ball indicates.

If the AI wins the game, it puts two balls of the type to each hat that has a ball next to it. Both balls have the same number. If the AI loses, it will throw away the balls that are next to the hats (note: A hat must always have at least one ball of each number, hence the last ball of a specific number cannot be thrown away and must be put back to the hat).

As more and more games are played, there will be more balls that indicate a good number of sticks to take. This means that as balls are taken at random, it becomes more likely that the AI is able to play well.

Example
Let us consider an example where there are 10 sticks at the beginning. The hat contents for the AI are as follows:
```
hat	1	2	3	4	5	6	7	8	9
content	1,2,3	1,2,3	1,2,3	1,2,3	1,2,3	1,2,3	1,2,3	1,2,3	1,2,3
```
The game may proceed as follows:

Player takes 3 sticks, there are 7 sticks remaining.
AI randomly picks up ball 2 from the hat 7. This means that the AI takes 2 sticks, and there are 5 sticks remaining.
Player takes 1 stick, there are 4 sticks remaining.
AI randomly picks up ball 3 from hat 4. This means that AI takes 3 sticks, and there is 1 stick remaining.
Player has to take the final stick and loses.
Now, the situation with the AI is as follows:
```
hat	1	2	3	4	5	6	7	8	9
content	1,2,3	1,2,3	1,2,3	1,2	1,2,3	1,2,3	1,3	1,2,3	1,2,3
beside				3			2		
```
As the AI wins the game, it will put the balls that are next to the hats back to the hats with extra balls. The situation is now as follows:
```
hat	1	2	3	4	5	6	7	8	9
content	1,2,3	1,2,3	1,2,3	1,2,3,3	1,2,3	1,2,3	1,2,2,3	1,2,3	1,2,3
```
Now the AI will more likely take 3 sticks in the case of four sticks remaining on the board, and 2 sticks in case there are 7 sticks remaining on the board.

Your task is to modify the human vs. human version of the game so that the player can choose to play against an AI that works as described above. After each game, the AI will update the contents of its hats. The AI will play relatively randomly at first, but you will notice that it will start to learn a strategy as you play against it.

The following example displays how the program would behave after you have finished this step.
```
Welcome to the Game of Sticks!
How many sticks are there on the table initially (10-100)? 10
Options:
 Play against a friend (1)
 Play against the computer (2)
Which option do you take (1-2)? 2

There are 10 sticks on the board.
Player 1: How many sticks do you take (1-3)? 3

There are 7 sticks on the board.
AI selects 2.

There are 5 sticks on the board.
Player 1: How many sticks do you take (1-3)? 3

There are 2 sticks on the board.
AI selects 2.
AI loses.
Play again (y/n)? y

There are 10 sticks on the board.
Player 1: How many sticks do you take (1-3)? 1

There are 9 sticks on the board.
AI selects 1.

There are 8 sticks on the board.
Player 1: How many sticks do you take (1-3)? 3

There are 5 sticks on the board.
AI selects 3.

There are 2 sticks on the board.
Player 1: How many sticks do you take (1-3)? 2
You lose.
Play again (y/n)? y

There are 10 sticks on the board.
Player 1: How many sticks do you take (1-3)? 3

There are 7 sticks on the board.
AI selects 2.

There are 5 sticks on the board.
Player 1: How many sticks do you take (1-3)? 3

There are 2 sticks on the board.
AI selects 2.
AI loses.
Play again (y/n)? n
```
