# SLR — Sparse + Low-Rank Kernel Approximation

This project approximates a stationary autocovariance function (ACF) as a sum of a **low-rank** and **sparse** components. More precisely, the former is done via a spectral truncation (i.e., keep a few [DFT](https://en.wikipedia.org/wiki/Discrete_Fourier_transform) bins) and the latter by fitting a sparse kernel (e.g., $\text{MA}(q)$) to the residual.

**Why this helps**
- A significant computational bottleneck in Gaussian Process (GP) applications is the inversion of an $n\times n$ matrix, when we have $n$ data points. A low-rank approximation, say using $r$ Fourier modes, allows us to substantially reduce the computational burden from $O(n^3)$ to $O(nr^2)$ by applying the [Woodbury identity](https://en.wikipedia.org/wiki/Woodbury_matrix_identity).
- Pure spectral truncation "smooths" the time-domain kernel (Fourier uncertainty): sharp small-lag structure is lost. To mitigate this, we additionally fit a sparse kernel on the residual, which plays the opposite role of the truncated DFT (i.e., truncated ACF and smooth DFT) and preserves computational efficiency.


**Repo contents**
- [`slr.ipynb`](slr.ipynb) - end-to-end demo and plots.
- [`dff.pdf`](dff.pdf) - brief note on deterministic Fourier/spectral truncation.