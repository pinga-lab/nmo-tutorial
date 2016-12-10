# Putting my code where my mouth is

Now I'll show how to implement the above algorithm in Python using the numpy and scipy libraries.
We'll split the algorithm into three functions.
This is very important when programming any moderately complex code because it allows us to test each part of our code independently.
This reduces the amount of code we have to search through to find that bug is messing up our results.
Modular code is also easier to understand and to reuse.

The first function I'll define performs the NMO correction on a given CMP gather.
We'll assume that the CMP gather is a 2D numpy array of amplitudes and that the velocities are a 1D numpy array with \(v_{NMO}\) for each time sample.

    import numpy as np
    import scipy.interpolate

    def nmo_correction(cmp, dt, offsets, velocities):
        

Now we have to define the function that calculates the reflection travel-time \(t\) and the one that samples the amplitude from the CMP using interpolation.

    def reflection_time(t0, offset, velocity):


For the interpolation, we'll use cubic splines from the `scipy.interpolate` package. 
For more information on interpolation with scipy, see the tutorial by \cite{Hall_2016}.

    def sample_trace(trace, time, dt):


Figure 2 shows the results of applying our `nmo_correction` function to a synthetic CMP. 
The Jupyter notebook has the full code for this application as well as an interactive example that uses the `nmo_correction` function for velocity analysis.