﻿# ai-project2
 Bài 1:
```python
        # tính khoảng cách mahatan giữa newPos và ghost
        distance_newpos_ghost = [manhattanDistance(newPos, ghost.getPosition()) for ghost in newGhostStates]
        # Trả về khoảng cách gần nhất
        nearghost = min(distance_newpos_ghost)
        # tương tự như trên nhưng tính giữa newPos và listFood
        foodList = newFood.asList()
        if foodList:
            distance_newpos_food = [manhattanDistance(newPos, food) for food in foodList]
            nearfood = min(distance_newpos_food)
        else:
            nearfood = 0
        score = 10/(nearfood+1) + 20/(len(foodList)+1) + successorGameState.getScore() #mahatan tự chỉnh

        if newScaredTimes[distance_newpos_ghost.index(nearghost)] <= 0:
            score -= 15/(nearghost+1)
            print(score)
        return score
        ```
 Bài 2: Cài đặt thuật toán minimax như trên lớp
```python
def minimax_search(self, gameState, agentIndex, depth):
    bestMove = None
    
    if gameState.isWin() or gameState.isLose() or depth >= self.depth:
        return bestMove, self.evaluationFunction(gameState)
    score = float("Inf")
    if agentIndex == 0:  
        score = -float("Inf")

    moves = gameState.getLegalActions(agentIndex)
    
    for move in moves:
        next_gameState = gameState.generateSuccessor(agentIndex, move)
        if agentIndex == 0:  
            next_move, next_score = minimax_search(self, next_gameState, agentIndex + 1, depth)
            if next_score > score:  
                score = next_score
                bestMove = move
        else:
            if agentIndex == (gameState.getNumAgents() - 1):
                next_agent = 0
                depth_next = depth + 1
            else:
                next_agent = agentIndex + 1
                depth_next = depth
            next_move, next_score = minimax_search(self, next_gameState, next_agent, depth_next)
            if next_score < score:  
                score = next_score
                bestMove = move
    return bestMove, score
    ```
