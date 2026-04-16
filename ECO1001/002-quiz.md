# Topic 2 Quiz（Q2: Interdependence and Gains from Trade）

**Course (課程)**: Principles of Economics 2026  
**Topic (主題)**: Topic 2: Interdependence and Gains from Trade

---

## Instructions（使用說明）
請為每道題目選擇一個選項，完成後點擊題目底部的 **「Submit / 提交答案」**。  
（若有未作答的題目，提交時將直接視為答錯）。  
提交後將會顯示正確答案與中英詳解，您的成績也會自動儲存至瀏覽器的學習紀錄中。

<script src="https://cdn.tailwindcss.com"></script>

<style>
.correct-bg { background-color: #dcfce7 !important; border-color: #22c55e !important; }
.wrong-bg { background-color: #fee2e2 !important; border-color: #ef4444 !important; }
.explanation { display: none; }
.show-explanation { display: block; margin-top: 10px; padding: 12px; background-color: #f0f9ff; border-left: 4px solid #3b82f6; border-radius: 4px; }
</style>

<div id="quiz-container" class="my-6">
<!-- 題目將由 JS 動態生成 -->
</div>

<div class="flex items-center gap-4 mb-12">
<button id="submit-btn" class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-6 rounded transition-colors">
Submit / 提交答案
</button>
<button id="reset-btn" class="bg-gray-500 hover:bg-gray-600 text-white font-bold py-2 px-6 rounded transition-colors hidden">
Retry / 重新測驗
</button>
<div id="score-display" class="text-xl font-bold hidden">
Score / 得分: <span id="score-value" class="text-blue-600 text-2xl">0</span> / 4
</div>
</div>

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
qDiv.className = 'mb-8 p-4 border border-gray-200 rounded bg-white shadow-sm';

const qTitle = document.createElement('p');
qTitle.className = 'font-bold text-lg mb-3';
qTitle.innerHTML = `${qIndex + 1}. ${q.question}`;
qDiv.appendChild(qTitle);

q.options.forEach((opt, oIndex) => {
const label = document.createElement('label');
label.className = 'block my-2 p-2 border border-gray-100 rounded cursor-pointer hover:bg-gray-50';
label.id = `label_q${qIndex}_o${oIndex}`;

const input = document.createElement('input');
input.type = 'radio';
input.name = `q${qIndex}`;
input.value = oIndex;
input.className = 'mr-2';

if (userAnswers[qIndex] === oIndex) {
input.checked = true;
}

input.onchange = () => { 
userAnswers[qIndex] = oIndex; 
};

label.appendChild(input);
label.appendChild(document.createTextNode(opt));
qDiv.appendChild(label);
});

const expBox = document.createElement('div');
expBox.id = `exp_q${qIndex}`;
expBox.className = 'explanation';
expBox.innerHTML = `
<strong>Explanation / 題解:</strong><br>
<span class="text-sm">${q.expEn}</span><br>
<hr class="my-2 border-blue-200">
<span class="text-sm text-gray-700"><strong>中文：</strong>${q.expZh}</span>
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
const inputs = document.querySelectorAll(`input[name="q${qIndex}"]`);

inputs.forEach(input => input.disabled = true);

const isCorrect = (selectedOptIndex === q.answer);
if (isCorrect) score++;

q.options.forEach((opt, oIndex) => {
const label = document.getElementById(`label_q${qIndex}_o${oIndex}`);
if (oIndex === q.answer) {
label.classList.add('correct-bg');
} else if (selectedOptIndex !== null && oIndex === selectedOptIndex && !isCorrect) {
label.classList.add('wrong-bg');
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

alert(`測驗完成！得分：${score}/${total}。\n成績已儲存至系統。`);
}

function resetQuiz() {
userAnswers = new Array(quizData.length).fill(null);
renderQuiz();

document.getElementById('score-display').classList.add('hidden');
document.getElementById('submit-btn').classList.remove('hidden');
document.getElementById('reset-btn').classList.add('hidden');
}
</script>