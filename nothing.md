from flask import Flask, render_template, request

app = Flask(__name__)
app.config.from_object(__name__)


@app.route('/')
def welcome():
    return render_template('form.html')


@app.route('/result', methods=['POST'])
def result():
    var_1 = request.form.get("var_1", type=int)
    var_2 = request.form.get("var_2", type=int)
    operation = request.form.get("operation")
    if(operation == 'Addition'):
        result = var_1 + var_2
    elif(operation == 'Subtraction'):
        result = var_1 - var_2
    elif(operation == 'Multiplication'):
        result = var_1 * var_2
    elif(operation == 'Division'):
        result = var_1 / var_2
    else:
        result = 'INVALID CHOICE'
    entry = result
    return render_template('result.html', entry=entry)

if __name__ == '__main__':
    app.run(debug=True)






<head>
    <title>Simple Form</title>
</head>
<body>
    <h1>Simple Calculator</h1>
    <form action="/result" method="post">
        <label for="var_1">Enter First Number:</label>
        <input type="number" id="var_1" name="var_1" required><br><br>

        <label for="var_2">Enter Second Number:</label>
        <input type="number" id="var_2" name="var_2" required><br><br>

        <label for="operation">Select Operation:</label>
        <select id="operation" name="operation" required>
            <option value="Addition">Addition</option>
            <option value="Subtraction">Subtraction</option>
            <option value="Multiplication">Multiplication</option>
            <option value="Division">Division</option>
        </select><br><br>

        <button type="submit">Calculate</button>
    </form>
</body>
</html>






<head>
    <title>Result</title>
</head>
<body>
    <h1>Calculation Result</h1>
    <p>The result of the operation is: <strong>{{ entry }}</strong></p>
    <a href="/">Perform Another Calculation</a>
</body>
</html>


