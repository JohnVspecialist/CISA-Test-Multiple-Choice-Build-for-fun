# CISA-Test-Multiple-Choice-Build-for-fun

# The code creates an interactive web-based multiple-choice quiz. The quiz displays one question at a time, evaluates the user's answer, shows whether the answer is correct or incorrect along with an explanation, and then proceeds to the next question. Here is a detailed explanation of what each part of the code does:

HTML
The HTML part of the code structures the content of the web page. It includes:

The document type declaration (<!DOCTYPE html>).
The <html>, <head>, and <body> tags which are the basic structure of any HTML document.
Inside the <head> tag, meta tags and the title of the web page (<title>CISA Practice Quiz>).
A <style> tag for CSS to style the content.
The main content within the <body> tag which includes:
A container for the quiz with a class of .quiz-container.
A heading for the quiz.
A <div> with an id of quiz to hold the current question.
A submit button.
A <div> with an id of results to display the result of the answer.
CSS
The CSS part styles the HTML elements to make the quiz visually appealing:

It sets the font, line height, margin, and padding for the body.
It styles the .quiz-container to center it and give it a background color, padding, border radius, and box shadow.
It sets styles for headings, questions, options, and the submit button to improve readability and usability.
JavaScript
The JavaScript part adds interactivity to the quiz:

Quiz Data:

An array of objects named quizData, where each object represents a question. Each object contains:
question: The question text.
options: An array of possible answers.
correct: The index of the correct answer in the options array.
explanation: A text explaining why the correct answer is correct.
DOM Elements:

Variables to reference the quiz container (quizContainer), results container (resultsContainer), and the submit button (submitButton).
Functions:

buildQuiz(): Builds and displays the current question and its options.
showResults(): Checks the selected answer, shows whether it's correct or incorrect, displays an explanation, and updates the result container.
nextQuestion(): Advances to the next question, clears the results container, and updates the quiz container.
Event Listener:

An event listener on the submit button that calls showResults() if the button text is "Submit" and nextQuestion() if the button text is "Next".
Overall Flow
When the page loads, buildQuiz() is called to display the first question.
The user selects an answer and clicks "Submit".
The showResults() function checks if the selected answer is correct or incorrect, displays the appropriate feedback, and changes the button text to "Next".
When the user clicks "Next", the nextQuestion() function clears the results, advances to the next question, and calls buildQuiz() again to display the next question.
This cycle continues until all questions are answered, at which point the final score is displayed and the submit button is hidden.
This code provides a functional framework for a quiz application with a user-friendly interface and interactive elements.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CISA Practice Quiz</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .quiz-container {
            max-width: 800px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .question {
            margin-bottom: 20px;
        }
        .options {
            list-style-type: none;
            padding: 0;
        }
        .options li {
            margin-bottom: 10px;
        }
        .options label {
            display: block;
            padding: 10px;
            background-color: #f0f0f0;
            border-radius: 5px;
            cursor: pointer;
            transition: background-color 0.3s;
        }
        .options label:hover {
            background-color: #e0e0e0;
        }
        button {
            display: block;
            width: 100%;
            padding: 10px;
            background-color: #4CAF50;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            transition: background-color 0.3s;
        }
        button:hover {
            background-color: #45a049;
        }
        .result {
            margin-top: 20px;
            font-weight: bold;
        }
        .explanation {
            margin-top: 10px;
            padding: 10px;
            background-color: #e7f3fe;
            border-left: 5px solid #2196F3;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <h1>CISA Practice Quiz</h1>
        <div id="quiz"></div>
        <button id="submit">Submit</button>
        <div id="results" class="result"></div>
    </div>

    <script>
        const quizData = [
            {
                question: "What is the primary purpose of an information system audit?",
                options: [
                    "To ensure that the system's performance meets business objectives",
                    "To assess the system's compliance with applicable laws and regulations",
                    "To evaluate the efficiency of the IT department",
                    "To identify and mitigate risks associated with the information system"
                ],
                correct: 1,
                explanation: "The primary purpose of an information system audit is to assess the system's compliance with applicable laws and regulations. This ensures that the organization is operating within legal and regulatory frameworks."
            },
            {
                question: "During the audit planning phase, what is the first step an auditor should take?",
                options: [
                    "Evaluate the effectiveness of the internal controls",
                    "Conduct a risk assessment",
                    "Develop the audit program",
                    "Review prior audit reports"
                ],
                correct: 1,
                explanation: "The first step during the audit planning phase is to conduct a risk assessment. This helps in identifying areas that require more focus and resources during the audit."
            },
            // Add other questions here
        ];

        const quizContainer = document.getElementById('quiz');
        const resultsContainer = document.getElementById('results');
        const submitButton = document.getElementById('submit');

        let currentQuestionIndex = 0;
        let score = 0;

        function buildQuiz() {
            const currentQuestion = quizData[currentQuestionIndex];
            const options = currentQuestion.options.map((option, index) => 
                `<li>
                    <label>
                        <input type="radio" name="question" value="${index}">
                        ${option}
                    </label>
                </li>`
            ).join('');

            quizContainer.innerHTML = `
                <div class="question">
                    <p><strong>Question ${currentQuestionIndex + 1}:</strong> ${currentQuestion.question}</p>
                    <ul class="options">${options}</ul>
                </div>
            `;
        }

        function showResults() {
            const selectedOption = document.querySelector('input[name="question"]:checked');
            if (!selectedOption) {
                alert("Please select an answer.");
                return;
            }

            const answer = parseInt(selectedOption.value);
            const currentQuestion = quizData[currentQuestionIndex];

            if (answer === currentQuestion.correct) {
                score++;
                resultsContainer.innerHTML = `<p style="color: green;">Correct!</p>`;
            } else {
                resultsContainer.innerHTML = `<p style="color: red;">Wrong! The correct answer is: ${currentQuestion.options[currentQuestion.correct]}</p>`;
            }

            resultsContainer.innerHTML += `<p><strong>Explanation:</strong> ${currentQuestion.explanation}</p>`;

            currentQuestionIndex++;
            if (currentQuestionIndex < quizData.length) {
                submitButton.textContent = "Next";
            } else {
                submitButton.textContent = "Finish";
            }
        }

        function nextQuestion() {
            resultsContainer.innerHTML = '';
            if (currentQuestionIndex < quizData.length) {
                buildQuiz();
                submitButton.textContent = "Submit";
            } else {
                quizContainer.innerHTML = `<p>You scored ${score} out of ${quizData.length}.</p>`;
                submitButton.style.display = 'none';
            }
        }

        buildQuiz();

        submitButton.addEventListener('click', () => {
            if (submitButton.textContent === "Submit") {
                showResults();
            } else {
                nextQuestion();
            }
        });
    </script>
</body>
</html>

