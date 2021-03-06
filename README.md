# entropyes
entropyes repository provides a peak into essential entropy toolkit building, for neural data visualisation in the context of randomness/predictability.

The toolkit, so far, contains a few processing pipelines needed to visualise the sampling bias regularisation output for neural units entropy(different bias-reduction approaches), raw and Poisson-regularised entropy plotted against firing rate and variance, essential spike train statistics, and mutual information computation between different extracellular and ground-truth (patch-clamp or juxtacellular) neural recordings. 

The toolkit in its current state helps in the information-theoretic analysis of the neural spike trains obtained from the spike sorting process, in that it adds a separate metric for assessing the sorting algorithms' performance (next to the sorting accuracy, obtained from the sorting output's comparison with invasively-obtained ground-truth data).

Next developments will be focused on estimating individual neural units' quality for specific sorters.

entropyes is to be integrated within the spikeforest framework (Flatiron Institute, https://github.com/flatironinstitute/spikeforest2).



