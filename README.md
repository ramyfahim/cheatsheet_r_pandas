# Cheatsheet for using R and the Python library Pandas


Many people know how to use Pandas but not R or the other way around. And the Internet is lacking in resources that provide a side-by-side comparison of the two scripting languages. This cheatsheet will address this issue and be of help if you know one but not the other (or neither) of these languages. You will see how these things work and we will focus on data wrangling.


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


### Get information about the dataset.


#### R

```
dim(iris)

nrow(iris)
ncol(iris)

summary(iris) #shows min, max quartiles, mean of columns

head(iris)

tail(iris)

colnames(iris)

```

1. Getting the dimensions of the dataset
2. Viewing summary statistics on the columns
3. Viewing the first and last rows of the dataset
4. Returning the column names of the dataset

#### Pandas

```
df.shape

df.describe() #shows min, max, quartiles, mean, standard deviation, and counts of columns

df.head()

df.tail()

df.columns

```

1. Getting the dimensions of the dataset
2. Viewing summary statistics on the columns. The pandas summary function gives some more information here.
3. Viewing the first and last rows of the dataset
4. Returning the column names of the dataset


### Select elements and use for loops to do a data transformation.


#### R

```
iris[1, 1]

iris$Sepal.Length[1]

iris$Sepal.Length

for (i in 1:nrow(iris)){
  iris$Sepal.Length[i] <- iris$Sepal.Length[i] + 100
}

```

Get the element in the first row and first column by index. In R indices start at 1, not 0.
Then get the same element by specifying the column name and the index.
Then return the entire column.

Run a for loop to go through each row of the dataset, and in the sepal length column, add 100 to every element.

#### Pandas

```
df.iloc[0, 0]

df.loc[0, 'sepal length (cm)']
df['sepal length (cm)'][0]

df.loc[:, 'sepal length (cm)']
df['sepal length (cm)']

for i in range(0, df.shape[0]):
    df['sepal length (cm)'][i] += 100

```

Get the element in the first row and first column by index. In Pandas, as in regular Python, indexing starts at 0.
Then get the same element by specifying the column name and the index.
Then return the entire column.

Run a for loop to go through each row of the dataset, and in the sepal length column, add 100 to every element.
