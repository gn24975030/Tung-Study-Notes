<style>
  .quiz-box { font-family: Arial, sans-serif; max-width: 800px; margin: 0 auto; line-height: 1.6; }
  .question-block { background: #f9f9f9; padding: 15px; margin-bottom: 20px; border-radius: 8px; border-left: 4px solid #007acc; }
  .question-text { font-weight: bold; margin-bottom: 10px; }
  .option-label { display: block; margin-bottom: 8px; cursor: pointer; }
  .submit-btn { background: #007acc; color: white; padding: 10px 20px; border: none; border-radius: 5px; font-size: 16px; cursor: pointer; width: 100%; margin-top: 10px; }
  .submit-btn:hover { background: #005f99; }
  .result-table { width: 100%; border-collapse: collapse; margin-top: 20px; font-size: 14px; }
  .result-table th, .result-table td { border: 1px solid #ddd; padding: 10px; text-align: left; }
  .result-table th { background-color: #f2f2f2; }
  .correct { color: green; font-weight: bold; }
  .incorrect { color: red; font-weight: bold; }
  .history-box { margin-top: 40px; padding-top: 20px; border-top: 2px dashed #ccc; }
</style>

<div class="quiz-box">
  <h2>ECO1000 - Revision Exercise (Interactive)</h2>
  
  <!-- 測驗區域 -->
  <div id="quiz-area"></div>
  <button id="submit-btn" class="submit-btn" onclick="submitQuiz()">Submit Answers</button>

  <!-- 結果與檢討表格區域 -->
  <div id="result-area" style="display: none;">
    <h3 id="score-display"></h3>
    <table class="result-table">
      <thead>
        <tr>
          <th width="5%">#</th>
          <th width="35%">Question</th>
          <th width="15%">Your Answer</th>
          <th width="15%">Correct Answer</th>
          <th width="30%">Explanation (題解)</th>
        </tr>
      </thead>
      <tbody id="review-table-body"></tbody>
    </table>
    <button class="submit-btn" style="margin-top: 20px; background: #555;" onclick="location.reload()">Retry (重新測驗)</button>
  </div>

  <!-- 歷史紀錄區域 -->
  <div class="history-box">
    <h3>Past Results (歷史成績)</h3>
    <ul id="history-list"></ul>
  </div>
</div>

<script>
  // 題庫資料 (抽取自 PDF 頭 5 題)
  const rawQuestions = [
    {
      id: 1,
      q: "The following table contains a demand schedule for a good. Price: $100 -> Quantity: 1,000. Price: $200 -> Quantity: Q1. If the law of demand applies to this good, then Q1 could be",
      options: ["0.", "1,000.", "2,000.", "3,000."],
      ans: "0.",
      expEn: "According to the law of demand, as price increases, quantity demanded decreases. Since price increased from $100 to $200, Q1 must be less than 1,000.",
      expZh: "根據需求法則，價格上升時，需求量會下降。因為價格從 $100 上升到 $200，Q1 必須小於 1,000。"
    },
    {
      id: 2,
      q: "Economists make assumptions to",
      options: [
        "provide issues for political discussion.",
        "make a complex world easier to understand.",
        "make it easier to teach economic concepts and analysis.",
        "create policy alternatives that are incomplete or subject to criticism."
      ],
      ans: "make a complex world easier to understand.",
      expEn: "Assumptions simplify the complex world, making it easier to understand and build economic models.",
      expZh: "假設能簡化複雜的現實世界，使其更容易理解並建立經濟模型。"
    },
    {
      id: 3,
      q: "The production possibilities frontier is a graph that shows the various combinations of output that an economy can possibly produce given the available resources and",
      options: [
        "society’s preferences.",
        "the available production technology.",
        "a fair distribution of the output.",
        "the available demand for the output."
      ],
      ans: "the available production technology.",
      expEn: "The PPF is defined by the available factors of production (resources) and the available production technology.",
      expZh: "生產可能線 (PPF) 是由可用的生產要素（資源）和可用的生產技術所決定的。"
    },
    {
      id: 4,
      q: "Which of the following concepts cannot be illustrated by the production possibilities frontier?",
      options: ["efficiency", "opportunity cost", "fairness", "trade-offs"],
      ans: "fairness",
      expEn: "The PPF illustrates efficiency (points on the curve), opportunity cost (slope), and trade-offs, but it tells us nothing about whether the distribution is fair.",
      expZh: "PPF 可以說明效率（線上的點）、機會成本（斜率）和權衡取捨，但無法說明資源分配是否公平。"
    },
    {
      id: 5,
      q: "When economists make",
      options: [
        "positive statements, they are speaking not as scientists but as policy advisers.",
        "positive statements, they are speaking not as scientists but as forecasters.",
        "normative statements, they are speaking not as scientists but as policy advisers.",
        "normative statements, they are speaking not as policy advisers but as model-builders."
      ],
      ans: "normative statements, they are speaking not as scientists but as policy advisers.",
      expEn: "Positive statements are descriptive (scientists), while normative statements are prescriptive (policy advisers).",
      expZh: "實證性陳述 (Positive) 是描述性的（科學家角色），而規範性陳述 (Normative) 是建議性的（政策顧問角色）。"
    }
  ];

  let currentQuiz = [];

  // 洗牌函數 (Fisher-Yates Shuffle)
  function shuffle(array) {
    let currentIndex = array.length, randomIndex;
    while (currentIndex !== 0) {
      randomIndex = Math.floor(Math.random() * currentIndex);
      currentIndex--;
      [array[currentIndex], array[randomIndex]] = [array[randomIndex], array[currentIndex]];
    }
    return array;
  }

  // 初始化測驗
  function initQuiz() {
    const quizArea = document.getElementById('quiz-area');
    quizArea.innerHTML = '';
    
    // 打亂題目次序
    currentQuiz = shuffle([...rawQuestions]).map(q => {
      return { ...q, shuffledOptions: shuffle([...q.options]) };
    });

    currentQuiz.forEach((q, index) => {
      let optionsHtml = q.shuffledOptions.map((opt, optIndex) => `
        <label class="option-label">
          <input type="radio" name="q_${index}" value="${opt}"> ${opt}
        </label>
      `).join('');

      quizArea.innerHTML += `
        <div class="question-block">
          <div class="question-text">${index + 1}. ${q.q}</div>
          ${optionsHtml}
        </div>
      `;
    });

    loadHistory();
  }

  // 提交答案
  function submitQuiz() {
    let score = 0;
    let reviewHtml = '';

    currentQuiz.forEach((q, index) => {
      const selected = document.querySelector(`input[name="q_${index}"]:checked`);
      const userAnswer = selected ? selected.value : "No answer";
      const isCorrect = userAnswer === q.ans;
      
      if (isCorrect) score++;

      const statusClass = isCorrect ? 'correct' : 'incorrect';
      const statusText = isCorrect ? '✓' : '✗';

      reviewHtml += `
        <tr>
          <td>${index + 1}</td>
          <td>${q.q}</td>
          <td class="${statusClass}">${statusText} ${userAnswer}</td>
          <td class="correct">${q.ans}</td>
          <td>
            <strong>EN:</strong> ${q.expEn}<br>
            <strong>ZH:</strong> ${q.expZh}
          </td>
        </tr>
      `;
    });

    // 顯示結果
    document.getElementById('quiz-area').style.display = 'none';
    document.getElementById('submit-btn').style.display = 'none';
    document.getElementById('result-area').style.display = 'block';
    
    const finalScoreText = `Your Score: ${score} / ${currentQuiz.length} (${Math.round((score/currentQuiz.length)*100)}%)`;
    document.getElementById('score-display').innerText = finalScoreText;
    document.getElementById('review-table-body').innerHTML = reviewHtml;

    saveHistory(finalScoreText);
  }

  // 儲存結果到 LocalStorage
  function saveHistory(scoreText) {
    const date = new Date().toLocaleString();
    const record = `${date} - ${scoreText}`;
    let history = JSON.parse(localStorage.getItem('ecoQuizHistory')) || [];
    history.unshift(record); // 加到最前
    localStorage.setItem('ecoQuizHistory', JSON.stringify(history));
    loadHistory();
  }

  // 載入歷史紀錄
  function loadHistory() {
    const historyList = document.getElementById('history-list');
    let history = JSON.parse(localStorage.getItem('ecoQuizHistory')) || [];
    if (history.length === 0) {
      historyList.innerHTML = "<li>No past records found.</li>";
    } else {
      historyList.innerHTML = history.slice(0, 5).map(h => `<li>${h}</li>`).join(''); // 只顯示最近 5 次
    }
  }

  // 網頁載入時執行
  window.onload = initQuiz;
</script>