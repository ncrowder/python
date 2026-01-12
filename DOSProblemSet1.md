---


---

<h1 id="dos-problem-set-1">DOS Problem Set 1</h1>
<ol>
<li>
<p>Simulate a deterministic process where a social media influencer wishes to reach 20,000 followers in 15 weeks.  Given her past experience, she assumes that each week she will get 1.5k new followers that had never followed the page and of her current followers she believes 8% will stop following the page each week. However, 15% of those that left the page in the past will join again each week. Will she reach her target if she’s starting fresh with 0 followers?</p>
</li>
<li>
<p>Create a function with the following signature:</p>
</li>
</ol>
<pre><code>social_media_sim(followers, weeks, new, per_unfollow, per_refollows)
</code></pre>
<p>such that the user can type in their own values for required followers, maximum number of weeks, new followers each week, unfollows from each week, and refollows from prior weeks.  The function returns either the phrase “Goal met.” or “Goal not met.”  In the first case the program should also return the week in which the goal was met and how much it was met by.  If the goal isn’t met the program should return the number of followers at the end of the target week and the number of additional weeks needed to achieve the target number.  If the number of followers drops to 0 or if the goal is not achieved within 52 weeks the program should stop and return the phrase “Goal will not be met.”</p>
<ol start="3">
<li>
<p>Extend the function in part 2 so that the function also plots followers vs time.</p>
</li>
<li>
<p>Suppose a mobile app has decided it is instituting a new ad campaign to draw more users. Assume that on a weekly basis the app gains 15% new users relative to the previous week’s total active users while 12% of existing users churn.  Each week 25% of previously inactive users become active again, but at most 500 previously inactive users can be reactivated in any given week.  What is the minimum number of users (rounded to the nearest multiple of 500) that the app must start with in order to hit 20,000 weekly active users in 20 weeks? Try using trial and error, but then try solving it programmatically and to the exact whole number in the general case by writing a function with this signature:</p>
</li>
</ol>
<pre><code>find_init_users(per_new, per_churn, per_reactivate, act_cap, target_num, weeks)   
</code></pre>
<p>The function will either return the minimum starting number of users or return “Not possible under given assumptions.”</p>
<ol start="5">
<li>
<p>Make up your own general discrete random variable that has 6 allowable integer outputs.  Generate plots for the pmf, cdf, and find the mean, median, mode, variance, and standard deviation.</p>
</li>
<li>
<p>Try reproducing the same results in Excel.  You can use two bar charts or side-by-side bar charts for the graphs.</p>
</li>
<li>
<p>Suppose we have a “rigged” coin that gives heads 52% of the time.<br>
a. What is the expected number of heads &amp; tails after 100 coin flips?<br>
b. What is the probability of getting 6 heads in 10 flips?<br>
c. What is the probability that we will have more then 580 heads after 1000 flips?<br>
d.  <strong>Challenge: How “rigged” would the coin have to be to ensure there is at least an 85% chance that after 500 flips we’d have at least 400 heads?</strong><br>
e. Generate a pmf of the case where there are 100 flips and the probability of a head is 70%.</p>
</li>
<li>
<p>Imagine a random 1-d walk with the probability of forward step at .41 and the probability of a backwards step at .59.<br>
a.	What is the probability that a walk of 10 steps will have 7 forward steps?<br>
b. What is the probability that our walk will end further than 3 steps from the start?  Try calculating the empirical probability using 100 different simulations as well as the exact probability using the binomial distribution.<br>
c. <strong>Challenge: What is the expected number of times a walk of 100 steps will return to within 5 steps of the beginning after having gone beyond that distance?</strong></p>
</li>
</ol>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

