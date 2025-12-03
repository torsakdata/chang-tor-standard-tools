<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8" />
  <title>คำนวณช่องไฟระแนง (cm) - ช่างต่อมีสไตล์ได้มาตรฐาน</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    * {
      box-sizing: border-box;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
    }

    body {
      margin: 0;
      padding: 0;
      background: #0b1120; /* navy เข้มด้านหลัง */
      display: flex;
      justify-content: center;
      min-height: 100vh;
    }

    .app {
      width: 100%;
      max-width: 900px;
      padding: 16px 12px 32px;
    }

    @media (min-width: 768px) {
      .app {
        padding: 24px 16px 40px;
      }
    }

    /* โลโก้ / แบรนด์ */
    .logo {
      text-align: center;
      margin-bottom: 18px;
    }

    .logo-badge {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 6px 12px;
      border-radius: 999px;
      background: rgba(248, 250, 252, 0.06);
      border: 1px solid rgba(148, 163, 184, 0.4);
      margin-bottom: 8px;
    }

    .logo-badge-dot {
      width: 8px;
      height: 8px;
      border-radius: 999px;
      background: #f97316; /* ส้มแบรนด์ */
      box-shadow: 0 0 0 4px rgba(249, 115, 22, 0.25);
    }

    .logo-badge-text {
      font-size: 0.75rem;
      color: #e5e7eb;
      letter-spacing: 0.08em;
      text-transform: uppercase;
    }

    .logo-title {
      font-size: 1.9rem;
      font-weight: 800;
      margin: 0;
      background: linear-gradient(120deg, #f97316, #facc15);
      -webkit-background-clip: text;
      color: transparent;
      letter-spacing: 0.04em;
    }

    .logo-sub {
      margin: 6px 0 0;
      font-size: 0.9rem;
      color: #9ca3af;
    }

    /* การ์ดหลัก */
    .card {
      background: radial-gradient(circle at top left, rgba(148, 163, 184, 0.22), rgba(15, 23, 42, 0.96));
      border-radius: 18px;
      padding: 18px 16px 18px;
      border: 1px solid rgba(148, 163, 184, 0.35);
      box-shadow:
        0 18px 45px rgba(15, 23, 42, 0.9),
        0 0 0 1px rgba(15, 23, 42, 0.9);
      margin-bottom: 14px;
      backdrop-filter: blur(18px);
    }

    @media (min-width: 768px) {
      .card {
        padding: 20px 20px 20px;
        margin-bottom: 18px;
      }
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-start;
      margin-bottom: 12px;
      gap: 8px;
    }

    .card-title {
      font-size: 1.1rem;
      font-weight: 700;
      color: #e5e7eb;
    }

    .card-note {
      font-size: 0.75rem;
      color: #9ca3af;
      text-align: right;
      flex-shrink: 0;
    }

    .grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
    }

    @media (max-width: 640px) {
      .grid {
        grid-template-columns: 1fr;
      }
    }

    label {
      font-size: 0.84rem;
      font-weight: 600;
      color: #e5e7eb;
      display: block;
      margin-bottom: 4px;
    }

    .hint {
      font-size: 0.75rem;
      color: #9ca3af;
      margin-top: 2px;
    }

    input[type="number"] {
      width: 100%;
      padding: 8px 10px;
      border-radius: 10px;
      border: 1px solid #374151;
      font-size: 0.92rem;
      outline: none;
      background: rgba(15, 23, 42, 0.9);
      color: #f9fafb;
      transition: border-color 0.15s ease, box-shadow 0.15s ease, background 0.15s ease, transform 0.06s ease;
    }

    input[type="number"]::placeholder {
      color: #6b7280;
    }

    input[type="number"]:focus {
      border-color: #f97316;
      box-shadow: 0 0 0 1px rgba(249, 115, 22, 0.3);
      background: #020617;
      transform: translateY(-1px);
    }

    .btn-row {
      margin-top: 14px;
      display: flex;
      flex-wrap: wrap;
      gap: 8px;
    }

    @media (max-width: 640px) {
      .btn-row {
        flex-direction: column;
      }

      .btn-row button {
        width: 100%;
        justify-content: center;
      }
    }

    button {
      border: none;
      border-radius: 999px;
      padding: 8px 16px;
      font-size: 0.9rem;
      font-weight: 600;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: transform 0.08s ease, box-shadow 0.12s ease, background 0.15s ease, opacity 0.15s ease;
      white-space: nowrap;
    }

    .btn-primary {
      background: linear-gradient(135deg, #f97316, #facc15);
      color: #111827;
      box-shadow: 0 10px 25px rgba(249, 115, 22, 0.45);
    }

    .btn-primary:hover {
      transform: translateY(-1px);
      box-shadow: 0 14px 32px rgba(249, 115, 22, 0.6);
    }

    .btn-secondary {
      background: rgba(15, 23, 42, 0.9);
      color: #e5e7eb;
      border: 1px solid #4b5563;
    }

    .btn-secondary:hover {
      background: rgba(17, 24, 39, 1);
      transform: translateY(-1px);
    }

    .btn-copy {
      background: rgba(15, 23, 42, 0.96);
      color: #e5e7eb;
      border: 1px dashed #6b7280;
      font-size: 0.8rem;
      padding: 6px 12px;
      box-shadow: none;
    }

    .btn-copy:hover {
      background: #020617;
      border-style: solid;
      transform: translateY(-1px);
    }

    .btn-icon {
      font-size: 1rem;
      line-height: 1;
    }

    .result-box {
      margin-top: 12px;
      padding: 10px 12px;
      border-radius: 12px;
      background: radial-gradient(circle at top left, rgba(15, 23, 42, 0.1), rgba(15, 23, 42, 0.9));
      border: 1px solid rgba(148, 163, 184, 0.5);
      font-size: 0.9rem;
      color: #e5e7eb;
    }

    .result-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      gap: 6px;
      margin-bottom: 4px;
    }

    .result-title {
      font-weight: 700;
      font-size: 0.9rem;
      color: #e5e7eb;
    }

    .result-value {
      font-size: 1.24rem;
      font-weight: 800;
      color: #facc15;
      margin-top: 2px;
      word-break: break-all;
    }

    .copy-msg {
      margin-top: 4px;
      font-size: 0.75rem;
      color: #22c55e;
      display: none;
    }

    .copy-msg.error {
      color: #f97373;
    }

    .error {
      margin-top: 8px;
      font-size: 0.8rem;
      color: #fecaca;
    }

    .footer-note {
      margin-top: 10px;
      font-size: 0.75rem;
      color: #6b7280;
      text-align: right;
    }

    @media (max-width: 640px) {
      .footer-note {
        text-align: center;
        margin-top: 14px;
      }
    }
  </style>
