# -mortgage-calculator--2
HTML and CSS and JAVA SCRIPT
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mortgage Calculator</title>
<link rel="icon" type="image/png" href="https://z-cdn-media.chatglm.cn/files/2f2dd2e2-1637-4ae7-a167-8d539ad01421_favicon-32x32.png?auth_key=1791969139-4a60865f325743a3924b6ed17a125785-0-006e6e900448bd8d8d1a5244211a1079">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;700&display=swap">
<style>
    :root {
        --primary-color: #D8DA2D;
        --secondary-color: #133041;
        --accent-color: #365E77;
        --error-color: #D73C3C;
        --text-color: #333333;
        --light-gray: #F8F8F8;
        --white: #FFFFFF;
        --transition: all 0.3s ease;
    }

    * {
        margin: 0;
        padding: 0;
        box-sizing: border-box;
    }

    body {
        font-family: 'Plus Jakarta Sans', sans-serif;
        background-color: var(--light-gray);
        color: var(--text-color);
        line-height: 1.5;
    }

    .container {
        display: flex;
        flex-direction: column;
        min-height: 100vh;
    }

    header {
        background-color: var(--secondary-color);
        color: var(--white);
        padding: 1rem;
        text-align: center;
    }

    header h1 {
        font-size: 2rem;
        font-weight: 700;
    }

    main {
        flex: 1;
        display: flex;
        flex-direction: column;
        padding: 2rem;
        width: 100%;
        max-width: 1200px;
        margin: auto;
    }

    .calculator-container {
        display: flex;
        flex-direction: column;
        gap: 2rem;
        width: 100%;
    }

    .form-section {
        background-color: var(--white);
        border-radius: 8px;
        padding: 2rem;
        box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    .form-header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 1rem;
    }

    .form-header h2 {
        font-size: 1.5rem;
        color: var(--secondary-color);
    }

    .clear-btn {
        background: none;
        border: none;
        color: var(--accent-color);
        text-decoration: underline;
        cursor: pointer;
        font-weight: 500;
        transition: var(--transition);
    }

    .clear-btn:hover {
        color: var(--secondary-color);
    }

    .form-group {
        margin-bottom: 1.5rem;
    }

    label {
        display: block;
        margin-bottom: 0.5rem;
        font-weight: 500;
        color: var(--secondary-color);
    }

    .input-container {
        position: relative;
    }

    .input-container input {
        width: 100%;
        padding: 0.75rem 1rem;
        border: 1px solid #ddd;
        border-radius: 4px;
        font-size: 1rem;
        transition: var(--transition);
    }

    .input-container input:focus {
        outline: none;
        border-color: var(--accent-color);
        box-shadow: 0 0 0 2px rgba(54,94,119,0.2);
    }

    .input-prefix {
        position: absolute;
        left: 1rem;
        top: 50%;
        transform: translateY(-50%);
        color: var(--text-color);
    }

    .input-suffix {
        position: absolute;
        right: 1rem;
        top: 50%;
        transform: translateY(-50%);
        color: var(--text-color);
    }

    .with-prefix input {
        padding-left: 2rem;
    }

    .with-suffix input {
        padding-right: 3rem;
    }

    .radio-group {
        display: flex;
        gap: 1.5rem;
        margin-top: 0.5rem;
    }

    .radio-option {
        display: flex;
        align-items: center;
        cursor: pointer;
    }

    .radio-option input[type="radio"] {
        margin-right: 0.5rem;
        cursor: pointer;
    }

    .calculate-btn {
        background-color: var(--primary-color);
        color: var(--secondary-color);
        border: none;
        padding: 0.75rem 1.5rem;
        border-radius: 4px;
        font-size: 1rem;
        font-weight: 700;
        cursor: pointer;
        transition: var(--transition);
        width: 100%;
        margin-top: 1rem;
    }

    .calculate-btn:hover {
        background-color: #c4c628;
    }

    .results-section {
        background-color: var(--secondary-color);
        color: var(--white);
        border-radius: 8px;
        padding: 2rem;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        text-align: center;
        min-height: 300px;
    }

    .results-empty {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100%;
    }

    .results-empty .financial-illustration {
        width: 150px;
        height: 150px;
        background-color: rgba(255,255,255,0.1);
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
        margin-bottom: 1.5rem;
        font-size: 3rem;
        color: var(--primary-color);
    }

    .results-empty p {
        font-size: 1.1rem;
        margin-bottom: 0.5rem;
    }

    .hint {
        font-size: 0.9rem;
        opacity: 0.8;
    }

    .results-content {
        display: none;
        width: 100%;
    }

    .result-item {
        display: flex;
        justify-content: space-between;
        padding: 1rem 0;
        border-bottom: 1px solid rgba(255,255,255,0.1);
    }

    .result-item:last-child {
        border-bottom: none;
    }

    .result-label {
        font-weight: 500;
    }

    .result-value {
        font-weight: 700;
        font-size: 1.2rem;
    }

    .error-message {
        color: var(--error-color);
        font-size: 0.875rem;
        margin-top: 0.25rem;
        display: none;
    }

    .form-group.error input {
        border-color: var(--error-color);
    }

    .form-group.error .error-message {
        display: block;
    }

    @media (min-width: 768px) {
        .calculator-container {
            flex-direction: row;
        }

        .form-section, .results-section {
            flex: 1;
        }
    }

