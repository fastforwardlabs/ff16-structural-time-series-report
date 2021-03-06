## What is a structural time series?

Many time series display common characteristics, such as a general
upwards or downwards trend; repeating, and potentially nested, patterns;
or sudden spikes or drops. Structural approaches to time series address
these features explicitly by representing an observed time series as a
combination of components.

![Some time series decompose naturally into component parts.](figures/ff16-02.png)

There are two broad approaches to structural time series. In the first,
a structural time series is treated as a state space model. In this
approach, the values of the time series we observe are generated by
latent space dynamics. This encompasses an enormously broad and flexible
class of models, including the likes of
[ARIMA](https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average)
and the [Kalman filter](https://en.wikipedia.org/wiki/Kalman_filter).
Popular open source packages like
[bsts](https://cran.r-project.org/web/packages/bsts/) (Bayesian
Structural Time Series, in R) and the TensorFlow Probability
[sts](https://www.tensorflow.org/probability/api_docs/python/tfp/sts)
module support the state space model formulation of structural time
series.

![Patterns in time series occur at different scales. Here, a global trend combines with a repeating seasonal pattern, and two impact effects.](figures/ff16-03.png)

In the second approach, structural time series are generalized additive
models (GAMs), where the time series is decomposed into functions that
add together (each of which may itself be the product or sum of multiple
components) to reproduce the original series. This approach casts the
time series problem as curve fitting, which does incur some trade-offs.
On the upside, it renders the model interpretable, easy to debug, and
able to handle missing and irregularly spaced observations. On the other
hand, we are likely to lose some accuracy, as compared to autoregressive
approaches that consider the previous few (or many) data points for each
next prediction. Just as with state space models, GAMs may be treated in
a Bayesian fashion, affording us a posterior distribution of forecasts
that capture uncertainty.

Both approaches have their place. In this report, we'll discuss the
latter. The GAM approach is not universally referred to as a structural
time series (which more often refers to state space models), but here we
take a broader view of the term: a structural time series model is any
model that seeks to decompose time series data into constituent
components---which generalized additive models can be applied to do.
