# InfoTrack Tech Challenge


## Task 1

This task is a bit abstract since not all the parameters are available to make a decision immediately. Some immediate caveats come up:

* Even an address, date of birth and place of birth don't garuantee unique identification of a person (It's easy to think of two John Smiths being born in London on the same day).
* Addresses can change, ergo, a different address doesn't necessarily indicate a different person.
* Since the system seems to allow free entries, people might also misspell their names at times?

Because of the two above reasons, I would definitely argue against merging records under one identifier in the main/base dataset.
It's very simply bad practice to risk false information at least if undeclared (merging data under a unique id clearly indicates that it belongs to the same record factually). 
A far more reasonable approach would be simply storing this "log" in it's raw format and generating other lists for application-specific purposes, because the aggregation (or matching) approach could be different depending on what it is you are trying to do with it.
For example, if the plan is to provide an overview of e.g. the companies a person has looked at, it would make sense to show two different lists, one that is the confirmed list of the specific record, the other being the extended list of records that could represent the same person with some uncertainty.

That being said, I think the correct way to do solve this issue would be to group by name (as that will reduce most of the possible duplication) and then process records according to deterministic rules e.g. 
```
if one of DoB/Address/PoB match and none of DoB/Address/PoB differ:
  merge record and generate unique id
```
Unfortunately, there is not really any way of avoiding the inefficiency that all incomplete records need to be loaded everytime to perform the merge.


## Task 2

The predicted "Exited" values can be found at `data/Task_2/predictions.csv` and the model used to generate them in `churn_predictions.ipynb`.