</style>
</head>
<body>
<div class="container">
    <header>
        <h1>Mortgage Calculator</h1>
    </header>
    <main>
        <div class="calculator-container">
            <!-- Form Section -->
            <section class="form-section">
                <div class="form-header">
                    <h2>Mortgage Calculator</h2>
                    <button type="button" class="clear-btn" id="clearAll">Clear All</button>
                </div>
                <form id="mortgageForm">
                    <div class="form-group" id="mortgageAmountGroup">
                        <label for="mortgageAmount">Mortgage Amount</label>
                        <div class="input-container with-prefix">
                            <span class="input-prefix">£</span>
                            <input type="text" id="mortgageAmount" placeholder="Enter amount">
                        </div>
                        <div class="error-message">This field is required</div>
                    </div>

                    <div class="form-group" id="mortgageTermGroup">
                        <label for="mortgageTerm">Mortgage Term</label>
                        <div class="input-container with-suffix">
                            <input type="text" id="mortgageTerm" placeholder="Enter term">
                            <span class="input-suffix">years</span>
                        </div>
                        <div class="error-message">This field is required</div>
                    </div>

                    <div class="form-group" id="interestRateGroup">
                        <label for="interestRate">Interest Rate</label>
                        <div class="input-container with-suffix">
                            <input type="text" id="interestRate" placeholder="Enter rate">
                            <span class="input-suffix">%</span>
                        </div>
                        <div class="error-message">This field is required</div>
                    </div>

                    <div class="form-group" id="mortgageTypeGroup">
                        <label>Mortgage Type</label>
                        <div class="radio-group">
                            <label class="radio-option">
                                <input type="radio" name="mortgageType" value="repayment" checked> Repayment
                            </label>
                            <label class="radio-option">
                                <input type="radio" name="mortgageType" value="interestOnly"> Interest Only
                            </label>
                        </div>
                        <div class="error-message">Please select a mortgage type</div>
                    </div>

                    <button type="submit" class="calculate-btn">Calculate Repayment</button>
                </form>
            </section>

            <!-- Results Section -->
            <section class="results-section">
                <div class="results-empty" id="resultsEmpty">
                    <div class="financial-illustration">£</div>
                    <p>Results show here</p>
                    <p class="hint">Complete the form and click "Calculate Repayment" to see your monthly repayments.</p>
                </div>

                <div class="results-content" id="resultsContent">
                    <h3>Your Results</h3>
                    <div class="result-item">
                        <span class="result-label">Monthly Repayment</span>
                        <span class="result-value" id="monthlyRepayment">£0.00</span>
                    </div>
                    <div class="result-item">
                        <span class="result-label">Total Repayment</span>
                        <span class="result-value" id="totalRepayment">£0.00</span>
                    </div>
                </div>
            </section>
        </div>
    </main>
</div>

<script>
document.addEventListener('DOMContentLoaded', function() {
    const form = document.getElementById('mortgageForm');
    const clearBtn = document.getElementById('clearAll');
    const resultsEmpty = document.getElementById('resultsEmpty');
    const resultsContent = document.getElementById('resultsContent');
    const monthlyRepayment = document.getElementById('monthlyRepayment');
    const totalRepayment = document.getElementById('totalRepayment');

    const mortgageAmountInput = document.getElementById('mortgageAmount');
    const mortgageTermInput = document.getElementById('mortgageTerm');
    const interestRateInput = document.getElementById('interestRate');

    const mortgageAmountGroup = document.getElementById('mortgageAmountGroup');
    const mortgageTermGroup = document.getElementById('mortgageTermGroup');
    const interestRateGroup = document.getElementById('interestRateGroup');
    const mortgageTypeGroup = document.getElementById('mortgageTypeGroup');

    // Clear form
    clearBtn.addEventListener('click', function() {
        form.reset();
        clearErrors();
        resultsEmpty.style.display = 'flex';
        resultsContent.style.display = 'none';
    });

    // Form submission
    form.addEventListener('submit', function(e) {
        e.preventDefault();
        clearErrors();

        let isValid = true;

        if (!mortgageAmountInput.value.trim()) { showError(mortgageAmountGroup); isValid = false; }
        if (!mortgageTermInput.value.trim()) { showError(mortgageTermGroup); isValid = false; }
        if (!interestRateInput.value.trim()) { showError(interestRateGroup); isValid = false; }

        const mortgageType = document.querySelector('input[name="mortgageType"]:checked');
        if (!mortgageType) { showError(mortgageTypeGroup); isValid = false; }

        if (!isValid) return;

        const principal = parseFloat(mortgageAmountInput.value.replace(/,/g, ''));
        const years = parseFloat(mortgageTermInput.value);
        const annualRate = parseFloat(interestRateInput.value) / 100;
        const monthlyRate = annualRate / 12;
        const numberOfPayments = years * 12;

        let monthlyPayment;
        if (mortgageType.value === 'repayment') {
            monthlyPayment = principal * (monthlyRate * Math.pow(1 + monthlyRate, numberOfPayments)) / 
                             (Math.pow(1 + monthlyRate, numberOfPayments) - 1);
        } else {
            monthlyPayment = principal * monthlyRate;
        }

        const totalPayment = monthlyPayment * numberOfPayments;

        monthlyRepayment.textContent = `£${monthlyPayment.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ',')}`;
        totalRepayment.textContent = `£${totalPayment.toFixed(2).replace(/\B(?=(\d{3})+(?!\d))/g, ',')}`;

        resultsEmpty.style.display = 'none';
        resultsContent.style.display = 'block';
    });

    function clearErrors() {
        document.querySelectorAll('.form-group').forEach(group => group.classList.remove('error'));
    }

    function showError(group) {
        group.classList.add('error');
    }
});
</script>
</body>
</html>

