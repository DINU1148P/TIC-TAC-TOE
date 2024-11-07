# TIC-TAC-TOE
Tic-Tac-Toe game using HTML, CSS, and JavaScript. This game allows two players to take turns and will display the winner or a draw once the game is over.
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic-Tac-Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      margin: 0;
      background-color: #f4f4f4;
    }

    .game-container {
      text-align: center;
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 5px;
      margin-top: 20px;
      justify-content: center;
    }

    .cell {
      width: 100px;
      height: 100px;
      background-color: white;
      border: 2px solid #000;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 2rem;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    .cell:hover {
      background-color: #f0f0f0;
    }

    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 1rem;
      cursor: pointer;
    }

    .status p {
      font-size: 1.5rem;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="game-container">
    <h1>Tic-Tac-Toe</h1>
    <div class="status">
      <p id="status">Player X's turn</p>
    </div>
    <div class="board">
      <div class="cell" data-index="0"></div>
      <div class="cell" data-index="1"></div>
      <div class="cell" data-index="2"></div>
      <div class="cell" data-index="3"></div>
      <div class="cell" data-index="4"></div>
      <div class="cell" data-index="5"></div>
      <div class="cell" data-index="6"></div>
      <div class="cell" data-index="7"></div>
      <div class="cell" data-index="8"></div>
    </div>
    <button id="reset" onclick="resetGame()">Restart Game</button>
  </div>

  <script>
    let board = ["", "", "", "", "", "", "", "", ""];
    let currentPlayer = "X";
    let gameOver = false;

    const cells = document.querySelectorAll(".cell");
    const status = document.getElementById("status");

    function handleCellClick(event) {
      const cell = event.target;
      const index = cell.getAttribute("data-index");

      // Ignore the cell if it has already been played or the game is over
      if (board[index] !== "" || gameOver) return;

      // Mark the cell with the current player's symbol
      board[index] = currentPlayer;
      cell.textContent = currentPlayer;

      // Check for a winner or a draw
      if (checkWinner()) {
        status.textContent = `${currentPlayer} wins!`;
        gameOver = true;
      } else if (board.every(cell => cell !== "")) {
        status.textContent = "It's a draw!";
        gameOver = true;
      } else {
        // Switch to the other player
        currentPlayer = currentPlayer === "X" ? "O" : "X";
        status.textContent = `${currentPlayer}'s turn`;
      }
    }

    function checkWinner() {
      const winningCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6]
      ];

      return winningCombinations.some(combination => {
        const [a, b, c] = combination;
        return board[a] !== "" && board[a] === board[b] && board[a] === board[c];
      });
    }

    function resetGame() {
      board = ["", "", "", "", "", "", "", "", ""];
      gameOver = false;
      currentPlayer = "X";
      status.textContent = `${currentPlayer}'s turn`;

      cells.forEach(cell => {
        cell.textContent = "";
      });
    }

    cells.forEach(cell => {
      cell.addEventListener("click", handleCellClick);
    });
  </script>
</body>
</html>
