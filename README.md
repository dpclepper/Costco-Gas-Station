# Costco Gas Station Simulation Modeling & Analysis

# 1. Executive Summary
This report details an analysis of the queuing system of a busy Costco gas station located in Madison, WI. This gas station is frequently busy, thus, customers are faced with long lines and wait times. This leads to some undesirable queue behavior such as balking (when a customer leaves the system due to a long wait time). Therefore, it is important to understand this system and how to maximize the number of customers that Costco can serve while still using the least amount of pumps required. 

By recording various statistics such as the arrival time, pump start time, and departure time for each vehicle, I created a computer model that represents Costco's current gas station system. Once the computer model was verified and validated, I conducted an analysis to better understand the performance of the gas station based on Key Performance Indicators (KPIs). This analysis helped highlight key issues that may be inhibiting gas station’s performance. To address these issues, I explored how different changes could improve the gas station. Since making these changes to the physical gas station would be time-consuming and costly, I made alternative computer models that represented the changes. 

In total, three alternative computer models were analyzed and compared to the current gas station model. The first alternative involved restructuring the layout and number of pumps per lane. The second alternative explored introducing a new CostcoPlus membership lane that was managed by a pump attendant. The third alternative looked at converting one lane into a FastTrack lane for customers who planned to spend less than three and a half minutes at the pump. 

Ultimately, the new CostcoPlus membership program was found to lead to the greatest system improvement. This improvement was found to be statistically significant. With that said, I advise caution in pursuing this alternative and recommend further analysis be conducted to determine if the costs of implementing this alternative are covered by the improved customer experience. It is also suggested that FastTrack lane be further studied as a potential alternative due to its simplicity and ease of implementation. While the statistical comparison was inconclusive on this alternative, it did show a preliminary average reduction of 28.8% in customer wait time. Regardless of the alternative Costco pursues or analyzes further, the base model built for the Costco gas station accurately represents the current system and I believe it will be very useful for exploring these alternatives, and potentially other alternatives further. 

# 2. Introduction
For this project, I analyzed the behavior of cars pumping gas at the Costco gas station on the west side of Madison, WI.  The gas station consists of 12 total pumps where 6 queues feed into each set of two pumps. I tracked the behavior for queues 1 and 2, see figure 1. Vehicles generally entered the lanes based on fuel door locations even if there was a long line (i.e. many Subarus entered lane 1 because their fuel door is on the passenger side of the vehicle).

| ![CostcoFigure1.png](Images/CostcoFigure1.png?raw=true) | 
|:--:| 
| ***Figure 1:** Queues of Interest* |

My main objectives and goals for the project were 
1) to build an Arena model that accurately represents the Costco gas station system
2) to propose and compare potential system improvements, and 
3) to provide a final recommendation on the best feasible alternative system. 

Ultimately, this report investigated three alternative models and found that alternative 2 can reduce total customer waiting by 47.7% on average. This reduction was found to be statistically significant. Alternative 3 showed an average reduction of 28.8% in total customer waiting time, but was not statistically significant. Alternative 1 showed no improvement and in fact decreased system performance. Even though alternative 2 showed a greater reduction, this report advises caution in implementing it due to its high overhead costs like hiring personnel to manage the lane. Alternative 3 is more feasible to implement but would require further analysis to determine if it would improve the system with statistical significance. Overall, this report provides these models as tools to further analyze and understand Costco’s gas station system and explore future improvements.

The remainder of this report is organized as follows: Section 3 details my assumptions and conceptual models. Section 4 covers data collection methods and theoretical distributions for interarrival and service time from input analysis. Section 5 contains an output analysis. Section 6 compares potential system improvements. Section 7 makes a final recommendation for the best feasible alternative and contains my concluding remarks. 

# 3. Assumptions and Conceptual Model
## 3.1. Key Simulation Details & Structural Assumptions
My first step in creating the conceptual model was identifying key simulation details like the entities, attributes, events, activities, and variables. The arriving vehicles and their drivers are considered temporary entities, while the 4 gas pumps are considered permanent entities. The first-in-first-out (FIFO) queuing discipline is the main attribute identified in the system. Key events include vehicle arrivals, pump starts, and vehicle departures. Activities include interarrival times and service times. The distributions for these activities are detailed in Section 4. Finally, some of the variables present in the system include fuel tank size, desired level of refueling, and driver familiarity/speed of using the pump. 

