---


---

<h2 id="linear-regression-lab">Linear Regression Lab</h2>
<p>Use the walkthrough and recording on multiple linear regression to help with these tasks.</p>
<p>As discussed previously, when one-hot encoding a categorical variable with n values, we do not need (and ideally do not keep) all the columns, since knowing that if all n-1 columns show a False or 0, that means the remaining column that was omitted is True or 1.  If a column of HS_Year is one-hot encoded and the columns Freshman, Sophomore, and Junior all show 0, then we know that means Senior  = 1, even if we don’t explicitly have a Senior column.</p>
<ol>
<li>
<p>Go back and refit a multiple linear regression model that uses all the numeric and dummy variables from before but only include the categorical column features that are maintained after using the “drop_first=True” parameter inside of pd.get_dummies.  It looks as if my score (R^2) on the test set was .77 roughly before.  <strong>Show what your resulting R^2 is.  What is the difference in actual price and predicted price for the bottom row in the test set?</strong></p>
</li>
<li>
<p>Because variables that are highly correlated (not just perfectly correlated as is the case with including ALL one-hot encoded variables) need not to be included in a multiple linear regression model, we have more sophisticated options that can help us to see whether a variable in correlated with a combination of all other features, not just looking at one feature compared to another single feature as we have done using the correlation matrix heatmap.  This is called the variance inflation factor.  It calculates for EVERY feature you give it, how well the other features could predict it.  As discussed above in the <em>perfect</em> correlation example: Freshman + Sophomore + Junior + Senior = 1, by definition.  So if we know 3 of these are equal to 0, the other is perfectly predicated to be 1.  In general though, we don’t expect <em>perfect</em> linearity, but if features are ENOUGH correlated to all the other ones, it’s best to drop it.  The following code shows you how to run this.  As a general rule, we should drop those features that have a VIF &gt; 10, and investigate those for which VIF &gt; 5.  <strong>Evaluate the VIF on all numerical variables and variables kept after one-hot encoding with drop_first.  Show the VIF score for all features and which features have a VIF higher than 5 or 10, if any.</strong></p>
</li>
</ol>
<pre class=" language-python"><code class="prism  language-python">
<span class="token keyword">from</span> statsmodels<span class="token punctuation">.</span>stats<span class="token punctuation">.</span>outliers_influence <span class="token keyword">import</span> variance_inflation_factor

