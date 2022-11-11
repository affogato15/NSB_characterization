The folder contains:
'assoc_PBS_100%.txt' - file with a few experimental measurements of SPR-signal in phase of Adsorption at the same contitions.

'diss_PBS_100%.txt' - file with a few experimental measurements of SPR-signal in phase of Desorption at the same contitions, every curve of dissociation corresponds to the one of Association.

'Discrete approach.ipynb' - Jupyter Notebook file with a script.

The script allows to process experimental data of SPR measurements of Blood Plasma(BP) proteins adsorption and desorption, average it.
Usually, to describe chemical kinetics of single protein adsorption the integrated Langmuir adsortion equation is applied. Initially, it is ODE. In the case of BP, it is impossible to describe it in this way as BP is a complex composition and contains hundreds of different proteins. The idea is to devide all proteins into as less number of groups of proteins as possible to describe the kinetics (rates of binding and unbinding). As it turned out, division into three groups is enough to describe it with resonable quality (deviation when fitting). 
The idea of the approach is devide the experimental curves both association and dissociation, find rates of adsorption and desorption via approximation and optimization and assemble it back together.
MAIN ASSUMPTION is that the affect of slowly binding proteins on signal level is negligible in a time scale of the ones with medium rate of binding.
The same for relation between fast and meduim dinding proteins independently on phase, whether it is adsorption or desorption.

Three parameters we would like to determine are coefficients of association (k_a) and dissociation (k_d) rates and concentration (C). As we can't split product of k_a'C so far, we get it as it is and call k_c.
Since k_d play role in both Association and Dissociation, we have to approximate corresponding curves conjugately. That has been done. As a result, we obtain list of parameters: k_c1,k_c2, k_c3, k_d1, k_d2, k_d3. Pairs of them represent rates of binding and unbiding of the group of proteins. Namely, k_c1 with k_d1 together reflect the group of the fastest binding and unbinding proteins, while k_c3 with k_d3 reflect the slowest group.

Bounderies and initial conditions for parameter optimization were picked manually to obtain the lowest value of the loss function. Among all accesible methods of defining of the function minimum, 'Nelder-Mead' method showed the best results.
