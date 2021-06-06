# A Maude simulator for Lending Pools

Lending Pools (LP) is a formal model of a subclass of Decentralised Finance applications deployed on Ethereum. It has been first formalised in [SoK: Lending Pools in Decentralized Finance](https://arxiv.org/abs/2012.13230) resulted from the joint effort of Università degli Studi di Cagliari (UniCa) and Technical University of Denmark. This tool provides a formal specification and discrete-event simulator of LP, supporting a number of analysis on the model:

- reachability analysis;
- LTL model checking on finite state-space;
- statistical analysis\*. 

> \* Statistical analysis, developed using [MultiVeStA](https://github.com/andrea-vandin/MultiVeStA/wiki), is not available in this version of the software.

The tool usage and implementation are explained [here](*TODO*: add link to MSc thesis.). 

# Getting started

The LP model has been developed in [Maude 3.0](http://maude.cs.illinois.edu/w/index.php?title=Maude_download_and_installation&oldid=252). 

In order to run the Lending Pools simulator follow the instructions:

1. download Maude 3.0 with Yices 2 ([linux](http://maude.cs.illinois.edu/w/images/2/27/Maude-3.0%2Byices2-linux.zip) | [MacOS](http://maude.cs.illinois.edu/w/images/b/bb/Maude-3.0%2Byices2-osx.zip))
2. `cd <project_root>/maude-lp`
3. `unzip ~/Downloads/Maude-3.0+yices2-linux.zip -d $PWD/internals # you might need to change the name of the zip` 
4. `mv ./internals/maude-Yices2.linux64 ./ && chmod +x maude-Yices2.linux64`
5. `export MAUDE_LIB=$MAUDE_LIB:$PWD/internals`
6. `./maude-Yices2.linux64`

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

7. `load run.maude`

> Note: `run.maude` contains a line to (un/)toggle tests. For (running/)stop running just (un/)comment the line `load tests/unit.maude` (unit tests) or `load tests/suite.maude` (unit and rules tests). 

> Note: A test is failing iff it returns false, so just search for `"false"` in the output of `load run.maude` when one of the lines triggering tests are untoggled.