## 3.2. Model Drawing
The next step I performed in creating the conceptual model was to hand-sketch the system on a satellite view of the Costco gas station (see figure 2). As shown in the drawing, vehicles all come into the system from the same location. The vehicles then decide on which lane they would like to queue in.  The vehicle waits in its chosen lane, or queue until one of the two pumps becomes free. Once a pump is free, the vehicle drives up to the pump and begins fueling. After fueling is complete, the vehicle departs the system.

| ![CostcoFigure2.png](Images/CostcoFigure2.png?raw=true) | 
|:--:| 
| ***Figure 2:** Satellite drawing of Costco Gas Station System* |

## 3.3. Building the Arena Model 
I translated the hand-sketched model into an Arena model (See Figure 3). First, a create module was placed in the work window. A “2-way by Chance” decide module with an assumed “Percent True” of 50% was connected to the create module.  A  process module was added for the lane 1 pumps and another was added for the lane 2 pumps. Since each lane has two servers or pumps, the resource capacity for each process module was changed to “2.” Finally, a dispose module was added to complete the Arena model. No warm-up period was used for this model.

| ![CostcoFigure3.png](Images/CostcoFigure3.png?raw=true) | 
|:--:| 
| ***Figure 3:** Arena Model of Costco Gas Station System* |

## 3.4. Model Verification & Data Assumptions
On 4/20/2022, I met with Vanessa Sawkmie to receive a preliminary check of the Arena model. She verified my assumption that each lane should have one process module with a resource capacity set equal to 2. She also verified that a 50% true 2-way by chance decide module would be appropriate for this model based on the data collected. Since jockeying and reneging occurred with very low probability, I was given permission to ignore them in the model. 

After the model was verified with Vanessa, I used Arena’s process analyzer to ensure the model responded correctly to varying interarrival rates and service time speeds. To do the analysis, the interarrival and service time distributions were set to constant values and multiplied by a “rate” and “speed” variable respectively. The rate and speed variables were then varied for four different scenarios to see how the model would respond. See figure 4 for a summary of the process analyzer responses. 

| ![CostcoFigure4.png](Images/CostcoFigure4.png?raw=true) | 
|:--:| 
| ***Figure 4:** Summary table of Arena's Process Analyzer* |

Intuitively, the numbers make sense. For example, a comparison of scenario 1 vs. scenario 2 shows a decrease in the total system output, lane 1 & 2 queue times, and lane 1 & 2 utilizations. This makes sense because the rate variable changes from 1 to 2 which effectively increases the time between vehicle arrivals by a factor of 2. Similar logic holds when comparing the other pairs of scenarios. Please note that these numbers do not reflect the actual system! They were arbitrarily chosen to verify the model responded as projected. 

The last step of verification entailed tracing 16 customers through a manual simulation and comparing the results to an Arena Model with 16 customers. The manual simulation was done in accordance with the simulation example given in Module 3 Lecture 2 from class. I set up a spreadsheet with columns “interarrival time”, “Lane #”, “Arrival Time”, “Wait Time”, etc. A screenshot of the manual simulation spreadsheet is available in Appendix A, figure A2.  Arbitrary interarrival times and services times were chosen to be 20 sec and 100 sec respectively. I assumed that the 2-way decide module could be simulated manually by having customers alternate which lane they entered (i.e. customer 1 went to lane 1, customer 2 went to lane 2, customer 3 went to lane 1, customer 4 went to lane 4, and so on…). 

After running the manual simulation and Arena simulation, I compared output values and found that they all matched (see Figure 5).

| ![CostcoFigure5.png](Images/CostcoFigure5.png?raw=true) | 
|:--:| 
| ***Figure 5:** Manual vs. Arena Simulation Results* |

A few minor modifications were made to the Arena model in order to have an accurate comparison. First, a “terminating condition” was added that specified the simulation should stop after 16 customers went through the system. Second, in the create module, the maximum arrivals were also set to 16 customers. Finally, to ensure that the decide module alternated every customer, it was temporarily changed to “2-way by condition” with the condition set to:  NQ(Lane 1.Queue) <= NQ(Lane 2.Queue).

