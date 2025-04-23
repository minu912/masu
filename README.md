<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>일본어 퀴즈</title>
  <style>
    body {
      background-color: #ccc;
      font-family: 'Arial', sans-serif;
      text-align: center;
      padding: 50px;
    }
    .card {
      background: #fff;
      border-radius: 20px;
      padding: 30px;
      box-shadow: 0 5px 15px rgba(0,0,0,0.2);
      max-width: 500px;
      margin: 0 auto;
    }
    h1 {
      font-size: 2rem;
      color: #333;
    }
    #question {
      font-size: 1.8rem;
      margin: 20px 0;
    }
    input {
      font-size: 1.5rem;
      padding: 10px;
      width: 80%;
    }
    .feedback {
      margin-top: 20px;
      font-size: 1.2rem;
    }
    .score {
      margin-top: 10px;
      font-size: 1rem;
      color: #333;
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 1rem;
      cursor: pointer;
      border-radius: 10px;
      border: none;
      background-color: #007BFF;
      color: white;
    }
    button:hover {
      background-color: #0056b3;
    }
  </style>
</head>
<body>
  <div class="card">
    <h1>일본어 퀴즈</h1>
    <div id="question">문제 로딩 중...</div>
    <input type="text" id="answer" placeholder="정답 입력" />
    <div class="feedback" id="result"></div>
    <div class="score" id="score"></div>
    <button onclick="resetQuiz()">다시 시작</button>
  </div>

  <script>
    const words = {
      "갑니다": "이키마스",
      "합니다": "시마스",
      "옵니다": "키마스",
      "봅니다": "미마스",
      "말합니다": "이이마스",
      "듣습니다": "키키마스",
      "씁니다": "카키마스",
      "읽습니다": "요미마스",
      "먹습니다": "타베마스",
      "마십니다": "노미마스",
      "만납니다": "아이마스",
      "이야기합니다": "하나시마스",
      "걷습니다": "아루키마스",
      "뜁니다": "하시리마스",
      "잡니다": "네마스",
      "일어납니다": "오키마스",
      "만듭니다": "츠쿠리마스",
      "기다립니다": "마치마스",
      "섭니다": "타치마스",
      "앉습니다": "스와리마스",
      "삽니다": "카이마스",
      "팝니다": "우리마스",
      "알려줍니다": "오시에마스",
      "탑니다": "노리마스",
      "내립니다": "오리마스",
      "일합니다": "하타라키마스",
      "돌아갑니다": "카에리마스",
      "찍습니다": "토리마스",
      "시작합니다": "하지메마스",
      "끝납니다": "오와리마스",
      "빌려줍니다": "카시마스",
      "빌립니다": "카리마스",
      "배웁니다": "나라이마스",
      "웃습니다": "와라이마스",
      "웁니다": "나키마스",
      "화냅니다": "오코리마스",
      "버립니다": "스테마스",
      "사용합니다": "츠카이마스",
      "엽니다": "아케마스",
      "닫습니다": "시메마스",
      "자릅니다": "키리마스",
      "보여줍니다": "미세마스",
      "노래합니다": "우타이마스",
      "이깁니다": "카치마스",
      "집니다": "마케마스",
      "놉니다": "아소비마스",
      "듭니다": "모치마스",
      "쉽니다": "야스미마스",
      "부릅니다": "요비마스",
      "움직입니다": "우고키마스",
      "보냅니다": "오쿠리마스",
      "생각해냅니다": "오모이다시마스",
      "정합니다": "키메마스",
      "입습니다": "키마스",
      "벗습니다": "누기마스",
      "신습니다": "하키마스",
      "대답합니다": "코타에마스",
      "돕습니다": "테츠다이마스",
      "찾습니다": "사가시마스",
      "고칩니다": "나오시마스"
    };

    const keys = Object.keys(words);
    let index = 0;
    let score = 0;

    function loadQuestion() {
      document.getElementById('question').innerText = keys[index];
      document.getElementById('answer').value = "";
      document.getElementById('answer').disabled = false;
      document.getElementById('result').innerText = "";
      document.getElementById('score').innerText = `현재 점수: ${score} / ${keys.length}`;
    }

    function checkAnswer() {
      const userAnswer = document.getElementById('answer').value.trim();
      const correct = words[keys[index]];
      if (userAnswer === correct) {
        document.getElementById('result').innerText = "✅ 정답입니다!";
        document.getElementById('result').style.color = 'green';
        score++;
      } else {
        document.getElementById('result').innerText = `❌ 오답입니다. 정답: ${correct}`;
        document.getElementById('result').style.color = 'red';
      }
      document.getElementById('score').innerText = `현재 점수: ${score} / ${keys.length}`;
      document.getElementById('answer').disabled = true;
      setTimeout(() => nextQuestion(), 3000);
    }

    function nextQuestion() {
      index++;
      if (index >= keys.length) {
        document.getElementById('question').innerText = "🎉 모든 문제 완료!";
        document.getElementById('result').innerText = `총 ${keys.length}문제 중 ${score}개 정답!`;
        return;
      }
      loadQuestion();
    }

    function resetQuiz() {
      index = 0;
      score = 0;
      document.getElementById('answer').disabled = false;
      loadQuestion();
    }

    // 처음 로딩 시
    window.onload = loadQuestion;
  </script>
</body>
</html>
