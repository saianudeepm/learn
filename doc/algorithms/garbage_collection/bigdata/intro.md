
## Sketching / Streaming

* Sketch: A sketch c(x) w.r.t some function f allows computing/approximating f(x) given access to only c(x).
Some times f has two args, and you want f(x,y) given c(x) and c(y).

* Streaming: We want to maintain sketch c(x) on the fly as x is updated. (eg: Running sum)

eg: sketch network traffic to query for traffic patterns/ anamoly detection/ compare traffic patterns etc


## Dimensionality Reduction:

*Idea:* If we have a high dimensional data, transform the data into a low dimensional version such that what ever computation
problem you are considering, if you solve that problem on low dimensional transformed data, you can lift that solution to 
original data.

* Point is since data is low dimensional, we can run our algorithms faster on this low dimensional data.

*Applications:*
* Speed up clustering algorithms
* Nearest neighbour search in high dimensions

```
eg: Images are high dimensional vectors. 
Every pixel in img => is a dimension
Value of pixel => intensity of the pixel
If we have a database of images and want to locate/query for a similar image we have (to auto tag pics on FB etc)
```

