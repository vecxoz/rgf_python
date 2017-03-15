# rgf_python
## Regularized Greedy Forest (RGF) Python wrapper (with x64 binaries)

**Summary:**

* The aim of this fork is to simplify installation and ensure usage out-of-the-box
* I forked [Python wrapper](https://github.com/fukatani/rgf_python), added [Win and Linux binaries](https://github.com/fukatani/rgf_python/releases/download/0.2.0/rgf1.2.zip), and made some changes in code
* So now you just need to install this package and you'll get working binaries with it
* Tested on: **Ubuntu 14.04 x64**, **Win 7 x64**
* Implementation (binaries) is **slow** (single thread)
* License for rgf_python: **Apache License v2.0**
* License for RGF: **GNU GPL v3**
* [RGF maintainer page](http://tongzhang-ml.org/software.html)
* [RGF page](http://tongzhang-ml.org/software/rgf/index.html)
* There are also multi-thread implementation [FastRGF](https://github.com/baidu/fast_rgf), but I didn't find Python wrapper for it and didn't try it

**Installation:**

```
git clone https://github.com/vecxoz/rgf_python
cd rgf_python
python setup.py install --user
```

**Usage:**

```python
from sklearn.datasets import load_iris, load_boston
from sklearn.model_selection import cross_val_score
from rgf.rgf import RGFClassifier, RGFRegressor

# Classification
iris = load_iris()
X = iris.data
y = iris.target
model = RGFClassifier()
print(cross_val_score(model, X, y, cv = 5))
# array([ 0.96666667,  0.96666667,  0.93333333,  0.9       ,  1.        ])

# Regression
boston = load_boston()
X = boston.data
y = boston.target
model = RGFRegressor()
print(cross_val_score(model, X, y, cv = 5))
# [ 0.7286153   0.79284581  0.7961001   0.47978064  0.1185657 ]
```

**Hyperparameter tuning:**

* *max_leaf*: Appropriate values are data-dependent and vary from 1000 to 10000.
* *test_interva*l: For efficiency, it must be either multiple or divisor of 100 (default of the optimization interval).
* *algorithm*: You can select "RGF", "RGF Opt" or "RGF Sib"
* *loss*: "LS", "Log" or "Expo".
* *reg_depth*: Must be no smaller than 1. Meant for being used with algorithm = "RGF Opt" or "RGF Sib".
* *l2*: Either 1, 0.1, or 0.01 often produces good results though with exponential loss (loss=Expo) and logistic loss (loss=Log) some data requires smaller values such as 1e-10 or 1e-20
* *sl2*: Default is equal to ls. On some data, λ/100 works well
