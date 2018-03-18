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


### Filtering by row values (subsetting), selecting by columns (slicing), creating columns, and renaming columns.


#### R

```
library(dplyr)

filter(iris, Sepal.Length == 105)
iris[iris$Sepal.Length == 105,]

select(iris, Sepal.Length, Petal.Length)
iris[, c('Sepal.Length', 'Petal.Length')]

iris <- mutate(iris, newcol = Sepal.Length + Sepal.Width)

iris <- mutate(iris, newcol2 = 1)

colnames(iris)[colnames(iris) == 'newcol'] <- 'new_name'

```

This requires importing the data manipulation library dplyr. When libraries are imported in R, their functions can be used without referencing the library, as in filter(iris, Sepal.Length == 105). Filter, select, and mutate are all dplyr functions.

Filter rows whose sepal length is equal to 105.

Select only the columns listed.

Create a new column that consists of the sum of sepal length and sepal width, and save it to the R data frame.

Create a new column that consists of only the number 1, and save it to the R data frame.

Rename newcol to new_name.


#### Pandas

```
df.loc[df['sepal length (cm)'] == 105]

df[['sepal length (cm)', 'petal length (cm)']]
df.loc[:, ['sepal length (cm)', 'petal length (cm)']]

df['newcol'] = df['sepal length (cm)'] + df['sepal width (cm)']

df['newcol2'] = 1

df.rename(columns={'newcol':'new_name'}, inplace=True)

```


Filter rows whose sepal length is equal to 105.

Select only the columns listed.

Create a new column that consists of the sum of sepal length and sepal width, and save it to the Pandas dataframe.

Create a new column that consists of only the number 1, and save it to the Pandas dataframe.

Rename newcol to new_name.

### R only: piping.


#### R

```
iris %>% select(Sepal.Length, Petal.Length) %>% head()

```

The piping operator %>% takes the output of the operations on the left and pipes it to the next function on the right until it reaches the end. This is useful when running many functions contained within one another. It makes the code cleaner.



### Ordering.


#### R

```
arrange(iris, Petal.Width)

```

Return the dataframe sorted by values in Pedal Width.
Arrange is a dplyr function.


#### Pandas

```
df.sort_values('petal width (cm)')

```

Return the data frame sorted by values in Pedal Width.


### Group by and summarizing.


#### R

```
iris %>% summarise(sepal_length = mean(Sepal.Length))

group_by(iris, Species) %>% summarise(sepal_length = mean(Sepal.Length))

```

Get mean of sepal length across entire dataset.

Then get mean of sepal length after grouping by species.


#### Pandas

```
Species = pd.DataFrame(data.target)
df = df.join(Species)
df.rename(columns={0:'Species'}, inplace=True)

df['sepal length (cm)'].mean()

new_df = df.groupby('Species')
new_df['sepal length (cm)'].mean()

```

First load target values and append target column to dataframe, and rename it.

Get mean of sepal length across entire dataset.

Then get mean of sepal length after grouping by species.

