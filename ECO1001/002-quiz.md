# Topic 2 Quiz（Q2: Interdependence and Gains from Trade）

**Course (課程)**: Principles of Economics 2026  
**Topic (主題)**: Topic 2: Interdependence and Gains from Trade

---

## Instructions（使用說明）
Pick one option for each question, then press **SUBMIT**.  
After submitting, the correct answers and explanations (with bilingual text) will appear.

<div id="quiz-container"></div>

<script>
const quizData = [
    {
        question: "Assume Zimbabwe and Portugal can switch between producing toothbrushes and producing hairbrushes at a constant rate. In 1 hour: Zimbabwe can produce 20 toothbrushes or 6 hairbrushes. Portugal can produce 12 toothbrushes or 10 hairbrushes. Which country has a comparative advantage in producing toothbrushes?",
        options: ["Zimbabwe", "Portugal", "Neither", "Both"],
        answer: 0,
        explanation: "Zimbabwe should specialize in producing toothbrushes because its opportunity cost of hairbrushes is lower when producing toothbrushes.<br>Opportunity cost (toothbrushes in terms of hairbrushes):<br>Zimbabwe: 6/20 = 0.3 hairbrush/toothbrush<br>Portugal: 10/12 ≈ 0.833 hairbrush/toothbrush<br>---<br>中文：Zimbabwe 應該專業分工在生產牙刷，因為它在把資源用來生產牙刷時，相對於其他商品的機會成本更低。"
    },
    {
        question: "The following table describes production possibilities (per worker per hour): Boston: 3 red socks (R) and 3 white socks (W). Chicago: 2 red socks (R) and 1 white sock (W). What is the range of prices at which trade can occur? (Price of red socks relative to white socks)",
        options: ["1W ≤ 1R ≤ 2W", "0.5W ≤ 1R ≤ 1W", "1R ≤ 0.5W", "2W ≤ 1R"],
        answer: 1,
        explanation: "The trade can occur when 1R/1W is between the opportunity-cost bounds. Here, the acceptable range is 0.5W ≤ 1R ≤ 1W.<br>---<br>中文：只要紅襪與白襪的「相對價格」落在雙方都接受的機會成本範圍內，貿易就能發生。本題可行範圍為 0.5W ≤ 1R ≤ 1W。"
    },
    {
        question: "True or False: 'Canada and the U.S. both produce wheat and computer software. Canada is said to have the comparative advantage in producing wheat if Canada requires fewer resources than the U.S. to produce a bushel of wheat.'",
        options: ["True", "False"],
        answer: 1,
        explanation: "False. Fewer resources to produce wheat means absolute advantage, not comparative advantage. Comparative advantage is about having a lower opportunity cost of producing wheat.<br>---<br>中文：錯。比較資源較少能生產小麥屬於「絕對利益」，不是「比較利益」。比較利益是看生產小麥的機會成本是否更低。"
    },
    {
        question: "True or False: 'Mike can make 4 tables or 20 chairs in one month. His opportunity cost of 1 chair is 1/5 table.'",
        options: ["True", "False"],
        answer: 0,
        explanation: "True. Opportunity cost of 1 chair is the number of tables Mike must give up. Since 20 chairs = 4 tables, 1 chair = 4/20 = 1/5 table.<br>---<br>中文：正確。1 把椅子的機會成本就是 Mike 需要放棄多少桌子。因為 20 把椅子 = 4 張桌子，所以 1 把椅子 = 4/20 = 1/5 桌。"
    }
];

function renderQuiz() {
    const container = document.getElementById('quiz-container');
    container.innerHTML = '';
    quizData.forEach((q, index) => {
        const div = document.createElement('div');
        div.className = 'quiz-question my-4 p-4 border rounded';
        div.innerHTML = `
            <p class="font-bold">${index + 1}. ${q.question}</p>
            ${q.options.map((opt, i) => `
                <label class="block my-2">
                    <input type="radio" name="q${index}" value="${i}"> ${opt}
                </label>
            `).join('')}
            <div id="result${index}" class="hidden mt-2 p-2 bg-gray-100 rounded"></div>
        `;
        container.appendChild(div);
    });
    container.innerHTML += `<button onclick="submitQuiz()" class="bg-blue-500 text-white px-4 py-2 rounded mt-4">SUBMIT</button>`;
}

function submitQuiz() {
    quizData.forEach((q, index) => {
        const selected = document.querySelector(`input[name="q${index}"]:checked`);
        const resultDiv = document.getElementById(`result${index}`);
        resultDiv.classList.remove('hidden');
        if (selected && parseInt(selected.value) === q.answer) {
            resultDiv.innerHTML = "✅ Correct!<br>" + q.explanation;
            resultDiv.classList.add('bg-green-100');
        } else {
            resultDiv.innerHTML = "❌ Incorrect. The correct answer was: " + q.options[q.answer] + "<br>" + q.explanation;
            resultDiv.classList.add('bg-red-100');
        }
    });
}

renderQuiz();
</script>