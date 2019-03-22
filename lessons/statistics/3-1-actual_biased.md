[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

>> Exercise 3.1 Something like the class size paradox appears if you survey
children and ask how many children are in their family. Families with many
children are more likely to appear in your sample, and families with no children have no chance to be in the sample.
Use the NSFG respondent variable NUMKDHH to construct the actual distribution for the number of children under 18 in the household.
Now compute the biased distribution we would see if we surveyed the children
and asked them how many children under 18 (including themselves) are in
their household.
Plot the actual and biased distributions, and compute their means. As a
starting place, you can use chap03ex.ipynb.

```resp = nsfg.ReadFemResp()

def UnbiasPmf(pmf, label=None):
    new_pmf = pmf.Copy(label=label)

    for x, p in pmf.Items():
        new_pmf[x] *= 1/x
        
    new_pmf.Normalize()
    return new_pmf

hist = thinkstats2.Pmf(resp.numkdhh, label = 'number of children under 18')
thinkplot.Pmf(hist)
thinkplot.config(xlabel='Children', ylabel='PMF')

pmf = thinkstats2.Pmf(resp.numkdhh, label = 'number of children under 18')
biased_pmf= BiasPmf(pmf, label='number of children under 18')
thinkplot.Pmf(biased_pmf)
thinkplot.config(xlabel='children',ylabel='PMF')

print('biased mean = ', biased_pmf.Mean())
print('unbiased mean = ',pmf.Mean())

```
