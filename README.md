# PRODIGY_WD_03
Embark on a journey of strategic fun with Tac-Toe Triumph, a captivating web application meticulously crafted using HTML, CSS, and JavaScript. Unleash the classic tic-tac-toe game in a modern, interactive format that guarantees hours of excitement for players of all ages.
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tic-Tac-Toe</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin: 50px;
        }
        #board {
            display: grid;
            grid-template-columns: repeat(3, 100px);
            gap: 5px;
        }
        .cell {
            width: 100px;
            height: 100px;
            font-size: 24px;
            cursor: pointer;
            border: 1px solid #ccc;
            display: flex;
            align-items: center;
            justify-content: center;
        }
    </style>
</head>
<body>
    <h1>Tic-Tac-Toe</h1>
    <div id="board"></div>
    <script>
        const board = document.getElementById('board');
        let currentPlayer = 'X';
        let gameBoard = ['', '', '', '', '', '', '', '', ''];
        let gameActive = true;

        function createCell(index) {
            const cell = document.createElement('div');
            cell.classList.add('cell');
            cell.dataset.index = index;
            cell.addEventListener('click', handleCellClick);
            board.appendChild(cell);
        }

        function renderBoard() {
            board.innerHTML = '';
            gameBoard.forEach((value, index) => {
                createCell(index);
                const cell = document.querySelector(`.cell[data-index="${index}"]`);
                cell.textContent = value;
            });
        }

        function handleCellClick() {
            if (!gameActive) return;

            const index = this.dataset.index;
            if (gameBoard[index] === '') {
                gameBoard[index] = currentPlayer;
                renderBoard();
                if (checkWinner()) {
                    alert(`${currentPlayer} wins!`);
                    resetGame();
                } else if (gameBoard.every(cell => cell !== '')) {
                    alert("It's a draw!");
                    resetGame();
                } else {
                    currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
                }
            }
        }

        function checkWinner() {
            const winPatterns = [
                [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
                [0, 3, 6], [1, 4, 7], [2, 5, 8], // columns
                [0, 4, 8], [2, 4, 6]             // diagonals
            ];

            for (const pattern of winPatterns) {
                const [a, b, c] = pattern;
                if (gameBoard[a] !== '' && gameBoard[a] === gameBoard[b] && gameBoard[b] === gameBoard[c]) {
                    gameActive = false;
                    return true;
                }
            }
            return false;
        }

        function resetGame() {
            currentPlayer = 'X';
            gameBoard = ['', '', '', '', '', '', '', '', ''];
            gameActive = true;
            renderBoard();
        }

        // Initialize the game board
        renderBoard();
    </script>
</body>
</html>
