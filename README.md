Multi-Objective Optimization Methods for Spatial Sampling
This repository contains the MATLAB code from my PhD thesis at Tarbiat Modares University. The work sits at the intersection of spatial statistics and multi-objective optimization, and it tackles a question that comes up constantly in environmental monitoring and field surveys: given limited resources, where should you place your measurement stations to get the most reliable predictions?
The answer is rarely obvious. More stations do not always mean better predictions, and placing them without a principled method leaves a lot on the table. This thesis develops tools to find genuinely optimal designs.
The HAN Algorithm
The central contribution is the HAN algorithm (Hybrid AMOSA-NSGA-II), which I built by combining two well-established metaheuristics. AMOSA is good at exploiting local search around promising solutions; NSGA-II is good at exploring the objective space broadly. On their own, each has blind spots. HAN runs them together, using NSGA-II's crossover and mutation operators directly on AMOSA's archive at every iteration, so the strengths of both carry through to the final Pareto frontier.
I compared HAN against four algorithms: NSGA-II, AMOSA, MOPSO, and MOGWO, across multiple scenarios and objective function combinations. HAN ranked first in all of them based on the AHP-TOPSIS evaluation.
Applications
Soil Sampling
The first application is soil sampling design. Knowing where to sample a field matters a lot for understanding soil nutrient distribution and making good agricultural decisions. The problem is framed as a bi-objective optimization: minimize the variance of the sample mean (or the mean total prediction error), while also minimizing the total distance the sampler has to travel between locations. These two objectives conflict, and the Pareto frontier HAN produces gives a clear picture of the tradeoffs a practitioner faces.
Rain Gauge Network, Khuzestan Province
The second application is a real monitoring network. Khuzestan Province in southwestern Iran covers around 64,000 km² and has 137 rain gauge stations managed by the Ministry of Energy. Those stations were installed incrementally over time with no systematic spatial design, which means some areas are over-covered and others are not covered well enough.
I used HAN to find optimized networks and compared them against the current setup. The results were clear: networks with fewer stations consistently outperformed the existing one on prediction accuracy.
Network	Stations	RMTE
Current (Ministry of Energy)	137	110.27
Optimized	105	102.18
Optimized	118	101.20
Optimized	124	100.57
Optimized	137	99.01
Papers
Lotfian, E., Mohammadzadeh, M. (2023). Multi-objective optimization of spatial sampling using a new hybrid AMOSA_NSGA-II algorithm. Computational and Applied Mathematics, 42, 24. https://doi.org/10.1007/s40314-022-02161-1
Lotfian, E., Mohammadzadeh, M. Assessing the efficiency of rain gauge station network in Khuzestan, Iran: an optimal design perspective. (Under review)
Requirements
MATLAB R2022a, Spatial Statistics Toolbox, Applied Statistics Toolbox, Optimization Toolbox.
Contact
e.lotfian@gmail.com
