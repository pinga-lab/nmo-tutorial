Open any text book about seismic data processing and you will inevitably find a section about the Normal Moveout (NMO) correction. 
There you'll see that we can correct the measured travel-time of a reflected wave (\(t\)) at a given offset (\(x\)) to obtain the travel-time at normal incidence (\(t_0\)) by applying the following equation (or something derived from it)

$$ t_0^2 = t^2 - \dfrac{x^2}{v_{NMO}^2} $$



in which \(v_{NMO}\) is the NMO velocity.

When applied to a Common Mid Point (CMP) section, equation 1 is supposed to turn the hyperbola associated with a reflection into a straight horizontal line, like we see in figure 1.
What most text books won't tell you is *how, exactly, do you apply this equation to the data*?

Read on and I'll explain step-by-step how the algorithm for NMO correction from \cite{Yilmaz_2001} works and how to implement it in Python.
The accompanying Jupyter notebook \cite{Perez_2007}contains the full source code as well as an interactive example of velocity analysis.
You can download the notebook at [github.com/seg](https://github.com/seg) or find links to run it online at [github.com/pinga-lab/nmo-tutorial](https://github.com/pinga-lab/nmo-tutorial).