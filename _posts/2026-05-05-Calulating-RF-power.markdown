---
layout: post
title: "Calculating RF power"
date: 2026-05-05
description: Calculating RF power
custom_css: /assets/css/calculators.css
--- 

I am often using an oscilloscope to measure the power being delivered by a transmitter. This calulator will convert peak to peak voltage across a 50 Ohm load into power.    

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
        <p>Power into 50Ω dBm: <span id="powerResultDbM">--</span></p>
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
                document.getElementById('powerResultDbM').textContent = '--';
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
            document.getElementById('powerResultDbM').textContent = `${(10 * Math.log10((Power*1000)/1)).toFixed(2)} dBm`;
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
  
#### 4. Power into 50Ω dBm
\[P_{dBm} = 10 \log_{10}(\frac{P_{mW}}{1 mW})\]
 

