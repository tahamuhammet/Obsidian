
Propensity score matching (PSM) is a statistical technique used in observational studies to reduce the effects of confounding variables in the estimation of treatment effects.

Purpose: PSM is used to control for the differences between treatment and control groups that may be related to the outcome of interest, but are not of interest themselves. This helps to isolate the effect of the treatment of interest and provides a more accurate estimate of its impact.

Assumptions: PSM assumes that the treatment and control groups are comparable on all observable and unobservable characteristics that are related to the outcome of interest. This assumption is often referred to as the "strong ignorability" assumption.

Limitations: PSM can be limited by the quality of the data used to estimate the propensity scores. If the data used to estimate the propensity scores are biased or incomplete, the results of the PSM may be unreliable. Additionally, PSM relies on the strong ignorability assumption, which is not always met in practice.

Pros: PSM can provide a more accurate estimate of treatment effects compared to other methods, as it controls for many confounding variables. It is also relatively simple to implement and interpret.

Cons: PSM can be sensitive to the choice of matching method and the quality of the data used to estimate the propensity scores. If the data used to estimate the propensity scores are biased or incomplete, the results of the PSM may be unreliable.

Example: To demonstrate PSM, consider a study of the effect of a new drug on the risk of heart attacks. Researchers might use PSM to control for differences in age, sex, and other risk factors between individuals who receive the drug and those who do not. By matching individuals with similar propensity scores, the researchers can isolate the effect of the drug on the risk of heart attacks and avoid the confounding effects of other variables.

In the MECE framework, the information provided on PSM can be organized as follows:

-   Pros: Provides a more accurate estimate of treatment effects, simple to implement and interpret.
-   Cons: Sensitive to the choice of matching method and quality of data, strong ignorability assumption may not be met in practice.
-   Limitations: Quality of data used to estimate propensity scores, relies on strong ignorability assumption.
-   Purpose: To control for confounding variables in the estimation of treatment effects.
-   Assumptions: Strong ignorability assumption that treatment and control groups are comparable on all variables related to the outcome.

The mathematical formulation of propensity score is defined as the probability that an individual will receive the treatment, given their observed covariates (x). It is typically estimated using logistic regression and can be represented mathematically as:

$$ \hat{e}(T=1|x) = \frac{1}{1 + e^{-\beta^{T}x}} $$

where $\hat{e}(T=1|x)$ is the estimated propensity score, $\beta$ is a vector of regression coefficients, and $x$ is a vector of observed covariates.

The matching process can then be performed by selecting control units with similar estimated propensity scores for each treated unit. This can be done using a variety of methods, including nearest neighbor matching, caliper matching, and others. The estimated treatment effect can then be calculated using the matched data.

```
* Generate a binary treatment variable
gen treatment = 0
replace treatment = 1 if x1 + x2 > 4

* Estimate the propensity score
logit treatment x1 x2
predict pscore, p

* Match treatment and control units using propensity score
p smatch2 treatment, propensity(pscore) nearest nn(1) balance

* Run regression analysis on the matched sample
reg y treatment x1 x2, vce(robust)
```

Consider a hypothetical study that aims to estimate the effect of a new education program (treatment) on student test scores (outcome). We have data on 100 students, half of whom received the new education program, and half of whom did not. The data include the following variables:

-   `Treatment`: a binary variable indicating whether the student received the new education program (1) or not (0)
-   `X1`, `X2`, and `X3`: three covariates that may influence both the treatment assignment and the outcome
-   `Y`: the student's test score

We can use propensity score matching to estimate the effect of the education program on test scores by matching students who received the treatment with those who did not, based on their covariate profiles.

The first step is to estimate the propensity score, which is the probability of receiving the treatment given the values of the covariates. This can be done using logistic regression:

logit Treatment X1 X2 X3

where `Treatment` is the binary treatment variable and `X1`, `X2`, and `X3` are the covariates. The logistic regression model estimates the coefficients `b1`, `b2`, and `b3`, which represent the relationship between each covariate and the treatment assignment. The estimated propensity score for each student is then calculated as follows:


$$p = \frac{{e}^{\left(b0 + b1 \cdot X1 + b2 \cdot X2 + b3 \cdot X3\right)}}{1 + {e}^{\left(b0 + b1 \cdot X1 + b2 \cdot X2 + b3 \cdot X3\right)}}$$

where `e` is the mathematical constant for natural logarithms (approximately equal to 2.71828), and `b0` is the constant term.

Next, we use the estimated propensity scores to match students who received the treatment with those who did not, based on their similarity in covariate profiles. There are several methods for matching, including nearest-neighbor matching, full matching, and optimal matching. In this example, we will use nearest-neighbor matching with a caliper of 0.25:

```
p smatch2 Treatment, propensity(p) nearest nn(1) caliper(0.25)
```


This command matches each student who received the treatment with the closest student who did not receive the treatment, based on their estimated propensity scores. The caliper of 0.25 means that only students whose estimated propensity scores are within 0.25 of each other are considered a match.

Finally, we can estimate the effect of the education program on test scores by comparing the mean test scores of students who received the treatment with those who did not, using a t-test

`t-test Y if Treatment == 1, by(Treatment)`


This command calculates the mean test score for students who received the treatment (`Treatment` == 1), and the mean test score for students who did not receive the treatment (`Treatment` == 0), and tests the hypothesis that the means are equal using a two-sample t-test. The `by(Treatment)` option indicates that the t-test should be performed separately for each group.

The t-test provides a point estimate of the mean difference in test scores between students who received the treatment and those who did not, along with a standard error and a p-value. The point estimate represents the average effect of the education program on test scores, while the standard error and p-value provide



