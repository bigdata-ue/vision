.. _using_modules:

Using modules
=============

To use software modules, the user just need to use the ``module load`` or ``module add`` commands to load the required module. When a module is loaded, all required dependencies will also be loaded, making the software ready for the user.

Vision uses a hierarchical module naming scheme (hmns) in which modules availability follows the software hierarchy Core/Compiler/MPI. Core refers to the basic core modules that have to be loaded in order to have access to next levels of software compiled against a specific compiler and a MPI API.

After logging into Vision, the user should execute the command ``module av`` (av for available) to list the available core modules:

.. code-block:: console

  $ module av

  ------------------------ /opt/software/modules/all/Core ------------------------
     Anaconda3/2021.05         binutils/2.36.1            (D)
     Bison/3.8.2               cuDNN/8.2.1.32-CUDA-11.3.1
     CUDA/11.3.1               flex/2.6.4
     GCC/10.3.0                foss/2021a
     GCCcore/10.2.0            gettext/0.21
     GCCcore/10.3.0    (D)     gompi/2021a
     Java/11.0.2       (11)    ncurses/6.2
     M4/1.4.19                 pkg-config/0.29.2
     OpenSSL/1.1               zlib/1.2.11
     binutils/2.35

    Where:
     Aliases:  Aliases exist: foo/1.2.3 (1.2) means that "module load foo/1.2" will load foo/1.2.3
     D:        Default Module


In the available modules, you can find the toolchains foss/2021a and gompi/2021a, which you can load to access other modules which are built againts each toolchain, e.g.: ``module load foss/2021a``. After loading the toolchain, you can view the associated modules using running again the comman ``module av``:

.. code-block:: console

  $ module load foss/2021a
  $ module av

  ----------- /opt/software/modules/all/MPI/GCC/10.3.0/OpenMPI/4.1.1 -----------
     FFTW/3.3.9                   (L)    h5py/3.2.1
     HDF5/1.10.7                         magma/2.6.1-CUDA-11.3.1
     ScaLAPACK/2.1.0-fb           (L)    matplotlib/3.4.2
     SciPy-bundle/2021.05                scikit-learn/0.24.2
     TensorFlow/2.5.3-CUDA-11.3.1        tensorboard/2.8.0
     TensorFlow/2.6.0-CUDA-11.3.1 (D)

  --------------- /opt/software/modules/all/Compiler/GCC/10.3.0 ----------------
     FlexiBLAS/3.0.4 (L)    OpenBLAS/0.3.15 (L)    OpenMPI/4.1.1 (L)

  ------------- /opt/software/modules/all/Compiler/GCCcore/10.3.0 --------------
     Autoconf/2.71                        cppy/1.1.0
     Automake/1.16.3                      double-conversion/3.1.5
     Autotools/20210128                   expat/2.2.9
     Bazel/3.7.2                          expecttest/0.1.3
     Bison/3.7.6                          flatbuffers-python/2.0
     Brotli/1.0.9                         flatbuffers/2.0.0
     CMake/3.20.1                         flex/2.6.4                 (D)
     DB/18.1.40                           fontconfig/2.13.93
     Eigen/3.3.9                          freetype/2.10.4
     FFmpeg/4.3.2                         gettext/0.21               (D)
     FriBidi/1.0.10                       giflib/5.2.1
     GDRCopy/2.2                          git/2.32.0-nodocs
     GMP/6.2.1                            gperf/3.1
     ICU/69.1                             groff/1.22.4
     JsonCpp/1.9.4                        gzip/1.10
     LAME/3.100                           help2man/1.48.3
     LMDB/0.9.28                          hwloc/2.4.1                (L)
     LibTIFF/4.2.0                        hypothesis/6.13.1
     M4/1.4.18                            intltool/0.51.0
     MPFR/4.1.0                           jbigkit/2.1
     Meson/0.58.0                         libarchive/3.5.1
     NASM/2.15.05                         libevent/2.1.12            (L)
     NCCL/2.10.3-CUDA-11.3.1              libfabric/1.12.1           (L)
     Ninja/1.10.2                         libffi/3.3
     PCRE/8.44                            libjpeg-turbo/2.0.6
     PMIx/3.2.3                  (L)      libpciaccess/0.16          (L)
     Perl/5.32.1-minimal                  libpng/1.6.37
     Perl/5.32.1                 (D)      libreadline/8.1
     Pillow/8.2.0                         libtool/2.4.6
     PyYAML/5.4.1                         libxml2/2.9.10             (L)
     Python/2.7.18-bare                   libyaml/0.2.5
     Python/3.9.5-bare                    lz4/1.9.3
     Python/3.9.5                (D)      makeinfo/6.7-minimal
     Qhull/2020.2                         ncurses/6.2                (D)
     Rust/1.52.1                          nsync/1.24.0
     SQLite/3.35.4                        numactl/2.0.14             (L)
     Szip/2.1.1                           pkg-config/0.29.2          (D)
     Tcl/8.6.11                           pkgconfig/1.5.4-python
     Tk/8.6.11                            protobuf-python/3.17.3
     Tkinter/3.9.5                        protobuf/3.17.3
     UCX-CUDA/1.10.0-CUDA-11.3.1          pybind11/2.6.2
     UCX/1.10.0                  (L)      snappy/1.1.8
     UnZip/6.0                            typing-extensions/3.10.0.0
     X11/20210518                         util-linux/2.36
     XZ/5.2.5                    (L)      x264/20210414
     Yasm/1.3.0                           x265/3.5
     Zip/3.0                              xorg-macros/1.19.3
     binutils/2.36.1             (L,D)    zlib/1.2.11                (L,D)
     bzip2/1.0.8                          zstd/1.4.9
     cURL/7.76.0

  ----------------------- /opt/software/modules/all/Core -----------------------
     Anaconda3/2021.05          binutils/2.36.1
     Bison/3.8.2       (D)      cuDNN/8.2.1.32-CUDA-11.3.1
     CUDA/11.3.1                flex/2.6.4
     GCC/10.3.0        (L)      foss/2021a                 (L)
     GCCcore/10.2.0             gettext/0.21
     GCCcore/10.3.0    (L,D)    gompi/2021a
     Java/11.0.2       (11)     ncurses/6.2
     M4/1.4.19         (D)      pkg-config/0.29.2
     OpenSSL/1.1       (L)      zlib/1.2.11
     binutils/2.35

    Where:
     L:        Module is loaded
     Aliases:  Aliases exist: foo/1.2.3 (1.2) means that "module load foo/1.2" will load foo/1.2.3
     D:        Default Module


