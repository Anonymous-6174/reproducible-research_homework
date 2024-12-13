# Reproducible research: version control and R

### Questions 1, 2, 3
https://github.com/Anonymous-6174/logistic_growth

### Question 4
**a)** 


**b)**


**c)**


**d)**
The comparison of the change made to the random_walk.R script is shown below

<img width="1373" alt="Screenshot 2024-12-12 at 15 12 32" src="https://github.com/user-attachments/assets/551faecc-edbe-4a90-9331-14f364c1789b" />


### Question 5
**a)** 33 rows and 13 columns 


**b)**
$`V = \alpha L^{\beta}`$ has a non-linear relationship. We can log transform genome volume and genome length to allow us to fit a linear model.
The transformation is applied below

```{r}
colnames(data)

data$logged_volume = log(data$Virion.volume..nm.nm.nm.) 
data$logged_length = log(data$Genome.length..kb.)
logged_data <- data
```

**c)**
The following code determines the exponent $\beta$ and scaling factor $\alpha$
```{r}
linear_model <- lm(logged_volume ~ logged_length, 
                   data = logged_data)

summary(linear_model)
# Intercept = 7.0748, P = 2.28e-10
exp(7.0748)
# = 1181.807
# Slope = 1.5152, P = 6.44e-10
```
So $\alpha$ = 1181.807 with a P value of 2.28 x 10<sup>-10</sup>
And $/beta$ = 1.5152 with a P value of 6.44 x 10<sup>-10</sup>

**d)**
The code to reproduce the figure is found below

```{r}
ggplot(logged_data, aes(x = logged_length, y= logged_volume)) +
  geom_point(size=1.8) +
  geom_smooth(method = "lm", se = T, color = "blue", size = 0.5) +
  labs(x = "log[Genome length (kb)]", y = "log[Virion volume (nm3)]") +
  theme_light() +
  theme(axis.title = element_text(hjust = 0.5, size = 9, face = "bold"))
```
My Graph
![e0f755db-9139-48c9-80dc-b394c577a386](https://github.com/user-attachments/assets/b26c4414-aadf-427a-94e5-1758f96c41ff)

**e)**
$`V = ($\alpha$) L^($\beta$)

$\alpha$ = 118.807

L = 300

$\beta$ = 1.5152

```{r}
1181.807 * (300^1.5152)
```
So volume = 6697006


## Instructions

The homework for this Computer skills practical is divided into 5 questions for a total of 100 points. First, fork this repo and make sure your fork is made **Public** for marking. Answers should be added to the # INSERT ANSWERS HERE # section above in the **README.md** file of your forked repository.

Questions 1, 2 and 3 should be answered in the **README.md** file of the `logistic_growth` repo that you forked during the practical. To answer those questions here, simply include a link to your logistic_growth repo.

**Submission**: Please submit a single **PDF** file with your candidate number (and no other identifying information), and a link to your fork of the `reproducible-research_homework` repo with the completed answers (also make sure that your username has been anonymised). All answers should be on the `main` branch.

## Assignment questions 

1) (**10 points**) Annotate the **README.md** file in your `logistic_growth` repo with more detailed information about the analysis. Add a section on the results and include the estimates for $N_0$, $r$ and $K$ (mention which *.csv file you used).
   
2) (**10 points**) Use your estimates of $N_0$ and $r$ to calculate the population size at $t$ = 4980 min, assuming that the population grows exponentially. How does it compare to the population size predicted under logistic growth? 

3) (**20 points**) Add an R script to your repository that makes a graph comparing the exponential and logistic growth curves (using the same parameter estimates you found). Upload this graph to your repo and include it in the **README.md** file so it can be viewed in the repo homepage.
   
4) (**30 points**) Sometimes we are interested in modelling a process that involves randomness. A good example is Brownian motion. We will explore how to simulate a random process in a way that it is reproducible:

   a) A script for simulating a random_walk is provided in the `question-4-code` folder of this repo. Execute the code to produce the paths of two random walks. What do you observe? (10 points) \
   b) Investigate the term **random seeds**. What is a random seed and how does it work? (5 points) \
   c) Edit the script to make a reproducible simulation of Brownian motion. Commit the file and push it to your forked `reproducible-research_homework` repo. (10 points) \
   d) Go to your commit history and click on the latest commit. Show the edit you made to the code in the comparison view (add this image to the **README.md** of the fork). (5 points) 

5) (**30 points**) In 2014, Cui, Schlub and Holmes published an article in the *Journal of Virology* (doi: https://doi.org/10.1128/jvi.00362-14) showing that the size of viral particles, more specifically their volume, could be predicted from their genome size (length). They found that this relationship can be modelled using an allometric equation of the form **$`V = \alpha L^{\beta}`$**, where $`V`$ is the virion volume in nm<sup>3</sup> and $`L`$ is the genome length in nucleotides.

   a) Import the data for double-stranded DNA (dsDNA) viruses taken from the Supplementary Materials of the original paper into Posit Cloud (the csv file is in the `question-5-data` folder). How many rows and columns does the table have? (3 points)\
   b) What transformation can you use to fit a linear model to the data? Apply the transformation. (3 points) \
   c) Find the exponent ($\beta$) and scaling factor ($\alpha$) of the allometric law for dsDNA viruses and write the p-values from the model you obtained, are they statistically significant? Compare the values you found to those shown in **Table 2** of the paper, did you find the same values? (10 points) \
   d) Write the code to reproduce the figure shown below. (10 points) 

  <p align="center">
     <img src="https://github.com/josegabrielnb/reproducible-research_homework/blob/main/question-5-data/allometric_scaling.png" width="600" height="500">
  </p>

  e) What is the estimated volume of a 300 kb dsDNA virus? (4 points) 
