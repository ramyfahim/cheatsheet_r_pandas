# Cheatsheet for using R and the Python library Pandas


Many people know how to use Pandas but not R or the other way around. And the Internet is lacking in resources that provide a side-by-side comparison of the two scripting languages. This cheatsheet will address this issue and be of help if you know one but not the other (or neither) of these languages. You will see how things work and we will focus on data wrangling.


### Preliminary: load the data. We will use the famous and simple Iris datset.

#### R

```
library(datasets)

data(iris)
```

Inside the library() function is the library we wish to import.
data(iris) loads the iris dataset and puts it in a dataframe called iris. You can check that it is a dataframe with the command is.data.frame(iris)

#### Pandas

```
from sklearn.datasets import load_iris
import pandas as pd

data = load_iris()

df = pd.DataFrame(data.data, columns=data.feature_names)
```

The imports are done at the top. Then the data is loaded. Finally the appropriate data is transformed into a pandas dataframe. Notice we had to specify the data as well as the column names.
