# Costco Gas Station Simulation Modeling & Analysis

# 1. Executive Summary
This report details an analysis of the queuing system of a busy Costco gas station located in Madison, WI. This gas station is frequently busy, thus, customers are faced with long lines and wait times. This leads to some undesirable queue behavior such as balking (when a customer leaves the system due to a long wait time). Therefore, it is important to understand this system and how to maximize the number of customers that Costco can serve while still using the least amount of pumps required. 

By recording various statistics such as the arrival time, pump start time, and departure time for each vehicle, I created a computer model that represents Costco's current gas station system. Once the computer model was verified and validated, I conducted an analysis to better understand the performance of the gas station based on Key Performance Indicators (KPIs). This analysis helped highlight key issues that may be inhibiting gas station’s performance. To address these issues, I explored how different changes could improve the gas station. Since making these changes to the physical gas station would be time-consuming and costly, I made alternative computer models that represented the changes. 

In total, three alternative computer models were analyzed and compared to the current gas station model. The first alternative involved restructuring the layout and number of pumps per lane. The second alternative explored introducing a new CostcoPlus membership lane that was managed by a pump attendant. The third alternative looked at converting one lane into a FastTrack lane for customers who planned to spend less than three and a half minutes at the pump. 

Ultimately, the new CostcoPlus membership program was found to lead to the greatest system improvement. This improvement was found to be statistically significant. With that said, I advise caution in pursuing this alternative and recommend further analysis be conducted to determine if the costs of implementing this alternative are covered by the improved customer experience. It is also suggested that FastTrack lane be further studied as a potential alternative due to its simplicity and ease of implementation. While the statistical comparison was inconclusive on this alternative, it did show a preliminary average reduction of 28.8% in customer wait time. Regardless of the alternative Costco pursues or analyzes further, the base model built for the Costco gas station accurately represents the current system and I believe it will be very useful for exploring these alternatives, and potentially other alternatives further. 

# 2. Introduction
For this project, I analyzed the behavior of cars pumping gas at the Costco gas station on the west side of Madison, WI.  The gas station consists of 12 total pumps where 6 queues feed into each set of two pumps. I tracked the behavior for queues 1 and 2, see figure 1. Vehicles generally entered the lanes based on fuel door locations even if there was a long line (i.e. many Subarus entered lane 1 because their fuel door is on the passenger side of the vehicle).

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

## 3.3. Building the Arena Model 
I translated the hand-sketched model into an Arena model (See Figure 3). First, a create module was placed in the work window. A “2-way by Chance” decide module with an assumed “Percent True” of 50% was connected to the create module.  A  process module was added for the lane 1 pumps and another was added for the lane 2 pumps. Since each lane has two servers or pumps, the resource capacity for each process module was changed to “2.” Finally, a dispose module was added to complete the Arena model. No warm-up period was used.


























