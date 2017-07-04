Converting between photon and energy fluxes
-------------------------------------------

Most things are given in Energy density - i.e. erg/s/m2/Angstrom

The thing is to remember that energy density is the amount of energy at a given wavelength per bin:

    Flux(E) = Energy(lambda) per bin (per time per area)
    
There should be an invisible dlambda sitting at the end to remind us of this. 

**Again - Energy Flux is a funciton of energy, which in turn is a function of wavelength**
    
Hence the units of **erg/.../Angstrom**

When we want to convert to photons, we use the photon-energy formula:

    E(ph) = h*f = h*(c/lambda) = h*c/lambda
    
We then divide the energy-flux, F(E), by the photon-energy, E(ph), to get the photon-flux, F(ph)

    F(ph) = F(E) / E(ph) = lambda * F(E) / (h*c)
    
This leaves us with the photons per bin (i.e. per dlambda) where lambda here is the central wavelength of the bin
    
The units of photon flux are **ph/s/m2** for a given bin.

If we want the number of photons coming through a filter, we must integrate over the bin to get rid of that invisible dlambda. In most cases, it surfices to just multiple by the effective filter width (fwhm). For the K band this is ~0.35um

Thus to calculate the integrated filter photon flux we use this formula:

    N(ph) = integrate( F(E) * lambda / (h*c) ) over dlambda
    
Or, if we assume a constant Energy-Flux over the filter range:
    
    N(ph) = F(E) * lambda / (h*c) * filter_width

For a K=0 star where the energy flux is given as 3.94e-11 erg/s/cm2/Angstrom for the central wavelength 2.2um, the photon flux through the 0.35um wide K-filter would be: ~1.53E9 ph/s/m2.

A quick python script which does the same:
    

    import astropy.units as u
    import astropy.constants as c

    K_zero_mag = 3.94e-11 * u.Unit("erg/s/cm2/Angstrom")
    K_centre = 2.2 * u.um
    K_width = 0.35 * u.um

    K_ph = K_zero_mag * (K_centre / (c.c * c.h)) * K_width
    K_ph.si
    
**Note** Don't forget that the Energy flux is wavelength dependent - hence the /Angstrom in the units! This Angstrom is not due to the bin width or filter width, but due to the fact than an instantateous energy flux is dependent on the wavelength