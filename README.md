# Supply-Chain-Analytics

# Performed the following challenges:
- Data check
- Explore Data
- Analyze and Visualize data
- Dashboarding
- Communicate insights

# Performed DAX calculations:
- Additional Unit Capacity Required
  - Additional Unit Capacity Required = MINX(Internal_Mfg_Resource_Estimates, MAX('Scenario Volume'[Scenario Volume Value] - Internal_Mfg_Resource_Estimates[Existing_Capacity], 0))
 - Capital Investments Required (Make)
  - Capital Investments Required (Make) = MINX(Internal_Mfg_Resource_Estimates, ROUNDUP([Additional Unit Capacity Required] / MIN(Internal_Mfg_Resource_Estimates[Unit_Capacity]), 0) * Internal_Mfg_Resource_Estimates[Machine_Fixed_Cost])
- Make Scenario Full Cost
  - Make Scenario Full Cost = MINX(Internal_Mfg_Resource_Estimates, [Capital Investments Required (Make)] + Internal_Mfg_Resource_Estimates[Cost_per_Unit] * 'Scenario Volume'[Scenario Volume Value])
- Extended Cost
  - Extended Cost = Quotes[Unit_Cost] * Quotes[Volume]
- Full Cost
  - Full Cost = Quotes[Extended Cost] + Quotes[Non_recurring_expenses]
- Yield Rate
  - Yield Rate = FIRSTNONBLANK('Yield Rate'[Yield Rate], TRUE)
- *Scenario Volume
  - Scenario Volume = GENERATESERIES(1000, 100000, 500)
- Buy Scenario Full Cost
  - Buy Scenario Full Cost = MINX(FILTER(Quotes, 'Scenario Volume'[Scenario Volume Value] >= Quotes[Volume]), Quotes[Non_recurring_expenses] + Quotes[Unit_Cost] * 'Scenario Volume'[Scenario Volume Value])
- Cost Avoidance
  - Cost Avoidance = ABS([Make Scenario Full Cost] - [Buy Scenario Full Cost])
- Make versus Buy
  - Make versus Buy = IF(ISBLANK([Make Scenario Full Cost]), BLANK(), IF([Make Scenario Full Cost] >= [Buy Scenario Full Cost], "Buy", "Make"))
- Scenario Full Cost 
  - Scenario Full Cost = MINX(FILTER(Quotes, 'Scenario Volume'[Scenario Volume Value] >= Quotes[Volume]), Quotes[Non_recurring_expenses] + Quotes[Unit_Cost] * 'Scenario Volume'[Scenario Volume Value])
- *Scenario Volume 
  - Scenario Volume = GENERATESERIES(1000, 100000, 500)
- Scenario Volume Value
  - Scenario Volume Value = SELECTEDVALUE('Scenario Volume'[Scenario Volume], 15000)
- *Scenario Volume (All) 
  - Scenario Volume (All) = 'Scenario Volume'
- Scenario Full Cost (All) 
  - Scenario Full Cost (All) = MINX(FILTER(Quotes, Quotes[Volume] <= MIN('Scenario Volume (All)'[Scenario Volume])), MIN('Scenario Volume (All)'[Scenario Volume]) * Quotes[Unit_Cost] + Quotes[Non_recurring_expenses])

# Dashboards:
- Supplier Selection
![j55m2ay1 ugd](https://github.com/MarcvWaes/Supply-Chain-Analytics/assets/120553175/1bff498e-338e-453c-bb3d-ba5507d14b9f)

- Scenario Analysis
![o5rsado1 oi3](https://github.com/MarcvWaes/Supply-Chain-Analytics/assets/120553175/bc76ec34-e79a-4b6d-9c9c-e610306acc55)

- Make versus Buy
![yd3slo10 4qd](https://github.com/MarcvWaes/Supply-Chain-Analytics/assets/120553175/ba98c4f9-ee13-4726-ad00-10793c95f914)
