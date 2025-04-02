# Investment Return Calculator

This calculator helps determine if your investments are outperforming inflation, 
currency depreciation and broker fees.

<div style="max-width: 800px; margin: 0 auto;">
  <!-- Paste your entire HTML calculator code here -->
  <!DOCTYPE html>
  <html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real Investment Return Calculator</title>
    <style>
        :root {
            --primary: #2563eb;
            --primary-hover: #1d4ed8;
            --secondary: #64748b;
            --danger: #ef4444;
            --success: #22c55e;
            --background: #f8fafc;
            --card: #ffffff;
            --text: #0f172a;
            --border: #e2e8f0;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
            background-color: var(--background);
            color: var(--text);
            line-height: 1.6;
            padding: 20px;
            margin: 0;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
        }

        .card {
            background-color: var(--card);
            border-radius: 10px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            margin-bottom: 20px;
            padding: 20px;
        }

        h1, h2, h3 {
            color: var(--text);
            margin-top: 0;
        }

        .form-group {
            margin-bottom: 15px;
        }

        label {
            display: block;
            margin-bottom: 5px;
            font-weight: 600;
        }

        input[type="number"], select {
            width: 100%;
            padding: 10px;
            border: 1px solid var(--border);
            border-radius: 5px;
            font-size: 16px;
        }

        .toggle-container {
            display: flex;
            align-items: center;
            margin-bottom: 15px;
        }

        .toggle-label {
            flex: 1;
            font-weight: 600;
        }

        .toggle {
            position: relative;
            display: inline-block;
            width: 60px;
            height: 30px;
        }

        .toggle input {
            opacity: 0;
            width: 0;
            height: 0;
        }

        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: var(--secondary);
            transition: .4s;
            border-radius: 30px;
        }

        .slider:before {
            position: absolute;
            content: "";
            height: 22px;
            width: 22px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }

        input:checked + .slider {
            background-color: var(--primary);
        }

        input:checked + .slider:before {
            transform: translateX(30px);
        }

        button {
            background-color: var(--primary);
            color: white;
            border: none;
            border-radius: 5px;
            padding: 12px 20px;
            font-size: 16px;
            cursor: pointer;
            transition: background-color 0.3s;
            width: 100%;
            font-weight: 600;
        }

        button:hover {
            background-color: var(--primary-hover);
        }

        .result-card {
            margin-top: 20px;
            display: none;
        }

        .result-row {
            display: flex;
            justify-content: space-between;
            padding: 10px 0;
            border-bottom: 1px solid var(--border);
        }

        .result-row:last-child {
            border-bottom: none;
        }

        .result-label {
            font-weight: 600;
        }

        .result-value {
            font-weight: 700;
        }

        .positive {
            color: var(--success);
        }

        .negative {
            color: var(--danger);
        }

        .step-header {
            background-color: var(--primary);
            color: white;
            padding: 10px 15px;
            margin: -20px -20px 20px -20px;
            border-top-left-radius: 10px;
            border-top-right-radius: 10px;
        }

        .hidden {
            display: none;
        }

        .info-icon {
            display: inline-block;
            width: 18px;
            height: 18px;
            border-radius: 50%;
            background-color: var(--secondary);
            color: white;
            text-align: center;
            line-height: 18px;
            font-size: 12px;
            margin-left: 5px;
            cursor: help;
        }

        .tooltip {
            position: relative;
            display: inline-block;
        }

        .tooltip .tooltiptext {
            visibility: hidden;
            width: 200px;
            background-color: #333;
            color: #fff;
            text-align: center;
            border-radius: 6px;
            padding: 5px;
            position: absolute;
            z-index: 1;
            bottom: 125%;
            left: 50%;
            margin-left: -100px;
            opacity: 0;
            transition: opacity 0.3s;
            font-size: 12px;
            font-weight: normal;
        }

        .tooltip:hover .tooltiptext {
            visibility: visible;
            opacity: 1;
        }

        .grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        @media (max-width: 600px) {
            .grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Real Investment Return Calculator</h1>
        <p>Calculate if your investments are outperforming inflation and currency depreciation after broker fees.</p>

        <div class="card">
            <div class="step-header">
                <h2>1. Investment Details</h2>
            </div>
            <div class="form-group">
                <label for="initial">Initial Investment Amount</label>
                <input type="number" id="initial" min="0" step="any" placeholder="10000">
            </div>
            <div class="form-group">
                <label for="final">Current Investment Value</label>
                <input type="number" id="final" min="0" step="any" placeholder="12000">
            </div>
            <div class="grid">
                <div class="form-group">
                    <label for="years">Investment Period (Years)</label>
                    <input type="number" id="years" min="0.1" step="0.1" placeholder="1">
                </div>
                <div class="form-group">
                    <label for="currency">Base Currency</label>
                    <select id="currency">
                        <option value="USD">USD - US Dollar</option>
                        <option value="EUR">EUR - Euro</option>
                        <option value="GBP">GBP - British Pound</option>
                        <option value="JPY">JPY - Japanese Yen</option>
                        <option value="CNY">CNY - Chinese Yuan</option>
                        <option value="INR">INR - Indian Rupee</option>
                        <option value="Other">Other</option>
                    </select>
                </div>
            </div>
        </div>

        <div class="card">
            <div class="step-header">
                <h2>2. Broker Fees</h2>
            </div>
            <div class="toggle-container">
                <span class="toggle-label">Include broker fees</span>
                <label class="toggle">
                    <input type="checkbox" id="toggle-fees" checked>
                    <span class="slider"></span>
                </label>
            </div>
            <div id="fees-section">
                <div class="grid">
                    <div class="form-group">
                        <label for="management-fee">Annual Management Fee (%)
                            <span class="tooltip">
                                <span class="info-icon">i</span>
                                <span class="tooltiptext">Ongoing percentage fee charged annually on total assets</span>
                            </span>
                        </label>
                        <input type="number" id="management-fee" min="0" max="10" step="0.01" placeholder="1.0">
                    </div>
                    <div class="form-group">
                        <label for="transaction-fee">Transaction Fees (% per trade)
                            <span class="tooltip">
                                <span class="info-icon">i</span>
                                <span class="tooltiptext">Fee charged when buying or selling assets</span>
                            </span>
                        </label>
                        <input type="number" id="transaction-fee" min="0" max="10" step="0.01" placeholder="0.25">
                    </div>
                </div>
                <div class="grid">
                    <div class="form-group">
                        <label for="platform-fee">Annual Platform Fee
                            <span class="tooltip">
                                <span class="info-icon">i</span>
                                <span class="tooltiptext">Fixed annual fee for using the broker's platform</span>
                            </span>
                        </label>
                        <input type="number" id="platform-fee" min="0" step="any" placeholder="120">
                    </div>
                    <div class="form-group">
                        <label for="trades-per-year">Average Trades Per Year
                            <span class="tooltip">
                                <span class="info-icon">i</span>
                                <span class="tooltiptext">Number of buy/sell transactions annually</span>
                            </span>
                        </label>
                        <input type="number" id="trades-per-year" min="0" step="1" placeholder="12">
                    </div>
                </div>
            </div>
        </div>

        <div class="card">
            <div class="step-header">
                <h2>3. Inflation & Currency</h2>
            </div>
            <div class="toggle-container">
                <span class="toggle-label">Account for local inflation</span>
                <label class="toggle">
                    <input type="checkbox" id="toggle-local-inflation" checked>
                    <span class="slider"></span>
                </label>
            </div>
            <div id="local-inflation-section">
                <div class="form-group">
                    <label for="local-inflation">Annual Local Inflation Rate (%)
                        <span class="tooltip">
                            <span class="info-icon">i</span>
                            <span class="tooltiptext">Average annual inflation rate in your country</span>
                        </span>
                    </label>
                    <input type="number" id="local-inflation" min="0" max="100" step="0.1" placeholder="2.5">
                </div>
            </div>

            <div class="toggle-container">
                <span class="toggle-label">Account for global inflation</span>
                <label class="toggle">
                    <input type="checkbox" id="toggle-global-inflation">
                    <span class="slider"></span>
                </label>
            </div>
            <div id="global-inflation-section" class="hidden">
                <div class="form-group">
                    <label for="global-inflation">Annual Global Inflation Rate (%)
                        <span class="tooltip">
                            <span class="info-icon">i</span>
                            <span class="tooltiptext">World average inflation, relevant for international investments</span>
                        </span>
                    </label>
                    <input type="number" id="global-inflation" min="0" max="100" step="0.1" placeholder="3.0">
                </div>
                <div class="form-group">
                    <label for="global-exposure">Percentage of Portfolio in Foreign Markets (%)
                        <span class="tooltip">
                            <span class="info-icon">i</span>
                            <span class="tooltiptext">Proportion of your portfolio exposed to international markets</span>
                        </span>
                    </label>
                    <input type="number" id="global-exposure" min="0" max="100" step="1" placeholder="50">
                </div>
            </div>

            <div class="toggle-container">
                <span class="toggle-label">Account for currency depreciation</span>
                <label class="toggle">
                    <input type="checkbox" id="toggle-currency" checked>
                    <span class="slider"></span>
                </label>
            </div>
            <div id="currency-section">
                <div class="form-group">
                    <label for="currency-depreciation">Annual Currency Depreciation Rate (%)
                        <span class="tooltip">
                            <span class="info-icon">i</span>
                            <span class="tooltiptext">Average annual rate your currency loses value against investment currencies</span>
                        </span>
                    </label>
                    <input type="number" id="currency-depreciation" min="-20" max="20" step="0.1" placeholder="1.0">
                </div>
            </div>
        </div>

        <button id="calculate">Calculate Real Return</button>

        <div class="card result-card" id="result-section">
            <div class="step-header">
                <h2>Results</h2>
            </div>
            <div class="result-row">
                <div class="result-label">Nominal Return</div>
                <div class="result-value" id="nominal-return">-</div>
            </div>
            <div class="result-row">
                <div class="result-label">Annual Return (Before Adjustments)</div>
                <div class="result-value" id="annual-return">-</div>
            </div>
            <div class="result-row">
                <div class="result-label">Total Broker Fees Impact</div>
                <div class="result-value" id="fees-impact">-</div>
            </div>
            <div class="result-row">
                <div class="result-label">Inflation Impact</div>
                <div class="result-value" id="inflation-impact">-</div>
            </div>
            <div class="result-row">
                <div class="result-label">Currency Depreciation Impact</div>
                <div class="result-value" id="currency-impact">-</div>
            </div>
            <div class="result-row">
                <div class="result-label">Real Return (After All Factors)</div>
                <div class="result-value" id="real-return">-</div>
            </div>
            <div class="result-row">
                <div class="result-label">Annual Real Return</div>
                <div class="result-value" id="annual-real-return">-</div>
            </div>
            <div class="result-row">
                <div class="result-label">Verdict</div>
                <div class="result-value" id="verdict">-</div>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            // Toggle sections visibility based on checkbox state
            document.getElementById('toggle-fees').addEventListener('change', function() {
                document.getElementById('fees-section').style.display = this.checked ? 'block' : 'none';
            });

            document.getElementById('toggle-local-inflation').addEventListener('change', function() {
                document.getElementById('local-inflation-section').style.display = this.checked ? 'block' : 'none';
            });

            document.getElementById('toggle-global-inflation').addEventListener('change', function() {
                document.getElementById('global-inflation-section').style.display = this.checked ? 'block' : 'none';
            });

            document.getElementById('toggle-currency').addEventListener('change', function() {
                document.getElementById('currency-section').style.display = this.checked ? 'block' : 'none';
            });

            // Calculate button click handler
            document.getElementById('calculate').addEventListener('click', calculateReturn);

            // Set default values
            document.getElementById('initial').value = '10000';
            document.getElementById('final').value = '12000';
            document.getElementById('years').value = '1';
            document.getElementById('management-fee').value = '1.0';
            document.getElementById('transaction-fee').value = '0.25';
            document.getElementById('platform-fee').value = '120';
            document.getElementById('trades-per-year').value = '12';
            document.getElementById('local-inflation').value = '2.5';
            document.getElementById('global-inflation').value = '3.0';
            document.getElementById('global-exposure').value = '50';
            document.getElementById('currency-depreciation').value = '1.0';
        });

        function calculateReturn() {
            // Get input values
            const initialInvestment = parseFloat(document.getElementById('initial').value) || 0;
            const finalValue = parseFloat(document.getElementById('final').value) || 0;
            const years = parseFloat(document.getElementById('years').value) || 1;
            
            // Calculate nominal return
            const nominalReturn = ((finalValue - initialInvestment) / initialInvestment) * 100;
            const annualReturn = Math.pow((1 + nominalReturn / 100), 1 / years) - 1;
            
            // Calculate fees impact if enabled
            let feesImpact = 0;
            if (document.getElementById('toggle-fees').checked) {
                const managementFee = parseFloat(document.getElementById('management-fee').value) || 0;
                const transactionFee = parseFloat(document.getElementById('transaction-fee').value) || 0;
                const platformFee = parseFloat(document.getElementById('platform-fee').value) || 0;
                const tradesPerYear = parseFloat(document.getElementById('trades-per-year').value) || 0;
                
                // Annual management fee impact over the investment period
                const managementFeeImpact = managementFee * years;
                
                // Transaction fees impact
                const avgTransactionSize = initialInvestment / tradesPerYear;
                const totalTransactions = tradesPerYear * years;
                const transactionFeeImpact = (transactionFee / 100) * totalTransactions * avgTransactionSize / initialInvestment * 100;
                
                // Platform fee impact
                const platformFeeImpact = (platformFee * years / initialInvestment) * 100;
                
                feesImpact = managementFeeImpact + transactionFeeImpact + platformFeeImpact;
            }
            
            // Calculate inflation impact if enabled
            let inflationImpact = 0;
            if (document.getElementById('toggle-local-inflation').checked) {
                const localInflation = parseFloat(document.getElementById('local-inflation').value) || 0;
                inflationImpact = localInflation * years;
            }
            
            // Add global inflation impact if enabled
            if (document.getElementById('toggle-global-inflation').checked) {
                const globalInflation = parseFloat(document.getElementById('global-inflation').value) || 0;
                const globalExposure = parseFloat(document.getElementById('global-exposure').value) || 0;
                inflationImpact += (globalInflation * years) * (globalExposure / 100);
            }
            
            // Calculate currency depreciation impact if enabled
            let currencyImpact = 0;
            if (document.getElementById('toggle-currency').checked) {
                const currencyDepreciation = parseFloat(document.getElementById('currency-depreciation').value) || 0;
                currencyImpact = currencyDepreciation * years;
            }
            
            // Calculate real return
            const realReturn = nominalReturn - feesImpact - inflationImpact - currencyImpact;
            const annualRealReturn = Math.pow((1 + realReturn / 100), 1 / years) - 1;
            
            // Display results
            document.getElementById('result-section').style.display = 'block';
            document.getElementById('nominal-return').textContent = nominalReturn.toFixed(2) + '%';
            document.getElementById('nominal-return').className = 'result-value ' + (nominalReturn >= 0 ? 'positive' : 'negative');
            
            document.getElementById('annual-return').textContent = (annualReturn * 100).toFixed(2) + '%';
            document.getElementById('annual-return').className = 'result-value ' + (annualReturn >= 0 ? 'positive' : 'negative');
            
            document.getElementById('fees-impact').textContent = '-' + feesImpact.toFixed(2) + '%';
            document.getElementById('fees-impact').className = 'result-value negative';
            
            document.getElementById('inflation-impact').textContent = '-' + inflationImpact.toFixed(2) + '%';
            document.getElementById('inflation-impact').className = 'result-value negative';
            
            document.getElementById('currency-impact').textContent = '-' + currencyImpact.toFixed(2) + '%';
            document.getElementById('currency-impact').className = 'result-value negative';
            
            document.getElementById('real-return').textContent = realReturn.toFixed(2) + '%';
            document.getElementById('real-return').className = 'result-value ' + (realReturn >= 0 ? 'positive' : 'negative');
            
            document.getElementById('annual-real-return').textContent = (annualRealReturn * 100).toFixed(2) + '%';
            document.getElementById('annual-real-return').className = 'result-value ' + (annualRealReturn >= 0 ? 'positive' : 'negative');
            
            // Provide verdict
            let verdict;
            if (realReturn > 0) {
                verdict = "Your investment is outperforming inflation, currency depreciation, and broker fees!";
                document.getElementById('verdict').className = 'result-value positive';
            } else {
                verdict = "Your investment is not keeping up with inflation, currency depreciation, and broker fees.";
                document.getElementById('verdict').className = 'result-value negative';
            }
            document.getElementById('verdict').textContent = verdict;
            
            // Scroll to results
            document.getElementById('result-section').scrollIntoView({ behavior: 'smooth' });
        }
    </script>
</body>
</html>
