Now that you're excited about evals, it's time to actually invest in it.

It's important to actually get the size right, expand your evals right, and to make them representative, reliable, and actionable.

So you're excited about investing in evals. Maybe your first instinct is to create a very large
eval data set of math, physics, history, politics, every possible topic under the sun,
and spend a lot of money on crowdsource labelers with human labelers.
Do not do this. This is not how you should invest in your evals.

In fact, your evals should start small. It should start with maybe 20 examples of
finance or some topic your users care most about, and it should have, you know,
metrics around factual accuracy. Maybe you have a metric around brevity.
And for annotation, all you need is one in-house expert for consistency.

So very simple, very slim. And in your first week, within your first week here,
you can actually see some issues with the model already because you will have finished your evals,
and you will see that the model hallucinates on numbers, maybe like
invent stock prices, or its summaries exceed that 100-word constraint.
And you can actually have an actionable insight to then improve the model.

So within your first week, you can already have a huge difference
in the model if you start your evals small. And that's exactly right.

Once the model improved on the small targeted eval, you can start to expand coverage
to other frontiers that might need to learn. Maybe it's science and politics, right?
And you can do that with more confidence.

And you can expand it, obviously, based on the failures you get to get a better
understanding of the failure, as well as, again, those new skills and domains.
And eventually, you'll get to that larger and larger data set.

This expansion tends to be exponential, not linear. So you might start with that
20, and then go to 200, 2,000, 20,000 examples. So you might want a 10x at every single time,
because you're trying to cover a much larger frontier.

And as you can see, you don't always want your evals to be 100% correct all of the time,
because then you're not actually testing the frontier.
One of the best practices is to keep it at around 80% max.
Okay, so now you know how to start small and then scale out the size of your eval.

What are other good qualities of evals? So one is that it needs to be representative
of how your users are actually using the model. So in this case, the user asks a non-math question,
and the model doesn't know what to do. Okay, it responds with four.
Your evals, however, have no question around anything unrelated to math.
It only has math questions. That's a problem. So instead, maybe in your evals,
you're starting to evaluate the model and make sure it has guardrails, like,
sorry, I only answer with math problems. You add these refusals to the evals,
and then you add it in training a model, and then now your model can handle it.

So just to go more into representative, suppose your users ask 20% math questions,
but 80% are conversational, but your evals are not representative of that distribution.
It puts a larger weight on conversational questions than math questions.
So maybe you see your model improving overall based on eval accuracy,
but actually your users are suffering. They're asking, why is it so bad at math?
And that's because it wasn't representative of users actually using your model.

The next important quality is making your evals actionable.
If the whole point of error analysis in evals is to fix the model,
then evals need to actually be actionable. This means errors will point to data
interventions themselves. So your eval should be enabling you to that next frontier.

Here it's division, right? So you're adding division examples through evals so that then
you can create a new dataset for division. So you see a failure pattern on division,
and you think, okay, I need more division data. So in your evals, you add these
division examples, you see those failures, and then that prompts you to create that new data.

And this, again, is why you want your evals to be at max 80% correct all the time.
So here's how you can also take action. So let's say you're looking at your model,
it's a math model, and you're taking a look at how it does for every single type of operation,
addition, multiplication, division, and mixed expressions. When you observe errors,
you see that it doesn't have any errors on addition, so you don't need any actual intervention.

For multiplication, it's doing quite well. Maybe you add a few examples of high magnitude
multiplication because it occasionally makes mistakes on large numbers.
For division, it does pretty poorly. So then you want to collect pretty targeted division problems
across different examples, integers, decimals, edge cases, and same with mixed expressions.
You probably want to add a lot more there as well as examples, and maybe even add division
reasoning examples to reinforcement learning.

Finally, a really important quality of your evals is making it reliable.
This is so you can actually trust deltas from one experiment to the next.
Remember how many experiments you're running for error analysis? You want to be able to trust that
one experiment is actually better than the other. You want to trust that model B here is better than
model A at division. Can you convince me? So if you look at the top level numbers,
model A is 90% correct on everything. Model B is lower at 82%. But when looking at division,
model A is at 0% and model B is at 100%. However, if you dig deeper and you look overall,
and then you look at the division subset, you see there are only five items in the division subset.
So maybe model B is dramatically better at division, but it's only five items. How can I be
sure? Then you expand your division subset in your evals and actually get a more reliable number.
And with this larger sample, the signal is more stable. And you can say, yes, actually model B is
reliably stronger at division. So reliability isn't just about sample size. It's about stability
of your conclusions. And there are also statistical significance tests that you can run across multiple
experiments or model runs at different random seeds to make sure the improvement isn't just
noise. And this is also why broad coverage is also encouraged. So you know your model is reliable
across a lot of different dimensions and axes. So now that you've invested in your evals and
made them super high quality, it's time to break your model with red teaming.
