# SimCADO Experiments


--------------------------------------------------------
# Observing Star Formation regions in high-z galaxies

Using the NUTFB simulations from Mark Richardson
- A single galaxy with 10pc resolution, 
- simulated at many epochs from z=100 down to z<3
- Cubes containing gas mass, stellar mass, SFR, age
- Cubes are XYZ coordinates, which allows us to project to 2D (flatten) along any  orientation

Observing the galaxy
- From the stellar mass + age, we we can derive an SED for the continuum 
- From the Gas Mass, we use the Kennicut-Schmidt law to derive SFR
- Based on the SFR, we can derive a Balmer series spectrum
- We then "observe" the galaxy using a broad band filter and a narrow band filter 
- To get the continuum, we subtract the NB flux from the BB flux and reduce the BB effective width by the width of the NB filter.


## Questions to answer
- What percentage of the SF can be resolved by MICADO
- What is the minimum mass per SFR for it to be detectable at which z
- How do projection effects play a role? I.e. if several SFR are aligned, do we get disconiuities in the apparent spatial distribution of SF? 
- Disentangle the myth of SFR uncertainties due to AGN emission. 

## Questions about the set-up
- Are the galaxies scalable? I.e. if the emission is too faint, can I just scale everything up?
- Is there a spatial dependence on SF? I.e. does one SF event trigger the next round of SF in the time and spatial domains?
- Is using H-beta and H-gamma a valid idea? Higher balmer lines are weaker, but SF is strong in high-z galaxies.


----------------------------------------------
# Ideas for the paper on IMF predictions

## How deep can the IMF be investigated
Take an IMF and observe it for various distances

http://www.ast.cam.ac.uk/~mike/local_members

Example distances would be
* 8kpc, the galactic centre
* 50 kpc, the magellanic clouds
* 200 kpc, the nearest star forming galaxy
* 770 kpc, Andromeda [**find a target that is in the southern hemisphere**]
* 2100 kpc, NGC 200
* 5000 kpc, M81 - nearest elliptical galaxy

From Sachez 2010 (list of 16 open clusters)
Min = 0.1pc, Max = 3.4pc, average 2+/-1 pc
From Pulenchikov 2007 - average mass 500Msun, 1 sigma goes between 60 Msun and 2800 Msun

From Melnik 1995 (list of 88 OB associations in the MW)
Min 5-10pc, Max 150pc, average ~50+/-25pc


## What objects can be observe at these distances

* Take a 10 Myr open cluster
    * IMF for 10 Myr
        * all stars, any giants? Or `pure` main sqeuence.
        * How far along are the <0.5 Msun stars? Are they visible yet, or are they still obscured?
    * Half light radius will be on the order of 1 pc
        * Should we look at HL radii of 0.25, 1, 4?
    * What extinction do we have to take into account? Towards galactic centre, we will need A_K = 3 mag, outside the galactic plane it's negligible: ~A_K ~ 0.5?
    * What cluster masses are we looking at?
        * 100, 1000, 10000 Msun?

* Take a 100 Myr OB association
    * IMF for 100 Myr,
        * We'll need the giants. Use the Stell Pop Syth website from Eline
        * All the stars are on the MS? Even the Brown dwarves?
    * Half light radius is around 20 pc? Up to 100 pc diameter?
        * Should we look at HL radii of 2.5, 10, 40?
    * What cluster masses are we looking at?
        * 100, 1000, 10000 Msun?

## Conditions for the "observation run"

Really only based on MICADO. The ground work of calibrating SimCADO to HAWKI was done in Paper 1, and we can are using the most up-to-date data for the E-ELT and MICADO

* Atmospheric conditions
    * We assume an Airmass of 1.2 for the atmospheric transmission
    * Atmospheric background brightness for Paranal
* Telescope conditions
    * Use the standard configuration for MICADO
    * Use MCAO PSF for anything that is larger than the inner chip
        * What do we do about Seeing?
        * Assume 0.8" or whatever MAORY has taken?
    * For the systems that don't take up more than the inner chip, we can use the predicted SCAO PSF, as this is good out to 10" from the centre. The inner chip covers +/- 8".
    * We assume a 0.1 emissivity for the whole system
* Instrument conditions
    * We assume perfect ADC and de-rotator
    * We assume only the mirrors that are needed
    * We assume the detector characteristics as given by NG-HxRG
* Observation run conditions
    * DIT to be chosen so that
        * We are background limited
        * All stars below 2Msun are within the detector linear range
        * Maximum observation length is 10 hours

## What is mathematically visible?

How do we define if a star is detectable?

* If the peak of the star is above 5 sigma
* If the integrated flux in an aperture is above 7 sigma
* Set the aperture to take only the 2nd Airy ring?
* Fit a gaussian to the core (i.e. 5x5 pixels)


## What results do we want to produce?

* Completeness graph of detectability for the whole cluster
    * Percentage detected vs magnitude
    * Percentage detected vs Mass
    * Difference between recovered and input flux (i.e. residuals) vs magnitude
    * Detection magitude limit vs distance