</head>
<body>
  <div class="app">
    <!-- LOGO / BRAND -->
    <div class="logo">
      <div class="logo-badge">
        <div class="logo-badge-dot"></div>
        <div class="logo-badge-text">Chang Tor Standard Tools</div>
      </div>
      <p class="logo-title">ช่างต่อมีสไตล์ได้มาตรฐาน</p>
      <p class="logo-sub">เครื่องมือคำนวณงานระแนง หน้างานจริง หน่วยเซนติเมตร (cm)</p>
    </div>

    <!-- CARD 1: คำนวณช่องไฟ -->
    <div class="card">
      <div class="card-header">
        <div class="card-title">คำนวณช่องไฟระแนง (G)</div>
        <div class="card-note">
          สูตร: G = (W − B×N) / (N − 1)<br />
          หน่วย: เซนติเมตร (cm)
        </div>
      </div>

      <div class="grid">
        <div>
          <label for="widthArea1">ความกว้างพื้นที่ทั้งหมด (W) – cm</label>
          <input type="number" id="widthArea1" step="0.01" min="0" placeholder="เช่น 300">
          <div class="hint">วัดจากผนังถึงผนัง หรือระยะระแนงที่จะติดตั้ง</div>
        </div>
        <div>
          <label for="slatWidth1">ความกว้างไม้ระแนง (B) – cm</label>
          <input type="number" id="slatWidth1" step="0.01" min="0" placeholder="เช่น 5">
          <div class="hint">ใช้ความกว้างจริงของไม้ระแนงที่ซื้อมา</div>
        </div>
        <div>
          <label for="slatCount1">จำนวนไม้ระแนง (N)</label>
          <input type="number" id="slatCount1" step="1" min="1" placeholder="เช่น 15">
          <div class="hint">จำนวนแผ่นที่ตั้งใจจะติดตั้ง</div>
        </div>
      </div>

      <div class="btn-row">
        <button class="btn-primary" onclick="calcGap()">
          <span class="btn-icon">📐</span> คำนวณช่องไฟ
        </button>
        <button class="btn-secondary" onclick="resetGapForm()">
          ล้างค่า
        </button>
      </div>

      <div id="gapError" class="error"></div>

      <div id="gapResult" class="result-box" style="display:none;">
        <div class="result-header">
          <div class="result-title">ผลลัพธ์ช่องไฟระแนง</div>
          <button class="btn-copy" type="button" onclick="copyGapResult()">
            <span class="btn-icon">📋</span> คัดลอกผลลัพธ์
          </button>
        </div>
        <div class="result-value" id="gapValue"></div>
        <div class="hint">ช่องไฟนี้จะเท่ากันทุกช่องระหว่างไม้แต่ละแผ่น</div>
        <div id="gapCopyMsg" class="copy-msg"></div>
      </div>
    </div>

    <!-- CARD 2: คำนวณจำนวนแผ่น -->
    <div class="card">
      <div class="card-header">
        <div class="card-title">คำนวณจำนวนไม้ระแนงที่ใส่ได้ (N)</div>
        <div class="card-note">
          สูตร: N = (W + G) / (B + G)<br />
          หน่วย: เซนติเมตร (cm)
        </div>
      </div>

      <div class="grid">
        <div>
          <label for="widthArea2">ความกว้างพื้นที่ทั้งหมด (W) – cm</label>
          <input type="number" id="widthArea2" step="0.01" min="0" placeholder="เช่น 300">
        </div>
        <div>
          <label for="slatWidth2">ความกว้างไม้ระแนง (B) – cm</label>
          <input type="number" id="slatWidth2" step="0.01" min="0" placeholder="เช่น 5">
        </div>
        <div>
          <label for="gapWanted">ช่องไฟที่ต้องการ (G) – cm</label>
          <input type="number" id="gapWanted" step="0.01" min="0" placeholder="เช่น 1.6">
        </div>
      </div>

      <div class="btn-row">
        <button class="btn-primary" onclick="calcSlatCount()">
          <span class="btn-icon">📏</span> คำนวณจำนวนแผ่น
        </button>
        <button class="btn-secondary" onclick="resetCountForm()">
          ล้างค่า
        </button>
      </div>

      <div id="countError" class="error"></div>

      <div id="countResult" class="result-box" style="display:none;">
        <div class="result-header">
          <div class="result-title">จำนวนไม้ระแนงที่ใส่ได้</div>
          <button class="btn-copy" type="button" onclick="copyCountResult()">
            <span class="btn-icon">📋</span> คัดลอกผลลัพธ์
          </button>
        </div>
        <div class="result-value" id="slatCountValue"></div>
        <div class="hint">เป็นจำนวนเต็ม ปัดลงให้เหมาะกับหน้างานจริง</div>
        <div id="countCopyMsg" class="copy-msg"></div>
      </div>
    </div>

    <div class="footer-note">
      *ควรวัดซ้ำที่หน้างานก่อนสั่งตัดหรือสั่งผลิตวัสดุทุกครั้ง
    </div>
  </div>

  <script>
    function calcGap() {
      const W = parseFloat(document.getElementById('widthArea1').value);
      const B = parseFloat(document.getElementById('slatWidth1').value);
      const N = parseInt(document.getElementById('slatCount1').value, 10);

      const errorEl = document.getElementById('gapError');
      const resultBox = document.getElementById('gapResult');
      const resultValue = document.getElementById('gapValue');
      const copyMsg = document.getElementById('gapCopyMsg');

      errorEl.textContent = '';
      resultBox.style.display = 'none';
      copyMsg.style.display = 'none';
      copyMsg.textContent = '';

      if (isNaN(W) || isNaN(B) || isNaN(N)) {
        errorEl.textContent = "กรุณากรอกค่าทั้งหมดก่อนคำนวณ";
        return;
      }
      if (N < 2) {
        errorEl.textContent = "ต้องมีไม้ระแนงอย่างน้อย 2 แผ่นเพื่อให้มีช่องไฟ";
        return;
      }

      const gap = (W - (B * N)) / (N - 1);

      if (gap < 0) {
        errorEl.textContent = "ความกว้างไม้รวมมากกว่าพื้นที่ทั้งหมด ทำให้ช่องไฟเป็นค่าติดลบ กรุณาลดจำนวนแผ่นหรือเปลี่ยนขนาดไม้";
        return;
      }

      resultValue.textContent = gap.toFixed(2) + " cm";
      resultBox.style.display = 'block';
    }

    function resetGapForm() {
      document.getElementById('widthArea1').value = "";
      document.getElementById('slatWidth1').value = "";
      document.getElementById('slatCount1').value = "";
      document.getElementById('gapError').textContent = "";
      document.getElementById('gapResult').style.display = "none";
    }

    function calcSlatCount() {
      const W = parseFloat(document.getElementById('widthArea2').value);
      const B = parseFloat(document.getElementById('slatWidth2').value);
      const G = parseFloat(document.getElementById('gapWanted').value);

      const errorEl = document.getElementById('countError');
      const resultBox = document.getElementById('countResult');
      const resultValue = document.getElementById('slatCountValue');
      const copyMsg = document.getElementById('countCopyMsg');

      errorEl.textContent = '';
      resultBox.style.display = 'none';
      copyMsg.style.display = 'none';
      copyMsg.textContent = '';

      if (isNaN(W) || isNaN(B) || isNaN(G)) {
        errorEl.textContent = "กรุณากรอกค่าทั้งหมดก่อนคำนวณ";
        return;
      }

      const denominator = B + G;
      if (denominator <= 0) {
        errorEl.textContent = "ค่าความกว้างไม้ + ช่องไฟ ต้องมากกว่า 0";
        return;
      }

      const rawN = (W + G) / denominator;
      const N = Math.floor(rawN);

      if (N < 1) {
        errorEl.textContent = "คำนวณแล้วไม่สามารถติดตั้งไม้ระแนงได้อย่างน้อย 1 แผ่น";
        return;
      }

      resultValue.textContent = N + " แผ่น";
      resultBox.style.display = "block";
    }

    function resetCountForm() {
      document.getElementById('widthArea2').value = "";
      document.getElementById('slatWidth2').value = "";
      document.getElementById('gapWanted').value = "";
      document.getElementById('countError').textContent = "";
      document.getElementById('countResult').style.display = "none";
    }

    async function copyGapResult() {
      const valueEl = document.getElementById('gapValue');
      const msgEl = document.getElementById('gapCopyMsg');
      const text = valueEl.textContent.trim();
      msgEl.style.display = 'none';
      msgEl.textContent = '';

      if (!text) return;

      try {
        if (navigator.clipboard && navigator.clipboard.writeText) {
          await navigator.clipboard.writeText(text);
        } else {
          // fallback
          const temp = document.createElement('textarea');
          temp.value = text;
          document.body.appendChild(temp);
          temp.select();
          document.execCommand('copy');
          document.body.removeChild(temp);
        }
        msgEl.textContent = "คัดลอกแล้ว: " + text;
        msgEl.classList.remove('error');
        msgEl.style.display = 'block';
      } catch (e) {
        msgEl.textContent = "ไม่สามารถคัดลอกอัตโนมัติได้ กรุณาคัดลอกเอง";
        msgEl.classList.add('error');
        msgEl.style.display = 'block';
      }
    }

    async function copyCountResult() {
      const valueEl = document.getElementById('slatCountValue');
      const msgEl = document.getElementById('countCopyMsg');
      const text = valueEl.textContent.trim();
      msgEl.style.display = 'none';
      msgEl.textContent = '';

      if (!text) return;

      try {
        if (navigator.clipboard && navigator.clipboard.writeText) {
          await navigator.clipboard.writeText(text);
        } else {
          const temp = document.createElement('textarea');
          temp.value = text;
          document.body.appendChild(temp);
          temp.select();
          document.execCommand('copy');
          document.body.removeChild(temp);
        }
        msgEl.textContent = "คัดลอกแล้ว: " + text;
        msgEl.classList.remove('error');
        msgEl.style.display = 'block';
      } catch (e) {
        msgEl.textContent = "ไม่สามารถคัดลอกอัตโนมัติได้ กรุณาคัดลอกเอง";
        msgEl.classList.add('error');
        msgEl.style.display = 'block';
      }
    }
  </script>
</body>
</html>
