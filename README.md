# Covid19PolicyHelper

Link to submission

https://devpost.com/submit-to/10147-aws-data-exchange-challenge/start/submissions/172323-covid-19-policy-decision-helper/edit


## What's your project called?
Covid-19 Policy Decision Helper


## Here's the elevator pitch
> What's your idea? This will be a short tagline for the project

Predictive modeling of Covid-19 transmission that helps policy makers make best decisions to controll mortality with the least costs.


## It's built with
> What languages, APIs, hardware, hosts, libraries, UI Kits or frameworks are you using?

......

## Created by
Yulin Li, Xinyi Lai

---

## Here's the whole story
> Be sure to write what inspired you, what you learned, how you built, and challenges you faced.

### Inspiration

As the COVID-19 pandemic spreads out all over the world, we see different strategies adopted by different countries and states, and (maybe therefore), we see different characteristics and trends in the transmission of virus in different regions. There are lots of concerns about the future of the pandemic, and there are lots of debates about the policy making in many countries and regions.

We think that it will be interesting to model the dynamics of the viral transmission and to visualize the future trend of COVID-19. Then by setting a tolerate threshold for the future motality rate, we can find the best combination of parameters using optimization methods. Furthermore, we can model the relationship between the transmission parameters and the environmental factors such as the control policy, hospital beds, mobility, population, and so on. Once it is modeled, the effects of them on the transmission process can be explained quantitively, and the optimal set of parameters obtained above will correspond to a set of control policy with the least cost, that is, the most relaxed policy acceptable.


### What it does

1. **Viral transmission model.**
    We built a dynamic model for the viral transmission using differential equations. The state-level timeseries data is used in the fitting of the model. After choosing a state of interest and a time period, the transmission parameters will be optimized and outputted, and a predicted curve will show the trend of the pandemic assuming all conditions stay the same in future.  
2. **Finding the best set of parameters.**
    With a tolerate threshold of mortality rate / infected rate in a given future period set, our algorithm can find the best set of parameters using the optimization methods. That is, the most relaxed conditions while keeping the mortality rate / infected rate under control for a given time period. In real policy making,  dynamic optimization can be of great help since it can continuously correct the model and give the optimal parameters based on the real-time data.
3. **Recommend the best policy decisions.**
    We modeled the relationship between the transmission parameters and the environmental factors. Given the optimal parameters obtianed above, we can determine the corresponding optimal policy and the value of environmental factors.



### How we built it


#### Part 0: Data

The dataset we used is the Global Coronavirus (COVID-19) Data (Corona Data Scraper) provided by Enigma. 

[AWS product link](https://aws.amazon.com/marketplace/pp/prodview-vtnf3vvvheqzw?qid=1597409751562&sr=0-1&ref_=brs_res_product_title#overview)
[Corona Data Scraper page](https://coronadatascraper.com/#home)

After preprocessing, we fetched the state-level timeseries data of cases, deaths, recovered, hospitalized, data and population.


#### Part 1: SEIR infection model

We built a viral transmission model based on the classical SEIR model with some modifications. 
![title](model.png)

We Assume...

* Susceptible (S): healthy people, will be infected and turn into E after close contact with E or Q.
* Exposed (E): infected but have no symptoms yet, infectious with a rate of $\lambda$. E will turn into I after the virus incubation period, which is 14 days on average. So we assume $\sigma = 1/14$, dE/dt (t) = dI/dt (t+14).
* Infectious (I): infected and have symptoms. We will take the data of test_positive or cases_reported as the data of I. The severe cases will be hospitalized (H), the mild cases will be in self quarantine (Q). I may recover or die after some time.
    * Self Quarantine (Q): have symptoms, may still have some contact with others, thus infectious with a different rate of $c\lambda$ ($0 \le c \le 1$). We also assume $Q = kI$, where $k = 1 - avg(\frac{\Delta hospitalized}{\Delta test\_pos}) $
    * Hospitalized (H): have symptoms, kept in hospitals, assume no contact with S. 
* Recovered (R): recovered and immune, may turn into S again (immunity lost or virus not cleared)
* Dead (X): dead unfortunately :(


Therefore, we have a set of differential equations to describe this process:

$\begin{aligned}
&\frac{dS}{dt}&
&=& - \lambda \frac{S}{N} E - c\lambda \frac{S}{N} Q + \alpha R ~~~
&=& - \lambda \frac{S}{N} E - c\lambda \frac{S}{N} kI + \alpha R
\\
&\frac{dE}{dt}&
&=&   \lambda \frac{S}{N} E + c\lambda \frac{S}{N} Q - \sigma E ~~~
&=&   \lambda \frac{S}{N} E + c\lambda \frac{S}{N} kI - \sigma E
\\
&\frac{dI}{dt}&
&=& \sigma E - \mu I - \omega I 
\\
&\frac{dX}{dt}&
&=& \omega I 
\\
&\frac{dR}{dt}&
&=& \mu I - \alpha R 
\end{aligned}$

$S + E + I + R + X = N,~ I = Q + H$


Apply to our datasets, we have:

$ R = recovered,~ X = deaths,~ I = test\_pos - deaths - recovered,\\
E(t) = I(t+14) - I(t),~ S = N - E - I - R - X,\\
k = 1 - avg(\frac{\Delta hospitalized}{\Delta test\_pos})
$



    and by controlling the transmission parameters, we can model the future trend of the pandemic under different circumstances. 

#### Part II: backward optimization





#### Part III: environmental factors modeling






### Challenges we ran into

### Accomplishments that we're proud of

### What we learned

### What's next for Covid-19 Policy Decision Helper
