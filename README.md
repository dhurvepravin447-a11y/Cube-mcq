<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Cube & Cube Root Online Test</title>
  <style>
    body { font-family: Arial, sans-serif; margin: 20px; background: #f9f9f9; }
    h1 { text-align: center; color: #333; }
    .quiz-container { max-width: 800px; margin: auto; background: #fff; padding: 20px; border-radius: 10px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    .question { font-size: 18px; margin: 15px 0; }
    .options label { display: block; margin-bottom: 8px; }
    button { margin-top: 20px; padding: 10px 20px; font-size: 16px; border: none; border-radius: 5px; background: #4CAF50; color: #fff; cursor: pointer; }
    button:hover { background: #45a049; }
    .result { font-size: 20px; margin-top: 20px; text-align: center; }
    .feedback { font-weight: bold; margin-top: 5px; }
    #timer { font-size: 18px; color: #333; text-align: center; margin-bottom: 20px; }
  </style>
</head>
<body>
  <h1>Cube & Cube Roots (1–30) - Online Test</h1>
  <div class="quiz-container">
    <div id="timer">Time Left: <span id="time">10:00</span></div>
    <form id="quizForm"></form>
    <button onclick="submitQuiz()">Submit Test</button>
    <div class="result" id="result"></div>
  </div>

  <script>
    const questions = [
      {q: "1 का cube कितना है?", options: ["0", "1", "2", "3"], ans: 1},
      {q: "2 का cube root क्या है?", options: ["2", "3", "4", "8"], ans: 0},
      {q: "3 का cube कितना है?", options: ["9", "18", "27", "36"], ans: 2},
      {q: "64 का cube root क्या है?", options: ["3", "4", "5", "6"], ans: 1},
      {q: "5 का cube कितना होगा?", options: ["100", "115", "120", "125"], ans: 3},
      {q: "216 का cube root क्या है?", options: ["5", "6", "7", "8"], ans: 1},
      {q: "7 का cube कितना होगा?", options: ["243", "343", "729", "512"], ans: 1},
      {q: "512 का cube root क्या है?", options: ["6", "7", "8", "9"], ans: 2},
      {q: "9 का cube कितना है?", options: ["729", "512", "1331", "1000"], ans: 0},
      {q: "1000 का cube root क्या है?", options: ["9", "10", "11", "12"], ans: 1},
      {q: "11 का cube कितना होगा?", options: ["1331", "1728", "2197", "2744"], ans: 0},
      {q: "1728 का cube root क्या है?", options: ["12", "13", "14", "15"], ans: 0},
      {q: "13 का cube कितना होगा?", options: ["1728", "2197", "3375", "4096"], ans: 1},
      {q: "2744 का cube root क्या है?", options: ["12", "13", "14", "15"], ans: 2},
      {q: "15 का cube कितना है?", options: ["2197", "2744", "3375", "4096"], ans: 2},
      {q: "4096 का cube root क्या है?", options: ["14", "15", "16", "17"], ans: 2},
      {q: "17 का cube कितना है?", options: ["4096", "4913", "5832", "6859"], ans: 1},
      {q: "5832 का cube root क्या है?", options: ["17", "18", "19", "20"], ans: 1},
      {q: "19 का cube कितना होगा?", options: ["5832", "6859", "8000", "9261"], ans: 1},
      {q: "8000 का cube root क्या है?", options: ["18", "19", "20", "21"], ans: 2},
      {q: "21 का cube कितना होगा?", options: ["9261", "10648", "12167", "13824"], ans: 0},
      {q: "10648 का cube root क्या है?", options: ["21", "22", "23", "24"], ans: 1},
      {q: "23 का cube कितना है?", options: ["12167", "13824", "15625", "17576"], ans: 0},
      {q: "13824 का cube root क्या है?", options: ["22", "23", "24", "25"], ans: 2},
      {q: "25 का cube कितना होगा?", options: ["13824", "15625", "17576", "19683"], ans: 1},
      {q: "17576 का cube root क्या है?", options: ["24", "25", "26", "27"], ans: 2},
      {q: "27 का cube कितना है?", options: ["17576", "19683", "21952", "24389"], ans: 1},
      {q: "21952 का cube root क्या है?", options: ["27", "28", "29", "30"], ans: 1},
      {q: "29 का cube कितना होगा?", options: ["21952", "24389", "27000", "30000"], ans: 1},
      {q: "27000 का cube root क्या है?", options: ["28", "29", "30", "31"], ans: 2},
      {q: "4913 किसका cube है?", options: ["15", "16", "17", "18"], ans: 2},
      {q: "कौन-सा perfect cube है?", options: ["2100", "2110", "2150", "2197"], ans: 3},
      {q: "Cube of 15 is?", options: ["1728", "3375", "4913", "5832"], ans: 1},
      {q: "Cube root of 9261 = ?", options: ["20", "21", "22", "23"], ans: 1},
      {q: "Smallest cube greater than 1000 = ?", options: ["1000", "1331", "1728", "2197"], ans: 1},
      {q: "Largest cube less than 2000 = ?", options: ["1331", "1728", "2197", "2744"], ans: 1},
      {q: "Cube of even number between 9 and 11 = ?", options: ["729", "1000", "1331", "1728"], ans: 1},
      {q: "Cube root of 5832 = ?", options: ["17", "18", "19", "20"], ans: 1},
      {q: "Which is NOT a perfect cube?", options: ["1331", "1728", "2000", "2197"], ans: 2},
      {q: "Cube of 29 = ?", options: ["24389", "27000", "21952", "19683"], ans: 0},
      {q: "2744 किसका cube है?", options: ["13", "14", "15", "16"], ans: 1},
      {q: "8000 का cube root क्या है?", options: ["18", "19", "20", "21"], ans: 2},
      {q: "Cube of 7 more than 15 = ?", options: ["22³", "21³", "20³", "19³"], ans: 0},
      {q: "Which cube lies between 5000 and 6000?", options: ["4913", "5832", "6859", "4096"], ans: 1},
      {q: "Cube of 25 = ?", options: ["13824", "15625", "17576", "19683"], ans: 1},
      {q: "3375 किसका cube है?", options: ["14", "15", "16", "17"], ans: 1},
      {q: "Cube root of 21952 = ?", options: ["27", "28", "29", "30"], ans: 1},
      {q: "Cube number nearest to 500 = ?", options: ["343", "512", "729", "1000"], ans: 1},
      {q: "Cube number nearest to 10000 = ?", options: ["9261", "10648", "12167", "13824"], ans: 0},
      {q: "Which is a perfect cube?", options: ["27000", "27100", "27200", "27300"], ans: 0}
    ];

    // Shuffle questions
    questions.sort(() => Math.random() - 0.5);

    const form = document.getElementById("quizForm");
    questions.forEach((item, i) => {
      let qDiv = document.createElement("div");
      qDiv.classList.add("question");
      qDiv.innerHTML = `<b>Q${i+1}. ${item.q}</b>`;
      let optDiv = document.createElement("div");
      optDiv.classList.add("options");
      item.options.forEach((opt, j) => {
        optDiv.innerHTML += `<label><input type='radio' name='q${i}' value='${j}' onchange='showFeedback(${i}, ${j})'> ${opt}</label>`;
      });
      qDiv.appendChild(optDiv);
      qDiv.innerHTML += `<div class='feedback' id='feedback${i}'></div>`;
      form.appendChild(qDiv);
    });

    function showFeedback(qIndex, selected) {
      const feedback = document.getElementById(`feedback${qIndex}`);
      if (selected === questions[qIndex].ans) {
        feedback.textContent = '✅ Correct';
        feedback.style.color = 'green';
      } else {
        feedback.textContent = '❌ Incorrect';
        feedback.style.color = 'red';
      }
    }

    function submitQuiz() {
      let score = 0;
      questions.forEach((item, i) => {
        let selected = document.querySelector(`input[name=q${i}]:checked`);
        if (selected && parseInt(selected.value) === item.ans) {
          score++;
        }
      });
      document.getElementById("result").innerHTML = `✅ Your Score: ${score} / ${questions.length}`;
    }

    // Timer 10 minutes
    let timeLeft = 600;
    const timerEl = document.getElementById('time');
    setInterval(() => {
      let minutes = Math.floor(timeLeft / 60);
      let seconds = timeLeft % 60;
      timerEl.textContent = `${minutes}:${seconds.toString().padStart(2, '0')}`;
      timeLeft--;
      if(timeLeft < 0) submitQuiz();
    }, 1000);
  </script>
</body>
</html>
