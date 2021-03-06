
Overview of the basic XOR example (xor2.py)
===========================================

The xor2.py example, shown in its entirety at the bottom of this page, evolves a network that implements the two-input
XOR function:

=======  =======  ======
Input 1  Input 2  Output
=======  =======  ======
0        0        0
0        1        1
1        0        1
1        1        0
=======  =======  ======

Fitness function
----------------

The key thing you need to figure out for a given problem is how to measure the fitness of the genomes that are produced
by NEAT.  Fitness is expected to be a Python float value.  If genome A solves your problem more successfully than genome B,
then the fitness value of A should be greater than the value of B.  The absolute magnitude and signs of these fitnesses
are not important, only their relative values.

In this example, we create a feed-forward neural network based on the genome, and then for each case in the
table above, we provide that network with the inputs, and compute the network's output.  The error for each genome
is 1 minus the root mean square difference between the expected and actual outputs, so that if the network produces exactly
the expected output, its fitness is 1, otherwise it is a value less than 1, with the fitness value decreasing the more
incorrect the network responses are.

This fitness computation is implemented in the ``eval_fitness`` function.  The single argument to this function is a list
of genomes in the current population.  neat-python expects the fitness function to calculate a fitness for each
genome and assign this value to the genome's ``fitness`` member.

Running NEAT
------------

Once you have implemented a fitness function, you mostly just need some additional boilerplate code that carries out
the following steps:

* Create a ``neat.config.Config`` object from the configuration file (described in :doc:`config_file`).

* Create a ``neat.population.Population`` object using the ``Config`` object created above.

* Call the ``epoch`` method on the ``Population`` object, giving it your fitness function and the maximum number of generations you want NEAT to run.

After these three things are completed, NEAT will run until either you reach the specified number of generations, or
at least one genome achieves the ``max_fitness_threshold`` value you specified in your config file.

Getting the results
-------------------

Once the call to the population object's ``epoch`` method has returned, a list of the most fit genome for each generation
is available as the ``most_fit_genomes`` member of the population.  We take the 'winner' genome as the last genome in
this list.

A list of the average fitness for each generation is also available as ``avg_fitness_scores``.

Visualizations
--------------

Functions are available in the ``neat.visualize`` module to plot the best and average fitness vs. generation, plot the
change in species vs. generation, and to show the structure of a network described by a genome.

Example Source
--------------

NOTE: This page shows the source and configuration file for the current version of neat-python available on
GitHub.  If you are using the version 0.6 installed from PyPI, make sure you get the script and config file from
the `archived source for that release
<https://github.com/CodeReclaimers/neat-python/releases/tag/v0.6>`_.

Here's the entire example:

.. literalinclude:: ../examples/xor/xor2.py

and here is the associated config file:

.. literalinclude:: ../examples/xor/xor2_config