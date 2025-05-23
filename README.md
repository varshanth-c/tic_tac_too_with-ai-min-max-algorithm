# tic_tac_too_with-ai-min-max-algorithm
# 🧠 Smart Tic-Tac-Toe AI

A classic Tic-Tac-Toe game playable in your browser, featuring a "smart" AI opponent with varying difficulty levels. Challenge yourself against an AI that ranges from making random moves to being an unbeatable opponent using the Minimax algorithm with Alpha-Beta pruning.

## ✨ Features

*   **Play Tic-Tac-Toe**: Enjoy the timeless game of X's and O's.
*   **Selectable Difficulty**:
    *   **Easy**: AI makes random moves.
    *   **Medium**: AI uses a depth-limited Minimax algorithm.
    *   **Hard**: AI uses the full Minimax algorithm with Alpha-Beta pruning (unbeatable!).
*   **Choose Your Symbol**: Play as 'X' (goes first) or 'O' (goes second).
*   **Game Statistics**: Tracks your wins, AI wins, and draws.
*   **Clear Statistics**: Option to reset the game score.
*   **Theme Toggle**: Switch between Light and Dark mode for comfortable viewing.
*   **Responsive Design**: Playable on various screen sizes.
*   **Visual Feedback**: Winning moves are highlighted with an animation.

## 🎮 How to Play

1.  **Open the Game**: Simply open the `index.html` (or the HTML file containing the game) in a modern web browser.
2.  **Choose Settings (Optional)**:
    *   **Difficulty**: Select from "Easy", "Medium", or "Hard" using the dropdown.
    *   **You play as**: Choose to be 'X' (first player) or 'O' (second player).
3.  **Start Playing**:
    *   If you are 'X', click on an empty cell on the 3x3 grid to place your mark.
    *   If you are 'O', the AI will make the first move.
4.  **Turns**: You and the AI will take turns placing your marks.
5.  **Objective**: Be the first to get three of your marks in a row (horizontally, vertically, or diagonally).
6.  **Game End**: The game ends when a player wins, or the board is full (a draw). The status will be displayed.
7.  **New Game**: Click the "🔄 New Game" button to play again. Current settings (difficulty, symbol) will be retained.
8.  **Clear Stats**: Click "📊 Clear Stats" to reset the win/draw/loss counters.
9.  **Toggle Theme**: Click the "🌙 Dark Mode" / "☀️ Light Mode" button to change the visual theme.

## 🤖 AI Difficulty Modes Explained

The AI's intelligence varies significantly based on the selected difficulty mode. Here's a detailed breakdown:

### 🟢 Easy Mode

*   **Approach**:
    The AI selects a move by picking a random available cell on the board. It does not employ any strategy or foresight.
*   **Theory**:
    This is the simplest form of AI. It relies purely on chance.
    1.  **Identify Empty Cells**: The AI first looks at the current state of the board and identifies all cells that are not yet occupied by 'X' or 'O'.
    2.  **Random Selection**: From this list of empty cells, it picks one at random.
    3.  **No Evaluation**: There's no evaluation of whether the chosen move is good or bad, leads to a win, or blocks an opponent's win.
    *This mode is good for beginners or for a quick, unpredictable game.*

### 🟡 Medium Mode

*   **Approach**:
    The AI uses the **Minimax algorithm** but with a **limited search depth**. This means it looks a few moves ahead to evaluate potential outcomes, but not all the way to the end of the game. In this implementation, the depth is limited (e.g., to 3 moves ahead).
