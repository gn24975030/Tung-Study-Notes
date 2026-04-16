# Topic 2 Quiz（Q2: Interdependence and Gains from Trade）

**Course (課程)**: Principles of Economics 2026  
**Topic (主題)**: Topic 2: Interdependence and Gains from Trade

---

## Instructions（使用說明）
請為每道題目選擇一個選項，完成後點擊畫面底部的 **「Submit / 提交答案」**。  
（若有未作答的題目，提交時將直接視為答錯）。  
提交後將會顯示正確答案與中英詳解，您的成績也會自動儲存至瀏覽器的學習紀錄中。

<!-- 引入 Tailwind CSS -->
<script src="https://cdn.tailwindcss.com"></script>

<!-- 自訂樣式 (必須頂格寫，避免被當成程式碼區塊) -->
<style>
.radio-custom:checked + label { background-color: #eff6ff; border-color: #3b82f6; box-shadow: 0 0 0 1px #3b82f6; }
.correct-answer { background-color: #dcfce7 !important; border-color: #22c55e !important; color: #166534; }
.wrong-answer { background-color: #fee2e2 !important; border-color: #ef4444 !important; color: #991b1b; }
.explanation { display: none; }
.show-explanation { display: block; animation: fadeIn 0.5s; }
@keyframes fadeIn { from { opacity: 0; transform: translateY(-5px); } to { opacity: 1; transform: translateY(0); } }
</style>

<!-- 主容器 (必須頂格寫) -->
<div class="max-w-4xl mx-auto p-2 md:p-4 text-gray-800">

<!-- 測驗題目容器 -->
<div id="quiz-container" class="bg-white rounded-xl shadow-md border border-gray-200 p-6 md:p-8 mb-24">
<!-- 題目將由 JavaScript 動態生成 -->
</div>

<!-- 底部懸浮按鈕與分數顯示 -->
<div class="fixed bottom-0 left-0 right-0 bg-white/90 backdrop-blur-md border-t border-gray-200 p-4 shadow-[0_-4px_6px_-1px_rgba(0,0,0,0.1)] z-50">
<div class="max-w-4xl mx-auto flex flex-col sm:flex-row justify-between items-center gap-4">
<div id="score-display" class="text-2xl font-bold text-gray-800 hidden">
Score / 得分: <span id="score-value" class="text-blue-600 text-3xl">0</span> <span class="text-gray-500 text-lg">/ 4</span>
</div>
<div class="flex-1"></div>
<div class="flex gap-4 w-full sm:w-auto">
<button id="reset-btn" class="flex-1 sm:flex-none px-8 py-3 bg-gray-200 text-gray-700 rounded-lg hover:bg-gray-300 transition font-bold text-lg hidden">
Retry / 重新測驗
</button>
<button id="submit-btn" class="flex-1 sm:flex-none px-8 py-3 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition font-bold text-lg shadow-md hover:shadow-lg transform hover:-translate-y-0.5">
Submit / 提交答案
</button>
</div>
</div>
</div>

</div>

<!-- JavaScript 邏輯 (必須頂格寫) -->
<script>
const quizData = [
    {
        question: "Assume Zimbabwe and Portugal can switch between producing toothbrushes and producing hairbrushes at a constant rate. In 1 hour: Zimbabwe can produce 20 toothbrushes or 6 hairbrushes. Portugal can produce 12 toothbrushes or 10 hairbrushes. Which country has a comparative advantage in producing toothbrushes?",
        options: ["Zimbabwe", "Portugal", "Neither", "Both"],
        answer: 0,
        expEn: "Zimbabwe should specialize in producing toothbrushes because its opportunity cost of hairbrushes is lower when producing toothbrushes.<br>Opportunity cost (toothbrushes in terms of hairbrushes):<br>Zimbabwe: 6/20 = 0.3 hairbrush/toothbrush<br>Portugal: 10/12 ≈ 0.833 hairbrush/toothbrush",
        expZh: "Zimbabwe 應該專業分工在生產牙刷，因為它在把資源用來生產牙刷時，相對於其他商品的機會成本更低。"
    },
    {
        question: "The following table describes production possibilities (per worker per hour): Boston: 3 red socks (R) and 3 white socks (W). Chicago: 2 red socks (R) and 1 white sock (W). What is the range of prices at which trade can occur? (Price of red socks relative to white socks)",
        options: ["1W ≤ 1R ≤ 2W", "0.5W ≤ 1R ≤ 1W", "1R ≤ 0.5W", "2W ≤ 1R"],
        answer: 1,
        expEn: "The trade can occur when 1R/1W is between the opportunity-cost bounds. Here, the acceptable range is 0.5W ≤ 1R ≤ 1W.",
        expZh: "只要紅襪與白襪的「相對價格」落在雙方都接受的機會成本範圍內，貿易就能發生。本題可行範圍為 0.5W ≤ 1R ≤ 1W。"
    },
    {
        question: "True or False: 'Canada and the U.S. both produce wheat and computer software. Canada is said to have the comparative advantage in producing wheat if Canada requires fewer resources than the U.S. to produce a bushel of wheat.'",
        options: ["True", "False"],
        answer: 1,
        expEn: "False. Fewer resources to produce wheat means absolute advantage, not comparative advantage. Comparative advantage is about having a lower opportunity cost of producing wheat.",
        expZh: "錯。比較資源較少能生產小麥屬於「絕對利益」，不是「比較利益」。比較利益是看生產小麥的機會成本是否更低。"
    },
    {
        question: "True or False: 'Mike can make 4 tables or 20 chairs in one month. His opportunity cost of 1 chair is 1/5 table.'",
        options: ["True", "False"],
        answer: 0,
        expEn: "True. Opportunity cost of 1 chair is the number of tables Mike must give up. Since 20 chairs = 4 tables, 1 chair = 4/20 = 1/5 table.",
        expZh: "正確。1 把椅子的機會成本就是 Mike 需要放棄多少桌子。因為 20 把椅子 = 4 張桌子，所以 1 把椅子 = 4/20 = 1/5 桌。"
    }
];

let userAnswers = new Array(quizData.length).fill(null);

document.addEventListener('DOMContentLoaded', () => {
    renderQuiz();
    document.getElementById('submit-btn').addEventListener('click', submitQuiz);
    document.getElementById('reset-btn').addEventListener('click', resetQuiz);
});

function renderQuiz() {
    const container = document.getElementById('quiz-container');
    container.innerHTML = '';

    quizData.forEach((q, qIndex) => {
        const qDiv = document.createElement('div');
        qDiv.className = 'mb-10 pb-8 border-b border-gray-100 last:border-0 last:pb-0 last:mb-0';
        
        const qTitle = document.createElement('h3');
        qTitle.className = 'text-lg md:text-xl font-semibold mb-5 text-gray-800 leading-relaxed';
        qTitle.innerHTML = `
            <div class="flex items-start">
                <span class="text-blue-600 mr-3 mt-1 text-xl font-bold">Q${qIndex + 1}.</span>
                <div>${q.question}</div>
            </div>
        `;
        qDiv.appendChild(qTitle);

        const optionsGrid = document.createElement('div');
        optionsGrid.className = 'grid grid-cols-1 gap-3 ml-0 md:ml-10';
        
        q.options.forEach((opt, oIndex) => {
            const optId = `q${qIndex}_o${oIndex}`;
            const wrapper = document.createElement('div');
            wrapper.className = 'relative';

            const input = document.createElement('input');
            input.type = 'radio';
            input.name = `q${qIndex}`;
            input.id = optId;
            input.value = oIndex;
            input.className = 'peer hidden radio-custom';
            
            if (userAnswers[qIndex] === oIndex) {
                input.checked = true;
            }

            input.onchange = () => { 
                userAnswers[qIndex] = oIndex; 
            };

            const label = document.createElement('label');
            label.htmlFor = optId;
            label.className = 'block p-4 border border-gray-200 rounded-xl cursor-pointer transition-all hover:bg-gray-50 peer-checked:bg-blue-50 peer-checked:border-blue-500';
            label.innerHTML = `
                <div class="flex items-center">
                    <div class="w-6 h-6 rounded-full border-2 border-gray-300 mr-4 flex-shrink-0 peer-checked:border-blue-500 peer-checked:bg-blue-500 flex items-center justify-center transition-colors">
                        <div class="w-2.5 h-2.5 rounded-full bg-white opacity-0 peer-checked:opacity-100"></div>
                    </div>
                    <div class="font-medium text-gray-700 text-base">${opt}</div>
                </div>
            `;

            const styleFix = document.createElement('style');
            styleFix.innerHTML = `
                #${optId}:checked ~ label .w-6 { border-color: #3b82f6; background-color: #3b82f6; }
                #${optId}:checked ~ label .w-2\\.5 { opacity: 1; }
            `;
            wrapper.appendChild(styleFix);

            wrapper.appendChild(input);
            wrapper.appendChild(label);
            optionsGrid.appendChild(wrapper);
        });
        
        qDiv.appendChild(optionsGrid);

        const expBox = document.createElement('div');
        expBox.id = `exp_q${qIndex}`;
        expBox.className = 'explanation mt-6 ml-0 md:ml-10 p-5 bg-blue-50 border-l-4 border-blue-500 rounded-r-xl text-gray-800 shadow-sm';
        expBox.innerHTML = `
            <div class="flex items-center mb-3 text-blue-800">
                <svg class="w-5 h-5 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path></svg>
                <strong class="text-lg">Explanation / 題解:</strong>
            </div>
            <p class="mb-3 text-base leading-relaxed">${q.expEn}</p>
            <div class="border-t border-blue-200 pt-3 mt-3">
                <p class="text-gray-700 text-sm leading-relaxed"><span class="font-bold">中文：</span>${q.expZh}</p>
            </div>
        `;
        qDiv.appendChild(expBox);

        container.appendChild(qDiv);
    });
}

function submitQuiz() {
    let score = 0;
    const total = quizData.length;

    quizData.forEach((q, qIndex) => {
        const selectedOptIndex = userAnswers[qIndex];
        const optionsDivs = document.querySelectorAll(`input[name="q${qIndex}"] + label`);
        const inputs = document.querySelectorAll(`input[name="q${qIndex}"]`);
        
        inputs.forEach(input => input.disabled = true);

        const isCorrect = (selectedOptIndex === q.answer);
        if (isCorrect) score++;

        q.options.forEach((opt, oIndex) => {
            if (oIndex === q.answer) {
                optionsDivs[oIndex].classList.add('correct-answer');
                optionsDivs[oIndex].innerHTML += `<svg class="w-6 h-6 text-green-600 absolute right-4 top-1/2 transform -translate-y-1/2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path></svg>`;
            } else if (selectedOptIndex !== null && oIndex === selectedOptIndex && !isCorrect) {
                optionsDivs[oIndex].classList.add('wrong-answer');
                optionsDivs[oIndex].innerHTML += `<svg class="w-6 h-6 text-red-500 absolute right-4 top-1/2 transform -translate-y-1/2" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path></svg>`;
            }
        });

        document.getElementById(`exp_q${qIndex}`).classList.add('show-explanation');
    });

    const timestamp = new Date().toLocaleString();
    const newResult = { topic: "Topic 2: Interdependence", score: score, total: total, date: timestamp };
    const history = JSON.parse(localStorage.getItem('study_results') || '[]');
    history.push(newResult);
    localStorage.setItem('study_results', JSON.stringify(history));

    document.getElementById('score-value').innerText = score;
    document.getElementById('score-display').classList.remove('hidden');
    document.getElementById('submit-btn').classList.add('hidden');
    document.getElementById('reset-btn').classList.remove('hidden');
    
    setTimeout(() => {
        alert(`測驗完成！得分：${score}/${total}。\n成績已儲存至系統。`);
    }, 100);

    window.scrollTo({ top: 0, behavior: 'smooth' });
}

function resetQuiz() {
    userAnswers = new Array(quizData.length).fill(null);
    renderQuiz();
    
    document.getElementById('score-display').classList.add('hidden');
    document.getElementById('submit-btn').classList.remove('hidden');
    document.getElementById('reset-btn').classList.add('hidden');
    
    window.scrollTo({ top: 0, behavior: 'smooth' });
}
</script>