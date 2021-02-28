<img width="790" alt="Screen Shot 2021-02-28 at 11 04 59" src="https://user-images.githubusercontent.com/60457723/109412204-05b52d80-79ea-11eb-92e5-e10d10a67cb1.png">
<img width="745" alt="Screen Shot 2021-02-28 at 11 06 19" src="https://user-images.githubusercontent.com/60457723/109412208-0cdc3b80-79ea-11eb-872c-7be05a29e9ea.png">

**(a) State the number of inputs for the NEURON[2]**

2

**(b) State the strength and direction of all the input connections to NEURON[2]**

Inpuit connections that Neuron[2] (id3) has are: - 0.4, and 0.3.
Since they work together (heading to the same direction), this indicates postive strength.

A function called check_inputs() returns True  if the total number of inputs for all the neurons is equal to the size of the array SOURCE and the array STRENGTH, otherwise it returns False. This helps test the integrity of the program.
 
**(c) Create the algorithm for the function check_inputs()**

![155566987_2906517476262231_2955186504936455903_n](https://user-images.githubusercontent.com/60457723/109412611-431aba80-79ec-11eb-9068-1c2d5b4a9e61.jpg)

Another function get_index(id)returns the index of the array NEURON where the neuron with the id provided is stored. Assume that neuron ids are random integer numbers. 

**(d) Create a flow diagram for this function.**

![155786306_483043889521062_1938143043616529614_n](https://user-images.githubusercontent.com/60457723/109412618-48780500-79ec-11eb-9741-b60ad2a94787.jpg)

**(e) The function simulate() shown above, calculates the outputs of the neurons based on the arrays defined previously.  State one line in the code where a precondition is used.**

out = 0.0

**(f) Trace the program simulate() with the arrays given above and show the output of NEURON[3].**


### Python Code

```.py
neuron = [1,2,3,4]
cur_output = [0.5,0.2,0.2, -0.1]
num_inputs = [1,2,2,1]
source = [4,1,3,1,2,1]
strength = [-0.1, 0.5, -0.4, 0.3, -0.4, 0.2]

def simulate(neuron, cur_output, num_inputs, source, strength):
    
    def check_inputs():
        so_len = len(source) - 1
        st_len = len(strength) - 1
        sum_inputs = 0
        for i in range(0, len(num_inputs) - 1):
            sum_inputs += num_inputs[i]
        if sum_inputs == so_len and so_len == st_len:
            return True
        else:
            return False
    
    def get_index(id):
        for i in range(0, len(neuron) - 1):
            if neuron[i] == id:
                return [i]
                
                
    if check_inputs():
        start_idx = 0
        for n in range(0,len(neuron) - 1):
            end_idx = start_idx + num_inputs[n]
            out = 0.0
            for k in range(start_idx, end_idx-1):
                temp = get_index(source[k])
                out += strength[temp] * cur_output[temp]

            cur_output[n] = out
            start_idx = end_idx
            print("Output of neuron id", neuron[n], "is", out)
        return cur_output
    else:
        return "Error in the initialization"
                
```


