# react-calculator
import { useState } from 'react';

export default function Calculator() {
  const [display, setDisplay] = useState('0');
  const [firstOperand, setFirstOperand] = useState(null);
  const [operator, setOperator] = useState(null);
  const [waitingForSecondOperand, setWaitingForSecondOperand] = useState(false);

  const inputDigit = (digit) => {
    if (waitingForSecondOperand) {
      setDisplay(String(digit));
      setWaitingForSecondOperand(false);
    } else {
      setDisplay(display === '0' ? String(digit) : display + digit);
    }
  };

  const inputDecimal = () => {
    if (waitingForSecondOperand) {
      setDisplay('0.');
      setWaitingForSecondOperand(false);
      return;
    }

    if (!display.includes('.')) {
      setDisplay(display + '.');
    }
  };

  const clearDisplay = () => {
    setDisplay('0');
    setFirstOperand(null);
    setOperator(null);
    setWaitingForSecondOperand(false);
  };

  const performOperation = (nextOperator) => {
    const inputValue = parseFloat(display);

    if (firstOperand === null) {
      setFirstOperand(inputValue);
    } else if (operator) {
      const result = calculate(firstOperand, inputValue, operator);
      setDisplay(String(result));
      setFirstOperand(result);
    }

    setWaitingForSecondOperand(true);
    setOperator(nextOperator);
  };

  const calculate = (firstOperand, secondOperand, operator) => {
    switch (operator) {
      case '+':
        return firstOperand + secondOperand;
      case '-':
        return firstOperand - secondOperand;
      case '*':
        return firstOperand * secondOperand;
      case '÷':
        return firstOperand / secondOperand;
      default:
        return secondOperand;
    }
  };

  return (
    <div className="flex flex-col items-center justify-center p-4 bg-gray-100 rounded-lg shadow-lg">
      <div className="w-64 mb-4">
        <div className="w-full p-2 mb-4 text-right bg-white rounded shadow text-2xl font-bold">
          {display}
        </div>
        <div className="grid grid-cols-4 gap-2">
          <button 
            className="p-2 bg-gray-200 hover:bg-gray-300 text-lg font-medium rounded"
            onClick={clearDisplay}
          >
            AC
          </button>
          <button 
            className="p-2 bg-gray-200 hover:bg-gray-300 text-lg font-medium rounded"
            onClick={() => setDisplay(String(parseFloat(display) * -1))}
          >
            +/-
          </button>
          <button 
            className="p-2 bg-gray-200 hover:bg-gray-300 text-lg font-medium rounded"
            onClick={() => setDisplay(String(parseFloat(display) / 100))}
          >
            %
          </button>
          <button 
            className="p-2 bg-orange-400 hover:bg-orange-500 text-white text-lg font-medium rounded"
            onClick={() => performOperation('÷')}
          >
            ÷
          </button>

          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(7)}
          >
            7
          </button>
          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(8)}
          >
            8
          </button>
          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(9)}
          >
            9
          </button>
          <button 
            className="p-2 bg-orange-400 hover:bg-orange-500 text-white text-lg font-medium rounded"
            onClick={() => performOperation('*')}
          >
            ×
          </button>

          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(4)}
          >
            4
          </button>
          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(5)}
          >
            5
          </button>
          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(6)}
          >
            6
          </button>
          <button 
            className="p-2 bg-orange-400 hover:bg-orange-500 text-white text-lg font-medium rounded"
            onClick={() => performOperation('-')}
          >
            -
          </button>

          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(1)}
          >
            1
          </button>
          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(2)}
          >
            2
          </button>
          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(3)}
          >
            3
          </button>
          <button 
            className="p-2 bg-orange-400 hover:bg-orange-500 text-white text-lg font-medium rounded"
            onClick={() => performOperation('+')}
          >
            +
          </button>

          <button 
            className="col-span-2 p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={() => inputDigit(0)}
          >
            0
          </button>
          <button 
            className="p-2 bg-gray-300 hover:bg-gray-400 text-lg font-medium rounded"
            onClick={inputDecimal}
          >
            .
          </button>
          <button 
            className="p-2 bg-orange-400 hover:bg-orange-500 text-white text-lg font-medium rounded"
            onClick={() => performOperation('=')}
          >
            =
          </button>
        </div>
      </div>
    </div>
  );
}
