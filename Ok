<!DOCTYPE html>
<html lang="el">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Sudoku - Βελτιωμένη Έκδοση</title>
    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            color: #333;
            line-height: 1.6;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background: linear-gradient(135deg, #6a89cc, #4a69bd);
        }
        
        .container {
            width: 100%;
            max-width: 500px;
        }
        
        .app-card {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
            overflow: hidden;
            padding: 20px;
            position: relative;
            backdrop-filter: blur(5px);
            border: 1px solid rgba(255, 255, 255, 0.5);
            transform-style: preserve-3d;
            perspective: 1000px;
        }
        
        .header-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
            padding-bottom: 15px;
            border-bottom: 1px solid #ddd;
        }
        
        h1 {
            color: #3e2723;
            font-size: 24px;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        }
        
        #timer {
            font-weight: bold;
            color: #4e342e;
            font-size: 18px;
            text-shadow: 1px 1px 1px rgba(0,0,0,0.1);
        }
        
        .controls {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-bottom: 15px;
            justify-content: center;
        }
        
        select {
            padding: 10px 15px;
            border-radius: 10px;
            border: 1px solid #ccc;
            background: white;
            font-size: 16px;
            flex-grow: 1;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            transition: all 0.3s;
        }
        
        select:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 10px rgba(0,0,0,0.15);
        }
        
        .board-wrap {
            display: flex;
            justify-content: center;
            margin: 10px 0 20px;
        }
        
        #sudoku-board {
            display: grid;
            border: 3px solid #3e2723;
            background: white;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            transform: rotateX(5deg) rotateY(5deg);
            transition: transform 0.5s;
        }
        
        #sudoku-board:hover {
            transform: rotateX(0deg) rotateY(0deg);
        }
        
        .cell {
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            background: white;
            position: relative;
            border: 1px solid #888;
            transition: all 0.3s;
        }
        
        .cell:hover {
            background-color: #f0f0f0;
            transform: scale(1.05);
            z-index: 1;
        }
        
        .prefilled {
            background-color: #f7f6f3;
            color: #3e2723;
        }
        
        .user-filled {
            color: #4a69bd;
            font-weight: bold;
        }
        
        .selected {
            background-color: rgba(255, 235, 59, 0.5);
            transform: scale(1.1);
            box-shadow: 0 0 10px rgba(255, 235, 59, 0.5);
            z-index: 2;
        }
        
        .buttons {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
            margin-top: 20px;
        }
        
        .app-btn {
            padding: 12px 20px;
            border: none;
            border-radius: 10px;
            background: #8d6e63;
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            flex-grow: 1;
            min-width: 120px;
        }
        
        .app-btn:hover {
            background: #6d4c41;
            transform: translateY(-2px);
            box-shadow: 0 6px 12px rgba(0, 0, 0, 0.25);
        }
        
        .app-btn:active {
            transform: translateY(0);
        }
        
        #daily-contest {
            text-align: center;
            margin-top: 20px;
            padding-top: 15px;
            border-top: 1px solid #ddd;
            color: #4e342e;
            font-size: 14px;
        }
        
        .number-pad {
            display: grid;
            gap: 10px;
            margin-top: 20px;
        }
        
        .number-btn {
            padding: 12px 0;
            border: none;
            border-radius: 10px;
            background: #8d6e63;
            color: white;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
            font-size: 18px;
        }
        
        .number-btn:hover {
            background: #6d4c41;
            transform: translateY(-3px);
        }
        
        .number-btn:active {
            transform: translateY(0);
        }
        
        .hint-btn {
            background: #e65100;
        }
        
        .hint-btn:hover {
            background: #bf360c;
        }
        
        .clear-btn {
            background: #bf360c;
        }
        
        .clear-btn:hover {
            background: #8d0000;
        }
        
        @media (max-width: 600px) {
            .app-card {
                padding: 15px;
            }
            
            h1 {
                font-size: 20px;
            }
            
            #timer {
                font-size: 16px;
            }
            
            .app-btn {
                padding: 10px 15px;
                font-size: 14px;
            }
            
            .number-btn {
                padding: 10px 0;
                font-size: 16px;
            }
        }
        
        .flash {
            animation: flash 0.5s;
        }
        
        @keyframes flash {
            0% { background-color: rgba(255, 235, 59, 0.3); }
            50% { background-color: rgba(255, 235, 59, 0.8); }
            100% { background-color: rgba(255, 235, 59, 0.3); }
        }
        
        .success {
            animation: success 1s;
        }
        
        @keyframes success {
            0% { 
                background-color: rgba(76, 175, 80, 0.3);
                transform: scale(1);
            }
            50% { 
                background-color: rgba(76, 175, 80, 0.8);
                transform: scale(1.05);
            }
            100% { 
                background-color: rgba(76, 175, 80, 0.3);
                transform: scale(1);
            }
        }
        
        .error {
            animation: error 0.5s;
        }
        
        @keyframes error {
            0% { 
                background-color: rgba(244, 67, 54, 0.3);
                transform: translateX(0);
            }
            25% { 
                background-color: rgba(244, 67, 54, 0.8);
                transform: translateX(-5px);
            }
            75% { 
                background-color: rgba(244, 67, 54, 0.8);
                transform: translateX(5px);
            }
            100% { 
                background-color: rgba(244, 67, 54, 0.3);
                transform: translateX(0);
            }
        }
        
        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background-color: #f44336;
            opacity: 0;
            pointer-events: none;
        }
        
        @keyframes confettiFall {
            0% {
                opacity: 1;
                transform: translateY(0) rotate(0deg);
            }
            100% {
                opacity: 0;
                transform: translateY(100vh) rotate(360deg);
            }
        }
        
        .combo-indicator {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            background: linear-gradient(45deg, #ff5722, #ff9800);
            color: white;
            padding: 10px 20px;
            border-radius: 30px;
            font-weight: bold;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            opacity: 0;
            transition: opacity 0.3s;
            z-index: 1000;
        }
        
        .combo-indicator.show {
            opacity: 1;
        }
        
        .theme-selector {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-top: 15px;
        }
        
        .theme-btn {
            width: 30px;
            height: 30px;
            border-radius: 50%;
            border: 2px solid transparent;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .theme-btn:hover {
            transform: scale(1.1);
        }
        
        .theme-btn.active {
            border-color: #3e2723;
        }
        
        .theme-classic {
            background: linear-gradient(45deg, #8d6e63, #4a69bd);
        }
        
        .theme-dark {
            background: linear-gradient(45deg, #2c3e50, #34495e);
        }
        
        .theme-nature {
            background: linear-gradient(45deg, #27ae60, #2ecc71);
        }
        
        .theme-sunset {
            background: linear-gradient(45deg, #e74c3c, #f39c12);
        }
        
        .ad-container {
            width: 100%;
            min-height: 90px;
            background-color: #f5f5f5;
            border-radius: 10px;
            margin: 15px 0;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 1px dashed #ccc;
            color: #888;
            font-size: 14px;
            text-align: center;
            padding: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="app-card">
            <div class="header-row">
                <h1>3D Sudoku</h1>
                <div id="timer">Χρόνος: 00:00</div>
            </div>
            
            <div class="controls">
                <select id="size">
                    <option value="4">4x4</option>
                    <option value="6">6x6</option>
                    <option value="8">8x8</option>
                    <option value="9" selected>9x9</option>
                </select>
                
                <select id="level">
                    <option value="easy">Εύκολο</option>
                    <option value="medium">Μεσαίο</option>
                    <option value="hard">Δύσκολο</option>
                </select>
            </div>
            
            <div class="board-wrap">
                <div id="sudoku-board"></div>
            </div>
            
            <div class="number-pad" id="number-pad">
                <!-- Numbers will be generated dynamically -->
            </div>
            
            <div class="buttons">
                <button class="app-btn" id="new-game">Νέο Sudoku</button>
                <button class="app-btn" id="check-solution">Έλεγξε</button>
                <button class="app-btn hint-btn" id="use-hint">Hint</button>
            </div>
            
            <div class="theme-selector">
                <div class="theme-btn theme-classic active" data-theme="classic"></div>
                <div class="theme-btn theme-dark" data-theme="dark"></div>
                <div class="theme-btn theme-nature" data-theme="nature"></div>
                <div class="theme-btn theme-sunset" data-theme="sunset"></div>
            </div>
            
            <div class="ad-container" id="ad-container">
                [Διαφήμιση Google AdSense θα εμφανιστεί εδώ]
            </div>
            
            <div id="daily-contest">
                🔥 Daily Contest: Κορυφαίος παίκτης: <span id="top-player">Επισκέπτης</span> — <span id="top-score">0</span>
            </div>
        </div>
    </div>
    
    <div class="combo-indicator" id="combo-indicator">Combo 2x!</div>

    <!-- Ηχητικά εφέ -->
    <audio id="complete-sound" src="https://assets.mixkit.co/sfx/preview/mixkit-winning-chimes-2015.mp3" preload="auto"></audio>
    <audio id="click-sound" src="https://assets.mixkit.co/sfx/preview/mixkit-select-click-1109.mp3" preload="auto"></audio>
    <audio id="error-sound" src="https://assets.mixkit.co/sfx/preview/mixkit-wrong-answer-fail-notification-946.mp3" preload="auto"></audio>

    <script>
        // Game state
        let board = [];
        let solution = [];
        let selectedCell = null;
        let level = 'easy';
        let size = 9;
        let gameTime = 0;
        let timerInterval = null;
        let lastAdTime = 0;
        
        // Solution templates for different sizes
        const solutionTemplates = {
            4: [
                [1, 2, 3, 4],
                [3, 4, 1, 2],
                [2, 1, 4, 3],
                [4, 3, 2, 1]
            ],
            6: [
                [1, 2, 3, 4, 5, 6],
                [4, 5, 6, 1, 2, 3],
                [2, 3, 1, 5, 6, 4],
                [5, 6, 4, 2, 3, 1],
                [3, 1, 2, 6, 4, 5],
                [6, 4, 5, 3, 1, 2]
            ],
            8: [
                [1, 2, 3, 4, 5, 6, 7, 8],
                [5, 6, 7, 8, 1, 2, 3, 4],
                [2, 3, 4, 1, 6, 5, 8, 7],
                [6, 7, 8, 5, 2, 1, 4, 3],
                [3, 4, 1, 2, 7, 8, 5, 6],
                [7, 8, 5, 6, 3, 4, 1, 2],
                [4, 1, 2, 3, 8, 7, 6, 5],
                [8, 5, 6, 7, 4, 3, 2, 1]
            ],
            9: [
                [5, 3, 4, 6, 7, 8, 9, 1, 2],
                [6, 7, 2, 1, 9, 5, 3, 4, 8],
                [1, 9, 8, 3, 4, 2, 5, 6, 7],
                [8, 5, 9, 7, 6, 1, 4, 2, 3],
                [4, 2, 6, 8, 5, 3, 7, 9, 1],
                [7, 1, 3, 9, 2, 4, 8, 5, 6],
                [9, 6, 1, 5, 3, 7, 2, 8, 4],
                [2, 8, 7, 4, 1, 9, 6, 3, 5],
                [3, 4, 5, 2, 8, 6, 1, 7, 9]
            ]
        };
        
        // Initialize the game
        function initGame() {
            loadFromLocalStorage();
            generateSudoku();
            renderBoard();
            setupNumberPad();
            setupEventListeners();
            updateUI();
            startTimer();
            setupAdTimer();
        }
        
        // Generate a new Sudoku puzzle
        function generateSudoku() {
            // Get the selected size
            size = parseInt(document.getElementById('size').value);
            
            // Copy the solution
            solution = JSON.parse(JSON.stringify(solutionTemplates[size]));
            
            // Determine how many cells to show based on difficulty
            let cellsToShow = Math.floor(size * size * 0.5); // Easy - 50% filled
            if (level === 'medium') cellsToShow = Math.floor(size * size * 0.4); // 40% filled
            if (level === 'hard') cellsToShow = Math.floor(size * size * 0.3); // 30% filled
            
            // Create an empty board
            board = Array(size).fill().map(() => Array(size).fill(''));
            
            // Fill some cells based on the solution
            let cellsFilled = 0;
            while (cellsFilled < cellsToShow) {
                const row = Math.floor(Math.random() * size);
                const col = Math.floor(Math.random() * size);
                
                if (board[row][col] === '') {
                    board[row][col] = solution[row][col];
                    cellsFilled++;
                }
            }
        }
        
        // Render the Sudoku board
        function renderBoard() {
            const boardElement = document.getElementById('sudoku-board');
            boardElement.innerHTML = '';
            
            // Set grid dimensions
            boardElement.style.gridTemplateColumns = `repeat(${size}, 1fr)`;
            boardElement.style.gridTemplateRows = `repeat(${size}, 1fr)`;
            
            // Calculate cell size based on board size
            const cellSize = Math.min(360 / size, 50);
            boardElement.style.width = `${cellSize * size}px`;
            boardElement.style.height = `${cellSize * size}px`;
            
            for (let row = 0; row < size; row++) {
                for (let col = 0; col < size; col++) {
                    const cell = document.createElement('div');
                    cell.className = 'cell';
                    cell.dataset.row = row;
                    cell.dataset.col = col;
                    cell.style.fontSize = `${cellSize * 0.5}px`;
                    
                    if (board[row][col] !== '') {
                        cell.textContent = board[row][col];
                        cell.classList.add('prefilled');
                    }
                    
                    // Add thicker borders for subgrids
                    if (size === 9) {
                        if (row % 3 === 0) cell.style.borderTop = '3px solid #3e2723';
                        if (col % 3 === 0) cell.style.borderLeft = '3px solid #3e2723';
                        if (row === size - 1) cell.style.borderBottom = '3px solid #3e2723';
                        if (col === size - 1) cell.style.borderRight = '3px solid #3e2723';
                    } else if (size === 4) {
                        if (row % 2 === 0) cell.style.borderTop = '3px solid #3e2723';
                        if (col % 2 === 0) cell.style.borderLeft = '3px solid #3e2723';
                        if (row === size - 1) cell.style.borderBottom = '3px solid #3e2723';
                        if (col === size - 1) cell.style.borderRight = '3px solid #3e2723';
                    } else if (size === 6) {
                        if (row % 2 === 0) cell.style.borderTop = '3px solid #3e2723';
                        if (col % 3 === 0) cell.style.borderLeft = '3px solid #3e2723';
                        if (row === size - 1) cell.style.borderBottom = '3px solid #3e2723';
                        if (col === size - 1) cell.style.borderRight = '3px solid #3e2723';
                    } else if (size === 8) {
                        if (row % 4 === 0) cell.style.borderTop = '3px solid #3e2723';
                        if (col % 4 === 0) cell.style.borderLeft = '3px solid #3e2723';
                        if (row === size - 1) cell.style.borderBottom = '3px solid #3e2723';
                        if (col === size - 1) cell.style.borderRight = '3px solid #3e2723';
                    }
                    
                    boardElement.appendChild(cell);
                }
            }
        }
        
        // Set up the number pad based on board size
        function setupNumberPad() {
            const numberPad = document.getElementById('number-pad');
            numberPad.innerHTML = '';
            
            // Set grid columns based on size
            const cols = size <= 6 ? size : Math.ceil(size / 2);
            numberPad.style.gridTemplateColumns = `repeat(${cols}, 1fr)`;
            
            // Create number buttons
            for (let i = 1; i <= size; i++) {
                const button = document.createElement('button');
                button.className = 'number-btn';
                button.dataset.number = i;
                button.textContent = i;
                numberPad.appendChild(button);
            }
            
            // Add clear button
            const clearButton = document.createElement('button');
            clearButton.className = 'number-btn clear-btn';
            clearButton.dataset.number = '0';
            clearButton.textContent = 'Clear';
            numberPad.appendChild(clearButton);
        }
        
        // Set up event listeners
        function setupEventListeners() {
            // Cell selection
            document.getElementById('sudoku-board').addEventListener('click', function(e) {
                const cell = e.target;
                if (cell.classList.contains('cell')) {
                    // Play click sound
                    document.getElementById('click-sound').play();
                    
                    // Deselect previous cell
                    if (selectedCell) {
                        selectedCell.classList.remove('selected');
                    }
                    
                    // Select new cell only if it's not prefilled
                    if (!cell.classList.contains('prefilled')) {
                        cell.classList.add('selected');
                        selectedCell = cell;
                    } else {
                        selectedCell = null;
                    }
                }
            });
            
            // Number buttons
            document.getElementById('number-pad').addEventListener('click', function(e) {
                if (e.target.classList.contains('number-btn') && selectedCell) {
                    const number = e.target.dataset.number;
                    
                    if (number === '0') {
                        // Clear the cell
                        selectedCell.textContent = '';
                        selectedCell.classList.remove('user-filled');
                        const row = parseInt(selectedCell.dataset.row);
                        const col = parseInt(selectedCell.dataset.col);
                        board[row][col] = '';
                    } else {
                        // Play click sound
                        document.getElementById('click-sound').play();
                        
                        // Set the number
                        selectedCell.textContent = number;
                        selectedCell.classList.add('user-filled');
                        const row = parseInt(selectedCell.dataset.row);
                        const col = parseInt(selectedCell.dataset.col);
                        board[row][col] = parseInt(number);
                        
                        // Check if the value is correct
                        const isCorrect = board[row][col] === solution[row][col];
                        
                        if (!isCorrect) {
                            // Wrong answer - shake effect and sound
                            selectedCell.classList.add('error');
                            document.getElementById('error-sound').play();
                            setTimeout(() => selectedCell.classList.remove('error'), 500);
                        }
                        
                        // Auto-check if the board is complete
                        if (isBoardComplete()) {
                            checkSolution();
                        }
                    }
                }
            });
            
            // New game button
            document.getElementById('new-game').addEventListener('click', function() {
                level = document.getElementById('level').value;
                generateSudoku();
                renderBoard();
                selectedCell = null;
                
                // Reset timer
                resetTimer();
            });
            
            // Check solution button
            document.getElementById('check-solution').addEventListener('click', checkSolution);
            
            // Use hint button
            document.getElementById('use-hint').addEventListener('click', useHint);
            
            // Level change
            document.getElementById('level').addEventListener('change', function() {
                level = this.value;
                generateSudoku();
                renderBoard();
                selectedCell = null;
                
                // Reset timer
                resetTimer();
            });
            
            // Size change
            document.getElementById('size').addEventListener('change', function() {
                size = parseInt(this.value);
                setupNumberPad();
                generateSudoku();
                renderBoard();
                selectedCell = null;
                
                // Reset timer
                resetTimer();
            });
            
            // Theme buttons
            document.querySelectorAll('.theme-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    document.querySelector('.theme-btn.active').classList.remove('active');
                    this.classList.add('active');
                    
                    const theme = this.dataset.theme;
                    changeTheme(theme);
                });
            });
        }
        
        // Change theme
        function changeTheme(theme) {
            const body = document.body;
            
            switch(theme) {
                case 'classic':
                    body.style.background = 'linear-gradient(135deg, #6a89cc, #4a69bd)';
                    break;
                case 'dark':
                    body.style.background = 'linear-gradient(135deg, #2c3e50, #34495e)';
                    break;
                case 'nature':
                    body.style.background = 'linear-gradient(135deg, #27ae60, #2ecc71)';
                    break;
                case 'sunset':
                    body.style.background = 'linear-gradient(135deg, #e74c3c, #f39c12)';
                    break;
            }
        }
        
        // Create confetti effect
        function createConfetti() {
            for (let i = 0; i < 30; i++) {
                const confetti = document.createElement('div');
                confetti.className = 'confetti';
                confetti.style.left = Math.random() * 100 + 'vw';
                confetti.style.top = '-10px';
                confetti.style.backgroundColor = `hsl(${Math.random() * 360}, 70%, 60%)`;
                confetti.style.animation = `confettiFall ${1 + Math.random() * 2}s linear forwards`;
                
                document.body.appendChild(confetti);
                
                // Remove after animation completes
                setTimeout(() => {
                    confetti.remove();
                }, 3000);
            }
        }
        
        // Check if the board is complete (no empty cells)
        function isBoardComplete() {
            for (let row = 0; row < size; row++) {
                for (let col = 0; col < size; col++) {
                    if (board[row][col] === '') {
                        return false;
                    }
                }
            }
            return true;
        }
        
        // Check the solution
        function checkSolution() {
            let correct = true;
            let incorrectCells = [];
            
            for (let row = 0; row < size; row++) {
                for (let col = 0; col < size; col++) {
                    if (board[row][col] !== solution[row][col]) {
                        correct = false;
                        incorrectCells.push({row, col});
                    }
                }
            }
            
            if (correct) {
                // Show success
                const boardElement = document.getElementById('sudoku-board');
                boardElement.classList.add('success');
                
                // Play completion sound
                document.getElementById('complete-sound').play();
                
                // Create confetti
                createConfetti();
                
                // Show success message
                setTimeout(() => {
                    alert('🎉 Συγχαρητήρια! Ολοκλήρωσες το Sudoku! 🎉');
                    boardElement.classList.remove('success');
                }, 1000);
                
                // Save to local storage
                saveToLocalStorage();
                
                // Stop timer
                stopTimer();
            } else {
                // Highlight incorrect cells
                incorrectCells.forEach(({row, col}) => {
                    const cell = document.querySelector(`.cell[data-row="${row}"][data-col="${col}"]`);
                    if (cell && !cell.classList.contains('prefilled')) {
                        cell.classList.add('error');
                        setTimeout(() => cell.classList.remove('error'), 1000);
                    }
                });
                
                alert('Κάποια κελιά είναι λάθος ή κενά. Συνέχισε!');
            }
        }
        
        // Use a hint
        function useHint() {
            if (!selectedCell || selectedCell.classList.contains('prefilled')) {
                alert('Παρακαλώ διάλεξε ένα κενό κελί πρώτα!');
                return;
            }
            
            const row = parseInt(selectedCell.dataset.row);
            const col = parseInt(selectedCell.dataset.col);
            
            // Fill in the correct number
            selectedCell.textContent = solution[row][col];
            selectedCell.classList.add('user-filled');
            board[row][col] = solution[row][col];
            
            // Save to local storage
            saveToLocalStorage();
            
            // Auto-check if the board is complete
            if (isBoardComplete()) {
                checkSolution();
            }
        }
        
        // Update the UI
        function updateUI() {
            // Update daily contest (for demo purposes)
            document.getElementById('top-player').textContent = 'Επισκέπτης';
            document.getElementById('top-score').textContent = Math.floor(gameTime / 60);
        }
        
        // Timer functions
        function startTimer() {
            if (timerInterval) clearInterval(timerInterval);
            
            timerInterval = setInterval(() => {
                gameTime++;
                const minutes = Math.floor(gameTime / 60);
                const seconds = gameTime % 60;
                document.getElementById('timer').textContent = `Χρόνος: ${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
                
                // Update UI every second
                updateUI();
            }, 1000);
        }
        
        function stopTimer() {
            if (timerInterval) {
                clearInterval(timerInterval);
                timerInterval = null;
            }
        }
        
        function resetTimer() {
            stopTimer();
            gameTime = 0;
            document.getElementById('timer').textContent = 'Χρόνος: 00:00';
            startTimer();
        }
        
        // Ad display function
        function setupAdTimer() {
            // Show ad every 5 minutes (300 seconds)
            setInterval(() => {
                showAd();
            }, 300000); // 5 minutes in milliseconds
        }
        
        function showAd() {
            // This would be replaced with actual AdSense code
            const adContainer = document.getElementById('ad-container');
            adContainer.innerHTML = '<strong>Διαφήμιση Google AdSense</strong><br>Αυτή η διαφήμιση εμφανίζεται κάθε 5 λεπτά';
            adContainer.style.backgroundColor = '#ffeaa7';
            adContainer.style.color = '#2d3436';
            
            // Hide ad after 30 seconds
            setTimeout(() => {
                adContainer.innerHTML = '[Διαφήμιση Google AdSense θα εμφανιστεί εδώ]';
                adContainer.style.backgroundColor = '#f5f5f5';
                adContainer.style.color = '#888';
            }, 30000);
        }
        
        // Save game state to local storage
        function saveToLocalStorage() {
            const gameState = {
                board: board,
                solution: solution,
                level: level,
                size: size,
                gameTime: gameTime
            };
            
            localStorage.setItem('sudokuGame', JSON.stringify(gameState));
        }
        
        // Load game state from local storage
        function loadFromLocalStorage() {
            const savedGame = localStorage.getItem('sudokuGame');
            
            if (savedGame) {
                const gameState = JSON.parse(savedGame);
                board = gameState.board;
                solution = gameState.solution;
                level = gameState.level;
                size = gameState.size || 9;
                gameTime = gameState.gameTime || 0;
                
                // Set the selectors
                document.getElementById('level').value = level;
                document.getElementById('size').value = size;
            } else {
                generateSudoku();
            }
        }
        
        // Initialize the game when the page loads
        document.addEventListener('DOMContentLoaded', initGame);
    </script>
</body>
</html>
