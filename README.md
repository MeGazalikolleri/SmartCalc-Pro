<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
  <title>SmartCalcPro</title>
  <!-- Anek Malayalam Font from Google Fonts -->
  <link href="https://fonts.googleapis.com/css2?family=Anek+Malayalam:wght@100;200;300;400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      user-select: none;
    }

    body {
      background: linear-gradient(145deg, #e8ddd0 0%, #d4c5b5 100%);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      font-family: 'Anek Malayalam', 'Segoe UI', 'Poppins', system-ui, sans-serif;
      padding: 20px;
    }

    /* Main Calculator Container - Pearl White + Soft Peach */
    .calculator {
      background: linear-gradient(145deg, #fff5eb 0%, #ffe8dc 100%);
      border-radius: 48px;
      box-shadow: 0 30px 45px rgba(0, 0, 0, 0.12), inset 0 1px 2px rgba(255, 255, 255, 0.8);
      padding: 28px 24px 32px 24px;
      width: 100%;
      max-width: 620px;
      transition: all 0.2s ease;
      border: 1px solid rgba(255, 235, 215, 0.9);
    }

    /* Display Section - Pearl Finish */
    .display-panel {
      background: #fef7f0;
      border-radius: 32px;
      padding: 20px 24px;
      margin-bottom: 28px;
      box-shadow: inset 0 2px 6px rgba(0, 0, 0, 0.05), 0 3px 8px rgba(255, 245, 235, 0.8);
      border: 1px solid #ffebe0;
    }

    .mode-indicators {
      display: flex;
      gap: 12px;
      margin-bottom: 12px;
      font-size: 0.7rem;
      font-weight: 700;
      letter-spacing: 0.5px;
      color: #c47a5a;
      border-bottom: 2px solid #ffd9c4;
      padding-bottom: 8px;
      flex-wrap: wrap;
    }

    .mode-badge {
      background: #ffded0;
      padding: 4px 12px;
      border-radius: 24px;
      font-family: 'Anek Malayalam', monospace;
      color: #b25d3a;
      font-weight: 700;
      font-size: 0.7rem;
    }

    .previous-operand {
      min-height: 36px;
      font-size: 1rem;
      color: #b87a5a;
      text-align: right;
      word-wrap: break-word;
      word-break: break-word;
      font-weight: 500;
      letter-spacing: 0.3px;
      font-family: 'Anek Malayalam', monospace;
    }

    .current-operand {
      font-size: 3.2rem;
      font-weight: 700;
      color: #6d3b20;
      text-align: right;
      word-wrap: break-word;
      word-break: break-word;
      line-height: 1.2;
      margin-top: 6px;
      font-family: 'Anek Malayalam', monospace;
      letter-spacing: 1px;
    }

    /* Buttons Grid */
    .buttons-grid {
      display: grid;
      grid-template-columns: repeat(5, 1fr);
      gap: 12px;
      margin-bottom: 14px;
    }

    /* Universal Button Style - Soft Peach & Pearl */
    button {
      border: none;
      border-radius: 28px;
      padding: 16px 0;
      font-size: 1.2rem;
      font-weight: 700;
      cursor: pointer;
      transition: all 0.08s linear;
      box-shadow: 0 4px 0 #deb887;
      font-family: 'Anek Malayalam', sans-serif;
      letter-spacing: 0.4px;
      display: flex;
      align-items: center;
      justify-content: center;
      background: #fff5ed;
      color: #8b5a3e;
    }

    button:active {
      transform: translateY(2px);
      box-shadow: 0 2px 0 #deb887;
    }

    /* Zero key spanning two columns */
    .zero-span {
      grid-column: span 2;
    }

    /* Special Function Categories - Peach Tones */
    .fn-math {
      background: #ffede3;
      color: #b25d3a;
      box-shadow: 0 4px 0 #e6c3aa;
    }

    .fn-advanced {
      background: #fff0e6;
      color: #c27a56;
      box-shadow: 0 4px 0 #e6c3aa;
    }

    .operator {
      background: #ffd9c4;
      color: #9b5a3a;
      font-size: 1.6rem;
      font-weight: 800;
      box-shadow: 0 4px 0 #d4a882;
    }

    .equals {
      background: #ffc9ad;
      color: #8b4a2a;
      font-size: 1.8rem;
      font-weight: 800;
      box-shadow: 0 4px 0 #d49c6c;
      background: linear-gradient(145deg, #ffcdb0, #ffc2a0);
    }

    .clear-btn {
      background: #ffd1bc;
      color: #b84a2a;
      font-weight: bold;
      box-shadow: 0 4px 0 #d49870;
    }

    .delete-btn {
      background: #ffd9c4;
      color: #b85a32;
      font-weight: bold;
      box-shadow: 0 4px 0 #d4a070;
    }

    .memory {
      background: #ffe8dc;
      color: #b56a42;
      border: 1px solid #ffd9c4;
      box-shadow: 0 4px 0 #e0bea0;
    }

    .number-btn {
      background: #fffaf5;
      color: #8b5a3e;
      box-shadow: 0 4px 0 #e6cfbc;
    }

    /* Branding */
    .brand {
      text-align: center;
      margin-top: 20px;
      font-size: 0.8rem;
      font-weight: 700;
      color: #c47a5a;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      font-family: 'Anek Malayalam', monospace;
      text-shadow: 0 1px 0 #fff0e6;
    }

    /* Responsive */
    @media (max-width: 580px) {
      .calculator {
        padding: 20px 16px 24px;
      }
      .buttons-grid {
        gap: 8px;
      }
      button {
        padding: 12px 0;
        font-size: 1rem;
      }
      .current-operand {
        font-size: 2.2rem;
      }
      .operator {
        font-size: 1.4rem;
      }
    }

    @media (hover: hover) {
      button:hover {
        filter: brightness(0.97);
        transform: scale(0.97);
      }
      button:active {
        transform: translateY(2px);
      }
    }
  </style>
</head>
<body>
<div class="calculator">
  <div class="display-panel">
    <div class="mode-indicators">
      <span class="mode-badge">● Natural-Upam</span>
      <span class="mode-badge">Equation</span>
      <span class="mode-badge">Base-N</span>
      <span class="mode-badge">Complex</span>
      <span class="mode-badge">Matrix</span>
    </div>
    <div class="previous-operand" id="previousOperand"></div>
    <div class="current-operand" id="currentOperand">0</div>
  </div>

  <!-- First Block: Core Functions -->
  <div class="buttons-grid">
    <button class="fn-math" data-action="table">Table</button>
    <button class="fn-math" data-action="equations">Equations</button>
    <button class="fn-advanced" data-action="percent">%</button>
    <button class="fn-advanced" data-action="base-n">Base-N</button>
    <button class="clear-btn" data-action="clear">Ac</button>
    
    <!-- Row 2 -->
    <button class="number-btn" data-number="7">7</button>
    <button class="number-btn" data-number="8">8</button>
    <button class="number-btn" data-number="9">9</button>
    <button class="operator" data-operator="/">÷</button>
    <button class="delete-btn" data-action="delete">Del</button>
    
    <!-- Row 3 -->
    <button class="number-btn" data-number="4">4</button>
    <button class="number-btn" data-number="5">5</button>
    <button class="number-btn" data-number="6">6</button>
    <button class="operator" data-operator="*">×</button>
    <button class="fn-advanced" data-action="sqrt">√</button>
    
    <!-- Row 4 -->
    <button class="number-btn" data-number="1">1</button>
    <button class="number-btn" data-number="2">2</button>
    <button class="number-btn" data-number="3">3</button>
    <button class="operator" data-operator="-">−</button>
    <button class="fn-advanced" data-action="power">Xʸ</button>
    
    <!-- Row 5: Zero spans 2 columns -->
    <button class="number-btn zero-span" data-number="0">0</button>
    <button class="number-btn" data-number=".">.</button>
    <button class="operator" data-operator="+">+</button>
    <button class="equals" data-action="equals">=</button>
  </div>

  <!-- Second Grid: Extra Commercial & Scientific Functions -->
  <div class="buttons-grid">
    <button class="fn-math" data-action="mod">Mod</button>
    <button class="fn-math" data-action="reciprocal">Reciprocal</button>
    <button class="fn-math" data-action="square">Square</button>
    <button class="fn-math" data-action="round">Round</button>
    <button class="fn-math" data-action="floor">Floor</button>
    
    <button class="fn-advanced" data-action="ceil">Ceil</button>
    <button class="fn-advanced" data-action="factorial">Factorial</button>
    <button class="fn-advanced" data-action="log">Log</button>
    <button class="fn-advanced" data-action="ln">Ln</button>
    <button class="fn-advanced" data-action="exp">Exp</button>
    
    <button class="memory" data-action="m-plus">M+</button>
    <button class="memory" data-action="m-minus">M-</button>
    <button class="memory" data-action="mr">Mr</button>
    <button class="memory" data-action="mc">Mc</button>
    <button class="fn-advanced" data-action="cube">X³</button>
    
    <button class="fn-advanced" data-action="paren-open">(</button>
    <button class="fn-advanced" data-action="paren-close">)</button>
    <button class="fn-advanced" data-action="plusminus">±</button>
    <button class="fn-advanced" data-action="ten-power">10ˣ</button>
    <button class="fn-advanced" data-action="pi">π</button>
  </div>

  <!-- Third Extra Row: Ans, Fraction, Sci, Eng, Fix -->
  <div class="buttons-grid">
    <button class="fn-math" data-action="ans">Ans</button>
    <button class="fn-math" data-action="frac">a b/c</button>
    <button class="fn-advanced" data-action="scientific">Sci</button>
    <button class="fn-advanced" data-action="eng">Eng</button>
    <button class="memory" data-action="fix">Fix</button>
  </div>

  <div class="brand">⚡SmartCalc-Pro⚡</div>
</div>

<script>
  // ----------------------------------------------
  // SmartCalc-Pro
  // Zero key spans 2 columns (standard calculator layout)
  // Full commercial features, Anek Malayalam font
  // ----------------------------------------------

  let expression = "";
  let justEvaluated = false;
  let memory = 0;
  let lastAnswer = 0;

  const previousOperandElem = document.getElementById('previousOperand');
  const currentOperandElem = document.getElementById('currentOperand');

  function updateDisplay() {
    if (expression === "Error" || expression === "Infinity" || expression === "NaN") {
      currentOperandElem.innerText = expression;
      previousOperandElem.innerText = "";
      return;
    }
    
    if (justEvaluated && expression !== "") {
      currentOperandElem.innerText = formatNumber(expression);
      previousOperandElem.innerText = "";
    } else {
      let disp = expression === "" ? "0" : expression;
      currentOperandElem.innerText = formatExpressionDisplay(disp);
      previousOperandElem.innerText = "";
    }
  }

  function formatExpressionDisplay(expr) {
    return expr.replace(/\*/g, '×').replace(/\//g, '÷').replace(/\^/g, '^');
  }

  function formatNumber(numStr) {
    let num = parseFloat(numStr);
    if (isNaN(num)) return "0";
    if (!isFinite(num)) return numStr;
    if (Math.abs(num) > 1e12 || (Math.abs(num) < 1e-8 && num !== 0)) {
      return num.toExponential(8);
    }
    let formatted = num.toLocaleString('en-US', { maximumFractionDigits: 10, useGrouping: false });
    return formatted;
  }

  function evaluateExpression(expr) {
    if (expr.trim() === "") return "0";
    let mathExpr = expr.replace(/×/g, '*').replace(/÷/g, '/');
    mathExpr = mathExpr.replace(/\^/g, '**');
    mathExpr = mathExpr.replace(/mod/g, '%');
    mathExpr = mathExpr.replace(/ans/gi, lastAnswer.toString());
    
    mathExpr = mathExpr.replace(/(\d+(?:\.\d+)?|\))(!)/g, (match, num) => {
      let n = parseFloat(num);
      if (isNaN(n) || n < 0 || !Number.isInteger(n)) return "NaN";
      let fact = 1;
      for (let i = 2; i <= n; i++) fact *= i;
      return fact;
    });
    
    mathExpr = mathExpr.replace(/sqrt\(/g, 'Math.sqrt(');
    mathExpr = mathExpr.replace(/log\(/g, 'Math.log10(');
    mathExpr = mathExpr.replace(/ln\(/g, 'Math.log(');
    mathExpr = mathExpr.replace(/exp\(/g, 'Math.exp(');
    mathExpr = mathExpr.replace(/floor\(/g, 'Math.floor(');
    mathExpr = mathExpr.replace(/ceil\(/g, 'Math.ceil(');
    mathExpr = mathExpr.replace(/round\(/g, 'Math.round(');
    mathExpr = mathExpr.replace(/tenpow\(/g, 'Math.pow(10,');
    mathExpr = mathExpr.replace(/π/g, 'Math.PI');
    
    try {
      const evaluated = Function('"use strict"; return (' + mathExpr + ')')();
      if (isNaN(evaluated)) throw new Error("NaN");
      if (!isFinite(evaluated)) return evaluated === Infinity ? "Infinity" : "-Infinity";
      let rounded = parseFloat(evaluated.toFixed(10));
      if (Math.abs(rounded) < 1e-10 && rounded !== 0) rounded = 0;
      return rounded.toString();
    } catch (err) {
      console.error(err);
      return "Error";
    }
  }

  function appendToExpression(value) {
    if (justEvaluated) {
      expression = "";
      justEvaluated = false;
    }
    if (expression === "0" && !isNaN(value) && value !== ".") {
      expression = value;
    } else {
      expression += value;
    }
    updateDisplay();
  }

  function clearAll() {
    expression = "";
    justEvaluated = false;
    updateDisplay();
  }

  function deleteLast() {
    if (justEvaluated) {
      clearAll();
      return;
    }
    expression = expression.slice(0, -1);
    updateDisplay();
  }

  function computeResult() {
    if (expression.trim() === "") {
      expression = "0";
      updateDisplay();
      return;
    }
    let result = evaluateExpression(expression);
    if (result === "Error") {
      expression = "Error";
    } else {
      lastAnswer = parseFloat(result);
      expression = result;
      justEvaluated = true;
    }
    updateDisplay();
  }

  function recallAns() {
    if (justEvaluated) justEvaluated = false;
    appendToExpression(lastAnswer.toString());
  }

  function fractionInput() {
    appendToExpression('/');
  }

  let sciMode = false;
  function toggleScientific() {
    sciMode = !sciMode;
    if (expression !== "" && !justEvaluated) {
      let val = parseFloat(evaluateExpression(expression));
      if (!isNaN(val)) {
        if (sciMode) {
          currentOperandElem.innerText = val.toExponential(6);
        } else {
          updateDisplay();
        }
      }
    }
    updateDisplay();
  }
  
  function engFormat() {
    let val = parseFloat(expression);
    if (!isNaN(val) && expression !== "") {
      let eng = val.toExponential(6).replace(/e\+?(\d+)/, (m, exp) => {
        let e = parseInt(exp);
        return `e${e}`;
      });
      currentOperandElem.innerText = eng;
      setTimeout(() => updateDisplay(), 800);
    }
  }
  
  function fixDecimal() {
    let val = parseFloat(expression);
    if (!isNaN(val)) {
      let fixed = val.toFixed(4);
      expression = fixed;
      justEvaluated = false;
      updateDisplay();
    }
  }

  function applyUnaryOp(opName, mathFn, needsParen = true) {
    if (justEvaluated && expression !== "" && !isNaN(parseFloat(expression))) {
      let val = parseFloat(expression);
      let res = mathFn(val);
      expression = res.toString();
      justEvaluated = false;
      updateDisplay();
      return;
    }
    let exprCore = expression === "" ? "0" : expression;
    if (needsParen) {
      expression = `${opName}(${exprCore})`;
    } else {
      expression = `${opName}${exprCore}`;
    }
    updateDisplay();
  }

  function applyBinaryWrapper(symbol) {
    if (justEvaluated) justEvaluated = false;
    appendToExpression(symbol);
  }

  function applyFactorial() {
    if (justEvaluated) justEvaluated = false;
    appendToExpression('!');
  }

  function applyPercent() {
    if (justEvaluated && expression !== "") {
      let val = parseFloat(expression);
      if (!isNaN(val)) {
        expression = (val / 100).toString();
        justEvaluated = false;
        updateDisplay();
      }
      return;
    }
    const lastNumMatch = expression.match(/(\d+(?:\.\d+)?|\.\d+)(?!.*\d)/);
    if (lastNumMatch) {
      let num = lastNumMatch[1];
      let start = lastNumMatch.index;
      let percentVal = `(${num}/100)`;
      let newExpr = expression.slice(0, start) + percentVal + expression.slice(start + num.length);
      expression = newExpr;
    } else {
      expression = `(${expression || '0'}/100)`;
    }
    updateDisplay();
  }

  function togglePlusMinus() {
    if (justEvaluated && expression !== "") {
      let num = parseFloat(expression);
      if (!isNaN(num)) {
        expression = (-num).toString();
        justEvaluated = false;
        updateDisplay();
      }
      return;
    }
    const lastMatch = expression.match(/(\d+(?:\.\d+)?|\.\d+)(?!.*\d)/);
    if (lastMatch) {
      let lastNum = lastMatch[1];
      let idx = lastMatch.index;
      let negNum = (parseFloat(lastNum) * -1).toString();
      expression = expression.slice(0, idx) + negNum + expression.slice(idx + lastNum.length);
    } else {
      expression = "-(" + (expression || "0") + ")";
    }
    updateDisplay();
  }

  function memoryPlus() {
    let val = expression === "" ? 0 : parseFloat(evaluateExpression(expression));
    if (isNaN(val)) val = 0;
    memory += val;
    justEvaluated = true;
    expression = val.toString();
    updateDisplay();
  }
  
  function memoryMinus() {
    let val = expression === "" ? 0 : parseFloat(evaluateExpression(expression));
    if (isNaN(val)) val = 0;
    memory -= val;
    justEvaluated = true;
    expression = val.toString();
    updateDisplay();
  }
  
  function memoryRecall() {
    expression = memory.toString();
    justEvaluated = false;
    updateDisplay();
  }
  
  function memoryClear() {
    memory = 0;
  }

  function tableMode() { appendToExpression("Table("); }
  function equationsMode() { appendToExpression("Solve("); }
  function baseNMode() {
    let val = parseFloat(expression);
    if (isNaN(val)) val = 0;
    let hexVal = "0x" + Math.floor(val).toString(16).toUpperCase();
    expression = hexVal;
    justEvaluated = false;
    updateDisplay();
  }
  
  function tenPower() {
    if (justEvaluated && expression !== "") {
      let val = parseFloat(expression);
      if (!isNaN(val)) {
        expression = Math.pow(10, val).toString();
        justEvaluated = false;
        updateDisplay();
      }
      return;
    }
    expression = `tenpow(${expression || '0'})`;
    updateDisplay();
  }
  
  function insertPi() { appendToExpression("π"); }
  
  function cubeFunction() {
    if (justEvaluated && expression !== "") {
      let val = parseFloat(expression);
      if (!isNaN(val)) {
        expression = (val * val * val).toString();
        justEvaluated = false;
        updateDisplay();
      }
      return;
    }
    expression = `(${expression || '0'})^3`;
    updateDisplay();
  }
  
  function applyLog() { applyUnaryOp("log", Math.log10, true); }
  function applyLn() { applyUnaryOp("ln", Math.log, true); }
  function applyExp() { applyUnaryOp("exp", Math.exp, true); }
  function applySqrt() { applyUnaryOp("sqrt", Math.sqrt, true); }
  function applyReciprocal() { 
    if (justEvaluated && expression !== "") {
      let val = parseFloat(expression);
      if (val !== 0) expression = (1/val).toString();
      else expression = "Error";
      justEvaluated = false;
      updateDisplay();
      return;
    }
    expression = `1/(${expression || '0'})`;
    updateDisplay();
  }
  function applySquare() { 
    if (justEvaluated && expression !== "") {
      let val = parseFloat(expression);
      expression = (val * val).toString();
      justEvaluated = false;
      updateDisplay();
      return;
    }
    expression = `(${expression || '0'})^2`;
    updateDisplay();
  }
  function applyRound() { applyUnaryOp("round", Math.round, true); }
  function applyFloor() { applyUnaryOp("floor", Math.floor, true); }
  function applyCeil() { applyUnaryOp("ceil", Math.ceil, true); }
  function applyPower() { applyBinaryWrapper("^"); }
  function applyMod() { applyBinaryWrapper(" mod "); }
  function addParenOpen() { appendToExpression("("); }
  function addParenClose() { appendToExpression(")"); }

  const actionMap = {
    clear: clearAll,
    delete: deleteLast,
    equals: computeResult,
    percent: applyPercent,
    sqrt: applySqrt,
    power: applyPower,
    cube: cubeFunction,
    mod: applyMod,
    reciprocal: applyReciprocal,
    square: applySquare,
    round: applyRound,
    floor: applyFloor,
    ceil: applyCeil,
    factorial: applyFactorial,
    log: applyLog,
    ln: applyLn,
    exp: applyExp,
    'ten-power': tenPower,
    pi: insertPi,
    'm-plus': memoryPlus,
    'm-minus': memoryMinus,
    mr: memoryRecall,
    mc: memoryClear,
    table: tableMode,
    equations: equationsMode,
    'base-n': baseNMode,
    'paren-open': addParenOpen,
    'paren-close': addParenClose,
    plusminus: togglePlusMinus,
    ans: recallAns,
    frac: fractionInput,
    scientific: toggleScientific,
    eng: engFormat,
    fix: fixDecimal,
  };

  // Attach number buttons
  document.querySelectorAll('[data-number]').forEach(btn => {
    btn.addEventListener('click', () => {
      let num = btn.getAttribute('data-number');
      appendToExpression(num);
    });
  });

  // Attach operator buttons
  document.querySelectorAll('[data-operator]').forEach(btn => {
    btn.addEventListener('click', () => {
      let op = btn.getAttribute('data-operator');
      if (justEvaluated) justEvaluated = false;
      appendToExpression(op);
    });
  });

  // Attach action buttons
  document.querySelectorAll('[data-action]').forEach(btn => {
    btn.addEventListener('click', () => {
      let action = btn.getAttribute('data-action');
      if (actionMap[action]) actionMap[action]();
    });
  });

  // Keyboard support
  window.addEventListener('keydown', (e) => {
    const key = e.key;
    if (!isNaN(key) || key === '.') appendToExpression(key);
    else if (key === '+') appendToExpression('+');
    else if (key === '-') appendToExpression('-');
    else if (key === '*') appendToExpression('*');
    else if (key === '/') appendToExpression('/');
    else if (key === 'Enter' || key === '=') computeResult();
    else if (key === 'Escape') clearAll();
    else if (key === 'Backspace') deleteLast();
    else if (key === '%') applyPercent();
    else if (key === '^') applyPower();
  });

  updateDisplay();
</script>
</body>
</html>
