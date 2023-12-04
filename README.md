# hw-7

Homework 7 in DSCI445: Statistical Machine Learning @ CSU

## Assignment

Be sure to `set.seed(445)`.

1. A researcher collects expression measurements for $1,000$ genes in $100$ tissue samples. The data can be written as a $1,000 \times 100$ matrix, which we call $\boldsymbol X$, in which each row represents a gene and each column represents a tissue sample. Each tissue sample was processed on a different day, and the columns of $\boldsymbol X$ are ordered so that the samples that were processed earliest  are on the left and the samples that were processed later are on the right. The tissue samples belong to two groups: control (C) and treatment (T). The C and T samples were processed in a random order across the days. The researcher wished to determine whether each gene's expression measurements differ between the treatment and control.

    As a pre-analysis (before comparing T and C), the researcher performs a principal component analysis of the data and finds that the first principal component (a vector of length $100$) has strong linear trend from left to right and explains $10$% of the variation. The researcher now remembers that each patient sample was run on one of two machines, A and B, and machine A was used more often in the earlier times with B was used more often later. The researcher has a record of which sample was run on which machine.
    
    a) Explain what it means that the first principal component "explains 10% of the variation".
    
    b) The researcher decides to replace the $(j, i)$th element of $\boldsymbol X$ with
        $$
        x_{ji} - \phi_{j1} z_{i1}
        $$
        where $z_{i1}$ is the $i$th score and $\phi_{j1}$ is the $j$th loading, for the first principal component (performed on $\boldsymbol X^\top$. They will then perform a two-sample $t$-test on each gene in this new data to determine whether its expression differs between the two conditions. Critique this idea and suggest a better approach.
        
    c) Design a run a small simulation experiment (generate your own data) to determine the superiority of your idea.
        
    
2. $K$-means clustering is a simple and elegant approach for partitioning a data set into $K$ distinct, non-overlapping clusters. To perform $K$-means clustering, we first specify the number of clusters $K$, and then the $K$-means algorithm assigns each observation to exactly one of the clusters. The clusters are chosen to minimize the total within-cluster variation. As is shown in the lab solution posted on the class website, $K$-means clustering can be accomplished using the `kmeans` function in `R`.

    In this problem you will generate simulated data and then perform PCA and $K$-means clustering on the data. First run the following to obtain the data.

    
    ```r
    library(mvtnorm)
    
    n <- 20
    p <- 10
    x <- rmvnorm(n*3, rep(0, p))
    
    # shift means
    x[seq_len(n), ] <- x[seq_len(n), ] + matrix(rep(runif(p, min = 1, max = 3), n), nrow = n, byrow = TRUE)
    x[seq_len(n) + 2*n, ] <- x[seq_len(n) + 2*n, ] + matrix(rep(runif(p, min = -3, max = -1), n), nrow = n, byrow = TRUE)
    
    # add class labels
    y <- c(rep("-1", n), rep("0", n), rep("1", n))
    ```
    
    a) Perform PCA on the $60$ observations and plot the first two principal comonent score vectors. Use a different color to indicate the observations in each of the true classes (`y`).
    
    b) Perform $K$ means clustering of the observations with $K = 3$. How well do the clusters you obtained in $K$-means clustering compare to the true class labels? (**Hint:** `table()` may be useful here.)
    
    c) Perform $K$ means clustering of the observations with $K = 2$.  Describe your results.
    
    d) Perform $K$ means clustering of the observations with $K = 4$.  Describe your results.
    
    e) Now perform $K$ means clustering with $K = 3$ on the first two principal components rather than the raw data. Comment on the results.
    
    f) Using the `scale()` function, perform $K$ means clustering with $K = 3$ on the data *after scaling each variable to have standard deviation one*. How do these results compare to those obtained in b)-e)?

Turn in in a pdf of your homework to canvas using the provided Rmd file as a template. Your Rmd file on the server will also be used in grading, so be sure they are identical.

**Be sure to share your server project with the instructor and grader. You only need to do this once per semester.**

1. Open your `homeworks` project on liberator.stat.colostate.edu
2. Click the drop down on the project (top right side) > Share Project...
    
    <div class="figure">
    <img src="share_project.png" alt="plot of chunk unnamed-chunk-2" width="25%" />
    <p class="caption">plot of chunk unnamed-chunk-2</p>
    </div>
  
3. Click the drop down and add "dsci445instructors" to your project.

    <div class="figure">
    <img src="share_dropdown.png" alt="plot of chunk unnamed-chunk-3" width="25%" />
    <p class="caption">plot of chunk unnamed-chunk-3</p>
    </div>

This is how you **receive points** for reproducibility on your homework!
