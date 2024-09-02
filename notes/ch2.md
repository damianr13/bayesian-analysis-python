# Glossary 

### Savage-Dickey - shows how much more support a resulting posterior gives for a certain value
In the coin example for instance, we would like to know how much the prior supports the value of 0.5 (fair coin).

### Region Of Practical Equivalence (ROPE) - An interval for we consider the coin to be fair

3 cases are distinguished here: 
- The ROPE does not overlap the HDI (High Density Interval) -> the coin is not fair
- The ROPE contains the entire HDI -> the coin is fair
- The ROPE partially overlaps HDI -> not a definitive answer, more data is required

# Code examples 

## Flipping coins in PyMC
```python
with pm.Model() as our_first_model:
    θ = pm.Beta('θ', alpha=1., beta=1.)
    y = pm.Bernoulli('y', p=θ, observed=data)
    idata = pm.sample(1000, random_seed=4591)
```
- Everything is enclosed in the `pm.Model()` context
- The last line creates an `InferenceData` object
- The backbone for PyMC is [PyTensor](https://github.com/pymc-devs/pytensor)

## Testing the posterior
```python
az.plot_trace(idata)
```
- We want the left chart (that shows the different channels) to show lines that are very similar
- We want the right chart to be very noisy, show indistinct lines (which means the data for our different channels 
is random and doesn't fall into a particular pattern) 

