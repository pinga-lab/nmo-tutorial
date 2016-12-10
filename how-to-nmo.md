# Doing it backwards

It's surprisingly difficult to find a description of a method for calculating the amplitudes in the NMO correction.
The only one I could find is a single paragraph in the book by \cite{Yilmaz_2001} (available on the SEG Wiki at [wiki.seg.org/wiki/NMO\_for\_a\_flat\_reflector](http://wiki.seg.org/wiki/NMO_for_a_flat_reflector)):

> "The idea is to find the amplitude value at A' on the NMO-corrected gather from the amplitude value at A on the original CMP gather. Given quantities \(t_0\), \(x\), and \(V_{NMO}\), compute \(t\) from equation (1). [...] The amplitude value at this time can be computed using the amplitudes at the neighboring integer sample values [...] This is done by an interpolation scheme that involves the four samples."

What that paragraph says is that we should actually do it backwards. 
Instead of mapping where each point in the CMP goes in the NMO corrected gather, we should map where each point in the NMO gather comes from in the CMP (see figure 1).
Here is the algorithm:

1. Start with an NMO gather filled with zeros.
2. For each point (\(t_0, x\)) in the NMO gather, do:

* Calculate the reflection travel-time (\(t\)) given \(v_{NMO}\).
* Go to the trace at offset \(x\) in the CMP and find the two samples before and the two samples after time \(t\).
* If \(t\) is greater than the recording time or if it doesn't have two samples after it, skip the next two steps.
* Use the amplitude in these four samples to interpolate the amplitude at time \(t\).
* Copy the interpolated amplitude to the NMO gather at (\(t_0, x\)).

At the end of this algorithm, we will have a fully populated NMO gather with the amplitudes sampled from the CMP. 
Notice that we didn't actually use the equation for \(t_0\).
Instead we calculate the reflection travel-time \(t\).
Good luck guessing that from the equation alone.