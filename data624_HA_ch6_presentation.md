<style>

body {
  background-color:#97D8B2;
}

.reveal h1 {
  line-height: 100px;
}

.reveal td {
  vertical-align:top
}

.center-text-large p {
  font-size: 90px;
  text-align: center;
}

.reveal table {
  width:100%
}

.reveal table, .reveal table td, .reveal table th {
  border-style: none;
}

</style>

DATA 624 - Forecasting: Principles and Practice - Chapter 6
========================================================
author: John Grando & Alex Low
date: 2/5/19
autosize: true

<div class='center-text-large'>
  <p>Time Series Decomposition</p>
</div>



Overview - Time Series Decomposition
========================================================

Decomposition of data into separate parts
<table>
<tr>
<td style="vertical-align:middle;" width=15%>
<ul>
<li>Trend-cycle (Trend)</li>
<li>Seasonality</li>
<li>Remainder</li>
</ul>
</td>
<td style="vertical-align:middle;">
<img src="data624_HA_ch6_presentation-figure/unnamed-chunk-2-1.png" title="plot of chunk unnamed-chunk-2" alt="plot of chunk unnamed-chunk-2" style="display: block; margin: auto;" />
</td>
</tr>
</table>

Formulaic Representation
========================================================
<br>
- Additive
  - $y_{t} = S_{t} + T_{t} + R{t}$
- Multiplicative
  - $y_{t} = S_{t} \times T_{t} \times R{t}$
  - $y_{t} = \log{S_{t}} + \log{T_{t}} + \log{R{t}}$

Moving Averages (MA)
========================================================

MAs are ussed to estimate trend-cycles and are simply an average value over a set time period

<table>
<tr>
<td>
<img src="data624_HA_ch6_presentation-figure/unnamed-chunk-3-1.png" title="plot of chunk unnamed-chunk-3" alt="plot of chunk unnamed-chunk-3" style="display: block; margin: auto;" />
</td>
</tr>
</table>

Moving Averages of Moving Averages (MA #x#)
========================================================

Moving Averages of Moving Averages can even be taken to further smooth the trend.  The first MA has been downshifted to a value of 4 to show a noticable difference between curves.

<table>
<tr>
<td>
<img src="data624_HA_ch6_presentation-figure/unnamed-chunk-4-1.png" title="plot of chunk unnamed-chunk-4" alt="plot of chunk unnamed-chunk-4" style="display: block; margin: auto;" />
</td>
</tr>
</table>

Classical Decomposition
========================================================

<table>
<tr>
<th>Additive</th>
<th>Multiplicative</th>
</tr>
<tr>
<td>
  <ol>
    <li>Compute Trend Cycle using MA (even m: 2xm, odd m:m) where m is the seasonal period <br>$\hat{T_{t}}$</li>
    <li>Calculate detrended series by subtraction <br>$y_{t}-\hat{T_{t}}$</li>
    <li>Estimate seasonal component <br>$\hat{S_{t}}$</li>
    <li>Calculate remainder by subracting all the above from the data <br>$\hat{R_{t}} = y_{t}-\hat{T_{t}}-\hat{S_{t}}$</li>
  </ol>
</td>
<td>
  <ol>
    <li>Compute Trend Cycle using MA (even m: 2xm, odd m:m) where m is the seasonal period <br>$\hat{T_{t}}$</li>
    <li>Calculate detrended series by division <br>$\frac{y_{t}}{\hat{T_{t}}}$</li>
    <li>Estimate seasonal component <br>$\hat{S_{t}}$</li>
    <li>Calculate remainder by subracting all the above from the data <br>$R_{t} = \frac{y_{t}}{\left( \hat{T_{t}}\hat{S_{t}} \right)}$</li>
  </ol>
</td>
</tr>
</table>

X11
========================================================

Similar to classical decomposition; however, has many additional steps to account for drawbacks using the classical method.

<img src="data624_HA_ch6_presentation-figure/unnamed-chunk-5-1.png" title="plot of chunk unnamed-chunk-5" alt="plot of chunk unnamed-chunk-5" style="display: block; margin: auto;" />


SEATS
========================================================

<strong>S</strong>easonal <strong>E</strong>xtraction in <strong>A</strong>RIMA <strong>T</strong>ime <strong>S</strong>eries.  Only works with quarterly and monthly data, and details of methodology beyond the scope of this book.

<img src="data624_HA_ch6_presentation-figure/unnamed-chunk-6-1.png" title="plot of chunk unnamed-chunk-6" alt="plot of chunk unnamed-chunk-6" style="display: block; margin: auto;" />

STL
========================================================

<strong>S</strong>easonal and <strong>T</strong>rend decomposition using <strong>L</strong>oess.  Has many advantages over other methods which inludes; handling any type of seasonality, changing seasonality over time, trend smoothness control, and robust to outliers.  However, it has some disadvantages; only additive decomposition, difficulty with calendar variations.

<img src="data624_HA_ch6_presentation-figure/unnamed-chunk-7-1.png" title="plot of chunk unnamed-chunk-7" alt="plot of chunk unnamed-chunk-7" style="display: block; margin: auto;" />

Forecasting
========================================================

Forecasts can be easily made using the decomposed components which can be rewritten as follows: 

<table>
<tr>
<th>Additive</th>
<th>Multiplicative</th>
</tr>
<tr>
<td>
  $y_{t}=\hat{S_{t}} + \hat{A_{t}}$<br>
  $\hat{A_{t}}=\hat{T_{t}} + \hat{R_{t}}$
</td>
<td>
  $y_{t}=\hat{S_{t}} \times \hat{A_{t}}$<br>
  $\hat{A_{t}}=\hat{T_{t}} \times \hat{R_{t}}$
</td>
</tr>
</table>

Then, the seasonal component and seasonally adjusted component can be forecast separately

Forecasting
========================================================

<img src="data624_HA_ch6_presentation-figure/unnamed-chunk-8-1.png" title="plot of chunk unnamed-chunk-8" alt="plot of chunk unnamed-chunk-8" style="display: block; margin: auto;" />

