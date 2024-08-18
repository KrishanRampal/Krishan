<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>iOS Calculator</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }

        body {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f0f0f0;
        }

        .calculator {
            background-color: #000;
            border-radius: 50px;
            padding: 20px;
            width: 375px;
        }

        .display {
            background-color: #000;
            color: #fff;
            font-size: 80px;
            text-align: right;
            padding: 20px;
            margin-bottom: 20px;
        }

        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 12px;
        }

        button {
            border: none;
            border-radius: 50%;
            font-size: 40px;
            height: 80px;
            cursor: pointer;
        }

        .number, .decimal {
            background-color: #333;
            color: #fff;
        }

        .operator {
            background-color: #f1a33c;
            color: #fff;
        }

        .function {
            background-color: #a5a5a5;
            color: #000;
        }

        .equals {
            background-color: #f1a33c;
            color: #fff;
        }

        button:active {
            opacity: 0.8;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display">0</div>
        <div class="buttons">
            <button class="function">AC</button>
            <button class="function">+/-</button>
            <button class="function">%</button>
            <button class="operator">÷</button>
            <button class="number">7</button>
            <button class="number">8</button>
            <button class="number">9</button>
            <button class="operator">x</button>
            <button class="number">4</button>
            <button class="number">5</button>
            <button class="number">6</button>
            <button class="operator">-</button>
            <button class="number">1</button>
            <button class="number">2</button>
            <button class="number">3</button>
            <button class="operator">+</button>
            <button class="number" style="grid-column: span 1/4;">0</button>
            <button class="decimal">.</button>
            <button class="equals">=</button>
        </div>
    </div>

    <script>
        const display = document.querySelector('.display');
        const buttons = document.querySelectorAll('button');

        let currentValue = '0';
        let previousValue = null;
        let operation = null;
        let shouldResetDisplay = false;

        buttons.forEach(button => {
            button.addEventListener('click', () => {
                const buttonValue = button.textContent;

                if (button.classList.contains('number')) {
                    handleNumber(buttonValue);
                } else if (button.classList.contains('operator')) {
                    handleOperator(buttonValue);
                } else if (button.classList.contains('function')) {
                    handleFunction(buttonValue);
                } else if (button.classList.contains('decimal')) {
                    handleDecimal();
                } else if (button.classList.contains('equals')) {
                    handleEquals();
                }

                updateDisplay();
            });
        });

        function handleNumber(num) {
            if (currentValue === '0' || shouldResetDisplay) {
                currentValue = num;
                shouldResetDisplay = false;
            } else {
                currentValue += num;
            }
        }

        function handleOperator(op) {
            if (operation !== null) handleEquals();
            previousValue = currentValue;
            operation = op;
            shouldResetDisplay = true;
        }

        function handleFunction(func) {
            switch (func) {
                case 'AC':
                    currentValue = '0';
                    previousValue = null;
                    operation = null;
                    break;
                case '+/-':
                    currentValue = (parseFloat(currentValue) * -1).toString();
                    break;
                case '%':
                    currentValue = (parseFloat(currentValue) / 100).toString();
                    break;
            }
        }

        function handleDecimal() {
            if (!currentValue.includes('.')) {
                currentValue += '.';
            }
        }

        function handleEquals() {
            if (operation === null || previousValue === null) return;

            const prev = parseFloat(previousValue);
            const current = parseFloat(currentValue);

            switch (operation) {
                case '+':
                    currentValue = (prev + current).toString();
                    break;
                case '-':
                    currentValue = (prev - current).toString();
                    break;
                case '×':
                    currentValue = (prev * current).toString();
                    break;
                case '÷':
                    currentValue = (prev / current).toString();
                    break;
            }

            operation = null;
            previousValue = null;
        }

        function updateDisplay() {
            display.textContent = currentValue;
        }
    </script>
</body>
</html>