*   **Theory**:
    **Minimax Algorithm (Core Concept)**:
    Minimax is a decision-making algorithm typically used in two-player turn-based games like Tic-Tac-Toe, Chess, or Checkers. The core idea is to minimize the possible loss for a worst-case scenario (minimize the maximum loss).
    1.  **Game Tree**: Minimax explores a "game tree" where each node represents a possible state of the game, and edges represent moves.
    2.  **Maximizing and Minimizing Players**:
        *   The **AI** is the **Maximizing Player**: It tries to achieve the highest possible score.
        *   The **Human Opponent** is the **Minimizing Player**: It is assumed to play optimally to achieve the lowest possible score (from the AI's perspective).
    3.  **Scoring Terminal States**:
        *   AI Win: High positive score (e.g., +10)
        *   Human Win: High negative score (e.g., -10)
        *   Draw: Neutral score (e.g., 0)
    4.  **Recursive Evaluation**: The algorithm recursively explores possible moves:
        *   On the AI's turn (Maximizer), it picks the move that leads to the state with the maximum score.
        *   On the Human's turn (Minimizer), it's assumed the human will pick the move that leads to the state with the minimum score.
    5.  **Backpropagation of Scores**: Scores are propagated up the game tree from the terminal states to the current state.
    **Limited Depth**:
    Instead of exploring the entire game tree until every possible game conclusion (win, loss, draw), the Medium AI stops its search after a predefined number of moves (depth). When it reaches this depth limit, it evaluates the current board position using a heuristic (a simpler evaluation function that estimates the desirability of the position, though in this specific Tic-Tac-Toe code, it defaults to 0 if it's not a terminal state at that depth).
    *   **Pros**: Faster than full Minimax, provides a decent challenge.
    *   **Cons**: Can make mistakes if the best move is beyond its search depth. It might not see an opponent's winning trap that is more than a few moves away.
    *This mode offers a more challenging opponent than Easy, as it has some level of strategic thinking.*

### 🔴 Hard Mode (Unbeatable)

*   **Approach**:
    The AI uses the **Minimax algorithm** with its full search depth, further optimized by **Alpha-Beta Pruning**. In Tic-Tac-Toe, the game tree is small enough that a full search is feasible, making the AI play perfectly.
*   **Theory**:
    **Minimax Algorithm (Full Depth)**:
    Same as described for Medium mode, but the algorithm explores the game tree all the way to terminal states (win, loss, or draw) for every possible sequence of moves. This ensures it finds the absolute best move in any situation.
    **Alpha-Beta Pruning (Optimization)**:
    While full Minimax finds the optimal move, it can be slow for complex games because it explores many branches of the game tree that are irrelevant. Alpha-Beta Pruning is an optimization technique that reduces the number of nodes evaluated by the Minimax algorithm.
    1.  **Alpha (α)**: Represents the best (highest-value) score found so far for the **Maximizing player** (AI) along the current path in the search tree. Initially, alpha is negative infinity.
    2.  **Beta (β)**: Represents the best (lowest-value) score found so far for the **Minimizing player** (Human) along the current path. Initially, beta is positive infinity.
    3.  **The Pruning Condition**:
        *   During the Maximizer's (AI's) turn, if it finds a move whose score is greater than or equal to `beta`, it means the Minimizer (Human) would have already avoided this path earlier because it had a better option (leading to a score <= `beta`). So, the current branch can be pruned (no need to explore further).
        *   During the Minimizer's (Human's) turn, if it finds a move whose score is less than or equal to `alpha`, it means the Maximizer (AI) would have already avoided this path earlier because it had a better option (leading to a score >= `alpha`). So, this branch can also be pruned.
        *   Essentially, if `alpha >= beta`, the current node's subtree doesn't need to be explored further.
    4.  **Efficiency**: Alpha-Beta Pruning does not affect the outcome of the Minimax algorithm; it still finds the optimal move. However, it can significantly speed up the search by eliminating large parts of the game tree that don't need to be evaluated.
    **Depth Adjustment for Scores**:
    The implementation also slightly adjusts scores based on depth:
    *   AI wins are preferred if they are quicker (score - depth).
    *   Human wins (AI losses) are preferred if they are delayed (score + depth from AI's perspective).
    This encourages the AI to win faster and lose slower, if multiple winning/losing paths exist.
    *This mode results in an AI that plays perfectly. If the human player does not make any mistakes, the game will always end in a draw or an AI win (if the human makes a mistake). You cannot beat this AI.*

## 🛠️ Technologies Used

*   **HTML**: Structure of the game.
*   **CSS**: Styling and visual presentation, including animations.
*   **JavaScript**: Game logic, AI implementation, and DOM manipulation.

## 🚀 How to Run

1.  Clone this repository or download the HTML file.
2.  Open the `[your-html-file-name].html` file in any modern web browser (e.g., Chrome, Firefox, Safari, Edge).
3.  No special setup or server is required.

---

Enjoy the game!
