<!DOCTYPE html>
<html>
<head>
    <title>Titanic Survival Prediction</title>
</head>
<body>
    <h1>Titanic Survival Prediction</h1>
    <form id="predictionForm">
        <label for="age">Age:</label>
        <input type="text" id="age" name="age"><br><br>
        <!-- Other input fields go here -->
        <button type="submit">Predict</button>
    </form>
    <div id="predictionResult"></div>
    <script>
        document.getElementById('predictionForm').addEventListener('submit', function(event) {
            event.preventDefault();
            const formData = new FormData(this);
            fetch('/predict', {
                method: 'POST',
                body: JSON.stringify(Object.fromEntries(formData)),
                headers: {
                    'Content-Type': 'application/json'
                }
            })
            .then(response => response.json())
            .then(data => {
                document.getElementById('predictionResult').innerText = `Survived: ${data.survived}`;
            })
            .catch(error => console.error('Error:', error));
        });
    </script>
</body>
</html>

Remember to replace placeholders such as model loading logic, input preprocessing, and prediction logic with your actual code. 