<!-- This is the markdown template for the final project of the Building AI course, 
created by Reaktor Innovations and University of Helsinki. 
Copy the template, paste it to your GitHub README and edit! -->

# Helsinki South-Haaga apartment price predictor

Final project for the Building AI course

## Summary

Describe briefly in 2-3 sentences what your project is about. About 250 characters is a nice length! 


## Background

Which problems does your idea solve? How common or frequent is this problem? What is your personal motivation? Why is this topic important or interesting?

This is how you make a list, if you need one:
* problem 1
* problem 2
* etc.


## How is it used?

Describe the process of using the solution. In what kind situations is the solution needed (environment, time, etc.)? Who are the users, what kinds of needs should be taken into account?

Images will make your README look nice!
Once you upload an image to your repository, you can link link to it like this (replace the URL with file path, if you've uploaded an image to Github.)
![Cat](https://upload.wikimedia.org/wikipedia/commons/5/5e/Sleeping_cat_on_her_back.jpg)

If you need to resize images, you have to use an HTML tag, like this:
<img src="https://upload.wikimedia.org/wikipedia/commons/5/5e/Sleeping_cat_on_her_back.jpg" width="300">

This is how you create code examples:
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

    # print out the linear regression coefficients
    print(c)

    # this will print out the predicted prics for the apartments in the test data set
    print(x_test @ c)

main()
```


## Data sources and AI methods
Where does your data come from? Do you collect it yourself or do you use data collected by someone else?
If you need to use links, here's an example:
[Twitter API](https://developer.twitter.com/en/docs)

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |

## Challenges

What does your project _not_ solve? Which limitations and ethical considerations should be taken into account when deploying a solution like this?

## What next?

How could your project grow and become something even more? What kind of skills, what kind of assistance would you  need to move on? 


## Acknowledgments

* list here the sources of inspiration 
* do not use code, images, data etc. from others without permission
* when you have permission to use other people's materials, always mention the original creator and the open source / Creative Commons licence they've used
  <br>For example: [Sleeping Cat on Her Back by Umberto Salvagnin](https://commons.wikimedia.org/wiki/File:Sleeping_cat_on_her_back.jpg#filelinks) / [CC BY 2.0](https://creativecommons.org/licenses/by/2.0)
* etc
