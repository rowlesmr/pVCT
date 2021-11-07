=====
Usage
=====

To use pvct in a project::

	import pvct

or, more likely, to run as a command-line program with arguments::

	pvct lam mono B abs formula min max [-f... | -D]


This program is used to creat a pseudo-variable-count-time (pVCT) diffraction pattern from many fixed-count-time (FCT)
diffraction patterns.

To do so, information must be given to the program to calculate the way in which to sum the given diffraction data.
Compulsory information is:
* ``lam``: (float) wavelength in A or energy in keV.
* ``mono``: (float) monochromator angle in deg 2Th (0 for none, 90 for synchrotron).
* ``B``: (float) average temperature factor (0.5 is a good start).
* ``abs``: (float) capillary absorption in mu*R or incident angle for fixed-incident-beam. (0 for no correction).
* ``formula``: (string) Chemical formula --> \"La 1 B 6\" of \"Fe 1\".
* ``min``: (float) angle of first peak in deg 2Th.
* ``max``: (float) maximum angle in deg 2Th.
  
You must also give one of the following options:
* --filenames: (string) list of file names - XY or XYE format. Wildcards accepted eg *.xy, la?.xy
* -D: (int) number of diffraction patterns to simulate.

One suggested workflow is to run ``pvct`` in simulation mode using the known experimental parameters with :math:`D\\approx`$ 20. An FCT diffraction pattern is then collected to assess both the factor, :math:`D`, by which the intensities at that position must be increased to match the intensities of the low angle peaks, and the required collection time to give adequate intensities for the low angle peaks. :math:`D` FCT diffraction patterns are collected, and ``pvct`` is then used to create a pVCT diffraction pattern. 

Two examples of valid invocations of ``pvct`` are ::

	pvct 0.7093 0 0.5 7 "La 1 B 6" 13 -1 -f *.xy
	pvct 16.5 90 0.3 0.9 "Mg 1.8 Fe 0.2 Si 1 O 4" 3 165 -D 20

The first will create a pVCT diffraction pattern from all XY files in the directory, using a wavelength of 0.7093 Å, no monochromator correction, an overall thermal parameter of 0.5 Å², an incident angle of 7°, and a specimen composition of :math:`\mathrm{LaB}_6`. The pattern summation calculations are taken with respect to the values at 13° 2θ and are carried out to a maximum angle as defined in the input data. The output files are written to the same directory as the source data.

The second will create a pVCT summary simulation using an energy of 16.5 keV, a monochromator angle of 90°, an overall thermal parameter of 0.3 Å², a capillary absorption of 0.9, and a specimen composition of :math:`\mathrm{Mg_{1.8}Fe_{0.2}SiO_4}` over the range 3 -- 165° 2θ, assuming 20 diffraction patterns.

If the program is run with no command-line arguments, a minimalist GUI is launched to enable the user to enter the same information.