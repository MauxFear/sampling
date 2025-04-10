# ASSIGNMENT: Sampling and Reproducibility in Python

Read the blog post [Contact tracing can give a biased sample of COVID-19 cases](https://andrewwhitby.com/2020/11/24/contact-tracing-biased/) by Andrew Whitby to understand the context and motivation behind the simulation model we will be examining.

Examine the code in `whitby_covid_tracing.py`. Identify all stages at which sampling is occurring in the model. Describe in words the sampling procedure, referencing the functions used, sample size, sampling frame, any underlying distributions involved, and how these relate to the procedure outlined in the blog post.

Run the Python script file called whitby_covid_tracing.py as is and compare the results to the graphs in the original blog post. Does this code appear to reproduce the graphs from the original blog post?

Modify the number of repetitions in the simulation to 100 (from the original 1000). Run the script multiple times and observe the outputted graphs. Comment on the reproducibility of the results.

Alter the code so that it is reproducible. Describe the changes you made to the code and how they affected the reproducibility of the script file. The output does not need to match Whitby’s original blogpost/graphs, it just needs to produce the same output when run multiple times

# Author: Mauricio Garcia Benitez

```
This a very interesting study on how a bias in the sampling procedure affects the outcome of contact tracing.
The blog and the Pyton code implementation both use two sample approaches:
A primary contact tracing, where a sample of the total infected population is randomly selected; and a
secondary contact tracing, where in the case of 2 or more attendees being detected as infected it goes back
test and trace the entired group of infected people who attended the event.
Additionally, there is the assumption that the infection rate is constant of 10% per event, but the trace
success rate is just 20%, meaning that the probability of successfully tracing an infected person is only 20%.
In the case, of the primary contact tracing, the sample size is randomly chosen using the trace success rate
as threshold. This approach can be be classified as simple random sampling.
The secondary contact tracing uses the entire group of infected people who attended the event as the sample
size. This approach can be classified as systematic sampling, since it uses a systematic approach to define a
threshold of infected people per event and then increase the sampling efforts to get the entire propulation of
infected people who attended the event.

The analysis showed in the blog, suggest that the differences in the attendance sizes between different types
 of events, such as weddings and restaurants events like brunches, has a significant impact on the outcome of the contact tracing process.
A wedding with 100 attendees would have higher chances of detecting more than two infected people leading to
applying the secondary contact tracing method increasing the number of infected people traced in weddings compared to brunches. The probability of having more than one traced infected people during a brunch event with 10 attendees is much lower, therefore, the secondary contact tracing procedure is not applied reducing the number of infected people traced in brunches compared to weddings. 

## Does the code appear to reproduce the graphs from the original blog post? 
No, In this case both distributions (Infected vs Traced) had a proportion around 20%, which is the expected
proportion given the constant infection rate of 10% and a total population of 1000 people where 200 people attended a wedding event. In the distribution of the Python script, we notice a small sub distribution of
cases where the proportion is between 0 and 5 %, while in the blog post the proportion of traced infections
is more spreaded to higher proportions. 

After reducing the number of repetitions to 100, I noticed that the distribution is similar both populations
have a mean around 20%. However, the results are not reproducible since each time I ran the script the results
change. To make the code reproducible, I added a seed value to the numpy.random.seed() function. After adding
the seed value, I ran the script several times and observed that the results were consistent across runs.
I added an additional violin plot to show the distribution along with the mean, and I noticed that by using
a higher number of repetitions the mean gets closer to 20%.
Even when I used 50,000 repetitions the distributions of Infected vs Traced are almost identical, expecting
for the subset of cases where the proportion is between 0 and 5 %. 

I analyzed the implementation from the blog post in R and I compared with the Python script. It was hard but
I noticed that the main difference was around how the events were defined.
In the blog post, the events were defined a set of lists containing the attendees of each event. This results
 in having two weddings events with 100 attendees and multiple brunch events with only 10 attendees.
On the other hand, in the Python script, the events are defined as a simple list of the total number of
attendees per event type, resulting in having only one wedding event with 200 attendees and one brunch event
with 800 attendees. This change resulted in a very different distribution given that the implementation with
multiple events of different sizes simulated better the scenario placed in the blog post.

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
- [ X ] Create a branch called `assignment-1`.
- [ X ] Ensure that the repository is public.
- [ X ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via the help channel in Slack. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
