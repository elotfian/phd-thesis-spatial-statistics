# Multi-Objective Optimization Methods for Spatial Sampling
This repository contains the MATLAB code from my PhD thesis at Tarbiat Modares University. The work sits at the intersection of spatial statistics and multi-objective optimization, and it tackles a question that comes up constantly in environmental monitoring and field surveys: given limited resources, where should you place your measurement stations to get the most reliable predictions?
The answer is rarely obvious. More stations do not always mean better predictions, and placing them without a principled method leaves a lot on the table. This thesis develops tools to find genuinely optimal designs.
## The HAN Algorithm
The central contribution is the HAN algorithm (Hybrid AMOSA-NSGA-II), which I built by combining two well-established metaheuristics. AMOSA is good at exploiting local search around promising solutions; NSGA-II is good at exploring the objective space broadly. On their own, each has blind spots. HAN runs them together, using NSGA-II's crossover and mutation operators directly on AMOSA's archive at every iteration, so the strengths of both carry through to the final Pareto frontier.
I compared HAN against four algorithms: NSGA-II, AMOSA, MOPSO, and MOGWO, across multiple scenarios and objective function combinations. HAN ranked first in all of them based on the AHP-TOPSIS evaluation.
## Applications
### Soil Sampling
The first application is soil sampling design. Knowing where to sample a field matters a lot for understanding soil nutrient distribution and making good agricultural decisions. Soil properties are spatially correlated; nearby locations tend to carry similar information, so blindly increasing the number of samples does not always improve predictions. The problem is framed as a bi-objective optimization: minimize the variance of the sample mean (or the mean total prediction error), while also minimizing the total distance the sampler has to travel between locations. These two objectives conflict, and the Pareto frontier HAN produces gives a clear picture of the tradeoffs a practitioner faces.
### Rain Gauge Network, Khuzestan Province
Accurate rainfall monitoring is essential for water resource management, flood forecasting, and climate adaptation. But building a reliable monitoring network is not just about having enough stations; it is about placing them in the right locations. Khuzestan Province in southwestern Iran covers 64,000 km² of mixed terrain and has 137 rain gauge stations managed by the Ministry of Energy. These stations were placed gradually over the years, without fully accounting for the spatial correlation of rainfall across the region. Any proposed network also has to satisfy WMO international standards, which set strict minimum spacing requirements depending on terrain type: at least one station per 250 km² in mountainous areas and one per 900 km² in plains. That turns out to matter a lot. Rainfall is spatially correlated, meaning the information a station contributes depends heavily on where it sits relative to others. 

We formulated the problem as a bi-objective optimization: minimize the Root Mean Total Error in rainfall predictions, which combines kriging variance and spatial model parameter uncertainty, and minimize the number of stations to cut costs. Under WMO spacing constraints, HAN found networks that do more with less. A 105-station network placed at optimal locations already outperforms the current 137-station setup, and an optimally placed 137-station network reduces prediction error by over 10%.

| Network | Stations | RMTE |
|---------|----------|------|
| Current (Ministry of Energy) | 137 | 110.27 |
| Optimized | 105 | 102.18 |
| Optimized | 118 | 101.20 |
| Optimized | 124 | 100.57 |
| Optimized | 137 | 99.01 |
## Papers
- Lotfian, E., Mohammadzadeh, M. (2023). Multi-objective optimization of spatial sampling using a new hybrid AMOSA\_NSGA-II algorithm. Computational and Applied Mathematics, 42, 24. https://doi.org/10.1007/s40314-022-02161-1

- Lotfian, E., Mohammadzadeh, M. Assessing the efficiency of rain gauge station network in Khuzestan, Iran: an optimal design perspective. (Under review)
## Requirements
MATLAB R2022a or later, Spatial Statistics Toolbox, Applied Statistics Toolbox, Optimization Toolbox.
## Contact
e.lotfian@gmail.com
