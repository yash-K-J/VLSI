<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>8-bit Left Shift Register</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Source+Serif+4:wght@400;600;700&family=Source+Code+Pro:wght@400;600&display=swap');

  :root {
    --blue: #1a5fa8;
    --green: #2a7a2a;
    --border: #b0b0b0;
    --light: #f5f7fa;
    --text: #1a1a1a;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'Source Serif 4', Georgia, serif;
    font-size: 15px;
    color: var(--text);
    background: #fff;
    max-width: 900px;
    margin: 0 auto;
    padding: 48px 36px;
    line-height: 1.75;
  }

  .cover {
    text-align: center;
    padding: 48px 0 32px;
    border-bottom: 3px double #ccc;
    margin-bottom: 40px;
  }
  .cover h1 {
    font-size: 2.2em;
    font-weight: 700;
    text-decoration: underline;
    letter-spacing: -0.5px;
    margin-bottom: 28px;
  }
  .cover .subtitle { font-size: 0.95em; color: #444; margin: 6px 0; }
  .cover .authors  { font-weight: 700; font-size: 1em; margin: 20px 0 6px; }
  .cover .supervisor { font-size: 0.95em; color: #333; }

  hr { border: none; border-top: 1.5px solid #ccc; margin: 36px 0; }

  h2 {
    color: var(--blue);
    font-size: 1.35em;
    border-bottom: 2px solid var(--blue);
    padding-bottom: 5px;
    margin: 40px 0 16px;
  }
  h3 { color: var(--blue); font-size: 1.1em; font-weight: 700; margin: 28px 0 10px; }
  h4 { font-size: 1em; font-weight: 700; margin: 20px 0 8px; }

  p  { margin-bottom: 12px; }
  ul, ol { margin: 8px 0 12px 28px; }
  li { margin: 5px 0; }
  ul ul, ol ol, ul ol, ol ul { margin: 4px 0 4px 20px; }

  .toc {
    background: var(--light);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 20px 32px;
    margin: 16px 0 32px;
  }
  .toc ol { margin: 0 0 0 18px; }
  .toc li { margin: 5px 0; font-weight: 600; }
  .toc li ol { font-weight: 400; margin-top: 3px; }

  table { border-collapse: collapse; margin: 16px auto; width: auto; min-width: 340px; }
  th, td { border: 1px solid var(--border); padding: 9px 18px; text-align: center; font-size: 0.95em; }
  th { background: var(--light); font-weight: 700; }

  .formula { text-align: center; font-style: italic; margin: 10px 0; font-size: 0.97em; }

  figure { margin: 24px 0; text-align: center; }
  figure img { max-width: 100%; border: 1px solid #ccc; border-radius: 4px; display: block; margin: 0 auto; }
  figcaption { font-size: 0.82em; color: #555; font-style: italic; margin-top: 7px; }

  .sig  { color: var(--green); font-family: 'Source Code Pro', monospace; font-size: 0.93em; }
  code  { background: #eef1f5; padding: 2px 6px; border-radius: 3px; font-family: 'Source Code Pro', monospace; font-size: 0.88em; }
</style>
</head>
<body>

<!-- COVER -->
<div class="cover">
  <h1>8-bit Left Shift Register</h1>
  <p class="subtitle"><strong>ED221:</strong> Digital IC Design Tape in &amp; Tape out Lab</p>
  <br>
  <p class="subtitle"><em>CMOS Implementation of an 8-Bit Left Shift Register in Cadence</em></p>
  <br>
  <p class="authors">
    Mansi Mangukiya - 202404021<br>
    Rashi Krishnani - 202404018<br>
    Yash Judal - 202404014
  </p>
  <br>
  <p class="supervisor"><strong>Supervised By:</strong> Biswajit Mishra</p>
</div>

<!-- CONTENTS -->
<h2>Contents</h2>
<div class="toc">
  <ol>
    <li>Introduction</li>
    <li>Circuit Schematic</li>
    <li>Pin Configuration</li>
    <li>Delays of Components used</li>
    <li>Power Characteristics (DATA = 11111111)</li>
    <li>Calculations</li>
    <li>Functional Description
      <ol>
        <li>SIPO</li><li>PISO</li><li>MUX</li><li>AND</li>
      </ol>
    </li>
    <li>Working</li>
    <li>Example stimulation of 7 - Bit Left Shift of 11111111</li>
    <li>LAYOUT</li>
    <li>AREA ANALYSIS</li>
    <li>POST LAYOUT &amp; PRE LAYOUT COMPARISION</li>
  </ol>
</div>

<hr>

<!-- 1 -->
<h2>1 | Introduction</h2>
<p>The 8-bit Left Shift Register circuit is implemented using a combination of Parallel-In Serial-Out (PISO), Serial-In Serial-Out (SISO) registers, multiplexers, and logic gates to perform logical left-shift operations on 8-bit data. The design operates at a nominal supply voltage of 1.8V and is implemented and simulated in Cadence Virtuoso. The register supports synchronized clock-driven shifting, serial data transfer, and logical left-shift functionality.</p>

<hr>

<!-- 2 -->
<h2>2 | Circuit Schematic</h2>
<figure>
  <img src="8blsr_schematic.png" alt="8-bit Left Shift Register Schematic">
  <figcaption>8-bit Left Shift Register — Top-level Schematic (Cadence Virtuoso)</figcaption>
</figure>

<h3>SYMBOL</h3>
<figure>
  <img src="8blsr_symbol.png" alt="LEFTSHIFT Symbol">
  <figcaption>LEFTSHIFT Symbol — CLK, SELECT, IN, LOADSTORE inputs; OUT, EN outputs</figcaption>
</figure>

<h3>PISO</h3>
<figure>
  <img src="piso_schematic.png" alt="PISO Schematic">
  <figcaption>PISO (Parallel-In Serial-Out) Schematic</figcaption>
</figure>

<h3>SIPO</h3>
<figure>
  <img src="sipo_schematic.png" alt="SIPO Schematic">
  <figcaption>SIPO (Serial-In Parallel-Out) Schematic</figcaption>
</figure>

<hr>

<!-- 3 -->
<h2>3 | Pin Configuration</h2>
<table>
  <tr><th>Pin</th><th>Description</th></tr>
  <tr><td>VDD</td><td>Supply voltage (1.8V)</td></tr>
  <tr><td>GND</td><td>Ground (0V)</td></tr>
  <tr><td>CLK</td><td>Clock input</td></tr>
  <tr><td>IN</td><td>Serial data input (MSB first)</td></tr>
  <tr><td>LOADSTORE</td><td>Control signal for load/shift operation</td></tr>
  <tr><td>SELECT</td><td>Shift operation select input</td></tr>
  <tr><td>EN</td><td>Enable signal for clock operation</td></tr>
  <tr><td>OUT</td><td>Serial Output (MSB first)</td></tr>
</table>

<hr>

<!-- 4 -->
<h2>4 | Delays of Components used</h2>
<table>
  <tr><th>Components</th><th>Delay</th></tr>
  <tr><td>AND Gate</td><td>227.7 ps</td></tr>
  <tr><td>OR Gate</td><td>174.05 ps</td></tr>
  <tr><td>MUX</td><td>189.72 ps</td></tr>
  <tr><td>LATCH</td><td>428.395 ps</td></tr>
  <tr><td>D Flip-Flop</td><td>506.35 ps</td></tr>
</table>
<ul>
  <li><strong>8-BIT LEFT SHIFT REGISTER DELAY (DATA = 11111111):</strong> 0.74 ns</li>
</ul>

<hr>

<!-- 5 -->
<h2>5 | Power Characteristics (DATA = 11111111)</h2>
<table>
  <tr><th>Parameter</th><th>Symbol</th><th>Value</th><th>Unit</th></tr>
  <tr><td>Average Current</td><td>I<sub>avg</sub></td><td>64.18</td><td>µA</td></tr>
  <tr><td>Peak Current</td><td>I<sub>peak</sub></td><td>2.92</td><td>mA</td></tr>
  <tr><td>Average Power</td><td>P<sub>avg</sub></td><td>115.524</td><td>µW</td></tr>
</table>

<hr>

<!-- 6 -->
<h2>6 | Calculations</h2>
<ul><li><strong>Average Power Consumption:</strong></li></ul>
<div class="formula">Average Power = V<sub>DD</sub> × I<sub>avg</sub></div>
<div class="formula">Average Power = 1.8 V × 64.18 µA</div>
<div class="formula">Average Power = 115.524 µW</div>
<ul><li><strong>Energy Consumption:</strong></li></ul>
<div class="formula">Energy = T<sub>sim</sub> × P<sub>avg</sub></div>
<div class="formula">Energy = 500 ns × 115.524 µW</div>
<div class="formula">Energy = 57.762 µJ</div>

<hr>

<!-- 7 -->
<h2>7 | Functional Description</h2>

<h3>7.1. SIPO</h3>
<ul>
  <li>SIPO is used for serial data input and left-shift data transfer operations. The shifted data is obtained serially with the MSB appearing first at the output.</li>
</ul>

<h3>7.2. PISO</h3>
<ul>
  <li>PISO is used for parallel data loading and serial data output operations. The stored 8-bit data is shifted out serially with the MSB appearing first at the output.</li>
  <li><span class="sig">LOADSTORE</span> is the control signal used for load and shift operations. When <span class="sig">LOADSTORE</span> = 0, the data is loaded into the register, and when <span class="sig">LOADSTORE</span> = 1, the data is shifted and given serially at output.</li>
</ul>

<h3>7.3. MUX</h3>
<ul>
  <li>MUX is used to select the amount of left-shift operation to be performed on the data. The shift selection is controlled using the <span class="sig">SELECT</span> input pin.</li>
</ul>
<table>
  <tr><th>SELECT</th><th>Function</th></tr>
  <tr><td>0</td><td>Extra zeroes for shifting</td></tr>
  <tr><td>1</td><td>Data in</td></tr>
</table>

<h3>7.4. AND</h3>
<ul>
  <li>The AND gates are used to control the clock signals of the SIPO and PISO shift registers using the Enable (EN) signal.
    <ul><li>For <strong>PISO</strong>, the clock is generated by:</li></ul>
  </li>
</ul>
<div class="formula">CLK<sub>PISO</sub> = CLK · EN</div>
<div class="formula">CLK<sub>SIPO</sub> = CLK · EN<em>bar</em></div>

<hr>

<!-- 8 -->
<h2>8 | Working</h2>
<h3>8.1. Stages of Operation of the SIPO–PISO System</h3>
<ul>
  <li><strong>Stage 1: Data Input</strong>
    <ul>
      <li>The serial input data is applied to the input line.</li>
      <li>Clock pulses are provided to synchronize the data transfer.</li>
      <li>At this stage, the system starts receiving bits one by one.</li>
    </ul>
  </li>
  <li><strong>Stage 2: SIPO Mode ON (Serial-In Parallel-Out)</strong>
    <ul>
      <li>The SIPO shift register is enabled.</li>
      <li>With every clock pulse, the incoming serial data shifts through the flip-flops.</li>
      <li>After all bits are received, the complete data becomes available in parallel form at the SIPO outputs.</li>
      <li>The SIPO stores and arranges the data properly for the next stage.</li>
    </ul>
  </li>
  <li><strong>Stage 3: PISO Mode ON (Parallel-In Serial-Out)</strong>
    <ul>
      <li>Once all parallel data is available from the SIPO, the PISO register is enabled.</li>
      <li>The enable signal is ANDed with the clock signal before being applied to the PISO.</li>
      <li>The PISO loads the parallel data from the SIPO outputs.</li>
      <li>On each clock pulse, the PISO shifts the data serially and provides serial output bit by bit.</li>
    </ul>
  </li>
</ul>

<hr>

<!-- 9 -->
<h2>9 | Example stimulation of 7 - Bit Left Shift of 11111111</h2>
<ol>
  <li>The input data <span class="sig">11111111</span> is applied through the <span class="sig">IN</span> pin, and the <span class="sig">SELECT</span> line of the MUX is kept at logic 1 so that the data can be serially entered into the SIPO register, which receives all 8 bits sequentially.</li>
  <li>After loading the complete data, the <span class="sig">SELECT</span> line is changed to logic 0 to perform the 7-bit left-shift operation by inserting seven zeros, due to which the output of the SIPO register becomes:
    <div class="formula"><strong style="color:var(--green);font-family:monospace;font-size:1.1em;">00000001</strong></div>
  </li>
  <li>During the shifting operation, the <span class="sig">LOADSTORE</span> signal remains at logic 1, so the shifted data is not loaded into the PISO register.</li>
  <li>After obtaining the shifted output from the SIPO register, the <span class="sig">LOADSTORE</span> signal is changed to logic 0 to load the data into the PISO register.</li>
  <li>The PISO register then sends the data serially from <span class="sig">MSB</span> to <span class="sig">LSB</span> through the output pin.</li>
</ol>

<h3>Setup:</h3>

<h4>1. Clock:</h4>
<ul>
  <li>The clock signal is configured with a time period of <code>20 ns</code> and a duty cycle of <code>50%</code>, where the ON time and OFF time are each equal to <code>10 ns</code>.</li>
</ul>
<figure>
  <img src="clk_diagram.png" alt="Clock Signal Waveform">
  <figcaption>Clock Signal — 20 ns period, 50% duty cycle</figcaption>
</figure>

<h4>2. Data:</h4>
<ul>
  <li>The data is sampled at the positive edge of the clock. Therefore, the data duration for one bit is equal to one complete clock cycle, i.e., <code>20 ns</code>.</li>
  <li>For example, if the input data is <code>10101010</code>, the ON time would be <code>20 ns</code> and the total cycle time would be <code>40 ns</code>. In this design, the input data used is <code>11111111</code>; therefore, the input behaves as a constant DC voltage of <code>1.8 V</code>, continuously representing logic 1.</li>
</ul>
<figure>
  <img src="data_diagram.png" alt="Data Signal Waveform">
  <figcaption>Data Signal — constant 1.8 V for input 11111111</figcaption>
</figure>

<h4>3. Select:</h4>
<ul>
  <li>Initially, the <span class="sig">SELECT</span> signal is set to logic 1 to allow serial loading of all 8 bits into the SIPO register. Since each bit requires <code>20 ns</code>, the total loading time is:
    <div class="formula">8 × 20 = 160 ns</div>
    For proper setup timing, the SELECT signal is kept high for <code>159 ns</code>.
  </li>
  <li>After loading the data, the <span class="sig">SELECT</span> signal is changed to logic 0 to perform the left-shift operation. Since the data is shifted by 7 bits, seven zeros are inserted. Therefore, the required shifting time is:
    <div class="formula">7 × 20 = 140 ns</div>
  </li>
</ul>
<figure>
  <img src="select_diagram.png" alt="SELECT Signal Waveform">
  <figcaption>SELECT Signal — high for 159 ns (load), then low for 140 ns (shift)</figcaption>
</figure>

<h4>4. ENABLE:</h4>
<ul>
  <li>During the initial loading and shifting operations, the PISO register should not load the data. Therefore, the <span class="sig">ENABLE</span> signal remains at logic 0 during this duration:
    <div class="formula">159 + 140 ≈ 300 ns</div>
  </li>
  <li>Then for 8 clock cycles PISO would be ON and will give serial output. Therefore, the <span class="sig">ENABLE</span> signal remains at logic 1 during this duration:
    <div class="formula">8 × 20 = 160 ns</div>
  </li>
  <li>After the shifted output becomes available, the <span class="sig">LOADSTORE</span> signal is changed to logic 0 for one clock cycle (<code>20 ns</code>) so that the PISO register can load the shifted data.</li>
  <li>Once the data is loaded, the PISO register returns to shift mode, and the <span class="sig">LOADSTORE</span> signal becomes logic 1 again.</li>
</ul>
<figure>
  <img src="enable_diagram.png" alt="ENABLE Signal Waveform">
  <figcaption>ENABLE Signal — low for ~300 ns, then high for 160 ns</figcaption>
</figure>

<h4>5. LOADSTORE:</h4>
<ul>
  <li>During the initial loading and shifting operations, the PISO register should not load the data. Therefore, the <span class="sig">LOADSTORE</span> signal remains at logic 1 during this duration:
    <div class="formula">159 + 140 ≈ 300 ns + 20 ns (For setup time of ENABLE) = 320 ns</div>
  </li>
  <li>After the shifted output becomes available, the <span class="sig">LOADSTORE</span> signal is changed to logic 0 for one clock cycle (<code>20 ns</code>) so that the PISO register can load the shifted data.</li>
  <li>Once the data is loaded, the PISO register returns to shift mode, and the <span class="sig">LOADSTORE</span> signal becomes logic 1 again.</li>
</ul>
<figure>
  <img src="loadstore_diagram.png" alt="LOADSTORE Signal Waveform">
  <figcaption>LOADSTORE Signal — high for 320 ns, low pulse for 20 ns (load), then high again</figcaption>
</figure>

<h3>OVERALL TIMING DIAGRAM:</h3>
<figure>
  <img src="8blsr_diagram.png" alt="Overall Timing Diagram">
  <figcaption>Overall Timing Diagram — SELECT, LOADSTORE, ENABLE, OUT, CLK, Data signals</figcaption>
</figure>

<h3>7.3. Analysis time</h3>
<ul>
  <li>The total analysis time is calculated as:
    <div class="formula">320 + 170 = 490 ns</div>
  </li>
  <li>Therefore, the simulation analysis time is taken as:
    <div class="formula">500 ns</div>
  </li>
</ul>

<hr>

<!-- 10 -->
<h2>10 | LAYOUT</h2>

<h3>PISO:</h3>
<figure>
  <img src="piso_layout.png" alt="PISO Layout">
  <figcaption>PISO Layout — Cadence Virtuoso GXL</figcaption>
</figure>

<h3>SIPO:</h3>
<figure>
  <img src="sipo_layout.png" alt="SIPO Layout">
  <figcaption>SIPO Layout — Cadence Virtuoso GXL</figcaption>
</figure>

<h3>FINAL LAYOUT:</h3>
<figure>
  <img src="8blsr_layout.png" alt="Final Complete Layout">
  <figcaption>Final Complete Layout — 8-bit Left Shift Register</figcaption>
</figure>

<h3>LAYOUT BREAKDOWN:</h3>
<figure>
  <img src="8blsr_layout_breakdown.png" alt="Layout Breakdown">
  <figcaption>Layout Breakdown — PISO (top), MUX (left), SIPO (bottom) regions annotated</figcaption>
</figure>

<hr>

<!-- 11 -->
<h2>11 | AREA ANALYSIS</h2>
<div class="formula"><strong>Height = 98.85 µm</strong></div>
<div class="formula"><strong>Width = 316.06 µm</strong></div>
<br>
<div class="formula"><strong>Area = Height × Width</strong></div>
<div class="formula"><strong>Area = 98.85 µm × 316.06 µm</strong></div>
<div class="formula"><strong>Area = 3.124 × 10<sup>4</sup> µm²</strong></div>

<hr>

<!-- 12 -->
<h2>12 | POST LAYOUT &amp; PRE LAYOUT COMPARISION</h2>
<ul>
  <li>Delay added due to parasitic capacitance &amp; resistance: 0.5003 ns</li>
  <li>Pre Layout delay = 0.74 ns</li>
  <li>Post Layout delay = 0.74 + 0.5003 = 1.2407 ns</li>
</ul>

<h3>12.1. Post Layout Power Analysis</h3>
<table>
  <tr><th>Parameter</th><th>Symbol</th><th>Value</th><th>Unit</th></tr>
  <tr><td>Average Current</td><td>I<sub>avg</sub></td><td>103.2</td><td>µA</td></tr>
  <tr><td>Peak Current</td><td>I<sub>peak</sub></td><td>3.616</td><td>mA</td></tr>
  <tr><td>Average Power</td><td>P<sub>avg</sub></td><td>185.76</td><td>µW</td></tr>
</table>
<ul><li><strong>Average Power Consumption:</strong></li></ul>
<div class="formula">Average Power = V<sub>DD</sub> × I<sub>avg</sub></div>
<div class="formula">Average Power = 1.8 V × 103.2 µA</div>
<div class="formula">Average Power = 185.76 µW</div>
<ul><li><strong>Energy Consumption:</strong></li></ul>
<div class="formula">Energy = T<sub>sim</sub> × P<sub>avg</sub></div>
<div class="formula">Energy = 500 ns × 185.76 µW</div>
<div class="formula">Energy = 92.88 µJ</div>

</body>
</html>
