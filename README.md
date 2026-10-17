<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Annuity Calculator - Kelompok 8 Elmsworth</title>
    
    <!-- Google Fonts untuk kesan Cutesy & Dreamy -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Fredoka:wght@400;600;700&family=Quicksand:wght@500;600;700&display=swap" rel="stylesheet">

    <style>
        :root {
            --veranda-blue: #6BB1AD;
            --sky-cloud: #A7BCBD;
            --lychee: #EDECDB;
            --melon: #E5A9A9;
            --cupid-pink: #E6748E;
            --text-color: #3d405b;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Quicksand', sans-serif;
        }

        body {
            background-color: var(--lychee);
            background-image: radial-gradient(var(--sky-cloud) 1.5px, transparent 1.5px);
            background-size: 24px 24px;
            color: var(--text-color);
            min-height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        h1, h2, h3 {
            font-family: 'Fredoka', cursive;
            color: var(--text-color);
        }

        /* Container Card Dreamy */
        .card {
            position: relative;
            background: #ffffff;
            border: 4px solid var(--sky-cloud);
            border-radius: 24px;
            padding: 35px 25px 25px 25px;
            max-width: 650px;
            width: 100%;
            box-shadow: 0 10px 25px rgba(230, 116, 142, 0.15);
            margin-top: 25px;
            text-align: center;
            display: none; /* Controlled by JS */
        }

        .card.active {
            display: block;
            animation: fadeIn 0.4s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Cute Cat Topper Decoration */
        .cat-topper {
            position: absolute;
            top: -24px;
            left: 50%;
            transform: translateX(-50%);
            background: #ffffff;
            padding: 0 15px;
            border-radius: 20px;
            border: 3px solid var(--sky-cloud);
            font-family: 'Fredoka', cursive;
            font-size: 14px;
            color: var(--cupid-pink);
            font-weight: bold;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        /* Buttons Style */
        .btn {
            background-color: var(--melon);
            color: #ffffff;
            border: none;
            padding: 14px 28px;
            font-size: 16px;
            font-weight: 700;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.25s ease;
            box-shadow: 0 5px 0px var(--cupid-pink);
            margin-top: 15px;
            display: inline-block;
            text-decoration: none;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 7px 0px var(--cupid-pink);
            background-color: var(--cupid-pink);
        }

        .btn:active {
            transform: translateY(3px);
            box-shadow: 0 2px 0px var(--cupid-pink);
        }

        .btn-secondary {
            background-color: var(--veranda-blue);
            box-shadow: 0 5px 0px #4f8b88;
        }

        .btn-secondary:hover {
            background-color: #4f8b88;
            box-shadow: 0 7px 0px #3c6b68;
        }

        /* Form Inputs */
        .form-group {
            margin-bottom: 20px;
            text-align: left;
        }

        .form-group label {
            display: block;
            font-weight: 700;
            margin-bottom: 8px;
            color: var(--text-color);
        }

        .input-wrapper {
            display: flex;
            gap: 10px;
        }

        input[type="text"], input[type="number"], select {
            width: 100%;
            padding: 12px 16px;
            border: 2px solid var(--sky-cloud);
            border-radius: 16px;
            font-size: 15px;
            outline: none;
            background-color: #fafafa;
            transition: border-color 0.2s;
        }

        input:focus, select:focus {
            border-color: var(--cupid-pink);
            background-color: #ffffff;
        }

        /* Presented By Section */
        .presented-by {
            margin-top: 30px;
            background-color: var(--melon);
            color: #ffffff;
            padding: 20px;
            border-radius: 18px;
            text-align: center;
        }

        .presented-by h3 {
            color: #ffffff;
            margin-bottom: 10px;
            font-size: 18px;
        }

        .presented-by ul {
            list-style: none;
            font-size: 14px;
            line-height: 1.8;
        }

        /* Table Styling */
        .table-container {
            overflow-x: auto;
            margin-top: 20px;
            border-radius: 16px;
            border: 2px solid var(--sky-cloud);
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: #ffffff;
            font-size: 14px;
        }

        th {
            background-color: var(--veranda-blue);
            color: #ffffff;
            padding: 12px 10px;
            font-weight: 700;
            text-align: center;
        }

        td {
            padding: 10px;
            border-bottom: 1px solid var(--lychee);
            text-align: right;
        }

        td:first-child, th:first-child {
            text-align: center;
        }

        tr:nth-child(even) {
            background-color: #f9fbfb;
        }

        .button-group-bottom {
            display: flex;
            justify-content: space-between;
            gap: 15px;
            margin-top: 25px;
            flex-wrap: wrap;
        }

        /* Print styling for PDF download */
        @media print {
            body {
                background: none;
                padding: 0;
            }
            .card {
                box-shadow: none;
                border: 1px solid #ccc;
                max-width: 100%;
            }
            .button-group-bottom, .cat-topper {
                display: none !important;
            }
        }
    </style>
</head>
<body>

    <!-- 1. HOME PAGE -->
    <div id="home-page" class="card active">
        <div class="cat-topper">ฅ⁠^⁠•⁠ﻌ⁠•⁠^⁠ฅ Welcome~</div>
        
        <h1 style="font-size: 28px; margin-bottom: 15px; color: var(--cupid-pink);">Annuity Calculator</h1>
        
        <p style="margin-bottom: 8px; font-weight: 600; font-size: 15px;">
            Simulasikan cicilan pinjamanmu dan dapatkan gambaran pembayaran bulanan sesuai tenor dan suku bunga.
        </p>
        <p style="font-style: italic; font-size: 13px; color: #666; margin-bottom: 25px;">
            "Simulate your loan repayments and get a clear overview of your monthly payments based on your loan term and interest rate."
        </p>

        <button class="btn" onclick="navigateTo('calculator-page')">Calculate Annuity ✨</button>

        <div class="presented-by">
            <h3>Presented By Kelompok 8 Elmsworth</h3>
            <ul>
                <li>Mohamad Dzakwaan Nurfawwaaz (14)</li>
                <li>Naura Zalfa Munifa (22)</li>
                <li>Nida Salsabila (25)</li>
                <li>Radithya Chandra Gavrila (27)</li>
                <li>Syamikha Dhiyaa Althafunnisa Putri Setiadi (38)</li>
            </ul>
        </div>
    </div>

    <!-- 2. CALCULATOR PAGE -->
    <div id="calculator-page" class="card">
        <div class="cat-topper">(=^･ω･^=) Input Details</div>
        
        <h2 style="margin-bottom: 20px; color: var(--veranda-blue);">Loan Calculator</h2>

        <div class="form-group">
            <label for="loanAmount">Loan Amount (Rp)</label>
            <input type="text" id="loanAmount" placeholder="e.g. 35.000.000" oninput="formatRupiahInput(this)">
        </div>

        <div class="form-group">
            <label for="interestRate">Interest Rate (%)</label>
            <div class="input-wrapper">
                <input type="number" id="interestRate" step="0.01" placeholder="e.g. 10">
                <select id="interestType" style="width: 140px;">
                    <option value="year">/ Year</option>
                    <option value="month">/ Month</option>
                </select>
            </div>
        </div>

        <div class="form-group">
            <label for="loanPeriod">Loan Period</label>
            <div class="input-wrapper">
                <input type="number" id="loanPeriod" step="0.1" placeholder="e.g. 2.5">
                <select id="periodType" style="width: 140px;">
                    <option value="year">Years</option>
                    <option value="month">Months</option>
                </select>
            </div>
        </div>

        <button class="btn" onclick="calculateAnnuity()">Calculate ➔</button>
    </div>

    <!-- 3. RESULT PAGE -->
    <div id="result-page" class="card">
        <div class="cat-topper">ฅ⁠/⁠ᐠ⁠.⁠ ⁠ḥ⁠.⁠ᐟ⁠\⁠ฅ Result Table</div>
        
        <h2 style="margin-bottom: 10px; color: var(--cupid-pink);">Annuity Result</h2>
        <p id="summaryText" style="font-size: 14px; font-weight: 600; margin-bottom: 15px;"></p>

        <div class="table-container">
            <table>
                <thead>
                    <tr>
                        <th>Month</th>
                        <th>Principal Payment (Rp)</th>
                        <th>Interest Payment (Rp)</th>
                        <th>Annuity (Rp)</th>
                        <th>Remaining Balance (Rp)</th>
                    </tr>
                </thead>
                <tbody id="resultTableBody">
                    <!-- Table content generated dynamically -->
                </tbody>
            </table>
        </div>

        <div class="button-group-bottom">
            <button class="btn btn-secondary" onclick="navigateTo('home-page')">◄ Back to Home Page</button>
            <button class="btn" onclick="downloadFile()">Download this file ⭳</button>
        </div>
    </div>

    <script>
        // Switch between pages
        function navigateTo(pageId) {
            document.querySelectorAll('.card').forEach(card => card.classList.remove('active'));
            document.getElementById(pageId).classList.add('active');
        }

        // Auto-format Rupiah Input with dots
        function formatRupiahInput(input) {
            let value = input.value.replace(/\D/g, '');
            if (value === "") {
                input.value = "";
                return;
            }
            input.value = new Intl.NumberFormat('id-ID').format(value);
        }

        // Get numeric value from formatted Rupiah input
        function getRawNumber(formattedValue) {
            return parseFloat(formattedValue.replace(/\./g, '')) || 0;
        }

        // Calculate Annuity Table
        function calculateAnnuity() {
            const rawAmount = getRawNumber(document.getElementById('loanAmount').value);
            let rate = parseFloat(document.getElementById('interestRate').value) || 0;
            const rateType = document.getElementById('interestType').value;
            let period = parseFloat(document.getElementById('loanPeriod').value) || 0;
            const periodType = document.getElementById('periodType').value;

            if (rawAmount <= 0 || rate <= 0 || period <= 0) {
                alert("Mohon isi semua data dengan angka yang benar ya! ✨");
                return;
            }

            // Convert period to total months (n)
            let totalMonths = periodType === 'year' ? Math.round(period * 12) : Math.round(period);

            // Convert rate to monthly interest rate decimal (i)
            let monthlyRate = rateType === 'year' ? (rate / 100) / 12 : (rate / 100);

            // Calculate monthly annuity payment A = P * [i / (1 - (1+i)^-n)]
            let annuity = rawAmount * (monthlyRate / (1 - Math.pow(1 + monthlyRate, -totalMonths)));

            const tbody = document.getElementById('resultTableBody');
            tbody.innerHTML = '';

            let remainingBalance = rawAmount;
            
            for (let month = 1; month <= totalMonths; month++) {
                let interestPayment = remainingBalance * monthlyRate;
                let principalPayment = annuity - interestPayment;
                
                // Final month adjustment to make remaining balance exactly 0
                if (month === totalMonths) {
                    principalPayment = remainingBalance;
                    annuity = principalPayment + interestPayment;
                    remainingBalance = 0;
                } else {
                    remainingBalance -= principalPayment;
                }

                const tr = document.createElement('tr');
                tr.innerHTML = `
                    <td>${month}</td>
                    <td>${formatCurrency(principalPayment)}</td>
                    <td>${formatCurrency(interestPayment)}</td>
                    <td>${formatCurrency(annuity)}</td>
                    <td>${formatCurrency(Math.max(0, remainingBalance))}</td>
                `;
                tbody.appendChild(tr);
            }

            document.getElementById('summaryText').innerText = 
                `Total Loan: Rp ${document.getElementById('loanAmount').value} | Tenor: ${totalMonths} Months`;

            navigateTo('result-page');
        }

        function formatCurrency(num) {
            return new Intl.NumberFormat('id-ID', { minimumFractionDigits: 2, maximumFractionDigits: 2 }).format(num);
        }

        function downloadFile() {
            window.print();
        }
    </script>
</body>
</html>
