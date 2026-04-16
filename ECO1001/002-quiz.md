<!-- 002-quiz.md：互動測驗頁（SUBMIT後才顯示答案），問題與選項皆全英文；答案與題解才中英對照 -->
<!-- 注意：本頁包含原生 JS 互動功能，直接可在 Docsify 使用 executeScript。 -->
<!-- QUIZ layout / spacing widen fix -->
<style>
  .quiz-block{
    max-width: 920px;
    margin-top: 12px;
  }

  .quiz-block label{
    display: block;
    margin: 7px 0;
    line-height: 1.45;
    padding-left: 2px;
  }

  .quiz-explain{
    max-width: 980px !important;
    width: calc(100% - 32px) !important;
    margin-left: auto;
    margin-right: auto;
    box-sizing: border-box;
  }

  .quiz-expl{
    overflow-wrap: anywhere;
    word-break: break-word;
  }

  .quiz-explain pre,
  .quiz-explain code{
    max-width: 100%;
    white-space: normal;
    overflow: auto;
    word-break: break-word;
  }

  #quiz-result{
    max-width: 980px;
    width: calc(100% - 32px);
    margin-left: auto;
    margin-right: auto;
    box-sizing: border-box;
  }

  #btn-submit{
    margin-top: 14px;
  }
</style>
# Topic 2 Quiz（Q2: Interdependence and Gains from Trade）

**Course (課程)**: Principles of Economics 2026  
**Topic (主題)**: Topic 2: Interdependence and Gains from Trade

---

## Instructions（使用說明）
Pick one option for each question, then press **SUBMIT**.  
After submitting, the correct answers and explanations (with bilingual text) will appear.

---

<!-- ========= Question 1 ========= -->
## Question 1
**Assume Zimbabwe and Portugal can switch between producing toothbrushes and producing hairbrushes at a constant rate.**

In 1 hour:
- Zimbabwe can produce **20 toothbrushes** or **6 hairbrushes**.
- Portugal can produce **12 toothbrushes** or **10 hairbrushes**.

**(Q1a)** Which country has a comparative advantage in producing **toothbrushes**?
<!-- options for Q1a -->
<div class="quiz-block" data-qid="q1a" data-type="radio" style="margin-top:12px;">
  <label><input type="radio" name="q1a" value="A" /> A) Zimbabwe</label><br/>
  <label><input type="radio" name="q1a" value="B" /> B) Portugal</label><br/>
  <label><input type="radio" name="q1a" value="C" /> C) Neither</label><br/>
  <label><input type="radio" name="q1a" value="D" /> D) Both</label>
</div>

<div id="ex-q1a" class="quiz-explain" style="display:none; margin-top:10px; padding:10px; border:1px solid #e5e7eb; border-radius:8px;">
  <div class="quiz-correct" style="font-weight:700; margin-bottom:6px;"></div>
  <div class="quiz-expl">
    <div class="bilingual" style="margin-bottom:6px;">
      <div><b>English (Answer & Explanation)</b>: Zimbabwe should specialize in producing toothbrushes because its opportunity cost of hairbrushes is lower when producing toothbrushes.</div>
      <div style="margin-top:4px;"><b>中文（答案與題解）</b>：Zimbabwe 應該專業分工在生產牙刷，因為它在把資源用來生產牙刷時，相對於其他商品的機會成本更低。</div>
    </div>
    <div style="font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 12px; background:#f9fafb; padding:8px; border-radius:6px;">
      Opportunity cost (toothbrushes in terms of hairbrushes):
      <br/>Zimbabwe: \( \frac{6}{20} = 0.3 \) hairbrush per toothbrush
      <br/>Portugal: \( \frac{10}{12} \approx 0.833 \) hairbrush per toothbrush
      <br/>Lower opportunity cost ⇒ comparative advantage.
    </div>
  </div>
</div>

---

<!-- ========= Question 2 ========= -->
## Question 2
The following table describes production possibilities (per worker per hour):

- **Boston**: 3 red socks (R) and 3 white socks (W)  
- **Chicago**: 2 red socks (R) and 1 white sock (W)

**(Q2d)** What is the range of prices at which trade can occur?