After loading the desired toolchain, the user can load the desired moduled using the ``module load`` command. For example, to load TensorFlow, the user can run the following command:

.. code-block:: console

  $ module load TensorFlow

To list the modules that are loaded, the user should use the ``module list`` command:

.. code-block:: console

  $ module list
  Currently Loaded Modules:
    1) GCCcore/10.3.0               29) Tcl/8.6.11
    2) zlib/1.2.11                  30) SQLite/3.35.4
    3) binutils/2.36.1              31) GMP/6.2.1
    4) GCC/10.3.0                   32) libffi/3.3
    5) numactl/2.0.14               33) Python/3.9.5
    6) XZ/5.2.5                     34) pybind11/2.6.2
    7) libxml2/2.9.10               35) SciPy-bundle/2021.05
    8) libpciaccess/0.16            36) Szip/2.1.1
    9) hwloc/2.4.1                  37) HDF5/1.10.7
   10) OpenSSL/1.1                  38) h5py/3.2.1
   11) libevent/2.1.12              39) cURL/7.76.0
   12) UCX/1.10.0                   40) double-conversion/3.1.5
   13) libfabric/1.12.1             41) flatbuffers/2.0.0
   14) PMIx/3.2.3                   42) giflib/5.2.1
   15) OpenMPI/4.1.1                43) ICU/69.1
   16) OpenBLAS/0.3.15              44) JsonCpp/1.9.4
   17) FlexiBLAS/3.0.4              45) NASM/2.15.05
   18) FFTW/3.3.9                   46) libjpeg-turbo/2.0.6
   19) ScaLAPACK/2.1.0-fb           47) LMDB/0.9.28
   20) foss/2021a                   48) nsync/1.24.0
   21) CUDA/11.3.1                  49) protobuf/3.17.3
   22) cuDNN/8.2.1.32-CUDA-11.3.1   50) protobuf-python/3.17.3
   23) GDRCopy/2.2                  51) flatbuffers-python/2.0
   24) UCX-CUDA/1.10.0-CUDA-11.3.1  52) typing-extensions/3.10.0.0
   25) NCCL/2.10.3-CUDA-11.3.1      53) libpng/1.6.37
   26) bzip2/1.0.8                  54) snappy/1.1.8
   27) ncurses/6.2                  55) TensorFlow/2.6.0-CUDA-11.3.1
   28) libreadline/8.1

If the user wants to "unload" the loaded modules, he can use the command ``module purge``:

.. code-block:: console

  $ module purge
  $ module list
  No modules loaded