vif_df <span class="token operator">=</span> pd<span class="token punctuation">.</span>DataFrame<span class="token punctuation">(</span><span class="token punctuation">)</span>
vif_df<span class="token punctuation">[</span><span class="token string">"feature"</span><span class="token punctuation">]</span> <span class="token operator">=</span> X<span class="token punctuation">.</span>columns
vif_df<span class="token punctuation">[</span><span class="token string">"VIF"</span><span class="token punctuation">]</span> <span class="token operator">=</span> <span class="token punctuation">[</span>variance_inflation_factor<span class="token punctuation">(</span>X<span class="token punctuation">.</span>values<span class="token punctuation">,</span> i<span class="token punctuation">)</span> <span class="token keyword">for</span> i <span class="token keyword">in</span> <span class="token builtin">range</span><span class="token punctuation">(</span>X<span class="token punctuation">.</span>shape<span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">]</span>

</code></pre>
<ol start="3">
<li>The score() function return the R^2 value, but as mentioned in lecture R^2 will always grow the more features that are added, but this can result in a case of overfitting if we aren’t careful.  A better choice is adjusted-R^2 in this case, which drops when a new feature is added if the baseline R^2 does not increase enough to justify it.  <strong>Choose a set of features (if using categorical one-hot encode using the drop_first = True parameter) and calculate both R and adjusted R^2.  Then add an additional feature and calculate R and adjusted R^2 again.</strong>  Try to pick a feature to add that you think might not add that much new predictive power (e.g. it’s correlated to your others).  The formula for computing adjusted R^2 depends on the number of predictors and the number of rows.  Here’s a code snippet to work from:</li>
</ol>
<pre class=" language-python"><code class="prism  language-python">
<span class="token keyword">import</span> numpy <span class="token keyword">as</span> np

<span class="token comment"># Fit your model</span>
model <span class="token operator">=</span> LinearRegression<span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">.</span>fit<span class="token punctuation">(</span>X<span class="token punctuation">,</span> y<span class="token punctuation">)</span>

<span class="token comment"># Get R^2</span>
r2 <span class="token operator">=</span> model<span class="token punctuation">.</span>score<span class="token punctuation">(</span>X<span class="token punctuation">,</span> y<span class="token punctuation">)</span>

<span class="token comment"># n = number of rows, p = number of predictors</span>
n <span class="token operator">=</span> X<span class="token punctuation">.</span>shape<span class="token punctuation">[</span><span class="token number">0</span><span class="token punctuation">]</span>
p <span class="token operator">=</span> X<span class="token punctuation">.</span>shape<span class="token punctuation">[</span><span class="token number">1</span><span class="token punctuation">]</span>

<span class="token comment"># Adjusted R^2</span>
adj_r2 <span class="token operator">=</span> <span class="token number">1</span> <span class="token operator">-</span> <span class="token punctuation">(</span><span class="token number">1</span> <span class="token operator">-</span> r2<span class="token punctuation">)</span> <span class="token operator">*</span> <span class="token punctuation">(</span>n <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">)</span> <span class="token operator">/</span> <span class="token punctuation">(</span>n <span class="token operator">-</span> p <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">)</span>

<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"R^2:"</span><span class="token punctuation">,</span> r2<span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Adjusted R^2:"</span><span class="token punctuation">,</span> adj_r2<span class="token punctuation">)</span>
</code></pre>
<ol start="4">
<li>Another tool we can employ is the so-called Lasso Regression.  The mathematics involves some higher-level ideas, but generally speaking Lasso not only tries to minimize the root mean square error (RMSE) but it also adds a penalty if any of the coefficients in the model grow too large, and this is normally caused by features being closely correlated.  That’s all you need to know from a theoretical standpoint.  You can use the resulting coefficients decided upon by Lasso to make predictions as normal. Coefficients that end up as zero have essentially shown that the corresponding feature has been eliminated from the model.   Scaling before running Lasso is essential especially here, since the penalty is directly related to the size of the coefficients.  Here’s a code snippet (where X has been scaled):</li>
</ol>
<pre class=" language-python"><code class="prism  language-python">
<span class="token keyword">from</span> sklearn<span class="token punctuation">.</span>linear_model <span class="token keyword">import</span> LassoCV

<span class="token comment"># 1. Fit LassoCV</span>
lasso <span class="token operator">=</span> LassoCV<span class="token punctuation">(</span>cv<span class="token operator">=</span><span class="token number">5</span><span class="token punctuation">,</span> random_state<span class="token operator">=</span><span class="token number">0</span><span class="token punctuation">)</span><span class="token punctuation">.</span>fit<span class="token punctuation">(</span>X<span class="token punctuation">,</span> y<span class="token punctuation">)</span>

<span class="token comment"># 2. Coefficients table</span>
coef_table <span class="token operator">=</span> pd<span class="token punctuation">.</span>DataFrame<span class="token punctuation">(</span><span class="token punctuation">{</span>
    <span class="token string">"feature"</span><span class="token punctuation">:</span> X<span class="token punctuation">.</span>columns<span class="token punctuation">,</span>
    <span class="token string">"coef"</span><span class="token punctuation">:</span> lasso<span class="token punctuation">.</span>coef_
<span class="token punctuation">}</span><span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span>coef_table<span class="token punctuation">)</span>

<span class="token comment"># 3. Lists of selected and dropped features</span>
selected <span class="token operator">=</span> coef_table<span class="token punctuation">[</span>coef_table<span class="token punctuation">[</span><span class="token string">"coef"</span><span class="token punctuation">]</span> <span class="token operator">!=</span> <span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">"feature"</span><span class="token punctuation">]</span>
dropped  <span class="token operator">=</span> coef_table<span class="token punctuation">[</span>coef_table<span class="token punctuation">[</span><span class="token string">"coef"</span><span class="token punctuation">]</span> <span class="token operator">==</span> <span class="token number">0</span><span class="token punctuation">]</span><span class="token punctuation">[</span><span class="token string">"feature"</span><span class="token punctuation">]</span>

<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Selected features:"</span><span class="token punctuation">,</span> <span class="token builtin">list</span><span class="token punctuation">(</span>selected<span class="token punctuation">)</span><span class="token punctuation">)</span>
<span class="token keyword">print</span><span class="token punctuation">(</span><span class="token string">"Dropped features:"</span><span class="token punctuation">,</span> <span class="token builtin">list</span><span class="token punctuation">(</span>dropped<span class="token punctuation">)</span><span class="token punctuation">)</span>

<span class="token comment"># 4. Generate predictions</span>
y_pred <span class="token operator">=</span> lasso<span class="token punctuation">.</span>predict<span class="token punctuation">(</span>X_test<span class="token punctuation">)</span>

</code></pre>
<p><strong>What features (if any) were eliminated using Lasso?  What are the features and prediction for the 100th row of the dataset?  How far is the prediction from the actual?</strong></p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

