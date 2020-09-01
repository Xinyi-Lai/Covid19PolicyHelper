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

#### Part I: SEIR model
    We first build a dynamic model for the viral transmission. We correct

    and by controlling the transmission parameters, we can model the future trend of the pandemic under different circumstances. 

#### Part II: backward optimization

#### Part III: environmental factors modeling


### Challenges we ran into

### Accomplishments that we're proud of

### What we learned

### What's next for Covid-19 Policy Decision Helper
