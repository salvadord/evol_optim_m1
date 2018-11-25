# Evolutionary optimization of M1 model

## 
We evaluated the feasibility of using evolutionary algorithms on a biophysically detailed model: a network of mouse M1 microcircuits with over 2.5k multicompartment neurons with conductance-based ionic channels, 7k point neurons for long-range inputs, and over 5M synapses. 

Ten parameters at different scales were optimized within biologically constrained ranges: firing rates of populations providing long-range inputs, weight scaling factors of local microcircuit connections, and maximum conductance of HCN channels in corticospinal cells. 

The fitness function quantified the similarity between experimental and model firing rates for the 15 network populations (see v53_batch24_batch.json and batchScript.py). 

Each simulation (fitness evaluation) was parallelized on 128 cores and all 60 evaluation were executed in parallel, resulting in approx. 20 minutes per generation. 

After 120 generations the best fitness had increased by a factor of four, which lead to a model with all population rates within a biologically reasonable range – in contrast to initial solutions where several populations were silent or hyperexcited. This optimization required approx. 40 hours on 7.7k cores (=308k core hours) of
Google Cloud supercomputers.

* Evolution of fitness error


* Example of poor solution from initial generation:
Generation 1  Candidate 24 fitness error = 401.8

Population 	| Rate (Hz) 	| Fitness error 
----------------------------------------------
CT6 		| 0.6	 		| 7 
PV2 		| 0.0 			| 1000 
PV6 		| 0.0 			| 1000 
SOM5A 		| 14.8 			| 1 
IT5A 		| 0.7 			| 6 
IT5B 		| 3.5 			| 4 
PT5B 		| 3.6 			| 4 
PV5A 		| 0.0 			| 1000 
PV5B 		| 0.0 			| 1000 
IT6 		| 8.5 			| 1 
IT4 		| 0.2 			| 1000 
SOM2 		| 13.7 			| 1 
IT2 		| 0.3 			| 1000 
SOM5B 		| 7.9 			| 2 
SOM6 		| 10.0 			| 2


* Best solution  
Generation 76  Candidate 16 fitness = 17.0
CT6 rate=4.0 fit=3; PV2 rate=7.1 fit=2; PV6 rate=0.4 fit=4; SOM5A rate=22.4 fit=2; IT5A rate=26.8 fit=29; IT5B rate=5.5 fit=2; PT5B rate=36.4 fit=194; PV5A rate=22.0 fit=2; PV5B rate=24.3 fit=3; IT6 rate=16.5 fit=4; IT4 rate=7.9 fit=2; SOM2 rate=26.6 fit=3; IT2 rate=8.6 fit=1; SOM5B rate=8.0 fit=2; SOM6 rate=19.0 fit=1

## Description of files

*