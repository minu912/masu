<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>일본어 퀴즈</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f4f4f4;
            color: #333;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
        }
        .quiz-container {
            background-color: #fff;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 90%;
            width: 500px;
        }
        h1 {
            color: #007bff;
            margin-bottom: 20px;
        }
        #question {
            font-size: 1.8em;
            margin-bottom: 20px;
            color: #555;
        }
        input[type="text"] {
            padding: 12px;
            font-size: 1.2em;
            border: 1px solid #ccc;
            border-radius: 8px;
            margin-bottom: 15px;
            width: 80%;
            box-sizing: border-box;
        }
        button {
            background-color: #28a745;
            color: white;
            border: none;
            padding: 12px 25px;
            font-size: 1.1em;
            border-radius: 8px;
            cursor: pointer;
            margin: 5px;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #1e7e34;
        }
        #result {
            font-size: 1.2em;
            margin-top: 20px;
            font-weight: bold;
        }
        #score {
            font-size: 1em;
            color: #777;
            margin-top: 10px;
        }
        .feedback.correct {
            color: green;
        }
        .feedback.incorrect {
            color: red;
        }
    </style>
</head>
<body>
    <div class="quiz-container">
        <h1>일본어 퀴즈</h1>
        <div id="question">문제 로딩 중...</div>
        <input type="text" id="answer" placeholder="정답 입력">
        <div id="result" class="feedback"></div>
        <div id="score"></div>
        <button onclick="checkAnswer()">정답 확인</button>
        <button onclick="nextQuestion()">다음 문제</button>
        <button onclick="resetQuiz()">다시 시작</button>
    </div>

    <script>
        const words = {
            "갑니다": "いきます",
            "합니다": "します",
            "옵니다": "きます",
            "봅니다": "みます",
            "말합니다": "いいます",
            "듣습니다": "ききます",
            "씁니다": "かきます",
            "읽습니다": "よみます",
            "먹습니다": "たべます",
            "마십니다": "のみます",
            "만납니다": "あいます",
            "이야기합니다": "はなします",
            "걷습니다": "あるきます",
            "뜁니다": "はしります",
            "잡니다": "ねます",
            "일어납니다": "おきます",
            "만듭니다": "つくります",
            "기다립니다": "まちます",
            "섭니다": "たちます",
            "앉습니다": "すわります",
            "삽니다": "かいます",
            "팝니다": "うります",
            "알려줍니다": "おしえます",
            "탑니다": "のります",
            "내립니다": "おります",
            "일합니다": "はたらきます",
            "돌아갑니다": "かえります",
            "찍습니다": "とります",
            "시작합니다": "はじめます",
            "끝납니다": "おわります",
            "빌려줍니다": "かします",
            "빌립니다": "かります",
            "배웁니다": "ならいます",
            "웃습니다": "わらいます",
            "웁니다": "なきます",
            "화냅니다": "おこります",
            "버립니다": "すてます",
            "사용합니다": "つかいます",
            "엽니다": "あけます",
            "닫습니다": "しめます",
            "자릅니다": "きります",
            "보여줍니다": "みせます",
            "노래합니다": "うたいます",
            "이깁니다": "かちます",
            "집니다": "まけます",
            "놉니다": "あそびます",
            "듭니다": "もちます",
            "쉽니다": "やすみます",
            "부릅니다": "よびます",
            "움직입니다": "うごきます",
            "보냅니다": "おくります",
            "생각해냅니다": "おもいだします",
            "정합니다": "きめます",
            "입습니다": "きます",
            "벗습니다": "ぬぎます",
            "신습니다": "はきます",
            "대답합니다": "こたえます",
            "돕습니다": "てつだいます",
            "찾습니다": "さがします",
            "고칩니다": "なおします"
        };

        const keys = Object.keys(words);
        let index = 0;
        let score = 0;
        let answered = false;

        const questionElement = document.getElementById('question');
        const answerInput = document.getElementById('answer');
        const resultElement = document.getElementById('result');
        const scoreElement = document.getElementById('score');
        const nextButton = document.querySelector('button:nth-child(3)');

        function loadQuestion() {
            if (index < keys.length) {
                questionElement.textContent = keys[index];
                answerInput.value = "";
                answerInput.disabled = false;
                answerInput.focus();
                resultElement.textContent = "";
                resultElement.className = "feedback";
                scoreElement.textContent = `현재 점수: ${score} / ${keys.length}`;
                answered = false;
                nextButton.disabled = true;
            } else {
                questionElement.textContent = "🎉 모든 문제 완료!";
                answerInput.style.display = "none";
                resultElement.textContent = `총 ${keys.length}문제 중 ${score}개 정답!`;
                resultElement.className = "feedback";
                scoreElement.textContent = `최종 점수: ${Math.round((score / keys.length) * 100)}점`;
                nextButton.disabled = true;
            }
        }

        function checkAnswer() {
            if (!answered) {
                const userAnswer = answerInput.value.trim();
                const correctAnswer = words[keys[index]];
                if (userAnswer === correctAnswer) {
                    resultElement.textContent = "✅ 정답입니다!";
                    resultElement.className = "feedback correct";
                    score++;
                } else {
                    resultElement.textContent = `❌ 오답입니다. 정답: ${correctAnswer}`;
                    resultElement.className = "feedback incorrect";
                }
                scoreElement.textContent = `현재 점수: ${score} / ${keys.length}`;
                answerInput.disabled = true;
                answered = true;
                nextButton.disabled = false;
            }
        }

        function nextQuestion() {
            if (answered) {
                index++;
                loadQuestion();
            }
        }

        function resetQuiz() {
            index = 0;
            score = 0;
            answerInput.style.display = "block";
            loadQuestion();
        }

        // 초기 로딩
        loadQuestion();
    </script>
</body>
</html>
