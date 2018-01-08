# PLATFORM
	DistAlgo Version : pyDistAlgo-1.0.9
	Python Implementation and Version : Python 3.6.2
	Operating Systems : macOS 10.12 Sierra and Windows 10
	Number and Types of Hosts : 2 [Mac OS Laptop,pyDistAlgo-1.0.9,Python 3.6.2 AND Windows10 OS Laptop,pyDistAlgo-1.0.9,Python 3.6.2]

# INSTRUCTIONS
	DistAlgo (version : pyDistAlgo-1.0.9) and Python (version 3.4 or higher) must be installed.
	Received/Downloaded code files(with .da extension) from this project should be placed under DistAlgo installation path folder (\pyDistAlgo-1.0.9\pyDistAlgo-1.0.9\)
	Execute following commands (in mentioned order) in terminal/command prompt/shell.
	1. python -m da -n OlympusNode --logfilelevel output --logfile --logfilename Olympus_Config1-log Olympus.da
	2. start python -m da -n ClientNode0 --logfilelevel output --logfile --logfilename Client0_Config1-log -D Olympus.da
	3. start python -m da -n ClientNode1 --logfilelevel output --logfile --logfilename Client1_Config1-log -D Olympus.da
	4. start python -m da -n ClientNode2 --logfilelevel output --logfile --logfilename Client2_Config1-log -D Olympus.da
	5. start python -m da -n ReplicaNode0 --logfilelevel output --logfile --logfilename Replica0_Config1-log -D Olympus.da
	6. start python -m da -n ReplicaNode1 --logfilelevel output --logfile --logfilename Replica1_Config1-log -D Olympus.da
	7. start python -m da -n ReplicaNode2 --logfilelevel output --logfile --logfilename Replica2_Config1-log -D Olympus.da

# WORKLOAD GENERATION
	Algorithm for pseudo-random client generation - 
		We have a pre-computed list for random keys, a list for for random values, and a dictionary for the 4 operation names(put,get,append and slice)
		For every operation(put,get,append and slice), the arguments(key-value pair) are decided before seed setting by random.choice() on the respective list.
		Now, Seed for the random is set to the second argument given in the config file. The seed is set at this step so as to not make the above operations look repetetive.
		The seed determines the operation names(put,get,append,slice) by calling random.randint(0, 3)
		THe seed makes sure that operations are consistent for a particular seed.
		The operation name along with the key and value are formed into a string.
		This string is appended to a list. 
		The list finally contains given number(n) of random operations.
		Every operation in this list is passed on as one normal operation to the Head Replica.
	
# BUGS AND LIMITATIONS
	BUGS
		Checked some test cases and output is attached along. No bugs for the checked test cases.
	LIMITATIONS
		1. 	We have skipped trigger for forward_request() because of lock of time
			
		2.	We have checked multi-host implementation earlier. It was working fine.
			Though, we could not verify before submission due to lack of time and that one of our laptops malfunctioned. 
			So, we can not commit on multi-host execution
	
# CONTRIBUTIONS
	Ankur Maheshwari (110008503)
	Vipul Gandhi (111483224)
	We acknowledged that it will be pretty difficult to code on the same file at the same time.
	Even distribution of work into modules seemed quite inconvenient to us because almost every module have dependency on previous modules.
	Moreover, Merging modules would have given rise to more bugs, which have been difficult to debug and thus time consuming.	
	So, we distributed our work in order that at any point of time only one of us will write the main code.
	While the other team member will provide every other required side functionality for the main logic.
	
	Ankur :
		Client - Handle results(check signature proofs)
		Client - timeout and send request to all replicas
		Olympus -  Multi-Node(create keys, create, setup, and start processes)
		Replica - Head : Handle new request
		Replica - Head : Retransmit new request
		Replica - Head : Handle shuttle: check validity of order proof
		Replica - Head : tail: send result to client
		Replica - Handle result shuttle
		Replica - Head : non-head: handle request
		Replica - Fault-injection implementation
		MultiHost Execution
		Adding Logs
		Documentation
		Testing and Debugging
	
	Vipul
		Client - Pseudorandom implemetation
		Client - Generate request sequence
		Client - Local Dictionary implemetation
		Replica - Dictionary object support put,get,slice,append
		Replica - Fault injection setup
		Olympus - Single Node implemetation(replica client setup and start processes)
		Support configuration files in project.txt
		Documentation
		Testing and Debugging

# MAIN FILES
	Main Driver File is Olympus.da which creates the distributed nodes for every replica, clients and 1 Olympus etc
	1. Client File : src/Client.da
	2. Replica File : src/Replica.da
	3. Olympus File : src/Olympus.da
	
# CODE SIZE
	Replica.da
		1.	LOC
			a.	Non-blank Line of Code
				- Algorithm 204
				- Other 188
				- Total 392
			b.	Python function of our own and Manually too.
		2.	Algorithm %age in Non-blank Line of Code
			80%
	Client.da
		1.	LOC
			a.	Non-blank Line of Code
				- Algorithm 149
				- Other 58
				- Total 207
			b.	Python function of our own and Manually too.
		2.	Algorithm %age in Non-blank Line of Code
			100%
	Olympus.da
		1.	LOC
			a.	Non-blank Line of Code
				- Algorithm 25 
				- Other 155
				- Total 180
			b.	Python function of our own and Manually too.
		2.	Algorithm %age in Non-blank Line of Code
			100%			
			
# LANGUAGE FEATURE USAGE
	list comprehensions - 29
	dictionary comprehensions - 24
	set comprehensions - 0
	aggregations - 0
	quantifications - 3