Assume price of red socks is measured relative to white socks.

<div class="quiz-block" data-qid="q2d" data-type="radio" style="margin-top:12px;">
  <label><input type="radio" name="q2d" value="A" /> A) \(1W \le 1R \le 2W\)</label><br/>
  <label><input type="radio" name="q2d" value="B" /> B) \(0.5W \le 1R \le 1W\)</label><br/>
  <label><input type="radio" name="q2d" value="C" /> C) \(1R \le 0.5W\)</label><br/>
  <label><input type="radio" name="q2d" value="D" /> D) \(2W \le 1R\)</label>
</div>

<div id="ex-q2d" class="quiz-explain" style="display:none; margin-top:10px; padding:10px; border:1px solid #e5e7eb; border-radius:8px;">
  <div class="quiz-correct" style="font-weight:700; margin-bottom:6px;"></div>
  <div class="quiz-expl">
    <div class="bilingual" style="margin-bottom:6px;">
      <div><b>English (Answer & Explanation)</b>: The trade can occur when \( \frac{1R}{1W} \) is between the opportunity-cost bounds. Here, the acceptable range is \(1W \le 1R \le 2W\).</div>
      <div style="margin-top:4px;"><b>中文（答案與題解）</b>：只要紅襪與白襪的「相對價格」落在雙方都接受的機會成本範圍內，貿易就能發生。本題可行範圍為 \(1W \le 1R \le 2W\)。</div>
    </div>
    <div style="font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 12px; background:#f9fafb; padding:8px; border-radius:6px;">
      Boston: Output per hour: R=3, W=3 ⇒ opportunity cost of 1R is 1W
      <br/>Chicago: Output per hour: R=2, W=1 ⇒ opportunity cost of 1R is 0.5W
      <br/>So trade price must satisfy: Boston accepts ≥ 1W per 1R, Chicago accepts ≤ 2R per 1W
      <br/>Equivalent acceptable range: \(1W \le 1R \le 2W\).
    </div>
  </div>
</div>

---

<!-- ========= Question 3 ========= -->
## Question 3
**True or False**

"Canada and the U.S. both produce wheat and computer software. Canada is said to have the comparative advantage in producing wheat if Canada requires fewer resources than the U.S. to produce a bushel of wheat."

<div class="quiz-block" data-qid="q3" data-type="radio" style="margin-top:12px;">
  <label><input type="radio" name="q3" value="A" /> A) True</label><br/>
  <label><input type="radio" name="q3" value="B" /> B) False</label>
</div>

<div id="ex-q3" class="quiz-explain" style="display:none; margin-top:10px; padding:10px; border:1px solid #e5e7eb; border-radius:8px;">
  <div class="quiz-correct" style="font-weight:700; margin-bottom:6px;"></div>
  <div class="quiz-expl">
    <div class="bilingual" style="margin-bottom:6px;">
      <div><b>English (Answer & Explanation)</b>: False. Fewer resources to produce wheat means absolute advantage, not comparative advantage. Comparative advantage is about having a lower opportunity cost of producing wheat.</div>
      <div style="margin-top:4px;"><b>中文（答案與題解）</b>：錯。比較資源較少能生產小麥屬於「絕對利益」，不是「比較利益」。比較利益是看生產小麥的機會成本是否更低。</div>
    </div>
  </div>
</div>

---

<!-- ========= Question 4 ========= -->
## Question 4
**True or False**

"Mike can make 4 tables or 20 chairs in one month. His opportunity cost of 1 chair is 1/5 table."

<div class="quiz-block" data-qid="q4" data-type="radio" style="margin-top:12px;">
  <label><input type="radio" name="q4" value="A" /> A) True</label><br/>
  <label><input type="radio" name="q4" value="B" /> B) False</label>
</div>

