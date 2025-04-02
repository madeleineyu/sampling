# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Madeleine Yu

```
In the model, sampling occurs at the primary contact tracing and the secondary contact tracing that aim to find the proportion of infections and traced cases that are attribuated to weddings. 

The model 'infects' a random subset of 1000 people with an infection rate ('ATTACK_RATE') of 10%, creating a target population with a sample size of 100 infected individuals that contact tracing is attempting to identify. Thus the sampling frame is the 1000 people who attended either one of 2 weddings (100 per wedding) or one of 80 brunches (10 people per brunch). Sampling of the population first occurs at the primary contact tracing, to decide which infected individuals get traced; however, an infection only has a 20% chance of being traced to a source event ('TRACE_SUCCESS'). Both populations infected from weddings and brunches would follow a normal distribution, with those infected from weddings centered on 20%, and those infected from brunches centered on 80%. The next sampling occurs at the secondary contact tracing, to decide the number of infections based on event attendance (if two infections are independently traced to the same event; SECONDARY_TRACE_THRESHOLD). Thus the proportion of perceived infected individuals traced to weddings would be the result of the sum of the individuals who are infected (10%) and successfully traced to a wedding (20%) and individuals who are traced as having attended the same wedding as an infected and traced individual. Thus this proportion of perceived infected individuals traced to weddings would likely be an overestimation of the true population, with a right-skewed distribution, while the proportion of perceived infected individuals traced to brunches would likely be an underestimation of the true population, with a left-skewed distribution.

The results of whitby_covid_tracing.py appears to be a better representation of the true proportion of infected individuals from weddings, likely because the simulation was run 1000 times. 

When the number of repetitions of the simulation is modified to 100, and the script is run multiple times, the output differs each time I run the script. Thus, the results are not reproducible. Therefore, to address this, and to make sure that the output is reproducible, I used the function np.random.seed() to set the seed prior to the creation of the dataset and assignment of infections to ensure that the same random people are infected are infected and traced. 
```


## Criteria

|Criteria|Complete|Incomplete|
|--------|----|----|
|Altercation of the code|The code changes made, made it reproducible.|The code is still not reproducible.|
|Description of changes|The author explained the reasonings for the changes made well.|The author did not explain the reasonings for the changes made well.|

## Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `23:59 - 09/04/2025`
* The branch name for your repo should be: `assignment-1`
* What to submit for this assignment:
    * This markdown file (a1_sampling_and_reproducibility.md) should be populated.
    * The `whitby_covid_tracing.py` should be changed.
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sampling/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `assignment-1`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
