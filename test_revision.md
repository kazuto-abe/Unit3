<img width="790" alt="Screen Shot 2021-02-28 at 11 04 59" src="https://user-images.githubusercontent.com/60457723/109412204-05b52d80-79ea-11eb-92e5-e10d10a67cb1.png">
<img width="745" alt="Screen Shot 2021-02-28 at 11 06 19" src="https://user-images.githubusercontent.com/60457723/109412208-0cdc3b80-79ea-11eb-872c-7be05a29e9ea.png">

**(a) State the number of inputs for the NEURON[2]**

2

**(b) State the strength and direction of all the input connections to NEURON[2]**

Inpuit connections that Neuron[2] (id3) has are: - 0.4, and 0.3.
Since they work together (heading to the same direction), this indicates postive strength.

A function called check_inputs() returns True  if the total number of inputs for all the neurons is equal to the size of the array SOURCE and the array STRENGTH, otherwise it returns False. This helps test the integrity of the program.
 
**(c) Create the algorithm for the function check_inputs()**



Another function get_index(id)returns the index of the array NEURON where the neuron with the id provided is stored. Assume that neuron ids are random integer numbers. 

**(d) Create a flow diagram for this function.**

**(e) The function simulate() shown above, calculates the outputs of the neurons based on the arrays defined previously.  State one line in the code where a precondition is used.**

out = 0.0

**(f) Trace the program simulate() with the arrays given above and show the output of NEURON[3].**


### Test result 

