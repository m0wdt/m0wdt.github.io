---
layout: post
title: "Calculating RF power"
date: 2026-05-05
description: Calculating RF power
--- 

I am often using an oscilloscope to measure the power being delivered by a transmitter. This calulator will convert peak to peak voltage across a 50 Ohm load into power.    

<style>

        .calculator-container {
            background: #f4f4f4;
            allign: center;
            margin-top: 20px;
            margin-bottom: 20px;
            padding: 30px;
            border-radius: 8px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 400px;
        }

        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }
        input[type="number"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 20px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box; /* Important for padding/width consistency */
        }
        button {
            background-color: #2a7ae2;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
        }
        button:hover {
            background-color: #1756a9;
        }
        .results {
            margin-top: 25px;
            padding: 15px;
            border: 1px solid #ddd;
            border-radius: 4px;
            background-color: #e8e8e8;
        }
        .results p {
            margin: 5px 0;
            font-size: 1.1em;
            display: flex;
            justify-content: space-between;
            flex-direction: row;
            align-items: center;
        }
</style>
<div class="calculator-container">
    <h2>RF Power Calculator</h2>

    <label for="vpp">Enter Peak Voltage (Vpp):</label>
    <input type="number" id="vpp" placeholder="Enter Peak Voltage (Vpp)">

    <button id="calculateBtn">Calculate</button>

    <div class="results" id="resultsArea">
        <p><h3>Results:</h3></p>
        <p>Peak Voltage: <span id="peakVpResult">--</span></p>
        <p>RMS Voltage: <span id="rmsVResult">--</span></p>
        <p>Power into 50Ω: <span id="powerResult">--</span></p>
    </div>
</div>
<script>
        document.getElementById('calculateBtn').addEventListener('click', calculate);

        function calculate() {
            const vppInput = document.getElementById('vpp').value;
            const resultsArea = document.getElementById('resultsArea');

            if (!vppInput || parseFloat(vppInput) <= 0) {
                // alert("Please enter a valid Peak Voltage (Vpp).");
                // Reset results if input is invalid
                document.getElementById('peakVpResult').textContent = '--';
                document.getElementById('rmsVResult').textContent = '--';
                document.getElementById('powerResult').textContent = '--';
                return;
            }

            const Vpp = parseFloat(vppInput);

            // Calculate Peak Voltage (Vp)
            const Vp = Vpp / 2;

            // Calculate RMS Voltage (Vrms) 
            const Vrms = Vp / Math.SQRT2;

            // Calculate Power into 50 Ohms (P)
            const R = 50; // Ohms
            const Power = Math.pow(Vrms, 2) / R;

            // Display results, rounding to 3
            document.getElementById('peakVpResult').textContent = `${Vp.toFixed(3)} V`;
            document.getElementById('rmsVResult').textContent = `${Vrms.toFixed(3)} V`;
            document.getElementById('powerResult').textContent = `${Power.toFixed(3)} W`;
        }
    
</script>
<br>


### The Formulas
#### 1. Peak Voltage (Vp)

\[V_{p} = \frac{V_{pp}}{2}\]

#### 2. RMS Voltage (Vrms)

\[V_{rms} = \frac{1}{\sqrt{2}} * V_{p}]


#### 3. Power into 50Ω
The power delivered to a 50 ohm load is calculated using the formula P = Vrms^2 / R.

\[V_{pp} = \sqrt{V_{rms} * 50} \]
  

 

