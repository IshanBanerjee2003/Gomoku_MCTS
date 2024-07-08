

# Gomoku with Monte Carlo Tree Search

In this project, I'll implement a Monte Carlo Tree Search (MCTS) for the classic game of Gomoku. The base game engine is derived from [this repository](https://github.com/HackerSir/PygameTutorials/tree/master/Lesson04/Gomoku). Gomoku is played on a Go board with two players, one placing black pieces and the other white pieces, aiming to form an unbroken line of five pieces either horizontally, vertically, or diagonally.

**Project Overview:**
1. **MCTS Implementation**: I'll develop the MCTS algorithm in `ai.py` to enable intelligent gameplay. The search should return the best move along with the table of winning rates for all possible actions at the root node.
2. **Game Rules**: Pieces are placed alternately by the two players, and the goal is to have five consecutive pieces of the same color.
3. **Active Area Optimization**: To accelerate the search process, I'll limit the search to an "active" area around existing pieces.

**Usage:**
I can run the program with:
```bash
python main.py
```
To test the implementation, I can use:
```bash
python main.py -t 1
```
To run the AI against a random policy, I'll use:
```bash
python main.py -t 2
```
I can interact with the game using the mouse and keyboard shortcuts.

**Extra Credit:**
I'll experiment with different strategies, heuristic evaluation functions, and reinforcement learning approaches to enhance the AI's performance. A small tournament will be held to test the strength of the implemented agents.

Implementing MCTS for Gomoku will deepen my understanding of search algorithms and game AI. This project offers ample opportunity to explore advanced techniques and improve the performance of the AI agent.

---

### README

```markdown
# Gomoku with Monte Carlo Tree Search

My task is to implement MCTS for playing Gomoku. The base game engine is from [here](https://github.com/HackerSir/PygameTutorials/tree/master/Lesson04/Gomoku). 

## The Game

Gomoku is a popular game played on the Go board, following much simpler rules. 

- There are two players, one placing black pieces and the other white pieces, at the grid intersections of the board. 
- The two players take turns to place one piece each time. Pieces are never moved or removed from the board. 
- The players' goal is to have five pieces of their own color to form an unbroken line horizontally (`examples/ex1.png`), vertically (`examples/ex2.png`), or diagonally (`examples/ex3.png`). Of course, these are unlikely realistic games between reasonable players. A real game is more like `examples/ex4.png` (black is still very lame at the end).  
- The game engine starts with human against a random-play agent. I can click any grid intersections and see what the computer does. Press enter to see a random game between two random-play agents (also press enter to pause autoplay and switch back to human vs random). Press 'm' to switch to manually playing both sides.  

Here's a youtube video of a competitive Gomoku game (in case I'm interested, or want to procrastinate): https://www.youtube.com/watch?v=siYgHaEwmZU&ab_channel=SandraJones

## Tasks

I need to implement MCTS in `ai.py`. I should read the comments carefully.

Note that the starter code makes it clear that my MCTS should return more than just one action in the end, but also the table of winning rates for all actions for the root node (number of wins divided by total number of samples, i.e., the X-bar term in the best child formula). The tests compare these values that I compute with the correct ones for a few predefined states. 

In MCTS, the search exits when the "computation budget" is reached. The current default value is 1000, which will be used for testing. I can increase or decrease it to see the different behaviors of AI. For instance, with a budget over 6000, a correctly implemented MCTS AI should be able to play a fairly interesting game against me (although it may still make some obvious mistakes when the number of next actions to consider gets larger). 

I can check the MCTS-1000.mov and MCTS-6000.mov files in the repo for a demo of the correctly implemented MCTS with 1000 and 6000 budgets respectively. There is randomness, so the behavior of my implementation does not need to exactly match the video. 

It is easy to see that good moves should be pretty close to the pieces already on the board. Thus, to accelerate search, I have limited the search to a small "active" area around existing pieces (this area uses black lines on the board, compared to grey lines in the inactive area). 

## Usage

To run the program, I can do:
```
python main.py
```

To run tests for the winning rate table in several predefined states, I can do:
```
python main.py -t 1
```

To run AI against random policy, I can do:
```
python main.py -t 2
```

The game engine starts with human against a random-play agent. I can click any grid intersections and see what the computer does. Press enter to see a random game between two random-play agents (also press enter to pause autoplay and switch back to human vs random). Press 'm' to switch to manually playing both sides.  

More details can be found in `Tests` section below.

## Tests

- `python main.py -t 1` runs tests for the winning rate table in several predefined states. Note that a budget of 1000 runs and parameter c=1 in the `best_child` function is used in the test cases. Note that the order in the table is important. To pass the tests, I should make sure to follow the instructions in the `ai.py` starter code. 

- `python main.py -t 2` runs my AI against a random policy. My AI should always win. 

Because the -t 1 tests rely on how the random states are generated, I may have a correct implementation that fails it. Still, the test should be valuable for me to debug. We will mostly check the -t 2 tests to see if I am close to getting things right. As usual, the overall correctness is determined by manual grading, and the tests are just heuristics. 


## Extra Credits

The game gives me an opportunity for testing out many approaches that have been covered in the class. For instance, what kind of heuristic evaluation function can I use to improve the performance? Can I run some form of reinforcement learning to automatically come up with value estimates that can help the MCTS agent? 

I can spend time to try out any strategies I like, to maximize the strength of my AI agent within given computational budget. We will run a small tournament during Week 10. There will be a separate, completely optional, assignment in Gradescope named "EC: Gomoku Competition" for me to submit to, if I would like to participate in the competition. The submission deadline is the same as the due date of the PA. I should implement all I need still only in ai.py and do not use any imports that fail to compile on the autograder. 

I should only work on this part if I am really interested and have the time. We do not specify a fixed amount of extra credits so that I feel the need of doing it just for the points, but submissions that perform well and implement interesting ideas will receive additional credits. In fact, if I am aiming for A+ in the class (which will be determined by soft rules when we give grades at the end), participating in this competition can be very useful. 

## Tips/FAQ

- I can check this [survey article](http://www.incompleteideas.net/609%20dropbox/other%20readings%20and%20resources/MCTS-survey.pdf) for more info on MCTS. 

- If I aren't already, I can check out `pdb` to help me debug!
```
