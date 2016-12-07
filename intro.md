# What the equation doesn't tell us

The equation for \(t_0\) relates travel-times: the one we can measure (\(t\)) and the one we want to know (\(t_0\)).
But looking at figure 1a, we can see that the data in our CMP gather are actually a matrix of *amplitudes* measured as a function of time (\(t\)) and offset.
Our NMO corrected gather will also be a matrix of amplitudes as a function of time (\(t_0\)) and offset.
So what we really have to do transform one matrix of amplitudes into the other.
*But the equation has no amplitudes*!

This is a major divide between the formula we've all seen before and what actually goes on in the software that implements it. 
And most of you probably never thought about it (I certainly hadn't).
So let us bridge this divide.
Next, I'll explain an algorithm that maps the amplitudes in the CMP to amplitudes in an NMO corrected gather.


Figure: A CMP (a) next to an NMO (b). Axis show that time in (b) is t0. Arrow connecting a cell in (a) to a cell in (b). Arrow should go both ways and show respective time conversion equations. Probably better to use travel time curves instead of real data for this.
