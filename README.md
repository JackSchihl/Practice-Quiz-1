# Practice-Quiz-1
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Quiz</title>
    <style>
    /* Basic styling for the quiz app */
    body {
        font-family: Arial, sans-serif;
        background: #f4f4f4;
        margin: 0;
        padding: 0;
    }
    #quiz-container {
        background: #fff;
        max-width: 600px;
        margin: 40px auto;
        padding: 30px;
        border-radius: 8px;
        box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }
    h1 {
        text-align: center;
    }
    #results {
        margin-top: 20px;
        font-weight: bold;
    }
    button {
        display: block;
        margin: 20px auto 0 auto;
        padding: 10px 30px;
        font-size: 1rem;
        border: none;
        border-radius: 4px;
        background: #007bff;
        color: #fff;
        cursor: pointer;
    }
    button:disabled {
        background: #aaa;
        cursor: not-allowed;
    }
    </style>
</head>
<body>
    <div id="quiz-container">
        <h1>Student Quiz</h1>
        <form id="quiz-form">
            <!-- Questions will be injected here by app.js -->
            <div id="questions-area"></div>
            <button type="submit" id="submit-btn">Submit Quiz</button>
        </form>
        <div id="results"></div>
    </div>
    <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
    <script src="https://cdn.plot.ly/plotly-latest.min.js"></script>
    <script>
    // Questions array
    const questions = [
        {
            question: "The graph below shows a straight line. What is the slope of this line?",
            options: ["positive", "negative", "zero", "undefined"],
            answer: 0 // positive
        },
        {
            question: "The graph below shows a straight line. What is the slope of this line?",
            options: ["positive", "negative", "zero", "undefined"],
            answer: 3 // undefined
        },
        {
            question: "The graph below shows a straight line. What is the slope of this line?",
            options: ["positive", "negative", "zero", "undefined"],
            answer: 2 // zero
        },
        {
            question: "The graph below shows a straight line. What is the slope of this line?",
            options: ["positive", "negative", "zero", "undefined"],
            answer: 1 // negative
        },
        {
            question: "What is the Capital of France?",
            options: ["Paris", "Brussels", "New Orleans", "Old Orleans"],
            answer: 0 // Paris
        },
    ];

    document.addEventListener('DOMContentLoaded', function() {
        const questionsArea = document.getElementById('questions-area');
        const quizForm = document.getElementById('quiz-form');
        const resultsDiv = document.getElementById('results');

        // Render questions
        questions.forEach((q, idx) => {
            const qDiv = document.createElement('div');
            qDiv.className = 'question-block';
            qDiv.innerHTML = `<p><strong>Q${idx + 1}:</strong> ${q.question}</p>`;

            // Add a div for the plot for the first four questions
            if (idx === 0 || idx === 1 || idx === 2 || idx === 3) {
                const plotDiv = document.createElement('div');
                plotDiv.id = `plotly-graph-${idx}`;
                plotDiv.style = 'max-width: 350px; height: 250px; margin-bottom: 10px;';
                qDiv.appendChild(plotDiv);
            }

            q.options.forEach((opt, oIdx) => {
                const optId = `q${idx}_opt${oIdx}`;
                qDiv.innerHTML += `
                    <label>
                        <input type="radio" name="q${idx}" value="${oIdx}" required> ${opt}
                    </label><br>`;
            });
            questionsArea.appendChild(qDiv);
        });

        // Common axis limits and line color
        const xAxisRange = [-5, 10];
        const yAxisRange = [0, 20];
        const lineColor = 'blue';

        // Draw the plot for the first question (y = 2x + 10)
        if (document.getElementById('plotly-graph-0')) {
            const x = [xAxisRange[0], xAxisRange[1]];
            const y = x.map(xi => 2 * xi + 10);
            const trace = {
                x: x,
                y: y,
                mode: 'lines',
                line: {color: lineColor},
                name: 'Line'
            };
            const layout = {
                xaxis: {title: 'x', range: xAxisRange},
                yaxis: {title: 'y', range: yAxisRange},
                margin: {t: 10, r: 10, l: 40, b: 40},
                showlegend: false
            };
            Plotly.newPlot('plotly-graph-0', [trace], layout, {displayModeBar: false});
        }

        // Draw the plot for the second question (x = 5)
        if (document.getElementById('plotly-graph-1')) {
            const y = yAxisRange;
            const x = [5, 5];
            const trace = {
                x: x,
                y: y,
                mode: 'lines',
                line: {color: lineColor},
                name: 'Line'
            };
            const layout = {
                xaxis: {title: 'x', range: xAxisRange},
                yaxis: {title: 'y', range: yAxisRange},
                margin: {t: 10, r: 10, l: 40, b: 40},
                showlegend: false
            };
            Plotly.newPlot('plotly-graph-1', [trace], layout, {displayModeBar: false});
        }

        // Draw the plot for the third question (y = 3)
        if (document.getElementById('plotly-graph-2')) {
            const x = xAxisRange;
            const y = [3, 3];
            const trace = {
                x: x,
                y: y,
                mode: 'lines',
                line: {color: lineColor},
                name: 'Line'
            };
            const layout = {
                xaxis: {title: 'x', range: xAxisRange},
                yaxis: {title: 'y', range: yAxisRange},
                margin: {t: 10, r: 10, l: 40, b: 40},
                showlegend: false
            };
            Plotly.newPlot('plotly-graph-2', [trace], layout, {displayModeBar: false});
        }

        // Draw the plot for the fourth question (y = -3x - 6)
        if (document.getElementById('plotly-graph-3')) {
            const x = xAxisRange;
            const y = x.map(xi => -3 * xi - 6);
            const trace = {
                x: x,
                y: y,
                mode: 'lines',
                line: {color: lineColor},
                name: 'Line'
            };
            const layout = {
                xaxis: {title: 'x', range: xAxisRange},
                yaxis: {title: 'y', range: yAxisRange},
                margin: {t: 10, r: 10, l: 40, b: 40},
                showlegend: false
            };
            Plotly.newPlot('plotly-graph-3', [trace], layout, {displayModeBar: false});
        }

        quizForm.addEventListener('submit', function(e) {
            e.preventDefault();
            let score = 0;
            let output = '';
            questions.forEach((q, idx) => {
                const selected = quizForm[`q${idx}`].value;
                const correct = q.answer;
                if (parseInt(selected) === correct) {
                    score++;
                    output += `<p>Q${idx + 1}: Correct!</p>`;
                } else {
                    output += `<p>Q${idx + 1}: Incorrect. Correct answer: <strong>${q.options[correct]}</strong></p>`;
                }
            });
            resultsDiv.innerHTML = `<h2>Your Score: ${score} / ${questions.length}</h2>` + output;
            document.getElementById('submit-btn').disabled = true;
        });
    });
    </script>
</body>
</html>
