# Regression

```
AMZN <- read.csv("amzn.us.txt")
FB <- read.csv("fb.us.txt")
```

```
AMZN_idx_s <- which(AMZN$Date == "2017-01-03")
AMZN_end <- nrow(AMZN)

FB_idx_s <- which(FB$Date == "2017-01-03")
FB_end <- nrow(FB)
```
```
x <- AMZN$Close[AMZN_idx_s:AMZN_end]
y <- FB$Close[FB_idx_s:FB_end]
```

```
# Length of x
len <- length(x)

# this is the common denominator
denom <- (len*sum(x %**% 2)-(sum(x))^2)
```

```
# value of a
a <- (len %*% sum(x*y)-(sum(x) %*% sum(y)))/denom
```

```
# value of b
b <- (sum(y)-a*sum(x))/len
```

```
# Yhat is simply aX + b
y_hat <- a*as.vector(x) + b
```
```
plot (x,y,col="red", xlab=substitute(x),ylab=substitute(y))
lines(x,y_hat,type="l", col="blue")
```
