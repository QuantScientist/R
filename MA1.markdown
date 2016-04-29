
An MA(1) process in C++11 & Rcpp.  
For instance: xt = 10 + wt + .7wt-1

Invoke using: 
```R
y =(ma2(10,1500, 0.7, 1))
mean(y)
sd(y)
acf(y,xlim=c(1,10))
```

C++ code: 

```cpp
// [[Rcpp::export]]
NumericVector ma2(double u, int n, double phi, double sigma){
  std::random_device rd;
  std::mt19937 e2(rd());
  std::normal_distribution<> dist(0, sigma);
  
  NumericVector out(n);
  //NumericVector wt(n);
  double wt1;
  double wt2;
  //cores <- parallel::detectCores();
  wt1=dist(e2);
  wt2=dist(e2);
  for(int i = 0; i < n; i++) {
    out[i] = u + wt2+ phi*wt1;
    wt1=wt2;
    wt2=dist(e2);
  }
  return out;
}
```

