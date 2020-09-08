# Downloading data from SpikeForest

## Prerequisites

* Python >= 3.6

Highly recommend using a conda or virtualenv

## Install kachery

```
pip install --upgrade kachery
```

Make a designated directory for storing large temporary files

```
# You can choose any location, for example:
export KACHERY_STORAGE_DIR=/home/<user>/kachery-storage
```

Add the above line to your `~/.bashrc` so that the variable gets set whenever a new terminal is opened.

## Find a ground truth spike train on spikeforest

Main site:

```
http://spikeforest.flatironinstitute.org
```

For example, you could navigate to: http://spikeforest.flatironinstitute.org/recording/paired_boyden32c/1103_1_1

You can then click on and copy the sha1:// URI to the ground truth spike trains... for this particular example it would be:

```
firings_true_path = 'sha1dir://49b1fe491cbb4e0f90bde9cfc31b64f985870528.paired_boyden32c/1103_1_1/firings_true.mda'
```

## Download ground truth spike train into a SpikeInterface sorting extractor

Now you can download that file in various ways.

```bash
# From the command line
kachery-load sha1dir://49b1fe491cbb4e0f90bde9cfc31b64f985870528.paired_boyden32c/1103_1_1/firings_true.mda --fr default_readonly --dest firings_true.mda
```

```python
# From python
import kachery as ka
with ka.config(fr='default_readonly'):
    path_local = ka.load_file(firings_true_path)
```

But most conveneniently, you would want to load it into a [SpikeInterface](https://github.com/SpikeInterface) object:

```python
# pip install --upgrade spikeextractors

import spikeextractors as se

with ka.config(fr='default_readonly'):
    path_local = ka.load_file(firings_true_path)
    sorting = se.MdaSortingExtractor(path_local)

# Now you can access the spike train through the sorting object
# See: https://github.com/SpikeInterface/spikeinterface/blob/master/examples/modules/extractors/plot_2_sorting_extractor.py

# We can now print properties of the sorting
print('Unit ids = {}'.format(sorting.get_unit_ids()))
st = sorting.get_unit_spike_train(unit_id=1)
print('Num. events for unit 1 = {}'.format(len(st)))
st1 = sorting.get_unit_spike_train(unit_id=1, start_frame=0, end_frame=30000)
print('Num. events for first second of unit 1 = {}'.format(len(st1)))
```

## Download sorting results from SpikeForest

It is also possible to download the results of SpikeForest spike sorting, in a very similar way. See the sorting outputs on the bottom of that same page: http://spikeforest.flatironinstitute.org/recording/paired_boyden32c/1103_1_1

For example, here is the sorting output for KiloSort2: `sha1://e2a202f8b97731f51e4c6e91f4471c3b56ede242/e2a202f8b97731f51e4c6e91f4471c3b56ede242/firings.mda`