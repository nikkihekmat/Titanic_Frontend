---
toc: true
comments: false
layout: post
title: Titanic Survival Prediction
courses: { compsci: {week: 26} }
type: hacks
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Titanic Survival Prediction</title>
<style>
    @import url('https://fonts.googleapis.com/css2?family=Lobster&display=swap');
    body {
        font-family: 'Arial', sans-serif;
        background-color: #ADD8E6; /* Light blue background */
        margin: 0;
        padding: 0;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
    }
    .container {
        background-color: #ADD8E6; /* Light blue container */
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        width: 300px;
    }
    h2 {
        text-align: center;
        color: #0E1621; /* Dark blue text */
        margin-bottom: 20px; /* Add some spacing */
        font-family: 'Lobster', cursive; /* Fun font for title */
    }
    form {
        display: flex;
        flex-direction: column;
    }
    label {
        margin-top: 10px;
        color: #0E1621; /* Dark blue text */
        font-family: 'Comic Sans MS', cursive; /* Fun font for subtitle */
    }
    input, select, button {
        padding: 10px;
        margin-top: 5px;
        border: 2px solid #0E1621; /* Thicker dark blue border */
        border-radius: 4px;
        color: #0E1621; /* Dark blue text */
    }
    input::placeholder {
        color: #0E1621; /* Dark blue placeholder */
        opacity: 1; /* Full opacity */
    }
    button {
        background-color: #0E1621; /* Dark blue button */
        color: #F5F5DC; /* Beige text */
        margin-top: 20px;
    }
    button:hover {
        background-color: #1D2A38; /* Darker blue on hover */
    }
    #predictionResult {
        margin-top: 20px;
        text-align: center;
        padding: 10px;
        background-color: #0E1621; /* Dark blue result background */
        color: #F5F5DC; /* Beige result text */
        border-radius: 4px;
        display: none;
    }
</style>

</head>
<body>
    <div class="container">
        <h2>Titanic Survival Predictor</h2>
        <form id="predictionForm">
            <label for="pclass">Class:</label>
            <select id="pclass">
                <option value="1">1st Class</option>
                <option value="2" selected>2nd Class</option>
                <option value="3">3rd Class</option>
            </select>
            <label for="sex">Sex:</label>
            <select id="sex">
                <option value="1">Male</option>
                <option value="0">Female</option>
            </select>
            <label for="age">Age:</label>
            <input type="number" id="age" placeholder="Age" required>
            <label for="sibsp">Siblings/Spouses Aboard:</label>
            <input type="number" id="sibsp" placeholder="Siblings/Spouses" required>
            <label for="parch">Parents/Children Aboard:</label>
            <input type="number" id="parch" placeholder="Parents/Children" required>
            <label for="fare">Fare:</label>
            <input type="number" step="0.01" id="fare" placeholder="Ticket Fare" required>
            <label for="alone">Traveling Alone:</label>
            <input type="checkbox" id="alone">
            <label for="embarked">Embarked From:</label>
            <select id="embarked">
                <option value="S">Southampton</option>
                <option value="C">Cherbourg</option>
                <option value="Q">Queenstown</option>
            </select>
            <button type="submit">Predict Survival</button>
        </form>
        <div id="predictionResult"></div>
    </div>
    <script>
        document.getElementById('predictionForm').onsubmit = async function(e) {
            e.preventDefault();
            const formData = {
                pclass: document.getElementById('pclass').value,
                sex: document.getElementById('sex').value,
                age: document.getElementById('age').value,
                sibsp: document.getElementById('sibsp').value,
                parch: document.getElementById('parch').value,
                fare: document.getElementById('fare').value,
                alone: document.getElementById('alone').checked ? 1 : 0,
                embarked: document.getElementById('embarked').value
            };
            const response = await fetch('ttp://127.0.0.1:8086/api/titanic/predict', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(formData),
            });
            const result = await response.json();
            const resultDiv = document.getElementById('predictionResult');
            resultDiv.style.display = 'block';
            resultDiv.innerText = `Survival Probability: ${result['LogisticRegression Survival Probability']}%`;
        };
    </script>
</body>
</html>


