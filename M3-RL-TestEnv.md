RL test environments are really important to testing how well your RL training has gone.

Take a look at those and other metrics for RL.

When evaluating models trained with RL, we need to be on the lookout for something
called reward hacking. Basically, it might look good on the eval until you run it in the RL
environment. And reward hacking is often too small a percentage in errors to be actually caught in
your test set eval, but the behavior can actually be pretty detrimental. And the best practice to
help with this is to create RL test environments.

You've seen this RL environment before, but
this time it's frozen. Okay, so the graders are frozen. Other things like tools and files are
frozen. You want to make this environment as deterministic as possible so that it's reliable
and reproducible. If you have external APIs, like a search API, keep these offline as much as
possible so that you can actually be able to reproduce it. And this means you pre-collect
some of that API information ahead of time. If you can grade with verifiers first, that'll help
you the most. That's best in making sure your results are trustworthy and not as reward hackable.

But of course, if you need to use a reward model to grade, then train a new reward model. That means
that reward model is trained on held out preference data that your previous reward model in training
has never seen. Otherwise, the LLM might know how to reward hack the models actually seen in
training already.

You'll also have to use a held out set of inputs that the model hasn't seen before
in the training environment. So these are all inputs that it just has not seen. And just to
understand what we mean by deterministic here, here's an example YAML file that freezes things
to be super deterministic. So first you have your name of your RL test environment. You have a fixed
*random number generator* for reproducibility. You freeze *time* inside of the environment even.
Maybe you're asking for what happened today or tomorrow,
that time is frozen for the model. And there's deterministic decoding like for *temperature*.

The *tools* are also pretty frozen. You're pre-collecting those offline responses,
and you're storing it in that fixture. If there's any kind of internal ranking for these tooling,
you're trying to fix that randomness as well. Your repo, your file system state, these are all
frozen. Your graders, you want them to be programmatic ideally, and everything needs to
align with this snapshot of the RL test environment. So now taking stock of all of our
evals, our different test sets and our RL test environments. So in test sets you see for fine
tuning, you see for reward model, you also see two for reward model. One is actually for that
new reward model if you need it for the RL test environment. You see held out inputs in the RL
test environment. And then you see that final evaluation data. That is also really important,
but basically an unseen mix of pretty diverse and extreme inputs that you could use for
adversarial testing or red teaming, which you'll learn about a little bit later. But essentially
final eval data to just check very, very different possible inputs to jailbreak your model and see
what works and doesn't. Okay, what else can you do during RL? What are things that you can monitor?

* One thing you can monitor is KL divergence to the base model, meaning how far your trained model
  is from the base model and you want to prevent it from drifting too far.

* Another is called the alignment tax, which is the difference between the reward for
  the reward model and human eval and what that gap looks like.

* And then there's sample efficiency as well. Like basically how many rollouts do we need
  to actually get the most gain from the model?
  And of course, rollout diversity. If all of your rollouts look the same, then your model has collapsed.

Let's take a look at every single one of these.

So KL divergence is a way to measure how different two probability distributions are.
And in this case, it's going to be the base model distribution and your new updated model.
And if they're the same distribution, it'll be zero nats. *nat* here is just short for
natural units. And if you compute it with the natural log, the KL divergence with natural log,
this is what you would use. If you compute it with like log base two, the unit is bits,
which you're probably more familiar with. So if it's the same distribution, it would be zero nats.
A safe KL divergence is usually 0.1 to 0.2 nats. And the KL divergence here is actually 1.5 nats
that you'll see. And as you can see, the outputs might look fluent from the new model, but it
prefers the word quantum everywhere. And that is not what you want. So the fix is to add a KL penalty
or reduce the RL learning rate to reduce that drift.

The alignment tax. So that's if there's a gap between what the reward is given by the reward model
and how humans would actually grade it. In this case, it's subtle, but essentially the reward score jumped 0.23 points,
but the human preference barely moved from step 50,000 to step 100,000 in training. What that means is the model
is likely gaming the reward model. So even though the human preference did go up as well, it barely
moved compared to the reward model. So the fix is probably to retrain that reward model on high
reward, but low human score outputs. That way it's able to balance out and get closer to that
human eval.

You can also inspect your rollouts. So if your model is producing the same or similar
output a lot without variance, then there's a collapse in terms of the rollouts it's outputting.
The fix is to encourage this in the reward function with some kind of entropy bonus.
Often you'll want to increase rollouts to make better use of every single input and to also
provide diverse outcomes in the grading, assuming you don't get that collapse. This is especially
true for GRPF. But increasing rollouts doesn't actually mean and always mean better outputs,
and when that's the case, don't just arbitrarily waste compute and scale out rollouts.
Improve your grader then or your reward signals and encourage exploration.
