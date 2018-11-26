# Evolutionary optimization of M1 model

## Description
We evaluated the feasibility of using evolutionary algorithms on a biophysically detailed model: a network of mouse M1 microcircuits with over 2.5k multicompartment neurons with conductance-based ionic channels, 7k point neurons for long-range inputs, and over 5M synapses. 

Ten parameters at different scales were optimized within biologically constrained ranges: firing rates of populations providing long-range inputs, weight scaling factors of local microcircuit connections, and maximum conductance of HCN channels in corticospinal cells. 

The fitness function quantified the similarity between experimental and model firing rates for the 15 network populations (see v53_batch24_batch.json and batchScript.py). 

Each simulation (fitness evaluation) was parallelized on 128 cores and all 60 evaluation were executed in parallel, resulting in approx. 20 minutes per generation. 

After 120 generations the best fitness had increased by a factor of four, which lead to a model with all population rates within a biologically reasonable range – in contrast to initial solutions where several populations were silent or hyperexcited. This optimization required approx. 40 hours on 7.7k cores (=308k core hours) of
Google Cloud supercomputers.

## Evolutionary optimization results

* Fitness error

![fitness_evol](https://github.com/salvadord/evol_optim_m1/blob/master/fitness_evol.png)


* Example of poor model solution from initial generation:

Generation 1  Candidate 24, fitness error = 401.8


| Population 	| Rate (Hz) 	| Fitness error |
| ----------|---------------|------------------ |
| CT6 		| 0.6	 		| 7					| 
| PV2 		| 0.0 			| 1000				|
| PV6 		| 0.0 			| 1000 				|
| SOM5A 	| 14.8 			| 1 				|
| IT5A 		| 0.7 			| 6 				|
| IT5B 		| 3.5 			| 4 				|
| PT5B 		| 3.6 			| 4 				|
| PV5A 		| 0.0 			| 1000 				|
| PV5B 		| 0.0 			| 1000 				|
| IT6 		| 8.5 			| 1 				|
| IT4 		| 0.2 			| 1000 				|
| SOM2 		| 13.7 			| 1 				|
| IT2 		| 0.3 			| 1000 				|
| SOM5B 	| 7.9 			| 2 				|
| SOM6 		| 10.0 			| 2					|


* Best model solution:

Generation 76  Candidate 16, fitness error = 17.0

| Population 	| Rate (Hz) 	| Fitness error |
| ----------|---------------|------------------ |
| CT6 | 4.0 | 3
| PV2 | 7.1 | 2 |
| PV6 | 0.4 | 4 |
| SOM5A | 22.4 | 2 |
| IT5A | 26.8 | 29 |
| IT5B | 5.5 | 2 |
| PT5B | 36.4 | 194 |
| PV5A | 22.0 | 2 |
| PV5B | 24.3 | 3 |
| IT6 | 16.5 | 4 |
| IT4 | 7.9 | 2 |
| SOM2 | 26.6 | 3 |
| IT2 | 8.6 | 1 |
| SOM5B | 8.0 | 2 |
| SOM6 | 19.0 | 1 |

## Description of files

* v53_batch24_netParams.py - High-level network parameters (M1 network model specifications)

* v53_batch24_batch.json - Batch simulation configuration (evolutionary algorithm parameters, fitness function, etc.)

* v53_batch24_stats.cvs	- Evolutionary optimization fitness error results across generations

* v53_batch24_stats_indiv.cvs - Evolutionary optimization individuals (solutions) fitness and parameter values

* fitness_evol.png - Fitness error evolution graph 

* gen_76_cand_16_cfg.json - Best solution simulation configuration parameters (simConfig object)

* gen_76_cand_16.json - Best solution output data

* gen_76_cand_16.run - Best solution simulation output log



