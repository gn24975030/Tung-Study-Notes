# 學習成績總覽 (My Progress)

這裡顯示你所有測驗的歷史紀錄。

<div id="results-table"></div>

<button onclick="clearResults()" class="bg-red-500 text-white px-4 py-2 rounded mt-4">清除所有紀錄</button>

<script>
function loadResults() {
    const tableDiv = document.getElementById('results-table');
    const history = JSON.parse(localStorage.getItem('study_results') || '[]');
    
    if (history.length === 0) {
        tableDiv.innerHTML = "<p>目前沒有測驗紀錄。</p>";
        return;
    }
    
    let html = `
        <table class="w-full border-collapse border border-gray-300 mt-4">
            <thead>
                <tr class="bg-gray-100">
                    <th class="border p-2">日期</th>
                    <th class="border p-2">單元</th>
                    <th class="border p-2">分數</th>
                </tr>
            </thead>
            <tbody>
    `;
    
    history.forEach(item => {
        html += `
            <tr>
                <td class="border p-2">${item.date}</td>
                <td class="border p-2">${item.topic}</td>
                <td class="border p-2 text-center">${item.score} / ${item.total}</td>
            </tr>
        `;
    });
    
    html += `</tbody></table>`;
    tableDiv.innerHTML = html;
}

function clearResults() {
    if (confirm("確定要清除所有紀錄嗎？")) {
        localStorage.removeItem('study_results');
        loadResults();
    }
}

// 頁面載入時執行
loadResults();
</script>