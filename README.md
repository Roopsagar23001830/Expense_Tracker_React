# Expense Tracker (ReactJS)
## Date: 24-05-2025

## AIM
To develop a simple Expense Tracker application using React that allows users to manage their personal finances by adding, viewing, and deleting income and expense transactions, while dynamically calculating the current balance, total income, and total expenses.

## ALGORITHM
### STEP 1: Initialize the Project
Create a new React app using:

npx create-react-app expense-tracker
or

npm create vite@latest expense-tracker --template react

Open the project in a code editor like VS Code.

### Step 2: Setup State
Define a state variable to store transactions:

Example: const [transactions, setTransactions] = useState([])

Define state variables for the form inputs:

const [text, setText] = useState("")

const [amount, setAmount] = useState("")

### Step 3: Add a New Transaction
Create a form with two inputs:

Text input for description

Number input for amount

On form submit:

Validate input

Create a new transaction object

Add the object to the transactions array using setTransactions.

### Step 4: Display Transaction List

Use map() to render each transaction in a list.

Conditionally style each item based on amount > 0 (income) or amount < 0 (expense).

Add a delete button next to each transaction.

### Step 5: Calculate and Display Summary

Use reduce() to calculate:

Total Balance: sum of all amounts

Total Income: sum of all positive amounts

Total Expenses: sum of all negative amounts

Display these values at the top of the UI.

### Step 6: Delete a Transaction

When delete is clicked:

Use filter() to remove the transaction from the array by id.

Update the state using setTransactions.

### Step 7: Style the Application

Use basic CSS to style:

Balance summary

Income/expense totals

Form inputs

Transaction list (with color coding)

## PROGRAM

app.js
```
import React, { useState } from 'react';
import './App.css';

function App() {
  const [transactions, setTransactions] = useState([]);
  const [text, setText] = useState('');
  const [amount, setAmount] = useState('');

  const addTransaction = (e) => {
    e.preventDefault();
    if (!text || !amount) return;

    const newTransaction = {
      id: Date.now(),
      text,
      amount: parseFloat(amount),
    };

    setTransactions([newTransaction, ...transactions]);
    setText('');
    setAmount('');
  };

  const deleteTransaction = (id) => {
    setTransactions(transactions.filter((tx) => tx.id !== id));
  };

  const balance = transactions.reduce((acc, tx) => acc + tx.amount, 0);
  const income = transactions.filter(tx => tx.amount > 0).reduce((acc, tx) => acc + tx.amount, 0);
  const expense = transactions.filter(tx => tx.amount < 0).reduce((acc, tx) => acc + tx.amount, 0);

  return (
    <div className="app-container">
      <header>
        <h1> Expense Vault</h1>
      </header>

      <div className="cards">
        <div className="card">
          <p>Total Balance</p>
          <h2>₹{balance.toFixed(2)}</h2>
        </div>
        <div className="card income">
          <p>Income</p>
          <h3 className="green">+₹{income.toFixed(2)}</h3>
        </div>
        <div className="card expense">
          <p>Expense</p>
          <h3 className="red">-₹{Math.abs(expense).toFixed(2)}</h3>
        </div>
      </div>

      <form className="transaction-form" onSubmit={addTransaction}>
        <input 
          type="text" 
          placeholder="eg. Chocolate Milkshake 🥤" 
          value={text} 
          onChange={(e) => setText(e.target.value)} 
        />
        <input 
          type="number" 
          placeholder="eg. -90 or +200" 
          value={amount} 
          onChange={(e) => setAmount(e.target.value)} 
        />
        <button type="submit">✨ Add Entry</button>
      </form>

      <ul className="transaction-list">
        {transactions.map((tx) => (
          <li key={tx.id} className={tx.amount >= 0 ? 'plus' : 'minus'}>
            {tx.text}
            <span>₹{tx.amount}</span>
            <button onClick={() => deleteTransaction(tx.id)}>❌</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
```
app.css

```
body {
  margin: 0;
  font-family: 'Poppins', sans-serif;
  background: #fff0f6;
}

.app-container {
  max-width: 480px;
  margin: 40px auto;
  padding: 20px;
  background: #ffffff;
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.08);
}

header h1 {
  text-align: center;
  background: linear-gradient(to right, #f06292, #ec407a);
  color: white;
  padding: 16px;
  border-radius: 12px;
  margin-bottom: 24px;
}

.cards {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 24px;
}

.card {
  flex: 1;
  background: #fce4ec;
  padding: 14px;
  border-radius: 8px;
  text-align: center;
  box-shadow: 0 4px 8px rgba(0,0,0,0.05);
}

.card.income {
  background: #e0f7fa;
}

.card.expense {
  background: #ffebee;
}

.green {
  color: green;
}
.red {
  color: crimson;
}

.transaction-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
}

.transaction-form input {
  padding: 12px;
  border-radius: 6px;
  border: 1px solid #ccc;
}

.transaction-form button {
  background: #e91e63;
  color: white;
  padding: 12px;
  border: none;
  border-radius: 6px;
  font-weight: bold;
  cursor: pointer;
  transition: 0.3s;
}

.transaction-form button:hover {
  background: #c2185b;
}

.transaction-list {
  list-style: none;
  padding: 0;
}

.transaction-list li {
  background: #f9f9f9;
  padding: 12px;
  margin-bottom: 10px;
  display: flex;
  justify-content: space-between;
  border-left: 6px solid;
  border-radius: 6px;
  box-shadow: 0 2px 4px rgba(0,0,0,0.05);
}

.transaction-list li.plus {
  border-color: green;
}
.transaction-list li.minus {
  border-color: crimson;
}

.transaction-list button {
  background: none;
  border: none;
  font-size: 18px;
  cursor: pointer;
}
```

## OUTPUT

![image](https://github.com/user-attachments/assets/489fb292-b3ff-4447-a42b-c6e2fda63566)

## RESULT
A fully functional React-based Expense Tracker application was successfully developed. 
