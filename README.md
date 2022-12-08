# AI-Project 
---
### Group 15  -  INT3401_22
#### Link repo: https://github.com/huuducsc/Pacman-search
#### Members:
- Hoàng Phan Hữu Đức (20020011) 
- Hoàng Phan Hữu Phúc (20020026)
- Hoàng Trọng Nghĩa (20020024)
- Phạm Đình Quân (20020067)
---

# Project 1: Search
https://inst.eecs.berkeley.edu/~cs188/fa20/project1/
## Question 1 (3 points): Finding a Fixed Food Dot using Depth First Search
#### Requirements:
* Problem: `PositionSearchProblem` (find paths to only 1 goal position) 
* Algorithm: Depth-First Search (DFS) 
* Heuristic: none
#### Solution:
* Normal DFS using stack (in function [`depthFirstSearch`)](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/search.py#L91-L105)
#### Result: 3/3

## Question 2 (3 points): Breadth First Search
#### Requirements:
* Problem: `PositionSearchProblem` 
* Algorithm: Breadth-First Search (BFS)
* Heuristic: none
#### Solution:
* Normal BFS using queue (see [`breadthFirstSearch`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/search.py#L113-L127))
#### Result: 3/3

## Question 3 (3 points): Varying the Cost Function
#### Requirements:
* Problem:  `PositionSearchProblem` with optimized cost
* Algorithm: Uniform-Cost Search (Dijkstra)
* Heuristic: none
#### Solution:
* Normal Dijsktra using priority-queue (heap) in [`uniformCostSearch`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/search.py#L132-L148)
#### Result: 3/3

## Question 4 (3 points): A* search
#### Requirements:
* Problem: `PositionSearchProblem` with optimized cost
* Algorithm: A* Search
* Heuristic: manhattanHeuristic (already implemented)
#### Solution:
* Uniform cost search with the priority of the total `cost` + `heuristic()` (see [`aStarSearch`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/search.py#L161-L179))
#### Result: 3/3


##  Question 5 (3 points): Finding All the Corners
#### Requirements:
* Problem: `CornersProblem` (find a path through all four corners of a layout, optimized cost)
* Algorithm: Breadth-First Search 
* Heuristic: None
#### Solution:
* Add new tuple to state, represent for list of corners was visited
* Search by BFS algorithm ()
    *  from `startingState` is `(startingPosition, ())` ([`getStartState`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/searchAgents.py#L316-L321))
    *  goal states are which state visited corners (length = 4) ([`isGoalState`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/searchAgents.py#L324-L330))
    *  change state by new implementation of [`getSuccessors`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/searchAgents.py#L332-L365)
#### Result: 3/3

## Question 6 (3 points): Corners Problem: Heuristic
#### Requirements:
* Problem: `CornersProblem` (find a path through all four corners of a layout,  optimized cost)
* Algorithm: A* Search
* Heuristic: `cornersHeuristic` (require)
#### Solution:
* [`cornersHeuristic`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/searchAgents.py#L383-L419): cost of the shortest journey from position through all remaining corners
    * Start at the current position, go to the nearest unvisited corner by Manhattan distance
    * Continue going to the nearest other corners until no one left
    * the total Manhattan distance of the journey is the result of heuristic
* A* search with this heuristic (in class [`AStarCornersAgent`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/searchAgents.py#L423-L429))
#### Result: 3/3

## Question 7 (4 points): Eating All The Dots
#### Requirements:
* Problem: `FoodSearchProblem` (find a path that collects all of the food (dots), optimized cost)
* Algorithm: A* Search
* Heuristic: need to implement `foodHeuristic ` 
#### Solution:
* [`foodHeuristic`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/searchAgents.py#L494-L531): return a max of `mazeDistance` from position to any unclaimed food
    * `mazeDistance` (already implemented) is BFS distance in the maze of 2 positions
    * This strategy prioritize the position that has the farthest distance to any food is closest
* Execute A* search with this heuristic ([`AStarFoodSearchAgent`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/searchAgents.py#L485-L491))

#### Result: 5/4 (1 point bonus)

## Question 8 (3 points): Suboptimal Search:
#### Requirements:
* Problem: `FoodSearchProblem` (find a path that collects all of the food (dots), optimized cost)
* Algorithm: Greedy (with any position, the agent will go to the closest food)
* Heuristic: None
#### Solutions:
* At a position, find a path to the closest food by uniform cost search (goal states are any dots) ([`findPathToClosestDot`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/searchAgents.py#L554-L570))
    * Use class `AnyFoodSearchProblem` to search, goal states is any food ([`isGoalState`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/search/searchAgents.py#L600-L607))
* Repeat searching until there is no food left
#### Result: 3/3

## Total result of project 1: 26/25

# Project 2: Multi-Agent Search
https://inst.eecs.berkeley.edu/~cs188/fa20/project2/

## Question 1 (4 points): Reflex Agent
#### Requirements:
* Problem: improve `ReflexAgent` by implementing function `evaluationFunction`
* Algorithm: any
#### Solution: 
[`evaluationFunction`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/multiagent/multiAgents.py#L54)
* Calculate the evaluation of each position from -1e6 to 1e6 as:
    * If its entity is ghost -> return min value (-1e6)
    * If its entity is food -> return max value (1e6)
    * Else return 1e6 * (distance from this position to closest food / 2 - distance from this position to closest ghost) (by manhattan distance)
* It means the evaluation considers that keeping distance from ghost is twice important than collecting food.
#### Result: 4/4

## Question 2 (5 points): Minimax
#### Requirements:
* Problem: find the minimax action for `MinimaxAgent`
* Algorithm: minimax
#### Solution:
* Implement function [`minimaxValue`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/multiagent/multiAgents.py#L167-L187) to evaluate the minimax action:
    * For the ghost, choose an action which has the min value with the next minimax action of Pacman. Ghosts start in order of indexes (not the best strategy)
    * For Pacman, choose an action which has the max value with the next minimax action of ghosts. 
#### Result: 5/5

## Question 3 (5 points): Alpha-Beta Pruning
#### Requirements:
* Problem: Add alpha-beta prunning for minimax from Q2
* Algorithm: minimax
#### Solution:
* Add alpha-beta prunning for function [`minimaxValue`](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/multiagent/multiAgents.py#L212-L241)
#### Result: 5/5

## Question 4 (5 points): Expectimax
#### Requirements:
* Problem: no longer take the min over all ghost actions, but the expectation according to your agent’s model of how the ghosts act
* Algorithm: minimax
#### Solution:
* `minimaxValue` for ghosts returns the average minimax value of all actions ([code snippet](https://github.com/huuducsc/AI-Project-Group15-INT3401_22/blob/main/multiagent/multiAgents.py#L279-L285)) 
#### Result: 5/5

## Question 5 (6 points): Evaluation Function
#### Requirements:
* Problem: a better evaluation function for pacman
* Algorithm: any
#### Solution: not found
#### Result: 0/6

## Total result of project 2: 19/25
