# Kieran's Astronomy Page

Here's where I keep little bits of information and calculations that I've 
already looked up or calcluates thousands of times before.

## Infrard sky background photon fluxes

### Useful Links

* [ESO's Paranal sky backgrounds](https://www.eso.org/gen-fac/pubs/astclim/paranal/skybackground/)
which seem to be the most accepted.

* [The E-ELT design reference mission ]()

* [ESO's SkyCalc](https://www.eso.org/observing/etc/bin/gen/form?INS.MODE=swspectr+INS.NAME=SKYCALC)
which is fine for JH, but the K band magnitude seems to be 2 mag weaker than it
should be

### NIR Numbers

Because the MICADO wide field pixel mode uses 4mas pixels and a 978m2 mirror, 
the background flux is ~1.5% that of the nominal per m2 per arcsec2 value.

| Filter | [mag/arcsec2] | General [ph/s/m2/arcsec2] | MICADO@E-ELT 4mas [ph/s] |
|----|------|------|----|
| J  | 16.5 | ~700  | ~10 |
| H  | 14.4 | ~5200 | ~80 |
| K  | 13.0 | ~9800 | ~150 |
| Ks | 13.6 | ~5500 | ~85 |

### Using SimCADO to quickly get these numbers

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