* Completeness for different masses at differenet radial distances
* Automatic source detection mis-classifications due to PSF artifacts
    * Relative number of false detections vs magnitude

What single number do we use to define IMF detectability for a cluster?
? The 10%, 50% and 90% recoverability limit? How does that fit with radial variability?
? The mass range over which the recoverability goes from 90% to 10%? (90-50%?) Is it symetrical around 50%?


* IMF plots
    For different levels of cluster stellar density (includes cluster mass and radius)
    * Input IMF (mass vs frequency)
    * Average Recovered IMF (mass vs frequency)

* CMD plots for each distance
    * J-Ks vs J


## Parameter space

What we can change for the simulations
Cluster Mass   (1E2, **1E3**, 1E4) Msun
Cluster Radius (0.3, 1, 3, 10, 30) pc
Cluster Age    (**10**, 100) Myr
Distance       (8.5, 50, 200, 770, 2100, 5000) kpc

Exposure time  (1, **10**) hr
* Lightly dependent variables
    * Mass, Radius, Age

* The results parameter space
    * Recoverability frequency vs Stellar mass vs distance vs radius



** REMEMBER - YOU NEED TO DO EVERYTHING WITH SIMCADO AGAIN **
   So only set up the mechanics. As little human intervention as possible.
    

    Uniform distribution, low density - see what is visible? What is recoverable? Down to what Mass is everything recoverable? For which distance is this?
Step 1:

   90% recovery at Ks=27 for 3 FWHM, 40% recovery for 1 FWHM. This is our completeness limit. Fainter than Ks=27 and the recovery rate for a 1 hour observation is always less than 90%. At Ks=28 it is always below 10%

   Ks=27 at 3 FWHM is the "completeness" limit.
    Redo graph for Ks=27 and 3 FWHMs.

Step 1a:
    Work out densities for various scenarios and what the limiting mass would be for differenet densities and distances.

   Start with the high mass stars and work down.
    **Assume that we will have good knowledge of the PSF**
    Develop an IMF function for Chabrier
    Develop a PSF subtraction function, based on the input PSF. See whether we can subtract away stars. What percentage can we still recover? What additional number of sources are found due to artifacts? How "complete" are the lower sigma levels? Start with Starfinder on high sigma, then remove those stars, rerun Starfinder with a lower sigma, then remove those stars.



Step 2:
    Shrink the radius of the cluster. At what average density do we start to lose the lowest mass stars?

Step 3:
    Repeat step 2 for slowly increasing distances
    What Mass is still 100% recoverable?
    Repeat this step for different distances. This graph should follow the sensitivity limit.
    Graph the




-----------------------------------
# Ideas for using reflected light variations from AGB shells to determine distances extremely accurately

AGB stuff

Can we use reflection from shells to get highly accurate distance measurements with the E-ELT

AGB shells are at a distance of 1E4 AU from their host star
At what distance does 50mas correspond to 1E4 AU
1AU is 1 arcsec at 1pc
0.05 arcsec means 0.05 AU at 1 pc
0.05 arcsec means 1E4 AU at 200 kpc

            mag      ph/cm^2/s/A/arcsec^2 W/m^2/Hz/arcsec^2 ergs/s/cm^2/A/arcsec^2
KPNO  B  23.0             9.2e-07           2.68e-32           4.16e-18




---------------------------------------
# PSF-R Experiment with Ric and Roland

Email from Ric

I think it would be very motivating to get some feedback from the science team (hence my other email to you and Renato). And many of them also would be very interested to know how PSF reconstruction is doing. In this context I would like to propose a test.
simple version:
- you simulate a PSF and send it to Kieran who 'observes' it realistically (including subtracting a sky or dark frame). I would suggest an 11mag A-star (i.e. R=11mag, H=11mag), and Kieran should simulate it with the 1.5mas scale and a 1% narrow band filter (so it doesn't saturate) around 1.64um for a 2sec integration. He could do this at several random positions (wrt a pixel centre).
- at the same time, you can reconstruct the PSF at the same wavelength.
- you give your reconstruction to Kieran and ask him to compare it with his observation.
- this would highlight some additional things, like how to best centre the reconstructed PSF with the observed one, how far out one really will be able to measure the PSF halo/wings, how to get the zero-level of the observation, to to scale the reconstruction to match the observation, how to compare them, etc.
- repeat the whole process with a fainter star, say 15mag, which can be observed in 2sec with the 1.5mas scale in the broad-band H filter.
- possibly repeat this faint star experiment but generate 30 2sec-PSFs (each with a time evolved phase screens, so that they are slightly different) and let Kieran use them to generate a 60sec exposure. Then compare this to the averaged reconstruction.

This, I think would provide a strong link to the science team, since they would see something that they can identify with.

If you are feeling adventurous, I would then propose a blind test. Basically do the same thing, but Yann do the AO simulations (which might include a different subset of ELT features & effects than you do) and send the PSF to Kieran and the WFS/DM data to Roland...





------------------------------------------
Dark Matter
- Velocity dispersion of halo stars?
- Velocity dispersion of in dwarf galaxies
- Lensing
- Intermediate black hole cases?