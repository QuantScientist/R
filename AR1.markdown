An AR(1) Process. 
An n-length realization from an AR(1) process with parameter phi, 
starting from start and having a white noise error with standard deviation equal to sigma.

Invoke using: 
```R
y =(arc2(0,10, 0.5, 1))
y
mean(y)
sd(y)
```

C++ code: 

```cpp
// [[Rcpp::export]]
NumericVector arc2(double start, int n, double phi, double sigma){
  std::random_device rd;
  std::mt19937 e2(rd());
  std::normal_distribution<> dist(0, sigma);
  NumericVector out(n);
  out[0]=start;
  for(int i = 1; i < n; i++) {
    out[i] = phi*out[i-1]+dist(e2);
  }
  return out;
}
```
