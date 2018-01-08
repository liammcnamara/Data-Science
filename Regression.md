# Regression


### Import data

The data used in this example is from US Stock market. The complete dataset can be obtained from (here)[https://www.kaggle.com/borismarjanovic/price-volume-data-for-all-us-stocks-etfs].

Within this data set are price histories for *Amazon* and *Facebook*, these can be imported into R using *read.csv()* function which will read in delimited files.
```
AMZN <- read.csv("amzn.us.txt")
FB <- read.csv("fb.us.txt")
```

Let's consider the previous year's *(2017)* price history for *AMZN* and *FB*. The *which()* will determine the index in the matrix where trading begins for 2017.
```
AMZN_idx_s <- which(AMZN$Date == "2017-01-03")
AMZN_end <- nrow(AMZN)

FB_idx_s <- which(FB$Date == "2017-01-03")
FB_end <- nrow(FB)
```
Using the indexes above, lets retrieve 2017's price close history for *AMZN* and *FB*. Let's define these two dataset's 
```
x <- AMZN$Close[AMZN_idx_s:AMZN_end]
y <- FB$Close[FB_idx_s:FB_end]
```

Let's setup a couple of variables that might be useful, *len* is the length of *x* and *denom* is a denominator that's going to be used.
```
# Length of x
len <- length(x)

# this is a denominator
denom <- (len*sum(x %**% 2)-(sum(x))^2)
```

Calculate least squares estimates *a* and *b*. Some literature may refer to these as \beta<sub>i</sub>.
```
# value of a
a <- (len %*% sum(x*y)-(sum(x) %*% sum(y)))/denom

# value of b
b <- (sum(y)-a*sum(x))/len
```

```
# Yhat is simply aX + b
y_hat <- a*as.vector(x) + b
```
```
plot (x,y,col="green")
lines(x,y_hat,type="l", col="black")
```
