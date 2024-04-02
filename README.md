# Metropolis and Metropolis-Hastings Algorithm for Markov Chain Monte Carlo method of sampling


<img width="915" alt="Screenshot 2024-04-02 at 10 15 18 AM" src="https://github.com/vizziviz/mcmc_example/assets/64040862/674a7bf3-394d-4ca2-8410-3faead83d263">

My simple example is 13 rows of data about a coin flip. My question: is my coin fair? 

In statistical terms, I am looking for p, the probability of getting heads, a parameter of the Binomial Distribution.

The steps of MCMC are:
1. I select a starting proposal, proposal_0.
2. The posterior probability of my current proposal, proposal_t, is calculated from Bayes' formula which is prior*likelihood / evidence. From the problem formulation, I know that I am calculating my likelihood using the pmf formula for the Binomial distribution. Assuming I have no idea what my probability distribution of p(heads), I can choose a Beta(1,1) distribution as my prior, which is a uniform distribution bounded between 0 and 1. In fact, we don't need to know the evidence (the denominator) portion of Bayes' formula because we will be using a ratio of posterior_new_proposal/posterior_previous_proposal which means the denominators will cancel out. Thus, the posterior at each step is $$Prior * Likelihood$$
3. I decide whether to accept or reject the new proposal. If posterior_new > posterior_previous, I always accept. But if posterior_new < posterior_previous, I may accept *some* proposals, but creating a uniform random variable U~Unif(0,1) and accepting the worse-perforrming new proposal if the U<posterior_ratio. This helps me to get a collection of samples as a result, rather than converging on one solution. 

## Metropolis Algorithm
<img width="761" alt="Screenshot 2024-04-02 at 10 27 31 AM" src="https://github.com/vizziviz/mcmc_example/assets/64040862/8b5e469b-1747-441e-8047-0e88352604e4">

I chose 0.9 as my starting probability, randomly. You can see a little bit of burn-in before the samples start to converge to the paramater space here:

<img width="756" alt="Screenshot 2024-04-02 at 10 28 26 AM" src="https://github.com/vizziviz/mcmc_example/assets/64040862/a57780db-ae8d-4cbc-a562-8f8f740df06b">

My distribution of Probabilities for Heads looks like the following:

<img width="738" alt="Screenshot 2024-04-02 at 10 29 21 AM" src="https://github.com/vizziviz/mcmc_example/assets/64040862/af24a983-8242-4677-bbd9-bcbdd314f1a5">

## Metropolis Hastings Algorithm
In this Algorithm, I change my proposal selection and my proposal acceptance a little bit to introduce a rightward or leftward bias. One reason to do this might be to not get caught in local extrema, another might be that I want to result in a skewed probability distribution, or in my case, I think my data may have undersampled Heads and I want to see what my probability distribution of P(heads) looks like if this is truly the case.

<img width="1278" alt="Screenshot 2024-04-02 at 10 33 01 AM" src="https://github.com/vizziviz/mcmc_example/assets/64040862/4f9e5435-8987-4d93-ba7a-c63671d4342a">

<img width="918" alt="Screenshot 2024-04-02 at 10 33 35 AM" src="https://github.com/vizziviz/mcmc_example/assets/64040862/4820aab6-6be1-4c6a-9954-e837ba4e488f">

My initial probability proposal_0 was too low (0.1), so you can see burn-in in the opposite direction from the last algorithm.

<img width="728" alt="Screenshot 2024-04-02 at 10 33 48 AM" src="https://github.com/vizziviz/mcmc_example/assets/64040862/51c4e95d-7e76-4fa4-9f37-ee302d656acb">

And here is the histogram of my distribution of p(Heads). We can see that it looks Normal and centered around 0.425.

<img width="750" alt="Screenshot 2024-04-02 at 10 34 51 AM" src="https://github.com/vizziviz/mcmc_example/assets/64040862/cb60a74b-ce40-4704-87ab-eca7d6d1cd72">



