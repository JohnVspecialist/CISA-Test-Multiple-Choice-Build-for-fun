# CISA-Test-Multiple-Choice-Build-for-fun

The code creates an interactive web-based multiple-choice quiz. The quiz displays one question at a time, evaluates the user's answer, shows whether the answer is correct or incorrect along with an explanation, and then proceeds to the next question. Here is a detailed explanation of what each part of the code does:

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