<div id="ex-q4" class="quiz-explain" style="display:none; margin-top:10px; padding:10px; border:1px solid #e5e7eb; border-radius:8px;">
  <div class="quiz-correct" style="font-weight:700; margin-bottom:6px;"></div>
  <div class="quiz-expl">
    <div class="bilingual" style="margin-bottom:6px;">
      <div><b>English (Answer & Explanation)</b>: True. Opportunity cost of 1 chair is the number of tables Mike must give up. Since 20 chairs = 4 tables, 1 chair = 4/20 = 1/5 table.</div>
      <div style="margin-top:4px;"><b>中文（答案與題解）</b>：正確。1 把椅子的機會成本就是 Mike 需要放棄多少桌子。因為 20 把椅子 = 4 張桌子，所以 1 把椅子 = 4/20 = 1/5 桌。</div>
    </div>
    <div style="font-family: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, 'Liberation Mono', 'Courier New', monospace; font-size: 12px; background:#f9fafb; padding:8px; border-radius:6px;">
      \(\text{tables per chair} = \frac{4}{20} = \frac{1}{5}\)
    </div>
  </div>
</div>

---

## Submit（提交）
<button id="btn-submit" type="button" style="margin-top:14px; padding:10px 14px; border:none; border-radius:8px; background:#2563eb; color:white; cursor:pointer;">
  SUBMIT
</button>

<div id="quiz-result" style="margin-top:12px; display:none; padding:10px; border-radius:8px; border:1px solid #e5e7eb;"></div>

<script>
(function () {
  const ANSWERS = {
    q1a: "A",
    q2d: "A",
    q3: "B",
    q4: "A"
  };

  const EXPL_IDS = {
    q1a: "ex-q1a",
    q2d: "ex-q2d",
    q3: "ex-q3",
    q4: "ex-q4"
  };

  const btn = document.getElementById("btn-submit");
  const resultBox = document.getElementById("quiz-result");

  function getSelectedValue(name) {
    const checked = document.querySelector('input[name="' + name + '"]:checked');
    return checked ? checked.value : null;
  }

  function showExplain(qid) {
    const ex = document.getElementById(EXPL_IDS[qid]);
    if (!ex) return;
    ex.style.display = "block";
    const correct = ANSWERS[qid];
    const correctText = "Correct answer: " + correct + ".";
    const el = ex.querySelector(".quiz-correct");
    if (el) el.textContent = correctText;
  }

  function markChosenStyle(qid, chosen, correct) {
    const container = document.querySelector('.quiz-block[data-qid="' + qid + '"]');
    if (!container) return;

    const inputs = container.querySelectorAll('input[type="radio"][name="' + qid + '"]');
    inputs.forEach(inp => {
      const label = inp.closest("label");
      if (!label) return;

      label.style.opacity = "1";
      label.style.fontWeight = "400";
      label.style.background = "transparent";
      label.style.padding = "0";
    });

    inputs.forEach(inp => {
      const label = inp.closest("label");
      if (!label) return;

      if (inp.value === chosen && chosen !== correct) {
        label.style.background = "#fef2f2";
        label.style.borderRadius = "6px";
        label.style.padding = "6px 8px";
        label.style.margin = "4px 0";
      }
      if (inp.value === correct) {
        label.style.background = "#ecfccb";
        label.style.borderRadius = "6px";
        label.style.padding = "6px 8px";
        label.style.margin = "4px 0";
        label.style.fontWeight = "700";
      }
    });
  }

  btn.addEventListener("click", function () {
    const qids = Object.keys(ANSWERS);

    // validation
    for (const qid of qids) {
      const chosen = getSelectedValue(qid);
      if (chosen === null) {
        resultBox.style.display = "block";
        resultBox.style.borderColor = "#fca5a5";
        resultBox.style.background = "#fef2f2";
        resultBox.innerHTML = "<b>Please answer all questions before submitting.</b>";
        return;
      }
    }

    // score
    let score = 0;
    for (const qid of qids) {
      const chosen = getSelectedValue(qid);
      const correct = ANSWERS[qid];
      if (chosen === correct) score++;

      showExplain(qid);
      markChosenStyle(qid, chosen, correct);
    }

    const total = qids.length;
    resultBox.style.display = "block";
    resultBox.style.borderColor = "#d1d5db";
    resultBox.style.background = "#f9fafb";
    resultBox.innerHTML = "<b>Score:</b> " + score + " / " + total + ".";
  });
})();
</script>