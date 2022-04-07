# Hyperoptimization

1.185±0.013

1.185±0.013

**clipnorm bugged candidate:** 

![pdf_210127-n3fit-001.png](Hyperoptim%20eb553/pdf_210127-n3fit-001.png)

## Validation delta chi2

**One requirement is that we do not want the PDFs to be correlated with the validation data as this suggests overfitting. Is there a way we can identify when this happens?**

Perform a fit in the usual way, and calculate (extract from the .json file) the $\chi_{\rm vl}^2$ of the validation data.  Then on average this $\chi_{\rm exp}^2$ should not be better than the loss of any other psueododate set that could have been (or the central value $\chi_{\rm exp}^2$ for that matter). Namely, if the loss on the validation data is better than the loss of the expected loss for the $\chi_{\rm exp}^2$, that means that data was extracted from the validation data. **This idea might be spoiled as a result of the vld and tr data not being uncorrelated.**

Is the difference between training and validation chi2s compared to the experimental chi2 really only due to not having replica'd data?

Actually, because the validation data is replica'd and thus the loss is worse than the experimental loss, this suggests that the experimental chi2 is (of course) not the same as the validation loss. However, the validation loss determined during the fit should be the same as the validation loss of a validation set not used during the fit. If the validation loss determined during the fit is better than that of alternative psuedodata replicas generated for the same points then we say the PDF is overfitted.

**Sure, but the there will be a distribution associated with the loss of the alternative psueodatata sets, so the loss of the validation replicas used during trainig is likely at an acceptable point (less than e.g. 2sigma) in this distribution.**

Indeed, but if we repeat this for order 100 replicas we can for example obtain a distirubtion of where these positions of the validation data loss within the distribution of losses of alternative validation data sets. And here it might be more clearly visible if the distirbution is clearly skewed towards overfitting. 

### Results

**expected_delta_chi2**  determined using **recreate_pdf_pseudodata** for various fits:

- 210612-n3fit-001: 0.00270472831526507
- 211220-jcm-overfitted-001: -0.02318586106422251
- 211202-01-rs-underfitted: -0.005522317627211817 🤔

While with **read_pdf_pseudodata** we find 

- 211220-jcm-overfitted-001:  -0.017693278196916577
- 211202-01-rs-underfitted: 0.0009364826521945036
- 220209-01-rs-nnpdf40:  -0.0012140624684351042

Or we can do the following script:

```python
# are they the same distriubtion?
print(fitted_val_erf.mean())
print(fitted_val_erf.std())
print(res_over.mean())
print(res_over.std())
```

Which for the training data and the PDF 211220-jcm-overfitted-001, gives

```python
2.209052801132202
0.0641141579862776
2.2500445682089785
0.07027106040385105
```

### Hyperopt with validation data demonstration:

### Step 1:

