# Topic 2 Quiz（Q2: Interdependence and Gains from Trade）

**Course (課程)**: Principles of Economics 2026  
**Topic (主題)**: Topic 2: Interdependence and Gains from Trade

---

## Instructions（使用說明）
請為每道題目選擇一個選項，完成後點擊題目底部的 **「Submit / 提交答案」**。  
（若有未作答的題目，提交時將直接視為答錯）。  
提交後將會顯示正確答案與中英詳解，您的成績也會自動儲存至瀏覽器的學習紀錄中。

<div id="quiz-app" class="p-6 bg-white border border-gray-200 rounded-lg shadow-sm">
    <div id="questions-list" class="space-y-8">
        <!-- 題目將透過 JavaScript 自動渲染 -->
    </div>
    
    <button id="submit-btn" class="mt-8 w-full py-3 bg-blue-600 text-white font-bold rounded hover:bg-blue-700 transition">
        Submit Answers
    </button>

    <div id="results-area" class="hidden mt-8 pt-8 border-t-2 border-gray-200">
        <h2 class="text-2xl font-bold mb-4">Results</h2>
        <p id="score-display" class="text-xl mb-6 font-semibold"></p>
        <div id="feedback-list" class="space-y-6"></div>
        <button onclick="location.reload()" class="mt-8 px-6 py-2 bg-gray-600 text-white rounded hover:bg-gray-700">
            Retake Quiz
        </button>
    </div>
</div>

<script>
(function() {
    // 題目資料庫
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

    const listContainer = document.getElementById('questions-list');
    const submitBtn = document.getElementById('submit-btn');
    const resultsArea = document.getElementById('results-area');
    const scoreDisplay = document.getElementById('score-display');
    const feedbackList = document.getElementById('feedback-list');

    // 1. 渲染所有題目
    questions.forEach((q, qIndex) => {
        const div = document.createElement('div');
        div.className = "question-block";
        div.innerHTML = `
            <p class="font-bold text-lg mb-3">${qIndex + 1}. ${q.q}</p>
            <div class="space-y-2">
                ${q.options.map((opt, oIndex) => `
                    <label class="flex items-center space-x-3 p-3 border rounded hover:bg-gray-50 cursor-pointer">
                        <input type="radio" name="q${qIndex}" value="${oIndex}" class="h-4 w-4 text-blue-600">
                        <span>${opt}</span>
                    </label>
                `).join('')}
            </div>
        `;
        listContainer.appendChild(div);
    });

    // 2. 提交邏輯
    submitBtn.onclick = () => {
        let score = 0;
        const userAnswers = [];

        // 檢查是否全填
        for (let i = 0; i < questions.length; i++) {
            const selected = document.querySelector(`input[name="q${i}"]:checked`);
            if (!selected) return alert(`Please answer question ${i + 1}`);
            userAnswers.push(parseInt(selected.value));
        }

        // 計算分數
        userAnswers.forEach((ans, index) => {
            if (ans === questions[index].answer) score++;
        });

        // 顯示結果
        submitBtn.classList.add('hidden');
        resultsArea.classList.remove('hidden');
        scoreDisplay.innerText = `You scored ${score} out of ${questions.length} (${Math.round((score/questions.length)*100)}%).`;

        // 渲染解析
        feedbackList.innerHTML = '';
        questions.forEach((q, index) => {
            const isCorrect = userAnswers[index] === q.answer;
            const div = document.createElement('div');
            div.className = `p-4 rounded border-l-4 ${isCorrect ? 'bg-green-50 border-green-500' : 'bg-red-50 border-red-500'}`;
            div.innerHTML = `
                <p class="font-bold">Q${index + 1}: ${q.q}</p>
                <p class="mt-2">Your answer: <strong>${q.options[userAnswers[index]]}</strong></p>
                <p class="text-green-700 font-semibold">Correct answer: ${q.options[q.answer]}</p>
                <div class="mt-3 text-gray-700 text-sm border-t pt-2">${q.explanation}</div>
            `;
            feedbackList.appendChild(div);
        });

        // 儲存至 localStorage
        const history = JSON.parse(localStorage.getItem('quiz_history') || '[]');
        history.push({
            date: new Date().toISOString().split('T')[0],
            unit: 'Topic 2: Interdependence',
            score: Math.round((score/questions.length)*100)
        });
        localStorage.setItem('quiz_history', JSON.stringify(history));
        
        // 滾動到結果區
        resultsArea.scrollIntoView({ behavior: 'smooth' });
    };
})();
</script>