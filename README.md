# A Maude simulator for Lending Pools

Lending Pools (LP) is a formal model of a subclass of Decentralised Finance applications deployed on Ethereum. It has been first formalised in [SoK: Lending Pools in Decentralized Finance](https://arxiv.org/abs/2012.13230) resulted from the joint effort of Università degli Studi di Cagliari (UniCa) and Technical University of Denmark. This tool provides a formal specification and discrete-event simulator of LP, supporting a number of analysis on the model:

- reachability analysis;
- LTL model checking on finite state-space;
- statistical analysis\*. 

> \* The source of the statistical analysis, developed using [MultiVeStA](https://github.com/andrea-vandin/MultiVeStA/wiki), is not available in this version of the software. This is due to the fact that the MultiVeStA source is not publicly available.

The tool usage and implementation are explained [here](https://aaltodoc.aalto.fi/bitstream/handle/123456789/109268/master_Mirelli_Massimiliano_2021.pdf). 

# Getting started

The LP model has been developed in [Maude 3.0](http://maude.cs.illinois.edu/w/index.php?title=Maude_download_and_installation&oldid=252). 

In order to run the Lending Pools simulator follow the instructions:

1. download Maude 3.0 with Yices 2 ([linux](http://maude.cs.illinois.edu/w/images/2/27/Maude-3.0%2Byices2-linux.zip) | [MacOS](http://maude.cs.illinois.edu/w/images/b/bb/Maude-3.0%2Byices2-osx.zip))
2. Execute:
```
cd <project_root>/maude-lp
unzip ~/Downloads/Maude-3.0+yices2-linux.zip -d $PWD/internals # you might need to change the name of the zip
mv ./internals/maude-Yices2.linux64 ./ && chmod +x maude-Yices2.linux64
export MAUDE_HOME=${PWD}
export MAUDE_LIB=${MAUDE_LIB}:${MAUDE_HOME}/internals 
./maude-Yices2.linux64
```

Then, you should be welcomed by the following:

```
		     \||||||||||||||||||/
		   --- Welcome to Maude ---
		     /||||||||||||||||||\
	     Maude 3.0 built: Dec 16 2019 20:24:06
	     Copyright 1997-2019 SRI International
		   Tue Apr 20 10:54:26 2021
```

Finally just run:

3. `load run.maude`

> Note: `run.maude` contains a line to (un/)toggle tests. For (running/)stop running just (un/)comment the line `load tests/unit.maude` (unit tests) or `load tests/suite.maude` (unit and rules tests). 

> Note: A test is failing iff it returns false, so just search for `"false"` in the output of `load run.maude` when one of the lines triggering tests are untoggled.

# Reproduce the thesis results

In order to reproduce the results in the thesis, please install java 11, follow the steps described in the [Getting started](#getting-started) and execute the additional ones below.

```
cd <project_root>/maude-lp
export MAUDE_BIN=maude-Yices2.linux64
wget https://github.com/MMirelli/maude-lp/releases/download/v1.0.0/LPMultivesta-1.0.0.tar
tar -xvf LPMultivesta-1.0.0.tar
java -jar LPMultivesta-1.0.0-jar-with-dependencies.jar
```

The application will then output the following logs:

```
Parameters: 
model: LendingPools
other parameters: --pc -1.0 --im SMC-INITIAL-CONFIGURATIONS --ic eth-usdc-10-3-1.1-0.1 --pe eth-usdc --cm 1.5 --rl 1.1
model arguments: 
formula: obsAtStep(i,x) = if ( s.rval("steps") == x )  then s.rval(i)  else # obsAtStep(i,x) fi ; eval parametric(E[ obsAtStep("1_COLLATERALIZATION",x) ],                  E[ obsAtStep("2_COLLATERALIZATION",x) ],                 E[ obsAtStep("3_COLLATERALIZATION",x) ],                  E[ obsAtStep("4_COLLATERALIZATION",x) ],                  E[ obsAtStep("5_COLLATERALIZATION",x) ],                  E[ obsAtStep("6_COLLATERALIZATION",x) ],                   E[ obsAtStep("7_COLLATERALIZATION",x) ],                   E[ obsAtStep("8_COLLATERALIZATION",x) ],                   E[ obsAtStep("9_COLLATERALIZATION",x) ],                   E[ obsAtStep("10_COLLATERALIZATION",x) ],                 x,1,1,91) ;
sims: 15
Class name of the StateEvaluator: NO-CLASS-NAME-PROVIDED
Class name of the StateDescriptor: dk.dtu.compute.lp.multivesta.LPState
sims: 15
Class name of the StateEvaluator: NO-CLASS-NAME-PROVIDED
Class name of the StateDescriptor: dk.dtu.compute.lp.multivesta.LPState
Server: Received all data from client. The model and the queries have been built.
Server: Running the simulation batches on demand... Please wait.
Server: Received all data from client. The model and the queries have been built.
Server: Running the simulation batches on demand... Please wait.
Simulation 1 completed
Simulation 1 completed
```

When the execution completes, results are stored in `<project_root>/maude-lp/MultiVeStA_OUTPUT`.
