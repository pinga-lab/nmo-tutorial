# The code for NMO

Now I'll show how to implement the above algorithm in Python using the numpy and scipy libraries.
We'll split the algorithm into three functions.
This is very important when programming any moderately complex code because it allows us to test each part of our code independently.
This reduces the amount of code we have to search through to find that bug is messing up our results.
Modular code is also easier to understand and to reuse.

The first function I'll define performs the NMO correction on a given CMP gather.
We'll assume that the CMP gather is a 2D numpy array of amplitudes and that the velocities are a 1D numpy array with \(v_{NMO}\) for each time sample.

    import numpy as np
    from scipy.interpolate import CubicSpline

    def nmo_correction(cmp, dt, offsets, velocities):
        nmo = np.zeros_like(cmp)
        nsamples = cmp.shape[0]
        times = np.arange(0, nsamples*dt, dt)
        for i, t0 in enumerate(times):
            for j, x in enumerate(offsets):
                t = reflection_time(t0, x, velocities[i])
                amplitude = sample_trace(cmp[:, j], t, dt)
                # If the time t is outside of the CMP time range,
                # amplitude will be None.
                if amplitude is not None:
                    nmo[i, j] = amplitude
        return nmo    
        

Now we have to define the function that calculates the reflection travel-time \(t\) and the one that samples the amplitude from the CMP using interpolation.

    def reflection_time(t0, offset, velocity):
        t = np.sqrt(t0**2 + offset**2/velocity**2)
        return t


For the interpolation, we'll use cubic splines from the `scipy.interpolate` package. 
For more information on interpolation with scipy, see the tutorial by \cite{Hall_2016}.

    def sample_trace(trace, time, dt):
        # The floor function will give us the integer
        # right behind a given float.
        before = int(np.floor(time/dt))
        nsamples = trace.size
        # Use the 4 samples around time to interpolate
        samples = np.arange(before - 1, before + 3, 1)
        if np.any(samples < 0) or np.any(samples >= nsamples):
            amplitude = None
        else:
            times = dt*samples
            amps = trace[samples]
            interpolator = CubicSpline(times, amps)
            amplitude = interpolator(time)
        return amplitude


Figure 2 shows the results of applying our `nmo_correction` function to a synthetic CMP. 
The Jupyter notebook has the full code for this application as well all the functions above with documentation in the form of docstrings and tests.