# Project 2: Calculator — Solution

## File Structure

```
calculator/
├── calculator.html
├── calc-style.css
└── calc.js
```

## calculator.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculator</title>
  <link rel="stylesheet" href="calc-style.css">
</head>
<body>
  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="btn number" data-value="7">7</button>
      <button class="btn number" data-value="8">8</button>
      <button class="btn number" data-value="9">9</button>
      <button class="btn operator" data-value="/">÷</button>

      <button class="btn number" data-value="4">4</button>
      <button class="btn number" data-value="5">5</button>
      <button class="btn number" data-value="6">6</button>
      <button class="btn operator" data-value="*">×</button>

      <button class="btn number" data-value="1">1</button>
      <button class="btn number" data-value="2">2</button>
      <button class="btn number" data-value="3">3</button>
      <button class="btn operator" data-value="-">−</button>

      <button class="btn number" data-value="0">0</button>
      <button class="btn number" data-value=".">.</button>
      <button class="btn clear" id="clear">C</button>
      <button class="btn operator" data-value="+">+</button>

      <button class="btn equals" id="equals">=</button>
    </div>
  </div>
  <script src="calc.js"></script>
</body>
</html>
```

## calc-style.css

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #1a1a1a;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
}

.calculator {
  background: #2d2d2d;
  border-radius: 16px;
  padding: 20px;
  box-shadow: 0 10px 40px rgba(0,0,0,0.5);
  width: 320px;
}

.display {
  background: #1a1a1a;
  color: white;
  font-size: 2.5rem;
  text-align: right;
  padding: 20px 15px;
  border-radius: 10px;
  margin-bottom: 15px;
  font-family: 'Courier New', monospace;
  overflow: hidden;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}

.btn {
  padding: 20px;
  font-size: 1.3rem;
  border: none;
  border-radius: 10px;
  cursor: pointer;
  transition: all 0.15s;
  font-weight: 500;
}

.btn:hover {
  opacity: 0.85;
  transform: scale(1.02);
}

.btn:active {
  transform: scale(0.95);
}

.number {
  background: #3d3d3d;
  color: white;
}

.operator {
  background: #ff9500;
  color: white;
}

.clear {
  background: #a5a5a5;
  color: black;
}

.equals {
  background: #ff9500;
  color: white;
  grid-column: span 2;
}
```

## calc.js

```javascript
// ─── State ───
let currentValue = '0';
let previousValue = null;
let operation = null;
let shouldResetDisplay = false;

// ─── DOM References ───
const display = document.getElementById('display');

// ─── Number Buttons ───
document.querySelectorAll('.number').forEach(btn => {
  btn.addEventListener('click', () => {
    const value = btn.dataset.value;

    if (shouldResetDisplay) {
      currentValue = value === '.' ? '0.' : value;
      shouldResetDisplay = false;
    } else {
      if (value === '.' && currentValue.includes('.')) return;
      if (currentValue === '0' && value !== '.') {
        currentValue = value;
      } else {
        currentValue += value;
      }
    }

    display.textContent = currentValue;
  });
});

// ─── Operator Buttons ───
document.querySelectorAll('.operator').forEach(btn => {
  btn.addEventListener('click', () => {
    const current = parseFloat(currentValue);

    if (previousValue !== null && !shouldResetDisplay) {
      previousValue = calculate(previousValue, current, operation);
      display.textContent = previousValue;
    } else {
      previousValue = current;
    }

    operation = btn.dataset.value;
    shouldResetDisplay = true;
  });
});

// ─── Equals Button ───
document.getElementById('equals').addEventListener('click', () => {
  if (previousValue === null || operation === null) return;

  const current = parseFloat(currentValue);
  const result = calculate(previousValue, current, operation);

  display.textContent = result;
  currentValue = result.toString();
  previousValue = null;
  operation = null;
  shouldResetDisplay = true;
});

// ─── Clear Button ───
document.getElementById('clear').addEventListener('click', () => {
  currentValue = '0';
  previousValue = null;
  operation = null;
  shouldResetDisplay = false;
  display.textContent = '0';
});

// ─── Calculate Helper ───
function calculate(a, b, op) {
  switch (op) {
    case '+': return a + b;
    case '-': return a - b;
    case '*': return a * b;
    case '/':
      if (b === 0) return 'Error';
      return a / b;
    default: return b;
  }
}
```
