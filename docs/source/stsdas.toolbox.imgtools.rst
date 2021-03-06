:orphan:


stsdas.toolbox.imgtools
=======================

Tasks for performing operations on images and masks.

Notes
-----

**For questions or comments please see** `our github
page <https://github.com/spacetelescope/stak>`__. **We encourage and
appreciate user feedback.**

**Most of these notebooks rely on basic knowledge of the Astropy FITS
I/O module. If you are unfamiliar with this module please see the**
`Astropy FITS I/O user
documentation <http://docs.astropy.org/en/stable/io/fits/>`__ **before
using this documentation**.

The various image tasks found in the stsdas.toolbox.imgtools package
have been replaced in the `Numpy <https://docs.scipy.org/doc/numpy/>`__
and `Astropy <http://docs.astropy.org/en/stable/>`__ libraries.

Contents:

-  `addmasks <#addmasks>`__
-  `iminsert <#iminsert>`__
-  `improject <#improject>`__
-  `mkgauss <#mkgauss>`__
-  `pixlocate <#pixlocate>`__
-  `rd2xy-xy2rd <#rd2xy-xy2rd>`__





addmasks
--------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

Addmasks is used to combine several masks or bad pixel lists. We can do
this using the ``numpy`` bitwise tasks:
`bitwise\_or <https://docs.scipy.org/doc/numpy/reference/generated/numpy.bitwise_or.html>`__,
`bitwise\_and <https://docs.scipy.org/doc/numpy/reference/generated/numpy.bitwise_and.html>`__,
and
`invert <https://docs.scipy.org/doc/numpy/reference/generated/numpy.invert.html>`__,
along with a slew of `other numpy bit
functions <https://docs.scipy.org/doc/numpy/reference/routines.bitwise.html>`__.
Below we show examples of ``bitwise_and`` and ``bitwise_or``.

.. code:: ipython3

    # Standard Imports
    import numpy as np

.. code:: ipython3

    a = np.array([1,4,10])
    b = np.array([1,0,8])
    
    # OR
    print(np.bitwise_or(a,b))
    
    # AND
    print(np.bitwise_and(a,b))


.. parsed-literal::

    [ 1  4 10]
    [1 0 8]




iminsert
--------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

Iminsert is used to insert a small image into a larger image. This is
easy to do with the Numpy array indexing after you've read in your
images with ``Astropy.io.fits``. Below we'll show a quick array example.

.. code:: ipython3

    # Standard Imports
    import numpy as np

.. code:: ipython3

    # generate test arrays
    my_array = np.random.rand(7,5)
    ones = np.array(([1,1],[1,1]))
    
    # replace middle 3x3 square with ones
    my_array[2:4,2:4] = ones
    
    # Print result
    print(my_array)


.. parsed-literal::

    [[ 0.06888833  0.15088263  0.00241     0.09282496  0.07325408]
     [ 0.78665832  0.3402431   0.5265134   0.46253075  0.54305974]
     [ 0.63473001  0.92986634  1.          1.          0.0904689 ]
     [ 0.2887482   0.50178461  1.          1.          0.78550679]
     [ 0.07945175  0.12885675  0.06588469  0.63534732  0.62024358]
     [ 0.53344071  0.2852475   0.03736071  0.30043438  0.97523821]
     [ 0.10331126  0.52996828  0.51318396  0.47988347  0.7098808 ]]




improject
---------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

Improject is used to sum or average an image along one axis. This can be
accomplised using the
`numpy.average <https://docs.scipy.org/doc/numpy/reference/generated/numpy.average.html>`__
or the
`numpy.sum <https://docs.scipy.org/doc/numpy/reference/generated/numpy.sum.html>`__
functions and choosing which dimensions you wish to collapse. Below we
show an example using ``numpy.average``.

.. code:: ipython3

    # Standard Imports
    import numpy as np

