--------------------
[0.1.6] - ****-**-**
--------------------

**Breaking changes**

- The standalone ``preprocess_ts`` function now defaults to not removing unreferenced
  individuals, populations, or sites, aiming to change the tree sequence tables as
  little as possible.

- Not strictly breaking, as not in the published API, but the "normalize" flag
  in ``get_dates`` and the internal ``normalize`` terminology is changed to
  ``standardize`` to better reflect the fact that the maximum (not sum) is one.

- The ``Ne`` argument to ``date`` has been deprecated (although it is
  still in the API for backward compatibility).  The equivalent argument
  ``population_size`` should be used instead.

- The CLI ``-verbosity`` flag no longer takes a number, but uses
  ``action="count"``, so ``-v`` turns verbosity to INFO level,
  whereas ``-vv`` turns verbosity to DEBUG level.

**Features**

- Priors may be calculated using a piecewise-constant effective population trajectory,
  which is implemented in the ``demography.PopulationSizeHistory`` class. The
  ``population_size`` argument to ``date`` accepts either a single scalar effective
  population size, or a ``PopulationSizeHistory`` instance.

**Bugfixes**

- The returned posteriors when ``return_posteriors=True`` now return actual
  probabilities (scaled so that they sum to one) rather than standardized
  "probabilities" whose maximum value is one.

- The population size is saved in provenance metadata when possible (e.g. if it is
  a single number)

- ``preprocess_ts`` always records provenance as being from the ``preprocess_ts``
  command, even if no gaps are removed. The command now has a (rarely used)
  `delete_intervals` parameter, which is normally filled out and saved in provenance
  (as it was before). If no gap deletion is done, the param is saved as ``[]``

--------------------
[0.1.5] - 2022-06-07
--------------------

**Features**

- Added the ``time_units`` parameter to ``tsdate.date``, allowing users to specify
  the time units of the dated tree sequence. Default is ``"generations"``.
- Added the ``return_posteriors`` parameter to ``tsdate.date``. If True, the function
  returns a tuple of ``(dated_ts, posteriors)``.
- ``mutation_rate`` is now a required argument in ``tsdate.date`` and ``tsdate.get_dates``
- tsdate returns an error if users attempt to date an unsimplified tree sequence.
- Updated tsdate citation information to cite the recent Science paper
- Built wheel on Python 3.10


--------------------
[0.1.4] - 2021-06-30
--------------------

**Features**

- The algorithm now operates completely in unscaled time (in units of generations) under
  the hood, which means that ``tsdate.build_prior_grid`` now requires the parameter
  ``Ne``.
- Users now have access to the marginal posterior distributions on node age by running 
  ``tsdate.get_dates``, though this is undocumented for now.

**Bugfixes**

- A fix to the way likelihoods are added should eliminate numerical errors that are
  sometimes encountered when dating very large tree sequences.

--------------------
[0.1.3] - 2021-02-15
--------------------

**Features**

- Two new methods, ``tsdate.sites_time_from_ts`` and ``tsdate.add_sampledata_times``, 
  support inference of tree sequences from non-contemporaneous samples.
- New tutorial on inferring tree sequences from modern and historic/ancient samples 
  explains how to use these functions in conjunction with ``tsinfer``.
- ``tsdate.preprocess_ts`` supports dating inferred tree sequences which include large, 
  uninformative stretches (i.e. centromeres and telomeres). Simply run this function 
  on the tree sequence before dating it.
- ``ignore_outside`` is a new parameter in the outside pass which tells ``tsdate`` to 
  ignore edges from oldest root (these edges are often of low quality in ``tsinfer``
  inferred tree sequences)
- Development environment is now equivalent to other ``tskit-dev`` projects


--------------------
[0.1.2] - 2020-02-28
--------------------

- Improve user experience with more progress bars and logging.
- Slightly change traversal method in outside and outside maximization algorithms,
  this should only affect inference on inferred tree sequences with large numbers 
  of nodes at the same frequency.
- Improve reporting of current project version
- Use appdirs for default caching location
- Prevent dating tree sequences with dangling nodes


--------------------
[0.1.1] - 2020-02-25
--------------------

Bugfix release: resolve issue with precalculating prior values.


--------------------
[0.1.0] - 2020-02-24
--------------------

Early Alpha release made available via PyPI for community testing and evaluation.

Please don't use this version in published works.


