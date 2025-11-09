<!-- This is the markdown template for the final project of the Building AI course, 
created by Reaktor Innovations and University of Helsinki. 
Copy the template, paste it to your GitHub README and edit! -->

# Apartment price predictor

Final project for the Building AI course

## Summary

Using linear regression model, optimized by the least squares method, to predict apartments' debt-free prices anywhere in Finland using publicly available data.

## Background

The solution helps people predict an apartment's current price anywhere in Finland using the publicly available data of a specific region whether a municipality or a city - even areas inside a city.

## How is it used?

This logic of the solution is contained in the Python code main() below. The example training data is based on Helsinki city's South-Haaga region, three room apartments, fetch date 9.11.2025:
```
import numpy as np
from io import StringIO

train_string = '''
67 1959 3 0 2 1 364000
68 2024 2 1 2 1 480000
60 1957 2 0 2 1	325000
72.5 1987 1 0 1 1 265000
72 1970 3 1 2 1 405000
61.4 1959 3 0 2 1 338000
80 2021 2 1 2 0 386000
65 1958 3 0 0 1 303000
66 1959 2 0 2 1 338000
75 1958 3 0 1 1 375000
63 1960 2 0 1 1 255000
73 1953 1 0 1 1 369000
80 1960 1 0 2 1	400000
69 1955	3 0 2 1 358000
61 1966	1 0 2 1	295000
68 1967	1 1 2 1	370000
72 1959	3 0 2 1	390300
62.5 1959 2 0 2	1 360000
67 1939	1 0 2 1	384000
72 1970	2 1 2 1	186000
70 1962	2 1 2 1	376000
60 1963	1 1 2 0	321500
64.5 1984 3 0 1	1 299000
68 1962	1 0 1 1	280000
'''

test_string = '''
74 1956 4 0 2 1 420000
68 1970 4 0 2 1 420000
'''

def main():
    np.set_printoptions(precision=1)    # this just changes the output settings for easier reading
    
    # read in the training data and separate it to x_train and y_train
    train_input_file = StringIO(train_string)
    train_input = np.genfromtxt(train_input_file, skip_header=1)
    num_cols = train_input.shape[1]
    x_train = np.delete(train_input, num_cols - 1, axis=1)
    y_train = train_input[:, -1]

    # fit a linear regression model to the data and get the coefficients
    c = np.linalg.lstsq(x_train, y_train)[0] # estimated coefficients #c = np.asarray([])

    # read in the test data and separate x_test from it
    test_input_file = StringIO(test_string)
    test_input = np.genfromtxt(test_input_file, skip_header=1)
    
    num_cols = test_input.shape[1]
    x_test = np.delete(test_input, num_cols - 1, axis=1)
    y_test = test_input[:, -1]

    # this will print out the predicted prices for the apartments in the test data set
    print(x_test @ c)

main()
```

## Data sources and AI methods

The training data comes from aparments sold in the last 12 months in Finland. Below is a link to the data used in the code example above:
[Asuntojen hintatiedot](https://asuntojen.hintatiedot.fi/haku/?c=Helsinki&renderType=renderTypeTable&cr=1&ps=00320&renderType=renderTypeTable&h=1&r=3&amin=60.0&amax=80.0&l=2&search=1&sf=3&so=d)

Input: Size in square meters, Year when built, Floor number, Has an elevator, Apartment condition, Property is owned by the building.

Output: Price in euros without debt.

## Challenges

The training data contains only apartments sold in the last 12 months and only by real estate companies (not individuals). Inputs like "Has an elevator", "Apartment condition" and "Property is owned by the building" are not so simple to present in numerical format unlike "Size in square meters" and "Year when built". 

Due to these facts, and probably many others that I don't even consider here, the model's accuracy could be improved in the future.

## What next?

The app could fetch data via REST API from the public source and offer an UI to input filters used in the API call and input the test data. The app could be deployed in the cloud. 

## Acknowledgments

Publicly available data sources in Finland such as:

* Asuntojen hintatiedot (Ministry of the Environment + KVKL) — transaction-level, last 12 months
* Statistics Finland (StatFin) PxWeb – “Prices of dwellings in housing companies” — downloadable stats, long time series
* Helsinki Region Infoshare (HRI) — city open data hub
* National Land Survey (Maanmittauslaitos) – Real Estate Price Register.
