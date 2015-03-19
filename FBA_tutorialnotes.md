#Day 1 Morning
Creating knockouts, knock out gene, see rxns removed, then go in and add that reaction to the FBA model file
__MetaCyc__ generated from nearly 6000 databases. Contains all the pathways, predictions, curated. Mother of all databases. 34,000 publications read and curated from.
PGDB is really a model of the organism. Focus on prokaryotes, but Eukaryotes add additional compartmental complications.
Tier 3 pathways add more pathways then it should, liberal use of the software because easier to remove then to add. SRI registry to find the full list of databases that have been contributed by other people, e.g from Stanford. Can create a webmode for any database for other people to view. Controlled vocabulary really important and Ontology classes and evidence codes. 13 common metabolites to pull all of these pathways together. Written in LISP even the web server, everything developed first on Linux. Ocelot object database, cannot query using SQL. Check out pathway tools blog to see what is new with each update of pathway tools.

__Pathologic__ uses metacyc to try to infer pathways from genome. 

__FBA__ organism is growing at an optimal rate. Using least amount of nutrients to maintain a steady state of growth per unit time. Has additional secretions. Requires a really good PGDB and is a good way to test whether the model is really good. Only include the good pathways in the PGDB. Here is the precision of my model based on knock out data. AKA remove gene die. mmol/gDW/hr is the unit of the flux. Work from core metabolism out or carve away from larger block of reactions. Could run CPLEX with a good solver (but costs $12000 for license, maybe free academic license?). Linear solve, not quadratic, not least squares. Sparse stoichiometric matrix. 

Sijv = 0 where 0 is a matrix that represents all the metabolites. 
Reactions are columns
Metabolites are rows
LP formulation where C, D, E are nutrients in the network. 

Uses the best non-commercial solver
http://scip.zib.de/

#Input file
When running the fba it first checks the file to make sure the parsing was done correctly.
One messed up mass balance reaction can mess up the whole model. If not mass balanced then software removes them from model. 
All of these are listed in the log file to make sure all the things are playing nicely
Also, all reactions included in the model, reversable reactions are seperated into 2 reactions going in one direction.
Blocked reactions are impossible reactions, even before solving are zero.

#Solution File
dat file using the cellular overview can be version controlled and have others look at output of model
lp file can be used with nearly any solver, standard format.

#community mode
can make many FBA models to work together.

#unbalanced reactions- instantiation MK
this now includes H+ charges for pH 7.3

There will be an "*" next to the name of the DB if it has been modified. You can revert back to the original if you need to, but you may need to redue all the curating if you overwrite the DB file. 

Molecular weight to less than 0.01 for things like "light", for a special case of photons. So this is a hack for less than the weight of an atom. 

Use the consistancy Checker that runs a balance report for all the rxns in the PGDB. You should do this for FBA, the unbalanced rxns will come up in an editor and then you can try and fix them.

Another thing that needs to be taken care of is the transporter reactions that need to be defined in subcellular compartments, like ATP synthase, ETC.

There can be a more than one way to represent these polymerization pathways. 
Instantiation of reactions will be wrong if there are different steriochemistry because you can have two reactions with the same chemical mass balance but because you have different sterioisomers it will not distinquish between them and might throw them out.

# Development Mode
model will not run so move all the 