# 4. Data Collection and Input Modeling
## 4.1. Data Collection
I deviated from the original project proposal and assigned two team members to collect data on 4/2/2022 and the other two members to collect data on 4/9/2022. On both days, the students arrived at Costco around 1 pm and collected about an hour's worth of data. The arrival time, pump start time, and departure time for each vehicle for each lane were recorded on separate spreadsheets. The pump start time was defined as the time that the car arrived at the pump such that no other vehicle could occupy the pump at the same time. Arrival and departures were when the vehicle arrived and departed from the system respectively. See figure 6 for a sample of the data collected in lane 1 on 4/2/2022. Screenshots for the full datasets can be found in Appendix A, figures A3 and A4. 

| ![CostcoFigure6.png](Images/CostcoFigure6.png?raw=true) | 
|:--:| 
| ***Figure 6:** Sample of Data Collected from Lane 1 on 4/2/2022* |

## 4.2. Data Processing
The data was processed to determine interarrival times and service times. First, the arrival, pump start, and departure times were all combined into one spreadsheet. These times were sorted by date and then time. To determine interarrival times, the difference between each consecutive arrival time was calculated and converted into seconds.  To determine service times, the difference between departure time and the pump start time was calculated and converted into seconds. These times were saved in separate text files. 

## 4.3. Input Analysis
The distributions for interarrival and service time were found using Arena’s input analyzer. The text file for the interarrival times was opened in the input analyzer. The “fit all” tool was used to determine the best fit distribution for interarrival time (in seconds):

-0.001 + 180*BETA(0.943, 2.22)

The same process was followed for the service times text file, and the resulting best fit distribution was:

NORM(211, 65.44)

See Appendix A, figures A5 and A6 for outputted images of the respective distibutions.

## 4.4. Model Validation
I started to validate the model by establishing face validity. The main approximations made were related to (1) the decide module and (2) the interarrival and service time distributions. The 50% average true value for the decide module mentioned in section 3.4 was supported by the “true” percentage approximated from the real data. An average of 49.6% of vehicles went to lane 1, while an average of 50.4% went to lane 2. The interarrival and service time approximations were detailed in section 4.3. Figure 7 displays some of the main summary values from the collected data and from the Arena simulation. The absolute difference between these values is given in the right column. The percent differences are minimal, suggesting that the approximations and assumptions used were reasonable. 

| ![CostcoFigure7.png](Images/CostcoFigure7.png?raw=true) | 
|:--:| 
| ***Figure 7:** Average Summary Values from Real Data vs. Arena Simulation* |

To further validate the model, I conducted hypothesis tests on the average service time, wait time, and interarrival time. To conduct these tests, t-test statistics were used with a significance level (α) of 0.05. In all three cases, I failed to reject the null hypothesis, suggesting that the values found by the simulation may likely be reasonable. The calculations for these tests are available in Appendix B and are labeled B1, B2, and B3.

# 5. Output Analysis
## 5.1. Replication-Deletion Method for Non-Terminating Steady-State Analysis
Next, the replication-deletion method was used to analyze how the system behaves and to understand the error in the simulation’s output. First, I chose to run the analysis for 20 replications because this would allow the simulation results to average out.   During data collection, one or two time periods were observed where the system had very few customers in it. Within three to seven minutes, the system would become quite full and operate in a steady state. I selected the upper end of that range, 7 minutes, as Arena’s warm-up period for the output analysis.  The upper end was chosen because it would help ensure the system was operating at a steady-state. The simulation was then run and the corresponding simulation report was automatically generated. From this report, I selected a set of Key Performance Indicators (KPIs) to calculate confidence intervals. The confidence intervals were found from the KPI averages and their half-widths. The KPIs and their 95% confidence intervals are organized in Figure 8. 

| ![CostcoFigure8.png](Images/CostcoFigure8.png?raw=true) | 
|:--:| 
| ***Figure 8:** Average Summary Values from Real Data vs. Arena Simulation*\
*Arena reports confidence intervals with built-in confidence level of 95%. |

To help interpret the results in figure 8, I also created Figure 9 which compares the KPI confidence intervals from Arena to the real data values found during data collection. 

