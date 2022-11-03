# NSB_characterization
The folder contains:\
'assoc_PBS_100%.txt' - file with a few experimental measurements of SPR-signal in phase of Adsorption at the same contitions.

'diss_PBS_100%.txt' - file with a few experimental measurements of SPR-signal in phase of Desorption at the same contitions,
                      every curve of dissociation corresponds to the one of Association.
										
'Blood_plasma_proteins_adsorption_100%_concentration.ipynb' - Jupyter Notebook file with a script.

The script allows to process experimental data of SPR measurements of Blood Plasma(BP) proteins adsorption and desorption,
average it. Usually, to describe chemical kinetics of single protein adsorption the integrated Langmuir adsortion equation is applied. Initially, it is ODE. 
In the case of BP, it is impossible to describe it in this way as BP is a complex composition and contains hundreds of different proteins.
The idea is to devide all proteins into as less number of groups of proteins as possible to describe the kinetics (rates of binding and unbinding). 
As it turned out, division into three groups is enough to describe it with resonable quality (deviation when fitting).
As the square of the sensor is not infinite and one protein competes with another for the site, competitive binding model has been applied. 
**In result we have the system of 3 ODE, which describes the signal change with a time, which in turn represents adsorption and desorption of proteins on the sensor surface depending on phase.**\
As the partial solution of 3-PDE system for competitive binding is very combersome, we solve it in the script numerically with SciPy library. 
Three parameters we would like to determine are coefficients of association (k_a) and dissociation (k_d) rates and concentration (C).
As we can't split product of k_a'C so far, we get it as it is and call k_c.\
Since k_d play role in both Association and Dissociation, we have to approximate corresponding curves conjugately. That has been done.
As a result, we obtain list of parameters: k_c1,k_c2, k_c3, k_d1, k_d2, k_d3. Pairs of them represent rates of binding and unbiding of the group of proteins.
Namely, k_c1 with k_d1 together reflect the group of the fastest binding and unbinding proteins, while k_c3 with k_d3 reflect the slowest group.

Bounderies and initial conditions for parameter optimization were picked manually to obtain the lowest value of the loss function. Among all accesible methods of defining of the function minimum, 'Nelder-Mead' method showed the best results.
