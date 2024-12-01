# UBSolver
In this challenge we have tried to solve the problem proposed by UBS about the Entity Resolution Challenge. <br>
Our solution is very time efficient and has a very good performance on the test dataset provided (we got a F-score of 0.87).

## Code structure
The code can be is in the main.ipynb file and it includes:
- A cleaning section: we have used some rules to clean the data and reduce the number of samples.
- A processing section: we compute some similarity metrics that we are then going to use to match the samples.
- A matching section: we match together similar samples with a graph-based approach.

## The idea
The main ideas that we have used are:
- Since we are in a case with lots of data (bilions!) we need to reduce them to avoid too high computational costs. For this reason we matched together samples that are clearly the same (i.e. IBAN, name, address, etc.). This was inspired by the observatin that almost all the transaction from a common entity matched on at least one of the features.<br>
- For every pair of matched elements we compute the Levenshtein similarity (all the features are strings) is computed for every feature. <br>
- We trained a Neural Network to predict if two samples are the same or not based on the similarity scores computed before. This neural network is very simple since it's a multi-layer perceptron with 2 hidden layers (100 - 50 neurons). <br>
- Finally we created a graph on the test set and we used the trained Neural Network to match together samples that are similar. Another important observation which allowed us to efficiently create the set was to discard the values which appeared too often as they weren't significant to match the entities. <br>
- Each strongly connected component of the graph is an entity representing a person or a company.

## The team
Our team:
- Matteo Santelmo matteo.santelmo@epfl.ch
- Alessandro Dalbesio alessandro.dalbesio@epfl.ch
- Stefano Viel stefano.viel@epfl.ch