| ![CostcoFigure9.png](Images/CostcoFigure9.png?raw=true) | 
|:--:| 
| ***Figure 9:** Average Summary Values from Real Data vs. Arena Simulation*\
*Arena reports confidence intervals with built-in confidence level of 95%. |

The real data values for interarrival time, wait time, service time, and total time in the system fit within the confidence interval generated by the simulation (highlighted green). The lane 1 server utilization and lane 2 server utilizations do not fit within the confidence interval (highlighted red). I observed system behavior that suggests this is due to the fact that the cars are occasionally unable to immediately fill an empty server due to physical restrictions or driver ability; however, in the Arena model, this behavior is not represented due to the way the process modules function. As a result, the server utilization in the real system is about 3.5% to 6.5% less than the lower bound of the confidence intervals from the simulation. 

## 5.2. Sensitivity Analysis 
To begin the sensitivity analysis, I used Arena’s process analyzer to conduct a sensitivity analysis for 4 different scenarios. The procedure for this analysis is very similar to the procedure covered in the verification Section 3.4; however, this sensitivity analysis used interarrival and service time distributions found from the input analysis rather than constant values.  The interarrival and service time distributions were multiplied by a “rate” and “speed” respectively. The rate and speed variables were then varied for four different scenarios to see how the model would respond. See figure 10 for a summary of the sensitivity analysis. 

| ![CostcoFigure10.png](Images/CostcoFigure10.png?raw=true) | 
|:--:| 
| ***Figure 10:** Summary table of Arena's Process Analyzer* |

As with the sensitivity analysis for the model verification, the rate and speed changes yielded sensible results. An increase in rate by a factor of 2 (scenarios 1 vs. 2) yielded near a 50% decrease in system output and server utilizations as well as a significant decrease in average queue times. This effect makes sense, as the rate increase causes an increase in the time between vehicle arrivals. Similar logic holds when comparing the other pairs of scenarios. 

# 6. Comparison of Alternative Models
To address bottlenecks and inefficiencies in the current Costco gas station system, I developed three alternative models. Alternative 1 tests a hypothesis that splitting the pumps into their own lanes will reduce overall customer queue time. It was also observed that service times could often be high simply due to vehicle drivers’ slow and inefficient use of the pump. Alternatives models 2 and 3 try to address this bottleneck.

## 6.1. Four Lanes with One Gas Pump Each Model (Alternative 1)
This alternative model features a gas station with four lanes with one gas pump per lane. I hypothesized that this may be an improvement because the total queue time may be improved by having four separate queues. To implement this in Arena, four process modules were used rather than the base model’s two process modules. The resource capacity for each process module, or lane, was changed from one to two. To split the customers into four lanes, an additional two 50% true 2-way decide modules were added. A screenshot of the model structure is available in figure A9 of Appendix A. 

## 6.2. New CostcoPlus Member Model (Alternative 2)
This alternative model features a full-service lane for CostcoPlus members and a regular self-service lane for regular Costco members. The full-service lane has two pumps that are operated by a single pump attendant. An assumption was made that this attendant would reduce the service time by about 30% since they would be more familiar with the pump and be readily available as soon as the vehicle pulls up to the pump. The 30% reduction was implemented by multiplying the service time distribution in the full-service lane by 0.70:

NORM(211, 65.44) * .70

For this model, I assumed that 55% of Costco customers would buy this premium membership, and the *decide* module was updated accordingly. A screenshot of the model structure is available in Figure A10 of Appendix A. 

## 6.3. FastTrack Model (Alternative 3)
This alternative model features a “FastTrack” lane for customers who plan to take less than 210 seconds (or 3.5 minutes) at the pump. Lane 1 became the FastTrack lane and lane 2 stayed as a normal lane. A new service time distribution was calculated for the FastTrack lane based on service times from the real data that were less than 210 seconds. The resulting best fit distribution (in seconds) was found:

53 + 156 * BETA(1.61, 0.77)

A visualization for this distribution can be found in figure A12 of Appendix A. A further assumption was made that the distribution in the normal lane would stay the same as the base model. This assumption was based on the fact that some customers might be hesitant to join the FastTrack lane, but still end up finishing in under 210 seconds. I also analyzed the real data to find that 45.3 % of customers had a service time of fewer than 210 seconds. The 2-way by chance decide module was changed from the base model’s 50% true value to a 45.3% true value. The 45.3% true output fed into the FastTrack lane while the false output fed into the normal lane. A screenshot of the model structure is available in Figure A11 of Appendix A. 