First we run a hyperopt. The results can be found here: [https://vp.nnpdf.science/sDCNBpWXTduorLz4bF_4pQ==](https://vp.nnpdf.science/sDCNBpWXTduorLz4bF_4pQ==)

### Step 2:

Then we select the top 10 setups and perform a full ~100 replica fit with them. Here 10 is chosen somewhat arbitarily, though in this case it roughly agrees with the size of the fluctuations on the hyperopt loss. 

Using the validation data delta chi2 idea we filter out any replica that has a mean/std of below -1. Base on only this metric there is of course some probability that these are not in truth overfitted (though looking at the pdfs will change ones mind on this), but we have many setups to try/investicage and so we don´t waste our time with ones that are likely overfitted. 

The results of the validation delta chi2 thing is listed below. The ones that we consider overfitted have been ~~striked out~~, and will be discarded / considered overfitted. 

**We also include the NNPDF4.0 baseline for comparison**

~~hyperopt_0: [https://vp.nnpdf.science/RYE2JP_eSAeHNApe1Mcz5w==](https://vp.nnpdf.science/RYE2JP_eSAeHNApe1Mcz5w==/)~~

![pdf_hyperopt_0.png](Hyperoptim%20eb553/pdf_hyperopt_0.png)

~~hyperopt_1: [https://vp.nnpdf.science/qoB9BiXyRcG7nv7hnFcviQ==/](https://vp.nnpdf.science/qoB9BiXyRcG7nv7hnFcviQ==/)~~

![pdf_hyperopt_1.png](Hyperoptim%20eb553/pdf_hyperopt_1.png)

hyperopt_2: [https://vp.nnpdf.science/3eNqRSZrSXGSKxaYg0rdUw==/](https://vp.nnpdf.science/3eNqRSZrSXGSKxaYg0rdUw==/)

![pdf_hyperopt_2.png](Hyperoptim%20eb553/pdf_hyperopt_2.png)

![training_pdf_hyperopt_2.png](Hyperoptim%20eb553/training_pdf_hyperopt_2.png)

~~hyperopt_3: [https://vp.nnpdf.science/ddsEL7VnSJ-gFWwOnK0YQA==/](https://vp.nnpdf.science/ddsEL7VnSJ-gFWwOnK0YQA==/)~~

![pdf_hyperopt_3.png](Hyperoptim%20eb553/pdf_hyperopt_3.png)

hyperopt_4 (100 replicas): [https://vp.nnpdf.science/UYvIpWLUQZCXhuIwl_O6OQ==](https://vp.nnpdf.science/UYvIpWLUQZCXhuIwl_O6OQ==)

![pdf_hyperopt_4.png](Hyperoptim%20eb553/pdf_hyperopt_4.png)

~~hyperopt_5: [https://vp.nnpdf.science/Ey9rqa8eSFy0dm4iid-t4Q==](https://vp.nnpdf.science/Ey9rqa8eSFy0dm4iid-t4Q==)~~

![pdf_hyperopt_5.png](Hyperoptim%20eb553/pdf_hyperopt_5.png)

hyperopt_6: [https://vp.nnpdf.science/3KIFy7ujQbeh5D_0-u_zOw==/](https://vp.nnpdf.science/3KIFy7ujQbeh5D_0-u_zOw==/)

![pdf_hyperopt_6.png](Hyperoptim%20eb553/pdf_hyperopt_6.png)

~~hyperopt_7: [https://vp.nnpdf.science/hdbJ2dESQaqUHFMTm-jl-g==](https://vp.nnpdf.science/hdbJ2dESQaqUHFMTm-jl-g==)~~

![pdf_hyperopt_7.png](Hyperoptim%20eb553/pdf_hyperopt_7.png)

~~hyperopt_8: [https://vp.nnpdf.science/UfqfMOZTTzixFQZAFLlH_A==/](https://vp.nnpdf.science/UfqfMOZTTzixFQZAFLlH_A==/)~~

![pdf_hyperopt_8.png](Hyperoptim%20eb553/pdf_hyperopt_8.png)

hyperopt_9: [https://vp.nnpdf.science/FcYghjYjTTShwtL2_gjTfA==](https://vp.nnpdf.science/FcYghjYjTTShwtL2_gjTfA==)

![pdf_hyperopt_9.png](Hyperoptim%20eb553/pdf_hyperopt_9.png)

### Step 3:

As has been seen, most setups suggested by this hyperot run actually turn out to result in overfitting, leaving us with three potential candidates

- hyperopt_2: Discard because it clearly has some odd outliers, also poorer validation loss than 9
- hyperopt_4: Looks overfitted — but let’s see if more samples make the signal clearer
- hyperopt_9: seems decent — let’s als do more samples to see if the deltachi2 remains around 0

Hyperopt_4 (~450 replicas): [https://vp.nnpdf.science/xf0D0goqQ26GOvePiqwU2A==/](https://vp.nnpdf.science/xf0D0goqQ26GOvePiqwU2A==/)

![pdf_hyperopt_4.png](Hyperoptim%20eb553/pdf_hyperopt_4%201.png)

While the overfitting signal has become cleares as expected, the mean values shifted by much more than I would have expected (2 standard deviations from the point with 100 replicas). Maybe there is a mistake in the code, or does the chi2 to psuedodata really fluctuate this much? In fact, it almost looks as if delta chi2 corresponding to the first 100 replicas cannot be found in this plot, though this might be explained by the fact that even the first 100 now use an additional ~350 pseudodata replicas to be calculated. 

Hyperopt_9 (~450 replicas): [https://vp.nnpdf.science/Px-t59jiQW221fLw5pULmQ==/](https://vp.nnpdf.science/Px-t59jiQW221fLw5pULmQ==/)

![pdf_hyperopt_9.png](Hyperoptim%20eb553/pdf_hyperopt_9%201.png)

fit with only 10.000 epochs (~450 replicas): [https://vp.nnpdf.science/mkvBHKcfRLak_I9tzY2xmA==](https://vp.nnpdf.science/mkvBHKcfRLak_I9tzY2xmA==)

![pdf_hyperopt_10.png](Hyperoptim%20eb553/pdf_hyperopt_10.png)

Fit with only 2000 epochs (~ 300 replicas): [https://vp.nnpdf.science/f8FC0vnISV2TJ5C2VdeE0A==/](https://vp.nnpdf.science/f8FC0vnISV2TJ5C2VdeE0A==/)

![pdf_2000_epochs.png](Hyperoptim%20eb553/pdf_2000_epochs.png)

1.34±0.24