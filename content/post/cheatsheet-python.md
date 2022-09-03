+++
title = "Cheatsheet Python"
date = 2022-08-30T21:05:31-04:00
lastmod = 2022-08-30T21:05:31-04:00
tags = []
categories = []
imgs = []
cover = ""  # image show on top
readingTime = true  # show reading time after article date
toc = true
comments = false
justify = false  # text-align: justify;
single = false  # display as a single page, hide navigation on bottom, like as about page.
license = ""  # CC License
draft = true
+++

# Conda
#### Create env
    conda create --name jupyter #python=3.5 numpy
#### Activate 
    conda activate jupyter
#### Envs list 
    conda info --envs
<!-- more -->

# Numpy 
{{<highlight python>}}
# Return evenly spaced values within a given interval. 
my_list = np.arange(0,10) 
# Return evenly spaced numbers over a specified interval.
np.array(my_list)
my_list = np.linspace(0,10,3)

arr_2d = np.random.rand(5,5)
arr_2d[arr_2d>2]
{{</highlight>}}

# Pandas 
