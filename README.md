# Driveway101
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Driveway Approval Helper</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <style>
    :root {
      --bg: #0f172a;
      --card: #020617;
      --accent: #38bdf8;
      --accent-soft: rgba(56, 189, 248, 0.1);
      --text: #e5e7eb;
      --muted: #9ca3af;
      --danger: #f97373;
      --warn: #facc15;
      --success: #4ade80;
      --border: #1f2937;
      --input-bg: #020617;
    }

    * {
      box-sizing: border-box;
      font-family: system-ui, -apple-system, BlinkMacSystemFont, "SF Pro Text",
        "SF Pro Display", "Segoe UI", sans-serif;
    }

    body {
      margin: 0;
      padding: 0;
      background: radial-gradient(circle at top, #1e293b 0, #020617 55%);
      color: var(--text);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: flex-start;
    }

    .app {
      width: 100%;
      max-width: 1100px;
      margin: 24px;
      padding: 24px;
      border-radius: 18px;
      background: radial-gradient(circle at top left, #0b1120 0, #020617 55%);
      border: 1px solid rgba(148, 163, 184, 0.25);
      box-shadow:
        0 24px 80px rgba(15, 23, 42, 0.9),
        0 0 0 1px rgba(15, 23, 42, 0.9);
    }

    .app-header {
      display: flex;
      justify-content: space-between;
      gap: 16px;
      align-items: center;
      margin-bottom: 20px;
    }

    .title-block h1 {
      margin: 0;
      font-size: 24px;
      letter-spacing: 0.03em;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .title-pill {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--muted);
      display: inline-flex;
      align-items: center;
      gap: 6px;
    }

    .title-pill span.dot {
      width: 6px;
      height: 6px;
      border-radius: 999px;
      background: var(--accent);
      box-shadow: 0 0 12px rgba(56, 189, 248, 0.9);
    }

    .subtitle {
      margin-top: 6px;
      font-size: 13px;
      color: var(--muted);
    }

    .badge {
      padding: 6px 10px;
      border-radius: 999px;
      border: 1px solid rgba(148, 163, 184, 0.4);
      font-size: 11px;
      color: var(--muted);
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: radial-gradient(circle at top, rgba(56, 189, 248, 0.12), transparent 60%);
    }

    .badge-dot {
      width: 7px;
      height: 7px;
      border-radius: 999px;
      background: var(--success);
      box-shadow: 0 0 10px rgba(74, 222, 128, 0.9);
    }

    .layout {
      display: grid;
      grid-template-columns: 1.1fr 1.1fr;
      gap: 18px;
    }

    @media (max-width: 900px) {
      .layout {
        grid-template-columns: 1fr;
      }
    }

    .card {
      background: radial-gradient(circle at top left, #020617 0, #020617 55%);
      border-radius: 16px;
      border: 1px solid rgba(31, 41, 55, 0.9);
      padding: 16px 16px 18px;
      position: relative;
      overflow: hidden;
    }

    .card::before {
      content: "";
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at top left, rgba(56, 189, 248, 0.06), transparent 60%);
      opacity: 0.9;
      pointer-events: none;
    }

    .card-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 10px;
      position: relative;
      z-index: 1;
    }

    .card-title {
      font-size: 13px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--muted);
    }

    .card-subtitle {
      font-size: 11px;
      color: var(--muted);
      margin-top: 2px;
    }

    .pill {
      font-size: 11px;
      padding: 4px 8px;
      border-radius: 999px;
      border: 1px solid rgba(148, 163, 184, 0.4);
      color: var(--muted);
    }

    .form-grid {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 10px;
      position: relative;
      z-index: 1;
    }

    .form-group {
      display: flex;
      flex-direction: column;
      gap: 4px;
    }

    label {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.14em;
      color: var(--muted);
    }

    input,
    select {
      padding: 8px 9px;
      border-radius: 10px;
      border: 1px solid rgba(55, 65, 81, 0.9);
      background: var(--input-bg);
      color: var(--text);
      font-size: 13px;
      outline: none;
      transition: border 0.15s ease, box-shadow 0.15s ease, background 0.15s ease;
    }

    input:focus,
    select:focus {
      border-color: var(--accent);
      box-shadow: 0 0 0 1px rgba(56, 189, 248, 0.6);
      background: #020617;
    }

    input::placeholder {
      color: #4b5563;
    }

    .full-width {
      grid-column: span 2;
    }

    .btn-row {
      margin-top: 12px;
      display: flex;
      justify-content: flex-end;
      gap: 8px;
      position: relative;
      z-index: 1;
    }

    button {
      border-radius: 999px;
      border: none;
      padding: 8px 14px;
      font-size: 13px;
      cursor: pointer;
      display: inline-flex;
      align-items: center;
      gap: 6px;
      transition: transform 0.12s ease, box-shadow 0.12s ease, background 0.12s ease;
    }

    .btn-primary {
      background: linear-gradient(135deg, #38bdf8, #0ea5e9);
      color: #0b1120;
      font-weight: 600;
      box-shadow:
        0 10px 30px rgba(56, 189, 248, 0.45),
        0 0 0 1px rgba(8, 47, 73, 0.9);
    }

    .btn-primary:hover {
      transform: translateY(-1px);
      box-shadow:
        0 14px 40px rgba(56, 189, 248, 0.6),
        0 0 0 1px rgba(8, 47, 73, 1);
    }

    .btn-secondary {
      background: rgba(15, 23, 42, 0.9);
      color: var(--muted);
      border: 1px solid rgba(55, 65, 81, 0.9);
    }

    .btn-secondary:hover {
      background: #020617;
      transform: translateY(-1px);
    }

    .status-row {
      display: flex;
      align-items: center;
      gap: 10px;
      margin-bottom: 10px;
      position: relative;
      z-index: 1;
    }

    .status-pill {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 6px 10px;
      border-radius: 999px;
      border: 1px solid rgba(31, 41, 55, 0.9);
      background: rgba(15, 23, 42, 0.9);
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
    }

    .status-dot {
      width: 9px;
      height: 9px;
      border-radius: 999px;
      box-shadow: 0 0 12px currentColor;
    }

    .status-green {
      color: var(--success);
    }

    .status-yellow {
      color: var(--warn);
    }

    .status-red {
      color: var(--danger);
    }

    .status-label {
      font-size: 12px;
      color: var(--muted);
    }

    .metrics-grid {
      display: grid;
      grid-template-columns: repeat(3, minmax(0, 1fr));
      gap: 10px;
      margin-bottom: 10px;
      position: relative;
      z-index: 1;
    }

    .metric {
      padding: 8px 9px;
      border-radius: 12px;
      border: 1px solid rgba(31, 41, 55, 0.9);
      background: rgba(15, 23, 42, 0.9);
    }

    .metric-label {
      font-size: 10px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--muted);
      margin-bottom: 4px;
    }

    .metric-value {
      font-size: 14px;
      font-weight: 600;
    }

    .metric-tag {
      font-size: 11px;
      color: var(--muted);
      margin-top: 2px;
    }

    .rules-list {
      margin: 0;
      padding-left: 16px;
      font-size: 12px;
      color: var(--muted);
    }

    .rules-list li {
      margin-bottom: 2px;
    }

    .rules-list span.ok {
      color: var(--success);
    }

    .rules-list span.warn {
      color: var(--warn);
    }

    .rules-list span.bad {
      color: var(--danger);
    }

    .section-label {
      font-size: 11px;
      text-transform: uppercase;
      letter-spacing: 0.16em;
      color: var(--muted);
      margin: 10px 0 4px;
    }

    .alt-list {
      display: grid;
      grid-template-columns: repeat(2, minmax(0, 1fr));
      gap: 8px;
      position: relative;
      z-index: 1;
    }

    @media (max-width: 600px) {
      .alt-list {
        grid-template-columns: 1fr;
      }
    }

    .alt-card {
      border-radius: 12px;
      border: 1px solid rgba(31, 41, 55, 0.9);
      background: rgba(15, 23, 42, 0.9);
      padding: 8px 9px;
      font-size: 12px;
    }

    .alt-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 4px;
    }

    .alt-title {
      font-weight: 600;
      font-size: 12px;
    }

    .alt-pill {
      font-size: 10px;
      padding: 3px 7px;
      border-radius: 999px;
      border: 1px solid rgba(55, 65, 81, 0.9);
      color: var(--muted);
    }

    .alt-meta {
      display: flex;
      justify-content: space-between;
      font-size: 11px;
      color: var(--muted);
    }

    .small {
      font-size: 11px;
      color: var(--muted);
    }

    .hint {
      font-size: 11px;
      color: var(--muted);
      margin-top: 6px;
    }

    .hint strong {
      color: var(--accent);
      font-weight: 500;
    }
  </style>
