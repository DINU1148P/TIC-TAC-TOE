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
      background: linear-gradient(135deg, #43cea2, #185a9d);
      background-size: 200% 200%;
      animation: backgroundColorShift 10s infinite alternate;
    }

    @keyframes backgroundColorShift {
      0% { background-position: 0% 50%; }
      100% { background-position: 100% 50%; }
    }

    .game-container {
      text-align: center;
      background: linear-gradient(145deg, #ffffff, #f0f0f0);
      padding: 40px;
      border-radius: 20px;
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);
    }

    h1 {
      color: #185a9d;
      font-size: 2.5rem;
      margin: 0;
      background: linear-gradient(45deg, #43cea2, #185a9d);
      -webkit-background-clip: text;
      color: transparent;
    }

    .status p {
      font-size: 1.5rem;
      font-weight: bold;
      color: #43cea2;
      margin-top: 10px;
      animation: textGlow 1.5s ease-in-out infinite alternate;
    }

    @keyframes textGlow {
      from { color: #43cea2; }
      to { color: #185a9d; }
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 10px;
      margin-top: 20px;
      justify-content: center;
    }

    .cell {
      width: 100px;
      height: 100px;
      background: #e8f7f2;
      border: 2px solid #ddd;
      border-radius: 15px;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 2.5rem;
      cursor: pointer;
      transition: transform 0.3s ease, background-color 0.3s ease;
      font-weight: bold;
      color: #333;
      box-shadow: 4px 4px 10px rgba(0, 0, 0, 0.15);
    }

    .cell:hover {
      background: #d0ece7;
      transform: scale(1.1);
    }

    .cell.X {
      color: #185a9d;
      animation: markPop 0.3s ease-in-out;
    }

    .cell.O {
      color: #43cea2;
      animation: markPop 0.3s ease-in-out;
    }

    @keyframes markPop {
      0% { transform: scale(0.8) rotate(0deg); }
      50% { transform: scale(1.2) rotate(10deg); }
      100% { transform: scale(1) rotate(0deg); }
    }

    button {
      margin-top: 20px;
      padding: 12px 24px;
      font-size: 1rem;
      font-weight: bold;
      color: #ffffff;
      background: linear-gradient(45deg, #43cea2, #185a9d);
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.2s ease;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
    }

    button:hover {
      background: linear-gradient(45deg, #185a9d, #43cea2);
      transform: scale(1.05);
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

      if (board[index] !== "" || gameOver) return;

      board[index] = currentPlayer;
      cell.textContent = currentPlayer;
      cell.classList.add(currentPlayer);

      if (checkWinner()) {
        status.textContent = `${currentPlayer} wins!`;
        gameOver = true;
      } else if (board.every(cell => cell !== "")) {
        status.textContent = "It's a draw!";
        gameOver = true;
      } else {
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
        cell.classList.remove("X", "O");
      });
    }

    cells.forEach(cell => {
      cell.addEventListener("click", handleCellClick);
    });
  </script>
</body>
</html>

