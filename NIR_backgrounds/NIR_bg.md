# Infrard sky background photon fluxes

## Useful Links

* [ESO's Paranal sky backgrounds](https://www.eso.org/gen-fac/pubs/astclim/paranal/skybackground/)
which seem to be the most accepted.

* [The E-ELT design reference mission ]()

* [ESO's SkyCalc](https://www.eso.org/observing/etc/bin/gen/form?INS.MODE=swspectr+INS.NAME=SKYCALC)
which is fine for JH, but the K band magnitude seems to be 2 mag weaker than it
should be

* [Reference data ](http://www.astronomy.ohio-state.edu/~martini/usefuldata.html)

## NIR Numbers

Because the MICADO wide field pixel mode uses 4mas pixels and a 978m2 mirror, 
the background flux is ~1.5% that of the nominal per m2 per arcsec2 value. 
(The zoom mode, with 1.5mas pixels contains only ~15% of the background flux in
the wide-field mode, i.e. 0.225% of the general case)

| Filter | [mag/arcsec2] | General [ph/s/m2/arcsec2] | MICADO@E-ELT 4mas [ph/s] |
|----|------|------|----|
| J  | 16.5 | ~700  | ~10 |
| H  | 14.4 | ~5200 | ~80 |
| K  | 13.0 | ~9800 | ~150 |
| Ks | 13.6 | ~5500 | ~85 |

## Using SimCADO to quickly get these numbers

    >>> import simcado as sim
    >>> f =sim.optics.get_filter_curve("Ks")
    >>> q = sim.source.flat_spectrum_sb(mag_per_arcsec=13.6, filter_name="Ks", 
                                        pix_res=0.004, return_ec=True)
    >>> 978 * (q*f).photons_in_range()
    86.132765881857338
    
or 

    >>> import simcado as sim
    >>> 0.004**2 * 978 * sim.source.mag_to_photons("Ks", 13.6)
    86.13276588185731

## Check that SimCADO is delivering the correct fluxes
[http://www.astronomy.ohio-state.edu/~martini/usefuldata.html](http://www.astronomy.ohio-state.edu/~martini/usefuldata.html)

    >>> import simcado as sim
    >>> from astropy import units as um
    >>>
    >>> # Data taken from the source above
    >>> a = ((1392.6, 995.5, 702.0, 452.0, 193.1, 93.3, 43.6) * u.Unit("ph cm-2 s-1 Angstrom-1") * \
    ...      (0.09, 0.085, 0.15, 0.15, 0.26, 0.3, 0.41)*u.um).to(u.ph/(u.s*u.m**2)).value
    >>> b = [sim.source.zero_magnitude_photon_flux(i) for i in "BVRIJHK"]
    >>>
    >>> plt.scatter(a, b)
    >>> plt.plot([1E9,1.3E10], [1E9, 1.3E10], "k:")
    >>> [plt.text(x+2E8, y, i, fontsize=14) for x,y,i in zip(a, b,"BVRIJHK")]
    >>> plt.xlabel("Reference Vega photon fluxes [ph/s/m2]")
    >>> plt.ylabel("SimCADO zero_magnitude_photon_flux()")
