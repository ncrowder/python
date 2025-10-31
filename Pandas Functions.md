---


---

<h1 id="useful-pandas-functions">Useful Pandas Functions</h1>
<p>In general, most of these functions are automatically applied column by column unless axis = 1 is specified inside parentheses.</p>
<h3 id="functions-for-summarizing-or-aggregating">Functions for summarizing or aggregating:</h3>
<ul>
<li>Sum()</li>
<li>Prod()</li>
<li>Mean()</li>
<li>Median()</li>
<li>Mode()</li>
<li>Min()</li>
<li>Max()</li>
<li>Count()</li>
<li>Nunique()</li>
</ul>
<p>The Describe() method will return many of these measures with one single call.  It works by default on all numeric columns.</p>
<h3 id="functions-for-providing-cumulative-measures">Functions for providing cumulative measures:</h3>
<ul>
<li>Cumsum()</li>
<li>Cumprod()</li>
<li>Cummax()</li>
<li>Cummin()</li>
</ul>
<h3 id="functions-for-identifying-the-index">Functions for identifying the index:</h3>
<ul>
<li>Idxmin()</li>
<li>Idxmax()</li>
</ul>
<h3 id="functions-which-compute-on-2-rowscolumns-at-once">Functions which compute on 2 rows/columns at once:</h3>
<ul>
<li>diff()</li>
<li>pct_change()</li>
</ul>
<h3 id="applied-on-the-whole-seriesframe">Applied on the whole series/frame:</h3>
<ul>
<li>round()</li>
<li>abs()</li>
</ul>
<hr>
<h3 id="value-counts">Value Counts</h3>
<p>Value_Counts() is another function worth mentioning.  If you call it directly on a df it returns a result that’s hard to decipher, so it’s best to call it directly on a series.  The result is a series with the original series values as the index and the counts (frequency) of each of the original values as the data.</p>
<h2 id="multiple-functions-performed-at-once">Multiple functions performed at once</h2>
<p>You can apply multiply functions at once if you place them in a list inside the agg method with quotes and no arguments.  As an example:</p>
<pre><code>df.agg ( [ 'idxmin', 'idxmax' ] )  
</code></pre>
<p>would return a dataframe with indices (row labels) of ‘idxmin’ and ‘idxmax’, columns corresponding to the rows of df, and the data would indicate the original row in which the min value or maximum value of that column occurred.</p>
<h2 id="using-a-custom-function">Using a custom function</h2>
<p>If we would like to use a custom function down each column we would use the apply method and feed the function in as an argument.</p>
<p>If we would like to do the same thing but across each row, we’d specify axis = 1.</p>
<p>If we are interested in applying the function to each individual element instead, we would use the map method instead of apply.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