## 6.4. Comparison of Alternatives Models and Base Model
To compare these models, I analyzed KPIs between the base and alternative models to find that alternatives 2 and 3 improved the Costco gas station while alternative 1 deteriorated the system. To compare these models, Arena’s process analysis was once again used, but this time, each scenario represented a different Arena model. Since each model had a different structure, I had to make the decision to focus on the comparison of overall system KPIs like total customer waiting time, total customer output, and customer WIP.  The values for each of these KPIs are summarized in Figure 11. 

| ![CostcoFigure11.png](Images/CostcoFigure11.png?raw=true) | 
|:--:| 
| ***Figure 11:** Base vs. Alternative Model KPIs* |

A comparison between the base model and alternative 1 shows a clear deterioration of the system. Total wait time, output, and WIP were negatively impacted, suggesting my hypothesis about the four separate queues in alternative 1 was incorrect. A comparison between the base model and Alternative 2 shows an improvement in all three KPIs; however, it is important to note that the cost of the CostcoPlus membership would need to be high enough to cover the cost of having a dedicated attendant. A comparison between the base model and alternative 3 shows an improvement in the total customer waiting time and WIP. Alternative 3 had negligible effects (0.8%) on the total customer output. 

## 6.5. Statistical Comparison of Base Model vs Alternatives 2 and 3
To further compare Alternatives 2 and 3 to the base model, I conducted a statistical comparison on the average total queue times. For each model, the average waiting time for every replication 1, …, 20 was determined from the simulation report. With these averages listed, the sample standard deviation was calculated in Excel. Furthermore, the confidence interval formula for independent sampling and unequal variance provided on slide 12 was also used. The confidence intervals were found to be:

Base Model vs Alternative 2: [39.26, 175.00]

Base Model vs Alternative 3: [-23.08, 125.42]

Since the confidence interval for Base Model vs. Alternative 3 contains zero, there is no strong statistical evidence that alternative 3 is better than the base model; however, since the confidence interval for the base model vs Alternative 2 is well above zero, it is highly likely that *μ_base - μ_Alternative2 > 0*. This suggests that the average total waiting time in Alternative 2 is less than that of the base model with statistical significance.

# 7. Recommendations and Conclusions 
Based on the analysis in Sections 6.4 and 6.5, Alternative 2 is the best option to reduce the average customer waiting time for Costco members. Implementing this option would require quite a bit of work on the backend. First, Costco would need to find a way to implement a new membership service. This may require ordering a new card for CostcoPlus members and working with the IT department to set up the extra perks for these members. Also, dedicated personnel would need to be hired to attend the CostcoPlus member lane.

The analysis in Section 6.4 also suggests that Alternative 3 may be a good option, but I was unable to justify this in the statistical comparison in Section 6.5. While Alternative 3 doesn’t increase customer output as Alternative 2 does, it may moderately decrease the average customer wait time and WIP. Alternative 3 is also easier to implement than Alternative 2. Costco could simply buy a FastTrack sign and enforce the time limit through programming changes to the pump. The Costco employee who is typically managing all the pumps could also help enforce the policy by asking customers to move their vehicles after their time is up. Unfortunately, there was no strong statistical evidence that this alternative would improve customer wait time.

Ultimately, Alternative 2 is the only option that I can recommend at this time since it shows a statistical improvement; however, additional analysis is recommended to determine if the costs associated with implementing the new membership program in Alternative 2 would be worth the improved customer experience. Additional statistical analysis is recommended for alternative 3 to determine if, in fact, it will lead to a significant improvement. If Alternative 3 is found in the future to lead to an improvement, it may be a more feasible option for Costco to implement. While this recommendation is somewhat inconclusive, I believe the model I built will prove to be quite useful in any further analysis that is needed. Overall, the models that I created were able to accurately simulate a real-life Costco gas station. I learned a lot about the entire process of conducting a simulation, starting with defining the problem, then collecting data and analyzing it to create an ultimate recommendation. I hope that the Costco team is able to take my recommendations and improve their queuing system.
























