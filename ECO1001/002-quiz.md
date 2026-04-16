# Topic 2 Quiz（Q2: Interdependence and Gains from Trade）

**Course (課程)**: Principles of Economics 2026  
**Topic (主題)**: Topic 2: Interdependence and Gains from Trade

---

## Instructions（使用說明）
請為每道題目選擇一個選項，完成後點擊題目底部的 **「Submit / 提交答案」**。  
（若有未作答的題目，提交時將直接視為答錯）。  
提交後將會顯示正確答案與中英詳解，您的成績也會自動儲存至瀏覽器的學習紀錄中。

<div id="quiz-container" class="p-6 bg-white border border-gray-200 rounded-lg shadow-sm">
    <div id="quiz-content">
        <h2 id="question-text" class="text-xl font-bold mb-4">Loading...</h2>
        <div id="options-container" class="space-y-3"></div>
        <button id="submit-btn" class="mt-6 px-6 py-2 bg-blue-600 text-white rounded hover:bg-blue-700 transition">Submit Answer</button>
    </div>
    
    <div id="feedback-container" class="hidden mt-4 p-4 bg-gray-50 rounded border-l-4 border-blue-500">
        <p id="explanation-text" class="text-gray-700"></p>
        <button id="next-btn" class="mt-4 px-4 py-2 bg-green-600 text-white rounded">Next Question</button>
    </div>

    <div id="result-container" class="hidden">
        <h2 class="text-2xl font-bold mb-4">Quiz Completed!</h2>
        <p id="score-text" class="text-lg mb-4"></p>
        <a href="#/result" class="px-4 py-2 bg-blue-600 text-white rounded inline-block">View Results Page</a>
    </div>
</div>

<script>
(function() {
    const questions = [
        {
            q: "Who has the absolute advantage in producing potatoes?",
            options: ["Farmer", "Rancher", "Both", "Neither"],
            answer: 1,
            explanation: "Rancher: 10 min/oz vs Farmer: 15 min/oz. The Rancher requires less time to produce the same amount. <br> 牧場主人：10分鐘/盎司 對比 農夫：15分鐘/盎司。牧場主人生產相同數量所需時間較少。"
        },
        {
            q: "What determines if there are gains from trade?",
            options: ["Absolute advantage", "Comparative advantage", "Market size", "Total output"],
            answer: 1,
            explanation: "Potential gains from trade are based on comparative advantage, not absolute advantage. <br> 潛在的貿易利得是基於比較優勢，而非絕對優勢。"
        }
    ];

    let currentQ = 0;
    let score = 0;

    const qText = document.getElementById('question-text');
    const optContainer = document.getElementById('options-container');
    const submitBtn = document.getElementById('submit-btn');
    const feedbackContainer = document.getElementById('feedback-container');
    const explanationText = document.getElementById('explanation-text');
    const nextBtn = document.getElementById('next-btn');
    const quizContent = document.getElementById('quiz-content');
    const resultContainer = document.getElementById('result-container');
    const scoreText = document.getElementById('score-text');

    function loadQuestion() {
        const q = questions[currentQ];
        qText.innerText = `Q${currentQ + 1}: ${q.q}`;
        optContainer.innerHTML = '';
        feedbackContainer.classList.add('hidden');
        submitBtn.classList.remove('hidden');
        
        q.options.forEach((opt, index) => {
            const div = document.createElement('div');
            div.innerHTML = `<label class="flex items-center space-x-2 cursor-pointer p-2 hover:bg-gray-100 rounded">
                <input type="radio" name="q" value="${index}" class="form-radio h-4 w-4 text-blue-600">
                <span>${opt}</span>
            </label>`;
            optContainer.appendChild(div);
        });
    }

    submitBtn.onclick = () => {
        const selected = document.querySelector('input[name="q"]:checked');
        if (!selected) return alert('Please select an answer.');
        
        const isCorrect = parseInt(selected.value) === questions[currentQ].answer;
        if (isCorrect) score++;
        
        explanationText.innerHTML = `<strong>${isCorrect ? 'Correct!' : 'Incorrect.'}</strong><br>${questions[currentQ].explanation}`;
        submitBtn.classList.add('hidden');
        feedbackContainer.classList.remove('hidden');
    };

    nextBtn.onclick = () => {
        currentQ++;
        if (currentQ < questions.length) {
            loadQuestion();
        } else {
            showResult();
        }
    };

    function showResult() {
        quizContent.classList.add('hidden');
        feedbackContainer.classList.add('hidden');
        resultContainer.classList.remove('hidden');
        const finalScore = Math.round((score / questions.length) * 100);
        scoreText.innerText = `You scored ${score}/${questions.length} (${finalScore}%).`;
        
        const history = JSON.parse(localStorage.getItem('quiz_history') || '[]');
        history.push({
            date: new Date().toISOString().split('T')[0],
            unit: 'Topic 2: Interdependence',
            score: finalScore
        });
        localStorage.setItem('quiz_history', JSON.stringify(history));
    }

    loadQuestion();
})();
</script>