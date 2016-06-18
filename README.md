# Supply-Chain-Metric
STATISTICAL CALCUATIONS to predict future inventory
 
To predict future inventory levels, a forecast must be calculated to anticipate weekly sales demand volume. Once forecasted demand has been calculated, these values can be used to predict the quantity need to fulfill a given percent of business demand. 
Order Up-To Model Definitions
Backorder = the total amount of demand that has not been satisfied within a given timeframe.  All backorders are eventually filled, i.e no lost sales. Backorders are calculated as:  
BO = (Quantity ordered / Quantity shipped)  
Inventory level = On-hand inventory - BO   
Inventory position = On-order inventory + Inventory level.   
On-order inventory = the number of units that have been ordered, but have not been received.   
On-hand inventory = number of units physically in stock   
Order up-to level (S) = maximum inventory position or target inventory level or base stock levels; i.e. do not exceed this number   Service Level (SL) = percent of fulfilled client purchase orders during one time period. The following formula is used to calculate SL:
SL = 1-(B /D)   
D = Customer demand per unit of time (e.g. one week)   
µ = Expected weekly demand for multiple units of time (e.g. four weeks)   
StDev = Standard deviation of weekly sales demand
σ = Expected standard deviation of demand over future time interval
Φ = Inverse cumulative density function of the Standard Normal Distribution 
Ti = the given time period
Z = Corresponding Z-score along a Standard Normal Distribution 
EOQ and Order up-to Calculations 
Calculation of the order up-to number is as follows: 
1.	Calculate the forecasted weekly demand and standard deviations of the historic weekly demand. The forecasted demand calculation is bases on of an average of the previous 9 weeks sales. 

    
Next, calculate expected weekly demand and standard deviation over the future time period (e.g. a four week time period would be: Ti *4 = 4 weeks). 

 µ = D ∙ Ti


2.	Establish an order up-to target for on-hand inventory levels; for this project, I set the benchmark at fulfilling 98.5% of customer demand (this corresponds to being in-stock for any given item 95% of the time). 

 
3.	To find the order up-to quantity, to fulfill 98.5% customer demand, we can use the formula:
 S= µ + Z ∙ σ
 Let assume that we found µ and σ above to be µ = 130 pieces and σ = 32.89 SD over Ti weeks respectively. To solve this equation we must find the value of Z, which corresponds to the Inverse Cumulative Density of the Standard Normal Distribution (Φ) with a mean and standard deviation equal to N(0,1). 
Therefore when we look up Φ in a Standard Normal Table for 98.5% we find it to be equal to: 
Φ (0.985) = 2.171= Z 
We can solve this equations in Excel using the function =NORMSINV (0.985) 
or we can also solve in R using the function: qnorm(0.985) #definition for qnorm(probability, mean = 0, sd = 1, lower.tail = TRUE, log.p = FALSE)
Now that we know Z, we can solve for S:
S = µ + Z ∙ σ
S = 130 + (2.171 ∙ 32.89) = 201.4 pieces
We can also use a shortcut calculation in Excel using the formula:
=NORMINV (probability, mean, standard deviation)
{e.g. =NORMINV (0.985, 130, 32.89) ~Note the absence of the S in NORMINV (…) compared to NORMSINV.}
Or in R:
qnorm(0.985, mean =130 , sd=32.89) #qnorm(probability, mean = 0, sd = 1, lower.tail = TRUE, log.p = FALSE)
