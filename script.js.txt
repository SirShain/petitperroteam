const quizData = [
    {
        question: "Qual é a fórmula da velocidade média?",
        options: ["v = d / t", "v = m * a", "v = E / t", "v = P / F"],
        correct: 0,
        explanation: "A velocidade média é calculada pela distância percorrida dividida pelo tempo." 
    },
    {
        question: "Qual das seguintes grandezas é uma unidade de força?",
        options: ["Newton", "Joule", "Watt", "Pascal"],
        correct: 0,
        explanation: "A unidade de força no SI é o Newton (N)." 
    },
    {
        question: "Qual é a primeira lei de Newton?",
        options: ["Lei da Inércia", "Lei da Ação e Reação", "Lei da Conservação de Energia", "Lei da Gravitação Universal"],
        correct: 0,
        explanation: "A Primeira Lei de Newton, também chamada de Lei da Inércia, afirma que um corpo tende a permanecer em repouso ou em movimento uniforme a menos que uma força externa atue sobre ele." 
    }
];

let currentQuestion = 0;

function loadQuestion() {
    const questionElement = document.getElementById("question");
    const optionsElement = document.getElementById("options");
    const explanationBox = document.getElementById("explanation-box");
    const finalMessage = document.getElementById("final-message");
    
    if (currentQuestion >= quizData.length) {
        questionElement.style.display = "none";
        optionsElement.style.display = "none";
        explanationBox.style.display = "none";
        finalMessage.style.display = "block";
        finalMessage.innerText = "Parabéns! Você concluiu o quiz.";
        return;
    }
    
    explanationBox.style.display = "none";
    finalMessage.style.display = "none";
    questionElement.innerText = quizData[currentQuestion].question;
    optionsElement.innerHTML = "";
    
    quizData[currentQuestion].options.forEach((option, index) => {
        const button = document.createElement("button");
        button.innerText = option;
        button.onclick = () => checkAnswer(index);
        optionsElement.appendChild(button);
    });
}

function checkAnswer(selectedIndex) {
    const optionsButtons = document.querySelectorAll("#options button");
    const explanationBox = document.getElementById("explanation-box");
    const explanationText = document.getElementById("explanation");
    const nextButton = document.getElementById("next-button");
    
    if (selectedIndex === quizData[currentQuestion].correct) {
        optionsButtons[selectedIndex].classList.add("correct");
    } else {
        optionsButtons[selectedIndex].classList.add("incorrect");
    }
    
    explanationText.innerText = quizData[currentQuestion].explanation;
    explanationBox.style.display = "block";
    nextButton.style.display = "block";
}

function nextQuestion() {
    currentQuestion++;
    loadQuestion();
}

document.getElementById("next-button").onclick = nextQuestion;

loadQuestion();
