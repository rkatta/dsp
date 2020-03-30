[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

**Exercise 4** - Using the variable totalwgt_lb, investigate whether first babies are lighter or heavier than others. Compute Cohen’s d to quantify the difference between the groups. How does it compare to the difference in pregnancy length?
##### Cohen's d measures effect size; we would like to know how weight of the first baby compares to the weight for all subsequent babies by copmuting Cohen's d for these groups.

#### Function from book:
```python
def CohenEffectSize(group1, group2):
    """Computes Cohen's effect size for two groups.
    
    group1: Series or DataFrame
    group2: Series or DataFrame
    
    returns: float if the arguments are Series;
             Series if the arguments are DataFrames
    """
    diff = group1.mean() - group2.mean()

    var1 = group1.var()
    var2 = group2.var()
    n1, n2 = len(group1), len(group2)

    pooled_var = (n1 * var1 + n2 * var2) / (n1 + n2)
    d = diff / np.sqrt(pooled_var)
    return d
```

Here we investigate mean of first child vs all other childs:
```python
firsts.totalwgt_lb.mean(), others.totalwgt_lb.mean()
```
* First baby mean weight is 7.201094430437772
* All other babies mean weight is 7.325855614973262)

```python
CohenEffectSize(firsts['totalwgt_lb'],others['totalwgt_lb'])
```

>-0.08867

Cohen's d can be computed for the difference in pregnancy length for first babies and others using the above function with two parameters as described in the ThinkStat's Github library:

```python
CohenEffectSize(firsts.prglngth,others.prglngth)
```
>0.02887

<b>This analysis seems to suggest that even though the length of pregnancy is greater for first borns, their weight is generally lower.</b>
