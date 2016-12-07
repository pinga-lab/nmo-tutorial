# Putting my code where my mouth is

Now I'll show how to implement the above algorithm in Python using the numpy and scipy libraries.
We'll split the algorithm into three functions.
This is very important when programming any moderately complex code because it allows us to test each part of our code independently.
This reduces the amount of code we have to search through to find that bug is messing up our results.
Modular code is also easier to understand and to reuse.

The first function I'll define performs the NMO correction on a given CMP gather.
We'll assume that the CMP gather is a 2D numpy array of amplitudes and that the velocities are a 1D numpy array with \(v_{NMO}\) for each time sample.

    def nmo_correction(cmp, dt, offsets, velocities):
        

Next,

    def reflection_time(t0, offset, velocity):

    def sample_trace(trace, time, dt):


Figure: (a) CMP, (b) velocity profile, (c) NMO. Maybe include lines in the NMO with the true two-way travel time.