</head>
<body>
  <div class="app">
    <div class="app-header">
      <div class="title-block">
        <div class="title-pill">
          <span class="dot"></span>
          DRIVEWAY · APPROVAL HELPER
        </div>
        <h1>
          Instant Vehicle Approval Signal
        </h1>
        <div class="subtitle">
          Use this while you’re on the phone to quickly see if a unit is
          <strong>Green / Yellow / Red</strong> for approval.
        </div>
      </div>
      <div class="badge">
        <span class="badge-dot"></span>
        Live call workflow · Built for Oliver · v0.2
      </div>
    </div>

    <div class="layout">
      <!-- LEFT: INPUTS -->
      <div class="card">
        <div class="card-header">
          <div>
            <div class="card-title">Vehicle & Deal Inputs</div>
            <div class="card-subtitle">
              Enter what you see in Driveway / CRM.
            </div>
          </div>
          <div class="pill">Step 1 · Fill & Evaluate</div>
        </div>

        <div class="form-grid">
          <div class="form-group">
            <label for="vehicleYear">Year</label>
            <input id="vehicleYear" type="number" placeholder="e.g. 2021" />
          </div>

          <div class="form-group">
            <label for="vehicleMileage">Mileage</label>
            <input id="vehicleMileage" type="number" placeholder="e.g. 42000" />
          </div>

          <div class="form-group">
            <label for="vehicleType">Vehicle type</label>
            <select id="vehicleType">
              <option value="sedan">Sedan / Coupe</option>
              <option value="suv">SUV / Crossover</option>
              <option value="truck">Truck</option>
              <option value="van">Van</option>
              <option value="sports">Sports / Performance</option>
              <option value="luxury">Luxury</option>
            </select>
          </div>

          <div class="form-group">
            <label for="vehiclePrice">Selling price ($)</label>
            <input id="vehiclePrice" type="number" placeholder="e.g. 28995" />
          </div>

          <div class="form-group">
            <label for="bookValue">Book value ($)</label>
            <input id="bookValue" type="number" placeholder="e.g. 27500" />
          </div>

          <div class="form-group">
            <label for="downPayment">Down payment ($)</label>
            <input id="downPayment" type="number" placeholder="e.g. 2000" />
          </div>

          <div class="form-group full-width">
            <label for="lender">Lender bucket</label>
            <select id="lender">
              <option value="prime">Prime / Big Bank (CapOne · BofA · Chase · Ally)</option>
              <option value="driveway">Driveway / Captive / Mid‑Tier</option>
              <option value="creditBuilder">Credit‑Building (Westlake · Santander · Others)</option>
            </select>
          </div>

          <div class="form-group full-width">
            <label for="notes">Quick notes (optional)</label>
            <input id="notes" type="text" placeholder="Customer profile, income, lender you’re thinking of, etc." />
          </div>
        </div>

        <div class="btn-row">
          <button class="btn-secondary" type="button" id="resetBtn">
            Reset
          </button>
          <button class="btn-primary" type="button" id="evaluateBtn">
            <span>Evaluate Vehicle</span>
          </button>
        </div>

        <div class="hint">
          If you’re not sure which lender yet, start with
          <strong>Driveway / Captive / Mid‑Tier</strong> and see how it looks.
        </div>
      </div>

      <!-- RIGHT: OUTPUTS -->
      <div class="card">
        <div class="card-header">
          <div>
            <div class="card-title">Approval Signal</div>
            <div class="card-subtitle">
              Simple rules for LTV, age, mileage, and lender style.
            </div>
          </div>
          <div class="pill">Step 2 · Read & Pivot</div>
        </div>

        <div class="status-row">
          <div id="statusPill" class="status-pill status-yellow">
            <span id="statusDot" class="status-dot status-yellow"></span>
            <span id="statusText">Waiting for inputs</span>
          </div>
          <div class="status-label" id="statusLabel">
            Fill in the left side and click “Evaluate Vehicle”.
          </div>
        </div>

        <div class="metrics-grid">
          <div class="metric">
            <div class="metric-label">LTV</div>
            <div class="metric-value" id="ltvValue">–</div>
            <div class="metric-tag" id="ltvTag">Loan-to-value</div>
          </div>
          <div class="metric">
            <div class="metric-label">Vehicle Fit</div>
            <div class="metric-value" id="fitValue">–</div>
            <div class="metric-tag" id="fitTag">Age · Mileage · Type</div>
          </div>
          <div class="metric">
            <div class="metric-label">Overall Signal</div>
            <div class="metric-value" id="overallValue">–</div>
            <div class="metric-tag" id="overallTag">Based on simple rules</div>
          </div>
        </div>

        <div class="section-label">Lender rule check</div>
        <ul class="rules-list" id="rulesList">
          <li>Rules will show here after evaluation.</li>
        </ul>

        <div class="section-label">Suggested alternatives (mock)</div>
        <div class="alt-list" id="altList">
          <!-- Alternatives will be injected here -->
        </div>

        <div class="hint">
          Green doesn’t guarantee an approval, but it helps you steer customers toward
          <strong>book‑friendly inventory</strong> and away from obvious landmines.
        </div>
      </div>
    </div>
  </div>

  <script>
    // --- Lender buckets tuned for your world ---
    const lenders = {
      prime: {
        name: "Prime / Big Bank (CapOne · BofA · Chase · Ally)",
        maxLTV: 115,
        softMaxLTV: 125,
        maxAgeYears: 7,
        maxMileage: 90000,
        notes: "Stronger credit, newer units. Keep LTV tight."
      },
      driveway: {
        name: "Driveway / Captive / Mid‑Tier",
        maxLTV: 125,
        softMaxLTV: 135,
        maxAgeYears: 10,
        maxMileage: 120000,
        notes: "Good middle ground. Flexible if structure is solid."
      },
      creditBuilder: {
        name: "Credit‑Building (Westlake · Santander · Others)",
        maxLTV: 140,
        softMaxLTV: 150,
        maxAgeYears: 12,
        maxMileage: 150000,
        notes: "More flexible, but down payment and structure matter a lot."
      }
    };

    function getCurrentYear() {
      return new Date().getFullYear();
    }

    function formatPercent(num) {
      if (isNaN(num)) return "–";
      return num.toFixed(1) + "%";
    }

    function classifyLTV(ltv, lender) {
      if (isNaN(ltv)) return { label: "Unknown", color: "yellow" };

      if (ltv <= lender.maxLTV) {
        return { label: "Strong", color: "green" };
      } else if (ltv <= lender.softMaxLTV) {
        return { label: "Borderline", color: "yellow" };
      } else {
        return { label: "High", color: "red" };
      }
    }

    function classifyVehicleFit(ageYears, mileage, lender, type) {
      let issues = 0;

      if (ageYears > lender.maxAgeYears) issues++;
      if (mileage > lender.maxMileage) issues++;

      // Slight penalty for sports / luxury with prime lenders
      if ((type === "sports" || type === "luxury") && lender === lenders.prime) {
        issues++;
      }

      if (issues === 0) return { label: "Good", color: "green" };
      if (issues === 1) return { label: "Mixed", color: "yellow" };
      return { label: "Weak", color: "red" };
    }

    function combineSignal(ltvClass, fitClass) {
      const colors = [ltvClass.color, fitClass.color];

      if (colors.includes("red")) return { label: "High Risk", color: "red" };
      if (colors.includes("yellow")) return { label: "Borderline", color: "yellow" };
      return { label: "Strong", color: "green" };
    }

    function buildRulesSummary(ageYears, mileage, ltv, lenderKey, type) {
      const lender = lenders[lenderKey];
      const items = [];

      // Age rule
      const ageOk = ageYears <= lender.maxAgeYears;
      items.push(
        `<li>Age: <span class="${ageOk ? "ok" : "bad"}">${ageYears} yrs</span> (limit ~${lender.maxAgeYears} yrs)</li>`
      );

      // Mileage rule
      const milesOk = mileage <= lender.maxMileage;
      items.push(
        `<li>Mileage: <span class="${milesOk ? "ok" : "bad"}">${mileage.toLocaleString()} mi</span> (limit ~${lender.maxMileage.toLocaleString()} mi)</li>`
      );

      // LTV rule
      const ltvClass = classifyLTV(ltv, lender);
      const ltvClassName =
        ltvClass.color === "green" ? "ok" : ltvClass.color === "yellow" ? "warn" : "bad";
      items.push(
        `<li>LTV: <span class="${ltvClassName}">${formatPercent(ltv)}</span> (target ≤ ${lender.maxLTV}% · soft cap ${lender.softMaxLTV}%)</li>`
      );

      // Type note
      if ((type === "sports" || type === "luxury") && lenderKey === "prime") {
        items.push(
          `<li>Type: <span class="warn">${type.toUpperCase()}</span> — some prime lenders are picky on sports / luxury.</li>`
        );
      } else {
        items.push(`<li>Type: <span class="ok">${type.toUpperCase()}</span></li>`);
      }

      items.push(`<li>Lender style: ${lender.notes}</li>`);

      return items.join("");
    }

    function buildAlternatives(basePrice, baseBook, lenderKey) {
      const lender = lenders[lenderKey];
      const altList = document.getElementById("altList");
      altList.innerHTML = "";

      if (!basePrice || !baseBook || isNaN(basePrice) || isNaN(baseBook)) {
        altList.innerHTML =
          '<div class="small">Enter price and book value to see simple alternative ideas.</div>';
        return;
      }

      const baseLTV = (basePrice / baseBook) * 100;

      // Create a few mock alternatives with slightly better LTV
      const alternatives = [
        {
          label: "Similar trim · Slightly lower price",
          price: Math.round(basePrice * 0.96),
          book: baseBook,
          tag: "Drop price ~4%"
        },
        {
          label: "Same price · Better book value unit",
          price: basePrice,
          book: Math.round(baseBook * 1.04),
          tag: "Find stronger book"
        },
        {
          label: "Lower price · Stronger book",
          price: Math.round(basePrice * 0.93),
          book: Math.round(baseBook * 1.03),
          tag: "Ideal switch unit"
        },
        {
          label: "Slightly cheaper model year",
          price: Math.round(basePrice * 0.9),
          book: Math.round(baseBook * 0.98),
          tag: "Older but safer"
        }
      ];

      alternatives.forEach((alt) => {
        const ltv = (alt.price / alt.book) * 100;
        const ltvClass = classifyLTV(ltv, lender);

        const div = document.createElement("div");
        div.className = "alt-card";
        div.innerHTML = `
          <div class="alt-header">
            <div class="alt-title">${alt.label}</div>
            <div class="alt-pill">${formatPercent(ltv)} LTV</div>
          </div>
          <div class="alt-meta">
            <span>$${alt.price.toLocaleString()} vs. book $${alt.book.toLocaleString()}</span>
            <span style="color:${
              ltvClass.color === "green"
                ? "#4ade80"
                : ltvClass.color === "yellow"
                ? "#facc15"
                : "#f97373"
            }">${ltvClass.label}</span>
          </div>
          <div class="small">${alt.tag}</div>
        `;
        altList.appendChild(div);
      });

      const note = document.createElement("div");
      note.className = "small";
      note.style.marginTop = "4px";
      note.textContent =
        "Use these as talking points: “I’ve got a similar option that books out stronger and is easier to get approved.”";
      altList.appendChild(note);
    }

    function setStatus(color, mainText, labelText) {
      const pill = document.getElementById("statusPill");
      const dot = document.getElementById("statusDot");
      const text = document.getElementById("statusText");
      const label = document.getElementById("statusLabel");

      pill.classList.remove("status-green", "status-yellow", "status-red");
      dot.classList.remove("status-green", "status-yellow", "status-red");

      if (color === "green") {
        pill.classList.add("status-green");
        dot.classList.add("status-green");
      } else if (color === "yellow") {
        pill.classList.add("status-yellow");
        dot.classList.add("status-yellow");
      } else {
        pill.classList.add("status-red");
        dot.classList.add("status-red");
      }

      text.textContent = mainText;
      label.textContent = labelText;
    }

    function evaluate() {
      const year = parseInt(document.getElementById("vehicleYear").value, 10);
      const mileage = parseInt(document.getElementById("vehicleMileage").value, 10);
      const type = document.getElementById("vehicleType").value;
      const price = parseFloat(document.getElementById("vehiclePrice").value);
      const book = parseFloat(document.getElementById("bookValue").value);
      const down = parseFloat(document.getElementById("downPayment").value || "0");
      const lenderKey = document.getElementById("lender").value;

      const rulesList = document.getElementById("rulesList");

      if (!year || !mileage || !price || !book || !lenderKey) {
        setStatus(
          "yellow",
          "Need more info",
          "Year, mileage, price, book value, and lender bucket are required for a useful signal."
        );
        document.getElementById("ltvValue").textContent = "–";
        document.getElementById("fitValue").textContent = "–";
        document.getElementById("overallValue").textContent = "–";
        rulesList.innerHTML = "<li>Please fill in the required fields on the left.</li>";
        document.getElementById("overallTag").textContent = "Based on simple rules";
        buildAlternatives(NaN, NaN, lenderKey);
        return;
      }

      const lender = lenders[lenderKey];
      const currentYear = getCurrentYear();
      const ageYears = Math.max(0, currentYear - year);

      const amountFinanced = price - down;
      const ltv = (amountFinanced / book) * 100;

      const ltvClass = classifyLTV(ltv, lender);
      const fitClass = classifyVehicleFit(ageYears, mileage, lender, type);
      const overall = combineSignal(ltvClass, fitClass);

      // Update metrics
      document.getElementById("ltvValue").textContent = formatPercent(ltv);
      document.getElementById("ltvTag").textContent =
        "On " + lender.name + " style structure";

      document.getElementById("fitValue").textContent = fitClass.label;
      document.getElementById("fitTag").textContent =
        ageYears + " yrs · " + mileage.toLocaleString() + " mi";

      document.getElementById("overallValue").textContent = overall.label;
      document.getElementById("overallTag").textContent =
        overall.color === "green"
          ? "Good candidate to lead with"
          : overall.color === "yellow"
          ? "Use with caution / structure carefully"
          : "Try to pivot to a stronger unit";

      // Update status pill
      if (overall.color === "green") {
        setStatus(
          "green",
          "Green — Lead with this unit",
          "Still not a guarantee, but this is a book‑friendly option to present confidently."
        );
      } else if (overall.color === "yellow") {
        setStatus(
          "yellow",
          "Yellow — Borderline",
          "Okay to discuss, but be ready with a backup unit that books out stronger."
        );
      } else {
        setStatus(
          "red",
          "Red — Tough approval",
          "Use this as a reference only; pivot the customer toward alternatives with better book value."
        );
      }

      // Rules summary
      rulesList.innerHTML = buildRulesSummary(ageYears, mileage, ltv, lenderKey, type);

      // Alternatives
      buildAlternatives(price, book, lenderKey);
    }

    function resetForm() {
      document.getElementById("vehicleYear").value = "";
      document.getElementById("vehicleMileage").value = "";
      document.getElementById("vehicleType").value = "sedan";
      document.getElementById("vehiclePrice").value = "";
      document.getElementById("bookValue").value = "";
      document.getElementById("downPayment").value = "";
      document.getElementById("lender").value = "driveway";
      document.getElementById("notes").value = "";

      setStatus(
        "yellow",
        "Waiting for inputs",
        "Fill in the left side and click “Evaluate Vehicle”."
      );
      document.getElementById("ltvValue").textContent = "–";
      document.getElementById("ltvTag").textContent = "Loan-to-value";
      document.getElementById("fitValue").textContent = "–";
      document.getElementById("fitTag").textContent = "Age · Mileage · Type";
      document.getElementById("overallValue").textContent = "–";
      document.getElementById("overallTag").textContent = "Based on simple rules";
      document.getElementById("rulesList").innerHTML =
        "<li>Rules will show here after evaluation.</li>";
      document.getElementById("altList").innerHTML =
        '<div class="small">Enter price and book value to see simple alternative ideas.</div>';
    }

    document.getElementById("evaluateBtn").addEventListener("click", evaluate);
    document.getElementById("resetBtn").addEventListener("click", resetForm);

    // Initialize
    resetForm();
  </script>
</body>
</html>
