[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/anikaitchatterjee10/Diffusion-in-autoclave-noble-metal-liners-/HEAD?urlpath=%2Fdoc%2Ftree%2Fserver_out_in.ipynb)



The tool uses 3 diffusion coefficients for each element calculated by 3 methods (Method 1, 2 and 3)

•	Method 1 (Two Scenarios):

o	Scenario A: Used when literature is available. Q and D0 is chosen from the most suitable value according to process conditions

o	Scenario B: Used when literature is not available. Q is calculated via a theoretical estimation using Eq. 4, and D0 is determined through extrapo
lation using MNR (Eq. 6).

•	Method 2:

o	Applicability: Based on the work of Zeng and Bai (2015).

o	Parameters: Q is reported using an ANN (Artificial Neural Network) method, while D0 is found via extrapolation using MNR (Eq. 6).

•	Method 3:

o	Applicability: Also based on Zeng and Bai (2015).

o	Parameters: Q is reported using a Regression method, while D0 continues to be determined via extrapolation using MNR (Eq. 6).