.. code:: ipython3

    # build random test array
    my_array = np.random.rand(5,4,3)
    
    # reduce third dimension down
    new_array = np.average(my_array, axis=2)
    print(new_array.shape)
    print(new_array)
    
    # reduce second dimension down
    new_array_2 = np.average(my_array, axis=1)
    print(new_array_2.shape)
    print(new_array_2)


.. parsed-literal::

    (5, 4)
    [[ 0.60660306  0.55628564  0.79297796  0.73016308]
     [ 0.48911929  0.36071454  0.6167648   0.4261005 ]
     [ 0.47187441  0.21748297  0.92223167  0.64068855]
     [ 0.14900289  0.70091688  0.51759779  0.29799824]
     [ 0.85235487  0.79360714  0.60374945  0.40032384]]
    (5, 3)
    [[ 0.70389997  0.59038403  0.72023831]
     [ 0.4937127   0.44684555  0.47896609]
     [ 0.43435416  0.5368765   0.71797754]
     [ 0.45942245  0.4114324   0.37828199]
     [ 0.64567646  0.51639255  0.82545747]]




mkgauss
-------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

The mkgauss funtionality has been replicated in the Photutils package
with
`photutils.datasets.make\_random\_gaussians\_table <http://photutils.readthedocs.io/en/stable/api/photutils.datasets.make_random_gaussians_table.html#photutils.datasets.make_random_gaussians_table>`__
and
`photutils.datasets.make\_gaussian\_sources\_image <http://photutils.readthedocs.io/en/stable/api/photutils.datasets.make_gaussian_sources_image.html#photutils.datasets.make_gaussian_sources_image>`__.



pixlocate
---------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

Pixlocate is used to print positions matching a certain value condition.
This is replicated with the ``numpy.where`` function. Please see the
`documentation <(https://docs.scipy.org/doc/numpy/reference/generated/numpy.where.html)>`__
for more details and examples.



rd2xy-xy2rd
-----------

**Please review the** `Notes <#notes>`__ **section above before running
any examples in this notebook**

Rd2xy and xy2rd are used to translate RA/Dec to the pixel coordinate and
vice-versa. This capability is well covered in the ``astropy.wcs``
package. Please see the
`documentation <http://docs.astropy.org/en/stable/wcs/>`__ for more
details on usage.





Not Replacing
-------------

-  boxinterp - Fill areas with smoothed values from surrounding area.
   See **images.imfit** notebook.
-  countfiles - Count how many files are in the input file template.
   Deprecated.
-  gcombine - Combine a set of GEIS images into one image. Deprecated,
   for FITS see **stsdas.toolbox.imgtools.mstools.mscombine**
-  gcopy - Generic multi-group copy utility. GEIS, deprecated.
-  gstatistics - Compute and print image pixel statistics for all
   groups. GEIS, deprecated. For FITS see **images.imutil.imstatistics**
-  imcalc - Perform general arithmetic operations on images. See
   **images.imtuil.imarith**.
-  imfill - Set fill value in image according to a mask. See
   **images.imutil.imreplace**.
-  listarea - Print an area of an image. See `numpy basics
   documentation <https://docs.scipy.org/doc/numpy-dev/user/quickstart.html>`__.
-  moveheader - Combine the header and pixels from two images. GEIS,
   deprecated.
-  pickfile - Get the file name picked from the input file template.
   Deprecated.
-  pixedit - Screen editor for image pixels. See **images.tv.imedit**
-  rbinary - Create an image from a binary file. Deprecated.
-  stack - Stack images to form a new image with one more dimension. See
   **images.imutil.imstack**
-  xyztable - Interpolate table values, writing results to a table. See
   **images.imfit.imsurfit** and **tables.ttools.tcopy-tdump**
-  xyztoim - Interpolate table values, writing results to an image. See
   **images.imfit.imsurfit**, `Astropy Tables
   documentation <http://docs.astropy.org/en/stable/table/>`__, and
   **tables.ttools.tcopy-tdump**.
