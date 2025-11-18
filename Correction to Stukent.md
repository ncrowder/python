---


---

<h1 id="what-does-p-value-really-mean">What does p-value REALLY mean?</h1>
<h4 id="the-p-value-gives-us-the-likelihood-i.e.-the-probability-that-we-would-obtain-a-slope-as-large-in-magnitude-as-the-one-we-found-from-performing-linear-regression-if-the-true-relationship-between-x-and-y-were-0-slope--0.">The p-value gives us the likelihood (i.e., the probability) that we would obtain a slope as large (in magnitude) as the one we found from performing linear regression IF the true relationship between x and y were 0 (slope = 0).</h4>
<ul>
<li>A small p-value means the data would be unusual if the true slope were zero, so the slope is probably not zero.</li>
<li>A large p-value means the data are consistent with a true slope of zero, so we cannot conclude there is a relationship.</li>
<li>A large p-value does not prove the slope is zero; it only means the data are too noisy or the effect is too weak to detect.</li>
</ul>
<h3 id="more-specifically-we-historically-use-5-as-the-cutoff.">More specifically, we historically use 5% as the cutoff.</h3>
<h4 id="if-p-≤-.05">If p ≤ .05</h4>
<ul>
<li>There is enough evidence that the slope is different from 0.</li>
<li>The predictor is considered statistically significant.</li>
</ul>
<h4 id="if-p--.05">If p &gt; .05</h4>
<ul>
<li>You do not have strong evidence that the slope differs from zero.</li>
<li>This does not mean the slope equals zero; it means the data do not strongly contradict a zero-slope model.</li>
<li>A non-significant slope still has an estimate and uncertainty. You by all means <strong>should not</strong> replace the slope with zero.</li>
</ul>
<p>The rule stating that If p &gt; .05 you should "ignore the [slope] and consider it as it were zero” is not statistically valid.  This is a grotesque misunderstanding of p-value and statistical significance testing.</p>
<p>A p-value above .05 means the data do not provide strong evidence against the null hypothesis (a zero slope), not that the true slope is zero. Replacing the slope with 0 throws away information and invents certainty that does not exist.</p>
<h3 id="confidence-intervals-and-their-relationship-to-p-values">Confidence intervals and their relationship to p-values</h3>
<p>A confidence interval for a regression slope shows the full range of values that are consistent with your data.</p>
<p>A 95% confidence interval can be interpreted as:</p>
<p><strong>If you repeated the study many times, about 95% of the intervals created using the same procedure would contain the true slope.</strong></p>
<p>In practice, the interval shows the range of slopes that are plausible, given the data.</p>
<p>Here is the key connection to hypothesis testing:</p>
<ul>
<li><strong>If the 95% confidence interval does not contain 0</strong>, then p ≤ .05.
<ul>
<li>This means the slope is significantly different from zero.</li>
</ul>
</li>
<li><strong>If the 95% confidence interval does contain 0</strong>, then p &gt; .05.
<ul>
<li>This means a zero slope is one of the plausible values consistent with the data.  In other words, you cannot rule out the possibility that the true slope is 0.</li>
</ul>
</li>
</ul>
<p>Confidence intervals show the range of slopes that are compatible with the data, giving much more information than a p-value alone.</p>
<h1 id="addendum-why-some-variables-are-treated-as-having-a-slope-of-zero-in-model-selection">Addendum: Why Some Variables Are Treated as Having a Slope of Zero in Model Selection</h1>
<p>In multiple regression, the meaning of a p-value (evidence against the hypothesis that a particular slope is zero) is different from the decision rule used in some model selection methods.</p>
<p>A p-value itself does not require you to set a slope to zero.<br>
It simply tells you whether your data provide strong evidence that the slope is not zero.</p>
<p>However, in certain model selection procedures, especially in traditional stepwise regression, a variable may be dropped from the model if its p-value exceeds a chosen threshold, usually 0.05. When this happens, the variable is removed from the equation entirely, which means that for the final chosen model, its slope is effectively treated as zero.</p>
<p>This is a modeling choice, not a statistical inference.</p>
<h3 id="how-this-works-in-practice">How this works in practice</h3>
<p>Suppose a multiple regression model initially includes five predictors. After fitting the full model:</p>
<ul>
<li>
<p>Predictor A has p = 0.002</p>
</li>
<li>
<p>Predictor B has p = 0.041</p>
</li>
<li>
<p>Predictor C has p = 0.131</p>
</li>
<li>
<p>Predictor D has p = 0.667</p>
</li>
<li>
<p>Predictor E has p = 0.094</p>
</li>
</ul>
<p>In stepwise or backward elimination approaches, predictors C, D, and E would be candidates for removal because their p-values exceed the threshold of 0.05. If those variables are removed, the final model simply does not contain them.</p>
<p>Removing a predictor means the model equation no longer has a term for that variable, which is equivalent to setting its slope coefficient to zero in the final model.  This is not because the p-value “proved” the slope is zero.</p>
<p>Note, that each time a variable predictor is removed we must re-run the regression again using only the remaining variables since our initial estimates for the slopes were based on all the included variables.</p>
<h3 id="important-distinction">Important distinction</h3>
<ul>
<li>
<p>The hypothesis test evaluates whether the evidence supports a non-zero slope.</p>
</li>
<li>
<p>The model selection rule is a decision strategy for choosing which predictors to include.</p>
</li>
<li>
<p>These two things are conceptually different.</p>
</li>
</ul>
<p>A non-significant p-value means “we cannot conclude the slope differs from zero,” but it does not mean the slope equals zero.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

