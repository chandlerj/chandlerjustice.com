---
title: "How I Created Instant Rice, An Automatic Theming Tool"
date: 2024-03-13T18:02:40-06:00
draft: false 
---

The amount of customization available on a Linux desktop absolutely scratches my OCD. I sometimes find myself spending hours tweaking
every aspect of the system I can. Every program that dropped a file in my `.config` folder was a new present, where I could dive in
and change every last variable of a configuration value. Beyond scratching an itch, tweaking a program's config file is a great way
to learn how that program works and how to use that program.

Eventually I realized my process for theming programs could be boiled down to:
 - Find a wallpaper I like
 - Pull out a color picker and find colors 
 I liked from the image
 - Use those colors as a palette and go through every
 configuration file replacing the colors throughout
 the configuration file.

I then remembered that I knew how to code and could automate this process!

## Grabbing the Most Prominent Colors From an Image

The first task I wanted to accomplish with this project was finding a way to find the most common (or popular) colors in an image and then use those as the system color scheme. The algorithm for this looked something like

```Python3
#Python3 (kinda)
def findPopularColors(img, numColors):
    colorvalues = {} # color : occurances
    for pixel in img:
        if pixel.value in colorvalues:
            colorvalues[pixel.value] += 1
        else:
            colorValues[pixel.value] = 1

    # sort the dictionary by number of occurances
    colorValues.sortByValue()
    
    # return number of requested colors
    nPopularcolors = []
    for i in range(numColors):
        nPopularcolors += colorValues[i].key

    return nPopularColors
```

After trying this function on a few different images, I noticed a big issue with this approach. Since we are picking the most popular colors, the algorithms was just giving me slight variations of the same color; this was especially bad with photos that were dark, the algorithm would usually give me back lots of blacks and grays that were not the most prominent colors in the image. For example, the image below would just return various shades of black.  

![photo of a bird](/images/crazybird.jpg)
> Fig (1): An absolutely insane bird

Looking at this image, it is obvious the most commonly occuring colors are various shades of black and gray, which is not going to work for creating a system color scheme. We want to actually pull the colors that "pop out" to us, being the various shades of brown, yellow, and white on the birds feathers. Because of this, we instead need to find a way to pick the most prominent colors and not necessarily the most popular colors.

## Using K-Means Clustering to Get Colors

The K-Means algorithm is a way of finding a defined number of points `n`, that exists in a dataset of `k` elements. As elements are observed they are assigned to one of the points, and the points value is modified to be the mean of all points associated with it.

I tried finding a *scholarly* article that summarizes the math behind
K-Means clustering I could site, but [Wikipedia](https://en.wikipedia.org/wiki/K-means_clustering) ended up having the most digestible explanation. (I changed some syntax to sooth my comp-sci mind)

Given observations 

$$(x_1, x_2, ..., x_n), \quad x_i \in \mathbb{R}^d$$

Partition the elements into sets 

$$S = (S_1, S_2, ..., S_k)$$

and minimize the within-cluster sum of squares

$$arg_s min \sum^{k}_{i=1} \sum_x^{S_i} ||x - \mu_i||^2, \quad \mu_i = \frac{1}{len(S_i)} \sum^{S_i}_x x $$

What this gives us back is the most prominent colors in the image. Here is the code I used to implement the K-means algorithm in Instant Rice

```
#Python3
import cv2 as cv
from sklearn.cluster import KMeans

def grabColors(img_path: str, num_colors: int) -> list():
    img = cv.imread(img_path)
    img = cv.cvtColor(img, cv.COLOR_BGR2RGB)
    
    # scale image down by factor of 10 to decrease computation time
    dim = (int(len(img[0])/10), int(len(img)/10))
    img = cv.resize(img, dim, interpolation= cv.INTER_AREA)
    clt = KMeans(n_clusters=num_colors, n_init='auto')
    clt.fit(img.reshape(-1, 3))
    return clt.cluster_centers_
```

Right now I am kind of cheating by using a package included in `scikit`, but I have not gotten around to implementing the algorithm from scratch. We are still in the MVP phase.

This function gives us exactly what we are looking for! Lets see what colors it gives us back on the image from above.

![the color picker interface on Instant Rice](/images/colorpicker.png)
> Fig (2): The color preview dialogue window for Instant Rice

Much better than various shades of black! The K-means clustering meant that we were able to place the colors in the image into groups and then return the mean color of each group. Right now, I am only grabbing 3 groups from the image, but there is nothing stopping someone from grabbing `n` groups of colors.

In addition to grabbing colors from the image, I wanted to generate some complimentary colors to use for foreground elements. This was easy to achieve after some research on color theory.

```
def compColors(color_list: list) -> list:
    compliments = []
    for color in color_list:
        curr_hex = color[1:] # slice off the # from the hex code
        rgb = (curr_hex[0:2], curr_hex[2:4], curr_hex[4:6])
        comp = ['%02X' % (255 - int(a, 16)) for a in rgb] # magic :D
        compliments.append('#' + ''.join(comp))
    return compliments

```

## Check It Out For Yourself

I have changed a lot with this tool and added several new features since writting this. If you want to see the current state of the tool, check out my [Github repository](https://github.com/chandlerj/InstantRice) to clone the project and try it out, and keep up with devlopment.