Propensity score matching is a method of estimating the effect of a treatment or intervention on an outcome by matching individuals with similar characteristics. It is based on the assumption that individuals with similar characteristics are more likely to have similar outcomes, regardless of whether they receive the treatment or not. The propensity score is a measure of the likelihood that an individual will receive the treatment, and it is used to match individuals with similar characteristics. This helps to reduce bias in the estimation of the treatment effect.

> [!note]
> -   Propensity scoring is a technique used in observational studies to balance the comparison between treatment and control groups.
> -   The purpose of propensity scoring is to estimate the effect of receiving treatment based on baseline characteristics and reduce the impact of confounding factors.
> -   An example of its use is comparing patient length of stay in two hospitals to determine the quality of care.
> -   The estimated propensity score is the conditional probability of being assigned to a treatment based on covariance.
> -   The model used to determine the estimated propensity score is based on probability and ranges from zero to one.
> -   The treatment type (t) is assigned a value of 1 for outcome under treatment or exposure and 0 for outcome without treatment or exposure.
> -   The covariance (X1, X2, X3, etc.) refers to the background characteristics affecting treatment.
> -   Common applications of propensity scoring include propensity score matching, propensity score weighting, and stratification.




| Step | Description |
|------|-------------|
| 1 | Estimation of the propensity score |
| 2 | Matching |
| 3 | Comparison of outcomes |

## Propensity Score Matching

Propensity Score Matching (PSM) is a statistical technique used to estimate the causal effect of a treatment in observational studies. The method is used to balance the distribution of covariates between the treated and control groups, so that any differences in outcomes can be attributed to the treatment and not to baseline differences between the groups.

## Step 1: Estimation of the propensity score
The first step in PSM is to estimate the probability of receiving the treatment, given a set of covariates. This is done using logistic regression, where the treatment status is the dependent variable and the covariates are the independent variables.

## Step 2: Matching
Once the propensity scores have been estimated, the next step is to match each treated individual with a control individual who has a similar propensity score. This can be done using a variety of methods, including nearest neighbor matching, caliper matching, and radius matching.

## Step 3: Comparison of outcomes
After the matching has been done, the outcomes of the treated and control groups can be compared. This can be done using a variety of techniques, including regression analysis or difference-in-differences estimation. The goal is to determine if there is a statistically significant difference in outcomes between the treated and control groups, which can be attributed to the treatment.```


Let Y_i be the outcome for individual i, T_i be the treatment status (0 = control, 1 = treated), and X_i be a vector of covariates for individual i. The goal of PSM is to estimate the average treatment effect, denoted as ATE:

```math
||{"id":1521092049969}||
ATE = E[Y_i | T_i = 1] - E[Y_i | T_i = 0]

```
where E[Y_i | T_i = 1] is the expected outcome for individuals who receive the treatment, and E[Y_i | T_i = 0] is the expected outcome for individuals who do not receive the treatment.

The first step in PSM is to estimate the propensity score, denoted as e(X_i):
```math
||{"id":218618531115}||
e(X_i) = Pr(T_i = 1 | X_i)
```
The propensity score is the probability of receiving the treatment, given the covariates. This can be estimated using logistic regression:

$$
T_i = \beta_0 + \beta_1 X_{i1} + \beta_2 X_{i2} + ... + \beta_k X_{ik} + \epsilon_i
$$
where $$\beta_0, \beta_1, \beta_2, ..., \beta_k$$ are the regression coefficients and $$`\epsilon_i`$$ is the error term.

Next, each treated individual is matched with a control individual who has a similar propensity score. This can be done using a variety of methods, such as nearest neighbor matching or caliper matching.

Finally, the outcomes of the treated and control groups can be compared. This can be done using regression analysis or difference-in-differences estimation. The goal is to determine if there is a statistically significant difference in outcomes between the treated and control groups, which can be attributed to the treatment.


| <mark style="background: #ADCCFFA6;">Assumptions</mark> | <mark style="background: #BBFABBA6;">Pros</mark> | <mark style="background: #BBFABBA6;">Cons</mark> |
|-------------|------|------|
| The treatment assignment process is independent of the covariates. | 1. Balances covariates between the treated and control groups, reducing the risk of omitted variable bias. <br> 2. Can be used with observational data, avoiding the ethical and practical challenges of randomized controlled trials. <br> 3. Can handle a large number of covariates. | 1. May lead to biased estimates if the propensity score is not well-calibrated or if there is unmeasured confounding. <br> 2. May be computationally intensive for large datasets. <br> 3. The choice of matching method can impact the results. |



> [!quote] Critics
> -   Introduction:
>     
>     -   The International Methods Colloquium is a periodic online seminar discussion of the application of quantitative statistical methods to the social sciences.
>     -   This week's speaker is Gary Kane from Harvard University, and his talk is entitled "Why Propensity Scores Should Not Be Used for Matching."
> -   Overview of Propensity Score Matching (PSM):
>     
>     -   PSM is the most commonly used matching method in social sciences research.
>     -   PSM is used to reduce model dependence, which is the variation in causal effects across different regression models.
>     -   The goal of matching is to find randomized experiments hidden in observational data.
> -   Benefits of Matching:
>     
>     -   Matching reduces imbalance by deleting some observations.
>     -   Matching reduces model dependence by eliminating researcher discretion.
>     -   Matching eliminates bias by finding randomized experiments in observational data.
> -   Problems with Propensity Score Matching (PSM):
>     
>     -   PSM is blind to the truth and finds the worst matches first.
>     -   PSM increases balance but is not a solution for simultaneity or endogeneity problems.
> -   Conclusion:
>     
>     -   Propensity score matching should not be used for matching because it is blind to the truth and finds the worst matches first.
>     -   If a researcher believes that there is a simultaneity or endogeneity problem, they should consider using other strategies.
> - https://www.youtube.com/watch?v=rBv39pK1iEs
