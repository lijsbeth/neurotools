## Freesurfer

Last login: Thu Mar 21 15:32:10 on ttys000
-------- freesurfer-Darwin-OSX-stable-pub-v6.0.0-2beb96c --------
Setting up environment for FreeSurfer/FS-FAST (and FSL)
FREESURFER_HOME   /Applications/freesurfer
FSFAST_HOME       /Applications/freesurfer/fsfast
FSF_OUTPUT_FORMAT nii.gz
SUBJECTS_DIR      /Applications/freesurfer/subjects
MNI_DIR           /Applications/freesurfer/mni
mbp-elizaveta:~ elizavetalavrova$ export TUTORIAL_DATA=/users/elizavetalavrova
mbp-elizaveta:~ elizavetalavrova$ cd TUTORIAL_DATA
mbp-elizaveta:TUTORIAL_DATA elizavetalavrova$ recon-all -help

USAGE: recon-all

 Required Arguments:
   -subjid <subjid>
   -<process directive>

 Fully-Automated Directive:
  -all           : performs all stages of cortical reconstruction
  -autorecon-all : same as -all

 Manual-Intervention Workflow Directives:
  -autorecon1    : process stages 1-5 (see below)
  -autorecon2    : process stages 6-23
                   after autorecon2, check white surfaces:
                     a. if wm edit was required, then run -autorecon2-wm
                     b. if control points added, then run -autorecon2-cp
                     c. proceed to run -autorecon3
  -autorecon2-cp : process stages 12-23 (uses -f w/ mri_normalize, -keep w/ mri_seg)
  -autorecon2-wm : process stages 15-23
  -autorecon2-inflate1 : 6-18
  -autorecon2-perhemi : tess, sm1, inf1, q, fix, sm2, inf2, finalsurf, ribbon
  -autorecon3    : process stages 24-34
                     if edits made to correct pial, then run -autorecon-pial
  -hemi ?h       : just do lh or rh (default is to do both)

  Autorecon Processing Stages (see -autorecon# flags above):
    1.  Motion Correction and Conform
    2.  NU (Non-Uniform intensity normalization)
    3.  Talairach transform computation
    4.  Intensity Normalization 1
    5.  Skull Strip

    6.  EM Register (linear volumetric registration)
    7.  CA Intensity Normalization
    8.  CA Non-linear Volumetric Registration 
    9.  Remove neck
    10. EM Register, with skull
    11. CA Label (Aseg: Volumetric Labeling) and Statistics

    12. Intensity Normalization 2 (start here for control points)
    13. White matter segmentation
    14. Edit WM With ASeg
    15. Fill (start here for wm edits)
    16. Tessellation (begins per-hemisphere operations)
    17. Smooth1
    18. Inflate1
    19. QSphere
    20. Automatic Topology Fixer
    21. White Surfs (start here for brain edits for pial surf)
    22. Smooth2
    23. Inflate2

    24. Spherical Mapping
    25. Spherical Registration 
    26. Spherical Registration, Contralater hemisphere
    27. Map average curvature to subject
    28. Cortical Parcellation (Labeling)
    29. Cortical Parcellation Statistics
    30. Pial Surfs
    31. WM/GM Contrast
    32. Cortical Ribbon Mask
    33. Cortical Parcellation mapped to ASeg
    34  Brodmann and exvio EC labels

 Step-wise Directives
  See -help

 Expert Preferences
  -pons-crs C R S : col, row, slice of seed point for pons, used in fill
  -cc-crs C R S : col, row, slice of seed point for corpus callosum, used in fill
  -lh-crs C R S : col, row, slice of seed point for left hemisphere, used in fill
  -rh-crs C R S : col, row, slice of seed point for right hemisphere, used in fill
  -nofill        : do not use the automatic subcort seg to fill
  -watershed cmd : control skull stripping/watershed program
  -wsless : decrease watershed threshold (leaves less skull, but can strip more brain)
  -wsmore : increase watershed threshold (leaves more skull, but can strip less brain)
  -wsatlas : use atlas when skull stripping
  -no-wsatlas : do not use atlas when skull stripping
  -no-wsgcaatlas : do not use GCA atlas when skull stripping
  -wsthresh pct : explicity set watershed threshold
  -wsseed C R S : identify an index (C, R, S) point in the skull
  -norm3diters niters : number of 3d iterations for mri_normalize
  -normmaxgrad maxgrad : max grad (-g) for mri_normalize. Default is 1.
  -norm1-b N : in the _first_ usage of mri_normalize, use control 
               point with intensity N below target (default=10.0) 
  -norm2-b N : in the _second_ usage of mri_normalize, use control 
               point with intensity N below target (default=10.0) 
  -norm1-n N : in the _first_ usage of mri_normalize, do N number 
               of iterations
  -norm2-n N : in the _second_ usage of mri_normalize, do N number 
               of iterations
  -cm           : conform volumes to the min voxel size 
  -no-fix-with-ga : do not use genetic algorithm when fixing topology
  -fix-diag-only  : topology fixer runs until ?h.defect_labels files
                    are created, then stops
  -seg-wlo wlo : set wlo value for mri_segment and mris_make_surfaces
  -seg-ghi ghi : set ghi value for mri_segment and mris_make_surfaces
  -nothicken   : pass '-thicken 0' to mri_segment
  -no-ca-align-after : turn off -align-after with mri_ca_register
  -no-ca-align : turn off -align with mri_ca_label
  -deface      : deface subject, written to orig_defaced.mgz

  -expert file     : read-in expert options file
  -xopts-use       : use pre-existing expert options file
  -xopts-clean     : delete pre-existing expert options file
  -xopts-overwrite : overwrite pre-existing expert options file
  -termscript script : run script before exiting (multiple -termscript flags possible)
   This can be good for running custom post-processing after recon-all
   The script must be in your path. The subjid is passed as the only argument
   The current directory is changed to SUBJECTS_DIR before the script is run
   The script should exit with 0 unless there is an error

  -mprage : assume scan parameters are MGH MP-RAGE protocol
  -washu_mprage : assume scan parameters are Wash.U. MP-RAGE protocol.
                  both mprage flags affect mri_normalize and mri_segment,
                  and assumes a darker gm.
  -schwartzya3t-atlas : for tal reg, use special young adult 3T atlas

  -use-gpu : use GPU versions of mri_em_register, mri_ca_register,
             mris_inflate and mris_sphere

 Notification Files (Optional)
  -waitfor file : wait for file to appear before beginning
  -notify  file : create this file after finishing

 Status and Log files (Optional)
  -log     file : default is scripts/recon-all.log
  -status  file : default is scripts/recon-all-status.log
  -noappend     : start new log and status files instead of appending
  -no-isrunning : do not check whether this subject is currently being processed

 Segmentation of substructures of hippocampus and brainstem
  -hippocampal-subfields-T1 : segmentation of hippocampal subfields using input T1 scan
  -hippocampal-subfields-T2 file ID : segmentation using an additional scan (given by file);
                                      ID is a user-defined identifier for the analysis
  -hippocampal-subfields-T1T2 file ID : segmentation using additional scan (given by file) and input T1
                                        simultaneously; ID is a user-defined identifier for the analysis
  -brainstem-structures : segmentation of brainstem structures

 Other Arguments (Optional)
  -sd subjectsdir : specify subjects dir (default env SUBJECTS_DIR)
  -mail username  : mail user when done
  -umask umask    : set unix file permission mask (default 002)
  -grp groupid    : check that current group is alpha groupid 
  -onlyversions   : print version of each binary and exit
  -debug          : print out lots of info
  -allowcoredump  : set coredump limit to unlimited
  -dontrun        : do everything but execute each command
  -version        : print version of this script and exit
  -help           : voluminous bits of wisdom

$Id: recon-all,v 1.580.2.16 2017/01/18 14:11:24 zkaufman Exp $


Performs all, or any part of, the FreeSurfer cortical reconstruction
process. This help only gives some simple information. For more
detailed documentation, see https://surfer.nmr.mgh.harvard.edu

Basic usages:

1. Subject dir does not exist:

  recon-all -subject subjectname -i invol1 <-i invol2> -all

Creates analysis directory $SUBJECTS_DIR/subjectname, converts one or
more input volumes to MGZ format in subjectname/mri/orig, and runs
all processing steps. If subjectname exists, then an error is returned
when -i is used; but this can be overridden with -force (in which
case any pre-existing source volumes are deleted).

2. Manual conversion into mgz:

  mkdir -p $SUBJECTS_DIR/subjectname/mri/orig
  mri_convert invol1 $SUBJECTS_DIR/subjectname/mri/orig/001.mgz
  mri_convert invol2 $SUBJECTS_DIR/subjectname/mri/orig/002.mgz
  recon-all -subject subjectname -all

If no input volumes are given, then it is assumed that the subject
directory has already been created and that the raw data already
exists in MGZ format in subjid/mri/orig as XXX.mgz, where XXX is a
3-digit, zero-padded number.


SUBJECT IDENTIFICATION STRING

-s subjectname
-sid subjectname
-subjid subjectname
-subject subjectname

'subjectname' is the FreeSurfer subject identification string which doubles
as the name of the reconstruction root directory for this subject. This
reconstruction should be referenced by this string for all FreeSurfer
commands and in the register.dat matrix (for functional interfacing).


SPECIFYING DIRECTIVES

Directives instruct recon-all which part(s) of the reconstruction
stream to run. While it is possible to do everything in one shot (using
the -all flag), there can be some benefits to customizing the
stream. These benefits include stopping to perform manual editing as
well as parallelization. Directives are either clustered or step-wise.
Clustered directives are sets of steps that can be performed by
specifying a single flag. A step-wise directive refers to a single
step.  Directives accumulate. A step can be removed from a cluster by
adding -no<step> after the cluster flag. For example, specifying
-all followed by -notalairach will perform all the reconstruction
steps except talairaching. However, note that if -notalairach *preceeded*
-all, talairaching would still be performed.


CLUSTERED DIRECTIVES

-all
-autorecon-all

Perform all reconstruction steps.

-autorecon1

Motion correction through skull strip.

-autorecon2

Subcortical segmentation through make white surfaces.

-autorecon2-cp

Normalization2 through make final surfaces.

-autorecon2-wm

Fill through make white surfaces. Used after editing wm volume after running
-autorecon2.

-autorecon-pial

Makes final surfaces (white and pial). Used after editing brain.finalsurfs
volume after running -autorecon2. The brain.finalsurfs.mgz volume may be
edited to fix problems with the pial surface.

-autorecon3

Spherical morph, automatic cortical parcellation, pial surf and ribbon mask.


STEP-WISE DIRECTIVES

Step-wise directives allow the user to implement a single step in the
reconstruction process. See also STEP DESCRIPTION SUMMARIES below.
They also allow users to include/exclude a step from a clustered
DIRECTIVE. To include a step, use -step (eg, -skullstrip). To exclude
a step, use -nostep (eg -noskullstrip).

Run times are approximate for an Intel Xeon E5-2643 64bit 3.4GHz processor:

  -<no>motioncor          2 min
  -<no>talairach        < 1 min
  -<no>normalization      2 min
  -<no>skullstrip        15 min
  -<no>nuintensitycor     1 min
  -<no>gcareg            15 min
  -<no>canorm             1 min
  -<no>careg              1 hour
  -<no>careginv           1 min
  -<no>rmneck             1 min
  -<no>skull-lta         12 min
  -<no>calabel           34 min
  -<no>normalization2     3 min
  -<no>maskbfs          < 1 min
  -<no>segmentation       1 min
  -<no>fill               1 min
  -<no>tessellate       < 1 min     per hemisphere
  -<no>smooth1          < 1 min     per hemisphere
  -<no>inflate1           1 min     per hemisphere
  -<no>qsphere            3 min     per hemisphere
  -<no>fix               15 min     per hemisphere
  -<no>white              3 min     per hemisphere
  -<no>smooth2          < 1 min     per hemisphere
  -<no>inflate2         < 1 min     per hemisphere
  -<no>curvHK           < 1 min     per hemisphere
  -<no>curvstats        < 1 min     per hemisphere
  -<no>sphere            40 min     per hemisphere
  -<no>surfreg           50 min     per hemisphere
  -<no>jacobian_white   < 1 min     per hemisphere
  -<no>avgcurv          < 1 min     per hemisphere
  -<no>cortparc           1 min     per hemisphere
  -<no>pial               4 min     per hemisphere
  -<no>surfvolune       < 1 min     per hemisphere
  -<no>cortribbon        15 min
  -<no>parcstats        < 1 min     per hemisphere
  -<no>cortparc2          1 min     per hemisphere
  -<no>parcstats2       < 1 min     per hemisphere
  -<no>cortparc3          1 min     per hemisphere
  -<no>parcstats3       < 1 min     per hemisphere
  -<no>pctsurfcon       < 1 min     per hemisphere
  -<no>hyporelabel      < 1 min     per hemisphere
  -<no>aparc2aseg         1 min
  -<no>apas2aseg          1 min
  -<no>segstats           3 min
  -<no>wmparc             7 min
  -<no>balabels           5 min     per hemisphere

  -all                    7 hours   both hemipheres

If -parallel is specified, runtime is reduced to 3 hours.


SEGMENTATION OF HIPPOCAMPAL SUBFIELDS 

The following flags can be used to obtain a segmentation of the hippocampal subfields.
The method is described in [17], and you can find further information here:
http://surfer.nmr.mgh.harvard.edu/fswiki/HippocampalSubfields

-hippocampal-subfields-T1 

It uses the T1 scan which the recon-all stream has processed at 1 mm resolution or higher (with -cm). 

-hippocampal-subfields-T2 file ID

Instead of the main T1 scan, it uses an additional scan ('file'), typically (but not necessarily)
a T2 volume with higher resolution, at least in the coronal plane. It also requires a second
argument ('ID'), which  uniquely identifies the output in the mri directory; this is useful when
different additional volumes are tried in this mode, in order to prevent files from being overwritten

-hippocampal-subfields-T1T2 file ID

This mode is very similar to the previous one, with the only difference that the main T1 and the 
additional volumes are used simultaneously in the segmentation.


SEGMENTATION OF BRAINSTEM STRUCTURES

-brainstem-structures

Performs segmentation of brains structures (medulla, pons, midbrain, SCP) on the T1 scan which the 
recon-all stream has processed, at 1 mm or higher resolution (with -cm). The method is described in [18];
you can read more at: http://surfer.nmr.mgh.harvard.edu/fswiki/BrainstemSubstructures


EXPERT PREFERENCES

-pons-crs C R S

Specify a seed point for the pons during the fill operation. This is
used to cut the brain stem from brain. By default, this point will be
determined automatically. It should only be specified if there is a
cut failure. To determine what this point should be, find the center
of the pons in the T1 volume (in tkmedit) and record the column, row,
and slice. Creates a file called scripts/seed-ponscrs.man.dat
with the CRS.

-cc-crs C R S

Specify a seed point for the corpus callosum during the fill
operation. This is used to help separate the hemispheres.  By default,
this point will be determined automatically. It should only be
specified if there is a cut failure.  To determine what this point
should be, find the center of the CC in the T1 volume (in tkmedit) and
record the column, row, and slice. Creates a file called
scripts/seed-cccrs.man.dat with the CRS.

-lh-crs C R S

Specify a seed point for the left hemisphere during the fill
operation. This is used to help identify the left hemisphere.  By
default, this point will be determined automatically. It should only
be specified if there is a cut failure.  To determine what this point
should be, find a point in the white matter mass of the left
hemisphere in the T1 volume (in tkmedit) and record the column, row,
and slice. Creates a file called scripts/seed-cccrs.man.dat with the
CRS. Remember that tkmedit displays the volume in radiological
convention (ie, left is right).

-rh-crs C R S

Same as -lh-crs but for the right hemisphere. Creates a file called
scripts/seed-rhcrs.man.dat with the CRS.

-watershed cmd

This controls how the skull stripping will be performed. Legal values are
normal (the default), atlas, nowatershed, watershedonly, and watershedtemplate.

-wsmore/-wsless

Increase/decrease the preflooding height (threshold) when skull
stripping. -wsmore will expand the skull surface; -wsless will shrink
the skull surface.  See also -wsthresh.

-wsthresh pctheight

Explicitly set the preflooding height when skull stripping.

-wsseed R C S

Supply a point in the volume that the user believes to be in the white
matter.  By default, this point will be determined automatically. It
should only be specified if there is a strip failure. To determine
what this point should be, find a point in the white matter using
tkmedit and record the Volume Index values (NOT the XYZ coordinates).

-no-wsgcaatlas

Disable usage of the GCA atlas when running mri_watershed skull-stripping.
The default is to use the GCA atlas to locate anatomy aiding skull-strip.

-gca gcafile

Specify the name of the gaussian classifier array (GCA) file
to be used with GCA registration and automatic subcortical
segmentation. It must be found in the FREESURFER_HOME/average directory (or
use -gca-dir to specify an alternate path).
The Default is RB_all_YYYY-MM-DD.gca located in
FREESURFER_HOME/average. This has no effect unless the GCA registration
or subcortical segmentation stages are to be performed.

-gca-skull gcafile

Specify the name of the gaussian classifier array (GCA) file to be used with
registration with skull.  It must be found in the FREESURFER_HOME/average
directory (or use -gca-dir to specify an alternate path).
The default is RB_all_withskull_YYYY-MM-DD.gca located in
FREESURFER_HOME/average.

-gcs gcsfile

Specify the name of the gaussian classifier surface atlas (GCS) file
to be used for the cortical parcellation stage. It must be found in the
FREESURFER_HOME/average directory (or use -gcs-dir to specify an alternate
path). The default is named
curvature.buckner40.filled.desikan_killiany.2007-06-20.gcs and is located in
FREESURFER_HOME/average.

-twm twmfile

Where (twmfile) is a control.dat format file (a point set in freeview)
with points manually selected to be in the white matter inferior to
hippocampus in the temporal lobe. This option is passed to mri_ca_register.

-nuiterations

Number of iterations in the non-uniform intensity correction.
Default is 1.

-norm3diters niters

Use niters 3d normalization iterations (passes as -n to _both_ runs of
mri_normalize).

-normmaxgrad maxgrad

Passes "-g maxgrad" to _both_ runs of mri_normalize. Max grad default is 1.

-norm1-b N

In the _first_ usage of mri_normalize (during creation of T1.mgz), use
control point with intensity N below target (default=10.0)

-norm1-n N

In the _first_ usage of mri_normalize, do N number of iterations

-norm2-b N

In the _second_ usage of mri_normalize (during creation of brain.mgz), use
control point with intensity N below target (default=10.0)

-norm2-n N

In the _second_ usage of mri_normalize, do N number of iterations

-noaseg

Skips subcortical segmentation steps (same as -nosubcortseg), and does
not use aseg.presurf.mgz for inorm2, wm segmentation, or filling. 
Use this flag for brains that do not support usage of Freesurfers subcortical
segmentation, such as baby brains, or non-human primates.

-noaseg-inorm2

Does not use aseg.presurf.mgz for the second mri_normalize step.

-bigventricles

If a subject has enlarged ventricles due to atrophy, include the -bigventricles
flag with the -autorecon2 stage in order to prevent surfaces extending into
the ventricle regions. The flag directly affects the binary mri_ca_register,
and mris_make_surfaces indirectly via aseg.presurf.mgz.

-norandomness

The random number generator used by certain binaries is seeded with the
same number, thus producing identical results from run to run.

-cw256

Include this flag after -autorecon1 if images have a FOV > 256.  The
flag causes mri_convert to conform the image to dimensions of 256^3.

-notal-check

Skip the automatic failure detection of Talairach alignment.

-qcache

Produce the pre-cached files required by the Qdec utility, allowing rapid
analysis of group data.  These files are created by running mris_preproc,
which creates smoothed surface data files sampled to the 'fsaverage'
common-space surface. By default, the surface data for thickness, curv, sulc,
area and jacobian_white are smoothed at 0, 5, 10, 15, 20, and 25 mm FWHM.
If just one set of surface data needs to be processed, then the option
-measure <surfmeas> can follow -qcache, where <surfmeas> is one of: thickness,
curv, sulc, area, jacobian_white or any surface measure. Multiple instances
of -measure <meas> is supported.  The -measuredir option allows
specifying a directory other than the default of surf. Another option is
-fwhm <num> where <num> is a value in mm.  Also, -target <name> allows
specifying a common-space target other than fsaverage (the default).
qcache is also a target for make, eg. recon-all -make qcache
See also: http://surfer.nmr.mgh.harvard.edu/fswiki/Qdec

-smooth-cortex-only

Only applies with -qcache. Only smooth data if it is part of the ?h.cortex.label.
This prevents values in the medial wall (which are meaningless) from being
smoothed into cortical areas. This is the default and you will have to turn
it off with -no-smooth-cortex-only.

-no-smooth-cortex-only

Allow medial wall values to smooth into cortex.

-make target

Runs recon-all through 'make', the standard utility used to create a file
only if its dependencies are out-of-date.  This -make option makes use of the
file recon-all.makefile, where the dependency chain is specified.
A 'target' argument must be specified.  The valid targets are:

  all
  autorecon1
  autorecon2
  autorecon2-volonly
  autorecon2-perhemi
  autorecon3
  qcache

These targets correspond to their flag equivalents in recon-all.  The
difference in behaviour is that files are created only if the file does not
exist or if an input file used to create it has a newer date than the file
in need of creation.  It is also possible to supply the full pathname to a
particular file as a target.

The flag -dontrun can also be specified to show the commands that will run
without excuting them.

-lgi
-lGI
-localGI

Computes local measurements of pial-surface gyrification at thousands of
points over the cortical surface. See reference [13] for details.

-label_v1

Create a label of V1, based on Hinds et al., NeuroImage 39 (2008) 1585-1599.

-balabels
-ba-labels
-ba_labels

Creates Brodmann area labels of BA1, BA2, BA3a, BA3b, BA4a, BA4p, BA6, BA44,
BA45, V1, V2, and V5/MT (and perirhinal) by mapping labels from the 
'fsaverage' subject, which must exist within the SUBJECTS_DIR.  
Based on:
"Cortical Folding Patterns and Predicting Cytoarchitecture", Fischl et al.,
Cerebral Cortex 2007.

-use-gpu

Use the GPU versions of the binaries mri_em_register, mri_ca_register,
mris_inflate, and mris_sphere.


EXPERT OPTIONS FILE

While the expert preferences flags supported by recon-all cover most of
the instances where special flags need to be passed to a FreeSurfer binary,
to allow passing an arbitrary flag to a binary, recon-all supports the
reading of a user-created file containing special options to include in
the command string (in addition to, not in place of).  The file should
contain as the first item the name of the command, and the items following
it on rest of the line will be passed as the extra options.  For example,
if a file called expert.opts is created containing these lines:

  mri_em_register -p .5
  mris_topo_fixer -asc

then the option "-p .5" will be passed to mri_em_register, and "-asc"
will be passed to mris_topo_fixer.  The name of the expert options file
is passed to recon-all with the -expert flag, eg.

  recon-all -expert expert.opts

When an expert options is passed, it will be copied to scripts/expert-options.
Future calls to recon-all, the user MUST explicitly specify how to treat this file.
Options are (1) use the file (-xopts-use), or (2) delete it (-xopts-clean). If
this file exsts and the user specifies another expert options file, then
the user must also specify -xopts-overwrite.

The following FreeSurfer binaries will accept an expert option:

  talairach_avi
  mri_normalize
  mri_watershed
  mri_em_register
  mri_ca_normalize
  mri_ca_register
  mri_remove_neck
  mri_ca_label
  mri_segstats
  mri_mask
  mri_segment
  mri_edit_wm_with_aseg
  mri_pretess
  mri_fill
  mri_tessellate
  mris_smooth
  mris_inflate
  mris_sphere
  mris_fix_topology
  mris_topo_fixer
  mris_remove_intersection
  mris_make_surfaces
  mris_surf2vol
  mris_register
  mris_jacobian
  mrisp_paint
  mris_ca_label
  mris_anatomical_stats
  mri_aparc2aseg


NOTIFICATION FILES

Notification files allow the user to cascade invocations to recon-all,
with one invocation waiting until another one terminates. This is done
by specifying a file that must exist before an invocation can precede
(-waitfor) and/or specifying a file that is created when an invocation
terminates (-notify). This type of interprocess communication can
allow users to parallelize the stream. If this is to be done, note
that each hemisphere can be run separately by specifying the -hemi
flag.


LOG AND STATUS FILES

By default, log and status files are created in subjid/scripts. The
log file contains all the output from all the programs that have been
run during the invocation to recon-all. The status file has a list of
all the programs that have been run and the time at which each
started. The log file is intended to be a record of what was done
whereas the status file allows the user to easily see where in the
stream a currently running process is. The log file should be sent
with all bug reports. By default, these files are called recon-all.log
and recon-all-status.log, but this can be changed with the -log and
-status options. By default, the log and status are appended to. New
log and status files can be forced with the -noappend flag.


OTHER ARGUMENTS

-sd subjectsdir

This allows the user to specify the root of the FreeSufer subjects
directory. If unspecified, the environment variable SUBJECTS_DIR
is used.

-mail username

Send email to username when the process terminates.


STEP DESCRIPTION SUMMARIES

Motion Correction (-<no>motioncor)

When there are multiple source volumes, this step will correct for
small motions between them and then average them together. The input
are the volumes found in file(s) mri/orig/XXX.mgz. The output will be
the volume mri/orig.mgz. If no runs are found, then it looks for
a volume in mri/orig (or mri/orig.mgz). If that volume is there, then
it is used in subsequent processes as if it was the motion corrected
volume. If no volume is found, then the process exits with errors.
The motion correction step uses a robust registration [14] procedure
to produce highly accurate registrations of the brain, ignoring outlier
regions, such as differen cropping planes, jaw, neck, eye movement etc.

Talairach (-<no>talairach)

This computes the affine transform from the orig volume to the MNI305
atlas using Avi Snyders 4dfp suite of image registration tools,
through a FreeSurfer script called talairach_avi. Several of the downstream
programs use talairach coordinates as seed points. You can/should check
how good the talairach registration is using
"tkregister2 --s subjid --fstal-avi". You must have an "fsaverage" subject in
your SUBJECTS_DIR. tkregister2 allows you to compare the orig volume
against the talairach volume resampled into the orig space. If you modify
the registration, it will change the talairach.xfm file. Your edits will
be *not* be overwritten unless you run recon-all specifying -clean-tal.
Run "tkregister2 --help" for more information.
Creates the files mri/transform/talairach.auto.xfm and talairach.xfm.
The flag -tal-check will check the registration against known-good transforms.
Adding the flag -use-mritotal after -talairach will use the MINC program
mritotal (see Collins, et al., 1994) to perform the transform.

Normalization (-<no>normalization)

Performs intensity normalization of the orig volume and places the
result in mri/T1.mgz. Attempts to correct for fluctuations in
intensity that would otherwise make intensity-based segmentation much
more difficult. Intensities for all voxels are scaled so that the mean
intensity of the white matter is 110. If there are problems with the
normalization, users can add control points. See also Normalization2.

Skull Strip (-<no>skullstrip)

Removes the skull from mri/T1.mgz and stores the result in
mri/brainmask.auto.mgz and mri/brainmask.mgz.
Runs the mri_watershed program. If the strip fails, users can specify
seed points (-wsseed) or change the threshold (-wsthresh, -wsmore, -wsless).
The -autorecon1 stage ends here.

NU Intensity Correction (-<no>nuintensitycor)

Non-parametric Non-uniform intensity Normalization (N3), corrects for
intensity non-uniformity in MR data,  making relatively few assumptions
about the data.  This runs the MINC tool 'nu_correct'.  By default, one
iteration of nu_correct is run.  The flag -nuiterations specification
of some other number of iterations.

Automatic Subcortical Segmentation (-<no>subcortseg)

This is done in six stages. (1) GCA linear registration
(-gcareg). This is an initial registration to a template. (2)
Canonical Normalization (-canorm), (3) Canonical Registration
(-careg). (4) Neck removal (-rmneck), (5) Registration, w/skull
(-skull-lta), and (6) Subcortical labeling (-calabel).
The stages are listed next.

EM (GCA) Registration (-<no>gcareg)

Computes transform to align the mri/nu.mgz volume to the default GCA atlas
found in FREESURFER_HOME/average (see -gca flag for more info).
Creates the file mri/transforms/talairach.lta.
The -autorecon2 stage starts here.

CA Normalize (-<no>canorm)

Further normalization, based on GCA model.
Creates mri/norm.mgz.
Note: -canorm-usecps will enable usage of control points during normalization.

CA Register (-<no>careg)

Computes a nonlinear transform to align with GCA atlas.
Creates the file mri/transform/talairach.m3z.

CA Register Inverse (-<no>careginv)

Computes the inverse of the nonlinear transform to align with GCA
atlas.  Creates the files mri/transform/talairach.m3z.{x,y,z}.mgz.

Remove neck (-<no>rmneck)

The neck region is removed from the NU-corrected volume mri/nu.mgz.
Makes use of transform computed from prior CA Register stage.
Creates the file mri/nu_noneck.mgz.

EM Registration, with Skull (-<no>skull-lta)

Computes transform to align volume mri/nu_noneck.mgz with GCA volume
possessing the skull.
Creates the file mri/transforms/talairach_with_skull_2.lta.

CA Label (-<no>calabel)

Labels subcortical structures, based in GCA model.
Creates the files mri/aseg.auto.mgz and mri/aseg.presurf.mgz.

ASeg Stats (-<no>segstats)

Computes statistics on the segmented subcortical structures found
in mri/aseg.mgz. Writes output to file stats/aseg.stats.

Normalization2 (-<no>normalization)

Performs a second (major) intensity correction using only the brain
volume as the input (so that it has to be done after the skull strip).
Intensity normalization works better when the skull has been removed.
Creates a new brain.mgz volume. The -autorecon2-cp stage begins here.
If -noaseg flag is used, then aseg.presurf.mgz is not used by mri_normalize.

WM Segmentation (-<no>segmentation)

Attempts to separate white matter from everything else. The input is
mri/brain.mgz, and the output is mri/wm.mgz.  Uses intensity,
neighborhood, and smoothness constraints.  This is the volume that is
edited when manually fixing defects. Calls mri_segment,
mri_edit_wm_with_aseg, and mri_pretess. To keep previous edits, run
with -keep. If -noaseg is used, them mri_edit_wm_aseg is skipped.

Cut/Fill (-<no>fill)

This creates the subcortical mass from which the orig surface is
created. The mid brain is cut from the cerebrum, and the hemispheres
are cut from each other. The left hemisphere is binarized to 255.
The right hemisphere is binarized to 127.  The input is mri/wm.mgz
and the output is mri/filled.mgz. Calls mri_fill. If the cut fails,
then seed points can be supplied (see -cc-crs, -pons-crs, -lh-crs,
-rh-crs). The actual points used for the cutting planes in the
corpus callosum and pons can be found in scripts/ponscc.cut.log.
The stage -autorecon2-wm begins here.  This is the last stage of
volumetric processing. If -noaseg is used, then aseg.presurf.mgz is 
not used by mri_fill.

Tessellation (-<no>tessellate)

This is the step where the orig surface (ie, surf/?h.orig.nofix) is
created. The surface is created by covering the filled hemisphere with
triangles. Runs mri_tessellate. The places where the points of the
triangles meet are called vertices. Creates the file surf/?h.orig.nofix
Note: the topology fixer will create the surface ?h.orig.

Orig Surface Smoothing (-<no>smooth1, -<no>smooth2)

After tesselation, the orig surface is very jagged because each
triangle is on the edge of a voxel face and so are at right angles to
each other. The vertex positions are adjusted slightly here to reduce
the angle. This is only necessary for the inflation processes.
Creates surf/?h.smoothwm(.nofix). Calls mris_smooth. Smooth1 is the step
just after tessellation, and smooth2 is the step just after topology
fixing.

Inflation (-<no>inflate1, -<no>inflate2)

Inflation of the surf/?h.smoothwm(.nofix) surface to create
surf/?h.inflated. The inflation attempts to minimize metric distortion
so that distances and areas are perserved (ie, the surface is not
stretched). In this sense, it is like inflating a paper bag and not a
balloon.  Inflate1 is the step just after tessellation, and inflate2
is the step just after topology fixing. Calls mris_inflate. Creates
?h.inflated, ?h.sulc, ?h.curv, and ?h.area.

QSphere (-<no>qsphere)

This is the initial step of automatic topology fixing. It is a
quasi-homeomorphic spherical transformation of the inflated surface designed
to localize topological defects for the subsequent automatic topology fixer.
Calls mris_sphere. Creates surf/?h.qsphere.nofix.

Automatic Topology Fixer (-<no>fix)

Finds topological defects (ie, holes in a filled hemisphere) using
surf/?h.qsphere.nofix, and changes the orig surface (surf/?h.orig.nofix)
to remove the defects. Changes the number of vertices.  All the defects
will be removed, but the user should check the orig surface in the volume
to make sure that it looks appropriate. Calls mris_topo_fixer.
Creates surf/?h.orig (by iteratively fixing surf/?h.orig.nofix).

White Surface (-<no>white)

Creates the ?h.white surfacees as well as the curvature file (?h.curv).
The white surface is created by "nudging" the orig surface so that it
closely follows the white-gray intensity gradient as found in the T1 volume.
Calls mris_make_surfaces.  See also "Pial Surface" and "Final Surfaces".

Spherical Inflation (-<no>sphere)

Inflates the orig surface into a sphere while minimizing metric
distortion.  This step is necessary in order to register the surface
to the spherical atlas. (also known as the spherical morph). Calls
mris_sphere. Creates surf/?h.sphere.  The -autorecon3 stage begins here.

Ipsilateral Surface Registation (Spherical Morph) (-<no>surfreg)

Registers the orig surface to the spherical atlas through
surf/?h.sphere. The surfaces are first coarsely registered by aligning
the large scale folding patterns found in ?h.sulc and then fine tuned
using the small-scale patterns as in ?h.curv.
Calls mris_register. Creates surf/?h.sphere.reg.

Jacobian (-<no>jacobian_white)

Computes how much the white surface was distorted in order to register
to the spherical atlas during the -surfreg step. Creates ?h.jacobian_white
(a curv formatted file). This step follows the surface registration step.

Surface Registation, maximal distortion, with Jacobian (-<no>jacobian_dist0)

Run spherical registration with no metric distortion penalty. This will
cause surface geometry to align regardless of the amount of distortion
induced (ie, distance contraints are turned off). The distortion will then
be quantified by the Jacobian of the transform. Creates ?h.jacobian_dist0 (a
curv formatted file) and ?h.sphere.dist0.jacobian.reg (a surface file). This
step is not run automatically because it can add about an hour per hemi.
Note: the file ?h.jacobian_white (see prior help text) is the Jacobian of
the white surface to spherical atlas alignment from -surfreg.

Contralateral Surface Registation (Spherical Morph) (-<no>contrasurfreg)

Same as ipsilateral but registers to the contralateral atlas.
Creates lh.rh.sphere.reg and rh.lh.sphere.reg.

Average Curvature (-<no>avgcurv)

Resamples the average curvature from the atlas to that of the subject.
Allows the user to display activity on the surface of an individual
with the folding pattern (ie, anatomy) of a group. Calls mrisp_paint.
Creates surf/?h.avg_curv.

Cortical Parcellation (-<no>cortparc, -<no>cortparc2, -<no>cortparc3 )

Assigns a neuroanatomical label to each location on the cortical surface.
Incorporates both geometric information derived from the cortical model
(sulcus and curvature), and neuroanatomical convention.
Calls mris_ca_label.  -cortparc creates label/?h.aparc.annot,
-cortparc2 creates /label/?h.aparc.a2009s.annot, and
-cortparc3 creates /label/?h.aparc.DKTatlas40.annot.

Pial Surface (-<no>pial)

Creates the ?h.pial surfaces as well as the thickness file (?h.thickness).
The pial surface is created by expanding the white surface so that it closely
follows the gray-CSF intensity gradient as found in the T1 volume.  The
cortical parcellation is also used to refine the surface in certain areas.
Calls mris_make_surfaces.  See also "Final Surfaces".

Final Surfaces (-<no>finalsurfs)

!!! DEPRECATED !!! This flag is intended to emulate the old-style single-run
mris_make_surfaces, where the white and pial surfaces are created at the same
time without aid from the cortical parcellation data.

WM/GM Contrast (-<no>pctsurfcon)

Computes the vertex-by-vertex percent contrast between white and gray matter.
The computation is:

         100*(W-G)
   pct = ---------
         0.5*(W+G)

The white matter is sampled 1mm below the white surface. The gray matter is
sampled 30% the thickness into the cortex. The volume that is sampled is
rawavg.mgz.  The output is stored in the surf dir of the given subject as
?h.w-g.pct.mgh.  Non-cortical regions (medial wall) are zeroed.
A stats file named ?h.w-g.pct.stats is also computed.

Surface Volume (-surfvolume)

Creates the ?h.volume file by first creating the ?h.mid.area file by
adding ?h.area(.white) to ?h.area.pial, then dividing by two.  Then
?h.volume is created by multiplying ?.mid.area with ?h.thickness.
This step is also run at the end of the -pial step.

Cortical Ribbon Mask (-<no>cortribbon)

Creates binary volume masks of the cortical ribbon, ie, each voxel is
either a 1 or 0 depending upon whether it falls in the ribbon or not.
Saved as ?h.ribbon.mgz.  Uses mgz regardless of whether the -mgz
option is used.

Parcellation Statistics (-<no>parcstats, -<no>parcstats2, -<no>parcstats3)

Runs mris_anatomical_stats to create a summary table of cortical
parcellation statistics for each structure, including 1. structure
name 2. number of vertices 3. total wm surface area (mm^2) 4. total gray
matter volume (mm^3) 5. average cortical thickness (mm) 6. standard
error of cortical thickness (mm) 7. integrated rectified mean wm
curvature 8. integrated rectified Gaussian wm curvature 9. folding index
10. intrinsic curvature index.
For -parcstats, the file is saved in stats/?h.aparc.stats.
For -parcstats2, the file is saved in stats/?h.aparc.${DESTRIEUX_NAME}.stats.
For -parcstats3, the file is saved in stats/?h.aparc.${DKTATLAS_NAME}.stats.

Curvature Statistics  (-<no>curvstats)

Runs mris_curvature_stats to create a summary file (stats/?h.curv.stats)
of cortical curvature statistics.

LONGITUDINAL PROCESSING

The longitudinal processing scheme aims to incorporate the subject-wise
correlation of longitudinal data into the processing stream in order to
increase sensitivity and repeatability, see [14-16]. Care is taken to
avoid introduction of asymmetry-induced bias.

Here is a summary of the longitudinal workflow, where tpN refers to the
name of one timepoint of subject data, and longbase refers to the name
given to the base subject of a collection of timepoints:

1) cross-sectionally process tpN subjects (the default workflow):
  recon-all -s tp1 -i path_to_tp1_dicom -all
  recon-all -s tp2 -i path_to_tp2_dicom -all

2) create and process the unbiased base (subject template):
  recon-all -base longbase -tp tp1 -tp tp2 -all

3) longitudinally process tpN subjects:
  recon-all -long tp1 longbase -all
  recon-all -long tp2 longbase -all

4) do comparisons on results from 3), e.g. calculate differences
between tp2.long.longbase - tp1.long.longbase

Note that the longitudinal processing stream always produces output subject
data containing  .long.  in the name (to help distinguish from the default
stream).

Notice that the -all flag is included in the -base and -long calls above.
A work directive flag is required.

Other flags:

-uselongbasectrlvol

With -long: Switch on use of control-points from the base in the long
runs for intensity normalization (T1.mgz).

-uselongbasewmedits

With -long: Optionally transfer WM edits from base/template.
Default: map WM edits from corresponding cross run.

-no-orig-pial

If the orig pial surface data is not available, then specify this flag so that
mris_make_surfaces does not attempt to use it.

-noasegfusion

Do not create 'fused' aseg from the longbase timepoints, which would normally
be used to initialize the ca_labeling.  Instead, initialize using the longbase
aseg.mgz.

-addtp

If a new timepoint needs to be added to a longitudinal run where a base subject
has already been created (from prior timepoints), then the -addtp command
can be added to the -long command in order to 'fix-up' the longitudinal
stream to accept the new timepoint. Note that the base subject is *not*
recomputed using the new timepoint. This potentially introduces a bias, and it
is recommended to NOT add a time point this way! Instead recreate the base
from all time points and run all longitudinals again.
See the LongitudinalProcessing wiki page.

Example:

  recon-all -long <tpNsubjid> <longbasesubjid> -addtp -all

In this example, 'tnNsubjid' is the subject name (assumed processed in the
cross-sectional stream) to add as a new timepoint and upon which to run
the longitudinal stream (creating <tpNsubjid>.long.<longbasesubjid>).



USING IMAGES FROM A 3T SCANNER 

The -3T flag enables two specific options in recon-all for images acquired with
a 3T scanner:  3T-specific NU intensity correction parameters are used in the 
Non-Uniform normalization stage, and the Schwartz 3T atlas is used for 
Talairach alignment.


T2 OR FLAIR TO IMPROVE PIAL SURFACES

Pial surfaces can be improved using the different contrast in T2 or FLAIR
images. The original pial surfaces without T2/FLAIR data are saved as  
?h.woT2.pial or ?h.woFLAIR.pial, and new ?h.pial surfaces are created.  One 
example where this is useful is when there is dura in the brainmask.mgz that 
isn't removed by skull stripping. The flags for these commands are:

  -T2 <input T2 volume>  or -FLAIR <input FLAIR volume> 
    (Specify the  path to the T2 or FLAIR image to use)
  -T2pial or -FLAIRpial 
    (Create new pial surfaces using T2 or FLAIR images)

An example of running a subject through Freesurfer with a T2 image is:
  
  recon-all -s subjectname -i /path/to/input -T2 /path/to/T2_input -T2pial -all

T2 or FLAIR images can also be used with Freesurfer subjects that have already
been processed without them. Note that autorecon3 should also be re-ran to 
compute statistics based on the new surfaces. For example:
  
  recon-all -s subjectname -T2 /path/to/T2_volume -T2pial -autorecon3


MANUAL CHECKING AND EDITING OF SURFACES

To manually edit segmenation, run the following command (make sure
that your SUBJECTS_DIR environment variable is properly set).

  tkmedit subjid wm.mgz -aux T1.mgz

The surfaces can be loaded through the menu item
File->LoadMainSurface. To enable editing, set Tools->EditVoxels.  It
may also be convenient to bring up the reconstruction toolbar with
View->ToolBars->Reconstruction. Alt-C toggles between the main (wm)
and auxiliary (T1) volumes. Middle clicking will set a voxel value to
255; left clicking will set a voxel value to 0. Only edit the wm
volume. When finished, File->SaveMainVolume.

To view the inflated surface simultaneosly with the volume, run the
following command from a different shell:

  tksurfer subjid lh inflated

To goto a point on the surface inside the volume, click on the point
and hit SavePoint (icon looks like a floppy disk), then, in tkmedit,
hit GotoSavedPoint (icon looks like an open file).

Be sure to see the tutorials found at:
https://surfer.nmr.mgh.harvard.edu/fswiki/FsTutorial


TOUCH FILES

This script creates a directory called "touch". Each time a stage is
run a "touch file" is created (eg, skull_strip.touch). This will be
used in the future to automatically determine which stages need to be
run or re-run. The modification time of the touch file is important.
The content is irrelevent, though it often contains a command-line.


FLATTENING

Flattening is not actually done in this script. This part just documents
how one would go about performing the flattening. First, load the subject
surface into tksurfer:

  tksurfer subjid lh inflated

Load the curvature through the File->Curvature->Load menu (load
lh.curv). This should show a green/red curvature pattern. Red = sulci.

Right click before making a cut; this will clear previous points. This
is needed because it will string together all the previous places you
have clicked to make the cut. To make a line cut, left click on a line
of points. Make the points fairly close together; if they are too far
appart, the cut fails. After making your line of points, execute the
cut by clicking on the Cut icon (scissors with an open triangle for a
line cut or scissors with a closed triangle for a closed cut). To make
a plane cut, left click on three points to define the plane, then left
click on the side to keep. Then hit the CutPlane icon.

Fill the patch. Left click in the part of the surface that you want to
form your patch. Then hit the Fill Uncut Area button (icon = filled
triangle). This will fill the patch with white. The non-patch area
will be unaccessible through the interface.  Save the patch through
File->Patch->SaveAs. For whole cortex, save it to something like
lh.cort.patch.3d. For occipital patches, save it to lh.occip.patch.3d.

Cd into the subject surf directory and run

  mris_flatten -w N -distances Size Radius lh.patch.3d lh.patch.flat

where N instructs mris_flatten to write out an intermediate surface
every N interations. This is only useful for making movies; otherwise
set N=0.  Size is maximum number of neighbors; Radius radius (mm) in
which to search for neighbors. In general, the more neighbors that are
taken into account, the less the metric distortion but the more
computationally intensive. Typical values are Size=12 for large
patches, and Size=20 for small patches. Radius is typically 7.
Note: flattening may take 12-24 hours to complete. The patch can be
viewed at any time by loading the subjects inflated surface, then
loading the patch through File->Patch->LoadPatch...


GETTING HELP

See https://surfer.nmr.mgh.harvard.edu
Send email to freesurfer@nmr.mgh.harvard.edu


REFERENCES

See https://www.zotero.org/freesurfer

[1] Collins, DL, Neelin, P., Peters, TM, and Evans, AC. (1994)
Automatic 3D Inter-Subject Registration of MR Volumetric Data in
Standardized Talairach Space, Journal of Computer Assisted Tomography,
18(2) p192-205, 1994 PMID: 8126267; UI: 94172121

[2] Cortical Surface-Based Analysis I: Segmentation and Surface
Reconstruction Dale, A.M., Fischl, Bruce, Sereno, M.I.,
(1999). Cortical Surface-Based Analysis I: Segmentation and Surface
Reconstruction.  NeuroImage 9(2):179-194

[3] Fischl, B.R., Sereno, M.I.,Dale, A. M.  (1999) Cortical
Surface-Based Analysis II: Inflation, Flattening, and Surface-Based
Coordinate System. NeuroImage, 9, 195-207.

[4] Fischl, Bruce, Sereno, M.I., Tootell, R.B.H., and Dale, A.M.,
(1999). High-resolution inter-subject averaging and a coordinate
system for the cortical surface. Human Brain Mapping, 8(4): 272-284

[5] Fischl, Bruce, and Dale, A.M., (2000).  Measuring the Thickness of
the Human Cerebral Cortex from Magnetic Resonance Images.  Proceedings
of the National Academy of Sciences, 97:11044-11049.

[6] Fischl, Bruce, Liu, Arthur, and Dale, A.M., (2001). Automated
Manifold Surgery: Constructing Geometrically Accurate and
Topologically Correct Models of the Human Cerebral Cortex. IEEE
Transactions on Medical Imaging, 20(1):70-80

[7] Non-Uniform Intensity Correction.
http://www.nitrc.org/projects/nu_correct/

[8] Fischl B, Salat DH, Busa E, Albert M, Dieterich M, Haselgrove C,
van der Kouwe A, Killiany R, Kennedy D, Klaveness S, Montillo A,
Makris N, Rosen B, Dale AM. Whole brain segmentation: automated
labeling of neuroanatomical structures in the human
brain. Neuron. 2002 Jan 31;33(3):341-55.

[9] Bruce Fischl, Andre van der Kouwe, Christophe Destrieux, Eric
Halgren, Florent Segonne, David H. Salat, Evelina Busa, Larry
J. Seidman, Jill Goldstein, David Kennedy, Verne Caviness, Nikos
Makris, Bruce Rosen, and Anders M. Dale.  Automatically Parcellating
the Human Cerebral Cortex. Cerebral Cortex January 2004; 14:11-22.

[10] Fischl B, Salat DH, van der Kouwe AJW, Makris N, Ségonne F, Dale
AM. Sequence-Independent  Segmentation of Magnetic Resonance Images.
NeuroImage 23 Suppl 1, S69-84.

[11] Segonne F, Dale, AM, Busa E, Glessner M, Salvolini U, Hahn HK,
Fischl B, A Hybrid Approach to the Skull-Stripping Problem in MRI.
NeuroImage, 22,  pp. 1160-1075, 2004

[12] Han et al.,  Reliability of MRI-derived measurements of human
cerebral cortical thickness: The effects of field strength, scanner
upgrade and manufacturer, (2006) NeuroImage, 32(1):180-194.

[13] Schaer et al., A Surface-based Approach to Quantify Local Cortical
Gyrification (2007) IEEE Transactions on Medical Imaging.

[14] Martin Reuter, H Diana Rosas, Bruce Fischl.
Highly Accurate Inverse Consistent Registration: A Robust Approach.
NeuroImage 53(4), 1181-1196, 2010. http://dx.doi.org/10.1016/j.neuroimage.2010.07.020

[15] Martin Reuter, Bruce Fischl.
Avoiding Asymmetry-Induced Bias in Longitudinal Image Processing.
NeuroImage 51(1), 19-21, 2011. http://dx.doi.org/10.1016/j.neuroimage.2011.02.076

[16] Martin Reuter, Nicholas J Schmansky, H Diana Rosas, Bruce Fischl.
Within-Subject Template Estimation for Unbiased Longitudinal Image Analysis.
NeuroImage 61(4), 1402-1418, 2012. http://dx.doi.org/10.1016/j.neuroimage.2012.02.084

[17] Iglesias, J.E., Augustinack, J.C., Nguyen, K., Player, C.M., Player, A., Wright,
M., Roy, N., Frosch, M.P., McKee, A.C., Wald, L.L., Fischl, B., and Van Leemput, K.,
A computational atlas of the hippocampal formation using ex vivo, ultra-high resolution
MRI: Application to adaptive segmentation of in vivo MRI.  Neuroimage 115, 2015, 117-137. 
http://dx.doi.org/10.1016/j.neuroimage.2015.04.042

[18] Iglesias, J.E., Van Leemput, K., Bhatt, P., Casillas, C., Dutt, S., Schuff, N.,
Truran-Sacrey, D., Boxer, A., and Fischl, B., Bayesian segmentation of brainstem 
structures in MRI. Neuroimage 113, 2015, 184-195.
http://dx.doi.org/10.1016/j.neuroimage.2015.02.065






mbp-elizaveta:TUTORIAL_DATA elizavetalavrova$ recon-all -skullstrip -subjid sample-001.mgz
ERROR: you do not have write permission to /Applications/freesurfer/subjects/sample-001.mgz
mbp-elizaveta:TUTORIAL_DATA elizavetalavrova$ recon-all -skullstrip sample-001.mgz
ERROR: Flag sample-001.mgz unrecognized.
-skullstrip sample-001.mgz
Darwin mbp-elizaveta.wireless.unimaas.local 18.2.0 Darwin Kernel Version 18.2.0: Thu Dec 20 20:46:53 PST 2018; root:xnu-4903.241.1~1/RELEASE_X86_64 x86_64

recon-all -s  exited with ERRORS at Thu Mar 21 15:50:52 CET 2019

For more details, see the log file 
To report a problem, see http://surfer.nmr.mgh.harvard.edu/fswiki/BugReporting

mbp-elizaveta:TUTORIAL_DATA elizavetalavrova$ recon-all  sample-001.mgz -skullstrip
ERROR: Flag sample-001.mgz unrecognized.
sample-001.mgz -skullstrip
Darwin mbp-elizaveta.wireless.unimaas.local 18.2.0 Darwin Kernel Version 18.2.0: Thu Dec 20 20:46:53 PST 2018; root:xnu-4903.241.1~1/RELEASE_X86_64 x86_64

recon-all -s  exited with ERRORS at Thu Mar 21 15:51:18 CET 2019

For more details, see the log file 
To report a problem, see http://surfer.nmr.mgh.harvard.edu/fswiki/BugReporting

mbp-elizaveta:TUTORIAL_DATA elizavetalavrova$ cd
mbp-elizaveta:~ elizavetalavrova$ mri_convert sample-001.mgz sample-001.nii.gz
mri_convert.bin sample-001.mgz sample-001.nii.gz 
$Id: mri_convert.c,v 1.226 2016/02/26 16:15:24 mreuter Exp $
reading from sample-001.mgz...
TR=7.25, TE=3.22, TI=600.00, flip angle=7.00
i_ras = (-0, -1, -0)
j_ras = (-0, 0, -1)
k_ras = (-1, 0, 0)
writing to sample-001.nii.gz...
mbp-elizaveta:~ elizavetalavrova$ recon-all -i sample-001.nii.gz -s bert -all
ERROR: You are trying to re-run an existing subject with (possibly)
 new input data (-i). If this is truly new input data, you should delete
 the subject folder and re-run, or specify a different subject name.
 If you are just continuing an analysis of an existing subject, then 
 omit all -i flags.
mbp-elizaveta:~ elizavetalavrova$ export SUBJECTS_DIR = /users/elizavetalavrova/
-bash: export: `=': not a valid identifier
-bash: export: `/users/elizavetalavrova/': not a valid identifier
mbp-elizaveta:~ elizavetalavrova$ export SUBJECTS_DIR=/users/elizavetalavrova/
mbp-elizaveta:~ elizavetalavrova$ recon-all -i sample-001.nii.gz -s bert -all
Subject Stamp: freesurfer-Darwin-OSX-stable-pub-v6.0.0-2beb96c
Current Stamp: freesurfer-Darwin-OSX-stable-pub-v6.0.0-2beb96c
INFO: SUBJECTS_DIR is /Users/elizavetalavrova
Actual FREESURFER_HOME /Applications/freesurfer
Darwin mbp-elizaveta.wireless.unimaas.local 18.2.0 Darwin Kernel Version 18.2.0: Thu Dec 20 20:46:53 PST 2018; root:xnu-4903.241.1~1/RELEASE_X86_64 x86_64
/Users/elizavetalavrova/bert
\n mri_convert /Users/elizavetalavrova/sample-001.nii.gz /Users/elizavetalavrova/bert/mri/orig/001.mgz \n
mri_convert.bin /Users/elizavetalavrova/sample-001.nii.gz /Users/elizavetalavrova/bert/mri/orig/001.mgz 
$Id: mri_convert.c,v 1.226 2016/02/26 16:15:24 mreuter Exp $
reading from /Users/elizavetalavrova/sample-001.nii.gz...
TR=7.25, TE=0.00, TI=0.00, flip angle=0.00
i_ras = (-0, -1, -0)
j_ras = (-0, 0, -1)
k_ras = (-1, 0, 0)
writing to /Users/elizavetalavrova/bert/mri/orig/001.mgz...
#--------------------------------------------
#@# MotionCor Thu Mar 21 15:53:28 CET 2019
Found 1 runs
/Users/elizavetalavrova/bert/mri/orig/001.mgz
Checking for (invalid) multi-frame inputs...
WARNING: only one run found. This is OK, but motion
correction cannot be performed on one run, so I'll
copy the run to rawavg and continue.
\n cp /Users/elizavetalavrova/bert/mri/orig/001.mgz /Users/elizavetalavrova/bert/mri/rawavg.mgz \n
/Users/elizavetalavrova/bert
\n mri_convert /Users/elizavetalavrova/bert/mri/rawavg.mgz /Users/elizavetalavrova/bert/mri/orig.mgz --conform \n
mri_convert.bin /Users/elizavetalavrova/bert/mri/rawavg.mgz /Users/elizavetalavrova/bert/mri/orig.mgz --conform 
$Id: mri_convert.c,v 1.226 2016/02/26 16:15:24 mreuter Exp $
reading from /Users/elizavetalavrova/bert/mri/rawavg.mgz...
TR=7.25, TE=0.00, TI=0.00, flip angle=0.00
i_ras = (-0, -1, -0)
j_ras = (-0, 0, -1)
k_ras = (-1, 0, 0)
changing data type from short to uchar (noscale = 0)...
MRIchangeType: Building histogram 
Reslicing using trilinear interpolation 
writing to /Users/elizavetalavrova/bert/mri/orig.mgz...
\n mri_add_xform_to_header -c /Users/elizavetalavrova/bert/mri/transforms/talairach.xfm /Users/elizavetalavrova/bert/mri/orig.mgz /Users/elizavetalavrova/bert/mri/orig.mgz \n
INFO: extension is mgz
#--------------------------------------------
#@# Talairach Thu Mar 21 15:53:37 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_nu_correct.mni --no-rescale --i orig.mgz --o orig_nu.mgz --n 1 --proto-iters 1000 --distance 50 \n
/Users/elizavetalavrova/bert/mri
/Applications/freesurfer/bin/mri_nu_correct.mni
--no-rescale --i orig.mgz --o orig_nu.mgz --n 1 --proto-iters 1000 --distance 50
nIters 1
$Id: FreeSurferEnv.csh,v 1.89 2016/06/09 14:54:31 zkaufman Exp $
Darwin mbp-elizaveta.wireless.unimaas.local 18.2.0 Darwin Kernel Version 18.2.0: Thu Dec 20 20:46:53 PST 2018; root:xnu-4903.241.1~1/RELEASE_X86_64 x86_64
Thu Mar 21 15:53:37 CET 2019
Program nu_correct, built from:
Package MNI N3, version 1.12.0, compiled by nicks@gust.nmr.mgh.harvard.edu (x86_64-apple-darwin11.4.2) on 2015-06-19 at 15:37:08
/usr/bin/bc
tmpdir is ./tmp.mri_nu_correct.mni.5227
/Users/elizavetalavrova/bert/mri
mri_convert orig.mgz ./tmp.mri_nu_correct.mni.5227/nu0.mnc -odt float
mri_convert.bin orig.mgz ./tmp.mri_nu_correct.mni.5227/nu0.mnc -odt float 
$Id: mri_convert.c,v 1.226 2016/02/26 16:15:24 mreuter Exp $
reading from orig.mgz...
TR=7.25, TE=0.00, TI=0.00, flip angle=0.00
i_ras = (-1, 0, 0)
j_ras = (0, 0, -1)
k_ras = (0, 1, 0)
changing data type from uchar to float (noscale = 0)...
writing to ./tmp.mri_nu_correct.mni.5227/nu0.mnc...
 
--------------------------------------------------------
Iteration 1 Thu Mar 21 15:53:39 CET 2019
nu_correct -clobber ./tmp.mri_nu_correct.mni.5227/nu0.mnc ./tmp.mri_nu_correct.mni.5227/nu1.mnc -tmpdir ./tmp.mri_nu_correct.mni.5227/0/ -iterations 1000 -distance 50
[elizavetalavrova@mbp-elizaveta.wireless.unimaas.local:/Users/elizavetalavrova/bert/mri/] [2019-03-21 15:53:39] running:
  /Applications/freesurfer/mni/bin/nu_estimate_np_and_em -parzen -log -sharpen 0.15 0.01 -iterations 1000 -stop 0.001 -shrink 4 -auto_mask -nonotify -b_spline 1.0e-7 -distance 50 -quiet -execute -clobber -nokeeptmp -tmpdir ./tmp.mri_nu_correct.mni.5227/0/ ./tmp.mri_nu_correct.mni.5227/nu0.mnc ./tmp.mri_nu_correct.mni.5227/nu1.imp

Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Number of iterations: 29 
CV of field change: 0.000957436
 
 
 
mri_convert ./tmp.mri_nu_correct.mni.5227/nu1.mnc orig_nu.mgz --like orig.mgz --conform
mri_convert.bin ./tmp.mri_nu_correct.mni.5227/nu1.mnc orig_nu.mgz --like orig.mgz --conform 
$Id: mri_convert.c,v 1.226 2016/02/26 16:15:24 mreuter Exp $
reading from ./tmp.mri_nu_correct.mni.5227/nu1.mnc...
TR=0.00, TE=0.00, TI=0.00, flip angle=0.00
i_ras = (-1, 0, 0)
j_ras = (0, 0, -1)
k_ras = (0, 1, 0)
INFO: transform src into the like-volume: orig.mgz
changing data type from float to uchar (noscale = 0)...
MRIchangeType: Building histogram 
writing to orig_nu.mgz...
 
 
Thu Mar 21 15:54:29 CET 2019
mri_nu_correct.mni done
\n talairach_avi --i orig_nu.mgz --xfm transforms/talairach.auto.xfm \n
talairach_avi log file is transforms/talairach_avi.log...
Started at Thu Mar 21 15:54:30 CET 2019
Ended   at Thu Mar 21 15:55:00 CET 2019
talairach_avi done
\n cp transforms/talairach.auto.xfm transforms/talairach.xfm \n
#--------------------------------------------
#@# Talairach Failure Detection Thu Mar 21 15:55:02 CET 2019
/Users/elizavetalavrova/bert/mri
\n talairach_afd -T 0.005 -xfm transforms/talairach.xfm \n
talairach_afd: Talairach Transform: transforms/talairach.xfm OK (p=0.7190, pval=0.4932 >= threshold=0.0050)
\n awk -f /Applications/freesurfer/bin/extract_talairach_avi_QA.awk /Users/elizavetalavrova/bert/mri/transforms/talairach_avi.log \n
\n tal_QC_AZS /Users/elizavetalavrova/bert/mri/transforms/talairach_avi.log \n
TalAviQA: 0.98348
z-score: 1
#--------------------------------------------
#@# Nu Intensity Correction Thu Mar 21 15:55:02 CET 2019
\n mri_nu_correct.mni --i orig.mgz --o nu.mgz --uchar transforms/talairach.xfm --n 2 \n
/Users/elizavetalavrova/bert/mri
/Applications/freesurfer/bin/mri_nu_correct.mni
--i orig.mgz --o nu.mgz --uchar transforms/talairach.xfm --n 2
nIters 2
$Id: FreeSurferEnv.csh,v 1.89 2016/06/09 14:54:31 zkaufman Exp $
Darwin mbp-elizaveta.wireless.unimaas.local 18.2.0 Darwin Kernel Version 18.2.0: Thu Dec 20 20:46:53 PST 2018; root:xnu-4903.241.1~1/RELEASE_X86_64 x86_64
Thu Mar 21 15:55:02 CET 2019
Program nu_correct, built from:
Package MNI N3, version 1.12.0, compiled by nicks@gust.nmr.mgh.harvard.edu (x86_64-apple-darwin11.4.2) on 2015-06-19 at 15:37:08
/usr/bin/bc
tmpdir is ./tmp.mri_nu_correct.mni.5868
/Users/elizavetalavrova/bert/mri
mri_convert orig.mgz ./tmp.mri_nu_correct.mni.5868/nu0.mnc -odt float
mri_convert.bin orig.mgz ./tmp.mri_nu_correct.mni.5868/nu0.mnc -odt float 
$Id: mri_convert.c,v 1.226 2016/02/26 16:15:24 mreuter Exp $
reading from orig.mgz...
TR=7.25, TE=0.00, TI=0.00, flip angle=0.00
i_ras = (-1, 0, 0)
j_ras = (0, 0, -1)
k_ras = (0, 1, 0)
changing data type from uchar to float (noscale = 0)...
writing to ./tmp.mri_nu_correct.mni.5868/nu0.mnc...
 
--------------------------------------------------------
Iteration 1 Thu Mar 21 15:55:04 CET 2019
nu_correct -clobber ./tmp.mri_nu_correct.mni.5868/nu0.mnc ./tmp.mri_nu_correct.mni.5868/nu1.mnc -tmpdir ./tmp.mri_nu_correct.mni.5868/0/
[elizavetalavrova@mbp-elizaveta.wireless.unimaas.local:/Users/elizavetalavrova/bert/mri/] [2019-03-21 15:55:04] running:
  /Applications/freesurfer/mni/bin/nu_estimate_np_and_em -parzen -log -sharpen 0.15 0.01 -iterations 50 -stop 0.001 -shrink 4 -auto_mask -nonotify -b_spline 1.0e-7 -distance 200 -quiet -execute -clobber -nokeeptmp -tmpdir ./tmp.mri_nu_correct.mni.5868/0/ ./tmp.mri_nu_correct.mni.5868/nu0.mnc ./tmp.mri_nu_correct.mni.5868/nu1.imp

Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Number of iterations: 23 
CV of field change: 0.000997107
 
 
--------------------------------------------------------
Iteration 2 Thu Mar 21 15:55:37 CET 2019
nu_correct -clobber ./tmp.mri_nu_correct.mni.5868/nu1.mnc ./tmp.mri_nu_correct.mni.5868/nu2.mnc -tmpdir ./tmp.mri_nu_correct.mni.5868/1/
[elizavetalavrova@mbp-elizaveta.wireless.unimaas.local:/Users/elizavetalavrova/bert/mri/] [2019-03-21 15:55:37] running:
  /Applications/freesurfer/mni/bin/nu_estimate_np_and_em -parzen -log -sharpen 0.15 0.01 -iterations 50 -stop 0.001 -shrink 4 -auto_mask -nonotify -b_spline 1.0e-7 -distance 200 -quiet -execute -clobber -nokeeptmp -tmpdir ./tmp.mri_nu_correct.mni.5868/1/ ./tmp.mri_nu_correct.mni.5868/nu1.mnc ./tmp.mri_nu_correct.mni.5868/nu2.imp

Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Processing:.................................................................Done
Number of iterations: 18 
CV of field change: 0.00095863
 
 
 
mri_binarize --i ./tmp.mri_nu_correct.mni.5868/nu2.mnc --min -1 --o ./tmp.mri_nu_correct.mni.5868/ones.mgz

$Id: mri_binarize.c,v 1.43 2016/06/09 20:46:21 greve Exp $
cwd /Users/elizavetalavrova/bert/mri
cmdline mri_binarize.bin --i ./tmp.mri_nu_correct.mni.5868/nu2.mnc --min -1 --o ./tmp.mri_nu_correct.mni.5868/ones.mgz 
sysname  Darwin
hostname mbp-elizaveta.wireless.unimaas.local
machine  x86_64
user     elizavetalavrova

input      ./tmp.mri_nu_correct.mni.5868/nu2.mnc
frame      0
nErode3d   0
nErode2d   0
output     ./tmp.mri_nu_correct.mni.5868/ones.mgz
Binarizing based on threshold
min        -1
max        +infinity
binval        1
binvalnot     0
fstart = 0, fend = 0, nframes = 1
Found 16777216 values in range
Counting number of voxels in first frame
Found 16777216 voxels in final mask
Count: 16777216 16777216.000000 16777216 100.000000
mri_binarize done
mri_segstats --id 1 --seg ./tmp.mri_nu_correct.mni.5868/ones.mgz --i orig.mgz --sum ./tmp.mri_nu_correct.mni.5868/sum.junk --avgwf ./tmp.mri_nu_correct.mni.5868/input.mean.dat

$Id: mri_segstats.c,v 1.121 2016/05/31 17:27:11 greve Exp $
cwd 
cmdline mri_segstats --id 1 --seg ./tmp.mri_nu_correct.mni.5868/ones.mgz --i orig.mgz --sum ./tmp.mri_nu_correct.mni.5868/sum.junk --avgwf ./tmp.mri_nu_correct.mni.5868/input.mean.dat 
sysname  Darwin
hostname mbp-elizaveta.wireless.unimaas.local
machine  x86_64
user     elizavetalavrova
UseRobust  0
Loading ./tmp.mri_nu_correct.mni.5868/ones.mgz
Loading orig.mgz
Voxel Volume is 1 mm^3
Generating list of segmentation ids
Found   1 segmentations
Computing statistics for each segmentation

Reporting on   1 segmentations
Using PrintSegStat
Computing spatial average of each frame
  0
Writing to ./tmp.mri_nu_correct.mni.5868/input.mean.dat
mri_segstats done
mri_segstats --id 1 --seg ./tmp.mri_nu_correct.mni.5868/ones.mgz --i ./tmp.mri_nu_correct.mni.5868/nu2.mnc --sum ./tmp.mri_nu_correct.mni.5868/sum.junk --avgwf ./tmp.mri_nu_correct.mni.5868/output.mean.dat

$Id: mri_segstats.c,v 1.121 2016/05/31 17:27:11 greve Exp $
cwd 
cmdline mri_segstats --id 1 --seg ./tmp.mri_nu_correct.mni.5868/ones.mgz --i ./tmp.mri_nu_correct.mni.5868/nu2.mnc --sum ./tmp.mri_nu_correct.mni.5868/sum.junk --avgwf ./tmp.mri_nu_correct.mni.5868/output.mean.dat 
sysname  Darwin
hostname mbp-elizaveta.wireless.unimaas.local
machine  x86_64
user     elizavetalavrova
UseRobust  0
Loading ./tmp.mri_nu_correct.mni.5868/ones.mgz
Loading ./tmp.mri_nu_correct.mni.5868/nu2.mnc
Voxel Volume is 1 mm^3
Generating list of segmentation ids
Found   1 segmentations
Computing statistics for each segmentation

Reporting on   1 segmentations
Using PrintSegStat
Computing spatial average of each frame
  0
Writing to ./tmp.mri_nu_correct.mni.5868/output.mean.dat
mri_segstats done
mris_calc -o ./tmp.mri_nu_correct.mni.5868/nu2.mnc ./tmp.mri_nu_correct.mni.5868/nu2.mnc mul 1.05123077215796365196
Saving result to './tmp.mri_nu_correct.mni.5868/nu2.mnc' (type = MINC )                       [ ok ]
mri_convert ./tmp.mri_nu_correct.mni.5868/nu2.mnc nu.mgz --like orig.mgz
mri_convert.bin ./tmp.mri_nu_correct.mni.5868/nu2.mnc nu.mgz --like orig.mgz 
$Id: mri_convert.c,v 1.226 2016/02/26 16:15:24 mreuter Exp $
reading from ./tmp.mri_nu_correct.mni.5868/nu2.mnc...
TR=0.00, TE=0.00, TI=0.00, flip angle=0.00
i_ras = (-1, 0, 0)
j_ras = (0, 0, -1)
k_ras = (0, 1, 0)
INFO: transform src into the like-volume: orig.mgz
writing to nu.mgz...
mri_make_uchar nu.mgz transforms/talairach.xfm nu.mgz
type change took 0 minutes and 7 seconds.
mapping (10, 162) to ( 3, 110)
 
 
Thu Mar 21 15:56:37 CET 2019
mri_nu_correct.mni done
\n mri_add_xform_to_header -c /Users/elizavetalavrova/bert/mri/transforms/talairach.xfm nu.mgz nu.mgz \n
INFO: extension is mgz
#--------------------------------------------
#@# Intensity Normalization Thu Mar 21 15:56:39 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_normalize -g 1 -mprage nu.mgz T1.mgz \n
using max gradient = 1.000
assuming input volume is MGH (Van der Kouwe) MP-RAGE
reading from nu.mgz...
normalizing image...
talairach transform
 1.10414  -0.00919  -0.01423  -5.36488;
-0.00769   0.94721   0.29028  -46.86255;
 0.01426  -0.25822   1.06262   24.15019;
 0.00000   0.00000   0.00000   1.00000;
processing without aseg, no1d=0
MRInormInit(): 
INFO: Modifying talairach volume c_(r,a,s) based on average_305
MRInormalize(): 
MRIsplineNormalize(): npeaks = 20
Starting OpenSpline(): npoints = 20
building Voronoi diagram...
performing soap bubble smoothing, sigma = 8...

Iterating 2 times
---------------------------------
3d normalization pass 1 of 2
white matter peak found at 110
white matter peak found at 105
gm peak at 57 (57), valley at 23 (23)
csf peak at 29, setting threshold to 47
building Voronoi diagram...
performing soap bubble smoothing, sigma = 8...
---------------------------------
3d normalization pass 2 of 2
white matter peak found at 110
white matter peak found at 110
gm peak at 55 (55), valley at 21 (21)
csf peak at 28, setting threshold to 46
building Voronoi diagram...
performing soap bubble smoothing, sigma = 8...
Done iterating ---------------------------------
writing output to T1.mgz
3D bias adjustment took 2 minutes and 17 seconds.
#--------------------------------------------
#@# Skull Stripping Thu Mar 21 15:58:57 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_em_register -rusage /Users/elizavetalavrova/bert/touch/rusage.mri_em_register.skull.dat -skull nu.mgz /Applications/freesurfer/average/RB_all_withskull_2016-05-10.vc700.gca transforms/talairach_with_skull.lta \n
aligning to atlas containing skull, setting unknown_nbr_spacing = 5

== Number of threads available to mri_em_register for OpenMP = 1 == 
reading 1 input volumes...
logging results to talairach_with_skull.log
reading '/Applications/freesurfer/average/RB_all_withskull_2016-05-10.vc700.gca'...
average std = 22.9   using min determinant for regularization = 52.6
0 singular and 9002 ill-conditioned covariance matrices regularized
reading 'nu.mgz'...
freeing gibbs priors...done.
accounting for voxel sizes in initial transform
bounding unknown intensity as < 8.7 or > 569.1 
total sample mean = 77.6 (1399 zeros)
************************************************
spacing=8, using 3243 sample points, tol=1.00e-05...
************************************************
register_mri: find_optimal_transform
find_optimal_transform: nsamples 3243, passno 0, spacing 8
resetting wm mean[0]: 100 --> 108
resetting gm mean[0]: 61 --> 61
input volume #1 is the most T1-like
using real data threshold=7.0
skull bounding box = (45, 45, 16) --> (211, 255, 239)
using (100, 115, 128) as brain centroid...
mean wm in atlas = 108, using box (80,89,100) --> (120, 140,155) to find MRI wm
before smoothing, mri peak at 104
robust fit to distribution - 104 +- 7.8
after smoothing, mri peak at 104, scaling input intensities by 1.038
scaling channel 0 by 1.03846
initial log_p = -4.419
************************************************
First Search limited to translation only.
************************************************
max log p =    -4.296256 @ (-9.091, -9.091, -9.091)
max log p =    -4.127731 @ (4.545, -4.545, -4.545)
max log p =    -4.079831 @ (2.273, -2.273, -2.273)
max log p =    -4.064560 @ (-1.136, 1.136, 3.409)
max log p =    -4.062497 @ (0.568, -0.568, -1.705)
max log p =    -4.062497 @ (0.000, 0.000, 0.000)
Found translation: (-2.8, -15.3, -14.2): log p = -4.062
****************************************
Nine parameter search.  iteration 0 nscales = 0 ...
****************************************
Result so far: scale 1.000: max_log_p=-3.783, old_max_log_p =-4.062 (thresh=-4.1)
 1.06375   0.00000   0.00000  -10.98281;
 0.00000   1.19413   0.31997  -69.83015;
 0.00000  -0.25882   0.96593   30.82699;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 1 nscales = 0 ...
****************************************
Result so far: scale 1.000: max_log_p=-3.783, old_max_log_p =-3.783 (thresh=-3.8)
 1.06375   0.00000   0.00000  -10.98281;
 0.00000   1.19413   0.31997  -69.83015;
 0.00000  -0.25882   0.96593   30.82699;
 0.00000   0.00000   0.00000   1.00000;
reducing scale to 0.2500
****************************************
Nine parameter search.  iteration 2 nscales = 1 ...
****************************************
Result so far: scale 0.250: max_log_p=-3.707, old_max_log_p =-3.783 (thresh=-3.8)
 1.10364   0.00000   0.00000  -16.07749;
 0.00000   1.17911   0.28395  -65.07129;
 0.00000  -0.21384   0.95729   25.23553;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 3 nscales = 1 ...
****************************************
Result so far: scale 0.250: max_log_p=-3.704, old_max_log_p =-3.707 (thresh=-3.7)
 1.08295   0.00000   0.00000  -13.43462;
 0.00000   1.15700   0.27862  -63.06043;
 0.00000  -0.21384   0.95729   25.23553;
 0.00000   0.00000   0.00000   1.00000;
reducing scale to 0.0625
****************************************
Nine parameter search.  iteration 4 nscales = 2 ...
****************************************
Result so far: scale 0.062: max_log_p=-3.673, old_max_log_p =-3.704 (thresh=-3.7)
 1.08603   0.03361   0.02572  -21.01215;
-0.03553   1.14546   0.31649  -60.98079;
-0.01743  -0.26094   0.94498   36.40415;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 5 nscales = 2 ...
****************************************
Result so far: scale 0.062: max_log_p=-3.672, old_max_log_p =-3.673 (thresh=-3.7)
 1.08730   0.03365   0.02575  -21.18310;
-0.03553   1.14546   0.31649  -60.98079;
-0.01743  -0.26094   0.94498   36.40415;
 0.00000   0.00000   0.00000   1.00000;
min search scale 0.025000 reached
***********************************************
Computing MAP estimate using 3243 samples...
***********************************************
dt = 5.00e-06, momentum=0.80, tol=1.00e-05
l_intensity = 1.0000
Aligning input volume to GCA...
Transform matrix
 1.08730   0.03365   0.02575  -21.18310;
-0.03553   1.14546   0.31649  -60.98079;
-0.01743  -0.26094   0.94498   36.40415;
 0.00000   0.00000   0.00000   1.00000;
nsamples 3243
Quasinewton: input matrix
 1.08730   0.03365   0.02575  -21.18310;
-0.03553   1.14546   0.31649  -60.98079;
-0.01743  -0.26094   0.94498   36.40415;
 0.00000   0.00000   0.00000   1.00000;
 IFLAG= -1  LINE SEARCH FAILED. SEE DOCUMENTATION OF ROUTINE MCSRCH ERROR RETURN OF LINE SEARCH: INFO= 4 POSSIBLE CAUSES: FUNCTION OR GRADIENT ARE INCORRECT OR INCORRECT TOLERANCESoutof QuasiNewtonEMA: 008: -log(p) =   -0.0  tol 0.000010
Resulting transform:
 1.08730   0.03365   0.02575  -21.18310;
-0.03553   1.14546   0.31649  -60.98079;
-0.01743  -0.26094   0.94498   36.40415;
 0.00000   0.00000   0.00000   1.00000;

pass 1, spacing 8: log(p) = -3.672 (old=-4.419)
transform before final EM align:
 1.08730   0.03365   0.02575  -21.18310;
-0.03553   1.14546   0.31649  -60.98079;
-0.01743  -0.26094   0.94498   36.40415;
 0.00000   0.00000   0.00000   1.00000;

**************************************************
 EM alignment process ...
 Computing final MAP estimate using 364799 samples. 
**************************************************
dt = 5.00e-06, momentum=0.80, tol=1.00e-07
l_intensity = 1.0000
Aligning input volume to GCA...
Transform matrix
 1.08730   0.03365   0.02575  -21.18310;
-0.03553   1.14546   0.31649  -60.98079;
-0.01743  -0.26094   0.94498   36.40415;
 0.00000   0.00000   0.00000   1.00000;
nsamples 364799
Quasinewton: input matrix
 1.08730   0.03365   0.02575  -21.18310;
-0.03553   1.14546   0.31649  -60.98079;
-0.01743  -0.26094   0.94498   36.40415;
 0.00000   0.00000   0.00000   1.00000;
 IFLAG= -1  LINE SEARCH FAILED. SEE DOCUMENTATION OF ROUTINE MCSRCH ERROR RETURN OF LINE SEARCH: INFO= 6 POSSIBLE CAUSES: FUNCTION OR GRADIENT ARE INCORRECT OR INCORRECT TOLERANCESoutof QuasiNewtonEMA: 010: -log(p) =    4.1  tol 0.000000
final transform:
 1.08730   0.03365   0.02575  -21.18310;
-0.03553   1.14546   0.31649  -60.98079;
-0.01743  -0.26094   0.94498   36.40415;
 0.00000   0.00000   0.00000   1.00000;

writing output transformation to transforms/talairach_with_skull.lta...
mri_em_register utimesec    663.056907
mri_em_register stimesec    1.121034
mri_em_register ru_maxrss   480325632
mri_em_register ru_ixrss    0
mri_em_register ru_idrss    0
mri_em_register ru_isrss    0
mri_em_register ru_minflt   124781
mri_em_register ru_majflt   119
mri_em_register ru_nswap    0
mri_em_register ru_inblock  0
mri_em_register ru_oublock  0
mri_em_register ru_msgsnd   0
mri_em_register ru_msgrcv   0
mri_em_register ru_nsignals 0
mri_em_register ru_nvcsw    2
mri_em_register ru_nivcsw   163087
registration took 11 minutes and 6 seconds.
\n mri_watershed -rusage /Users/elizavetalavrova/bert/touch/rusage.mri_watershed.dat -T1 -brain_atlas /Applications/freesurfer/average/RB_all_withskull_2016-05-10.vc700.gca transforms/talairach_with_skull.lta T1.mgz brainmask.auto.mgz \n

Mode:          T1 normalized volume
Mode:          Use the information of atlas (default parms, --help for details)

*********************************************************
The input file is T1.mgz
The output file is brainmask.auto.mgz
Weighting the input with atlas information before watershed

*************************WATERSHED**************************
Sorting...
      first estimation of the COG coord: x=128 y=121 z=119 r=89
      first estimation of the main basin volume: 2978147 voxels
      Looking for seedpoints 
        2 found in the cerebellum 
        17 found in the rest of the brain 
      global maximum in x=150, y=120, z=77, Imax=255
      CSF=14, WM_intensity=110, WM_VARIANCE=5
      WM_MIN=110, WM_HALF_MIN=110, WM_HALF_MAX=110, WM_MAX=110 
      preflooding height equal to 10 percent
done.
Analyze...

      main basin size=2671206108215496 voxels, voxel volume =1.000 
                     = 2671206108215496 mmm3 = 2671206054494.208 cm3
done.
PostAnalyze...Basin Prior
 126 basins merged thanks to atlas 
      ***** 0 basin(s) merged in 1 iteration(s)
      ***** 0 voxel(s) added to the main basin
done.
Weighting the input with prior template 

****************TEMPLATE DEFORMATION****************

      second estimation of the COG coord: x=128,y=128, z=112, r=10567 iterations
^^^^^^^^ couldn't find WM with original limits - expanding ^^^^^^

   GLOBAL      CSF_MIN=0, CSF_intensity=9, CSF_MAX=46 , nb = 41806
  RIGHT_CER    CSF_MIN=1, CSF_intensity=2, CSF_MAX=37 , nb = 1090818677
  LEFT_CER     CSF_MIN=1, CSF_intensity=2, CSF_MAX=24 , nb = 1108189583
 RIGHT_BRAIN   CSF_MIN=0, CSF_intensity=9, CSF_MAX=43 , nb = -1030132012
 LEFT_BRAIN    CSF_MIN=0, CSF_intensity=9, CSF_MAX=41 , nb = 18047
    OTHER      CSF_MIN=1, CSF_intensity=2, CSF_MAX=19 , nb = 1092616822
 Problem with the least square interpolation in GM_MIN calculation.
   
                     CSF_MAX  TRANSITION  GM_MIN  GM
    GLOBAL     
  before analyzing :    46,      37,        33,   54
  after  analyzing :    29,      37,        37,   41
   RIGHT_CER   
  before analyzing :    37,      38,        39,   55
  after  analyzing :    37,      38,        39,   42
   LEFT_CER    
  before analyzing :    24,      29,        35,   55
  after  analyzing :    24,      33,        35,   38
  RIGHT_BRAIN  
  before analyzing :    43,      36,        32,   53
  after  analyzing :    29,      36,        36,   40
  LEFT_BRAIN   
  before analyzing :    41,      35,        31,   54
  after  analyzing :    28,      35,        35,   39
     OTHER     
  before analyzing :    19,      39,        70,   95
  after  analyzing :    19,      59,        70,   68
      mri_strip_skull: done peeling brain
      highly tesselated surface with 10242 vertices
      matching...65 iterations

*********************VALIDATION*********************
curvature mean = -0.013, std = 0.011
curvature mean = 70.195, std = 8.289

No Rigid alignment: -atlas Mode Off (basic atlas / no registration)
      before rotation: sse = 0.85, sigma = 1.43
      after  rotation: sse = 0.85, sigma = 1.43
Localization of inacurate regions: Erosion-Dilation steps
      the sse mean is  0.85, its var is  1.11   
      before Erosion-Dilatation  0.00% of inacurate vertices
      after  Erosion-Dilatation  0.00% of inacurate vertices
      Validation of the shape of the surface done.
Scaling of atlas fields onto current surface fields

********FINAL ITERATIVE TEMPLATE DEFORMATION********
Compute Local values csf/gray
Fine Segmentation...39 iterations

      mri_strip_skull: done peeling brain

Brain Size = 1668659 voxels, voxel volume = 1.000 mm3
           = 1668659 mmm3 = 1668.659 cm3


******************************
Saving brainmask.auto.mgz
done
mri_watershed utimesec    26.482424
mri_watershed stimesec    0.345186
mri_watershed ru_maxrss   724328448
mri_watershed ru_ixrss    0
mri_watershed ru_idrss    0
mri_watershed ru_isrss    0
mri_watershed ru_minflt   207296
mri_watershed ru_majflt   139
mri_watershed ru_nswap    0
mri_watershed ru_inblock  0
mri_watershed ru_oublock  0
mri_watershed ru_msgsnd   0
mri_watershed ru_msgrcv   0
mri_watershed ru_nsignals 0
mri_watershed ru_nvcsw    15
mri_watershed ru_nivcsw   1354
mri_watershed done
\n cp brainmask.auto.mgz brainmask.mgz \n
#-------------------------------------
#@# EM Registration Thu Mar 21 16:10:30 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_em_register -rusage /Users/elizavetalavrova/bert/touch/rusage.mri_em_register.dat -uns 3 -mask brainmask.mgz nu.mgz /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca transforms/talairach.lta \n
setting unknown_nbr_spacing = 3
using MR volume brainmask.mgz to mask input volume...

== Number of threads available to mri_em_register for OpenMP = 1 == 
reading 1 input volumes...
logging results to talairach.log
reading '/Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca'...
average std = 7.3   using min determinant for regularization = 5.3
0 singular and 841 ill-conditioned covariance matrices regularized
reading 'nu.mgz'...
freeing gibbs priors...done.
accounting for voxel sizes in initial transform
bounding unknown intensity as < 6.3 or > 503.7 
total sample mean = 78.8 (1011 zeros)
************************************************
spacing=8, using 2830 sample points, tol=1.00e-05...
************************************************
register_mri: find_optimal_transform
find_optimal_transform: nsamples 2830, passno 0, spacing 8
resetting wm mean[0]: 98 --> 107
resetting gm mean[0]: 61 --> 61
input volume #1 is the most T1-like
using real data threshold=23.9
skull bounding box = (64, 70, 37) --> (191, 210, 204)
using (106, 117, 121) as brain centroid...
mean wm in atlas = 107, using box (90,100,100) --> (121, 134,141) to find MRI wm
before smoothing, mri peak at 104
robust fit to distribution - 105 +- 7.0
after smoothing, mri peak at 105, scaling input intensities by 1.019
scaling channel 0 by 1.01905
initial log_p = -4.094
************************************************
First Search limited to translation only.
************************************************
max log p =    -3.949484 @ (-9.091, -9.091, -9.091)
max log p =    -3.852388 @ (4.545, 4.545, -4.545)
max log p =    -3.718939 @ (2.273, -6.818, 2.273)
max log p =    -3.710421 @ (-1.136, 1.136, 1.136)
max log p =    -3.668775 @ (1.705, 1.705, -0.568)
max log p =    -3.668775 @ (0.000, 0.000, 0.000)
Found translation: (-1.7, -8.5, -10.8): log p = -3.669
****************************************
Nine parameter search.  iteration 0 nscales = 0 ...
****************************************
Result so far: scale 1.000: max_log_p=-3.457, old_max_log_p =-3.669 (thresh=-3.7)
 1.15000   0.00000   0.00000  -20.97079;
 0.00000   1.11081   0.29764  -57.28410;
 0.00000  -0.23650   0.88261   40.57657;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 1 nscales = 0 ...
****************************************
Result so far: scale 1.000: max_log_p=-3.441, old_max_log_p =-3.457 (thresh=-3.5)
 1.06375   0.00000   0.00000  -9.89270;
 0.00000   1.11081   0.29764  -57.28410;
 0.00000  -0.25423   0.94881   35.71148;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 2 nscales = 0 ...
****************************************
Result so far: scale 1.000: max_log_p=-3.434, old_max_log_p =-3.441 (thresh=-3.4)
 1.06375   0.00000   0.00000  -9.89270;
 0.00000   1.13450   0.17125  -46.67152;
 0.00000  -0.09904   0.90608   12.67430;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 3 nscales = 0 ...
****************************************
Result so far: scale 1.000: max_log_p=-3.375, old_max_log_p =-3.434 (thresh=-3.4)
 1.06375   0.00000   0.00000  -9.89270;
 0.00000   1.11186   0.28805  -57.36063;
 0.00000  -0.26474   0.94167   37.35673;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 4 nscales = 0 ...
****************************************
Result so far: scale 1.000: max_log_p=-3.375, old_max_log_p =-3.375 (thresh=-3.4)
 1.06375   0.00000   0.00000  -9.89270;
 0.00000   1.11186   0.28805  -57.36063;
 0.00000  -0.26474   0.94167   37.35673;
 0.00000   0.00000   0.00000   1.00000;
reducing scale to 0.2500
****************************************
Nine parameter search.  iteration 5 nscales = 1 ...
****************************************
Result so far: scale 0.250: max_log_p=-3.218, old_max_log_p =-3.375 (thresh=-3.4)
 1.08179   0.02756   0.03730  -19.87684;
-0.03677   1.09779   0.25095  -46.75553;
-0.03679  -0.22366   0.93160   35.93835;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 6 nscales = 1 ...
****************************************
Result so far: scale 0.250: max_log_p=-3.204, old_max_log_p =-3.218 (thresh=-3.2)
 1.08241  -0.00837   0.02907  -14.36548;
-0.00138   1.11870   0.25677  -54.66531;
-0.03748  -0.22786   0.94907   32.76012;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 7 nscales = 1 ...
****************************************
Result so far: scale 0.250: max_log_p=-3.204, old_max_log_p =-3.204 (thresh=-3.2)
 1.08241  -0.00837   0.02907  -14.36548;
-0.00138   1.11870   0.25677  -54.66531;
-0.03748  -0.22786   0.94907   32.76012;
 0.00000   0.00000   0.00000   1.00000;
reducing scale to 0.0625
****************************************
Nine parameter search.  iteration 8 nscales = 2 ...
****************************************
Result so far: scale 0.062: max_log_p=-3.175, old_max_log_p =-3.204 (thresh=-3.2)
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;
****************************************
Nine parameter search.  iteration 9 nscales = 2 ...
****************************************
Result so far: scale 0.062: max_log_p=-3.175, old_max_log_p =-3.175 (thresh=-3.2)
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;
min search scale 0.025000 reached
***********************************************
Computing MAP estimate using 2830 samples...
***********************************************
dt = 5.00e-06, momentum=0.80, tol=1.00e-05
l_intensity = 1.0000
Aligning input volume to GCA...
Transform matrix
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;
nsamples 2830
Quasinewton: input matrix
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;
 IFLAG= -1  LINE SEARCH FAILED. SEE DOCUMENTATION OF ROUTINE MCSRCH ERROR RETURN OF LINE SEARCH: INFO= 4 POSSIBLE CAUSES: FUNCTION OR GRADIENT ARE INCORRECT OR INCORRECT TOLERANCESoutof QuasiNewtonEMA: 012: -log(p) =   -0.0  tol 0.000010
Resulting transform:
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;

pass 1, spacing 8: log(p) = -3.175 (old=-4.094)
transform before final EM align:
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;

**************************************************
 EM alignment process ...
 Computing final MAP estimate using 315557 samples. 
**************************************************
dt = 5.00e-06, momentum=0.80, tol=1.00e-07
l_intensity = 1.0000
Aligning input volume to GCA...
Transform matrix
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;
nsamples 315557
Quasinewton: input matrix
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;
 IFLAG= -1  LINE SEARCH FAILED. SEE DOCUMENTATION OF ROUTINE MCSRCH ERROR RETURN OF LINE SEARCH: INFO= 6 POSSIBLE CAUSES: FUNCTION OR GRADIENT ARE INCORRECT OR INCORRECT TOLERANCESoutof QuasiNewtonEMA: 014: -log(p) =    3.7  tol 0.000000
final transform:
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;

writing output transformation to transforms/talairach.lta...
mri_em_register utimesec    932.505830
mri_em_register stimesec    0.605492
mri_em_register ru_maxrss   485031936
mri_em_register ru_ixrss    0
mri_em_register ru_idrss    0
mri_em_register ru_isrss    0
mri_em_register ru_minflt   125617
mri_em_register ru_majflt   0
mri_em_register ru_nswap    0
mri_em_register ru_inblock  0
mri_em_register ru_oublock  0
mri_em_register ru_msgsnd   0
mri_em_register ru_msgrcv   0
mri_em_register ru_nsignals 0
mri_em_register ru_nvcsw    2
mri_em_register ru_nivcsw   24901
registration took 15 minutes and 33 seconds.
#--------------------------------------
#@# CA Normalize Thu Mar 21 16:26:04 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_ca_normalize -c ctrl_pts.mgz -mask brainmask.mgz nu.mgz /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca transforms/talairach.lta norm.mgz \n
writing control point volume to ctrl_pts.mgz
using MR volume brainmask.mgz to mask input volume...
reading 1 input volume
reading atlas from '/Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca'...
reading transform from 'transforms/talairach.lta'...
reading input volume from nu.mgz...
resetting wm mean[0]: 98 --> 107
resetting gm mean[0]: 61 --> 61
input volume #1 is the most T1-like
using real data threshold=23.9
skull bounding box = (64, 70, 37) --> (191, 210, 204)
using (106, 117, 121) as brain centroid...
mean wm in atlas = 107, using box (90,100,100) --> (121, 134,141) to find MRI wm
before smoothing, mri peak at 104
robust fit to distribution - 105 +- 7.0
after smoothing, mri peak at 105, scaling input intensities by 1.019
scaling channel 0 by 1.01905
using 246344 sample points...
INFO: compute sample coordinates transform
 1.08201  -0.00123   0.03908  -16.84014;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;
INFO: transform used
finding control points in Left_Cerebral_White_Matter....
found 39915 control points for structure...
bounding box (128, 71, 34) --> (190, 174, 203)
Left_Cerebral_White_Matter: limiting intensities to 102.0 --> 132.0
0 of 8 (0.0%) samples deleted
finding control points in Right_Cerebral_White_Matter....
found 39557 control points for structure...
bounding box (69, 71, 32) --> (129, 170, 202)
Right_Cerebral_White_Matter: limiting intensities to 100.0 --> 132.0
0 of 24 (0.0%) samples deleted
finding control points in Left_Cerebellum_White_Matter....
found 3059 control points for structure...
bounding box (131, 152, 64) --> (175, 190, 119)
Left_Cerebellum_White_Matter: limiting intensities to 103.0 --> 132.0
8 of 21 (38.1%) samples deleted
finding control points in Right_Cerebellum_White_Matter....
found 2705 control points for structure...
bounding box (88, 152, 59) --> (130, 188, 118)
Right_Cerebellum_White_Matter: limiting intensities to 101.0 --> 132.0
3 of 7 (42.9%) samples deleted
finding control points in Brain_Stem....
found 3518 control points for structure...
bounding box (113, 139, 99) --> (145, 201, 130)
Brain_Stem: limiting intensities to 103.0 --> 132.0
7 of 9 (77.8%) samples deleted
using 69 total control points for intensity normalization...
bias field = 0.892 +- 0.094
0 of 51 control points discarded
finding control points in Left_Cerebral_White_Matter....
found 39915 control points for structure...
bounding box (128, 71, 34) --> (190, 174, 203)
Left_Cerebral_White_Matter: limiting intensities to 88.0 --> 132.0
0 of 161 (0.0%) samples deleted
finding control points in Right_Cerebral_White_Matter....
found 39557 control points for structure...
bounding box (69, 71, 32) --> (129, 170, 202)
Right_Cerebral_White_Matter: limiting intensities to 90.0 --> 132.0
0 of 138 (0.0%) samples deleted
finding control points in Left_Cerebellum_White_Matter....
found 3059 control points for structure...
bounding box (131, 152, 64) --> (175, 190, 119)
Left_Cerebellum_White_Matter: limiting intensities to 88.0 --> 132.0
26 of 53 (49.1%) samples deleted
finding control points in Right_Cerebellum_White_Matter....
found 2705 control points for structure...
bounding box (88, 152, 59) --> (130, 188, 118)
Right_Cerebellum_White_Matter: limiting intensities to 88.0 --> 132.0
32 of 45 (71.1%) samples deleted
finding control points in Brain_Stem....
found 3518 control points for structure...
bounding box (113, 139, 99) --> (145, 201, 130)
Brain_Stem: limiting intensities to 89.0 --> 132.0
88 of 96 (91.7%) samples deleted
using 493 total control points for intensity normalization...
bias field = 1.022 +- 0.060
0 of 345 control points discarded
finding control points in Left_Cerebral_White_Matter....
found 39915 control points for structure...
bounding box (128, 71, 34) --> (190, 174, 203)
Left_Cerebral_White_Matter: limiting intensities to 88.0 --> 132.0
12 of 283 (4.2%) samples deleted
finding control points in Right_Cerebral_White_Matter....
found 39557 control points for structure...
bounding box (69, 71, 32) --> (129, 170, 202)
Right_Cerebral_White_Matter: limiting intensities to 88.0 --> 132.0
4 of 252 (1.6%) samples deleted
finding control points in Left_Cerebellum_White_Matter....
found 3059 control points for structure...
bounding box (131, 152, 64) --> (175, 190, 119)
Left_Cerebellum_White_Matter: limiting intensities to 88.0 --> 132.0
37 of 65 (56.9%) samples deleted
finding control points in Right_Cerebellum_White_Matter....
found 2705 control points for structure...
bounding box (88, 152, 59) --> (130, 188, 118)
Right_Cerebellum_White_Matter: limiting intensities to 88.0 --> 132.0
71 of 84 (84.5%) samples deleted
finding control points in Brain_Stem....
found 3518 control points for structure...
bounding box (113, 139, 99) --> (145, 201, 130)
Brain_Stem: limiting intensities to 88.0 --> 132.0
108 of 130 (83.1%) samples deleted
using 814 total control points for intensity normalization...
bias field = 1.015 +- 0.055
0 of 577 control points discarded
writing normalized volume to norm.mgz...
writing control points to ctrl_pts.mgz
freeing GCA...done.
normalization took 1 minutes and 30 seconds.
#--------------------------------------
#@# CA Reg Thu Mar 21 16:27:34 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_ca_register -rusage /Users/elizavetalavrova/bert/touch/rusage.mri_ca_register.dat -nobigventricles -T transforms/talairach.lta -align-after -mask brainmask.mgz norm.mgz /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca transforms/talairach.m3z \n
not handling expanded ventricles...
using previously computed transform transforms/talairach.lta
renormalizing sequences with structure alignment, equivalent to:
	-renormalize
	-regularize_mean 0.500
	-regularize 0.500
using MR volume brainmask.mgz to mask input volume...

== Number of threads available to mri_ca_register for OpenMP = 1 == 
reading 1 input volumes...
logging results to talairach.log
reading input volume 'norm.mgz'...
reading GCA '/Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca'...
label assignment complete, 0 changed (0.00%)
det(m_affine) = 1.21 (predicted orig area = 6.6)
label assignment complete, 0 changed (0.00%)
freeing gibbs priors...done.
average std[0] = 5.0
**************** pass 1 of 1 ************************
enabling zero nodes
setting smoothness coefficient to 0.039
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.781, neg=0, invalid=762
0001: dt=180.515195, rms=0.740 (5.237%), neg=0, invalid=762
0002: dt=158.013793, rms=0.727 (1.820%), neg=0, invalid=762
0003: dt=175.881481, rms=0.718 (1.214%), neg=0, invalid=762
0004: dt=147.200000, rms=0.713 (0.686%), neg=0, invalid=762
0005: dt=369.920000, rms=0.707 (0.845%), neg=0, invalid=762
0006: dt=94.006557, rms=0.703 (0.634%), neg=0, invalid=762
0007: dt=2071.552000, rms=0.687 (2.215%), neg=0, invalid=762
0008: dt=129.472000, rms=0.685 (0.239%), neg=0, invalid=762
0009: dt=129.472000, rms=0.684 (0.206%), neg=0, invalid=762
0010: dt=129.472000, rms=0.682 (0.260%), neg=0, invalid=762
0011: dt=129.472000, rms=0.680 (0.262%), neg=0, invalid=762
0012: dt=129.472000, rms=0.679 (0.193%), neg=0, invalid=762
0013: dt=129.472000, rms=0.678 (0.213%), neg=0, invalid=762
0014: dt=129.472000, rms=0.676 (0.244%), neg=0, invalid=762
0015: dt=129.472000, rms=0.674 (0.263%), neg=0, invalid=762
0016: dt=129.472000, rms=0.672 (0.249%), neg=0, invalid=762
0017: dt=129.472000, rms=0.671 (0.238%), neg=0, invalid=762
0018: dt=129.472000, rms=0.669 (0.245%), neg=0, invalid=762
0019: dt=129.472000, rms=0.668 (0.206%), neg=0, invalid=762
0020: dt=129.472000, rms=0.667 (0.175%), neg=0, invalid=762
0021: dt=129.472000, rms=0.666 (0.143%), neg=0, invalid=762
0022: dt=129.472000, rms=0.665 (0.141%), neg=0, invalid=762
0023: dt=129.472000, rms=0.664 (0.132%), neg=0, invalid=762
0024: dt=129.472000, rms=0.663 (0.114%), neg=0, invalid=762
0025: dt=129.472000, rms=0.662 (0.119%), neg=0, invalid=762
0026: dt=129.472000, rms=0.662 (0.131%), neg=0, invalid=762
0027: dt=129.472000, rms=0.661 (0.127%), neg=0, invalid=762
0028: dt=129.472000, rms=0.660 (0.105%), neg=0, invalid=762
0029: dt=129.472000, rms=0.659 (0.094%), neg=0, invalid=762
0030: dt=369.920000, rms=0.659 (0.024%), neg=0, invalid=762
0031: dt=369.920000, rms=0.659 (-0.050%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.660, neg=0, invalid=762
0032: dt=129.472000, rms=0.659 (0.207%), neg=0, invalid=762
0033: dt=517.888000, rms=0.657 (0.167%), neg=0, invalid=762
0034: dt=517.888000, rms=0.657 (-0.329%), neg=0, invalid=762
setting smoothness coefficient to 0.154
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.663, neg=0, invalid=762
0035: dt=130.966887, rms=0.657 (0.879%), neg=0, invalid=762
0036: dt=134.301538, rms=0.652 (0.813%), neg=0, invalid=762
0037: dt=84.119488, rms=0.647 (0.623%), neg=0, invalid=762
0038: dt=99.018868, rms=0.645 (0.384%), neg=0, invalid=762
0039: dt=105.830065, rms=0.642 (0.456%), neg=0, invalid=762
0040: dt=72.117073, rms=0.640 (0.309%), neg=0, invalid=762
0041: dt=145.152000, rms=0.638 (0.358%), neg=0, invalid=762
0042: dt=67.034483, rms=0.636 (0.278%), neg=0, invalid=762
0043: dt=145.152000, rms=0.634 (0.289%), neg=0, invalid=762
0044: dt=67.863517, rms=0.633 (0.222%), neg=0, invalid=762
0045: dt=67.863517, rms=0.632 (0.150%), neg=0, invalid=762
0046: dt=67.863517, rms=0.630 (0.238%), neg=0, invalid=762
0047: dt=67.863517, rms=0.628 (0.377%), neg=0, invalid=762
0048: dt=67.863517, rms=0.625 (0.405%), neg=0, invalid=762
0049: dt=67.863517, rms=0.623 (0.447%), neg=0, invalid=762
0050: dt=67.863517, rms=0.620 (0.403%), neg=0, invalid=762
0051: dt=67.863517, rms=0.618 (0.408%), neg=0, invalid=762
0052: dt=67.863517, rms=0.615 (0.360%), neg=0, invalid=762
0053: dt=67.863517, rms=0.613 (0.298%), neg=0, invalid=762
0054: dt=67.863517, rms=0.612 (0.264%), neg=0, invalid=762
0055: dt=67.863517, rms=0.610 (0.232%), neg=0, invalid=762
0056: dt=67.863517, rms=0.609 (0.219%), neg=0, invalid=762
0057: dt=67.863517, rms=0.608 (0.170%), neg=0, invalid=762
0058: dt=67.863517, rms=0.607 (0.166%), neg=0, invalid=762
0059: dt=67.863517, rms=0.606 (0.164%), neg=0, invalid=762
0060: dt=67.863517, rms=0.605 (0.148%), neg=0, invalid=762
0061: dt=67.863517, rms=0.604 (0.132%), neg=0, invalid=762
0062: dt=67.863517, rms=0.604 (0.121%), neg=0, invalid=762
0063: dt=67.863517, rms=0.603 (0.113%), neg=0, invalid=762
0064: dt=103.680000, rms=0.603 (0.040%), neg=0, invalid=762
0065: dt=103.680000, rms=0.603 (-0.051%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.603, neg=0, invalid=762
0066: dt=89.125926, rms=0.602 (0.305%), neg=0, invalid=762
0067: dt=124.416000, rms=0.601 (0.115%), neg=0, invalid=762
0068: dt=124.416000, rms=0.601 (-0.169%), neg=0, invalid=762
setting smoothness coefficient to 0.588
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.621, neg=0, invalid=762
0069: dt=0.000000, rms=0.621 (0.111%), neg=0, invalid=762
0070: dt=0.000000, rms=0.621 (0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.621, neg=0, invalid=762
0071: dt=0.175000, rms=0.621 (0.111%), neg=0, invalid=762
0072: dt=0.000000, rms=0.621 (0.001%), neg=0, invalid=762
0073: dt=0.250000, rms=0.621 (-0.000%), neg=0, invalid=762
setting smoothness coefficient to 2.000
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.681, neg=0, invalid=762
0074: dt=5.215686, rms=0.662 (2.807%), neg=0, invalid=762
0075: dt=2.304000, rms=0.661 (0.089%), neg=0, invalid=762
0076: dt=2.304000, rms=0.661 (-0.031%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.662, neg=0, invalid=762
0077: dt=0.000000, rms=0.661 (0.086%), neg=0, invalid=762
0078: dt=0.000000, rms=0.661 (0.000%), neg=0, invalid=762
setting smoothness coefficient to 5.000
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.718, neg=0, invalid=762
0079: dt=1.536000, rms=0.712 (0.781%), neg=0, invalid=762
0080: dt=1.981132, rms=0.707 (0.815%), neg=0, invalid=762
0081: dt=0.384000, rms=0.706 (0.026%), neg=0, invalid=762
0082: dt=0.384000, rms=0.706 (0.015%), neg=0, invalid=762
0083: dt=0.384000, rms=0.706 (-0.008%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.707, neg=0, invalid=762
0084: dt=1.280000, rms=0.705 (0.263%), neg=0, invalid=762
0085: dt=1.280000, rms=0.704 (0.090%), neg=0, invalid=762
0086: dt=1.280000, rms=0.704 (0.029%), neg=0, invalid=762
0087: dt=1.280000, rms=0.704 (-0.075%), neg=0, invalid=762
resetting metric properties...
setting smoothness coefficient to 10.000
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.672, neg=0, invalid=762
0088: dt=0.916070, rms=0.650 (3.283%), neg=0, invalid=762
0089: dt=0.080000, rms=0.649 (0.163%), neg=0, invalid=762
0090: dt=0.080000, rms=0.649 (-0.087%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.649, neg=0, invalid=762
0091: dt=0.028000, rms=0.648 (0.109%), neg=0, invalid=762
0092: dt=0.007000, rms=0.648 (0.001%), neg=0, invalid=762
0093: dt=0.007000, rms=0.648 (-0.002%), neg=0, invalid=762
renormalizing by structure alignment....
renormalizing input #0
gca peak = 0.10027 (20)
mri peak = 0.15314 ( 8)
Left_Lateral_Ventricle (4): linear fit = 0.44 x + 0.0 (251 voxels, overlap=0.115)
Left_Lateral_Ventricle (4): linear fit = 0.44 x + 0.0 (251 voxels, peak =  9), gca=8.7
gca peak = 0.15565 (16)
mri peak = 0.14901 ( 9)
Right_Lateral_Ventricle (43): linear fit = 0.37 x + 0.0 (353 voxels, overlap=0.148)
Right_Lateral_Ventricle (43): linear fit = 0.40 x + 0.0 (353 voxels, peak =  6), gca=6.4
gca peak = 0.26829 (96)
mri peak = 0.08407 (96)
Right_Pallidum (52): linear fit = 0.99 x + 0.0 (676 voxels, overlap=1.002)
Right_Pallidum (52): linear fit = 0.99 x + 0.0 (676 voxels, peak = 95), gca=94.6
gca peak = 0.20183 (93)
mri peak = 0.06866 (96)
Left_Pallidum (13): linear fit = 1.02 x + 0.0 (572 voxels, overlap=1.016)
Left_Pallidum (13): linear fit = 1.02 x + 0.0 (572 voxels, peak = 95), gca=95.3
gca peak = 0.21683 (55)
mri peak = 0.10316 (56)
Right_Hippocampus (53): linear fit = 0.92 x + 0.0 (563 voxels, overlap=0.996)
Right_Hippocampus (53): linear fit = 0.92 x + 0.0 (563 voxels, peak = 50), gca=50.3
gca peak = 0.30730 (58)
mri peak = 0.08012 (57)
Left_Hippocampus (17): linear fit = 0.96 x + 0.0 (369 voxels, overlap=0.996)
Left_Hippocampus (17): linear fit = 0.96 x + 0.0 (369 voxels, peak = 56), gca=56.0
gca peak = 0.11430 (101)
mri peak = 0.06072 (108)
Right_Cerebral_White_Matter (41): linear fit = 1.07 x + 0.0 (52545 voxels, overlap=0.748)
Right_Cerebral_White_Matter (41): linear fit = 1.07 x + 0.0 (52545 voxels, peak = 108), gca=107.6
gca peak = 0.12076 (102)
mri peak = 0.06441 (104)
Left_Cerebral_White_Matter (2): linear fit = 1.05 x + 0.0 (52090 voxels, overlap=0.719)
Left_Cerebral_White_Matter (2): linear fit = 1.05 x + 0.0 (52090 voxels, peak = 108), gca=107.6
gca peak = 0.14995 (59)
mri peak = 0.04173 (54)
Left_Cerebral_Cortex (3): linear fit = 0.94 x + 0.0 (13255 voxels, overlap=0.927)
Left_Cerebral_Cortex (3): linear fit = 0.94 x + 0.0 (13255 voxels, peak = 56), gca=55.8
gca peak = 0.15082 (58)
mri peak = 0.03621 (52)
Right_Cerebral_Cortex (42): linear fit = 0.94 x + 0.0 (14917 voxels, overlap=0.950)
Right_Cerebral_Cortex (42): linear fit = 0.94 x + 0.0 (14917 voxels, peak = 55), gca=54.8
gca peak = 0.14161 (67)
mri peak = 0.08610 (71)
Right_Caudate (50): linear fit = 1.04 x + 0.0 (804 voxels, overlap=0.898)
Right_Caudate (50): linear fit = 1.04 x + 0.0 (804 voxels, peak = 70), gca=70.0
gca peak = 0.15243 (71)
mri peak = 0.06931 (74)
Left_Caudate (11): linear fit = 0.99 x + 0.0 (807 voxels, overlap=0.995)
Left_Caudate (11): linear fit = 0.99 x + 0.0 (807 voxels, peak = 70), gca=69.9
gca peak = 0.13336 (57)
mri peak = 0.03749 (51)
Left_Cerebellum_Cortex (8): linear fit = 0.93 x + 0.0 (12124 voxels, overlap=0.678)
Left_Cerebellum_Cortex (8): linear fit = 0.93 x + 0.0 (12124 voxels, peak = 53), gca=52.7
gca peak = 0.13252 (56)
mri peak = 0.04045 (50)
Right_Cerebellum_Cortex (47): linear fit = 0.88 x + 0.0 (14675 voxels, overlap=0.557)
Right_Cerebellum_Cortex (47): linear fit = 0.88 x + 0.0 (14675 voxels, peak = 49), gca=49.0
gca peak = 0.18181 (84)
mri peak = 0.05786 (84)
Left_Cerebellum_White_Matter (7): linear fit = 1.03 x + 0.0 (4757 voxels, overlap=0.929)
Left_Cerebellum_White_Matter (7): linear fit = 1.03 x + 0.0 (4757 voxels, peak = 87), gca=86.9
gca peak = 0.20573 (83)
mri peak = 0.06841 (80)
Right_Cerebellum_White_Matter (46): linear fit = 0.99 x + 0.0 (4995 voxels, overlap=0.978)
Right_Cerebellum_White_Matter (46): linear fit = 0.99 x + 0.0 (4995 voxels, peak = 82), gca=81.8
gca peak = 0.21969 (57)
mri peak = 0.06333 (61)
Left_Amygdala (18): linear fit = 1.04 x + 0.0 (304 voxels, overlap=0.894)
Left_Amygdala (18): linear fit = 1.04 x + 0.0 (304 voxels, peak = 60), gca=59.6
gca peak = 0.39313 (56)
mri peak = 0.06053 (54)
Right_Amygdala (54): linear fit = 1.04 x + 0.0 (391 voxels, overlap=1.003)
Right_Amygdala (54): linear fit = 1.04 x + 0.0 (391 voxels, peak = 59), gca=58.5
gca peak = 0.14181 (85)
mri peak = 0.05212 (93)
Left_Thalamus_Proper (10): linear fit = 1.07 x + 0.0 (4614 voxels, overlap=0.735)
Left_Thalamus_Proper (10): linear fit = 1.07 x + 0.0 (4614 voxels, peak = 91), gca=90.5
gca peak = 0.11978 (83)
mri peak = 0.06172 (91)
Right_Thalamus_Proper (49): linear fit = 1.09 x + 0.0 (3709 voxels, overlap=0.776)
Right_Thalamus_Proper (49): linear fit = 1.09 x + 0.0 (3709 voxels, peak = 90), gca=90.1
gca peak = 0.13399 (79)
mri peak = 0.04288 (79)
Left_Putamen (12): linear fit = 1.04 x + 0.0 (1625 voxels, overlap=0.954)
Left_Putamen (12): linear fit = 1.04 x + 0.0 (1625 voxels, peak = 83), gca=82.6
gca peak = 0.14159 (79)
mri peak = 0.04488 (84)
Right_Putamen (51): linear fit = 1.10 x + 0.0 (1792 voxels, overlap=0.999)
Right_Putamen (51): linear fit = 1.10 x + 0.0 (1792 voxels, peak = 87), gca=86.5
gca peak = 0.10025 (80)
mri peak = 0.11001 (80)
Brain_Stem (16): linear fit = 1.07 x + 0.0 (10733 voxels, overlap=0.402)
Brain_Stem (16): linear fit = 1.07 x + 0.0 (10733 voxels, peak = 85), gca=85.2
gca peak = 0.13281 (86)
mri peak = 0.06624 (87)
Right_VentralDC (60): linear fit = 1.08 x + 0.0 (1247 voxels, overlap=0.711)
Right_VentralDC (60): linear fit = 1.08 x + 0.0 (1247 voxels, peak = 92), gca=92.5
gca peak = 0.12801 (89)
mri peak = 0.05919 (89)
Left_VentralDC (28): linear fit = 1.10 x + 0.0 (1293 voxels, overlap=0.799)
Left_VentralDC (28): linear fit = 1.10 x + 0.0 (1293 voxels, peak = 97), gca=97.5
gca peak = 0.20494 (23)
mri peak = 0.11129 (47)
gca peak = 0.15061 (21)
mri peak = 0.10765 ( 6)
Fourth_Ventricle (15): linear fit = 0.28 x + 0.0 (252 voxels, overlap=0.110)
Fourth_Ventricle (15): linear fit = 0.28 x + 0.0 (252 voxels, peak =  6), gca=6.0
gca peak Unknown = 0.94835 ( 0)
gca peak Left_Inf_Lat_Vent = 0.18056 (32)
gca peak Left_Thalamus = 0.64095 (94)
gca peak Third_Ventricle = 0.20494 (23)
gca peak Fourth_Ventricle = 0.15061 (21)
gca peak CSF = 0.20999 (34)
gca peak Left_Accumbens_area = 0.39030 (62)
gca peak Left_undetermined = 0.95280 (25)
gca peak Left_vessel = 0.67734 (53)
gca peak Left_choroid_plexus = 0.09433 (44)
gca peak Right_Inf_Lat_Vent = 0.23544 (26)
gca peak Right_Accumbens_area = 0.30312 (64)
gca peak Right_vessel = 0.46315 (51)
gca peak Right_choroid_plexus = 0.14086 (44)
gca peak Fifth_Ventricle = 0.51669 (36)
gca peak WM_hypointensities = 0.09722 (76)
gca peak non_WM_hypointensities = 0.11899 (47)
gca peak Optic_Chiasm = 0.39033 (72)
label assignment complete, 0 changed (0.00%)
not using caudate to estimate GM means
estimating mean gm scale to be 0.98 x + 0.0
estimating mean wm scale to be 1.06 x + 0.0
estimating mean csf scale to be 0.42 x + 0.0
saving intensity scales to talairach.label_intensities.txt
**************** pass 1 of 1 ************************
enabling zero nodes
setting smoothness coefficient to 0.008
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.675, neg=0, invalid=762
0094: dt=135.384615, rms=0.670 (0.711%), neg=0, invalid=762
0095: dt=295.936000, rms=0.667 (0.438%), neg=0, invalid=762
0096: dt=110.976000, rms=0.665 (0.257%), neg=0, invalid=762
0097: dt=129.472000, rms=0.664 (0.136%), neg=0, invalid=762
0098: dt=129.472000, rms=0.663 (0.148%), neg=0, invalid=762
0099: dt=129.472000, rms=0.663 (0.104%), neg=0, invalid=762
0100: dt=129.472000, rms=0.662 (0.113%), neg=0, invalid=762
0101: dt=129.472000, rms=0.661 (0.082%), neg=0, invalid=762
0102: dt=295.936000, rms=0.660 (0.125%), neg=0, invalid=762
0103: dt=73.984000, rms=0.660 (0.107%), neg=0, invalid=762
0104: dt=1775.616000, rms=0.657 (0.435%), neg=0, invalid=762
0105: dt=73.984000, rms=0.656 (0.156%), neg=0, invalid=762
0106: dt=1183.744000, rms=0.655 (0.172%), neg=0, invalid=762
0107: dt=73.984000, rms=0.654 (0.102%), neg=0, invalid=762
0108: dt=295.936000, rms=0.654 (0.044%), neg=0, invalid=762
0109: dt=295.936000, rms=0.654 (-0.030%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.654, neg=0, invalid=762
0110: dt=129.472000, rms=0.653 (0.256%), neg=0, invalid=762
0111: dt=517.888000, rms=0.652 (0.185%), neg=0, invalid=762
0112: dt=110.976000, rms=0.651 (0.056%), neg=0, invalid=762
0113: dt=129.472000, rms=0.651 (0.027%), neg=0, invalid=762
0114: dt=129.472000, rms=0.651 (0.022%), neg=0, invalid=762
0115: dt=129.472000, rms=0.651 (0.035%), neg=0, invalid=762
0116: dt=129.472000, rms=0.650 (0.048%), neg=0, invalid=762
0117: dt=129.472000, rms=0.650 (0.056%), neg=0, invalid=762
0118: dt=129.472000, rms=0.650 (0.067%), neg=0, invalid=762
0119: dt=129.472000, rms=0.649 (0.064%), neg=0, invalid=762
0120: dt=129.472000, rms=0.649 (0.065%), neg=0, invalid=762
0121: dt=129.472000, rms=0.648 (0.059%), neg=0, invalid=762
0122: dt=129.472000, rms=0.648 (0.062%), neg=0, invalid=762
0123: dt=129.472000, rms=0.648 (0.053%), neg=0, invalid=762
0124: dt=129.472000, rms=0.647 (0.050%), neg=0, invalid=762
0125: dt=129.472000, rms=0.647 (0.051%), neg=0, invalid=762
0126: dt=129.472000, rms=0.647 (0.049%), neg=0, invalid=762
0127: dt=129.472000, rms=0.646 (0.051%), neg=0, invalid=762
0128: dt=129.472000, rms=0.646 (0.042%), neg=0, invalid=762
0129: dt=129.472000, rms=0.646 (0.053%), neg=0, invalid=762
0130: dt=129.472000, rms=0.645 (0.041%), neg=0, invalid=762
0131: dt=129.472000, rms=0.645 (0.043%), neg=0, invalid=762
0132: dt=129.472000, rms=0.645 (0.044%), neg=0, invalid=762
0133: dt=129.472000, rms=0.645 (0.050%), neg=0, invalid=762
0134: dt=129.472000, rms=0.644 (0.040%), neg=0, invalid=762
0135: dt=129.472000, rms=0.644 (0.037%), neg=0, invalid=762
0136: dt=129.472000, rms=0.644 (0.038%), neg=0, invalid=762
0137: dt=129.472000, rms=0.644 (0.037%), neg=0, invalid=762
0138: dt=129.472000, rms=0.643 (0.040%), neg=0, invalid=762
0139: dt=129.472000, rms=0.643 (0.039%), neg=0, invalid=762
0140: dt=129.472000, rms=0.643 (0.034%), neg=0, invalid=762
0141: dt=129.472000, rms=0.643 (0.032%), neg=0, invalid=762
0142: dt=129.472000, rms=0.642 (0.029%), neg=0, invalid=762
0143: dt=129.472000, rms=0.642 (0.030%), neg=0, invalid=762
0144: dt=129.472000, rms=0.642 (0.028%), neg=0, invalid=762
0145: dt=129.472000, rms=0.642 (0.025%), neg=0, invalid=762
0146: dt=129.472000, rms=0.642 (0.023%), neg=0, invalid=762
0147: dt=517.888000, rms=0.642 (0.006%), neg=0, invalid=762
0148: dt=517.888000, rms=0.642 (-0.067%), neg=0, invalid=762
setting smoothness coefficient to 0.031
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.643, neg=0, invalid=762
0149: dt=84.853933, rms=0.639 (0.508%), neg=0, invalid=762
0150: dt=201.142857, rms=0.635 (0.761%), neg=0, invalid=762
0151: dt=55.172414, rms=0.632 (0.408%), neg=0, invalid=762
0152: dt=145.152000, rms=0.629 (0.417%), neg=0, invalid=762
0153: dt=36.288000, rms=0.628 (0.233%), neg=0, invalid=762
0154: dt=580.608000, rms=0.621 (1.097%), neg=0, invalid=762
0155: dt=72.585366, rms=0.618 (0.469%), neg=0, invalid=762
0156: dt=36.288000, rms=0.618 (0.098%), neg=0, invalid=762
0157: dt=414.720000, rms=0.616 (0.325%), neg=0, invalid=762
0158: dt=83.478261, rms=0.614 (0.292%), neg=0, invalid=762
0159: dt=36.288000, rms=0.613 (0.122%), neg=0, invalid=762
0160: dt=145.152000, rms=0.612 (0.121%), neg=0, invalid=762
0161: dt=103.680000, rms=0.611 (0.130%), neg=0, invalid=762
0162: dt=36.288000, rms=0.611 (0.053%), neg=0, invalid=762
0163: dt=497.664000, rms=0.610 (0.219%), neg=0, invalid=762
0164: dt=36.288000, rms=0.608 (0.243%), neg=0, invalid=762
0165: dt=145.152000, rms=0.607 (0.156%), neg=0, invalid=762
0166: dt=36.288000, rms=0.607 (0.028%), neg=0, invalid=762
0167: dt=36.288000, rms=0.607 (0.023%), neg=0, invalid=762
0168: dt=36.288000, rms=0.607 (0.045%), neg=0, invalid=762
0169: dt=36.288000, rms=0.606 (0.071%), neg=0, invalid=762
0170: dt=36.288000, rms=0.606 (0.098%), neg=0, invalid=762
0171: dt=36.288000, rms=0.605 (0.115%), neg=0, invalid=762
0172: dt=36.288000, rms=0.604 (0.122%), neg=0, invalid=762
0173: dt=36.288000, rms=0.604 (0.126%), neg=0, invalid=762
0174: dt=36.288000, rms=0.603 (0.128%), neg=0, invalid=762
0175: dt=36.288000, rms=0.602 (0.133%), neg=0, invalid=762
0176: dt=36.288000, rms=0.601 (0.135%), neg=0, invalid=762
0177: dt=36.288000, rms=0.600 (0.141%), neg=0, invalid=762
0178: dt=36.288000, rms=0.599 (0.140%), neg=0, invalid=762
0179: dt=36.288000, rms=0.599 (0.136%), neg=0, invalid=762
0180: dt=36.288000, rms=0.599 (0.012%), neg=0, invalid=762
0181: dt=36.288000, rms=0.598 (0.026%), neg=0, invalid=762
0182: dt=36.288000, rms=0.598 (0.038%), neg=0, invalid=762
0183: dt=36.288000, rms=0.598 (0.057%), neg=0, invalid=762
0184: dt=36.288000, rms=0.597 (0.063%), neg=0, invalid=762
0185: dt=36.288000, rms=0.597 (0.073%), neg=0, invalid=762
0186: dt=36.288000, rms=0.597 (0.073%), neg=0, invalid=762
0187: dt=36.288000, rms=0.596 (0.078%), neg=0, invalid=762
0188: dt=36.288000, rms=0.596 (0.081%), neg=0, invalid=762
0189: dt=36.288000, rms=0.595 (0.086%), neg=0, invalid=762
0190: dt=36.288000, rms=0.595 (0.095%), neg=0, invalid=762
0191: dt=36.288000, rms=0.594 (0.098%), neg=0, invalid=762
0192: dt=36.288000, rms=0.593 (0.095%), neg=0, invalid=762
0193: dt=4.536000, rms=0.593 (0.003%), neg=0, invalid=762
0194: dt=2.268000, rms=0.593 (-0.002%), neg=0, invalid=762
0195: dt=2.268000, rms=0.593 (0.001%), neg=0, invalid=762
0196: dt=0.141750, rms=0.593 (0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.594, neg=0, invalid=762
0197: dt=135.314286, rms=0.591 (0.547%), neg=0, invalid=762
0198: dt=76.467532, rms=0.590 (0.235%), neg=0, invalid=762
0199: dt=82.944000, rms=0.589 (0.086%), neg=0, invalid=762
0200: dt=103.680000, rms=0.588 (0.154%), neg=0, invalid=762
0201: dt=36.288000, rms=0.588 (0.050%), neg=0, invalid=762
0202: dt=414.720000, rms=0.587 (0.196%), neg=0, invalid=762
0203: dt=36.288000, rms=0.586 (0.176%), neg=0, invalid=762
0204: dt=145.152000, rms=0.585 (0.074%), neg=0, invalid=762
0205: dt=36.288000, rms=0.585 (0.027%), neg=0, invalid=762
0206: dt=36.288000, rms=0.585 (0.014%), neg=0, invalid=762
0207: dt=36.288000, rms=0.585 (0.032%), neg=0, invalid=762
0208: dt=36.288000, rms=0.585 (0.044%), neg=0, invalid=762
0209: dt=36.288000, rms=0.584 (0.055%), neg=0, invalid=762
0210: dt=36.288000, rms=0.584 (0.066%), neg=0, invalid=762
0211: dt=36.288000, rms=0.583 (0.069%), neg=0, invalid=762
0212: dt=36.288000, rms=0.583 (0.072%), neg=0, invalid=762
0213: dt=36.288000, rms=0.583 (0.072%), neg=0, invalid=762
0214: dt=36.288000, rms=0.582 (0.080%), neg=0, invalid=762
0215: dt=36.288000, rms=0.582 (0.082%), neg=0, invalid=762
0216: dt=36.288000, rms=0.581 (0.082%), neg=0, invalid=762
0217: dt=36.288000, rms=0.581 (0.078%), neg=0, invalid=762
0218: dt=36.288000, rms=0.580 (0.080%), neg=0, invalid=762
0219: dt=36.288000, rms=0.580 (0.081%), neg=0, invalid=762
0220: dt=36.288000, rms=0.579 (0.084%), neg=0, invalid=762
0221: dt=36.288000, rms=0.579 (0.082%), neg=0, invalid=762
0222: dt=36.288000, rms=0.578 (0.077%), neg=0, invalid=762
0223: dt=36.288000, rms=0.578 (0.076%), neg=0, invalid=762
0224: dt=36.288000, rms=0.578 (0.003%), neg=0, invalid=762
0225: dt=36.288000, rms=0.578 (0.017%), neg=0, invalid=762
0226: dt=36.288000, rms=0.578 (0.017%), neg=0, invalid=762
0227: dt=4.536000, rms=0.578 (-0.001%), neg=0, invalid=762
0228: dt=6.480000, rms=0.578 (0.001%), neg=0, invalid=762
0229: dt=0.035437, rms=0.578 (-0.001%), neg=0, invalid=762
setting smoothness coefficient to 0.118
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.584, neg=0, invalid=762
0230: dt=53.333333, rms=0.578 (0.909%), neg=0, invalid=762
0231: dt=11.200000, rms=0.576 (0.411%), neg=0, invalid=762
0232: dt=11.200000, rms=0.574 (0.297%), neg=0, invalid=762
0233: dt=2.800000, rms=0.574 (0.066%), neg=0, invalid=762
0234: dt=0.700000, rms=0.574 (0.014%), neg=0, invalid=762
0235: dt=0.350000, rms=0.574 (0.007%), neg=0, invalid=762
0236: dt=0.087500, rms=0.574 (0.001%), neg=0, invalid=762
0237: dt=0.043750, rms=0.574 (0.001%), neg=0, invalid=762
0238: dt=0.010937, rms=0.574 (0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.575, neg=0, invalid=762
0239: dt=0.002734, rms=0.574 (0.129%), neg=0, invalid=762
0240: dt=0.000488, rms=0.574 (0.000%), neg=0, invalid=762
0241: dt=0.000008, rms=0.574 (0.000%), neg=0, invalid=762
0242: dt=0.000002, rms=0.574 (0.000%), neg=0, invalid=762
0243: dt=0.000001, rms=0.574 (0.000%), neg=0, invalid=762
0244: dt=0.000000, rms=0.574 (0.000%), neg=0, invalid=762
setting smoothness coefficient to 0.400
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.590, neg=0, invalid=762
0245: dt=4.032000, rms=0.583 (1.260%), neg=0, invalid=762
0246: dt=4.032000, rms=0.578 (0.872%), neg=0, invalid=762
0247: dt=11.520000, rms=0.568 (1.732%), neg=0, invalid=762
0248: dt=16.128000, rms=0.561 (1.092%), neg=0, invalid=762
0249: dt=1.008000, rms=0.561 (0.030%), neg=0, invalid=762
0250: dt=0.126000, rms=0.561 (0.005%), neg=0, invalid=762
0251: dt=0.007875, rms=0.561 (-0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.562, neg=0, invalid=762
0252: dt=13.157025, rms=0.559 (0.531%), neg=0, invalid=762
0253: dt=20.756757, rms=0.557 (0.320%), neg=0, invalid=762
0254: dt=11.672956, rms=0.556 (0.231%), neg=0, invalid=762
0255: dt=14.465753, rms=0.555 (0.167%), neg=0, invalid=762
0256: dt=10.962963, rms=0.554 (0.143%), neg=0, invalid=762
0257: dt=13.824000, rms=0.554 (0.104%), neg=0, invalid=762
0258: dt=11.520000, rms=0.553 (0.114%), neg=0, invalid=762
0259: dt=11.471698, rms=0.553 (0.083%), neg=0, invalid=762
0260: dt=11.520000, rms=0.552 (0.080%), neg=0, invalid=762
0261: dt=11.520000, rms=0.552 (0.061%), neg=0, invalid=762
0262: dt=11.259259, rms=0.551 (0.071%), neg=0, invalid=762
0263: dt=10.400000, rms=0.551 (0.054%), neg=0, invalid=762
0264: dt=13.647059, rms=0.551 (0.070%), neg=0, invalid=762
0265: dt=9.056604, rms=0.550 (0.056%), neg=0, invalid=762
0266: dt=15.333333, rms=0.550 (0.057%), neg=0, invalid=762
0267: dt=7.836735, rms=0.550 (0.040%), neg=0, invalid=762
0268: dt=7.836735, rms=0.550 (0.039%), neg=0, invalid=762
0269: dt=7.836735, rms=0.549 (0.057%), neg=0, invalid=762
0270: dt=7.836735, rms=0.549 (0.082%), neg=0, invalid=762
0271: dt=7.836735, rms=0.548 (0.090%), neg=0, invalid=762
0272: dt=7.836735, rms=0.548 (0.112%), neg=0, invalid=762
0273: dt=7.836735, rms=0.547 (0.132%), neg=0, invalid=762
0274: dt=7.836735, rms=0.546 (0.128%), neg=0, invalid=762
0275: dt=7.836735, rms=0.546 (0.119%), neg=0, invalid=762
0276: dt=7.836735, rms=0.545 (0.106%), neg=0, invalid=762
0277: dt=7.836735, rms=0.545 (0.097%), neg=0, invalid=762
0278: dt=7.836735, rms=0.544 (0.103%), neg=0, invalid=762
0279: dt=7.836735, rms=0.543 (0.105%), neg=0, invalid=762
0280: dt=7.836735, rms=0.543 (0.096%), neg=0, invalid=762
0281: dt=7.836735, rms=0.542 (0.088%), neg=0, invalid=762
0282: dt=7.836735, rms=0.542 (0.085%), neg=0, invalid=762
0283: dt=7.836735, rms=0.542 (0.078%), neg=0, invalid=762
0284: dt=7.836735, rms=0.541 (0.080%), neg=0, invalid=762
0285: dt=7.836735, rms=0.541 (0.055%), neg=0, invalid=762
0286: dt=7.836735, rms=0.541 (0.051%), neg=0, invalid=762
0287: dt=7.836735, rms=0.540 (0.033%), neg=0, invalid=762
0288: dt=7.836735, rms=0.540 (0.056%), neg=0, invalid=762
0289: dt=7.836735, rms=0.540 (0.043%), neg=0, invalid=762
0290: dt=7.836735, rms=0.540 (0.031%), neg=0, invalid=762
0291: dt=7.836735, rms=0.539 (0.030%), neg=0, invalid=762
0292: dt=7.836735, rms=0.539 (0.036%), neg=0, invalid=762
0293: dt=7.836735, rms=0.539 (0.032%), neg=0, invalid=762
0294: dt=7.836735, rms=0.539 (0.025%), neg=0, invalid=762
0295: dt=7.836735, rms=0.539 (0.022%), neg=0, invalid=762
0296: dt=7.836735, rms=0.539 (0.029%), neg=0, invalid=762
0297: dt=7.836735, rms=0.539 (0.011%), neg=0, invalid=762
0298: dt=7.836735, rms=0.539 (0.017%), neg=0, invalid=762
0299: dt=7.836735, rms=0.538 (0.024%), neg=0, invalid=762
0300: dt=7.836735, rms=0.538 (0.032%), neg=0, invalid=762
0301: dt=7.836735, rms=0.538 (0.026%), neg=0, invalid=762
0302: dt=7.836735, rms=0.538 (0.020%), neg=0, invalid=762
0303: dt=7.836735, rms=0.538 (0.014%), neg=0, invalid=762
0304: dt=4.032000, rms=0.538 (0.002%), neg=0, invalid=762
0305: dt=4.032000, rms=0.538 (-0.001%), neg=0, invalid=762
setting smoothness coefficient to 1.000
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.552, neg=0, invalid=762
0306: dt=0.000000, rms=0.551 (0.129%), neg=0, invalid=762
0307: dt=0.000000, rms=0.551 (0.000%), neg=0, invalid=762
0308: dt=0.100000, rms=0.551 (-0.181%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.552, neg=0, invalid=762
0309: dt=0.000000, rms=0.551 (0.129%), neg=0, invalid=762
0310: dt=0.000000, rms=0.551 (0.000%), neg=0, invalid=762
0311: dt=0.100000, rms=0.551 (-0.165%), neg=0, invalid=762
resetting metric properties...
setting smoothness coefficient to 2.000
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.530, neg=0, invalid=762
0312: dt=0.448000, rms=0.513 (3.191%), neg=0, invalid=762
0313: dt=0.448000, rms=0.509 (0.683%), neg=0, invalid=762
0314: dt=0.448000, rms=0.507 (0.380%), neg=0, invalid=762
0315: dt=0.448000, rms=0.506 (0.224%), neg=0, invalid=762
0316: dt=0.500000, rms=0.505 (0.185%), neg=0, invalid=762
0317: dt=0.448000, rms=0.505 (0.111%), neg=0, invalid=762
0318: dt=0.448000, rms=0.504 (0.105%), neg=0, invalid=762
0319: dt=0.448000, rms=0.504 (0.065%), neg=0, invalid=762
0320: dt=0.448000, rms=0.504 (0.069%), neg=0, invalid=762
0321: dt=0.448000, rms=0.503 (0.043%), neg=0, invalid=762
0322: dt=0.448000, rms=0.503 (0.051%), neg=0, invalid=762
0323: dt=0.448000, rms=0.503 (0.072%), neg=0, invalid=762
0324: dt=0.448000, rms=0.502 (0.093%), neg=0, invalid=762
0325: dt=0.448000, rms=0.502 (0.087%), neg=0, invalid=762
0326: dt=0.448000, rms=0.501 (0.086%), neg=0, invalid=762
0327: dt=0.448000, rms=0.501 (0.055%), neg=0, invalid=762
0328: dt=0.448000, rms=0.501 (0.025%), neg=0, invalid=762
0329: dt=0.448000, rms=0.501 (0.017%), neg=0, invalid=762
0330: dt=0.080000, rms=0.501 (0.001%), neg=0, invalid=762
0331: dt=0.080000, rms=0.501 (-0.005%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.502, neg=0, invalid=762
0332: dt=0.448000, rms=0.495 (1.416%), neg=0, invalid=762
0333: dt=0.448000, rms=0.494 (0.120%), neg=0, invalid=762
0334: dt=0.448000, rms=0.494 (0.037%), neg=0, invalid=762
0335: dt=0.448000, rms=0.494 (-0.005%), neg=0, invalid=762
label assignment complete, 0 changed (0.00%)
********************* ALLOWING NEGATIVE NODES IN DEFORMATION********************************
**************** pass 1 of 1 ************************
enabling zero nodes
setting smoothness coefficient to 0.008
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.492, neg=0, invalid=762
0336: dt=0.000000, rms=0.491 (0.160%), neg=0, invalid=762
0337: dt=0.000000, rms=0.491 (0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.492, neg=0, invalid=762
0338: dt=129.472000, rms=0.491 (0.219%), neg=0, invalid=762
0339: dt=32.368000, rms=0.491 (0.004%), neg=0, invalid=762
0340: dt=32.368000, rms=0.491 (0.003%), neg=0, invalid=762
0341: dt=32.368000, rms=0.491 (0.002%), neg=0, invalid=762
0342: dt=32.368000, rms=0.491 (0.004%), neg=0, invalid=762
0343: dt=32.368000, rms=0.491 (0.011%), neg=0, invalid=762
0344: dt=32.368000, rms=0.491 (0.010%), neg=0, invalid=762
setting smoothness coefficient to 0.031
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.492, neg=0, invalid=762
0345: dt=5.333333, rms=0.491 (0.167%), neg=0, invalid=762
0346: dt=1.296000, rms=0.491 (-0.001%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.492, neg=0, invalid=762
0347: dt=145.152000, rms=0.489 (0.419%), neg=0, invalid=762
0348: dt=31.104000, rms=0.489 (0.080%), neg=0, invalid=762
0349: dt=31.104000, rms=0.489 (0.037%), neg=0, invalid=762
0350: dt=31.104000, rms=0.489 (0.044%), neg=0, invalid=762
0351: dt=31.104000, rms=0.488 (0.075%), neg=0, invalid=762
0352: dt=31.104000, rms=0.488 (0.072%), neg=0, invalid=762
0353: dt=31.104000, rms=0.488 (0.070%), neg=0, invalid=762
0354: dt=145.152000, rms=0.487 (0.052%), neg=0, invalid=762
setting smoothness coefficient to 0.118
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.488, neg=0, invalid=762
iter 0, gcam->neg = 4
after 0 iterations, nbhd size=0, neg = 0
0355: dt=24.328767, rms=0.486 (0.439%), neg=0, invalid=762
iter 0, gcam->neg = 2
after 0 iterations, nbhd size=0, neg = 0
0356: dt=25.600000, rms=0.486 (0.128%), neg=0, invalid=762
iter 0, gcam->neg = 8
after 10 iterations, nbhd size=1, neg = 0
0357: dt=25.600000, rms=0.485 (0.085%), neg=0, invalid=762
iter 0, gcam->neg = 13
after 8 iterations, nbhd size=1, neg = 0
0358: dt=25.600000, rms=0.485 (0.078%), neg=0, invalid=762
iter 0, gcam->neg = 25
after 10 iterations, nbhd size=1, neg = 0
0359: dt=25.600000, rms=0.485 (-0.157%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.486, neg=0, invalid=762
iter 0, gcam->neg = 1
after 0 iterations, nbhd size=0, neg = 0
0360: dt=43.789474, rms=0.479 (1.423%), neg=0, invalid=762
0361: dt=20.466431, rms=0.477 (0.445%), neg=0, invalid=762
0362: dt=38.400000, rms=0.475 (0.240%), neg=0, invalid=762
0363: dt=38.400000, rms=0.475 (0.022%), neg=0, invalid=762
iter 0, gcam->neg = 2
after 0 iterations, nbhd size=0, neg = 0
0364: dt=38.400000, rms=0.473 (0.568%), neg=0, invalid=762
0365: dt=38.400000, rms=0.472 (0.081%), neg=0, invalid=762
iter 0, gcam->neg = 1
after 1 iterations, nbhd size=0, neg = 0
0366: dt=38.400000, rms=0.469 (0.587%), neg=0, invalid=762
iter 0, gcam->neg = 4
after 7 iterations, nbhd size=1, neg = 0
0367: dt=38.400000, rms=0.469 (0.148%), neg=0, invalid=762
iter 0, gcam->neg = 5
after 0 iterations, nbhd size=0, neg = 0
0368: dt=38.400000, rms=0.467 (0.430%), neg=0, invalid=762
iter 0, gcam->neg = 3
after 1 iterations, nbhd size=0, neg = 0
0369: dt=38.400000, rms=0.466 (0.234%), neg=0, invalid=762
iter 0, gcam->neg = 3
after 7 iterations, nbhd size=1, neg = 0
0370: dt=38.400000, rms=0.465 (0.229%), neg=0, invalid=762
iter 0, gcam->neg = 1
after 0 iterations, nbhd size=0, neg = 0
0371: dt=38.400000, rms=0.464 (0.131%), neg=0, invalid=762
iter 0, gcam->neg = 4
after 0 iterations, nbhd size=0, neg = 0
0372: dt=38.400000, rms=0.463 (0.321%), neg=0, invalid=762
0373: dt=38.400000, rms=0.462 (-0.085%), neg=0, invalid=762
0374: dt=11.200000, rms=0.462 (0.143%), neg=0, invalid=762
0375: dt=11.200000, rms=0.462 (0.042%), neg=0, invalid=762
setting smoothness coefficient to 0.400
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.467, neg=0, invalid=762
0376: dt=2.304000, rms=0.466 (0.201%), neg=0, invalid=762
0377: dt=0.252000, rms=0.466 (-0.001%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.467, neg=0, invalid=762
0378: dt=2.880000, rms=0.466 (0.195%), neg=0, invalid=762
0379: dt=1.008000, rms=0.466 (0.003%), neg=0, invalid=762
0380: dt=1.008000, rms=0.466 (-0.002%), neg=0, invalid=762
setting smoothness coefficient to 1.000
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.475, neg=0, invalid=762
0381: dt=0.448000, rms=0.474 (0.193%), neg=0, invalid=762
0382: dt=0.192000, rms=0.474 (0.003%), neg=0, invalid=762
0383: dt=0.192000, rms=0.474 (-0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.475, neg=0, invalid=762
0384: dt=1.536000, rms=0.473 (0.348%), neg=0, invalid=762
0385: dt=0.448000, rms=0.473 (0.020%), neg=0, invalid=762
0386: dt=0.448000, rms=0.473 (0.008%), neg=0, invalid=762
0387: dt=0.448000, rms=0.473 (-0.011%), neg=0, invalid=762
resetting metric properties...
setting smoothness coefficient to 2.000
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.466, neg=0, invalid=762
iter 0, gcam->neg = 765
after 12 iterations, nbhd size=1, neg = 0
0388: dt=2.257552, rms=0.434 (6.879%), neg=0, invalid=762
0389: dt=0.096000, rms=0.434 (0.082%), neg=0, invalid=762
0390: dt=0.096000, rms=0.434 (-0.082%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.435, neg=0, invalid=762
0391: dt=0.096000, rms=0.433 (0.314%), neg=0, invalid=762
0392: dt=0.006000, rms=0.433 (-0.001%), neg=0, invalid=762
0393: dt=0.006000, rms=0.433 (0.000%), neg=0, invalid=762
0394: dt=0.006000, rms=0.433 (-0.001%), neg=0, invalid=762
label assignment complete, 0 changed (0.00%)
label assignment complete, 0 changed (0.00%)
***************** morphing with label term set to 0 *******************************
**************** pass 1 of 1 ************************
enabling zero nodes
setting smoothness coefficient to 0.008
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.419, neg=0, invalid=762
0395: dt=0.000000, rms=0.419 (0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.419, neg=0, invalid=762
0396: dt=32.368000, rms=0.419 (0.004%), neg=0, invalid=762
0397: dt=32.368000, rms=0.419 (0.001%), neg=0, invalid=762
0398: dt=32.368000, rms=0.419 (0.000%), neg=0, invalid=762
0399: dt=32.368000, rms=0.419 (-0.000%), neg=0, invalid=762
setting smoothness coefficient to 0.031
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.419, neg=0, invalid=762
0400: dt=0.000000, rms=0.419 (0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.419, neg=0, invalid=762
0401: dt=36.288000, rms=0.419 (0.025%), neg=0, invalid=762
0402: dt=103.680000, rms=0.419 (0.025%), neg=0, invalid=762
0403: dt=103.680000, rms=0.419 (0.025%), neg=0, invalid=762
0404: dt=103.680000, rms=0.419 (0.019%), neg=0, invalid=762
0405: dt=103.680000, rms=0.419 (-0.007%), neg=0, invalid=762
setting smoothness coefficient to 0.118
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.420, neg=0, invalid=762
0406: dt=2.400000, rms=0.420 (0.004%), neg=0, invalid=762
0407: dt=0.400000, rms=0.420 (0.000%), neg=0, invalid=762
0408: dt=0.400000, rms=0.420 (-0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.420, neg=0, invalid=762
0409: dt=102.400000, rms=0.417 (0.616%), neg=0, invalid=762
0410: dt=25.600000, rms=0.416 (0.169%), neg=0, invalid=762
0411: dt=25.600000, rms=0.416 (0.088%), neg=0, invalid=762
iter 0, gcam->neg = 1
after 6 iterations, nbhd size=1, neg = 0
0412: dt=25.600000, rms=0.415 (0.099%), neg=0, invalid=762
iter 0, gcam->neg = 1
after 6 iterations, nbhd size=1, neg = 0
0413: dt=25.600000, rms=0.415 (0.141%), neg=0, invalid=762
0414: dt=25.600000, rms=0.414 (0.127%), neg=0, invalid=762
0415: dt=25.600000, rms=0.414 (0.153%), neg=0, invalid=762
0416: dt=25.600000, rms=0.413 (0.137%), neg=0, invalid=762
iter 0, gcam->neg = 1
after 6 iterations, nbhd size=1, neg = 0
0417: dt=25.600000, rms=0.413 (0.127%), neg=0, invalid=762
iter 0, gcam->neg = 1
after 0 iterations, nbhd size=0, neg = 0
0418: dt=25.600000, rms=0.412 (0.104%), neg=0, invalid=762
0419: dt=25.600000, rms=0.412 (0.092%), neg=0, invalid=762
0420: dt=44.800000, rms=0.412 (0.037%), neg=0, invalid=762
0421: dt=44.800000, rms=0.412 (-0.020%), neg=0, invalid=762
setting smoothness coefficient to 0.400
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.415, neg=0, invalid=762
0422: dt=1.008000, rms=0.415 (0.005%), neg=0, invalid=762
0423: dt=0.252000, rms=0.415 (0.000%), neg=0, invalid=762
0424: dt=0.252000, rms=0.415 (-0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.415, neg=0, invalid=762
0425: dt=8.396694, rms=0.415 (0.114%), neg=0, invalid=762
0426: dt=11.151515, rms=0.415 (0.060%), neg=0, invalid=762
0427: dt=11.151515, rms=0.414 (0.071%), neg=0, invalid=762
iter 0, gcam->neg = 1
after 0 iterations, nbhd size=0, neg = 0
0428: dt=11.151515, rms=0.414 (0.095%), neg=0, invalid=762
iter 0, gcam->neg = 3
after 1 iterations, nbhd size=0, neg = 0
0429: dt=11.151515, rms=0.413 (0.125%), neg=0, invalid=762
iter 0, gcam->neg = 4
after 7 iterations, nbhd size=1, neg = 0
0430: dt=11.151515, rms=0.413 (0.154%), neg=0, invalid=762
iter 0, gcam->neg = 1
after 0 iterations, nbhd size=0, neg = 0
0431: dt=11.151515, rms=0.412 (0.258%), neg=0, invalid=762
iter 0, gcam->neg = 1
after 0 iterations, nbhd size=0, neg = 0
0432: dt=11.151515, rms=0.411 (0.226%), neg=0, invalid=762
iter 0, gcam->neg = 2
after 1 iterations, nbhd size=0, neg = 0
0433: dt=11.151515, rms=0.410 (0.132%), neg=0, invalid=762
iter 0, gcam->neg = 3
after 0 iterations, nbhd size=0, neg = 0
0434: dt=11.151515, rms=0.410 (0.030%), neg=0, invalid=762
0435: dt=11.151515, rms=0.410 (-0.033%), neg=0, invalid=762
0436: dt=0.000984, rms=0.410 (0.000%), neg=0, invalid=762
0437: dt=0.000703, rms=0.410 (0.000%), neg=0, invalid=762
setting smoothness coefficient to 1.000
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.416, neg=0, invalid=762
0438: dt=0.000000, rms=0.416 (0.000%), neg=0, invalid=762
0439: dt=0.100000, rms=0.416 (-0.070%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.416, neg=0, invalid=762
0440: dt=0.000000, rms=0.416 (0.000%), neg=0, invalid=762
resetting metric properties...
setting smoothness coefficient to 2.000
blurring input image with Gaussian with sigma=2.000...
0000: dt=0.000, rms=0.406, neg=0, invalid=762
iter 0, gcam->neg = 545
after 11 iterations, nbhd size=1, neg = 0
0441: dt=1.669677, rms=0.395 (2.811%), neg=0, invalid=762
0442: dt=0.000013, rms=0.395 (0.000%), neg=0, invalid=762
0443: dt=0.000013, rms=0.395 (-0.000%), neg=0, invalid=762
blurring input image with Gaussian with sigma=0.500...
0000: dt=0.000, rms=0.395, neg=0, invalid=762
0444: dt=0.112000, rms=0.394 (0.088%), neg=0, invalid=762
0445: dt=0.028000, rms=0.394 (0.004%), neg=0, invalid=762
0446: dt=0.028000, rms=0.394 (-0.001%), neg=0, invalid=762
writing output transformation to transforms/talairach.m3z...
GCAMwrite
mri_ca_register took 139 hours, 14 minutes and 31 seconds.
mri_ca_register utimesec    7539.967485
mri_ca_register stimesec    40.971915
mri_ca_register ru_maxrss   1276346368
mri_ca_register ru_ixrss    0
mri_ca_register ru_idrss    0
mri_ca_register ru_isrss    0
mri_ca_register ru_minflt   1459232
mri_ca_register ru_majflt   413
mri_ca_register ru_nswap    0
mri_ca_register ru_inblock  0
mri_ca_register ru_oublock  0
mri_ca_register ru_msgsnd   0
mri_ca_register ru_msgrcv   0
mri_ca_register ru_nsignals 0
mri_ca_register ru_nvcsw    4635
mri_ca_register ru_nivcsw   6387677
FSRUNTIME@ mri_ca_register 139.2419 hours 1 threads
#--------------------------------------
#@# SubCort Seg Wed Mar 27 11:42:05 CET 2019
\n mri_ca_label -relabel_unlikely 9 .3 -prior 0.5 -align norm.mgz transforms/talairach.m3z /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca aseg.auto_noCCseg.mgz \n
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64

setenv SUBJECTS_DIR /Users/elizavetalavrova
cd /Users/elizavetalavrova/bert/mri
mri_ca_label -relabel_unlikely 9 .3 -prior 0.5 -align norm.mgz transforms/talairach.m3z /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca aseg.auto_noCCseg.mgz 


== Number of threads available to mri_ca_label for OpenMP = 1 == 
relabeling unlikely voxels with window_size = 9 and prior threshold 0.30
using Gibbs prior factor = 0.500
renormalizing sequences with structure alignment, equivalent to:
	-renormalize
	-renormalize_mean 0.500
	-regularize 0.500
reading 1 input volumes
reading classifier array from /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca
reading input volume from norm.mgz
average std[0] = 7.3
reading transform from transforms/talairach.m3z
setting orig areas to linear transform determinant scaled 6.59
Atlas used for the 3D morph was /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca
average std = 7.3   using min determinant for regularization = 5.3
0 singular and 0 ill-conditioned covariance matrices regularized
labeling volume...
renormalizing by structure alignment....
renormalizing input #0
gca peak = 0.16259 (20)
mri peak = 0.11563 ( 5)
Left_Lateral_Ventricle (4): linear fit = 0.20 x + 0.0 (564 voxels, overlap=0.109)
Left_Lateral_Ventricle (4): linear fit = 0.40 x + 0.0 (564 voxels, peak =  4), gca=8.0
gca peak = 0.17677 (13)
mri peak = 0.11315 ( 3)
Right_Lateral_Ventricle (43): linear fit = 0.16 x + 0.0 (562 voxels, overlap=0.185)
Right_Lateral_Ventricle (43): linear fit = 0.40 x + 0.0 (562 voxels, peak =  2), gca=5.2
gca peak = 0.28129 (95)
mri peak = 0.08718 (95)
Right_Pallidum (52): linear fit = 1.00 x + 0.0 (577 voxels, overlap=1.017)
Right_Pallidum (52): linear fit = 1.00 x + 0.0 (577 voxels, peak = 95), gca=94.5
gca peak = 0.16930 (96)
mri peak = 0.07987 (96)
Left_Pallidum (13): linear fit = 1.03 x + 0.0 (626 voxels, overlap=1.014)
Left_Pallidum (13): linear fit = 1.03 x + 0.0 (626 voxels, peak = 99), gca=99.4
gca peak = 0.24553 (55)
mri peak = 0.11003 (56)
Right_Hippocampus (53): linear fit = 0.92 x + 0.0 (544 voxels, overlap=1.008)
Right_Hippocampus (53): linear fit = 0.92 x + 0.0 (544 voxels, peak = 50), gca=50.3
gca peak = 0.30264 (59)
mri peak = 0.09600 (57)
Left_Hippocampus (17): linear fit = 0.94 x + 0.0 (413 voxels, overlap=1.012)
Left_Hippocampus (17): linear fit = 0.94 x + 0.0 (413 voxels, peak = 56), gca=55.8
gca peak = 0.07580 (103)
mri peak = 0.06545 (108)
Right_Cerebral_White_Matter (41): linear fit = 1.04 x + 0.0 (43083 voxels, overlap=0.693)
Right_Cerebral_White_Matter (41): linear fit = 1.04 x + 0.0 (43083 voxels, peak = 108), gca=107.6
gca peak = 0.07714 (104)
mri peak = 0.06468 (107)
Left_Cerebral_White_Matter (2): linear fit = 1.04 x + 0.0 (44917 voxels, overlap=0.659)
Left_Cerebral_White_Matter (2): linear fit = 1.04 x + 0.0 (44917 voxels, peak = 109), gca=108.7
gca peak = 0.09712 (58)
mri peak = 0.04285 (58)
Left_Cerebral_Cortex (3): linear fit = 0.96 x + 0.0 (16165 voxels, overlap=0.947)
Left_Cerebral_Cortex (3): linear fit = 0.96 x + 0.0 (16165 voxels, peak = 56), gca=56.0
gca peak = 0.11620 (58)
mri peak = 0.03923 (55)
Right_Cerebral_Cortex (42): linear fit = 0.96 x + 0.0 (17327 voxels, overlap=0.967)
Right_Cerebral_Cortex (42): linear fit = 0.96 x + 0.0 (17327 voxels, peak = 56), gca=56.0
gca peak = 0.30970 (66)
mri peak = 0.08617 (71)
Right_Caudate (50): linear fit = 1.07 x + 0.0 (822 voxels, overlap=1.011)
Right_Caudate (50): linear fit = 1.07 x + 0.0 (822 voxels, peak = 70), gca=70.3
gca peak = 0.15280 (69)
mri peak = 0.07356 (69)
Left_Caudate (11): linear fit = 0.95 x + 0.0 (934 voxels, overlap=1.005)
Left_Caudate (11): linear fit = 0.95 x + 0.0 (934 voxels, peak = 66), gca=65.9
gca peak = 0.13902 (56)
mri peak = 0.04977 (51)
Left_Cerebellum_Cortex (8): linear fit = 0.93 x + 0.0 (11277 voxels, overlap=0.870)
Left_Cerebellum_Cortex (8): linear fit = 0.93 x + 0.0 (11277 voxels, peak = 52), gca=51.8
gca peak = 0.14777 (55)
mri peak = 0.05234 (50)
Right_Cerebellum_Cortex (47): linear fit = 0.89 x + 0.0 (11535 voxels, overlap=0.853)
Right_Cerebellum_Cortex (47): linear fit = 0.89 x + 0.0 (11535 voxels, peak = 49), gca=49.2
gca peak = 0.16765 (84)
mri peak = 0.07669 (84)
Left_Cerebellum_White_Matter (7): linear fit = 1.02 x + 0.0 (3599 voxels, overlap=0.960)
Left_Cerebellum_White_Matter (7): linear fit = 1.02 x + 0.0 (3599 voxels, peak = 86), gca=86.1
gca peak = 0.18739 (84)
mri peak = 0.08053 (79)
Right_Cerebellum_White_Matter (46): linear fit = 0.98 x + 0.0 (4178 voxels, overlap=0.989)
Right_Cerebellum_White_Matter (46): linear fit = 0.98 x + 0.0 (4178 voxels, peak = 82), gca=81.9
gca peak = 0.29869 (57)
mri peak = 0.07046 (53)
Left_Amygdala (18): linear fit = 1.01 x + 0.0 (385 voxels, overlap=1.032)
Left_Amygdala (18): linear fit = 1.01 x + 0.0 (385 voxels, peak = 58), gca=57.9
gca peak = 0.33601 (57)
mri peak = 0.06651 (54)
Right_Amygdala (54): linear fit = 1.04 x + 0.0 (438 voxels, overlap=1.032)
Right_Amygdala (54): linear fit = 1.04 x + 0.0 (438 voxels, peak = 60), gca=59.6
gca peak = 0.11131 (90)
mri peak = 0.05839 (91)
Left_Thalamus_Proper (10): linear fit = 1.03 x + 0.0 (3857 voxels, overlap=0.974)
Left_Thalamus_Proper (10): linear fit = 1.03 x + 0.0 (3857 voxels, peak = 93), gca=93.1
gca peak = 0.11793 (83)
mri peak = 0.06185 (91)
Right_Thalamus_Proper (49): linear fit = 1.09 x + 0.0 (3654 voxels, overlap=0.855)
Right_Thalamus_Proper (49): linear fit = 1.09 x + 0.0 (3654 voxels, peak = 90), gca=90.1
gca peak = 0.08324 (81)
mri peak = 0.05070 (81)
Left_Putamen (12): linear fit = 1.04 x + 0.0 (2026 voxels, overlap=0.915)
Left_Putamen (12): linear fit = 1.04 x + 0.0 (2026 voxels, peak = 85), gca=84.6
gca peak = 0.10360 (77)
mri peak = 0.04323 (81)
Right_Putamen (51): linear fit = 1.03 x + 0.0 (2109 voxels, overlap=0.942)
Right_Putamen (51): linear fit = 1.03 x + 0.0 (2109 voxels, peak = 80), gca=79.7
gca peak = 0.08424 (78)
mri peak = 0.11016 (80)
Brain_Stem (16): linear fit = 1.05 x + 0.0 (9595 voxels, overlap=0.476)
Brain_Stem (16): linear fit = 1.05 x + 0.0 (9595 voxels, peak = 82), gca=82.3
gca peak = 0.12631 (89)
mri peak = 0.06559 (87)
Right_VentralDC (60): linear fit = 1.00 x + 0.0 (1171 voxels, overlap=0.808)
Right_VentralDC (60): linear fit = 1.00 x + 0.0 (1171 voxels, peak = 89), gca=88.6
gca peak = 0.14500 (87)
mri peak = 0.06342 (90)
Left_VentralDC (28): linear fit = 1.02 x + 0.0 (1083 voxels, overlap=0.879)
Left_VentralDC (28): linear fit = 1.02 x + 0.0 (1083 voxels, peak = 89), gca=89.2
gca peak = 0.14975 (24)
mri peak = 1.00000 (39)
gca peak = 0.19357 (14)
mri peak = 0.14194 ( 3)
Fourth_Ventricle (15): linear fit = 0.12 x + 0.0 (146 voxels, overlap=0.235)
Fourth_Ventricle (15): linear fit = 0.12 x + 0.0 (146 voxels, peak =  2), gca=1.8
gca peak Unknown = 0.94835 ( 0)
gca peak Left_Inf_Lat_Vent = 0.16825 (27)
gca peak Left_Thalamus = 1.00000 (94)
gca peak Third_Ventricle = 0.14975 (24)
gca peak Fourth_Ventricle = 0.19357 (14)
gca peak CSF = 0.23379 (36)
gca peak Left_Accumbens_area = 0.70037 (62)
gca peak Left_undetermined = 1.00000 (26)
gca peak Left_vessel = 0.75997 (52)
gca peak Left_choroid_plexus = 0.12089 (35)
gca peak Right_Inf_Lat_Vent = 0.24655 (23)
gca peak Right_Accumbens_area = 0.45042 (65)
gca peak Right_vessel = 0.82168 (52)
gca peak Right_choroid_plexus = 0.14516 (37)
gca peak Fifth_Ventricle = 0.65475 (32)
gca peak WM_hypointensities = 0.07854 (76)
gca peak non_WM_hypointensities = 0.08491 (43)
gca peak Optic_Chiasm = 0.71127 (75)
not using caudate to estimate GM means
estimating mean gm scale to be 0.98 x + 0.0
estimating mean wm scale to be 1.04 x + 0.0
estimating mean csf scale to be 0.40 x + 0.0
saving intensity scales to aseg.auto_noCCseg.label_intensities.txt
renormalizing by structure alignment....
renormalizing input #0
gca peak = 0.30837 ( 7)
mri peak = 0.11563 ( 5)
Left_Lateral_Ventricle (4): linear fit = 0.54 x + 0.0 (564 voxels, overlap=0.862)
Left_Lateral_Ventricle (4): linear fit = 0.54 x + 0.0 (564 voxels, peak =  4), gca=3.7
gca peak = 0.30173 ( 5)
mri peak = 0.11315 ( 3)
Right_Lateral_Ventricle (43): linear fit = 0.63 x + 0.0 (562 voxels, overlap=0.893)
Right_Lateral_Ventricle (43): linear fit = 0.63 x + 0.0 (562 voxels, peak =  3), gca=3.2
gca peak = 0.28673 (93)
mri peak = 0.08718 (95)
Right_Pallidum (52): linear fit = 1.00 x + 0.0 (577 voxels, overlap=1.015)
Right_Pallidum (52): linear fit = 1.00 x + 0.0 (577 voxels, peak = 93), gca=92.5
gca peak = 0.17346 (100)
mri peak = 0.07987 (96)
Left_Pallidum (13): linear fit = 1.00 x + 0.0 (626 voxels, overlap=1.011)
Left_Pallidum (13): linear fit = 1.00 x + 0.0 (626 voxels, peak = 100), gca=100.5
gca peak = 0.31375 (51)
mri peak = 0.11003 (56)
Right_Hippocampus (53): linear fit = 1.00 x + 0.0 (544 voxels, overlap=1.005)
Right_Hippocampus (53): linear fit = 1.00 x + 0.0 (544 voxels, peak = 51), gca=51.0
gca peak = 0.30420 (53)
mri peak = 0.09600 (57)
Left_Hippocampus (17): linear fit = 1.00 x + 0.0 (413 voxels, overlap=1.012)
Left_Hippocampus (17): linear fit = 1.00 x + 0.0 (413 voxels, peak = 53), gca=53.0
gca peak = 0.07601 (108)
mri peak = 0.06545 (108)
Right_Cerebral_White_Matter (41): linear fit = 1.00 x + 0.0 (43083 voxels, overlap=0.861)
Right_Cerebral_White_Matter (41): linear fit = 1.00 x + 0.0 (43083 voxels, peak = 108), gca=108.0
gca peak = 0.07787 (109)
mri peak = 0.06468 (107)
Left_Cerebral_White_Matter (2): linear fit = 1.00 x + 0.0 (44917 voxels, overlap=0.827)
Left_Cerebral_White_Matter (2): linear fit = 1.00 x + 0.0 (44917 voxels, peak = 108), gca=108.5
gca peak = 0.10062 (56)
mri peak = 0.04285 (58)
Left_Cerebral_Cortex (3): linear fit = 1.02 x + 0.0 (16165 voxels, overlap=0.986)
Left_Cerebral_Cortex (3): linear fit = 1.02 x + 0.0 (16165 voxels, peak = 57), gca=57.4
gca peak = 0.11996 (56)
mri peak = 0.03923 (55)
Right_Cerebral_Cortex (42): linear fit = 0.99 x + 0.0 (17327 voxels, overlap=0.996)
Right_Cerebral_Cortex (42): linear fit = 0.99 x + 0.0 (17327 voxels, peak = 55), gca=55.2
gca peak = 0.26053 (71)
mri peak = 0.08617 (71)
Right_Caudate (50): linear fit = 1.00 x + 0.0 (822 voxels, overlap=1.008)
Right_Caudate (50): linear fit = 1.00 x + 0.0 (822 voxels, peak = 71), gca=71.0
gca peak = 0.14677 (74)
mri peak = 0.07356 (69)
Left_Caudate (11): linear fit = 1.00 x + 0.0 (934 voxels, overlap=0.998)
Left_Caudate (11): linear fit = 1.00 x + 0.0 (934 voxels, peak = 74), gca=74.0
gca peak = 0.15083 (51)
mri peak = 0.04977 (51)
Left_Cerebellum_Cortex (8): linear fit = 0.98 x + 0.0 (11277 voxels, overlap=1.000)
Left_Cerebellum_Cortex (8): linear fit = 0.98 x + 0.0 (11277 voxels, peak = 50), gca=49.7
gca peak = 0.16765 (49)
mri peak = 0.05234 (50)
Right_Cerebellum_Cortex (47): linear fit = 1.00 x + 0.0 (11535 voxels, overlap=0.998)
Right_Cerebellum_Cortex (47): linear fit = 1.00 x + 0.0 (11535 voxels, peak = 49), gca=49.0
gca peak = 0.15784 (86)
mri peak = 0.07669 (84)
Left_Cerebellum_White_Matter (7): linear fit = 1.00 x + 0.0 (3599 voxels, overlap=0.985)
Left_Cerebellum_White_Matter (7): linear fit = 1.00 x + 0.0 (3599 voxels, peak = 86), gca=85.6
gca peak = 0.18659 (82)
mri peak = 0.08053 (79)
Right_Cerebellum_White_Matter (46): linear fit = 1.00 x + 0.0 (4178 voxels, overlap=0.970)
Right_Cerebellum_White_Matter (46): linear fit = 1.00 x + 0.0 (4178 voxels, peak = 82), gca=82.0
gca peak = 0.29182 (58)
mri peak = 0.07046 (53)
Left_Amygdala (18): linear fit = 0.99 x + 0.0 (385 voxels, overlap=1.028)
Left_Amygdala (18): linear fit = 0.99 x + 0.0 (385 voxels, peak = 57), gca=57.1
gca peak = 0.30158 (60)
mri peak = 0.06651 (54)
Right_Amygdala (54): linear fit = 1.02 x + 0.0 (438 voxels, overlap=1.018)
Right_Amygdala (54): linear fit = 1.02 x + 0.0 (438 voxels, peak = 62), gca=61.5
gca peak = 0.10953 (93)
mri peak = 0.05839 (91)
Left_Thalamus_Proper (10): linear fit = 1.00 x + 0.0 (3857 voxels, overlap=1.000)
Left_Thalamus_Proper (10): linear fit = 1.00 x + 0.0 (3857 voxels, peak = 93), gca=92.5
gca peak = 0.09822 (90)
mri peak = 0.06185 (91)
Right_Thalamus_Proper (49): linear fit = 1.00 x + 0.0 (3654 voxels, overlap=0.962)
Right_Thalamus_Proper (49): linear fit = 1.00 x + 0.0 (3654 voxels, peak = 90), gca=89.6
gca peak = 0.07460 (79)
mri peak = 0.05070 (81)
Left_Putamen (12): linear fit = 0.99 x + 0.0 (2026 voxels, overlap=0.924)
Left_Putamen (12): linear fit = 0.99 x + 0.0 (2026 voxels, peak = 78), gca=77.8
gca peak = 0.10883 (78)
mri peak = 0.04323 (81)
Right_Putamen (51): linear fit = 1.00 x + 0.0 (2109 voxels, overlap=0.991)
Right_Putamen (51): linear fit = 1.00 x + 0.0 (2109 voxels, peak = 78), gca=77.6
gca peak = 0.07775 (85)
mri peak = 0.11016 (80)
Brain_Stem (16): linear fit = 0.99 x + 0.0 (9595 voxels, overlap=0.681)
Brain_Stem (16): linear fit = 0.99 x + 0.0 (9595 voxels, peak = 84), gca=83.7
gca peak = 0.10844 (88)
mri peak = 0.06559 (87)
Right_VentralDC (60): linear fit = 1.07 x + 0.0 (1171 voxels, overlap=0.804)
Right_VentralDC (60): linear fit = 1.07 x + 0.0 (1171 voxels, peak = 94), gca=93.7
gca peak = 0.14458 (89)
mri peak = 0.06342 (90)
Left_VentralDC (28): linear fit = 1.00 x + 0.0 (1083 voxels, overlap=0.916)
Left_VentralDC (28): linear fit = 1.00 x + 0.0 (1083 voxels, peak = 89), gca=88.6
gca peak = 0.33708 (10)
mri peak = 1.00000 (39)
gca peak = 0.45928 ( 6)
mri peak = 0.14194 ( 3)
Fourth_Ventricle (15): linear fit = 0.35 x + 0.0 (146 voxels, overlap=0.975)
Fourth_Ventricle (15): linear fit = 0.35 x + 0.0 (146 voxels, peak =  2), gca=2.1
gca peak Unknown = 0.94835 ( 0)
gca peak Left_Inf_Lat_Vent = 0.18199 (30)
gca peak Left_Thalamus = 0.64095 (92)
gca peak Third_Ventricle = 0.33708 (10)
gca peak Fourth_Ventricle = 0.45928 ( 6)
gca peak CSF = 0.26605 (13)
gca peak Left_Accumbens_area = 0.64475 (59)
gca peak Left_undetermined = 1.00000 (26)
gca peak Left_vessel = 0.76011 (52)
gca peak Left_choroid_plexus = 0.12089 (35)
gca peak Right_Inf_Lat_Vent = 0.23494 (21)
gca peak Right_Accumbens_area = 0.31948 (69)
gca peak Right_vessel = 0.82109 (52)
gca peak Right_choroid_plexus = 0.14516 (37)
gca peak Fifth_Ventricle = 0.65560 (13)
gca peak WM_hypointensities = 0.06917 (81)
gca peak non_WM_hypointensities = 0.08561 (45)
gca peak Optic_Chiasm = 0.70931 (75)
not using caudate to estimate GM means
estimating mean gm scale to be 1.00 x + 0.0
estimating mean wm scale to be 1.00 x + 0.0
estimating mean csf scale to be 0.59 x + 0.0
saving intensity scales to aseg.auto_noCCseg.label_intensities.txt
saving sequentially combined intensity scales to aseg.auto_noCCseg.label_intensities.txt
 78286 voxels changed in iteration 0 of unlikely voxel relabeling
201 voxels changed in iteration 1 of unlikely voxel relabeling
12 voxels changed in iteration 2 of unlikely voxel relabeling
2 voxels changed in iteration 3 of unlikely voxel relabeling
0 voxels changed in iteration 4 of unlikely voxel relabeling
36324 gm and wm labels changed (%24 to gray, %76 to white out of all changed labels)
316 hippocampal voxels changed.
1 amygdala voxels changed.
pass 1: 78516 changed. image ll: -2.153, PF=0.500
pass 2: 22815 changed. image ll: -2.152, PF=0.500
pass 3: 6834 changed.
pass 4: 2374 changed.
47076 voxels changed in iteration 0 of unlikely voxel relabeling
237 voxels changed in iteration 1 of unlikely voxel relabeling
18 voxels changed in iteration 2 of unlikely voxel relabeling
5 voxels changed in iteration 3 of unlikely voxel relabeling
0 voxels changed in iteration 4 of unlikely voxel relabeling
7284 voxels changed in iteration 0 of unlikely voxel relabeling
39 voxels changed in iteration 1 of unlikely voxel relabeling
0 voxels changed in iteration 2 of unlikely voxel relabeling
6451 voxels changed in iteration 0 of unlikely voxel relabeling
65 voxels changed in iteration 1 of unlikely voxel relabeling
1 voxels changed in iteration 2 of unlikely voxel relabeling
0 voxels changed in iteration 3 of unlikely voxel relabeling
4800 voxels changed in iteration 0 of unlikely voxel relabeling
15 voxels changed in iteration 1 of unlikely voxel relabeling
0 voxels changed in iteration 2 of unlikely voxel relabeling
MRItoUCHAR: min=0, max=85
MRItoUCHAR: converting to UCHAR
writing labeled volume to aseg.auto_noCCseg.mgz
mri_ca_label utimesec    2861.099562
mri_ca_label stimesec    13.470053
mri_ca_label ru_maxrss   2070351872
mri_ca_label ru_ixrss    0
mri_ca_label ru_idrss    0
mri_ca_label ru_isrss    0
mri_ca_label ru_minflt   1958087
mri_ca_label ru_majflt   531
mri_ca_label ru_nswap    0
mri_ca_label ru_inblock  0
mri_ca_label ru_oublock  0
mri_ca_label ru_msgsnd   0
mri_ca_label ru_msgrcv   0
mri_ca_label ru_nsignals 0
mri_ca_label ru_nvcsw    24
mri_ca_label ru_nivcsw   2018110
auto-labeling took 48 minutes and 17 seconds.
\n mri_cc -aseg aseg.auto_noCCseg.mgz -o aseg.auto.mgz -lta /Users/elizavetalavrova/bert/mri/transforms/cc_up.lta bert \n
will read input aseg from aseg.auto_noCCseg.mgz
writing aseg with cc labels to aseg.auto.mgz
will write lta as /Users/elizavetalavrova/bert/mri/transforms/cc_up.lta
reading aseg from /Users/elizavetalavrova/bert/mri/aseg.auto_noCCseg.mgz
reading norm from /Users/elizavetalavrova/bert/mri/norm.mgz
22985 voxels in left wm, 29670 in right wm, xrange [125, 131]
searching rotation angles z=[-6  8], y=[-7  7]
searching scale 1 Z rot 7.4  global minimum found at slice 128.0, rotations (0.67, 0.67)
final transformation (x=128.0, yr=0.665, zr=0.667):
 0.99986  -0.01163   0.01161   0.04286;
 0.01163   0.99993   0.00014   11.50357;
-0.01161   0.00000   0.99993   16.49419;
 0.00000   0.00000   0.00000   1.00000;
updating x range to be [126, 130] in xformed coordinates
best xformed slice 128
cc center is found at 128 115 113
eigenvectors:
-0.00076   0.00300   1.00000;
-0.04964  -0.99876   0.00296;
 0.99877  -0.04964   0.00091;
writing aseg with callosum to /Users/elizavetalavrova/bert/mri/aseg.auto.mgz...
corpus callosum segmentation took 0.5 minutes
#--------------------------------------
#@# Merge ASeg Wed Mar 27 12:30:54 CET 2019
\n cp aseg.auto.mgz aseg.presurf.mgz \n
#--------------------------------------------
#@# Intensity Normalization2 Wed Mar 27 12:30:54 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_normalize -mprage -aseg aseg.presurf.mgz -mask brainmask.mgz norm.mgz brain.mgz \n
assuming input volume is MGH (Van der Kouwe) MP-RAGE
using segmentation for initial intensity normalization
using MR volume brainmask.mgz to mask input volume...
reading from norm.mgz...
Reading aseg aseg.presurf.mgz
normalizing image...
processing with aseg
removing outliers in the aseg WM...
942 control points removed
Building bias image
building Voronoi diagram...
performing soap bubble smoothing, sigma = 0...
Smoothing with sigma 8
Applying bias correction
building Voronoi diagram...
performing soap bubble smoothing, sigma = 8...

Iterating 2 times
---------------------------------
3d normalization pass 1 of 2
white matter peak found at 110
white matter peak found at 107
gm peak at 62 (62), valley at 14 (14)
csf peak at 31, setting threshold to 51
building Voronoi diagram...
performing soap bubble smoothing, sigma = 8...
---------------------------------
3d normalization pass 2 of 2
white matter peak found at 110
white matter peak found at 110
gm peak at 59 (59), valley at 13 (13)
csf peak at 30, setting threshold to 49
building Voronoi diagram...
performing soap bubble smoothing, sigma = 8...
Done iterating ---------------------------------
writing output to brain.mgz
3D bias adjustment took 3 minutes and 32 seconds.
#--------------------------------------------
#@# Mask BFS Wed Mar 27 12:34:28 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_mask -T 5 brain.mgz brainmask.mgz brain.finalsurfs.mgz \n
threshold mask volume at 5
DoAbs = 0
Found 1632604 voxels in mask (pct=  9.73)
Writing masked volume to brain.finalsurfs.mgz...done.
#--------------------------------------------
#@# WM Segmentation Wed Mar 27 12:34:30 CET 2019
\n mri_segment -mprage brain.mgz wm.seg.mgz \n
doing initial intensity segmentation...
using local statistics to label ambiguous voxels...
computing class statistics for intensity windows...
WM (105.0): 106.6 +- 5.3 [79.0 --> 125.0]
GM (67.0) : 65.5 +- 10.3 [30.0 --> 95.0]
setting bottom of white matter range to 75.8
setting top of gray matter range to 86.1
doing initial intensity segmentation...
using local statistics to label ambiguous voxels...
using local geometry to label remaining ambiguous voxels...

reclassifying voxels using Gaussian border classifier...

removing voxels with positive offset direction...
smoothing T1 volume with sigma = 0.250
removing 1-dimensional structures...
10161 sparsely connected voxels removed...
thickening thin strands....
20 segments, 4972 filled
4073 bright non-wm voxels segmented.
5420 diagonally connected voxels added...
white matter segmentation took 1.4 minutes
writing output to wm.seg.mgz...
assuming input volume is MGH (Van der Kouwe) MP-RAGE
\n mri_edit_wm_with_aseg -keep-in wm.seg.mgz brain.mgz aseg.presurf.mgz wm.asegedit.mgz \n
preserving editing changes in input volume...
auto filling took 0.50 minutes
reading wm segmentation from wm.seg.mgz...
81 voxels added to wm to prevent paths from MTL structures to cortex
3151 additional wm voxels added
0 additional wm voxels added
SEG EDIT: 47736 voxels turned on, 27648 voxels turned off.
propagating editing to output volume from wm.seg.mgz
115,126,128 old 110   new 110
115,126,128 old 110   new 110
writing edited volume to wm.asegedit.mgz....
\n mri_pretess wm.asegedit.mgz wm norm.mgz wm.mgz \n

Iteration Number : 1
pass   1 (xy+):  47 found -  47 modified     |    TOTAL:  47
pass   2 (xy+):   0 found -  47 modified     |    TOTAL:  47
pass   1 (xy-):  20 found -  20 modified     |    TOTAL:  67
pass   2 (xy-):   0 found -  20 modified     |    TOTAL:  67
pass   1 (yz+):  65 found -  65 modified     |    TOTAL: 132
pass   2 (yz+):   0 found -  65 modified     |    TOTAL: 132
pass   1 (yz-):  34 found -  34 modified     |    TOTAL: 166
pass   2 (yz-):   0 found -  34 modified     |    TOTAL: 166
pass   1 (xz+):  31 found -  31 modified     |    TOTAL: 197
pass   2 (xz+):   0 found -  31 modified     |    TOTAL: 197
pass   1 (xz-):  44 found -  44 modified     |    TOTAL: 241
pass   2 (xz-):   0 found -  44 modified     |    TOTAL: 241
Iteration Number : 1
pass   1 (+++):  31 found -  31 modified     |    TOTAL:  31
pass   2 (+++):   0 found -  31 modified     |    TOTAL:  31
pass   1 (+++):  28 found -  28 modified     |    TOTAL:  59
pass   2 (+++):   0 found -  28 modified     |    TOTAL:  59
pass   1 (+++):  40 found -  40 modified     |    TOTAL:  99
pass   2 (+++):   0 found -  40 modified     |    TOTAL:  99
pass   1 (+++):  32 found -  32 modified     |    TOTAL: 131
pass   2 (+++):   0 found -  32 modified     |    TOTAL: 131
Iteration Number : 1
pass   1 (++): 166 found - 166 modified     |    TOTAL: 166
pass   2 (++):   0 found - 166 modified     |    TOTAL: 166
pass   1 (+-): 176 found - 176 modified     |    TOTAL: 342
pass   2 (+-):   0 found - 176 modified     |    TOTAL: 342
pass   1 (--): 184 found - 184 modified     |    TOTAL: 526
pass   2 (--):   1 found - 185 modified     |    TOTAL: 527
pass   3 (--):   0 found - 185 modified     |    TOTAL: 527
pass   1 (-+): 172 found - 172 modified     |    TOTAL: 699
pass   2 (-+):   0 found - 172 modified     |    TOTAL: 699
Iteration Number : 2
pass   1 (xy+):   7 found -   7 modified     |    TOTAL:   7
pass   2 (xy+):   0 found -   7 modified     |    TOTAL:   7
pass   1 (xy-):  15 found -  15 modified     |    TOTAL:  22
pass   2 (xy-):   0 found -  15 modified     |    TOTAL:  22
pass   1 (yz+):  15 found -  15 modified     |    TOTAL:  37
pass   2 (yz+):   0 found -  15 modified     |    TOTAL:  37
pass   1 (yz-):   5 found -   5 modified     |    TOTAL:  42
pass   2 (yz-):   0 found -   5 modified     |    TOTAL:  42
pass   1 (xz+):  11 found -  11 modified     |    TOTAL:  53
pass   2 (xz+):   0 found -  11 modified     |    TOTAL:  53
pass   1 (xz-):  13 found -  13 modified     |    TOTAL:  66
pass   2 (xz-):   0 found -  13 modified     |    TOTAL:  66
Iteration Number : 2
pass   1 (+++):   2 found -   2 modified     |    TOTAL:   2
pass   2 (+++):   0 found -   2 modified     |    TOTAL:   2
pass   1 (+++):   4 found -   4 modified     |    TOTAL:   6
pass   2 (+++):   0 found -   4 modified     |    TOTAL:   6
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   6
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   6
Iteration Number : 2
pass   1 (++):   3 found -   3 modified     |    TOTAL:   3
pass   2 (++):   0 found -   3 modified     |    TOTAL:   3
pass   1 (+-):   4 found -   4 modified     |    TOTAL:   7
pass   2 (+-):   0 found -   4 modified     |    TOTAL:   7
pass   1 (--):   2 found -   2 modified     |    TOTAL:   9
pass   2 (--):   0 found -   2 modified     |    TOTAL:   9
pass   1 (-+):   8 found -   8 modified     |    TOTAL:  17
pass   2 (-+):   0 found -   8 modified     |    TOTAL:  17
Iteration Number : 3
pass   1 (xy+):   1 found -   1 modified     |    TOTAL:   1
pass   2 (xy+):   0 found -   1 modified     |    TOTAL:   1
pass   1 (xy-):   0 found -   0 modified     |    TOTAL:   1
pass   1 (yz+):   2 found -   2 modified     |    TOTAL:   3
pass   2 (yz+):   0 found -   2 modified     |    TOTAL:   3
pass   1 (yz-):   0 found -   0 modified     |    TOTAL:   3
pass   1 (xz+):   2 found -   2 modified     |    TOTAL:   5
pass   2 (xz+):   0 found -   2 modified     |    TOTAL:   5
pass   1 (xz-):   0 found -   0 modified     |    TOTAL:   5
Iteration Number : 3
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 3
pass   1 (++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+-):   2 found -   2 modified     |    TOTAL:   2
pass   2 (+-):   0 found -   2 modified     |    TOTAL:   2
pass   1 (--):   1 found -   1 modified     |    TOTAL:   3
pass   2 (--):   0 found -   1 modified     |    TOTAL:   3
pass   1 (-+):   1 found -   1 modified     |    TOTAL:   4
pass   2 (-+):   0 found -   1 modified     |    TOTAL:   4
Iteration Number : 4
pass   1 (xy+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xy-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (yz+):   1 found -   1 modified     |    TOTAL:   1
pass   2 (yz+):   0 found -   1 modified     |    TOTAL:   1
pass   1 (yz-):   0 found -   0 modified     |    TOTAL:   1
pass   1 (xz+):   0 found -   0 modified     |    TOTAL:   1
pass   1 (xz-):   0 found -   0 modified     |    TOTAL:   1
Iteration Number : 4
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 4
pass   1 (++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (--):   0 found -   0 modified     |    TOTAL:   0
pass   1 (-+):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 5
pass   1 (xy+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xy-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (yz+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (yz-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xz+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xz-):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 5
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 5
pass   1 (++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (--):   0 found -   0 modified     |    TOTAL:   0
pass   1 (-+):   0 found -   0 modified     |    TOTAL:   0

Total Number of Modified Voxels = 1170 (out of 597143: 0.195933)
binarizing input wm segmentation...
Ambiguous edge configurations... 

mri_pretess done

#--------------------------------------------
#@# Fill Wed Mar 27 12:36:31 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_fill -a ../scripts/ponscc.cut.log -xform transforms/talairach.lta -segmentation aseg.auto_noCCseg.mgz wm.mgz filled.mgz \n
logging cutting plane coordinates to ../scripts/ponscc.cut.log...
INFO: Using transforms/talairach.lta and its offset for Talairach volume ...
using segmentation aseg.auto_noCCseg.mgz...
reading input volume...done.
searching for cutting planes...voxel to talairach voxel transform
 1.08201  -0.00123   0.03908  -16.84013;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;
voxel to talairach voxel transform
 1.08201  -0.00123   0.03908  -16.84013;
-0.01058   1.11811   0.26468  -53.37259;
-0.04643  -0.23675   0.94552   36.40947;
 0.00000   0.00000   0.00000   1.00000;
reading segmented volume aseg.auto_noCCseg.mgz...
Looking for area (min, max) = (350, 1400)
area[0] = 1891 (min = 350, max = 1400), aspect = 0.73 (min = 0.10, max = 0.75)
need search nearby
using seed (126, 107, 96), TAL = (2.0, -32.0, 21.0)
talairach voxel to voxel transform
 0.92258  -0.00667  -0.03627   16.50101;
-0.00189   0.84434  -0.23628   53.63539;
 0.04483   0.21109   0.99667  -24.26703;
 0.00000   0.00000   0.00000   1.00000;
segmentation indicates cc at (126,  107,  96) --> (2.0, -32.0, 21.0)
done.
writing output to filled.mgz...
filling took 0.6 minutes
talairach cc position changed to (2.00, -32.00, 21.00)
Erasing brainstem...done.
seed_search_size = 9, min_neighbors = 5
search rh wm seed point around talairach space:(20.00, -32.00, 21.00) SRC: (111.94, 121.09, 98.84)
search lh wm seed point around talairach space (-16.00, -32.00, 21.00), SRC: (145.16, 121.03, 100.46)
compute mri_fill using aseg
Erasing Brain Stem and Cerebellum ...
Define left and right masks using aseg:
Building Voronoi diagram ...
Using the Voronoi diagram to separate WM into two hemispheres ...
Find the largest connected component for each hemisphere ...
#--------------------------------------------
#@# Tessellate lh Wed Mar 27 12:37:10 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mri_pretess ../mri/filled.mgz 255 ../mri/norm.mgz ../mri/filled-pretess255.mgz \n

Iteration Number : 1
pass   1 (xy+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xy-):   2 found -   2 modified     |    TOTAL:   2
pass   2 (xy-):   0 found -   2 modified     |    TOTAL:   2
pass   1 (yz+):   4 found -   4 modified     |    TOTAL:   6
pass   2 (yz+):   0 found -   4 modified     |    TOTAL:   6
pass   1 (yz-):   1 found -   1 modified     |    TOTAL:   7
pass   2 (yz-):   0 found -   1 modified     |    TOTAL:   7
pass   1 (xz+):   4 found -   4 modified     |    TOTAL:  11
pass   2 (xz+):   0 found -   4 modified     |    TOTAL:  11
pass   1 (xz-):   0 found -   0 modified     |    TOTAL:  11
Iteration Number : 1
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 1
pass   1 (++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+-):   1 found -   1 modified     |    TOTAL:   1
pass   2 (+-):   0 found -   1 modified     |    TOTAL:   1
pass   1 (--):   1 found -   1 modified     |    TOTAL:   2
pass   2 (--):   0 found -   1 modified     |    TOTAL:   2
pass   1 (-+):   0 found -   0 modified     |    TOTAL:   2
Iteration Number : 2
pass   1 (xy+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xy-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (yz+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (yz-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xz+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xz-):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 2
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 2
pass   1 (++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (--):   0 found -   0 modified     |    TOTAL:   0
pass   1 (-+):   0 found -   0 modified     |    TOTAL:   0

Total Number of Modified Voxels = 13 (out of 292094: 0.004451)
Ambiguous edge configurations... 

mri_pretess done

\n mri_tessellate ../mri/filled-pretess255.mgz 255 ../surf/lh.orig.nofix \n
$Id: mri_tessellate.c,v 1.38.2.1 2016/07/26 18:46:38 zkaufman Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
slice 40: 1561 vertices, 1715 faces
slice 50: 8372 vertices, 8680 faces
slice 60: 18675 vertices, 19091 faces
slice 70: 30483 vertices, 30946 faces
slice 80: 41571 vertices, 41979 faces
slice 90: 53961 vertices, 54357 faces
slice 100: 66189 vertices, 66642 faces
slice 110: 78134 vertices, 78571 faces
slice 120: 89348 vertices, 89810 faces
slice 130: 99896 vertices, 100317 faces
slice 140: 110259 vertices, 110703 faces
slice 150: 120047 vertices, 120453 faces
slice 160: 128274 vertices, 128657 faces
slice 170: 135901 vertices, 136264 faces
slice 180: 142314 vertices, 142620 faces
slice 190: 147994 vertices, 148274 faces
slice 200: 152156 vertices, 152378 faces
slice 210: 153356 vertices, 153476 faces
slice 220: 153356 vertices, 153476 faces
slice 230: 153356 vertices, 153476 faces
slice 240: 153356 vertices, 153476 faces
slice 250: 153356 vertices, 153476 faces
using the conformed surface RAS to save vertex points...
writing ../surf/lh.orig.nofix
using vox2ras matrix:
-1.00000   0.00000   0.00000   128.00000;
 0.00000   0.00000   1.00000  -128.00000;
 0.00000  -1.00000   0.00000   128.00000;
 0.00000   0.00000   0.00000   1.00000;
\n rm -f ../mri/filled-pretess255.mgz \n
\n mris_extract_main_component ../surf/lh.orig.nofix ../surf/lh.orig.nofix \n

counting number of connected components...
   153356 voxel in cpt #1: X=-120 [v=153356,e=460428,f=306952] located at (-26.612015, -16.918594, 5.797048)
For the whole surface: X=-120 [v=153356,e=460428,f=306952]
One single component has been found
nothing to do
done

#--------------------------------------------
#@# Tessellate rh Wed Mar 27 12:37:17 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mri_pretess ../mri/filled.mgz 127 ../mri/norm.mgz ../mri/filled-pretess127.mgz \n

Iteration Number : 1
pass   1 (xy+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xy-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (yz+):   6 found -   6 modified     |    TOTAL:   6
pass   2 (yz+):   0 found -   6 modified     |    TOTAL:   6
pass   1 (yz-):   0 found -   0 modified     |    TOTAL:   6
pass   1 (xz+):   1 found -   1 modified     |    TOTAL:   7
pass   2 (xz+):   0 found -   1 modified     |    TOTAL:   7
pass   1 (xz-):   1 found -   1 modified     |    TOTAL:   8
pass   2 (xz-):   0 found -   1 modified     |    TOTAL:   8
Iteration Number : 1
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 1
pass   1 (++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (--):   0 found -   0 modified     |    TOTAL:   0
pass   1 (-+):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 2
pass   1 (xy+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xy-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (yz+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (yz-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xz+):   0 found -   0 modified     |    TOTAL:   0
pass   1 (xz-):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 2
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+++):   0 found -   0 modified     |    TOTAL:   0
Iteration Number : 2
pass   1 (++):   0 found -   0 modified     |    TOTAL:   0
pass   1 (+-):   0 found -   0 modified     |    TOTAL:   0
pass   1 (--):   0 found -   0 modified     |    TOTAL:   0
pass   1 (-+):   0 found -   0 modified     |    TOTAL:   0

Total Number of Modified Voxels = 8 (out of 291731: 0.002742)
Ambiguous edge configurations... 

mri_pretess done

\n mri_tessellate ../mri/filled-pretess127.mgz 127 ../surf/rh.orig.nofix \n
$Id: mri_tessellate.c,v 1.38.2.1 2016/07/26 18:46:38 zkaufman Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
slice 40: 522 vertices, 599 faces
slice 50: 5405 vertices, 5664 faces
slice 60: 15076 vertices, 15461 faces
slice 70: 27257 vertices, 27697 faces
slice 80: 39620 vertices, 40093 faces
slice 90: 51448 vertices, 51884 faces
slice 100: 63423 vertices, 63855 faces
slice 110: 75505 vertices, 75961 faces
slice 120: 86929 vertices, 87384 faces
slice 130: 97935 vertices, 98427 faces
slice 140: 108797 vertices, 109250 faces
slice 150: 118950 vertices, 119342 faces
slice 160: 127496 vertices, 127918 faces
slice 170: 135696 vertices, 136066 faces
slice 180: 142724 vertices, 143064 faces
slice 190: 148952 vertices, 149244 faces
slice 200: 152992 vertices, 153243 faces
slice 210: 154280 vertices, 154406 faces
slice 220: 154280 vertices, 154406 faces
slice 230: 154280 vertices, 154406 faces
slice 240: 154280 vertices, 154406 faces
slice 250: 154280 vertices, 154406 faces
using the conformed surface RAS to save vertex points...
writing ../surf/rh.orig.nofix
using vox2ras matrix:
-1.00000   0.00000   0.00000   128.00000;
 0.00000   0.00000   1.00000  -128.00000;
 0.00000  -1.00000   0.00000   128.00000;
 0.00000   0.00000   0.00000   1.00000;
\n rm -f ../mri/filled-pretess127.mgz \n
\n mris_extract_main_component ../surf/rh.orig.nofix ../surf/rh.orig.nofix \n

counting number of connected components...
   154280 voxel in cpt #1: X=-126 [v=154280,e=463218,f=308812] located at (26.442696, -14.645340, 5.889377)
For the whole surface: X=-126 [v=154280,e=463218,f=308812]
One single component has been found
nothing to do
done

#--------------------------------------------
#@# Smooth1 lh Wed Mar 27 12:37:23 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_smooth -nw -seed 1234 ../surf/lh.orig.nofix ../surf/lh.smoothwm.nofix \n
setting seed for random number generator to 1234
smoothing surface tessellation for 10 iterations...
smoothing complete - recomputing first and second fundamental forms...
#--------------------------------------------
#@# Smooth1 rh Wed Mar 27 12:37:32 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_smooth -nw -seed 1234 ../surf/rh.orig.nofix ../surf/rh.smoothwm.nofix \n
setting seed for random number generator to 1234
smoothing surface tessellation for 10 iterations...
smoothing complete - recomputing first and second fundamental forms...
#--------------------------------------------
#@# Inflation1 lh Wed Mar 27 12:37:41 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_inflate -no-save-sulc ../surf/lh.smoothwm.nofix ../surf/lh.inflated.nofix \n
Not saving sulc
Reading ../surf/lh.smoothwm.nofix
avg radius = 49.9 mm, total surface area = 78921 mm^2
writing inflated surface to ../surf/lh.inflated.nofix
inflation took 0.6 minutes
step 060: RMS=0.041 (target=0.015)   
inflation complete.
Not saving sulc
mris_inflate utimesec    33.243254
mris_inflate stimesec    0.326109
mris_inflate ru_maxrss   204308480
mris_inflate ru_ixrss    0
mris_inflate ru_idrss    0
mris_inflate ru_isrss    0
mris_inflate ru_minflt   49638
mris_inflate ru_majflt   393
mris_inflate ru_nswap    0
mris_inflate ru_inblock  0
mris_inflate ru_oublock  0
mris_inflate ru_msgsnd   0
mris_inflate ru_msgrcv   0
mris_inflate ru_nsignals 0
mris_inflate ru_nvcsw    5
mris_inflate ru_nivcsw   40670
#--------------------------------------------
#@# Inflation1 rh Wed Mar 27 12:38:19 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_inflate -no-save-sulc ../surf/rh.smoothwm.nofix ../surf/rh.inflated.nofix \n
Not saving sulc
Reading ../surf/rh.smoothwm.nofix
avg radius = 49.2 mm, total surface area = 78818 mm^2
writing inflated surface to ../surf/rh.inflated.nofix
inflation took 0.5 minutes
step 060: RMS=0.044 (target=0.015)   
inflation complete.
Not saving sulc
mris_inflate utimesec    30.782566
mris_inflate stimesec    0.254838
mris_inflate ru_maxrss   208125952
mris_inflate ru_ixrss    0
mris_inflate ru_idrss    0
mris_inflate ru_isrss    0
mris_inflate ru_minflt   50977
mris_inflate ru_majflt   0
mris_inflate ru_nswap    0
mris_inflate ru_inblock  0
mris_inflate ru_oublock  0
mris_inflate ru_msgsnd   0
mris_inflate ru_msgrcv   0
mris_inflate ru_nsignals 0
mris_inflate ru_nvcsw    3
mris_inflate ru_nivcsw   30936
#--------------------------------------------
#@# QSphere lh Wed Mar 27 12:38:51 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_sphere -q -seed 1234 ../surf/lh.inflated.nofix ../surf/lh.qsphere.nofix \n
doing quick spherical unfolding.
setting seed for random number genererator to 1234
$Id: mris_sphere.c,v 1.61 2016/01/20 23:42:15 greve Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading original vertex positions...
unfolding cortex into spherical form...
surface projected - minimizing metric distortion...
vertex spacing 0.92 +- 0.58 (0.00-->5.90) (max @ vno 85210 --> 86329)
face area 0.02 +- 0.03 (-0.08-->0.48)

== Number of threads available to mris_sphere for OpenMP = 1 == 
scaling brain by 0.290...
inflating to sphere (rms error < 2.00)
000: dt: 0.0000, rms radial error=176.987, avgs=0
005/300: dt: 0.9000, rms radial error=176.727, avgs=0
010/300: dt: 0.9000, rms radial error=176.168, avgs=0
015/300: dt: 0.9000, rms radial error=175.433, avgs=0
020/300: dt: 0.9000, rms radial error=174.595, avgs=0
025/300: dt: 0.9000, rms radial error=173.698, avgs=0
030/300: dt: 0.9000, rms radial error=172.768, avgs=0
035/300: dt: 0.9000, rms radial error=171.821, avgs=0
040/300: dt: 0.9000, rms radial error=170.871, avgs=0
045/300: dt: 0.9000, rms radial error=169.923, avgs=0
050/300: dt: 0.9000, rms radial error=168.976, avgs=0
055/300: dt: 0.9000, rms radial error=168.031, avgs=0
060/300: dt: 0.9000, rms radial error=167.090, avgs=0
065/300: dt: 0.9000, rms radial error=166.154, avgs=0
070/300: dt: 0.9000, rms radial error=165.222, avgs=0
075/300: dt: 0.9000, rms radial error=164.295, avgs=0
080/300: dt: 0.9000, rms radial error=163.373, avgs=0
085/300: dt: 0.9000, rms radial error=162.457, avgs=0
090/300: dt: 0.9000, rms radial error=161.544, avgs=0
095/300: dt: 0.9000, rms radial error=160.637, avgs=0
100/300: dt: 0.9000, rms radial error=159.735, avgs=0
105/300: dt: 0.9000, rms radial error=158.838, avgs=0
110/300: dt: 0.9000, rms radial error=157.946, avgs=0
115/300: dt: 0.9000, rms radial error=157.058, avgs=0
120/300: dt: 0.9000, rms radial error=156.176, avgs=0
125/300: dt: 0.9000, rms radial error=155.298, avgs=0
130/300: dt: 0.9000, rms radial error=154.424, avgs=0
135/300: dt: 0.9000, rms radial error=153.556, avgs=0
140/300: dt: 0.9000, rms radial error=152.692, avgs=0
145/300: dt: 0.9000, rms radial error=151.833, avgs=0
150/300: dt: 0.9000, rms radial error=150.978, avgs=0
155/300: dt: 0.9000, rms radial error=150.128, avgs=0
160/300: dt: 0.9000, rms radial error=149.283, avgs=0
165/300: dt: 0.9000, rms radial error=148.442, avgs=0
170/300: dt: 0.9000, rms radial error=147.606, avgs=0
175/300: dt: 0.9000, rms radial error=146.774, avgs=0
180/300: dt: 0.9000, rms radial error=145.947, avgs=0
185/300: dt: 0.9000, rms radial error=145.125, avgs=0
190/300: dt: 0.9000, rms radial error=144.307, avgs=0
195/300: dt: 0.9000, rms radial error=143.494, avgs=0
200/300: dt: 0.9000, rms radial error=142.685, avgs=0
205/300: dt: 0.9000, rms radial error=141.881, avgs=0
210/300: dt: 0.9000, rms radial error=141.082, avgs=0
215/300: dt: 0.9000, rms radial error=140.287, avgs=0
220/300: dt: 0.9000, rms radial error=139.497, avgs=0
225/300: dt: 0.9000, rms radial error=138.711, avgs=0
230/300: dt: 0.9000, rms radial error=137.929, avgs=0
235/300: dt: 0.9000, rms radial error=137.152, avgs=0
240/300: dt: 0.9000, rms radial error=136.380, avgs=0
245/300: dt: 0.9000, rms radial error=135.611, avgs=0
250/300: dt: 0.9000, rms radial error=134.847, avgs=0
255/300: dt: 0.9000, rms radial error=134.087, avgs=0
260/300: dt: 0.9000, rms radial error=133.331, avgs=0
265/300: dt: 0.9000, rms radial error=132.580, avgs=0
270/300: dt: 0.9000, rms radial error=131.832, avgs=0
275/300: dt: 0.9000, rms radial error=131.089, avgs=0
280/300: dt: 0.9000, rms radial error=130.350, avgs=0
285/300: dt: 0.9000, rms radial error=129.615, avgs=0
290/300: dt: 0.9000, rms radial error=128.884, avgs=0
295/300: dt: 0.9000, rms radial error=128.158, avgs=0
300/300: dt: 0.9000, rms radial error=127.435, avgs=0

spherical inflation complete.
epoch 1 (K=10.0), pass 1, starting sse = 18443.66
taking momentum steps...
taking momentum steps...
taking momentum steps...
pass 1 complete, delta sse/iter = 0.00/10 = 0.00018
epoch 2 (K=40.0), pass 1, starting sse = 3301.34
taking momentum steps...
taking momentum steps...
taking momentum steps...
pass 1 complete, delta sse/iter = 0.00/10 = 0.00012
epoch 3 (K=160.0), pass 1, starting sse = 399.44
taking momentum steps...
taking momentum steps...
taking momentum steps...
pass 1 complete, delta sse/iter = 0.09/11 = 0.00785
epoch 4 (K=640.0), pass 1, starting sse = 29.86
taking momentum steps...
taking momentum steps...
taking momentum steps...
pass 1 complete, delta sse/iter = 0.17/14 = 0.01244
final distance error %29.03
writing spherical brain to ../surf/lh.qsphere.nofix
spherical transformation took 0.05 hours
mris_sphere utimesec    193.035693
mris_sphere stimesec    1.266795
mris_sphere ru_maxrss   209285120
mris_sphere ru_ixrss    0
mris_sphere ru_idrss    0
mris_sphere ru_isrss    0
mris_sphere ru_minflt   50843
mris_sphere ru_majflt   406
mris_sphere ru_nswap    0
mris_sphere ru_inblock  0
mris_sphere ru_oublock  0
mris_sphere ru_msgsnd   0
mris_sphere ru_msgrcv   0
mris_sphere ru_nsignals 0
mris_sphere ru_nvcsw    4
mris_sphere ru_nivcsw   220363
FSRUNTIME@ mris_sphere  0.0547 hours 1 threads
#--------------------------------------------
#@# QSphere rh Wed Mar 27 12:42:08 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_sphere -q -seed 1234 ../surf/rh.inflated.nofix ../surf/rh.qsphere.nofix \n
doing quick spherical unfolding.
setting seed for random number genererator to 1234
$Id: mris_sphere.c,v 1.61 2016/01/20 23:42:15 greve Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading original vertex positions...
unfolding cortex into spherical form...
surface projected - minimizing metric distortion...
vertex spacing 0.93 +- 0.58 (0.00-->6.47) (max @ vno 114968 --> 114969)
face area 0.02 +- 0.03 (-0.12-->0.65)

== Number of threads available to mris_sphere for OpenMP = 1 == 
scaling brain by 0.296...
inflating to sphere (rms error < 2.00)
000: dt: 0.0000, rms radial error=176.555, avgs=0
005/300: dt: 0.9000, rms radial error=176.293, avgs=0
010/300: dt: 0.9000, rms radial error=175.733, avgs=0
015/300: dt: 0.9000, rms radial error=174.996, avgs=0
020/300: dt: 0.9000, rms radial error=174.156, avgs=0
025/300: dt: 0.9000, rms radial error=173.263, avgs=0
030/300: dt: 0.9000, rms radial error=172.343, avgs=0
035/300: dt: 0.9000, rms radial error=171.408, avgs=0
040/300: dt: 0.9000, rms radial error=170.465, avgs=0
045/300: dt: 0.9000, rms radial error=169.520, avgs=0
050/300: dt: 0.9000, rms radial error=168.576, avgs=0
055/300: dt: 0.9000, rms radial error=167.634, avgs=0
060/300: dt: 0.9000, rms radial error=166.697, avgs=0
065/300: dt: 0.9000, rms radial error=165.763, avgs=0
070/300: dt: 0.9000, rms radial error=164.835, avgs=0
075/300: dt: 0.9000, rms radial error=163.911, avgs=0
080/300: dt: 0.9000, rms radial error=162.993, avgs=0
085/300: dt: 0.9000, rms radial error=162.079, avgs=0
090/300: dt: 0.9000, rms radial error=161.170, avgs=0
095/300: dt: 0.9000, rms radial error=160.266, avgs=0
100/300: dt: 0.9000, rms radial error=159.368, avgs=0
105/300: dt: 0.9000, rms radial error=158.473, avgs=0
110/300: dt: 0.9000, rms radial error=157.584, avgs=0
115/300: dt: 0.9000, rms radial error=156.699, avgs=0
120/300: dt: 0.9000, rms radial error=155.820, avgs=0
125/300: dt: 0.9000, rms radial error=154.946, avgs=0
130/300: dt: 0.9000, rms radial error=154.077, avgs=0
135/300: dt: 0.9000, rms radial error=153.212, avgs=0
140/300: dt: 0.9000, rms radial error=152.352, avgs=0
145/300: dt: 0.9000, rms radial error=151.497, avgs=0
150/300: dt: 0.9000, rms radial error=150.646, avgs=0
155/300: dt: 0.9000, rms radial error=149.801, avgs=0
160/300: dt: 0.9000, rms radial error=148.959, avgs=0
165/300: dt: 0.9000, rms radial error=148.123, avgs=0
170/300: dt: 0.9000, rms radial error=147.291, avgs=0
175/300: dt: 0.9000, rms radial error=146.463, avgs=0
180/300: dt: 0.9000, rms radial error=145.640, avgs=0
185/300: dt: 0.9000, rms radial error=144.822, avgs=0
190/300: dt: 0.9000, rms radial error=144.008, avgs=0
195/300: dt: 0.9000, rms radial error=143.198, avgs=0
200/300: dt: 0.9000, rms radial error=142.393, avgs=0
205/300: dt: 0.9000, rms radial error=141.592, avgs=0
210/300: dt: 0.9000, rms radial error=140.796, avgs=0
215/300: dt: 0.9000, rms radial error=140.003, avgs=0
220/300: dt: 0.9000, rms radial error=139.216, avgs=0
225/300: dt: 0.9000, rms radial error=138.432, avgs=0
230/300: dt: 0.9000, rms radial error=137.653, avgs=0
235/300: dt: 0.9000, rms radial error=136.879, avgs=0
240/300: dt: 0.9000, rms radial error=136.108, avgs=0
245/300: dt: 0.9000, rms radial error=135.343, avgs=0
250/300: dt: 0.9000, rms radial error=134.581, avgs=0
255/300: dt: 0.9000, rms radial error=133.823, avgs=0
260/300: dt: 0.9000, rms radial error=133.070, avgs=0
265/300: dt: 0.9000, rms radial error=132.321, avgs=0
270/300: dt: 0.9000, rms radial error=131.576, avgs=0
275/300: dt: 0.9000, rms radial error=130.836, avgs=0
280/300: dt: 0.9000, rms radial error=130.099, avgs=0
285/300: dt: 0.9000, rms radial error=129.366, avgs=0
290/300: dt: 0.9000, rms radial error=128.638, avgs=0
295/300: dt: 0.9000, rms radial error=127.913, avgs=0
300/300: dt: 0.9000, rms radial error=127.193, avgs=0

spherical inflation complete.
epoch 1 (K=10.0), pass 1, starting sse = 18459.55
taking momentum steps...
taking momentum steps...
taking momentum steps...
pass 1 complete, delta sse/iter = 0.00/10 = 0.00012
epoch 2 (K=40.0), pass 1, starting sse = 3267.44
taking momentum steps...
taking momentum steps...
taking momentum steps...
pass 1 complete, delta sse/iter = 0.00/10 = 0.00004
epoch 3 (K=160.0), pass 1, starting sse = 381.30
taking momentum steps...
taking momentum steps...
taking momentum steps...
pass 1 complete, delta sse/iter = 0.06/10 = 0.00573
epoch 4 (K=640.0), pass 1, starting sse = 30.24
taking momentum steps...
taking momentum steps...
taking momentum steps...
pass 1 complete, delta sse/iter = 0.10/14 = 0.00728
final distance error %28.59
writing spherical brain to ../surf/rh.qsphere.nofix
spherical transformation took 0.05 hours
mris_sphere utimesec    190.595703
mris_sphere stimesec    0.996904
mris_sphere ru_maxrss   210866176
mris_sphere ru_ixrss    0
mris_sphere ru_idrss    0
mris_sphere ru_isrss    0
mris_sphere ru_minflt   51890
mris_sphere ru_majflt   0
mris_sphere ru_nswap    0
mris_sphere ru_inblock  0
mris_sphere ru_oublock  0
mris_sphere ru_msgsnd   0
mris_sphere ru_msgrcv   0
mris_sphere ru_nsignals 0
mris_sphere ru_nvcsw    3
mris_sphere ru_nivcsw   158189
FSRUNTIME@ mris_sphere  0.0538 hours 1 threads
#--------------------------------------------
#@# Fix Topology Copy lh Wed Mar 27 12:45:21 CET 2019
/Users/elizavetalavrova/bert/scripts
\n cp ../surf/lh.orig.nofix ../surf/lh.orig \n
\n cp ../surf/lh.inflated.nofix ../surf/lh.inflated \n
#--------------------------------------------
#@# Fix Topology Copy rh Wed Mar 27 12:45:22 CET 2019
/Users/elizavetalavrova/bert/scripts
\n cp ../surf/rh.orig.nofix ../surf/rh.orig \n
\n cp ../surf/rh.inflated.nofix ../surf/rh.inflated \n
#@# Fix Topology lh Wed Mar 27 12:45:22 CET 2019
\n mris_fix_topology -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_fix_topology.lh.dat -mgz -sphere qsphere.nofix -ga -seed 1234 bert lh \n
reading spherical homeomorphism from 'qsphere.nofix'
using genetic algorithm with optimized parameters
setting seed for random number genererator to 1234

*************************************************************
Topology Correction Parameters
retessellation mode:           genetic search
number of patches/generation : 10
number of generations :        10
surface mri loglikelihood coefficient :         1.0
volume mri loglikelihood coefficient :          10.0
normal dot loglikelihood coefficient :          1.0
quadratic curvature loglikelihood coefficient : 1.0
volume resolution :                             2
eliminate vertices during search :              1
initial patch selection :                       1
select all defect vertices :                    0
ordering dependant retessellation:              0
use precomputed edge table :                    0
smooth retessellated patch :                    2
match retessellated patch :                     1
verbose mode :                                  0

*************************************************************
INFO: assuming .mgz format
$Id: mris_fix_topology.c,v 1.50.2.1 2016/10/27 22:25:58 zkaufman Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
before topology correction, eno=-120 (nv=153356, nf=306952, ne=460428, g=61)
using quasi-homeomorphic spherical map to tessellate cortical surface...

Correction of the Topology
Finding true center and radius of Spherical Surface...done
Surface centered at (0,0,0) with radius 100.0 in 9 iterations
marking ambiguous vertices...
5256 ambiguous faces found in tessellation
segmenting defects...
74 defects found, arbitrating ambiguous regions...
analyzing neighboring defects...
      -merging segment 35 into 34
      -merging segment 40 into 39
72 defects to be corrected 
0 vertices coincident
reading input surface /Users/elizavetalavrova/bert/surf/lh.qsphere.nofix...
reading brain volume from brain...
reading wm segmentation from wm...
Computing Initial Surface Statistics
      -face       loglikelihood: -9.5929  (-4.7965)
      -vertex     loglikelihood: -6.6820  (-3.3410)
      -normal dot loglikelihood: -3.6047  (-3.6047)
      -quad curv  loglikelihood: -6.4745  (-3.2372)
      Total Loglikelihood : -26.3541

CORRECTING DEFECT 0 (vertices=36, convex hull=70, v0=190)
After retessellation of defect 0 (v0=190), euler #=-71 (149922,447878,297885) : difference with theory (-69) = 2 

CORRECTING DEFECT 1 (vertices=49, convex hull=65, v0=737)
After retessellation of defect 1 (v0=737), euler #=-70 (149931,447932,297931) : difference with theory (-68) = 2 

CORRECTING DEFECT 2 (vertices=6, convex hull=19, v0=1692)
After retessellation of defect 2 (v0=1692), euler #=-69 (149932,447937,297936) : difference with theory (-67) = 2 

CORRECTING DEFECT 3 (vertices=38, convex hull=66, v0=3362)
After retessellation of defect 3 (v0=3362), euler #=-68 (149941,447991,297982) : difference with theory (-66) = 2 

CORRECTING DEFECT 4 (vertices=36, convex hull=75, v0=3862)
After retessellation of defect 4 (v0=3862), euler #=-67 (149957,448074,298050) : difference with theory (-65) = 2 

CORRECTING DEFECT 5 (vertices=44, convex hull=84, v0=5016)
After retessellation of defect 5 (v0=5016), euler #=-66 (149985,448195,298144) : difference with theory (-64) = 2 

CORRECTING DEFECT 6 (vertices=29, convex hull=63, v0=5063)
After retessellation of defect 6 (v0=5063), euler #=-65 (149996,448255,298194) : difference with theory (-63) = 2 

CORRECTING DEFECT 7 (vertices=38, convex hull=82, v0=5256)
After retessellation of defect 7 (v0=5256), euler #=-64 (150016,448346,298266) : difference with theory (-62) = 2 

CORRECTING DEFECT 8 (vertices=21, convex hull=67, v0=6821)
After retessellation of defect 8 (v0=6821), euler #=-63 (150028,448405,298314) : difference with theory (-61) = 2 

CORRECTING DEFECT 9 (vertices=25, convex hull=71, v0=12227)
After retessellation of defect 9 (v0=12227), euler #=-62 (150039,448462,298361) : difference with theory (-60) = 2 

CORRECTING DEFECT 10 (vertices=303, convex hull=157, v0=13861)
After retessellation of defect 10 (v0=13861), euler #=-61 (150090,448687,298536) : difference with theory (-59) = 2 

CORRECTING DEFECT 11 (vertices=46, convex hull=81, v0=15712)
After retessellation of defect 11 (v0=15712), euler #=-60 (150118,448808,298630) : difference with theory (-58) = 2 

CORRECTING DEFECT 12 (vertices=54, convex hull=115, v0=19996)
After retessellation of defect 12 (v0=19996), euler #=-59 (150151,448960,298750) : difference with theory (-57) = 2 

CORRECTING DEFECT 13 (vertices=52, convex hull=69, v0=24098)
After retessellation of defect 13 (v0=24098), euler #=-58 (150177,449071,298836) : difference with theory (-56) = 2 

CORRECTING DEFECT 14 (vertices=28, convex hull=58, v0=25133)
After retessellation of defect 14 (v0=25133), euler #=-57 (150188,449127,298882) : difference with theory (-55) = 2 

CORRECTING DEFECT 15 (vertices=39, convex hull=58, v0=25167)
After retessellation of defect 15 (v0=25167), euler #=-56 (150202,449191,298933) : difference with theory (-54) = 2 

CORRECTING DEFECT 16 (vertices=17, convex hull=44, v0=27383)
After retessellation of defect 16 (v0=27383), euler #=-55 (150211,449234,298968) : difference with theory (-53) = 2 

CORRECTING DEFECT 17 (vertices=45, convex hull=58, v0=33723)
After retessellation of defect 17 (v0=33723), euler #=-54 (150227,449304,299023) : difference with theory (-52) = 2 

CORRECTING DEFECT 18 (vertices=19, convex hull=49, v0=33893)
After retessellation of defect 18 (v0=33893), euler #=-53 (150236,449351,299062) : difference with theory (-51) = 2 

CORRECTING DEFECT 19 (vertices=45, convex hull=80, v0=33957)
After retessellation of defect 19 (v0=33957), euler #=-52 (150245,449410,299113) : difference with theory (-50) = 2 

CORRECTING DEFECT 20 (vertices=10, convex hull=13, v0=39795)
After retessellation of defect 20 (v0=39795), euler #=-51 (150247,449418,299120) : difference with theory (-49) = 2 

CORRECTING DEFECT 21 (vertices=73, convex hull=112, v0=46239)
After retessellation of defect 21 (v0=46239), euler #=-50 (150288,449590,299252) : difference with theory (-48) = 2 

CORRECTING DEFECT 22 (vertices=32, convex hull=63, v0=47776)
After retessellation of defect 22 (v0=47776), euler #=-49 (150309,449675,299317) : difference with theory (-47) = 2 

CORRECTING DEFECT 23 (vertices=38, convex hull=83, v0=50264)
After retessellation of defect 23 (v0=50264), euler #=-48 (150336,449787,299403) : difference with theory (-46) = 2 

CORRECTING DEFECT 24 (vertices=28, convex hull=47, v0=56205)
After retessellation of defect 24 (v0=56205), euler #=-47 (150348,449842,299447) : difference with theory (-45) = 2 

CORRECTING DEFECT 25 (vertices=8, convex hull=28, v0=57308)
After retessellation of defect 25 (v0=57308), euler #=-46 (150349,449852,299457) : difference with theory (-44) = 2 

CORRECTING DEFECT 26 (vertices=29, convex hull=61, v0=63496)
After retessellation of defect 26 (v0=63496), euler #=-45 (150358,449899,299496) : difference with theory (-43) = 2 

CORRECTING DEFECT 27 (vertices=26, convex hull=29, v0=66963)
After retessellation of defect 27 (v0=66963), euler #=-44 (150362,449919,299513) : difference with theory (-42) = 2 

CORRECTING DEFECT 28 (vertices=38, convex hull=58, v0=67229)
After retessellation of defect 28 (v0=67229), euler #=-43 (150375,449980,299562) : difference with theory (-41) = 2 

CORRECTING DEFECT 29 (vertices=21, convex hull=47, v0=67570)
After retessellation of defect 29 (v0=67570), euler #=-42 (150383,450022,299597) : difference with theory (-40) = 2 

CORRECTING DEFECT 30 (vertices=33, convex hull=47, v0=76246)
After retessellation of defect 30 (v0=76246), euler #=-41 (150395,450075,299639) : difference with theory (-39) = 2 

CORRECTING DEFECT 31 (vertices=27, convex hull=50, v0=81367)
After retessellation of defect 31 (v0=81367), euler #=-40 (150404,450124,299680) : difference with theory (-38) = 2 

CORRECTING DEFECT 32 (vertices=156, convex hull=64, v0=82320)
After retessellation of defect 32 (v0=82320), euler #=-39 (150442,450266,299785) : difference with theory (-37) = 2 

CORRECTING DEFECT 33 (vertices=33, convex hull=48, v0=99176)
After retessellation of defect 33 (v0=99176), euler #=-38 (150460,450338,299840) : difference with theory (-36) = 2 

CORRECTING DEFECT 34 (vertices=49, convex hull=39, v0=100660)
After retessellation of defect 34 (v0=100660), euler #=-36 (150466,450370,299868) : difference with theory (-35) = 1 

CORRECTING DEFECT 35 (vertices=19, convex hull=34, v0=101532)
After retessellation of defect 35 (v0=101532), euler #=-35 (150470,450393,299888) : difference with theory (-34) = 1 

CORRECTING DEFECT 36 (vertices=21, convex hull=31, v0=102649)
After retessellation of defect 36 (v0=102649), euler #=-34 (150476,450419,299909) : difference with theory (-33) = 1 

CORRECTING DEFECT 37 (vertices=29, convex hull=66, v0=105056)
After retessellation of defect 37 (v0=105056), euler #=-33 (150493,450496,299970) : difference with theory (-32) = 1 

CORRECTING DEFECT 38 (vertices=65, convex hull=88, v0=105764)
After retessellation of defect 38 (v0=105764), euler #=-31 (150525,450632,300076) : difference with theory (-31) = 0 

CORRECTING DEFECT 39 (vertices=78, convex hull=69, v0=106756)
After retessellation of defect 39 (v0=106756), euler #=-30 (150534,450687,300123) : difference with theory (-30) = 0 

CORRECTING DEFECT 40 (vertices=17, convex hull=31, v0=106865)
After retessellation of defect 40 (v0=106865), euler #=-29 (150538,450709,300142) : difference with theory (-29) = 0 

CORRECTING DEFECT 41 (vertices=178, convex hull=154, v0=107861)
After retessellation of defect 41 (v0=107861), euler #=-28 (150604,450987,300355) : difference with theory (-28) = 0 

CORRECTING DEFECT 42 (vertices=52, convex hull=45, v0=111280)
After retessellation of defect 42 (v0=111280), euler #=-27 (150616,451039,300396) : difference with theory (-27) = 0 

CORRECTING DEFECT 43 (vertices=6, convex hull=22, v0=112032)
After retessellation of defect 43 (v0=112032), euler #=-26 (150617,451047,300404) : difference with theory (-26) = 0 

CORRECTING DEFECT 44 (vertices=28, convex hull=71, v0=112111)
After retessellation of defect 44 (v0=112111), euler #=-25 (150626,451103,300452) : difference with theory (-25) = 0 

CORRECTING DEFECT 45 (vertices=7, convex hull=26, v0=112273)
After retessellation of defect 45 (v0=112273), euler #=-24 (150627,451112,300461) : difference with theory (-24) = 0 

CORRECTING DEFECT 46 (vertices=22, convex hull=42, v0=113133)
After retessellation of defect 46 (v0=113133), euler #=-23 (150638,451159,300498) : difference with theory (-23) = 0 

CORRECTING DEFECT 47 (vertices=16, convex hull=38, v0=113334)
After retessellation of defect 47 (v0=113334), euler #=-22 (150639,451174,300513) : difference with theory (-22) = 0 

CORRECTING DEFECT 48 (vertices=31, convex hull=29, v0=114129)
After retessellation of defect 48 (v0=114129), euler #=-21 (150646,451205,300538) : difference with theory (-21) = 0 

CORRECTING DEFECT 49 (vertices=20, convex hull=43, v0=114417)
After retessellation of defect 49 (v0=114417), euler #=-20 (150654,451245,300571) : difference with theory (-20) = 0 

CORRECTING DEFECT 50 (vertices=181, convex hull=153, v0=115113)
After retessellation of defect 50 (v0=115113), euler #=-19 (150714,451490,300757) : difference with theory (-19) = 0 

CORRECTING DEFECT 51 (vertices=12, convex hull=37, v0=116163)
After retessellation of defect 51 (v0=116163), euler #=-18 (150716,451508,300774) : difference with theory (-18) = 0 

CORRECTING DEFECT 52 (vertices=20, convex hull=27, v0=117759)
After retessellation of defect 52 (v0=117759), euler #=-17 (150720,451527,300790) : difference with theory (-17) = 0 

CORRECTING DEFECT 53 (vertices=140, convex hull=122, v0=118842)
After retessellation of defect 53 (v0=118842), euler #=-16 (150781,451763,300966) : difference with theory (-16) = 0 

CORRECTING DEFECT 54 (vertices=9, convex hull=21, v0=118926)
After retessellation of defect 54 (v0=118926), euler #=-15 (150782,451769,300972) : difference with theory (-15) = 0 

CORRECTING DEFECT 55 (vertices=44, convex hull=80, v0=119375)
After retessellation of defect 55 (v0=119375), euler #=-14 (150813,451897,301070) : difference with theory (-14) = 0 

CORRECTING DEFECT 56 (vertices=70, convex hull=100, v0=119879)
After retessellation of defect 56 (v0=119879), euler #=-13 (150847,452047,301187) : difference with theory (-13) = 0 

CORRECTING DEFECT 57 (vertices=43, convex hull=47, v0=121744)
After retessellation of defect 57 (v0=121744), euler #=-12 (150862,452107,301233) : difference with theory (-12) = 0 

CORRECTING DEFECT 58 (vertices=46, convex hull=71, v0=124178)
After retessellation of defect 58 (v0=124178), euler #=-11 (150882,452196,301303) : difference with theory (-11) = 0 

CORRECTING DEFECT 59 (vertices=178, convex hull=163, v0=124906)
After retessellation of defect 59 (v0=124906), euler #=-10 (150927,452409,301472) : difference with theory (-10) = 0 

CORRECTING DEFECT 60 (vertices=77, convex hull=83, v0=126432)
After retessellation of defect 60 (v0=126432), euler #=-9 (150953,452526,301564) : difference with theory (-9) = 0 

CORRECTING DEFECT 61 (vertices=62, convex hull=76, v0=126664)
After retessellation of defect 61 (v0=126664), euler #=-8 (150965,452595,301622) : difference with theory (-8) = 0 

CORRECTING DEFECT 62 (vertices=46, convex hull=95, v0=129101)
After retessellation of defect 62 (v0=129101), euler #=-7 (150997,452732,301728) : difference with theory (-7) = 0 

CORRECTING DEFECT 63 (vertices=104, convex hull=103, v0=131436)
After retessellation of defect 63 (v0=131436), euler #=-6 (151030,452881,301845) : difference with theory (-6) = 0 

CORRECTING DEFECT 64 (vertices=23, convex hull=61, v0=132302)
After retessellation of defect 64 (v0=132302), euler #=-5 (151043,452947,301899) : difference with theory (-5) = 0 

CORRECTING DEFECT 65 (vertices=31, convex hull=86, v0=132981)
After retessellation of defect 65 (v0=132981), euler #=-4 (151063,453042,301975) : difference with theory (-4) = 0 

CORRECTING DEFECT 66 (vertices=8, convex hull=29, v0=135061)
After retessellation of defect 66 (v0=135061), euler #=-3 (151065,453054,301986) : difference with theory (-3) = 0 

CORRECTING DEFECT 67 (vertices=45, convex hull=83, v0=136680)
After retessellation of defect 67 (v0=136680), euler #=-2 (151095,453178,302081) : difference with theory (-2) = 0 

CORRECTING DEFECT 68 (vertices=88, convex hull=112, v0=137823)
After retessellation of defect 68 (v0=137823), euler #=-1 (151134,453347,302212) : difference with theory (-1) = 0 

CORRECTING DEFECT 69 (vertices=29, convex hull=52, v0=139289)
After retessellation of defect 69 (v0=139289), euler #=0 (151148,453410,302262) : difference with theory (0) = 0 

CORRECTING DEFECT 70 (vertices=20, convex hull=52, v0=145384)
After retessellation of defect 70 (v0=145384), euler #=1 (151159,453463,302305) : difference with theory (1) = 0 

CORRECTING DEFECT 71 (vertices=6, convex hull=21, v0=151576)
After retessellation of defect 71 (v0=151576), euler #=2 (151159,453471,302314) : difference with theory (2) = 0 
computing original vertex metric properties...
storing new metric properties...
computing tessellation statistics...
vertex spacing 0.88 +- 0.23 (0.07-->6.19) (max @ vno 45293 --> 52779)
face area 0.00 +- 0.00 (0.00-->0.00)
performing soap bubble on retessellated vertices for 0 iterations...
vertex spacing 0.88 +- 0.23 (0.07-->6.19) (max @ vno 45293 --> 52779)
face area 0.00 +- 0.00 (0.00-->0.00)
tessellation finished, orienting corrected surface...
243 mutations (37.8%), 400 crossovers (62.2%), 111 vertices were eliminated
building final representation...
2197 vertices and 0 faces have been removed from triangulation
after topology correction, eno=2 (nv=151159, nf=302314, ne=453471, g=0)
writing corrected surface to /Users/elizavetalavrova/bert/surf/lh.orig...

0.000 % of the vertices (0 vertices) exhibit an orientation change
topology fixing took 28.0 minutes
0 defective edges
removing intersecting faces
000: 311 intersecting
001: 5 intersecting
mris_fix_topology utimesec    1658.916718
mris_fix_topology stimesec    6.150717
mris_fix_topology ru_maxrss   505978880
mris_fix_topology ru_ixrss    0
mris_fix_topology ru_idrss    0
mris_fix_topology ru_isrss    0
mris_fix_topology ru_minflt   169313
mris_fix_topology ru_majflt   472
mris_fix_topology ru_nswap    0
mris_fix_topology ru_inblock  0
mris_fix_topology ru_oublock  0
mris_fix_topology ru_msgsnd   0
mris_fix_topology ru_msgrcv   0
mris_fix_topology ru_nsignals 0
mris_fix_topology ru_nvcsw    8
mris_fix_topology ru_nivcsw   1017951
FSRUNTIME@ mris_fix_topology lh  0.4667 hours 1 threads
#@# Fix Topology rh Wed Mar 27 13:13:22 CET 2019
\n mris_fix_topology -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_fix_topology.rh.dat -mgz -sphere qsphere.nofix -ga -seed 1234 bert rh \n
reading spherical homeomorphism from 'qsphere.nofix'
using genetic algorithm with optimized parameters
setting seed for random number genererator to 1234

*************************************************************
Topology Correction Parameters
retessellation mode:           genetic search
number of patches/generation : 10
number of generations :        10
surface mri loglikelihood coefficient :         1.0
volume mri loglikelihood coefficient :          10.0
normal dot loglikelihood coefficient :          1.0
quadratic curvature loglikelihood coefficient : 1.0
volume resolution :                             2
eliminate vertices during search :              1
initial patch selection :                       1
select all defect vertices :                    0
ordering dependant retessellation:              0
use precomputed edge table :                    0
smooth retessellated patch :                    2
match retessellated patch :                     1
verbose mode :                                  0

*************************************************************
INFO: assuming .mgz format
$Id: mris_fix_topology.c,v 1.50.2.1 2016/10/27 22:25:58 zkaufman Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
before topology correction, eno=-126 (nv=154280, nf=308812, ne=463218, g=64)
using quasi-homeomorphic spherical map to tessellate cortical surface...

Correction of the Topology
Finding true center and radius of Spherical Surface...done
Surface centered at (0,0,0) with radius 100.0 in 9 iterations
marking ambiguous vertices...
7363 ambiguous faces found in tessellation
segmenting defects...
69 defects found, arbitrating ambiguous regions...
analyzing neighboring defects...
      -merging segment 20 into 25
      -merging segment 47 into 44
      -merging segment 48 into 44
66 defects to be corrected 
0 vertices coincident
reading input surface /Users/elizavetalavrova/bert/surf/rh.qsphere.nofix...
reading brain volume from brain...
reading wm segmentation from wm...
Computing Initial Surface Statistics
      -face       loglikelihood: -9.5862  (-4.7931)
      -vertex     loglikelihood: -6.6833  (-3.3417)
      -normal dot loglikelihood: -3.6316  (-3.6316)
      -quad curv  loglikelihood: -6.6039  (-3.3019)
      Total Loglikelihood : -26.5049

CORRECTING DEFECT 0 (vertices=25, convex hull=18, v0=117)
After retessellation of defect 0 (v0=117), euler #=-63 (149735,447269,297471) : difference with theory (-63) = 0 

CORRECTING DEFECT 1 (vertices=54, convex hull=80, v0=420)
After retessellation of defect 1 (v0=420), euler #=-62 (149761,447380,297557) : difference with theory (-62) = 0 

CORRECTING DEFECT 2 (vertices=43, convex hull=70, v0=3267)
After retessellation of defect 2 (v0=3267), euler #=-61 (149771,447440,297608) : difference with theory (-61) = 0 

CORRECTING DEFECT 3 (vertices=32, convex hull=61, v0=3546)
After retessellation of defect 3 (v0=3546), euler #=-60 (149793,447532,297679) : difference with theory (-60) = 0 

CORRECTING DEFECT 4 (vertices=41, convex hull=84, v0=4066)
After retessellation of defect 4 (v0=4066), euler #=-59 (149808,447615,297748) : difference with theory (-59) = 0 

CORRECTING DEFECT 5 (vertices=9, convex hull=20, v0=4606)
After retessellation of defect 5 (v0=4606), euler #=-58 (149808,447623,297757) : difference with theory (-58) = 0 

CORRECTING DEFECT 6 (vertices=58, convex hull=60, v0=9693)
After retessellation of defect 6 (v0=9693), euler #=-57 (149823,447690,297810) : difference with theory (-57) = 0 

CORRECTING DEFECT 7 (vertices=29, convex hull=55, v0=10476)
After retessellation of defect 7 (v0=10476), euler #=-56 (149838,447754,297860) : difference with theory (-56) = 0 

CORRECTING DEFECT 8 (vertices=27, convex hull=67, v0=10667)
After retessellation of defect 8 (v0=10667), euler #=-55 (149850,447816,297911) : difference with theory (-55) = 0 

CORRECTING DEFECT 9 (vertices=35, convex hull=68, v0=11042)
After retessellation of defect 9 (v0=11042), euler #=-54 (149865,447884,297965) : difference with theory (-54) = 0 

CORRECTING DEFECT 10 (vertices=82, convex hull=101, v0=17900)
After retessellation of defect 10 (v0=17900), euler #=-53 (149890,448002,298059) : difference with theory (-53) = 0 

CORRECTING DEFECT 11 (vertices=55, convex hull=74, v0=18287)
After retessellation of defect 11 (v0=18287), euler #=-52 (149904,448073,298117) : difference with theory (-52) = 0 

CORRECTING DEFECT 12 (vertices=11, convex hull=28, v0=19364)
After retessellation of defect 12 (v0=19364), euler #=-51 (149906,448087,298130) : difference with theory (-51) = 0 

CORRECTING DEFECT 13 (vertices=58, convex hull=75, v0=19714)
After retessellation of defect 13 (v0=19714), euler #=-50 (149925,448176,298201) : difference with theory (-50) = 0 

CORRECTING DEFECT 14 (vertices=26, convex hull=84, v0=20844)
After retessellation of defect 14 (v0=20844), euler #=-49 (149944,448269,298276) : difference with theory (-49) = 0 

CORRECTING DEFECT 15 (vertices=189, convex hull=242, v0=23021)
After retessellation of defect 15 (v0=23021), euler #=-49 (150006,448579,298524) : difference with theory (-48) = 1 

CORRECTING DEFECT 16 (vertices=55, convex hull=85, v0=23191)
After retessellation of defect 16 (v0=23191), euler #=-48 (150023,448666,298595) : difference with theory (-47) = 1 

CORRECTING DEFECT 17 (vertices=31, convex hull=73, v0=25117)
After retessellation of defect 17 (v0=25117), euler #=-47 (150034,448724,298643) : difference with theory (-46) = 1 

CORRECTING DEFECT 18 (vertices=37, convex hull=87, v0=34415)
After retessellation of defect 18 (v0=34415), euler #=-46 (150052,448809,298711) : difference with theory (-45) = 1 

CORRECTING DEFECT 19 (vertices=40, convex hull=26, v0=41070)
After retessellation of defect 19 (v0=41070), euler #=-45 (150054,448824,298725) : difference with theory (-44) = 1 

CORRECTING DEFECT 20 (vertices=6, convex hull=12, v0=57317)
After retessellation of defect 20 (v0=57317), euler #=-44 (150055,448829,298730) : difference with theory (-43) = 1 

CORRECTING DEFECT 21 (vertices=23, convex hull=45, v0=57606)
After retessellation of defect 21 (v0=57606), euler #=-43 (150069,448885,298773) : difference with theory (-42) = 1 

CORRECTING DEFECT 22 (vertices=44, convex hull=71, v0=57700)
After retessellation of defect 22 (v0=57700), euler #=-42 (150093,448989,298854) : difference with theory (-41) = 1 

CORRECTING DEFECT 23 (vertices=570, convex hull=200, v0=58280)
After retessellation of defect 23 (v0=58280), euler #=-41 (150147,449249,299061) : difference with theory (-40) = 1 

CORRECTING DEFECT 24 (vertices=66, convex hull=105, v0=58641)
After retessellation of defect 24 (v0=58641), euler #=-39 (150169,449360,299152) : difference with theory (-39) = 0 

CORRECTING DEFECT 25 (vertices=22, convex hull=27, v0=65310)
After retessellation of defect 25 (v0=65310), euler #=-38 (150173,449382,299171) : difference with theory (-38) = 0 

CORRECTING DEFECT 26 (vertices=59, convex hull=71, v0=70673)
After retessellation of defect 26 (v0=70673), euler #=-37 (150212,449531,299282) : difference with theory (-37) = 0 

CORRECTING DEFECT 27 (vertices=31, convex hull=90, v0=74613)
After retessellation of defect 27 (v0=74613), euler #=-36 (150234,449631,299361) : difference with theory (-36) = 0 

CORRECTING DEFECT 28 (vertices=51, convex hull=68, v0=76344)
After retessellation of defect 28 (v0=76344), euler #=-35 (150251,449710,299424) : difference with theory (-35) = 0 

CORRECTING DEFECT 29 (vertices=19, convex hull=49, v0=79154)
After retessellation of defect 29 (v0=79154), euler #=-34 (150261,449758,299463) : difference with theory (-34) = 0 

CORRECTING DEFECT 30 (vertices=5, convex hull=15, v0=80599)
After retessellation of defect 30 (v0=80599), euler #=-33 (150262,449764,299469) : difference with theory (-33) = 0 

CORRECTING DEFECT 31 (vertices=67, convex hull=72, v0=81490)
After retessellation of defect 31 (v0=81490), euler #=-32 (150292,449882,299558) : difference with theory (-32) = 0 

CORRECTING DEFECT 32 (vertices=11, convex hull=31, v0=83384)
After retessellation of defect 32 (v0=83384), euler #=-31 (150294,449898,299573) : difference with theory (-31) = 0 

CORRECTING DEFECT 33 (vertices=113, convex hull=47, v0=86673)
After retessellation of defect 33 (v0=86673), euler #=-30 (150304,449949,299615) : difference with theory (-30) = 0 

CORRECTING DEFECT 34 (vertices=21, convex hull=43, v0=88586)
After retessellation of defect 34 (v0=88586), euler #=-29 (150313,449992,299650) : difference with theory (-29) = 0 

CORRECTING DEFECT 35 (vertices=93, convex hull=102, v0=93177)
After retessellation of defect 35 (v0=93177), euler #=-28 (150340,450118,299750) : difference with theory (-28) = 0 

CORRECTING DEFECT 36 (vertices=53, convex hull=99, v0=100988)
After retessellation of defect 36 (v0=100988), euler #=-27 (150366,450236,299843) : difference with theory (-27) = 0 

CORRECTING DEFECT 37 (vertices=7, convex hull=21, v0=101093)
After retessellation of defect 37 (v0=101093), euler #=-26 (150367,450243,299850) : difference with theory (-26) = 0 

CORRECTING DEFECT 38 (vertices=45, convex hull=34, v0=102204)
After retessellation of defect 38 (v0=102204), euler #=-25 (150371,450269,299873) : difference with theory (-25) = 0 

CORRECTING DEFECT 39 (vertices=44, convex hull=80, v0=102371)
After retessellation of defect 39 (v0=102371), euler #=-24 (150384,450344,299936) : difference with theory (-24) = 0 

CORRECTING DEFECT 40 (vertices=921, convex hull=241, v0=103044)
After retessellation of defect 40 (v0=103044), euler #=-24 (150441,450641,300176) : difference with theory (-23) = 1 

CORRECTING DEFECT 41 (vertices=34, convex hull=35, v0=106202)
After retessellation of defect 41 (v0=106202), euler #=-23 (150447,450674,300204) : difference with theory (-22) = 1 

CORRECTING DEFECT 42 (vertices=14, convex hull=17, v0=107297)
After retessellation of defect 42 (v0=107297), euler #=-22 (150448,450682,300212) : difference with theory (-21) = 1 

CORRECTING DEFECT 43 (vertices=125, convex hull=104, v0=108537)
After retessellation of defect 43 (v0=108537), euler #=-19 (150493,450873,300361) : difference with theory (-20) = -1 

CORRECTING DEFECT 44 (vertices=30, convex hull=66, v0=108802)
After retessellation of defect 44 (v0=108802), euler #=-18 (150506,450940,300416) : difference with theory (-19) = -1 

CORRECTING DEFECT 45 (vertices=74, convex hull=55, v0=109489)
After retessellation of defect 45 (v0=109489), euler #=-17 (150523,451011,300471) : difference with theory (-18) = -1 

CORRECTING DEFECT 46 (vertices=64, convex hull=81, v0=113181)
After retessellation of defect 46 (v0=113181), euler #=-16 (150547,451112,300549) : difference with theory (-17) = -1 

CORRECTING DEFECT 47 (vertices=26, convex hull=35, v0=114873)
After retessellation of defect 47 (v0=114873), euler #=-15 (150552,451137,300570) : difference with theory (-16) = -1 

CORRECTING DEFECT 48 (vertices=37, convex hull=43, v0=116713)
After retessellation of defect 48 (v0=116713), euler #=-14 (150561,451180,300605) : difference with theory (-15) = -1 

CORRECTING DEFECT 49 (vertices=103, convex hull=128, v0=117779)
After retessellation of defect 49 (v0=117779), euler #=-13 (150596,451346,300737) : difference with theory (-14) = -1 

CORRECTING DEFECT 50 (vertices=5, convex hull=24, v0=120003)
After retessellation of defect 50 (v0=120003), euler #=-12 (150597,451355,300746) : difference with theory (-13) = -1 

CORRECTING DEFECT 51 (vertices=67, convex hull=55, v0=121166)
After retessellation of defect 51 (v0=121166), euler #=-12 (150609,451418,300797) : difference with theory (-12) = 0 

CORRECTING DEFECT 52 (vertices=187, convex hull=113, v0=125653)
After retessellation of defect 52 (v0=125653), euler #=-11 (150651,451597,300935) : difference with theory (-11) = 0 

CORRECTING DEFECT 53 (vertices=115, convex hull=122, v0=127393)
After retessellation of defect 53 (v0=127393), euler #=-10 (150687,451761,301064) : difference with theory (-10) = 0 

CORRECTING DEFECT 54 (vertices=37, convex hull=84, v0=132233)
After retessellation of defect 54 (v0=132233), euler #=-9 (150708,451861,301144) : difference with theory (-9) = 0 

CORRECTING DEFECT 55 (vertices=46, convex hull=63, v0=136386)
After retessellation of defect 55 (v0=136386), euler #=-8 (150717,451911,301186) : difference with theory (-8) = 0 

CORRECTING DEFECT 56 (vertices=48, convex hull=63, v0=136965)
After retessellation of defect 56 (v0=136965), euler #=-7 (150730,451976,301239) : difference with theory (-7) = 0 

CORRECTING DEFECT 57 (vertices=16, convex hull=44, v0=140684)
After retessellation of defect 57 (v0=140684), euler #=-6 (150734,452004,301264) : difference with theory (-6) = 0 

CORRECTING DEFECT 58 (vertices=31, convex hull=54, v0=140703)
After retessellation of defect 58 (v0=140703), euler #=-5 (150751,452075,301319) : difference with theory (-5) = 0 

CORRECTING DEFECT 59 (vertices=41, convex hull=81, v0=143442)
After retessellation of defect 59 (v0=143442), euler #=-4 (150765,452148,301379) : difference with theory (-4) = 0 

CORRECTING DEFECT 60 (vertices=39, convex hull=62, v0=146018)
After retessellation of defect 60 (v0=146018), euler #=-3 (150774,452201,301424) : difference with theory (-3) = 0 

CORRECTING DEFECT 61 (vertices=12, convex hull=18, v0=146628)
After retessellation of defect 61 (v0=146628), euler #=-2 (150775,452211,301434) : difference with theory (-2) = 0 

CORRECTING DEFECT 62 (vertices=68, convex hull=96, v0=148383)
After retessellation of defect 62 (v0=148383), euler #=-1 (150805,452342,301536) : difference with theory (-1) = 0 

CORRECTING DEFECT 63 (vertices=25, convex hull=57, v0=148999)
After retessellation of defect 63 (v0=148999), euler #=0 (150817,452396,301579) : difference with theory (0) = 0 

CORRECTING DEFECT 64 (vertices=45, convex hull=43, v0=150391)
After retessellation of defect 64 (v0=150391), euler #=1 (150830,452452,301623) : difference with theory (1) = 0 

CORRECTING DEFECT 65 (vertices=42, convex hull=77, v0=153054)
After retessellation of defect 65 (v0=153054), euler #=2 (150852,452550,301700) : difference with theory (2) = 0 
computing original vertex metric properties...
storing new metric properties...
computing tessellation statistics...
vertex spacing 0.88 +- 0.26 (0.04-->28.34) (max @ vno 109220 --> 130794)
face area 0.00 +- 0.00 (0.00-->0.00)
performing soap bubble on retessellated vertices for 0 iterations...
vertex spacing 0.88 +- 0.26 (0.04-->28.34) (max @ vno 109220 --> 130794)
face area 0.00 +- 0.00 (0.00-->0.00)
tessellation finished, orienting corrected surface...
230 mutations (33.4%), 459 crossovers (66.6%), 429 vertices were eliminated
building final representation...
3428 vertices and 0 faces have been removed from triangulation
after topology correction, eno=2 (nv=150852, nf=301700, ne=452550, g=0)
writing corrected surface to /Users/elizavetalavrova/bert/surf/rh.orig...

0.000 % of the vertices (0 vertices) exhibit an orientation change
topology fixing took 35.7 minutes
0 defective edges
removing intersecting faces
000: 529 intersecting
001: 17 intersecting
mris_fix_topology utimesec    2135.790165
mris_fix_topology stimesec    3.552344
mris_fix_topology ru_maxrss   519667712
mris_fix_topology ru_ixrss    0
mris_fix_topology ru_idrss    0
mris_fix_topology ru_isrss    0
mris_fix_topology ru_minflt   167987
mris_fix_topology ru_majflt   88
mris_fix_topology ru_nswap    0
mris_fix_topology ru_inblock  0
mris_fix_topology ru_oublock  0
mris_fix_topology ru_msgsnd   0
mris_fix_topology ru_msgrcv   0
mris_fix_topology ru_nsignals 0
mris_fix_topology ru_nvcsw    18
mris_fix_topology ru_nivcsw   430727
FSRUNTIME@ mris_fix_topology rh  0.5953 hours 1 threads
\n mris_euler_number ../surf/lh.orig \n
euler # = v-e+f = 2g-2: 151159 - 453471 + 302314 = 2 --> 0 holes
      F =2V-4:          302314 = 302318-4 (0)
      2E=3F:            906942 = 906942 (0)

total defect index = 0
\n mris_euler_number ../surf/rh.orig \n
euler # = v-e+f = 2g-2: 150852 - 452550 + 301700 = 2 --> 0 holes
      F =2V-4:          301700 = 301704-4 (0)
      2E=3F:            905100 = 905100 (0)

total defect index = 0
/Users/elizavetalavrova/bert/scripts
\n mris_remove_intersection ../surf/lh.orig ../surf/lh.orig \n
intersection removal took 0.00 hours
removing intersecting faces
000: 13 intersecting
writing corrected surface to ../surf/lh.orig
\n rm ../surf/lh.inflated \n
/Users/elizavetalavrova/bert/scripts
\n mris_remove_intersection ../surf/rh.orig ../surf/rh.orig \n
intersection removal took 0.00 hours
removing intersecting faces
000: 78 intersecting
writing corrected surface to ../surf/rh.orig
\n rm ../surf/rh.inflated \n
#--------------------------------------------
#@# Make White Surf lh Wed Mar 27 13:49:14 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_make_surfaces -aseg ../mri/aseg.presurf -white white.preaparc -noaparc -whiteonly -mgz -T1 brain.finalsurfs bert lh \n
using white.preaparc as white matter name...
only generating white matter surface
using aseg volume ../mri/aseg.presurf to prevent surfaces crossing the midline
not using aparc to prevent surfaces crossing the midline
INFO: assuming MGZ format for volumes.
using brain.finalsurfs as T1 volume...
$Id: mris_make_surfaces.c,v 1.164.2.4 2016/12/13 22:26:32 zkaufman Exp $
$Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading volume /Users/elizavetalavrova/bert/mri/filled.mgz...
reading volume /Users/elizavetalavrova/bert/mri/brain.finalsurfs.mgz...
reading volume /Users/elizavetalavrova/bert/mri/../mri/aseg.presurf.mgz...
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
37202 bright wm thresholded.
4434 bright non-wm voxels segmented.
reading original surface position from /Users/elizavetalavrova/bert/surf/lh.orig...
computing class statistics...
border white:    284022 voxels (1.69%)
border gray      322545 voxels (1.92%)
WM (95.0): 95.8 +- 9.4 [70.0 --> 110.0]
GM (66.0) : 65.1 +- 11.3 [30.0 --> 110.0]
setting MIN_GRAY_AT_WHITE_BORDER to 49.7 (was 70)
setting MAX_BORDER_WHITE to 109.4 (was 105)
setting MIN_BORDER_WHITE to 61.0 (was 85)
setting MAX_CSF to 38.4 (was 40)
setting MAX_GRAY to 90.6 (was 95)
setting MAX_GRAY_AT_CSF_BORDER to 49.7 (was 75)
setting MIN_GRAY_AT_CSF_BORDER to 27.1 (was 40)
repositioning cortical surface to gray/white boundary
smoothing T1 volume with sigma = 2.000
vertex spacing 0.81 +- 0.23 (0.03-->3.19) (max @ vno 45293 --> 52779)
face area 0.27 +- 0.13 (0.00-->2.01)
mean absolute distance = 0.74 +- 0.93
3621 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
using class modes intead of means, discounting robust sigmas....
intensity peaks found at WM=100+-7.8,    GM=61+-8.7
mean inside = 90.7, mean outside = 69.0
smoothing surface for 5 iterations...
inhibiting deformation at non-cortical midline structures...
removing 4 vertex label from ripped group
mean border=74.1, 49 (49) missing vertices, mean dist 0.3 [0.7 (%34.5)->0.8 (%65.5))]
%63 local maxima, %32 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=4, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
complete_dist_mat 0
rms 0
smooth_averages 0
remove_neg 0
ico_order 0
which_surface 0
target_radius 0.000000
nfields 0
scale 0.000000
desired_rms_height 0.000000
momentum 0.000000
nbhd_size 0
max_nbrs 0
niterations 25
nsurfaces 0
SURFACES 3
flags 0 (0)
use curv 0
no sulc 0
no rigid align 0
mris->nsize 2
mris->hemisphere 0
randomSeed 0

smoothing T1 volume with sigma = 1.000
vertex spacing 0.91 +- 0.26 (0.07-->4.16) (max @ vno 107108 --> 107107)
face area 0.27 +- 0.13 (0.00-->2.41)
mean absolute distance = 0.37 +- 0.64
4207 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=4958138.0, rms=12.220
001: dt: 0.5000, sse=2782103.0, rms=8.725 (28.603%)
002: dt: 0.5000, sse=1847177.8, rms=6.633 (23.980%)
003: dt: 0.5000, sse=1399340.5, rms=5.346 (19.396%)
004: dt: 0.5000, sse=1197990.2, rms=4.651 (12.998%)
005: dt: 0.5000, sse=1116149.8, rms=4.330 (6.894%)
006: dt: 0.5000, sse=1080483.5, rms=4.185 (3.367%)
007: dt: 0.5000, sse=1068810.5, rms=4.123 (1.473%)
rms = 4.08, time step reduction 1 of 3 to 0.250...
008: dt: 0.5000, sse=1058329.8, rms=4.081 (1.022%)
009: dt: 0.2500, sse=815781.7, rms=2.790 (31.621%)
010: dt: 0.2500, sse=754874.2, rms=2.377 (14.808%)
011: dt: 0.2500, sse=743195.2, rms=2.284 (3.906%)
012: dt: 0.2500, sse=733557.8, rms=2.208 (3.322%)
rms = 2.19, time step reduction 2 of 3 to 0.125...
013: dt: 0.2500, sse=731339.8, rms=2.186 (1.015%)
014: dt: 0.1250, sse=709964.7, rms=1.999 (8.542%)
rms = 1.98, time step reduction 3 of 3 to 0.062...
015: dt: 0.1250, sse=707483.7, rms=1.978 (1.077%)
positioning took 1.8 minutes
inhibiting deformation at non-cortical midline structures...
removing 3 vertex label from ripped group
mean border=77.7, 69 (12) missing vertices, mean dist -0.2 [0.4 (%70.8)->0.2 (%29.2))]
%73 local maxima, %23 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=1.0, host=mbp-e, nav=2, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.500
vertex spacing 0.90 +- 0.25 (0.09-->4.67) (max @ vno 107108 --> 107107)
face area 0.35 +- 0.16 (0.00-->3.27)
mean absolute distance = 0.29 +- 0.45
4048 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1474540.6, rms=4.980
016: dt: 0.5000, sse=1134761.2, rms=3.592 (27.883%)
rms = 3.94, time step reduction 1 of 3 to 0.250...
017: dt: 0.2500, sse=949050.9, rms=2.567 (28.528%)
018: dt: 0.2500, sse=885169.8, rms=2.092 (18.504%)
019: dt: 0.2500, sse=857701.4, rms=1.865 (10.826%)
rms = 1.83, time step reduction 2 of 3 to 0.125...
020: dt: 0.2500, sse=853479.0, rms=1.831 (1.850%)
021: dt: 0.1250, sse=837340.4, rms=1.662 (9.202%)
rms = 1.65, time step reduction 3 of 3 to 0.062...
022: dt: 0.1250, sse=835900.2, rms=1.645 (1.049%)
positioning took 0.9 minutes
inhibiting deformation at non-cortical midline structures...
removing 2 vertex label from ripped group
removing 4 vertex label from ripped group
removing 3 vertex label from ripped group
removing 4 vertex label from ripped group
mean border=80.3, 73 (10) missing vertices, mean dist -0.2 [0.3 (%66.5)->0.2 (%33.5))]
%82 local maxima, %13 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=0.5, host=mbp-e, nav=1, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.250
vertex spacing 0.89 +- 0.25 (0.07-->5.08) (max @ vno 107108 --> 107107)
face area 0.34 +- 0.16 (0.00-->3.16)
mean absolute distance = 0.25 +- 0.38
3589 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1102797.1, rms=3.554
023: dt: 0.5000, sse=1091260.4, rms=3.478 (2.126%)
rms = 3.85, time step reduction 1 of 3 to 0.250...
024: dt: 0.2500, sse=894756.1, rms=2.314 (33.464%)
025: dt: 0.2500, sse=839225.1, rms=1.854 (19.861%)
026: dt: 0.2500, sse=822209.4, rms=1.703 (8.187%)
rms = 1.70, time step reduction 2 of 3 to 0.125...
027: dt: 0.2500, sse=820944.4, rms=1.701 (0.100%)
028: dt: 0.1250, sse=802369.0, rms=1.489 (12.455%)
rms = 1.47, time step reduction 3 of 3 to 0.062...
029: dt: 0.1250, sse=800499.9, rms=1.473 (1.111%)
positioning took 0.9 minutes
inhibiting deformation at non-cortical midline structures...
removing 2 vertex label from ripped group
removing 2 vertex label from ripped group
removing 3 vertex label from ripped group
mean border=81.3, 100 (5) missing vertices, mean dist -0.1 [0.3 (%55.2)->0.2 (%44.8))]
%86 local maxima, % 9 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=0.2, host=mbp-e, nav=0, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
writing white matter surface to /Users/elizavetalavrova/bert/surf/lh.white.preaparc...
writing smoothed curvature to lh.curv
000: dt: 0.0000, sse=839367.2, rms=1.972
rms = 2.47, time step reduction 1 of 3 to 0.250...
030: dt: 0.2500, sse=778404.6, rms=1.340 (32.051%)
031: dt: 0.2500, sse=759318.4, rms=1.073 (19.884%)
rms = 1.08, time step reduction 2 of 3 to 0.125...
rms = 1.06, time step reduction 3 of 3 to 0.062...
032: dt: 0.1250, sse=758136.1, rms=1.064 (0.870%)
positioning took 0.5 minutes
generating cortex label...
4 non-cortical segments detected
only using segment with 7671 vertices
erasing segment 1 (vno[0] = 96316)
erasing segment 2 (vno[0] = 103035)
erasing segment 3 (vno[0] = 106062)
writing cortex label to /Users/elizavetalavrova/bert/label/lh.cortex.label...
writing curvature file /Users/elizavetalavrova/bert/surf/lh.curv
writing smoothed area to lh.area
writing curvature file /Users/elizavetalavrova/bert/surf/lh.area
vertex spacing 0.89 +- 0.25 (0.05-->5.09) (max @ vno 107107 --> 107108)
face area 0.33 +- 0.16 (0.00-->3.03)
refinement took 5.8 minutes
#--------------------------------------------
#@# Make White Surf rh Wed Mar 27 13:55:01 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_make_surfaces -aseg ../mri/aseg.presurf -white white.preaparc -noaparc -whiteonly -mgz -T1 brain.finalsurfs bert rh \n
using white.preaparc as white matter name...
only generating white matter surface
using aseg volume ../mri/aseg.presurf to prevent surfaces crossing the midline
not using aparc to prevent surfaces crossing the midline
INFO: assuming MGZ format for volumes.
using brain.finalsurfs as T1 volume...
$Id: mris_make_surfaces.c,v 1.164.2.4 2016/12/13 22:26:32 zkaufman Exp $
$Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading volume /Users/elizavetalavrova/bert/mri/filled.mgz...
reading volume /Users/elizavetalavrova/bert/mri/brain.finalsurfs.mgz...
reading volume /Users/elizavetalavrova/bert/mri/../mri/aseg.presurf.mgz...
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
37202 bright wm thresholded.
4434 bright non-wm voxels segmented.
reading original surface position from /Users/elizavetalavrova/bert/surf/rh.orig...
computing class statistics...
border white:    284022 voxels (1.69%)
border gray      322545 voxels (1.92%)
WM (95.0): 95.8 +- 9.4 [70.0 --> 110.0]
GM (66.0) : 65.1 +- 11.3 [30.0 --> 110.0]
setting MIN_GRAY_AT_WHITE_BORDER to 48.7 (was 70)
setting MAX_BORDER_WHITE to 109.4 (was 105)
setting MIN_BORDER_WHITE to 60.0 (was 85)
setting MAX_CSF to 37.4 (was 40)
setting MAX_GRAY to 90.6 (was 95)
setting MAX_GRAY_AT_CSF_BORDER to 48.7 (was 75)
setting MIN_GRAY_AT_CSF_BORDER to 26.1 (was 40)
repositioning cortical surface to gray/white boundary
smoothing T1 volume with sigma = 2.000
vertex spacing 0.81 +- 0.23 (0.01-->6.96) (max @ vno 58451 --> 62899)
face area 0.27 +- 0.13 (0.00-->6.31)
mean absolute distance = 0.73 +- 0.91
4090 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
using class modes intead of means, discounting robust sigmas....
intensity peaks found at WM=100+-8.7,    GM=60+-9.6
mean inside = 90.7, mean outside = 69.3
smoothing surface for 5 iterations...
inhibiting deformation at non-cortical midline structures...
removing 3 vertex label from ripped group
mean border=73.9, 53 (53) missing vertices, mean dist 0.3 [0.6 (%34.1)->0.8 (%65.9))]
%69 local maxima, %27 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=4, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
complete_dist_mat 0
rms 0
smooth_averages 0
remove_neg 0
ico_order 0
which_surface 0
target_radius 0.000000
nfields 0
scale 0.000000
desired_rms_height 0.000000
momentum 0.000000
nbhd_size 0
max_nbrs 0
niterations 25
nsurfaces 0
SURFACES 3
flags 0 (0)
use curv 0
no sulc 0
no rigid align 0
mris->nsize 2
mris->hemisphere 1
randomSeed 0

smoothing T1 volume with sigma = 1.000
vertex spacing 0.92 +- 0.27 (0.08-->9.76) (max @ vno 58451 --> 62899)
face area 0.27 +- 0.14 (0.00-->7.08)
mean absolute distance = 0.37 +- 0.62
3999 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=4955467.5, rms=12.227
001: dt: 0.5000, sse=2834405.5, rms=8.826 (27.819%)
002: dt: 0.5000, sse=1900515.9, rms=6.773 (23.258%)
003: dt: 0.5000, sse=1441644.6, rms=5.478 (19.124%)
004: dt: 0.5000, sse=1222130.6, rms=4.737 (13.528%)
005: dt: 0.5000, sse=1130468.5, rms=4.386 (7.411%)
006: dt: 0.5000, sse=1090970.1, rms=4.223 (3.709%)
007: dt: 0.5000, sse=1074016.4, rms=4.154 (1.622%)
008: dt: 0.5000, sse=1062823.1, rms=4.102 (1.269%)
rms = 4.08, time step reduction 1 of 3 to 0.250...
009: dt: 0.5000, sse=1058884.4, rms=4.084 (0.422%)
010: dt: 0.2500, sse=819692.8, rms=2.810 (31.208%)
011: dt: 0.2500, sse=762075.1, rms=2.420 (13.857%)
012: dt: 0.2500, sse=752871.9, rms=2.327 (3.871%)
013: dt: 0.2500, sse=740687.7, rms=2.260 (2.866%)
rms = 2.23, time step reduction 2 of 3 to 0.125...
014: dt: 0.2500, sse=737805.8, rms=2.231 (1.273%)
015: dt: 0.1250, sse=716089.7, rms=2.054 (7.960%)
rms = 2.04, time step reduction 3 of 3 to 0.062...
016: dt: 0.1250, sse=714414.0, rms=2.037 (0.827%)
positioning took 2.0 minutes
inhibiting deformation at non-cortical midline structures...
removing 2 vertex label from ripped group
removing 2 vertex label from ripped group
removing 1 vertex label from ripped group
removing 4 vertex label from ripped group
removing 3 vertex label from ripped group
mean border=77.3, 74 (14) missing vertices, mean dist -0.2 [0.4 (%69.5)->0.2 (%30.5))]
%76 local maxima, %19 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=1.0, host=mbp-e, nav=2, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.500
vertex spacing 0.90 +- 0.26 (0.09-->10.22) (max @ vno 58451 --> 62899)
face area 0.35 +- 0.18 (0.00-->9.77)
mean absolute distance = 0.29 +- 0.44
3802 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1464893.1, rms=4.931
017: dt: 0.5000, sse=1131523.5, rms=3.542 (28.169%)
rms = 3.90, time step reduction 1 of 3 to 0.250...
018: dt: 0.2500, sse=948942.8, rms=2.544 (28.177%)
019: dt: 0.2500, sse=887444.4, rms=2.058 (19.093%)
020: dt: 0.2500, sse=860258.1, rms=1.851 (10.062%)
rms = 1.81, time step reduction 2 of 3 to 0.125...
021: dt: 0.2500, sse=856715.9, rms=1.805 (2.489%)
022: dt: 0.1250, sse=840155.0, rms=1.645 (8.846%)
rms = 1.63, time step reduction 3 of 3 to 0.062...
023: dt: 0.1250, sse=838671.8, rms=1.629 (1.012%)
positioning took 1.0 minutes
inhibiting deformation at non-cortical midline structures...
removing 3 vertex label from ripped group
removing 2 vertex label from ripped group
removing 1 vertex label from ripped group
removing 4 vertex label from ripped group
removing 2 vertex label from ripped group
mean border=79.8, 77 (10) missing vertices, mean dist -0.1 [0.3 (%66.3)->0.2 (%33.7))]
%84 local maxima, %11 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=0.5, host=mbp-e, nav=1, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.250
vertex spacing 0.90 +- 0.26 (0.11-->10.40) (max @ vno 58451 --> 62899)
face area 0.34 +- 0.17 (0.00-->9.84)
mean absolute distance = 0.26 +- 0.37
3453 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1097816.5, rms=3.508
024: dt: 0.5000, sse=1085087.1, rms=3.432 (2.169%)
rms = 3.83, time step reduction 1 of 3 to 0.250...
025: dt: 0.2500, sse=894172.5, rms=2.279 (33.594%)
026: dt: 0.2500, sse=841399.8, rms=1.838 (19.373%)
027: dt: 0.2500, sse=824809.0, rms=1.696 (7.733%)
rms = 1.70, time step reduction 2 of 3 to 0.125...
028: dt: 0.1250, sse=815986.8, rms=1.604 (5.425%)
029: dt: 0.1250, sse=804886.1, rms=1.472 (8.187%)
rms = 1.47, time step reduction 3 of 3 to 0.062...
030: dt: 0.1250, sse=804502.8, rms=1.467 (0.337%)
positioning took 1.0 minutes
inhibiting deformation at non-cortical midline structures...
removing 3 vertex label from ripped group
removing 2 vertex label from ripped group
removing 1 vertex label from ripped group
removing 4 vertex label from ripped group
removing 2 vertex label from ripped group
mean border=80.8, 76 (6) missing vertices, mean dist -0.1 [0.3 (%55.5)->0.2 (%44.5))]
%88 local maxima, % 8 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=0.2, host=mbp-e, nav=0, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
writing white matter surface to /Users/elizavetalavrova/bert/surf/rh.white.preaparc...
writing smoothed curvature to rh.curv
000: dt: 0.0000, sse=843009.9, rms=1.963
rms = 2.46, time step reduction 1 of 3 to 0.250...
031: dt: 0.2500, sse=786895.1, rms=1.342 (31.647%)
032: dt: 0.2500, sse=764533.6, rms=1.076 (19.854%)
rms = 1.08, time step reduction 2 of 3 to 0.125...
rms = 1.07, time step reduction 3 of 3 to 0.062...
033: dt: 0.1250, sse=762701.5, rms=1.067 (0.812%)
positioning took 0.6 minutes
generating cortex label...
8 non-cortical segments detected
only using segment with 7607 vertices
erasing segment 1 (vno[0] = 85473)
erasing segment 2 (vno[0] = 98010)
erasing segment 3 (vno[0] = 99983)
erasing segment 4 (vno[0] = 103895)
erasing segment 5 (vno[0] = 109091)
erasing segment 6 (vno[0] = 117140)
erasing segment 7 (vno[0] = 150507)
writing cortex label to /Users/elizavetalavrova/bert/label/rh.cortex.label...
writing curvature file /Users/elizavetalavrova/bert/surf/rh.curv
writing smoothed area to rh.area
writing curvature file /Users/elizavetalavrova/bert/surf/rh.area
vertex spacing 0.90 +- 0.26 (0.01-->10.36) (max @ vno 58451 --> 62899)
face area 0.34 +- 0.17 (0.00-->9.77)
refinement took 6.4 minutes
#--------------------------------------------
#@# Smooth2 lh Wed Mar 27 14:01:25 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_smooth -n 3 -nw -seed 1234 ../surf/lh.white.preaparc ../surf/lh.smoothwm \n
smoothing for 3 iterations
setting seed for random number generator to 1234
smoothing surface tessellation for 3 iterations...
smoothing complete - recomputing first and second fundamental forms...
#--------------------------------------------
#@# Smooth2 rh Wed Mar 27 14:01:35 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_smooth -n 3 -nw -seed 1234 ../surf/rh.white.preaparc ../surf/rh.smoothwm \n
smoothing for 3 iterations
setting seed for random number generator to 1234
smoothing surface tessellation for 3 iterations...
smoothing complete - recomputing first and second fundamental forms...
#--------------------------------------------
#@# Inflation2 lh Wed Mar 27 14:01:43 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_inflate -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_inflate.lh.dat ../surf/lh.smoothwm ../surf/lh.inflated \n
Reading ../surf/lh.smoothwm
avg radius = 50.0 mm, total surface area = 90875 mm^2
writing inflated surface to ../surf/lh.inflated
writing sulcal depths to ../surf/lh.sulc
step 060: RMS=0.024 (target=0.015)   
inflation complete.
inflation took 0.5 minutes
mris_inflate utimesec    29.876077
mris_inflate stimesec    0.321648
mris_inflate ru_maxrss   202502144
mris_inflate ru_ixrss    0
mris_inflate ru_idrss    0
mris_inflate ru_isrss    0
mris_inflate ru_minflt   49456
mris_inflate ru_majflt   404
mris_inflate ru_nswap    0
mris_inflate ru_inblock  0
mris_inflate ru_oublock  0
mris_inflate ru_msgsnd   0
mris_inflate ru_msgrcv   0
mris_inflate ru_nsignals 0
mris_inflate ru_nvcsw    17
mris_inflate ru_nivcsw   36612
#--------------------------------------------
#@# Inflation2 rh Wed Mar 27 14:02:14 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_inflate -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_inflate.rh.dat ../surf/rh.smoothwm ../surf/rh.inflated \n
Reading ../surf/rh.smoothwm
avg radius = 49.4 mm, total surface area = 91073 mm^2
writing inflated surface to ../surf/rh.inflated
writing sulcal depths to ../surf/rh.sulc
step 060: RMS=0.022 (target=0.015)   
inflation complete.
inflation took 0.5 minutes
mris_inflate utimesec    30.465358
mris_inflate stimesec    0.347049
mris_inflate ru_maxrss   206262272
mris_inflate ru_ixrss    0
mris_inflate ru_idrss    0
mris_inflate ru_isrss    0
mris_inflate ru_minflt   50757
mris_inflate ru_majflt   18
mris_inflate ru_nswap    0
mris_inflate ru_inblock  0
mris_inflate ru_oublock  0
mris_inflate ru_msgsnd   0
mris_inflate ru_msgrcv   0
mris_inflate ru_nsignals 0
mris_inflate ru_nvcsw    16
mris_inflate ru_nivcsw   42188
#--------------------------------------------
#@# Curv .H and .K lh Wed Mar 27 14:02:45 CET 2019
/Users/elizavetalavrova/bert/surf
\n mris_curvature -w lh.white.preaparc \n
total integrated curvature = -3.163*4pi (-39.753) --> 4 handles
ICI = 224.1, FI = 2079.9, variation=33872.366
writing Gaussian curvature to /Users/elizavetalavrova/bert/surf/lh.white.preaparc.K...done.
writing mean curvature to /Users/elizavetalavrova/bert/surf/lh.white.preaparc.H...done.
rm -f lh.white.H
ln -s lh.white.preaparc.H lh.white.H
rm -f lh.white.K
ln -s lh.white.preaparc.K lh.white.K
\n mris_curvature -thresh .999 -n -a 5 -w -distances 10 10 lh.inflated \n
normalizing curvature values.
averaging curvature patterns 5 times.
sampling 10 neighbors out to a distance of 10 mm
283 vertices thresholded to be in k1 ~ [-0.74 0.24], k2 ~ [-0.19 0.08]
total integrated curvature = 0.413*4pi (5.190) --> 1 handles
ICI = 1.5, FI = 10.1, variation=170.569
139 vertices thresholded to be in [-0.03 0.03]
writing Gaussian curvature to /Users/elizavetalavrova/bert/surf/lh.inflated.K...thresholding curvature at 99.90% level
curvature mean = 0.000, std = 0.001
122 vertices thresholded to be in [-0.24 0.13]
done.
writing mean curvature to /Users/elizavetalavrova/bert/surf/lh.inflated.H...curvature mean = -0.016, std = 0.022
done.
#--------------------------------------------
#@# Curv .H and .K rh Wed Mar 27 14:04:06 CET 2019
/Users/elizavetalavrova/bert/surf
\n mris_curvature -w rh.white.preaparc \n
total integrated curvature = -13.830*4pi (-173.795) --> 15 handles
ICI = 219.4, FI = 2095.1, variation=34023.412
writing Gaussian curvature to /Users/elizavetalavrova/bert/surf/rh.white.preaparc.K...done.
writing mean curvature to /Users/elizavetalavrova/bert/surf/rh.white.preaparc.H...done.
rm -f rh.white.H
ln -s rh.white.preaparc.H rh.white.H
rm -f rh.white.K
ln -s rh.white.preaparc.K rh.white.K
\n mris_curvature -thresh .999 -n -a 5 -w -distances 10 10 rh.inflated \n
normalizing curvature values.
averaging curvature patterns 5 times.
sampling 10 neighbors out to a distance of 10 mm
236 vertices thresholded to be in k1 ~ [-0.19 1.32], k2 ~ [-0.13 0.05]
total integrated curvature = 0.528*4pi (6.634) --> 0 handles
ICI = 1.5, FI = 9.7, variation=165.016
119 vertices thresholded to be in [-0.01 0.02]
writing Gaussian curvature to /Users/elizavetalavrova/bert/surf/rh.inflated.K...thresholding curvature at 99.90% level
curvature mean = 0.000, std = 0.001
136 vertices thresholded to be in [-0.14 0.15]
done.
writing mean curvature to /Users/elizavetalavrova/bert/surf/rh.inflated.H...curvature mean = -0.015, std = 0.021
done.
\n#-----------------------------------------
#@# Curvature Stats lh Wed Mar 27 14:05:24 CET 2019
/Users/elizavetalavrova/bert/surf
\n mris_curvature_stats -m --writeCurvatureFiles -G -o ../stats/lh.curv.stats -F smoothwm bert lh curv sulc \n
             Toggling save flag on curvature files                       [ ok ]
                 Outputting results using filestem   [ ../stats/lh.curv.stats ]
             Toggling save flag on curvature files                       [ ok ]
                                   Setting surface         [ bert/lh.smoothwm ]
                                Reading surface...                       [ ok ]
                                   Setting texture                     [ curv ]
                                Reading texture...                       [ ok ]
                                   Setting texture                     [ sulc ]
                                Reading texture...Gb_filter = 0
                       [ ok ]
      Calculating Discrete Principal Curvatures...
   Determining geometric order for vertex faces... [####################] [ ok ]
                      Determining KH curvatures... [####################] [ ok ]
                    Determining k1k2 curvatures... [####################] [ ok ]
                                   deltaViolations                      [ 276 ]
Gb_filter = 0

WARN:    S lookup   min:                          -0.674834
WARN:    S explicit min:                          0.000000	vertex = 1550
\n#-----------------------------------------
#@# Curvature Stats rh Wed Mar 27 14:05:30 CET 2019
/Users/elizavetalavrova/bert/surf
\n mris_curvature_stats -m --writeCurvatureFiles -G -o ../stats/rh.curv.stats -F smoothwm bert rh curv sulc \n
             Toggling save flag on curvature files                       [ ok ]
                 Outputting results using filestem   [ ../stats/rh.curv.stats ]
             Toggling save flag on curvature files                       [ ok ]
                                   Setting surface         [ bert/rh.smoothwm ]
                                Reading surface...                       [ ok ]
                                   Setting texture                     [ curv ]
                                Reading texture...                       [ ok ]
                                   Setting texture                     [ sulc ]
                                Reading texture...Gb_filter = 0
                       [ ok ]
      Calculating Discrete Principal Curvatures...
   Determining geometric order for vertex faces... [####################] [ ok ]
                      Determining KH curvatures... [####################] [ ok ]
                    Determining k1k2 curvatures... [####################] [ ok ]
                                   deltaViolations                      [ 300 ]
Gb_filter = 0
#--------------------------------------------
#@# Sphere lh Wed Mar 27 14:05:36 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_sphere -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_sphere.lh.dat -seed 1234 ../surf/lh.inflated ../surf/lh.sphere \n
setting seed for random number genererator to 1234
$Id: mris_sphere.c,v 1.61 2016/01/20 23:42:15 greve Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading original vertex positions...
unfolding cortex into spherical form...
surface projected - minimizing metric distortion...

== Number of threads available to mris_sphere for OpenMP = 1 == 
scaling brain by 0.269...
MRISunfold() max_passes = 1 -------
tol=5.0e-01, sigma=0.0, host=mbp-e, nav=1024, nbrs=2, l_area=1.000, l_dist=1.000
using quadratic fit line minimization
complete_dist_mat 0
rms 0
smooth_averages 0
remove_neg 0
ico_order 0
which_surface 0
target_radius 0.000000
nfields 0
scale 1.000000
desired_rms_height -1.000000
momentum 0.900000
nbhd_size 7
max_nbrs 8
niterations 25
nsurfaces 0
SURFACES 3
flags 0 (0)
use curv 0
no sulc 0
no rigid align 0
mris->nsize 2
mris->hemisphere 0
randomSeed 1234

--------------------
  mrisRemoveNegativeArea()
pass 1: epoch 1 of 3 starting distance error %20.75
pass 1: epoch 2 of 3 starting distance error %20.67
unfolding complete - removing small folds...
starting distance error %20.51
removing remaining folds...
final distance error %20.53
MRISunfold() return, current seed 1234
-01: dt=0.0000, 222 negative triangles
224: dt=0.9900, 222 negative triangles
225: dt=0.9900, 100 negative triangles
226: dt=0.9900, 81 negative triangles
227: dt=0.9900, 67 negative triangles
228: dt=0.9900, 71 negative triangles
229: dt=0.9900, 60 negative triangles
230: dt=0.9900, 64 negative triangles
231: dt=0.9900, 53 negative triangles
232: dt=0.9900, 57 negative triangles
233: dt=0.9900, 54 negative triangles
234: dt=0.9900, 55 negative triangles
235: dt=0.9900, 45 negative triangles
236: dt=0.9900, 48 negative triangles
237: dt=0.9900, 37 negative triangles
238: dt=0.9900, 31 negative triangles
239: dt=0.9900, 31 negative triangles
240: dt=0.9900, 22 negative triangles
241: dt=0.9900, 23 negative triangles
242: dt=0.9900, 17 negative triangles
243: dt=0.9900, 18 negative triangles
244: dt=0.9900, 12 negative triangles
245: dt=0.9900, 11 negative triangles
246: dt=0.9900, 13 negative triangles
247: dt=0.9900, 12 negative triangles
248: dt=0.9900, 7 negative triangles
249: dt=0.9900, 11 negative triangles
250: dt=0.9900, 8 negative triangles
251: dt=0.9900, 5 negative triangles
252: dt=0.9900, 8 negative triangles
253: dt=0.9900, 6 negative triangles
254: dt=0.9900, 5 negative triangles
255: dt=0.9900, 2 negative triangles
256: dt=0.9900, 1 negative triangles
257: dt=0.9900, 1 negative triangles
258: dt=0.9900, 1 negative triangles
259: dt=0.9900, 2 negative triangles
260: dt=0.9900, 2 negative triangles
261: dt=0.9900, 1 negative triangles
writing spherical brain to ../surf/lh.sphere
spherical transformation took 0.72 hours
mris_sphere utimesec    2575.692172
mris_sphere stimesec    9.702709
mris_sphere ru_maxrss   272490496
mris_sphere ru_ixrss    0
mris_sphere ru_idrss    0
mris_sphere ru_isrss    0
mris_sphere ru_minflt   66271
mris_sphere ru_majflt   406
mris_sphere ru_nswap    0
mris_sphere ru_inblock  0
mris_sphere ru_oublock  0
mris_sphere ru_msgsnd   0
mris_sphere ru_msgrcv   0
mris_sphere ru_nsignals 0
mris_sphere ru_nvcsw    10
mris_sphere ru_nivcsw   1898334
FSRUNTIME@ mris_sphere  0.7233 hours 1 threads
#--------------------------------------------
#@# Sphere rh Wed Mar 27 14:49:00 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_sphere -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_sphere.rh.dat -seed 1234 ../surf/rh.inflated ../surf/rh.sphere \n
setting seed for random number genererator to 1234
$Id: mris_sphere.c,v 1.61 2016/01/20 23:42:15 greve Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading original vertex positions...
unfolding cortex into spherical form...
surface projected - minimizing metric distortion...

== Number of threads available to mris_sphere for OpenMP = 1 == 
scaling brain by 0.274...
MRISunfold() max_passes = 1 -------
tol=5.0e-01, sigma=0.0, host=mbp-e, nav=1024, nbrs=2, l_area=1.000, l_dist=1.000
using quadratic fit line minimization
complete_dist_mat 0
rms 0
smooth_averages 0
remove_neg 0
ico_order 0
which_surface 0
target_radius 0.000000
nfields 0
scale 1.000000
desired_rms_height -1.000000
momentum 0.900000
nbhd_size 7
max_nbrs 8
niterations 25
nsurfaces 0
SURFACES 3
flags 0 (0)
use curv 0
no sulc 0
no rigid align 0
mris->nsize 2
mris->hemisphere 1
randomSeed 1234

--------------------
  mrisRemoveNegativeArea()
pass 1: epoch 1 of 3 starting distance error %21.00
pass 1: epoch 2 of 3 starting distance error %20.94
unfolding complete - removing small folds...
starting distance error %20.84
removing remaining folds...
final distance error %20.86
MRISunfold() return, current seed 1234
-01: dt=0.0000, 219 negative triangles
230: dt=0.9900, 219 negative triangles
231: dt=0.9900, 107 negative triangles
232: dt=0.9900, 81 negative triangles
233: dt=0.9900, 70 negative triangles
234: dt=0.9900, 73 negative triangles
235: dt=0.9900, 73 negative triangles
236: dt=0.9900, 65 negative triangles
237: dt=0.9900, 70 negative triangles
238: dt=0.9900, 64 negative triangles
239: dt=0.9900, 57 negative triangles
240: dt=0.9900, 52 negative triangles
241: dt=0.9900, 49 negative triangles
242: dt=0.9900, 45 negative triangles
243: dt=0.9900, 47 negative triangles
244: dt=0.9900, 52 negative triangles
245: dt=0.9900, 40 negative triangles
246: dt=0.9900, 44 negative triangles
247: dt=0.9900, 39 negative triangles
248: dt=0.9900, 32 negative triangles
249: dt=0.9900, 36 negative triangles
250: dt=0.9900, 31 negative triangles
251: dt=0.9900, 35 negative triangles
252: dt=0.9900, 24 negative triangles
253: dt=0.9900, 26 negative triangles
254: dt=0.9900, 24 negative triangles
255: dt=0.9900, 22 negative triangles
256: dt=0.9900, 16 negative triangles
257: dt=0.9900, 22 negative triangles
258: dt=0.9900, 16 negative triangles
259: dt=0.9900, 17 negative triangles
260: dt=0.9900, 16 negative triangles
261: dt=0.9900, 16 negative triangles
262: dt=0.9900, 13 negative triangles
263: dt=0.9900, 12 negative triangles
264: dt=0.9900, 13 negative triangles
265: dt=0.9900, 18 negative triangles
266: dt=0.9900, 15 negative triangles
267: dt=0.9900, 12 negative triangles
268: dt=0.9900, 17 negative triangles
269: dt=0.9900, 17 negative triangles
270: dt=0.9900, 15 negative triangles
271: dt=0.9900, 17 negative triangles
272: dt=0.9900, 17 negative triangles
273: dt=0.9405, 14 negative triangles
274: dt=0.9405, 14 negative triangles
275: dt=0.9405, 16 negative triangles
276: dt=0.9405, 11 negative triangles
277: dt=0.9405, 15 negative triangles
278: dt=0.9405, 12 negative triangles
279: dt=0.9405, 12 negative triangles
280: dt=0.9405, 13 negative triangles
281: dt=0.9405, 10 negative triangles
282: dt=0.9405, 9 negative triangles
283: dt=0.9405, 11 negative triangles
284: dt=0.9405, 9 negative triangles
285: dt=0.9405, 8 negative triangles
286: dt=0.9405, 10 negative triangles
287: dt=0.9405, 9 negative triangles
288: dt=0.9405, 12 negative triangles
289: dt=0.9405, 10 negative triangles
290: dt=0.9405, 8 negative triangles
291: dt=0.9405, 11 negative triangles
292: dt=0.9405, 11 negative triangles
293: dt=0.9405, 7 negative triangles
294: dt=0.9405, 3 negative triangles
295: dt=0.9405, 5 negative triangles
296: dt=0.9405, 3 negative triangles
297: dt=0.9405, 3 negative triangles
298: dt=0.9405, 5 negative triangles
299: dt=0.9405, 2 negative triangles
300: dt=0.9405, 1 negative triangles
301: dt=0.9405, 2 negative triangles
302: dt=0.9405, 2 negative triangles
writing spherical brain to ../surf/rh.sphere
spherical transformation took 0.75 hours
mris_sphere utimesec    2630.260604
mris_sphere stimesec    17.276004
mris_sphere ru_maxrss   273420288
mris_sphere ru_ixrss    0
mris_sphere ru_idrss    0
mris_sphere ru_isrss    0
mris_sphere ru_minflt   66816
mris_sphere ru_majflt   85
mris_sphere ru_nswap    0
mris_sphere ru_inblock  0
mris_sphere ru_oublock  0
mris_sphere ru_msgsnd   0
mris_sphere ru_msgrcv   0
mris_sphere ru_nsignals 0
mris_sphere ru_nvcsw    11
mris_sphere ru_nivcsw   3426315
FSRUNTIME@ mris_sphere  0.7450 hours 1 threads
#--------------------------------------------
#@# Surf Reg lh Wed Mar 27 15:33:42 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_register -curv -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_register.lh.dat ../surf/lh.sphere /Applications/freesurfer/average/lh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif ../surf/lh.sphere.reg \n
using smoothwm curvature for final alignment

cwd /Users/elizavetalavrova/bert/scripts
cmdline mris_register -curv -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_register.lh.dat ../surf/lh.sphere /Applications/freesurfer/average/lh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif ../surf/lh.sphere.reg 

0 inflated.H
1 sulc
2 smoothwm (computed)
$Id: mris_register.c,v 1.63 2016/01/20 23:43:04 greve Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading surface from ../surf/lh.sphere...
reading template parameterization from /Applications/freesurfer/average/lh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif...
MRISregister() -------
max_passes = 4 
min_degrees = 0.500000 
max_degrees = 64.000000 
nangles = 8 
tol=5.0e-01, sigma=0.0, host=mbp-e, nav=1024, nbrs=1, l_extern=10000.000, l_parea=0.200, l_nlarea=1.000, l_corr=1.000, l_dist=5.000
using quadratic fit line minimization
complete_dist_mat 0
rms 0
smooth_averages 0
remove_neg 0
ico_order 0
which_surface 0
target_radius 0.000000
nfields 0
scale 0.000000
desired_rms_height -1.000000
momentum 0.950000
nbhd_size -10
max_nbrs 10
niterations 25
nsurfaces 0
SURFACES 3
flags 16 (10)
use curv 16
no sulc 0
no rigid align 0
mris->nsize 1
mris->hemisphere 0
randomSeed 0

tol=5.0e-01, sigma=0.0, host=mbp-e, nav=1024, nbrs=1, l_extern=10000.000, l_parea=0.200, l_nlarea=1.000, l_corr=1.000, l_dist=5.000
using quadratic fit line minimization
--------------------
1 Reading lh.sulc
curvature mean = 0.000, std = 5.430
curvature mean = 0.030, std = 0.820
curvature mean = 0.019, std = 0.849
Starting MRISrigidBodyAlignGlobal()
  d=64.00 min @ (0.00, -16.00, 0.00) sse = 376552.3, tmin=0.8363
  d=32.00 min @ (8.00, 8.00, 0.00) sse = 274087.8, tmin=1.7070
  d=16.00 min @ (-4.00, 0.00, -4.00) sse = 228703.2, tmin=2.5948
  d=8.00 min @ (2.00, 2.00, 2.00) sse = 221013.6, tmin=3.5203
  d=4.00 min @ (-1.00, 0.00, 0.00) sse = 218340.4, tmin=4.4395
  d=2.00 min @ (0.00, -0.50, 0.00) sse = 218037.3, tmin=5.4037
  d=1.00 min @ (0.00, 0.00, -0.25) sse = 217983.5, tmin=6.3719
  d=0.50 min @ (0.00, 0.12, 0.12) sse = 217923.6, tmin=7.3406
tol=1.0e+00, sigma=0.5, host=mbp-e, nav=1024, nbrs=1, l_extern=10000.000, l_parea=0.200, l_nlarea=1.000, l_corr=0.050, l_spring=0.500, l_dist=5.000
using quadratic fit line minimization
MRISrigidBodyAlignGlobal() done   7.34 min
curvature mean = 0.011, std = 0.830
curvature mean = 0.007, std = 0.941
curvature mean = 0.008, std = 0.841
curvature mean = 0.003, std = 0.976
curvature mean = 0.006, std = 0.841
curvature mean = 0.000, std = 0.990
2 Reading smoothwm
curvature mean = -0.023, std = 0.371
curvature mean = 0.042, std = 0.247
curvature mean = 0.054, std = 0.252
curvature mean = 0.039, std = 0.304
curvature mean = 0.031, std = 0.408
curvature mean = 0.038, std = 0.331
curvature mean = 0.018, std = 0.524
curvature mean = 0.038, std = 0.343
curvature mean = 0.007, std = 0.620
MRISregister() return, current seed 0
-01: dt=0.0000, 174 negative triangles
115: dt=0.9900, 174 negative triangles
expanding nbhd size to 1
116: dt=0.9900, 204 negative triangles
117: dt=0.9900, 170 negative triangles
118: dt=0.9900, 153 negative triangles
119: dt=0.9900, 146 negative triangles
120: dt=0.9900, 136 negative triangles
121: dt=0.9900, 133 negative triangles
122: dt=0.9900, 131 negative triangles
123: dt=0.9900, 132 negative triangles
124: dt=0.9900, 124 negative triangles
125: dt=0.9900, 125 negative triangles
126: dt=0.9900, 134 negative triangles
127: dt=0.9900, 127 negative triangles
128: dt=0.9900, 130 negative triangles
129: dt=0.9900, 130 negative triangles
130: dt=0.9900, 132 negative triangles
131: dt=0.9900, 132 negative triangles
132: dt=0.9900, 135 negative triangles
133: dt=0.9900, 135 negative triangles
134: dt=0.9405, 137 negative triangles
135: dt=0.9405, 134 negative triangles
136: dt=0.9405, 136 negative triangles
137: dt=0.9405, 141 negative triangles
138: dt=0.9405, 142 negative triangles
139: dt=0.9405, 143 negative triangles
140: dt=0.9405, 140 negative triangles
141: dt=0.9405, 144 negative triangles
142: dt=0.9405, 143 negative triangles
143: dt=0.9405, 142 negative triangles
144: dt=0.8935, 143 negative triangles
145: dt=0.8935, 150 negative triangles
146: dt=0.8935, 147 negative triangles
147: dt=0.8935, 146 negative triangles
148: dt=0.8935, 144 negative triangles
149: dt=0.8935, 140 negative triangles
150: dt=0.8935, 143 negative triangles
151: dt=0.8935, 139 negative triangles
152: dt=0.8935, 141 negative triangles
153: dt=0.8935, 134 negative triangles
154: dt=0.8488, 133 negative triangles
155: dt=0.8488, 133 negative triangles
156: dt=0.8488, 136 negative triangles
157: dt=0.8488, 133 negative triangles
158: dt=0.8488, 126 negative triangles
159: dt=0.8488, 126 negative triangles
160: dt=0.8488, 124 negative triangles
161: dt=0.8488, 124 negative triangles
162: dt=0.8488, 121 negative triangles
163: dt=0.8488, 115 negative triangles
164: dt=0.8488, 117 negative triangles
165: dt=0.8488, 121 negative triangles
166: dt=0.8488, 111 negative triangles
167: dt=0.8488, 116 negative triangles
168: dt=0.8488, 115 negative triangles
169: dt=0.8488, 112 negative triangles
170: dt=0.8488, 112 negative triangles
171: dt=0.8488, 111 negative triangles
172: dt=0.8488, 111 negative triangles
173: dt=0.8488, 110 negative triangles
174: dt=0.8488, 112 negative triangles
175: dt=0.8488, 109 negative triangles
176: dt=0.8488, 107 negative triangles
177: dt=0.8488, 104 negative triangles
178: dt=0.8488, 105 negative triangles
179: dt=0.8488, 101 negative triangles
180: dt=0.8488, 101 negative triangles
181: dt=0.8488, 95 negative triangles
182: dt=0.8488, 92 negative triangles
183: dt=0.8488, 89 negative triangles
184: dt=0.8488, 85 negative triangles
185: dt=0.8488, 87 negative triangles
186: dt=0.8488, 82 negative triangles
187: dt=0.8488, 77 negative triangles
188: dt=0.8488, 76 negative triangles
189: dt=0.8488, 72 negative triangles
190: dt=0.8488, 72 negative triangles
191: dt=0.8488, 67 negative triangles
192: dt=0.8488, 63 negative triangles
193: dt=0.8488, 59 negative triangles
194: dt=0.8488, 62 negative triangles
195: dt=0.8488, 57 negative triangles
196: dt=0.8488, 53 negative triangles
197: dt=0.8488, 49 negative triangles
198: dt=0.8488, 49 negative triangles
199: dt=0.8488, 47 negative triangles
200: dt=0.8488, 42 negative triangles
201: dt=0.8488, 41 negative triangles
202: dt=0.8488, 41 negative triangles
203: dt=0.8488, 33 negative triangles
204: dt=0.8488, 32 negative triangles
205: dt=0.8488, 33 negative triangles
206: dt=0.8488, 30 negative triangles
207: dt=0.8488, 31 negative triangles
208: dt=0.8488, 24 negative triangles
209: dt=0.8488, 25 negative triangles
210: dt=0.8488, 23 negative triangles
211: dt=0.8488, 20 negative triangles
212: dt=0.8488, 19 negative triangles
213: dt=0.8488, 17 negative triangles
214: dt=0.8488, 17 negative triangles
215: dt=0.8488, 16 negative triangles
216: dt=0.8488, 15 negative triangles
217: dt=0.8488, 19 negative triangles
218: dt=0.8488, 14 negative triangles
219: dt=0.8488, 13 negative triangles
220: dt=0.8488, 10 negative triangles
221: dt=0.8488, 11 negative triangles
222: dt=0.8488, 9 negative triangles
223: dt=0.8488, 8 negative triangles
224: dt=0.8488, 8 negative triangles
225: dt=0.8488, 9 negative triangles
226: dt=0.8488, 6 negative triangles
227: dt=0.8488, 5 negative triangles
228: dt=0.8488, 7 negative triangles
229: dt=0.8488, 3 negative triangles
230: dt=0.8488, 3 negative triangles
231: dt=0.8488, 2 negative triangles
232: dt=0.8488, 2 negative triangles
233: dt=0.8488, 1 negative triangles
234: dt=0.8488, 1 negative triangles
235: dt=0.8488, 1 negative triangles
writing registered surface to ../surf/lh.sphere.reg...
registration took 0.75 hours
mris_register utimesec    2663.907705
mris_register stimesec    7.846199
mris_register ru_maxrss   252399616
mris_register ru_ixrss    0
mris_register ru_idrss    0
mris_register ru_isrss    0
mris_register ru_minflt   64191
mris_register ru_majflt   472
mris_register ru_nswap    0
mris_register ru_inblock  0
mris_register ru_oublock  0
mris_register ru_msgsnd   0
mris_register ru_msgrcv   0
mris_register ru_nsignals 0
mris_register ru_nvcsw    44
mris_register ru_nivcsw   1275762
FSRUNTIME@ mris_register  0.7468 hours 1 threads
#--------------------------------------------
#@# Surf Reg rh Wed Mar 27 16:18:31 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_register -curv -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_register.rh.dat ../surf/rh.sphere /Applications/freesurfer/average/rh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif ../surf/rh.sphere.reg \n
using smoothwm curvature for final alignment

cwd /Users/elizavetalavrova/bert/scripts
cmdline mris_register -curv -rusage /Users/elizavetalavrova/bert/touch/rusage.mris_register.rh.dat ../surf/rh.sphere /Applications/freesurfer/average/rh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif ../surf/rh.sphere.reg 

0 inflated.H
1 sulc
2 smoothwm (computed)
$Id: mris_register.c,v 1.63 2016/01/20 23:43:04 greve Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading surface from ../surf/rh.sphere...
reading template parameterization from /Applications/freesurfer/average/rh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif...
MRISregister() -------
max_passes = 4 
min_degrees = 0.500000 
max_degrees = 64.000000 
nangles = 8 
tol=5.0e-01, sigma=0.0, host=mbp-e, nav=1024, nbrs=1, l_extern=10000.000, l_parea=0.200, l_nlarea=1.000, l_corr=1.000, l_dist=5.000
using quadratic fit line minimization
complete_dist_mat 0
rms 0
smooth_averages 0
remove_neg 0
ico_order 0
which_surface 0
target_radius 0.000000
nfields 0
scale 0.000000
desired_rms_height -1.000000
momentum 0.950000
nbhd_size -10
max_nbrs 10
niterations 25
nsurfaces 0
SURFACES 3
flags 16 (10)
use curv 16
no sulc 0
no rigid align 0
mris->nsize 1
mris->hemisphere 1
randomSeed 0

tol=5.0e-01, sigma=0.0, host=mbp-e, nav=1024, nbrs=1, l_extern=10000.000, l_parea=0.200, l_nlarea=1.000, l_corr=1.000, l_dist=5.000
using quadratic fit line minimization
--------------------
1 Reading rh.sulc
curvature mean = -0.000, std = 5.445
curvature mean = 0.022, std = 0.807
curvature mean = 0.017, std = 0.847
Starting MRISrigidBodyAlignGlobal()
  d=32.00 min @ (8.00, 0.00, 8.00) sse = 277394.8, tmin=1.6615
  d=16.00 min @ (-4.00, -4.00, -4.00) sse = 227845.9, tmin=2.5026
  d=8.00 min @ (2.00, 0.00, 2.00) sse = 226360.3, tmin=3.3904
  d=4.00 min @ (-1.00, 0.00, -1.00) sse = 222419.1, tmin=4.2973
  d=2.00 min @ (0.50, 0.50, 0.00) sse = 221675.1, tmin=5.1915
  d=1.00 min @ (-0.25, 0.00, 0.00) sse = 221548.7, tmin=6.0711
  d=0.50 min @ (0.12, 0.12, 0.00) sse = 221523.5, tmin=6.9483
tol=1.0e+00, sigma=0.5, host=mbp-e, nav=1024, nbrs=1, l_extern=10000.000, l_parea=0.200, l_nlarea=1.000, l_corr=0.050, l_spring=0.500, l_dist=5.000
using quadratic fit line minimization
MRISrigidBodyAlignGlobal() done   6.95 min
curvature mean = 0.006, std = 0.821
curvature mean = 0.008, std = 0.941
curvature mean = 0.003, std = 0.829
curvature mean = 0.003, std = 0.976
curvature mean = 0.002, std = 0.829
curvature mean = 0.000, std = 0.990
2 Reading smoothwm
curvature mean = -0.020, std = 0.338
curvature mean = 0.038, std = 0.239
curvature mean = 0.055, std = 0.275
curvature mean = 0.037, std = 0.296
curvature mean = 0.031, std = 0.441
curvature mean = 0.036, std = 0.322
curvature mean = 0.018, std = 0.570
curvature mean = 0.036, std = 0.334
curvature mean = 0.007, std = 0.674
MRISregister() return, current seed 0
-01: dt=0.0000, 65 negative triangles
119: dt=0.9900, 65 negative triangles
120: dt=0.9405, 79 negative triangles
expanding nbhd size to 1
121: dt=0.9900, 79 negative triangles
122: dt=0.9900, 67 negative triangles
123: dt=0.9900, 62 negative triangles
124: dt=0.9900, 64 negative triangles
125: dt=0.9900, 60 negative triangles
126: dt=0.9900, 54 negative triangles
127: dt=0.9900, 57 negative triangles
128: dt=0.9900, 54 negative triangles
129: dt=0.9900, 52 negative triangles
130: dt=0.9900, 50 negative triangles
131: dt=0.9900, 51 negative triangles
132: dt=0.9900, 53 negative triangles
133: dt=0.9900, 51 negative triangles
134: dt=0.9900, 44 negative triangles
135: dt=0.9900, 46 negative triangles
136: dt=0.9900, 38 negative triangles
137: dt=0.9900, 36 negative triangles
138: dt=0.9900, 38 negative triangles
139: dt=0.9900, 35 negative triangles
140: dt=0.9900, 30 negative triangles
141: dt=0.9900, 25 negative triangles
142: dt=0.9900, 28 negative triangles
143: dt=0.9900, 23 negative triangles
144: dt=0.9900, 20 negative triangles
145: dt=0.9900, 19 negative triangles
146: dt=0.9900, 23 negative triangles
147: dt=0.9900, 22 negative triangles
148: dt=0.9900, 22 negative triangles
149: dt=0.9900, 21 negative triangles
150: dt=0.9900, 18 negative triangles
151: dt=0.9900, 19 negative triangles
152: dt=0.9900, 18 negative triangles
153: dt=0.9900, 19 negative triangles
154: dt=0.9900, 17 negative triangles
155: dt=0.9900, 17 negative triangles
156: dt=0.9900, 16 negative triangles
157: dt=0.9900, 15 negative triangles
158: dt=0.9900, 15 negative triangles
159: dt=0.9900, 15 negative triangles
160: dt=0.9900, 15 negative triangles
161: dt=0.9900, 14 negative triangles
162: dt=0.9900, 15 negative triangles
163: dt=0.9900, 16 negative triangles
164: dt=0.9900, 17 negative triangles
165: dt=0.9900, 17 negative triangles
166: dt=0.9900, 16 negative triangles
167: dt=0.9900, 13 negative triangles
168: dt=0.9900, 12 negative triangles
169: dt=0.9900, 11 negative triangles
170: dt=0.9900, 10 negative triangles
171: dt=0.9900, 13 negative triangles
172: dt=0.9900, 13 negative triangles
173: dt=0.9900, 10 negative triangles
174: dt=0.9900, 10 negative triangles
175: dt=0.9900, 9 negative triangles
176: dt=0.9900, 12 negative triangles
177: dt=0.9900, 12 negative triangles
178: dt=0.9900, 9 negative triangles
179: dt=0.9900, 8 negative triangles
180: dt=0.9900, 8 negative triangles
181: dt=0.9900, 11 negative triangles
182: dt=0.9900, 11 negative triangles
183: dt=0.9900, 8 negative triangles
184: dt=0.9900, 7 negative triangles
185: dt=0.9900, 9 negative triangles
186: dt=0.9900, 11 negative triangles
187: dt=0.9900, 7 negative triangles
188: dt=0.9900, 8 negative triangles
189: dt=0.9900, 9 negative triangles
190: dt=0.9900, 7 negative triangles
191: dt=0.9900, 6 negative triangles
192: dt=0.9900, 5 negative triangles
193: dt=0.9900, 5 negative triangles
194: dt=0.9900, 5 negative triangles
195: dt=0.9900, 5 negative triangles
196: dt=0.9900, 8 negative triangles
197: dt=0.9900, 6 negative triangles
198: dt=0.9900, 4 negative triangles
199: dt=0.9900, 3 negative triangles
200: dt=0.9900, 3 negative triangles
201: dt=0.9900, 2 negative triangles
writing registered surface to ../surf/rh.sphere.reg...
registration took 0.72 hours
mris_register utimesec    2567.813831
mris_register stimesec    11.726110
mris_register ru_maxrss   266895360
mris_register ru_ixrss    0
mris_register ru_idrss    0
mris_register ru_isrss    0
mris_register ru_minflt   65232
mris_register ru_majflt   88
mris_register ru_nswap    0
mris_register ru_inblock  0
mris_register ru_oublock  0
mris_register ru_msgsnd   0
mris_register ru_msgrcv   0
mris_register ru_nsignals 0
mris_register ru_nvcsw    36
mris_register ru_nivcsw   2048365
FSRUNTIME@ mris_register  0.7220 hours 1 threads
#--------------------------------------------
#@# Jacobian white lh Wed Mar 27 17:01:50 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_jacobian ../surf/lh.white.preaparc ../surf/lh.sphere.reg ../surf/lh.jacobian_white \n
reading surface from ../surf/lh.white.preaparc...
writing curvature file ../surf/lh.jacobian_white
#--------------------------------------------
#@# Jacobian white rh Wed Mar 27 17:01:52 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_jacobian ../surf/rh.white.preaparc ../surf/rh.sphere.reg ../surf/rh.jacobian_white \n
reading surface from ../surf/rh.white.preaparc...
writing curvature file ../surf/rh.jacobian_white
#--------------------------------------------
#@# AvgCurv lh Wed Mar 27 17:01:54 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mrisp_paint -a 5 /Applications/freesurfer/average/lh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif#6 ../surf/lh.sphere.reg ../surf/lh.avg_curv \n
averaging curvature patterns 5 times...
reading surface from ../surf/lh.sphere.reg...
reading template parameterization from /Applications/freesurfer/average/lh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif...
writing curvature file to ../surf/lh.avg_curv...
#--------------------------------------------
#@# AvgCurv rh Wed Mar 27 17:01:56 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mrisp_paint -a 5 /Applications/freesurfer/average/rh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif#6 ../surf/rh.sphere.reg ../surf/rh.avg_curv \n
averaging curvature patterns 5 times...
reading surface from ../surf/rh.sphere.reg...
reading template parameterization from /Applications/freesurfer/average/rh.folding.atlas.acfb40.noaparc.i12.2016-08-02.tif...
writing curvature file to ../surf/rh.avg_curv...
#-----------------------------------------
#@# Cortical Parc lh Wed Mar 27 17:01:58 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_ca_label -l ../label/lh.cortex.label -aseg ../mri/aseg.presurf.mgz -seed 1234 bert lh ../surf/lh.sphere.reg /Applications/freesurfer/average/lh.DKaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs ../label/lh.aparc.annot \n
setting seed for random number generator to 1234
using ../mri/aseg.presurf.mgz aseg volume to correct midline
$Id: mris_ca_label.c,v 1.37 2014/02/04 17:46:42 fischl Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading atlas from /Applications/freesurfer/average/lh.DKaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs...
reading color table from GCSA file....
average std = 0.8   using min determinant for regularization = 0.006
0 singular and 342 ill-conditioned covariance matrices regularized
input 0: MEAN CURVATURE, flags 0, avgs 5, name mean_curvature
labeling surface...
1495 labels changed using aseg
relabeling using gibbs priors...
000:   3318 changed, 151159 examined...
001:    771 changed, 14053 examined...
002:    201 changed, 4253 examined...
003:     82 changed, 1213 examined...
004:     31 changed, 487 examined...
005:      9 changed, 169 examined...
006:      2 changed, 60 examined...
007:      2 changed, 15 examined...
008:      0 changed, 12 examined...
209 labels changed using aseg
000: 133 total segments, 87 labels (314 vertices) changed
001: 48 total segments, 2 labels (3 vertices) changed
002: 45 total segments, 4 labels (12 vertices) changed
003: 41 total segments, 0 labels (0 vertices) changed
10 filter iterations complete (10 requested, 6 changed)
rationalizing unknown annotations with cortex label
relabeling unknown label...
relabeling corpuscallosum label...
1443 vertices marked for relabeling...
1443 labels changed in reclassification.
writing output to ../label/lh.aparc.annot...
classification took 0 minutes and 17 seconds.
#-----------------------------------------
#@# Cortical Parc rh Wed Mar 27 17:02:15 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_ca_label -l ../label/rh.cortex.label -aseg ../mri/aseg.presurf.mgz -seed 1234 bert rh ../surf/rh.sphere.reg /Applications/freesurfer/average/rh.DKaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs ../label/rh.aparc.annot \n
setting seed for random number generator to 1234
using ../mri/aseg.presurf.mgz aseg volume to correct midline
$Id: mris_ca_label.c,v 1.37 2014/02/04 17:46:42 fischl Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading atlas from /Applications/freesurfer/average/rh.DKaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs...
reading color table from GCSA file....
average std = 0.7   using min determinant for regularization = 0.004
0 singular and 309 ill-conditioned covariance matrices regularized
input 0: MEAN CURVATURE, flags 0, avgs 5, name mean_curvature
labeling surface...
1346 labels changed using aseg
relabeling using gibbs priors...
000:   3040 changed, 150852 examined...
001:    702 changed, 13091 examined...
002:    162 changed, 3942 examined...
003:     58 changed, 1015 examined...
004:     21 changed, 348 examined...
005:      7 changed, 127 examined...
006:      2 changed, 45 examined...
007:      0 changed, 15 examined...
137 labels changed using aseg
000: 100 total segments, 61 labels (266 vertices) changed
001: 40 total segments, 1 labels (1 vertices) changed
002: 39 total segments, 0 labels (0 vertices) changed
10 filter iterations complete (10 requested, 9 changed)
rationalizing unknown annotations with cortex label
relabeling unknown label...
relabeling corpuscallosum label...
1152 vertices marked for relabeling...
1152 labels changed in reclassification.
writing output to ../label/rh.aparc.annot...
classification took 0 minutes and 16 seconds.
#--------------------------------------------
#@# Make Pial Surf lh Wed Mar 27 17:02:31 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_make_surfaces -orig_white white.preaparc -orig_pial white.preaparc -aseg ../mri/aseg.presurf -mgz -T1 brain.finalsurfs bert lh \n
using white.preaparc starting white location...
using white.preaparc starting pial locations...
using aseg volume ../mri/aseg.presurf to prevent surfaces crossing the midline
INFO: assuming MGZ format for volumes.
using brain.finalsurfs as T1 volume...
$Id: mris_make_surfaces.c,v 1.164.2.4 2016/12/13 22:26:32 zkaufman Exp $
$Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading volume /Users/elizavetalavrova/bert/mri/filled.mgz...
reading volume /Users/elizavetalavrova/bert/mri/brain.finalsurfs.mgz...
reading volume /Users/elizavetalavrova/bert/mri/../mri/aseg.presurf.mgz...
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
37202 bright wm thresholded.
4434 bright non-wm voxels segmented.
reading original surface position from /Users/elizavetalavrova/bert/surf/lh.orig...
computing class statistics...
border white:    284022 voxels (1.69%)
border gray      322545 voxels (1.92%)
WM (95.0): 95.8 +- 9.4 [70.0 --> 110.0]
GM (66.0) : 65.1 +- 11.3 [30.0 --> 110.0]
setting MIN_GRAY_AT_WHITE_BORDER to 49.7 (was 70)
setting MAX_BORDER_WHITE to 109.4 (was 105)
setting MIN_BORDER_WHITE to 61.0 (was 85)
setting MAX_CSF to 38.4 (was 40)
setting MAX_GRAY to 90.6 (was 95)
setting MAX_GRAY_AT_CSF_BORDER to 49.7 (was 75)
setting MIN_GRAY_AT_CSF_BORDER to 27.1 (was 40)
using class modes intead of means, discounting robust sigmas....
intensity peaks found at WM=100+-7.8,    GM=61+-8.7
mean inside = 90.7, mean outside = 69.0
smoothing surface for 5 iterations...
reading initial white vertex positions from white.preaparc...
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
repositioning cortical surface to gray/white boundary
smoothing T1 volume with sigma = 2.000
vertex spacing 0.89 +- 0.25 (0.05-->5.09) (max @ vno 107107 --> 107108)
face area 0.33 +- 0.16 (0.00-->3.03)
mean absolute distance = 0.63 +- 0.88
2862 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
inhibiting deformation at non-cortical midline structures...
deleting segment 0 with 10 points - only 0.00% unknown
deleting segment 1 with 10 points - only 0.00% unknown
removing 2 vertex label from ripped group
deleting segment 2 with 2 points - only 0.00% unknown
deleting segment 3 with 8 points - only 0.00% unknown
removing 4 vertex label from ripped group
deleting segment 7 with 5 points - only 0.00% unknown
deleting segment 8 with 183 points - only 0.00% unknown
removing 4 vertex label from ripped group
deleting segment 9 with 4 points - only 0.00% unknown
deleting segment 10 with 5 points - only 0.00% unknown
removing 1 vertex label from ripped group
deleting segment 11 with 1 points - only 0.00% unknown
deleting segment 12 with 30 points - only 0.00% unknown
removing 3 vertex label from ripped group
deleting segment 13 with 3 points - only 0.00% unknown
mean border=74.0, 82 (82) missing vertices, mean dist 0.3 [1.2 (%12.5)->0.5 (%87.5))]
%61 local maxima, %35 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=4, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
complete_dist_mat 0
rms 0
smooth_averages 0
remove_neg 0
ico_order 0
which_surface 0
target_radius 0.000000
nfields 0
scale 0.000000
desired_rms_height 0.000000
momentum 0.000000
nbhd_size 0
max_nbrs 0
niterations 25
nsurfaces 0
SURFACES 3
flags 0 (0)
use curv 0
no sulc 0
no rigid align 0
mris->nsize 2
mris->hemisphere 0
randomSeed 0

smoothing T1 volume with sigma = 1.000
vertex spacing 0.92 +- 0.27 (0.07-->4.55) (max @ vno 107108 --> 107107)
face area 0.33 +- 0.16 (0.00-->3.14)
mean absolute distance = 0.37 +- 0.65
4079 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=2963677.0, rms=8.802
001: dt: 0.5000, sse=1541919.0, rms=5.316 (39.601%)
002: dt: 0.5000, sse=1226903.5, rms=4.198 (21.037%)
003: dt: 0.5000, sse=1210745.5, rms=4.126 (1.713%)
004: dt: 0.5000, sse=1141600.4, rms=3.854 (6.592%)
rms = 4.05, time step reduction 1 of 3 to 0.250...
005: dt: 0.2500, sse=935727.3, rms=2.722 (29.366%)
006: dt: 0.2500, sse=875531.1, rms=2.278 (16.325%)
007: dt: 0.2500, sse=855005.9, rms=2.107 (7.496%)
rms = 2.07, time step reduction 2 of 3 to 0.125...
008: dt: 0.2500, sse=851283.2, rms=2.073 (1.611%)
009: dt: 0.1250, sse=836290.2, rms=1.934 (6.702%)
rms = 1.92, time step reduction 3 of 3 to 0.062...
010: dt: 0.1250, sse=834472.1, rms=1.918 (0.849%)
positioning took 1.3 minutes
inhibiting deformation at non-cortical midline structures...
deleting segment 0 with 11 points - only 0.00% unknown
deleting segment 1 with 10 points - only 0.00% unknown
deleting segment 2 with 8 points - only 0.00% unknown
removing 1 vertex label from ripped group
deleting segment 5 with 110 points - only 0.00% unknown
deleting segment 6 with 5 points - only 0.00% unknown
removing 3 vertex label from ripped group
deleting segment 7 with 3 points - only 0.00% unknown
removing 3 vertex label from ripped group
deleting segment 8 with 3 points - only 0.00% unknown
mean border=77.6, 89 (24) missing vertices, mean dist -0.2 [0.4 (%70.5)->0.2 (%29.5))]
%72 local maxima, %23 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=1.0, host=mbp-e, nav=2, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.500
vertex spacing 0.90 +- 0.26 (0.08-->5.00) (max @ vno 107108 --> 107107)
face area 0.35 +- 0.17 (0.00-->3.72)
mean absolute distance = 0.29 +- 0.44
3976 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1449317.9, rms=4.855
011: dt: 0.5000, sse=1141617.1, rms=3.505 (27.809%)
rms = 3.85, time step reduction 1 of 3 to 0.250...
012: dt: 0.2500, sse=947620.6, rms=2.483 (29.143%)
013: dt: 0.2500, sse=883702.4, rms=1.990 (19.867%)
014: dt: 0.2500, sse=859596.2, rms=1.774 (10.877%)
rms = 1.74, time step reduction 2 of 3 to 0.125...
015: dt: 0.2500, sse=855711.6, rms=1.738 (1.983%)
016: dt: 0.1250, sse=840521.1, rms=1.575 (9.373%)
rms = 1.56, time step reduction 3 of 3 to 0.062...
017: dt: 0.1250, sse=840396.1, rms=1.562 (0.828%)
positioning took 0.9 minutes
inhibiting deformation at non-cortical midline structures...
deleting segment 0 with 11 points - only 0.00% unknown
deleting segment 1 with 10 points - only 0.00% unknown
deleting segment 2 with 9 points - only 0.00% unknown
deleting segment 3 with 99 points - only 0.00% unknown
deleting segment 4 with 5 points - only 0.00% unknown
deleting segment 5 with 10 points - only 0.00% unknown
removing 3 vertex label from ripped group
deleting segment 6 with 3 points - only 0.00% unknown
mean border=80.2, 84 (18) missing vertices, mean dist -0.2 [0.3 (%66.7)->0.2 (%33.3))]
%82 local maxima, %13 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=0.5, host=mbp-e, nav=1, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.250
vertex spacing 0.90 +- 0.26 (0.11-->5.33) (max @ vno 107108 --> 107107)
face area 0.34 +- 0.17 (0.00-->3.52)
mean absolute distance = 0.25 +- 0.37
3470 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1107737.8, rms=3.542
018: dt: 0.5000, sse=1093914.9, rms=3.448 (2.658%)
rms = 3.80, time step reduction 1 of 3 to 0.250...
019: dt: 0.2500, sse=896945.7, rms=2.273 (34.067%)
020: dt: 0.2500, sse=840136.6, rms=1.804 (20.626%)
021: dt: 0.2500, sse=825000.2, rms=1.660 (8.015%)
rms = 1.66, time step reduction 2 of 3 to 0.125...
022: dt: 0.2500, sse=824019.3, rms=1.659 (0.065%)
023: dt: 0.1250, sse=805899.1, rms=1.444 (12.970%)
rms = 1.43, time step reduction 3 of 3 to 0.062...
024: dt: 0.1250, sse=803591.6, rms=1.427 (1.161%)
positioning took 0.9 minutes
inhibiting deformation at non-cortical midline structures...
deleting segment 0 with 15 points - only 0.00% unknown
deleting segment 1 with 10 points - only 0.00% unknown
deleting segment 2 with 9 points - only 0.00% unknown
removing 2 vertex label from ripped group
deleting segment 3 with 2 points - only 0.00% unknown
deleting segment 4 with 145 points - only 0.00% unknown
removing 2 vertex label from ripped group
deleting segment 5 with 2 points - only 0.00% unknown
deleting segment 6 with 5 points - only 0.00% unknown
deleting segment 7 with 23 points - only 0.00% unknown
removing 4 vertex label from ripped group
deleting segment 8 with 4 points - only 0.00% unknown
mean border=81.2, 96 (13) missing vertices, mean dist -0.1 [0.3 (%55.3)->0.2 (%44.7))]
%86 local maxima, % 9 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=0.2, host=mbp-e, nav=0, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
writing white matter surface to /Users/elizavetalavrova/bert/surf/lh.white...
writing smoothed curvature to lh.curv
000: dt: 0.0000, sse=844247.5, rms=1.956
rms = 2.46, time step reduction 1 of 3 to 0.250...
025: dt: 0.2500, sse=783787.4, rms=1.316 (32.733%)
026: dt: 0.2500, sse=778920.4, rms=1.047 (20.414%)
rms = 1.06, time step reduction 2 of 3 to 0.125...
rms = 1.04, time step reduction 3 of 3 to 0.062...
027: dt: 0.1250, sse=776069.4, rms=1.037 (0.925%)
positioning took 0.5 minutes
generating cortex label...
4 non-cortical segments detected
only using segment with 7648 vertices
erasing segment 1 (vno[0] = 103035)
erasing segment 2 (vno[0] = 104149)
erasing segment 3 (vno[0] = 106061)
writing cortex label to /Users/elizavetalavrova/bert/label/lh.cortex.label...
writing curvature file /Users/elizavetalavrova/bert/surf/lh.curv
writing smoothed area to lh.area
writing curvature file /Users/elizavetalavrova/bert/surf/lh.area
vertex spacing 0.89 +- 0.26 (0.05-->5.44) (max @ vno 107107 --> 107108)
face area 0.34 +- 0.17 (0.00-->3.42)
repositioning cortical surface to gray/csf boundary.
smoothing T1 volume with sigma = 2.000
averaging target values for 5 iterations...
inhibiting deformation at non-cortical midline structures...
removing 4 vertex label from ripped group
smoothing surface for 5 iterations...
reading initial pial vertex positions from white.preaparc...
mean border=47.4, 90 (90) missing vertices, mean dist 1.8 [0.0 (%0.0)->2.6 (%100.0))]
%13 local maxima, %54 large gradients and %29 min vals, 399 gradients ignored
perforing initial smooth deformation to move away from white surface
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=16, nbrs=2, l_surf_repulse=1.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.05
000: dt: 0.0000, sse=34965072.0, rms=34.389
001: dt: 0.0500, sse=30673212.0, rms=32.161 (6.479%)
002: dt: 0.0500, sse=27572070.0, rms=30.450 (5.321%)
003: dt: 0.0500, sse=25200232.0, rms=29.073 (4.522%)
004: dt: 0.0500, sse=23293554.0, rms=27.917 (3.977%)
005: dt: 0.0500, sse=21701294.0, rms=26.913 (3.595%)
006: dt: 0.0500, sse=20335892.0, rms=26.022 (3.313%)
007: dt: 0.0500, sse=19141982.0, rms=25.216 (3.095%)
008: dt: 0.0500, sse=18079488.0, rms=24.477 (2.931%)
009: dt: 0.0500, sse=17122854.0, rms=23.792 (2.799%)
010: dt: 0.0500, sse=16253493.0, rms=23.152 (2.691%)
positioning took 1.1 minutes
mean border=47.2, 80 (42) missing vertices, mean dist 1.5 [0.4 (%0.0)->2.1 (%100.0))]
%14 local maxima, %54 large gradients and %28 min vals, 341 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=16, nbrs=2, l_surf_repulse=1.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.05
000: dt: 0.0000, sse=16939190.0, rms=23.665
011: dt: 0.0500, sse=16139010.0, rms=23.073 (2.501%)
012: dt: 0.0500, sse=15402986.0, rms=22.515 (2.419%)
013: dt: 0.0500, sse=14723077.0, rms=21.987 (2.346%)
014: dt: 0.0500, sse=14093606.0, rms=21.486 (2.277%)
015: dt: 0.0500, sse=13508942.0, rms=21.010 (2.214%)
016: dt: 0.0500, sse=12965271.0, rms=20.558 (2.153%)
017: dt: 0.0500, sse=12457718.0, rms=20.126 (2.099%)
018: dt: 0.0500, sse=11983964.0, rms=19.715 (2.044%)
019: dt: 0.0500, sse=11540487.0, rms=19.322 (1.994%)
020: dt: 0.0500, sse=11124711.0, rms=18.946 (1.946%)
positioning took 1.2 minutes
mean border=47.1, 105 (35) missing vertices, mean dist 1.2 [0.1 (%0.9)->1.7 (%99.1))]
%14 local maxima, %54 large gradients and %27 min vals, 346 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=16, nbrs=2, l_surf_repulse=1.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.05
000: dt: 0.0000, sse=11208179.0, rms=19.030
021: dt: 0.0500, sse=10809803.0, rms=18.664 (1.922%)
022: dt: 0.0500, sse=10436186.0, rms=18.314 (1.874%)
023: dt: 0.0500, sse=10082989.0, rms=17.977 (1.840%)
024: dt: 0.0500, sse=9750589.0, rms=17.654 (1.797%)
025: dt: 0.0500, sse=9436636.0, rms=17.344 (1.760%)
026: dt: 0.0500, sse=9140009.0, rms=17.045 (1.723%)
027: dt: 0.0500, sse=8856476.0, rms=16.754 (1.706%)
028: dt: 0.0500, sse=8584320.0, rms=16.470 (1.695%)
029: dt: 0.0500, sse=8323195.0, rms=16.193 (1.683%)
030: dt: 0.0500, sse=8071599.0, rms=15.921 (1.678%)
positioning took 1.1 minutes
mean border=47.0, 133 (28) missing vertices, mean dist 1.0 [0.1 (%7.6)->1.5 (%92.4))]
%14 local maxima, %54 large gradients and %27 min vals, 317 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=16, nbrs=2, l_surf_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 1.000
averaging target values for 5 iterations...
000: dt: 0.0000, sse=8147782.5, rms=16.004
031: dt: 0.5000, sse=6339877.0, rms=13.911 (13.078%)
032: dt: 0.5000, sse=5039751.5, rms=12.179 (12.456%)
033: dt: 0.5000, sse=4049526.2, rms=10.676 (12.340%)
034: dt: 0.5000, sse=3325289.5, rms=9.416 (11.800%)
035: dt: 0.5000, sse=2797941.2, rms=8.384 (10.960%)
036: dt: 0.5000, sse=2411182.8, rms=7.532 (10.167%)
037: dt: 0.5000, sse=2128667.0, rms=6.848 (9.080%)
038: dt: 0.5000, sse=1934758.9, rms=6.330 (7.557%)
039: dt: 0.5000, sse=1807774.1, rms=5.971 (5.674%)
040: dt: 0.5000, sse=1728964.2, rms=5.732 (4.006%)
041: dt: 0.5000, sse=1683826.9, rms=5.593 (2.423%)
042: dt: 0.5000, sse=1653904.4, rms=5.496 (1.740%)
043: dt: 0.5000, sse=1633157.1, rms=5.430 (1.195%)
044: dt: 0.5000, sse=1616034.6, rms=5.371 (1.084%)
045: dt: 0.5000, sse=1599769.0, rms=5.320 (0.950%)
rms = 5.29, time step reduction 1 of 3 to 0.250...
046: dt: 0.5000, sse=1592891.1, rms=5.294 (0.499%)
047: dt: 0.2500, sse=1433510.9, rms=4.689 (11.429%)
048: dt: 0.2500, sse=1387077.9, rms=4.512 (3.757%)
rms = 4.51, time step reduction 2 of 3 to 0.125...
049: dt: 0.1250, sse=1372758.6, rms=4.453 (1.310%)
050: dt: 0.1250, sse=1354652.4, rms=4.376 (1.735%)
rms = 4.37, time step reduction 3 of 3 to 0.062...
051: dt: 0.1250, sse=1353848.0, rms=4.370 (0.131%)
positioning took 2.7 minutes
mean border=45.8, 2077 (14) missing vertices, mean dist 0.1 [0.2 (%49.3)->0.5 (%50.7))]
%27 local maxima, %43 large gradients and %24 min vals, 144 gradients ignored
tol=1.0e-04, sigma=1.0, host=mbp-e, nav=8, nbrs=2, l_surf_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.500
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1660711.5, rms=4.788
052: dt: 0.5000, sse=1615686.4, rms=4.635 (3.187%)
rms = 4.60, time step reduction 1 of 3 to 0.250...
053: dt: 0.5000, sse=1594292.4, rms=4.598 (0.797%)
054: dt: 0.2500, sse=1416981.6, rms=3.792 (17.545%)
055: dt: 0.2500, sse=1366988.1, rms=3.560 (6.118%)
rms = 3.55, time step reduction 2 of 3 to 0.125...
056: dt: 0.2500, sse=1367122.4, rms=3.555 (0.141%)
057: dt: 0.1250, sse=1321344.8, rms=3.313 (6.799%)
rms = 3.28, time step reduction 3 of 3 to 0.062...
058: dt: 0.1250, sse=1314651.5, rms=3.279 (1.023%)
positioning took 1.0 minutes
mean border=44.8, 2208 (12) missing vertices, mean dist 0.1 [0.2 (%52.2)->0.4 (%47.8))]
%42 local maxima, %29 large gradients and %23 min vals, 157 gradients ignored
tol=1.0e-04, sigma=0.5, host=mbp-e, nav=4, nbrs=2, l_surf_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.250
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1388723.4, rms=3.630
rms = 4.18, time step reduction 1 of 3 to 0.250...
059: dt: 0.2500, sse=1338698.0, rms=3.376 (7.016%)
rms = 3.33, time step reduction 2 of 3 to 0.125...
060: dt: 0.2500, sse=1328271.2, rms=3.326 (1.473%)
061: dt: 0.1250, sse=1312211.0, rms=3.237 (2.677%)
rms = 3.21, time step reduction 3 of 3 to 0.062...
062: dt: 0.1250, sse=1306947.4, rms=3.212 (0.763%)
positioning took 0.7 minutes
mean border=44.1, 3582 (10) missing vertices, mean dist 0.1 [0.2 (%52.3)->0.3 (%47.7))]
%47 local maxima, %24 large gradients and %23 min vals, 176 gradients ignored
tol=1.0e-04, sigma=0.2, host=mbp-e, nav=2, nbrs=2, l_surf_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
writing pial surface to /Users/elizavetalavrova/bert/surf/lh.pial...
writing smoothed curvature to lh.curv.pial
000: dt: 0.0000, sse=1337433.1, rms=3.368
rms = 3.87, time step reduction 1 of 3 to 0.250...
063: dt: 0.2500, sse=1310457.4, rms=3.223 (4.322%)
064: dt: 0.2500, sse=1296137.8, rms=3.162 (1.894%)
rms = 3.17, time step reduction 2 of 3 to 0.125...
rms = 3.13, time step reduction 3 of 3 to 0.062...
065: dt: 0.1250, sse=1290150.2, rms=3.126 (1.129%)
positioning took 0.7 minutes
writing curvature file /Users/elizavetalavrova/bert/surf/lh.curv.pial
writing smoothed area to lh.area.pial
writing curvature file /Users/elizavetalavrova/bert/surf/lh.area.pial
vertex spacing 1.01 +- 0.44 (0.06-->7.13) (max @ vno 104217 --> 103163)
face area 0.40 +- 0.31 (0.00-->5.31)
measuring cortical thickness...
writing cortical thickness estimate to 'thickness' file.
0 of 151159 vertices processed
25000 of 151159 vertices processed
50000 of 151159 vertices processed
75000 of 151159 vertices processed
100000 of 151159 vertices processed
125000 of 151159 vertices processed
150000 of 151159 vertices processed
0 of 151159 vertices processed
25000 of 151159 vertices processed
50000 of 151159 vertices processed
75000 of 151159 vertices processed
100000 of 151159 vertices processed
125000 of 151159 vertices processed
150000 of 151159 vertices processed
thickness calculation complete, 146:686 truncations.
32943 vertices at 0 distance
111882 vertices at 1 distance
95745 vertices at 2 distance
35556 vertices at 3 distance
9787 vertices at 4 distance
2516 vertices at 5 distance
681 vertices at 6 distance
217 vertices at 7 distance
94 vertices at 8 distance
68 vertices at 9 distance
45 vertices at 10 distance
26 vertices at 11 distance
17 vertices at 12 distance
23 vertices at 13 distance
22 vertices at 14 distance
20 vertices at 15 distance
19 vertices at 16 distance
12 vertices at 17 distance
3 vertices at 18 distance
4 vertices at 19 distance
2 vertices at 20 distance
writing curvature file /Users/elizavetalavrova/bert/surf/lh.thickness
positioning took 15.7 minutes
#--------------------------------------------
#@# Make Pial Surf rh Wed Mar 27 17:18:15 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_make_surfaces -orig_white white.preaparc -orig_pial white.preaparc -aseg ../mri/aseg.presurf -mgz -T1 brain.finalsurfs bert rh \n
using white.preaparc starting white location...
using white.preaparc starting pial locations...
using aseg volume ../mri/aseg.presurf to prevent surfaces crossing the midline
INFO: assuming MGZ format for volumes.
using brain.finalsurfs as T1 volume...
$Id: mris_make_surfaces.c,v 1.164.2.4 2016/12/13 22:26:32 zkaufman Exp $
$Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading volume /Users/elizavetalavrova/bert/mri/filled.mgz...
reading volume /Users/elizavetalavrova/bert/mri/brain.finalsurfs.mgz...
reading volume /Users/elizavetalavrova/bert/mri/../mri/aseg.presurf.mgz...
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
37202 bright wm thresholded.
4434 bright non-wm voxels segmented.
reading original surface position from /Users/elizavetalavrova/bert/surf/rh.orig...
computing class statistics...
border white:    284022 voxels (1.69%)
border gray      322545 voxels (1.92%)
WM (95.0): 95.8 +- 9.4 [70.0 --> 110.0]
GM (66.0) : 65.1 +- 11.3 [30.0 --> 110.0]
setting MIN_GRAY_AT_WHITE_BORDER to 48.7 (was 70)
setting MAX_BORDER_WHITE to 109.4 (was 105)
setting MIN_BORDER_WHITE to 60.0 (was 85)
setting MAX_CSF to 37.4 (was 40)
setting MAX_GRAY to 90.6 (was 95)
setting MAX_GRAY_AT_CSF_BORDER to 48.7 (was 75)
setting MIN_GRAY_AT_CSF_BORDER to 26.1 (was 40)
using class modes intead of means, discounting robust sigmas....
intensity peaks found at WM=100+-8.7,    GM=60+-9.6
mean inside = 90.7, mean outside = 69.3
smoothing surface for 5 iterations...
reading initial white vertex positions from white.preaparc...
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
repositioning cortical surface to gray/white boundary
smoothing T1 volume with sigma = 2.000
vertex spacing 0.90 +- 0.26 (0.01-->10.36) (max @ vno 58451 --> 62899)
face area 0.34 +- 0.17 (0.00-->9.75)
mean absolute distance = 0.61 +- 0.85
2770 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
inhibiting deformation at non-cortical midline structures...
deleting segment 0 with 26 points - only 0.00% unknown
deleting segment 1 with 11 points - only 0.00% unknown
removing 3 vertex label from ripped group
deleting segment 3 with 3 points - only 0.00% unknown
deleting segment 4 with 5 points - only 0.00% unknown
deleting segment 5 with 108 points - only 0.00% unknown
deleting segment 6 with 6 points - only 0.00% unknown
deleting segment 7 with 17 points - only 0.00% unknown
removing 2 vertex label from ripped group
deleting segment 8 with 2 points - only 0.00% unknown
deleting segment 9 with 94 points - only 0.00% unknown
deleting segment 11 with 93 points - only 0.00% unknown
deleting segment 12 with 9 points - only 0.00% unknown
mean border=73.6, 69 (69) missing vertices, mean dist 0.3 [1.0 (%13.9)->0.5 (%86.1))]
%66 local maxima, %30 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=4, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
complete_dist_mat 0
rms 0
smooth_averages 0
remove_neg 0
ico_order 0
which_surface 0
target_radius 0.000000
nfields 0
scale 0.000000
desired_rms_height 0.000000
momentum 0.000000
nbhd_size 0
max_nbrs 0
niterations 25
nsurfaces 0
SURFACES 3
flags 0 (0)
use curv 0
no sulc 0
no rigid align 0
mris->nsize 2
mris->hemisphere 1
randomSeed 0

smoothing T1 volume with sigma = 1.000
vertex spacing 0.92 +- 0.27 (0.08-->10.86) (max @ vno 58451 --> 62899)
face area 0.34 +- 0.17 (0.00-->9.64)
mean absolute distance = 0.37 +- 0.63
3992 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=2980830.8, rms=8.821
001: dt: 0.5000, sse=1559412.9, rms=5.334 (39.538%)
002: dt: 0.5000, sse=1242736.4, rms=4.213 (21.013%)
003: dt: 0.5000, sse=1202656.0, rms=4.088 (2.956%)
004: dt: 0.5000, sse=1148587.4, rms=3.856 (5.695%)
rms = 4.01, time step reduction 1 of 3 to 0.250...
005: dt: 0.2500, sse=943563.5, rms=2.737 (29.023%)
006: dt: 0.2500, sse=885648.8, rms=2.281 (16.651%)
007: dt: 0.2500, sse=860994.9, rms=2.116 (7.213%)
rms = 2.08, time step reduction 2 of 3 to 0.125...
008: dt: 0.2500, sse=863358.6, rms=2.075 (1.939%)
009: dt: 0.1250, sse=843403.0, rms=1.941 (6.469%)
rms = 1.93, time step reduction 3 of 3 to 0.062...
010: dt: 0.1250, sse=840436.2, rms=1.925 (0.811%)
positioning took 1.3 minutes
inhibiting deformation at non-cortical midline structures...
deleting segment 0 with 18 points - only 0.00% unknown
deleting segment 1 with 9 points - only 0.00% unknown
removing 3 vertex label from ripped group
deleting segment 2 with 3 points - only 0.00% unknown
deleting segment 3 with 48 points - only 0.00% unknown
deleting segment 4 with 10 points - only 0.00% unknown
removing 1 vertex label from ripped group
deleting segment 5 with 1 points - only 0.00% unknown
deleting segment 6 with 11 points - only 0.00% unknown
deleting segment 7 with 76 points - only 0.00% unknown
deleting segment 8 with 50 points - only 0.00% unknown
removing 3 vertex label from ripped group
deleting segment 9 with 3 points - only 0.00% unknown
deleting segment 10 with 11 points - only 0.00% unknown
mean border=77.1, 72 (23) missing vertices, mean dist -0.2 [0.4 (%70.3)->0.2 (%29.7))]
%76 local maxima, %20 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=1.0, host=mbp-e, nav=2, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.500
vertex spacing 0.90 +- 0.26 (0.07-->10.99) (max @ vno 58451 --> 62899)
face area 0.36 +- 0.18 (0.00-->10.70)
mean absolute distance = 0.29 +- 0.44
3831 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1460417.2, rms=4.866
011: dt: 0.5000, sse=1128566.6, rms=3.459 (28.919%)
rms = 3.81, time step reduction 1 of 3 to 0.250...
012: dt: 0.2500, sse=951508.9, rms=2.465 (28.730%)
013: dt: 0.2500, sse=889978.1, rms=1.977 (19.816%)
014: dt: 0.2500, sse=869087.1, rms=1.778 (10.051%)
rms = 1.74, time step reduction 2 of 3 to 0.125...
015: dt: 0.2500, sse=866229.8, rms=1.743 (1.969%)
016: dt: 0.1250, sse=848987.2, rms=1.588 (8.885%)
rms = 1.57, time step reduction 3 of 3 to 0.062...
017: dt: 0.1250, sse=847810.5, rms=1.575 (0.855%)
positioning took 0.9 minutes
inhibiting deformation at non-cortical midline structures...
deleting segment 0 with 19 points - only 0.00% unknown
deleting segment 1 with 9 points - only 0.00% unknown
removing 3 vertex label from ripped group
deleting segment 2 with 3 points - only 0.00% unknown
removing 4 vertex label from ripped group
deleting segment 3 with 4 points - only 0.00% unknown
deleting segment 4 with 51 points - only 0.00% unknown
deleting segment 5 with 10 points - only 0.00% unknown
removing 1 vertex label from ripped group
deleting segment 6 with 1 points - only 0.00% unknown
deleting segment 7 with 14 points - only 0.00% unknown
deleting segment 8 with 79 points - only 0.00% unknown
removing 4 vertex label from ripped group
deleting segment 9 with 4 points - only 0.00% unknown
deleting segment 10 with 74 points - only 0.00% unknown
removing 2 vertex label from ripped group
deleting segment 11 with 2 points - only 0.00% unknown
deleting segment 12 with 11 points - only 0.00% unknown
mean border=79.7, 66 (14) missing vertices, mean dist -0.1 [0.3 (%66.6)->0.2 (%33.4))]
%84 local maxima, %11 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=0.5, host=mbp-e, nav=1, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.250
vertex spacing 0.90 +- 0.26 (0.03-->11.08) (max @ vno 58451 --> 62899)
face area 0.34 +- 0.18 (0.00-->10.59)
mean absolute distance = 0.26 +- 0.37
3476 vertices more than 2 sigmas from mean.
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1107605.4, rms=3.517
018: dt: 0.5000, sse=1097581.5, rms=3.415 (2.892%)
rms = 3.79, time step reduction 1 of 3 to 0.250...
019: dt: 0.2500, sse=901811.2, rms=2.257 (33.902%)
020: dt: 0.2500, sse=845513.2, rms=1.807 (19.942%)
021: dt: 0.2500, sse=830732.5, rms=1.663 (7.964%)
rms = 1.67, time step reduction 2 of 3 to 0.125...
022: dt: 0.1250, sse=821662.5, rms=1.570 (5.590%)
023: dt: 0.1250, sse=810525.6, rms=1.438 (8.397%)
rms = 1.43, time step reduction 3 of 3 to 0.062...
024: dt: 0.1250, sse=809885.9, rms=1.432 (0.441%)
positioning took 1.0 minutes
inhibiting deformation at non-cortical midline structures...
deleting segment 0 with 19 points - only 0.00% unknown
deleting segment 1 with 9 points - only 0.00% unknown
removing 3 vertex label from ripped group
deleting segment 2 with 3 points - only 0.00% unknown
deleting segment 3 with 6 points - only 0.00% unknown
deleting segment 4 with 55 points - only 0.00% unknown
deleting segment 5 with 12 points - only 0.00% unknown
deleting segment 6 with 17 points - only 0.00% unknown
removing 1 vertex label from ripped group
deleting segment 7 with 1 points - only 0.00% unknown
deleting segment 8 with 84 points - only 0.00% unknown
removing 4 vertex label from ripped group
deleting segment 9 with 4 points - only 0.00% unknown
deleting segment 10 with 89 points - only 0.00% unknown
removing 2 vertex label from ripped group
deleting segment 11 with 2 points - only 0.00% unknown
deleting segment 12 with 14 points - only 0.00% unknown
mean border=80.7, 71 (11) missing vertices, mean dist -0.1 [0.3 (%55.7)->0.2 (%44.3))]
%88 local maxima, % 8 large gradients and % 0 min vals, 0 gradients ignored
tol=1.0e-04, sigma=0.2, host=mbp-e, nav=0, nbrs=2, l_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
writing white matter surface to /Users/elizavetalavrova/bert/surf/rh.white...
writing smoothed curvature to rh.curv
000: dt: 0.0000, sse=847700.7, rms=1.935
rms = 2.45, time step reduction 1 of 3 to 0.250...
025: dt: 0.2500, sse=791208.0, rms=1.308 (32.402%)
026: dt: 0.2500, sse=777563.2, rms=1.049 (19.794%)
rms = 1.06, time step reduction 2 of 3 to 0.125...
rms = 1.04, time step reduction 3 of 3 to 0.062...
027: dt: 0.1250, sse=769475.4, rms=1.041 (0.775%)
positioning took 0.5 minutes
generating cortex label...
10 non-cortical segments detected
only using segment with 7596 vertices
erasing segment 1 (vno[0] = 85473)
erasing segment 2 (vno[0] = 98010)
erasing segment 3 (vno[0] = 99983)
erasing segment 4 (vno[0] = 103895)
erasing segment 5 (vno[0] = 103943)
erasing segment 6 (vno[0] = 108034)
erasing segment 7 (vno[0] = 109091)
erasing segment 8 (vno[0] = 117140)
erasing segment 9 (vno[0] = 150507)
writing cortex label to /Users/elizavetalavrova/bert/label/rh.cortex.label...
writing curvature file /Users/elizavetalavrova/bert/surf/rh.curv
writing smoothed area to rh.area
writing curvature file /Users/elizavetalavrova/bert/surf/rh.area
vertex spacing 0.90 +- 0.27 (0.01-->11.10) (max @ vno 58451 --> 62899)
face area 0.34 +- 0.18 (0.00-->10.49)
repositioning cortical surface to gray/csf boundary.
smoothing T1 volume with sigma = 2.000
averaging target values for 5 iterations...
inhibiting deformation at non-cortical midline structures...
removing 3 vertex label from ripped group
removing 1 vertex label from ripped group
smoothing surface for 5 iterations...
reading initial pial vertex positions from white.preaparc...
mean border=46.8, 65 (65) missing vertices, mean dist 1.7 [0.2 (%0.0)->2.7 (%100.0))]
%12 local maxima, %49 large gradients and %35 min vals, 346 gradients ignored
perforing initial smooth deformation to move away from white surface
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=16, nbrs=2, l_surf_repulse=1.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.05
000: dt: 0.0000, sse=34895744.0, rms=34.376
001: dt: 0.0500, sse=30641784.0, rms=32.164 (6.434%)
002: dt: 0.0500, sse=27567456.0, rms=30.466 (5.280%)
003: dt: 0.0500, sse=25216096.0, rms=29.100 (4.484%)
004: dt: 0.0500, sse=23329682.0, rms=27.956 (3.932%)
005: dt: 0.0500, sse=21758148.0, rms=26.965 (3.542%)
006: dt: 0.0500, sse=20410870.0, rms=26.086 (3.260%)
007: dt: 0.0500, sse=19232548.0, rms=25.292 (3.043%)
008: dt: 0.0500, sse=18184168.0, rms=24.565 (2.878%)
009: dt: 0.0500, sse=17239744.0, rms=23.890 (2.747%)
010: dt: 0.0500, sse=16380269.0, rms=23.259 (2.642%)
positioning took 1.0 minutes
mean border=46.7, 68 (35) missing vertices, mean dist 1.4 [0.1 (%0.0)->2.2 (%100.0))]
%13 local maxima, %50 large gradients and %34 min vals, 317 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=16, nbrs=2, l_surf_repulse=1.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.05
000: dt: 0.0000, sse=17138444.0, rms=23.825
011: dt: 0.0500, sse=16344872.0, rms=23.241 (2.450%)
012: dt: 0.0500, sse=15613962.0, rms=22.690 (2.371%)
013: dt: 0.0500, sse=14937810.0, rms=22.168 (2.300%)
014: dt: 0.0500, sse=14311020.0, rms=21.673 (2.233%)
015: dt: 0.0500, sse=13728300.0, rms=21.202 (2.172%)
016: dt: 0.0500, sse=13185355.0, rms=20.754 (2.114%)
017: dt: 0.0500, sse=12678289.0, rms=20.326 (2.061%)
018: dt: 0.0500, sse=12204786.0, rms=19.919 (2.006%)
019: dt: 0.0500, sse=11761711.0, rms=19.529 (1.954%)
020: dt: 0.0500, sse=11345914.0, rms=19.157 (1.908%)
positioning took 1.0 minutes
mean border=46.6, 97 (28) missing vertices, mean dist 1.2 [0.1 (%0.7)->1.8 (%99.3))]
%13 local maxima, %50 large gradients and %33 min vals, 325 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=16, nbrs=2, l_surf_repulse=1.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.05
000: dt: 0.0000, sse=11445174.0, rms=19.255
021: dt: 0.0500, sse=11046706.0, rms=18.893 (1.881%)
022: dt: 0.0500, sse=10671784.0, rms=18.546 (1.838%)
023: dt: 0.0500, sse=10316848.0, rms=18.211 (1.806%)
024: dt: 0.0500, sse=9982130.0, rms=17.889 (1.766%)
025: dt: 0.0500, sse=9666024.0, rms=17.580 (1.729%)
026: dt: 0.0500, sse=9366684.0, rms=17.282 (1.695%)
027: dt: 0.0500, sse=9081095.0, rms=16.993 (1.674%)
028: dt: 0.0500, sse=8806710.0, rms=16.710 (1.664%)
029: dt: 0.0500, sse=8543236.0, rms=16.434 (1.653%)
030: dt: 0.0500, sse=8289647.5, rms=16.163 (1.645%)
positioning took 1.0 minutes
mean border=46.5, 139 (27) missing vertices, mean dist 1.0 [0.1 (%6.6)->1.6 (%93.4))]
%13 local maxima, %50 large gradients and %33 min vals, 298 gradients ignored
tol=1.0e-04, sigma=2.0, host=mbp-e, nav=16, nbrs=2, l_surf_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 1.000
averaging target values for 5 iterations...
000: dt: 0.0000, sse=8347153.5, rms=16.228
031: dt: 0.5000, sse=6539763.5, rms=14.164 (12.719%)
032: dt: 0.5000, sse=5230258.0, rms=12.449 (12.103%)
033: dt: 0.5000, sse=4210753.5, rms=10.934 (12.176%)
034: dt: 0.5000, sse=3440731.8, rms=9.623 (11.990%)
035: dt: 0.5000, sse=2865273.0, rms=8.516 (11.503%)
036: dt: 0.5000, sse=2429139.2, rms=7.565 (11.170%)
037: dt: 0.5000, sse=2117552.5, rms=6.809 (9.987%)
038: dt: 0.5000, sse=1911430.9, rms=6.253 (8.163%)
039: dt: 0.5000, sse=1777882.1, rms=5.870 (6.126%)
040: dt: 0.5000, sse=1701287.1, rms=5.632 (4.056%)
041: dt: 0.5000, sse=1645749.2, rms=5.460 (3.061%)
042: dt: 0.5000, sse=1617211.6, rms=5.363 (1.776%)
043: dt: 0.5000, sse=1590762.1, rms=5.278 (1.584%)
rms = 5.25, time step reduction 1 of 3 to 0.250...
044: dt: 0.5000, sse=1585219.6, rms=5.255 (0.441%)
045: dt: 0.2500, sse=1436765.6, rms=4.686 (10.824%)
046: dt: 0.2500, sse=1394532.2, rms=4.524 (3.453%)
rms = 4.53, time step reduction 2 of 3 to 0.125...
047: dt: 0.1250, sse=1382442.9, rms=4.474 (1.113%)
048: dt: 0.1250, sse=1367665.1, rms=4.410 (1.430%)
rms = 4.40, time step reduction 3 of 3 to 0.062...
049: dt: 0.1250, sse=1366643.5, rms=4.403 (0.146%)
positioning took 2.6 minutes
mean border=45.3, 2374 (13) missing vertices, mean dist 0.1 [0.2 (%49.7)->0.5 (%50.3))]
%24 local maxima, %41 large gradients and %29 min vals, 123 gradients ignored
tol=1.0e-04, sigma=1.0, host=mbp-e, nav=8, nbrs=2, l_surf_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.500
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1660844.6, rms=4.789
050: dt: 0.5000, sse=1602330.1, rms=4.583 (4.290%)
rms = 4.57, time step reduction 1 of 3 to 0.250...
051: dt: 0.5000, sse=1588758.5, rms=4.573 (0.216%)
052: dt: 0.2500, sse=1426709.8, rms=3.827 (16.324%)
053: dt: 0.2500, sse=1380672.5, rms=3.614 (5.568%)
rms = 3.59, time step reduction 2 of 3 to 0.125...
054: dt: 0.2500, sse=1378112.4, rms=3.594 (0.532%)
055: dt: 0.1250, sse=1339572.5, rms=3.391 (5.650%)
rms = 3.36, time step reduction 3 of 3 to 0.062...
056: dt: 0.1250, sse=1332633.4, rms=3.356 (1.041%)
positioning took 1.0 minutes
mean border=44.5, 2583 (10) missing vertices, mean dist 0.1 [0.1 (%52.6)->0.4 (%47.4))]
%39 local maxima, %27 large gradients and %28 min vals, 153 gradients ignored
tol=1.0e-04, sigma=0.5, host=mbp-e, nav=4, nbrs=2, l_surf_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
smoothing T1 volume with sigma = 0.250
averaging target values for 5 iterations...
000: dt: 0.0000, sse=1399061.2, rms=3.677
rms = 4.15, time step reduction 1 of 3 to 0.250...
057: dt: 0.2500, sse=1358794.4, rms=3.474 (5.503%)
058: dt: 0.2500, sse=1347444.2, rms=3.424 (1.457%)
rms = 3.43, time step reduction 2 of 3 to 0.125...
rms = 3.39, time step reduction 3 of 3 to 0.062...
059: dt: 0.1250, sse=1340758.4, rms=3.387 (1.084%)
positioning took 0.6 minutes
mean border=43.8, 4378 (8) missing vertices, mean dist 0.1 [0.2 (%52.5)->0.3 (%47.5))]
%43 local maxima, %23 large gradients and %27 min vals, 142 gradients ignored
tol=1.0e-04, sigma=0.2, host=mbp-e, nav=2, nbrs=2, l_surf_repulse=5.000, l_tspring=1.000, l_nspring=0.500, l_intensity=0.200, l_curv=1.000
mom=0.00, dt=0.50
writing pial surface to /Users/elizavetalavrova/bert/surf/rh.pial...
writing smoothed curvature to rh.curv.pial
000: dt: 0.0000, sse=1370173.6, rms=3.528
rms = 4.00, time step reduction 1 of 3 to 0.250...
060: dt: 0.2500, sse=1339073.0, rms=3.366 (4.604%)
061: dt: 0.2500, sse=1320015.1, rms=3.284 (2.442%)
rms = 3.27, time step reduction 2 of 3 to 0.125...
062: dt: 0.2500, sse=1315600.2, rms=3.272 (0.374%)
063: dt: 0.1250, sse=1290267.2, rms=3.130 (4.334%)
rms = 3.10, time step reduction 3 of 3 to 0.062...
064: dt: 0.1250, sse=1283573.1, rms=3.097 (1.047%)
positioning took 0.9 minutes
writing curvature file /Users/elizavetalavrova/bert/surf/rh.curv.pial
writing smoothed area to rh.area.pial
writing curvature file /Users/elizavetalavrova/bert/surf/rh.area.pial
vertex spacing 1.01 +- 0.45 (0.06-->12.12) (max @ vno 58451 --> 62899)
face area 0.40 +- 0.32 (0.00-->13.54)
measuring cortical thickness...
writing cortical thickness estimate to 'thickness' file.
0 of 150852 vertices processed
25000 of 150852 vertices processed
50000 of 150852 vertices processed
75000 of 150852 vertices processed
100000 of 150852 vertices processed
125000 of 150852 vertices processed
150000 of 150852 vertices processed
0 of 150852 vertices processed
25000 of 150852 vertices processed
50000 of 150852 vertices processed
75000 of 150852 vertices processed
100000 of 150852 vertices processed
125000 of 150852 vertices processed
150000 of 150852 vertices processed
thickness calculation complete, 100:621 truncations.
32683 vertices at 0 distance
107892 vertices at 1 distance
95508 vertices at 2 distance
37554 vertices at 3 distance
10807 vertices at 4 distance
3155 vertices at 5 distance
955 vertices at 6 distance
348 vertices at 7 distance
119 vertices at 8 distance
67 vertices at 9 distance
40 vertices at 10 distance
20 vertices at 11 distance
17 vertices at 12 distance
16 vertices at 13 distance
10 vertices at 14 distance
16 vertices at 15 distance
9 vertices at 16 distance
1 vertices at 17 distance
1 vertices at 18 distance
2 vertices at 19 distance
12 vertices at 20 distance
writing curvature file /Users/elizavetalavrova/bert/surf/rh.thickness
positioning took 15.6 minutes
#--------------------------------------------
#@# Surf Volume lh Wed Mar 27 17:33:52 CET 2019
/Users/elizavetalavrova/bert/surf
/Users/elizavetalavrova/bert/surf
mris_calc -o lh.area.mid lh.area add lh.area.pial
Saving result to 'lh.area.mid' (type = MRI_CURV_FILE)                       [ ok ]
mris_calc -o lh.area.mid lh.area.mid div 2
Saving result to 'lh.area.mid' (type = MRI_CURV_FILE)                       [ ok ]
mris_convert --volume bert lh /Users/elizavetalavrova/bert/surf/lh.volume
masking with /Users/elizavetalavrova/bert/label/lh.cortex.label
Total face volume 263342
Total vertex volume 258917 (mask=0)
#@# bert lh 258917
 
vertexvol Done
#--------------------------------------------
#@# Surf Volume rh Wed Mar 27 17:33:56 CET 2019
/Users/elizavetalavrova/bert/surf
/Users/elizavetalavrova/bert/surf
mris_calc -o rh.area.mid rh.area add rh.area.pial
Saving result to 'rh.area.mid' (type = MRI_CURV_FILE)                       [ ok ]
mris_calc -o rh.area.mid rh.area.mid div 2
Saving result to 'rh.area.mid' (type = MRI_CURV_FILE)                       [ ok ]
mris_convert --volume bert rh /Users/elizavetalavrova/bert/surf/rh.volume
masking with /Users/elizavetalavrova/bert/label/rh.cortex.label
Total face volume 266424
Total vertex volume 262392 (mask=0)
#@# bert rh 262392
 
vertexvol Done
#--------------------------------------------
#@# Cortical ribbon mask Wed Mar 27 17:33:59 CET 2019
/Users/elizavetalavrova/bert/mri
\n mris_volmask --aseg_name aseg.presurf --label_left_white 2 --label_left_ribbon 3 --label_right_white 41 --label_right_ribbon 42 --save_ribbon bert \n
SUBJECTS_DIR is /Users/elizavetalavrova
loading input data...
computing distance to left white surface 
computing distance to left pial surface 
computing distance to right white surface 
computing distance to right pial surface 
 hemi masks overlap voxels = 66
writing volume /Users/elizavetalavrova/bert/mri/ribbon.mgz
mris_volmask took 17.32 minutes
 writing ribbon files
#-----------------------------------------
#@# Parcellation Stats lh Wed Mar 27 17:51:19 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_anatomical_stats -th3 -mgz -cortex ../label/lh.cortex.label -f ../stats/lh.aparc.stats -b -a ../label/lh.aparc.annot -c ../label/aparc.annot.ctab bert lh white \n
computing statistics for each annotation in ../label/lh.aparc.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/lh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/lh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/lh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
INFO: using ../label/lh.cortex.label as mask to calc cortex NumVert, SurfArea and MeanThickness.
Using TH3 vertex volume calc
Total face volume 263342
Total vertex volume 258917 (mask=0)
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Saving annotation colortable ../label/aparc.annot.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 1611   1091   2604  2.461 0.401     0.109     0.022       12     1.4  bankssts
 1237    797   2142  2.472 0.558     0.128     0.028       19     1.3  caudalanteriorcingulate
 3731   2493   6500  2.448 0.481     0.128     0.036       40     5.0  caudalmiddlefrontal
 2714   1745   3667  1.920 0.422     0.145     0.043       42     4.6  cuneus
  542    415   1643  3.258 0.834     0.124     0.026        4     0.6  entorhinal
 4478   3121   9475  2.618 0.621     0.138     0.034       65     5.8  fusiform
 7937   5444  14178  2.386 0.432     0.133     0.033      109    10.3  inferiorparietal
 5523   3778  12186  2.712 0.688     0.136     0.036       90     7.8  inferiortemporal
 1964   1297   2979  2.097 0.780     0.130     0.034       29     2.5  isthmuscingulate
 8631   5564  12907  2.103 0.498     0.143     0.043      135    14.1  lateraloccipital
 4689   3248   9028  2.463 0.588     0.133     0.041       72     8.1  lateralorbitofrontal
 4883   3238   7458  2.098 0.610     0.150     0.048       76     9.2  lingual
 2969   2088   5568  2.324 0.656     0.127     0.034       53     4.3  medialorbitofrontal
 4979   3465  12129  2.823 0.644     0.126     0.031       65     5.8  middletemporal
  892    627   2174  2.954 0.804     0.116     0.030       10     1.0  parahippocampal
 2464   1598   3585  2.122 0.452     0.128     0.039       28     3.9  paracentral
 2745   1831   5179  2.514 0.463     0.119     0.030       30     3.3  parsopercularis
 1168    813   2754  2.637 0.644     0.134     0.037       17     1.7  parsorbitalis
 1733   1161   3296  2.468 0.476     0.121     0.030       22     1.9  parstriangularis
 2274   1472   2174  1.669 0.373     0.147     0.047       29     4.2  pericalcarine
 7229   4708  11174  2.148 0.586     0.125     0.036       91     9.9  postcentral
 1878   1279   2998  2.178 0.553     0.128     0.029       28     2.2  posteriorcingulate
 8909   5677  14951  2.416 0.606     0.128     0.045      106    16.9  precentral
 5798   3961   9533  2.286 0.498     0.131     0.033       71     7.4  precuneus
 1267    874   2603  2.554 0.611     0.131     0.033       21     1.6  rostralanteriorcingulate
10749   7354  19620  2.329 0.560     0.136     0.036      147    16.1  rostralmiddlefrontal
13571   9213  27726  2.563 0.580     0.134     0.040      176    21.7  superiorfrontal
 7730   5083  11646  2.126 0.441     0.124     0.030       87     8.6  superiorparietal
 6455   4480  13985  2.712 0.601     0.116     0.027       68     7.3  superiortemporal
 5940   4033  10582  2.419 0.493     0.126     0.030       73     7.0  supramarginal
  490    315   1036  2.428 0.567     0.177     0.074       15     1.4  frontalpole
  682    518   2471  3.347 0.921     0.145     0.043        8     1.2  temporalpole
  749    430   1122  2.361 0.290     0.121     0.034        8     0.9  transversetemporal
 3868   2597   7831  2.887 0.754     0.126     0.040       52     6.3  insula
\n mris_anatomical_stats -th3 -mgz -cortex ../label/lh.cortex.label -f ../stats/lh.aparc.pial.stats -b -a ../label/lh.aparc.annot -c ../label/aparc.annot.ctab bert lh pial \n
computing statistics for each annotation in ../label/lh.aparc.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/lh.pial...
reading input pial surface /Users/elizavetalavrova/bert/surf/lh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/lh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
INFO: using ../label/lh.cortex.label as mask to calc cortex NumVert, SurfArea and MeanThickness.
Using TH3 vertex volume calc
Total face volume 263342
Total vertex volume 258917 (mask=0)
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Saving annotation colortable ../label/aparc.annot.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 1611   1025   2604  2.461 0.401     0.124     0.036       21     2.3  bankssts
 1237    969   2142  2.472 0.558     0.167     0.046       57     2.2  caudalanteriorcingulate
 3731   2735   6500  2.448 0.481     0.137     0.038       57     6.5  caudalmiddlefrontal
 2714   2076   3667  1.920 0.422     0.142     0.035       45     4.2  cuneus
  542    625   1643  3.258 0.834     0.199     0.059       14     1.3  entorhinal
 4478   3959   9475  2.618 0.621     0.176     0.048       96     9.7  fusiform
 7937   6378  14178  2.386 0.432     0.143     0.033      101    11.2  inferiorparietal
 5523   5017  12186  2.712 0.688     0.160     0.041       75    10.1  inferiortemporal
 1964   1518   2979  2.097 0.780     0.151     0.039       54     3.3  isthmuscingulate
 8631   6652  12907  2.103 0.498     0.144     0.037      144    13.9  lateraloccipital
 4689   4084   9028  2.463 0.588     0.169     0.049       85     9.8  lateralorbitofrontal
 4883   3913   7458  2.098 0.610     0.153     0.043       82     9.3  lingual
 2969   2738   5568  2.324 0.656     0.173     0.044       51     5.9  medialorbitofrontal
 4979   4863  12129  2.823 0.644     0.159     0.036       67     8.0  middletemporal
  892    866   2174  2.954 0.804     0.171     0.044       12     1.8  parahippocampal
 2464   1759   3585  2.122 0.452     0.119     0.026       33     2.8  paracentral
 2745   2256   5179  2.514 0.463     0.142     0.035       36     4.2  parsopercularis
 1168   1223   2754  2.637 0.644     0.183     0.041       22     2.0  parsorbitalis
 1733   1436   3296  2.468 0.476     0.139     0.031       21     2.2  parstriangularis
 2274   1187   2174  1.669 0.373     0.118     0.034       47     3.4  pericalcarine
 7229   5672  11174  2.148 0.586     0.133     0.029       74     9.2  postcentral
 1878   1452   2998  2.178 0.553     0.147     0.037       33     3.0  posteriorcingulate
 8909   6273  14951  2.416 0.606     0.119     0.049      111    11.8  precentral
 5798   4293   9533  2.286 0.498     0.137     0.034       80     7.9  precuneus
 1267   1193   2603  2.554 0.611     0.176     0.046       26     2.2  rostralanteriorcingulate
10749   9226  19620  2.329 0.560     0.162     0.042      173    20.0  rostralmiddlefrontal
13571  11898  27726  2.563 0.580     0.159     0.040      196    23.9  superiorfrontal
 7730   5749  11646  2.126 0.441     0.134     0.031       96    10.4  superiorparietal
 6455   5587  13985  2.712 0.601     0.144     0.034       81     9.7  superiortemporal
 5940   4651  10582  2.419 0.493     0.137     0.032       86     7.9  supramarginal
  490    561   1036  2.428 0.567     0.213     0.047        9     1.1  frontalpole
  682    949   2471  3.347 0.921     0.194     0.036        7     1.2  temporalpole
  749    548   1122  2.361 0.290     0.112     0.027        6     0.9  transversetemporal
 3868   2567   7831  2.887 0.754     0.143     0.043       94     6.6  insula
#-----------------------------------------
#@# Parcellation Stats rh Wed Mar 27 17:52:48 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_anatomical_stats -th3 -mgz -cortex ../label/rh.cortex.label -f ../stats/rh.aparc.stats -b -a ../label/rh.aparc.annot -c ../label/aparc.annot.ctab bert rh white \n
computing statistics for each annotation in ../label/rh.aparc.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/rh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/rh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/rh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
INFO: using ../label/rh.cortex.label as mask to calc cortex NumVert, SurfArea and MeanThickness.
Using TH3 vertex volume calc
Total face volume 266424
Total vertex volume 262392 (mask=0)
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Saving annotation colortable ../label/aparc.annot.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 1285    915   2388  2.687 0.365     0.120     0.023       10     1.2  bankssts
 1469   1015   2757  2.456 0.628     0.150     0.035       28     2.1  caudalanteriorcingulate
 3795   2562   6652  2.385 0.456     0.128     0.035       41     5.4  caudalmiddlefrontal
 2900   1871   3565  1.838 0.493     0.150     0.045       45     5.2  cuneus
  642    498   2036  3.073 0.727     0.139     0.035        7     0.9  entorhinal
 4492   3096   9764  2.723 0.646     0.139     0.034       64     6.0  fusiform
 7930   5361  14343  2.393 0.477     0.131     0.032      100    10.5  inferiorparietal
 5555   3806  12777  2.778 0.689     0.123     0.029       77     6.3  inferiortemporal
 1334    874   2207  2.251 0.743     0.118     0.034       18     1.3  isthmuscingulate
 8599   5784  14210  2.205 0.554     0.152     0.047      139    15.7  lateraloccipital
 4570   3163   9164  2.614 0.562     0.134     0.041       67     7.6  lateralorbitofrontal
 4746   3258   7611  2.102 0.675     0.148     0.045       68     8.6  lingual
 3430   2482   6835  2.511 0.584     0.139     0.042       86     5.5  medialorbitofrontal
 5219   3624  11898  2.752 0.610     0.127     0.030       67     6.2  middletemporal
  972    656   2170  2.821 0.827     0.115     0.025       10     0.9  parahippocampal
 2210   1361   3136  2.218 0.498     0.133     0.046       34     4.5  paracentral
 2115   1440   4175  2.694 0.547     0.133     0.044       32     3.8  parsopercularis
 1457    967   2937  2.442 0.615     0.144     0.040       22     2.3  parsorbitalis
 2577   1717   4885  2.552 0.529     0.129     0.032       31     3.3  parstriangularis
 2443   1639   2242  1.582 0.439     0.142     0.040       28     4.1  pericalcarine
 6543   4284   9464  1.999 0.599     0.118     0.033       71     8.4  postcentral
 2021   1319   3400  2.311 0.669     0.140     0.038       34     2.7  posteriorcingulate
 9962   6351  16145  2.384 0.577     0.131     0.046      124    19.5  precentral
 6391   4240  10837  2.389 0.562     0.125     0.031       75     7.7  precuneus
  933    624   2066  2.882 0.544     0.134     0.040       17     1.3  rostralanteriorcingulate
10264   7151  18477  2.337 0.523     0.145     0.040      149    17.1  rostralmiddlefrontal
12657   8657  25476  2.609 0.596     0.137     0.039      159    19.5  superiorfrontal
 8514   5605  13244  2.154 0.420     0.129     0.033      104    10.7  superiorparietal
 5795   3974  12855  2.870 0.653     0.117     0.027       58     6.5  superiortemporal
 6436   4426  12155  2.457 0.510     0.129     0.033       80     8.3  supramarginal
  546    372   1202  2.777 0.501     0.177     0.056       14     1.2  frontalpole
  688    534   2749  3.598 0.707     0.153     0.043        9     1.5  temporalpole
  573    340   1049  2.546 0.332     0.121     0.027        7     0.5  transversetemporal
 3554   2410   7493  2.912 0.783     0.124     0.042       58     6.4  insula
\n mris_anatomical_stats -th3 -mgz -cortex ../label/rh.cortex.label -f ../stats/rh.aparc.pial.stats -b -a ../label/rh.aparc.annot -c ../label/aparc.annot.ctab bert rh pial \n
computing statistics for each annotation in ../label/rh.aparc.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/rh.pial...
reading input pial surface /Users/elizavetalavrova/bert/surf/rh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/rh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
INFO: using ../label/rh.cortex.label as mask to calc cortex NumVert, SurfArea and MeanThickness.
Using TH3 vertex volume calc
Total face volume 266424
Total vertex volume 262392 (mask=0)
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Saving annotation colortable ../label/aparc.annot.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 1285    850   2388  2.687 0.365     0.128     0.032       23     1.8  bankssts
 1469   1210   2757  2.456 0.628     0.187     0.059       89     3.4  caudalanteriorcingulate
 3795   2927   6652  2.385 0.456     0.140     0.036       58     6.0  caudalmiddlefrontal
 2900   2116   3565  1.838 0.493     0.144     0.041       48     5.3  cuneus
  642    769   2036  3.073 0.727     0.230     0.057       16     1.9  entorhinal
 4492   3902   9764  2.723 0.646     0.166     0.046       99     9.5  fusiform
 7930   6363  14343  2.393 0.477     0.152     0.038      127    13.3  inferiorparietal
 5555   5182  12777  2.778 0.689     0.161     0.040       80    10.1  inferiortemporal
 1334   1038   2207  2.251 0.743     0.161     0.072       72     2.4  isthmuscingulate
 8599   6901  14210  2.205 0.554     0.152     0.043      167    16.9  lateraloccipital
 4570   3839   9164  2.614 0.562     0.166     0.050       94    10.0  lateralorbitofrontal
 4746   3947   7611  2.102 0.675     0.153     0.041       69     8.9  lingual
 3430   3034   6835  2.511 0.584     0.162     0.045       72     6.4  medialorbitofrontal
 5219   4891  11898  2.752 0.610     0.162     0.038       73     8.8  middletemporal
  972    859   2170  2.821 0.827     0.156     0.042       14     1.8  parahippocampal
 2210   1491   3136  2.218 0.498     0.121     0.031       39     3.0  paracentral
 2115   1615   4175  2.694 0.547     0.148     0.044       40     4.2  parsopercularis
 1457   1382   2937  2.442 0.615     0.166     0.041       21     2.9  parsorbitalis
 2577   2111   4885  2.552 0.529     0.148     0.035       34     4.0  parstriangularis
 2443   1334   2242  1.582 0.439     0.111     0.036       56     3.3  pericalcarine
 6543   5110   9464  1.999 0.599     0.129     0.027       60     8.2  postcentral
 2021   1574   3400  2.311 0.669     0.161     0.048       42     4.0  posteriorcingulate
 9962   6910  16145  2.384 0.577     0.120     0.032      135    15.2  precentral
 6391   4801  10837  2.389 0.562     0.145     0.037       99    10.6  precuneus
  933    852   2066  2.882 0.544     0.190     0.057       64     2.1  rostralanteriorcingulate
10264   8598  18477  2.337 0.523     0.165     0.042      177    19.7  rostralmiddlefrontal
12657  10463  25476  2.609 0.596     0.152     0.040      184    21.2  superiorfrontal
 8514   6563  13244  2.154 0.420     0.138     0.031      105    11.6  superiorparietal
 5795   4857  12855  2.870 0.653     0.143     0.034       70     8.9  superiortemporal
 6436   5219  12155  2.457 0.510     0.144     0.034       94     9.5  supramarginal
  546    520   1202  2.777 0.501     0.170     0.038       10     0.9  frontalpole
  688    978   2749  3.598 0.707     0.212     0.048        8     1.5  temporalpole
  573    461   1049  2.546 0.332     0.113     0.023        3     0.6  transversetemporal
 3554   2438   7493  2.912 0.783     0.151     0.050       91     7.5  insula
#-----------------------------------------
#@# Cortical Parc 2 lh Wed Mar 27 17:54:11 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_ca_label -l ../label/lh.cortex.label -aseg ../mri/aseg.presurf.mgz -seed 1234 bert lh ../surf/lh.sphere.reg /Applications/freesurfer/average/lh.CDaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs ../label/lh.aparc.a2009s.annot \n
setting seed for random number generator to 1234
using ../mri/aseg.presurf.mgz aseg volume to correct midline
$Id: mris_ca_label.c,v 1.37 2014/02/04 17:46:42 fischl Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading atlas from /Applications/freesurfer/average/lh.CDaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs...
reading color table from GCSA file....
average std = 2.9   using min determinant for regularization = 0.086
0 singular and 762 ill-conditioned covariance matrices regularized
input 0: MEAN CURVATURE, flags 0, avgs 5, name mean_curvature
labeling surface...
10 labels changed using aseg
relabeling using gibbs priors...
000:  10017 changed, 151159 examined...
001:   2285 changed, 38881 examined...
002:    671 changed, 11888 examined...
003:    277 changed, 3804 examined...
004:    137 changed, 1553 examined...
005:     67 changed, 799 examined...
006:     31 changed, 385 examined...
007:     20 changed, 179 examined...
008:      9 changed, 112 examined...
009:      7 changed, 50 examined...
010:      3 changed, 41 examined...
011:      1 changed, 17 examined...
012:      0 changed, 9 examined...
8 labels changed using aseg
000: 294 total segments, 205 labels (2858 vertices) changed
001: 101 total segments, 13 labels (18 vertices) changed
002: 88 total segments, 0 labels (0 vertices) changed
10 filter iterations complete (10 requested, 39 changed)
rationalizing unknown annotations with cortex label
relabeling Medial_wall label...
829 vertices marked for relabeling...
829 labels changed in reclassification.
writing output to ../label/lh.aparc.a2009s.annot...
classification took 0 minutes and 21 seconds.
#-----------------------------------------
#@# Cortical Parc 2 rh Wed Mar 27 17:54:32 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_ca_label -l ../label/rh.cortex.label -aseg ../mri/aseg.presurf.mgz -seed 1234 bert rh ../surf/rh.sphere.reg /Applications/freesurfer/average/rh.CDaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs ../label/rh.aparc.a2009s.annot \n
setting seed for random number generator to 1234
using ../mri/aseg.presurf.mgz aseg volume to correct midline
$Id: mris_ca_label.c,v 1.37 2014/02/04 17:46:42 fischl Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading atlas from /Applications/freesurfer/average/rh.CDaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs...
reading color table from GCSA file....
average std = 1.4   using min determinant for regularization = 0.020
0 singular and 719 ill-conditioned covariance matrices regularized
input 0: MEAN CURVATURE, flags 0, avgs 5, name mean_curvature
labeling surface...
23 labels changed using aseg
relabeling using gibbs priors...
000:   9809 changed, 150852 examined...
001:   2285 changed, 38554 examined...
002:    671 changed, 12000 examined...
003:    255 changed, 3753 examined...
004:    119 changed, 1492 examined...
005:     76 changed, 715 examined...
006:     26 changed, 406 examined...
007:     14 changed, 166 examined...
008:      5 changed, 81 examined...
009:      4 changed, 31 examined...
010:      2 changed, 23 examined...
011:      2 changed, 10 examined...
012:      3 changed, 10 examined...
013:      1 changed, 12 examined...
014:      1 changed, 7 examined...
015:      3 changed, 9 examined...
016:      1 changed, 11 examined...
017:      0 changed, 7 examined...
2 labels changed using aseg
000: 294 total segments, 203 labels (3038 vertices) changed
001: 103 total segments, 12 labels (56 vertices) changed
002: 92 total segments, 1 labels (1 vertices) changed
003: 91 total segments, 0 labels (0 vertices) changed
10 filter iterations complete (10 requested, 45 changed)
rationalizing unknown annotations with cortex label
relabeling Medial_wall label...
757 vertices marked for relabeling...
757 labels changed in reclassification.
writing output to ../label/rh.aparc.a2009s.annot...
classification took 0 minutes and 23 seconds.
#-----------------------------------------
#@# Parcellation Stats 2 lh Wed Mar 27 17:54:55 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_anatomical_stats -th3 -mgz -cortex ../label/lh.cortex.label -f ../stats/lh.aparc.a2009s.stats -b -a ../label/lh.aparc.a2009s.annot -c ../label/aparc.annot.a2009s.ctab bert lh white \n
computing statistics for each annotation in ../label/lh.aparc.a2009s.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/lh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/lh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/lh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
INFO: using ../label/lh.cortex.label as mask to calc cortex NumVert, SurfArea and MeanThickness.
Using TH3 vertex volume calc
Total face volume 263342
Total vertex volume 258917 (mask=0)
reading colortable from annotation file...
colortable with 76 entries read (originally Simple_surface_labels2008.txt)
Saving annotation colortable ../label/aparc.annot.a2009s.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 1666   1134   2985  2.247 0.593     0.144     0.042       28     2.8  G&S_frontomargin
 1937   1304   3413  2.236 0.519     0.149     0.041       31     3.1  G&S_occipital_inf
 1837   1146   2843  2.123 0.495     0.136     0.051       29     3.7  G&S_paracentral
 1688   1139   3872  2.835 0.451     0.133     0.035       23     2.2  G&S_subcentral
  979    653   2050  2.460 0.522     0.168     0.058       24     2.4  G&S_transv_frontopol
 2242   1624   4361  2.416 0.605     0.119     0.029       24     2.6  G&S_cingul-Ant
 1766   1208   2925  2.392 0.468     0.120     0.025       19     1.8  G&S_cingul-Mid-Ant
 1586   1135   2763  2.299 0.416     0.122     0.028       16     1.9  G&S_cingul-Mid-Post
  788    526   1688  2.588 0.514     0.162     0.045       15     1.4  G_cingul-Post-dorsal
  379    245    675  2.332 0.800     0.156     0.049        8     0.7  G_cingul-Post-ventral
 2514   1587   3460  1.882 0.469     0.153     0.047       42     4.5  G_cuneus
 1628   1074   3798  2.705 0.521     0.130     0.033       23     2.3  G_front_inf-Opercular
  504    329   1185  2.584 0.599     0.150     0.044       10     0.8  G_front_inf-Orbital
  811    536   1841  2.604 0.477     0.134     0.041       13     1.1  G_front_inf-Triangul
 6111   4121  12999  2.487 0.571     0.145     0.044      106    10.6  G_front_middle
 9221   6131  20389  2.664 0.600     0.145     0.047      144    17.0  G_front_sup
  818    581   1993  3.214 0.700     0.149     0.046       13     1.5  G_Ins_lg&S_cent_ins
  857    555   2673  3.422 0.855     0.141     0.057       21     1.8  G_insular_short
 2686   1754   5333  2.428 0.484     0.144     0.042       50     4.0  G_occipital_middle
 1445    969   2340  2.079 0.433     0.144     0.044       21     2.1  G_occipital_sup
 1585   1113   4031  2.810 0.613     0.152     0.041       33     2.3  G_oc-temp_lat-fusifor
 3475   2232   5358  2.014 0.672     0.159     0.057       62     7.6  G_oc-temp_med-Lingual
 1337    936   3743  3.139 0.805     0.138     0.041       18     2.2  G_oc-temp_med-Parahip
 2935   2028   6868  2.580 0.580     0.143     0.045       55     5.5  G_orbital
 2956   1984   6136  2.498 0.456     0.149     0.041       54     4.7  G_pariet_inf-Angular
 3179   2101   6211  2.507 0.500     0.140     0.036       52     4.3  G_pariet_inf-Supramar
 2813   1833   5040  2.287 0.420     0.123     0.029       35     3.1  G_parietal_sup
 2947   1837   4895  2.189 0.567     0.134     0.045       49     4.8  G_postcentral
 3428   2042   6648  2.540 0.651     0.138     0.063       57     9.1  G_precentral
 2810   1915   5769  2.416 0.513     0.146     0.042       51     4.2  G_precuneus
 1185    860   2865  2.448 0.706     0.140     0.046       31     2.2  G_rectus
  142    105    366  2.901 0.598     0.085     0.029        2     0.1  G_subcallosal
  556    331   1043  2.548 0.441     0.120     0.036        6     0.6  G_temp_sup-G_T_transv
 2229   1542   6775  3.042 0.594     0.148     0.044       41     4.0  G_temp_sup-Lateral
  735    542   2161  3.370 0.662     0.097     0.021        4     0.6  G_temp_sup-Plan_polar
 1219    892   2187  2.431 0.379     0.107     0.019       10     1.0  G_temp_sup-Plan_tempo
 3051   2055   8416  3.008 0.662     0.152     0.045       69     5.2  G_temporal_inf
 2684   1852   8010  3.040 0.631     0.141     0.041       51     3.6  G_temporal_middle
  240    167    357  2.425 0.282     0.108     0.017        1     0.2  Lat_Fis-ant-Horizont
  326    237    563  2.428 0.323     0.082     0.015        1     0.2  Lat_Fis-ant-Vertical
 1304    854   1631  2.353 0.502     0.113     0.029       10     1.5  Lat_Fis-post
 2343   1426   3115  1.892 0.509     0.153     0.056       47     5.1  Pole_occipital
 1561   1111   4746  3.038 0.832     0.136     0.036       18     2.4  Pole_temporal
 2768   1879   3076  1.881 0.533     0.138     0.037       31     4.2  S_calcarine
 4051   2698   4610  1.970 0.510     0.121     0.033       33     6.0  S_central
 1043    707   1367  2.106 0.346     0.106     0.021        6     1.0  S_cingul-Marginalis
  683    450    959  2.425 0.486     0.095     0.036        5     1.2  S_circular_insula_ant
 1429    964   2153  2.563 0.491     0.091     0.020        6     1.3  S_circular_insula_inf
 1946   1313   2709  2.480 0.467     0.105     0.022       10     1.8  S_circular_insula_sup
 1320    929   2011  2.355 0.460     0.112     0.019        8     1.1  S_collat_transv_ant
  713    492    819  2.030 0.419     0.140     0.032        7     1.1  S_collat_transv_post
 2373   1628   3618  2.334 0.471     0.112     0.023       18     2.3  S_front_inf
 1865   1286   2725  2.142 0.487     0.126     0.028       17     2.3  S_front_middle
 3920   2684   6242  2.264 0.475     0.121     0.033       34     5.2  S_front_sup
  187    140    327  2.478 0.410     0.141     0.035        2     0.3  S_interm_prim-Jensen
 3045   2034   3830  2.052 0.384     0.119     0.026       29     3.3  S_intrapariet&P_trans
  846    599    994  1.900 0.315     0.119     0.025        6     0.9  S_oc_middle&Lunatus
 1697   1097   2037  2.055 0.353     0.113     0.025       13     1.6  S_oc_sup&transversal
  728    480    882  2.338 0.357     0.146     0.036       10     1.1  S_occipital_ant
  969    678   1416  2.202 0.454     0.152     0.040       16     1.6  S_oc-temp_lat
 1879   1359   3351  2.505 0.514     0.123     0.029       19     2.0  S_oc-temp_med&Lingual
  442    304    675  2.251 0.414     0.129     0.034        4     0.6  S_orbital_lateral
  811    572   1049  2.003 0.550     0.122     0.032       13     1.2  S_orbital_med-olfact
 1835   1271   3427  2.510 0.642     0.125     0.032       21     2.2  S_orbital-H_Shaped
 2433   1644   3270  2.196 0.443     0.118     0.026       23     2.6  S_parieto_occipital
 1654    996   1353  1.778 0.655     0.108     0.023       23     1.2  S_pericallosal
 2864   1899   3988  2.113 0.409     0.107     0.022       22     2.4  S_postcentral
 1788   1212   2579  2.342 0.431     0.117     0.027       14     1.8  S_precentral-inf-part
 1355    922   1877  2.203 0.414     0.106     0.023        8     1.3  S_precentral-sup-part
  930    633   1361  2.297 0.610     0.117     0.028       10     1.1  S_suborbital
 1229    858   1679  2.096 0.380     0.128     0.028       11     1.5  S_subparietal
 1752   1216   2595  2.429 0.456     0.114     0.023       10     1.7  S_temporal_inf
 7006   4834  10855  2.384 0.412     0.106     0.021       50     6.0  S_temporal_sup
  418    286    567  2.324 0.359     0.126     0.021        4     0.4  S_temporal_transverse
#-----------------------------------------
#@# Parcellation Stats 2 rh Wed Mar 27 17:55:42 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_anatomical_stats -th3 -mgz -cortex ../label/rh.cortex.label -f ../stats/rh.aparc.a2009s.stats -b -a ../label/rh.aparc.a2009s.annot -c ../label/aparc.annot.a2009s.ctab bert rh white \n
computing statistics for each annotation in ../label/rh.aparc.a2009s.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/rh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/rh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/rh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
INFO: using ../label/rh.cortex.label as mask to calc cortex NumVert, SurfArea and MeanThickness.
Using TH3 vertex volume calc
Total face volume 266424
Total vertex volume 262392 (mask=0)
reading colortable from annotation file...
colortable with 76 entries read (originally Simple_surface_labels2008.txt)
Saving annotation colortable ../label/aparc.annot.a2009s.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 1105    759   2015  2.412 0.599     0.164     0.045       19     2.3  G&S_frontomargin
 1609   1081   3234  2.601 0.629     0.167     0.056       31     3.1  G&S_occipital_inf
 1386    814   2120  2.209 0.530     0.137     0.051       21     2.5  G&S_paracentral
 1547   1056   3334  2.729 0.513     0.131     0.033       20     2.0  G&S_subcentral
 1396    979   2962  2.500 0.497     0.161     0.052       25     2.8  G&S_transv_frontopol
 3863   2671   7515  2.669 0.526     0.132     0.036       61     5.1  G&S_cingul-Ant
 1880   1267   3477  2.606 0.466     0.131     0.034       23     2.4  G&S_cingul-Mid-Ant
 2019   1347   3341  2.384 0.498     0.138     0.040       28     2.9  G&S_cingul-Mid-Post
  463    313   1216  2.870 0.560     0.151     0.043        9     0.6  G_cingul-Post-dorsal
  383    231    700  2.443 0.614     0.134     0.051        6     0.7  G_cingul-Post-ventral
 2807   1812   3519  1.781 0.530     0.153     0.047       46     5.0  G_cuneus
 1544   1018   3840  2.868 0.525     0.145     0.055       34     3.4  G_front_inf-Opercular
  418    264    979  2.673 0.451     0.126     0.036        6     0.5  G_front_inf-Orbital
 1191    787   2738  2.731 0.432     0.148     0.043       20     1.9  G_front_inf-Triangul
 4462   3047   9638  2.476 0.547     0.155     0.045       83     8.2  G_front_middle
 7919   5290  17699  2.710 0.605     0.146     0.049      140    15.0  G_front_sup
  785    530   1818  2.925 0.808     0.152     0.078       31     2.6  G_Ins_lg&S_cent_ins
  743    491   2444  3.619 0.770     0.137     0.043       14     1.5  G_insular_short
 2807   1933   6154  2.485 0.479     0.158     0.048       57     4.9  G_occipital_middle
 1857   1216   3028  2.114 0.453     0.141     0.044       27     3.3  G_occipital_sup
 1918   1264   5418  3.120 0.572     0.156     0.046       37     3.5  G_oc-temp_lat-fusifor
 2999   2070   5310  2.081 0.748     0.154     0.048       47     5.6  G_oc-temp_med-Lingual
 1337    950   4015  3.111 0.743     0.134     0.034       19     1.7  G_oc-temp_med-Parahip
 3101   2162   7514  2.697 0.614     0.147     0.048       60     5.8  G_orbital
 2780   1787   6069  2.567 0.489     0.140     0.040       50     4.2  G_pariet_inf-Angular
 3064   2124   6848  2.622 0.523     0.140     0.040       47     4.9  G_pariet_inf-Supramar
 2753   1773   5097  2.266 0.449     0.141     0.038       47     3.8  G_parietal_sup
 2601   1657   4033  1.975 0.535     0.128     0.040       40     3.9  G_postcentral
 3880   2348   7388  2.515 0.610     0.142     0.064       62    10.3  G_precentral
 2551   1660   5114  2.455 0.624     0.141     0.040       42     3.7  G_precuneus
  909    734   2545  2.533 0.628     0.154     0.052       36     2.2  G_rectus
  240    162    463  2.620 0.623     0.094     0.033        2     0.3  G_subcallosal
  460    265    908  2.549 0.317     0.120     0.027        6     0.4  G_temp_sup-G_T_transv
 1899   1326   5793  3.278 0.513     0.143     0.038       31     3.0  G_temp_sup-Lateral
  775    543   2181  3.504 0.716     0.109     0.031        6     1.0  G_temp_sup-Plan_polar
 1342    941   2579  2.418 0.472     0.134     0.032       17     1.7  G_temp_sup-Plan_tempo
 2878   1975   8037  2.954 0.730     0.135     0.035       56     3.9  G_temporal_inf
 3152   2158   8560  2.963 0.543     0.141     0.036       55     4.3  G_temporal_middle
  492    325    624  2.209 0.403     0.092     0.017        2     0.4  Lat_Fis-ant-Horizont
  242    176    366  2.817 0.594     0.127     0.018        1     0.3  Lat_Fis-ant-Vertical
 1573   1053   2168  2.402 0.429     0.108     0.022       10     1.4  Lat_Fis-post
 3894   2619   5909  1.968 0.575     0.156     0.055       67     8.1  Pole_occipital
 1727   1284   5318  3.054 0.758     0.154     0.041       30     3.2  Pole_temporal
 2538   1695   2871  1.960 0.622     0.137     0.038       27     4.1  S_calcarine
 3635   2399   3774  1.862 0.508     0.124     0.035       32     5.6  S_central
 1200    813   1798  2.035 0.488     0.128     0.031       14     1.5  S_cingul-Marginalis
  587    394    978  2.750 0.486     0.103     0.023        3     0.6  S_circular_insula_ant
 1373    925   1978  2.548 0.602     0.087     0.016        5     1.0  S_circular_insula_inf
 1589   1100   2509  2.738 0.410     0.101     0.022        7     1.5  S_circular_insula_sup
 1253    879   1953  2.375 0.510     0.101     0.016        6     0.9  S_collat_transv_ant
  592    392    649  2.111 0.403     0.119     0.024        4     0.7  S_collat_transv_post
 2343   1609   3548  2.281 0.407     0.112     0.022       17     2.3  S_front_inf
 3059   2139   4601  2.156 0.472     0.138     0.037       37     5.1  S_front_middle
 3604   2519   6022  2.361 0.503     0.129     0.033       37     4.8  S_front_sup
  311    228    485  2.041 0.365     0.075     0.013        1     0.2  S_interm_prim-Jensen
 3113   2100   4035  2.084 0.369     0.120     0.026       26     3.5  S_intrapariet&P_trans
 1147    814   1332  1.937 0.321     0.130     0.026       10     1.3  S_oc_middle&Lunatus
 1806   1208   2263  2.147 0.403     0.130     0.029       17     2.3  S_oc_sup&transversal
  986    675   1600  2.376 0.460     0.137     0.034       11     1.4  S_occipital_ant
 1182    803   1839  2.517 0.481     0.107     0.027        6     1.2  S_oc-temp_lat
 1776   1239   2711  2.464 0.534     0.115     0.024       15     1.6  S_oc-temp_med&Lingual
  448    332    565  1.845 0.327     0.144     0.032        4     0.6  S_orbital_lateral
  870    608   1206  2.251 0.621     0.110     0.020        6     0.6  S_orbital_med-olfact
 1892   1299   3205  2.476 0.504     0.135     0.038       23     3.1  S_orbital-H_Shaped
 2777   1826   3533  2.214 0.438     0.112     0.023       22     2.7  S_parieto_occipital
 1542    972   1343  1.836 0.743     0.128     0.026       25     1.3  S_pericallosal
 2576   1721   3057  2.013 0.426     0.107     0.025       16     2.6  S_postcentral
 2424   1623   3467  2.373 0.385     0.121     0.027       20     2.9  S_precentral-inf-part
 1780   1194   2291  2.192 0.434     0.115     0.030       12     2.1  S_precentral-sup-part
  346    254    529  2.595 0.461     0.153     0.037        3     0.5  S_suborbital
 1363    957   2193  2.293 0.511     0.121     0.027       12     1.6  S_subparietal
 1529   1070   2225  2.291 0.528     0.120     0.021       11     1.4  S_temporal_inf
 5959   4131   9387  2.440 0.451     0.102     0.018       33     4.7  S_temporal_sup
  296    210    417  2.449 0.409     0.143     0.030        3     0.4  S_temporal_transverse
#-----------------------------------------
#@# Cortical Parc 3 lh Wed Mar 27 17:56:26 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_ca_label -l ../label/lh.cortex.label -aseg ../mri/aseg.presurf.mgz -seed 1234 bert lh ../surf/lh.sphere.reg /Applications/freesurfer/average/lh.DKTaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs ../label/lh.aparc.DKTatlas.annot \n
setting seed for random number generator to 1234
using ../mri/aseg.presurf.mgz aseg volume to correct midline
$Id: mris_ca_label.c,v 1.37 2014/02/04 17:46:42 fischl Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading atlas from /Applications/freesurfer/average/lh.DKTaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs...
reading color table from GCSA file....
average std = 1.4   using min determinant for regularization = 0.020
0 singular and 383 ill-conditioned covariance matrices regularized
input 0: MEAN CURVATURE, flags 0, avgs 5, name mean_curvature
labeling surface...
1628 labels changed using aseg
relabeling using gibbs priors...
000:   2224 changed, 151159 examined...
001:    517 changed, 10096 examined...
002:    153 changed, 2883 examined...
003:     60 changed, 896 examined...
004:     31 changed, 342 examined...
005:     27 changed, 163 examined...
006:     19 changed, 138 examined...
007:      8 changed, 96 examined...
008:      6 changed, 50 examined...
009:      9 changed, 41 examined...
010:      6 changed, 41 examined...
011:      7 changed, 32 examined...
012:      8 changed, 40 examined...
013:      4 changed, 41 examined...
014:      3 changed, 27 examined...
015:      2 changed, 17 examined...
016:      3 changed, 14 examined...
017:      2 changed, 14 examined...
018:      1 changed, 14 examined...
019:      1 changed, 7 examined...
020:      1 changed, 7 examined...
021:      1 changed, 7 examined...
022:      0 changed, 7 examined...
292 labels changed using aseg
000: 68 total segments, 35 labels (367 vertices) changed
001: 33 total segments, 0 labels (0 vertices) changed
10 filter iterations complete (10 requested, 7 changed)
rationalizing unknown annotations with cortex label
relabeling unknown label...
relabeling corpuscallosum label...
689 vertices marked for relabeling...
689 labels changed in reclassification.
writing output to ../label/lh.aparc.DKTatlas.annot...
classification took 0 minutes and 17 seconds.
#-----------------------------------------
#@# Cortical Parc 3 rh Wed Mar 27 17:56:43 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_ca_label -l ../label/rh.cortex.label -aseg ../mri/aseg.presurf.mgz -seed 1234 bert rh ../surf/rh.sphere.reg /Applications/freesurfer/average/rh.DKTaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs ../label/rh.aparc.DKTatlas.annot \n
setting seed for random number generator to 1234
using ../mri/aseg.presurf.mgz aseg volume to correct midline
$Id: mris_ca_label.c,v 1.37 2014/02/04 17:46:42 fischl Exp $
  $Id: mrisurf.c,v 1.781.2.6 2016/12/27 16:47:14 zkaufman Exp $
reading atlas from /Applications/freesurfer/average/rh.DKTaparc.atlas.acfb40.noaparc.i12.2016-08-02.gcs...
reading color table from GCSA file....
average std = 0.9   using min determinant for regularization = 0.009
0 singular and 325 ill-conditioned covariance matrices regularized
input 0: MEAN CURVATURE, flags 0, avgs 5, name mean_curvature
labeling surface...
1650 labels changed using aseg
relabeling using gibbs priors...
000:   2172 changed, 150852 examined...
001:    538 changed, 10212 examined...
002:    185 changed, 3086 examined...
003:     85 changed, 1040 examined...
004:     35 changed, 455 examined...
005:     13 changed, 195 examined...
006:      7 changed, 90 examined...
007:      7 changed, 38 examined...
008:      5 changed, 32 examined...
009:      4 changed, 27 examined...
010:      1 changed, 19 examined...
011:      1 changed, 7 examined...
012:      0 changed, 6 examined...
213 labels changed using aseg
000: 60 total segments, 27 labels (172 vertices) changed
001: 33 total segments, 0 labels (0 vertices) changed
10 filter iterations complete (10 requested, 12 changed)
rationalizing unknown annotations with cortex label
relabeling unknown label...
relabeling corpuscallosum label...
630 vertices marked for relabeling...
630 labels changed in reclassification.
writing output to ../label/rh.aparc.DKTatlas.annot...
classification took 0 minutes and 17 seconds.
#-----------------------------------------
#@# Parcellation Stats 3 lh Wed Mar 27 17:57:00 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_anatomical_stats -th3 -mgz -cortex ../label/lh.cortex.label -f ../stats/lh.aparc.DKTatlas.stats -b -a ../label/lh.aparc.DKTatlas.annot -c ../label/aparc.annot.DKTatlas.ctab bert lh white \n
computing statistics for each annotation in ../label/lh.aparc.DKTatlas.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/lh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/lh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/lh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
INFO: using ../label/lh.cortex.label as mask to calc cortex NumVert, SurfArea and MeanThickness.
Using TH3 vertex volume calc
Total face volume 263342
Total vertex volume 258917 (mask=0)
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Saving annotation colortable ../label/aparc.annot.DKTatlas.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 2203   1461   3950  2.510 0.542     0.123     0.027       29     2.3  caudalanteriorcingulate
 4052   2715   7038  2.441 0.480     0.128     0.035       43     5.5  caudalmiddlefrontal
 3510   2274   4826  1.977 0.427     0.142     0.040       51     5.5  cuneus
  509    387   1581  3.278 0.856     0.129     0.029        4     0.6  entorhinal
 4080   2858   8356  2.574 0.589     0.138     0.035       61     5.2  fusiform
 8051   5502  14233  2.370 0.431     0.134     0.034      113    10.6  inferiorparietal
 5566   3803  12865  2.760 0.708     0.140     0.037       93     8.2  inferiortemporal
 1950   1286   2973  2.110 0.768     0.133     0.036       30     2.7  isthmuscingulate
 8532   5501  12643  2.104 0.498     0.142     0.042      127    13.6  lateraloccipital
 5073   3517  10306  2.481 0.659     0.139     0.043       89     8.9  lateralorbitofrontal
 5065   3353   7655  2.082 0.611     0.150     0.048       80     9.7  lingual
 2461   1722   4895  2.370 0.679     0.123     0.035       45     3.6  medialorbitofrontal
 6537   4548  14652  2.724 0.612     0.122     0.029       77     7.1  middletemporal
  932    656   2276  2.940 0.807     0.115     0.029       10     1.0  parahippocampal
 2916   1883   4420  2.165 0.460     0.127     0.039       33     4.7  paracentral
 2542   1693   4818  2.523 0.461     0.120     0.030       29     3.1  parsopercularis
 1201    799   2355  2.513 0.579     0.125     0.032       14     1.5  parsorbitalis
 2217   1495   3811  2.373 0.476     0.119     0.028       24     2.4  parstriangularis
 2296   1477   2197  1.671 0.372     0.147     0.047       30     4.3  pericalcarine
 8143   5325  12625  2.157 0.588     0.126     0.036      100    11.3  postcentral
 2167   1470   3545  2.204 0.558     0.125     0.028       32     2.5  posteriorcingulate
 8800   5597  14801  2.427 0.607     0.127     0.045      106    16.8  precentral
 5696   3902   9625  2.299 0.501     0.132     0.033       71     7.3  precuneus
 1802   1242   3402  2.462 0.596     0.133     0.033       27     2.3  rostralanteriorcingulate
 7725   5286  14878  2.375 0.561     0.135     0.037      107    11.4  rostralmiddlefrontal
14616   9977  29223  2.518 0.594     0.137     0.041      201    24.3  superiorfrontal
 5966   3916   9005  2.133 0.436     0.119     0.028       64     6.1  superiorparietal
 8254   5757  18326  2.752 0.654     0.119     0.029       86     9.9  superiortemporal
 5591   3768   9745  2.406 0.490     0.126     0.030       70     6.7  supramarginal
  753    438   1109  2.341 0.272     0.123     0.033        8     1.0  transversetemporal
 3276   2197   6783  2.877 0.752     0.122     0.040       42     5.4  insula
#-----------------------------------------
#@# Parcellation Stats 3 rh Wed Mar 27 17:57:41 CET 2019
/Users/elizavetalavrova/bert/scripts
\n mris_anatomical_stats -th3 -mgz -cortex ../label/rh.cortex.label -f ../stats/rh.aparc.DKTatlas.stats -b -a ../label/rh.aparc.DKTatlas.annot -c ../label/aparc.annot.DKTatlas.ctab bert rh white \n
computing statistics for each annotation in ../label/rh.aparc.DKTatlas.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/rh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/rh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/rh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
INFO: using ../label/rh.cortex.label as mask to calc cortex NumVert, SurfArea and MeanThickness.
Using TH3 vertex volume calc
Total face volume 266424
Total vertex volume 262392 (mask=0)
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Saving annotation colortable ../label/aparc.annot.DKTatlas.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 1622   1118   2977  2.450 0.625     0.150     0.035       30     2.3  caudalanteriorcingulate
 3800   2568   6710  2.395 0.462     0.130     0.035       42     5.4  caudalmiddlefrontal
 3584   2302   4590  1.897 0.498     0.146     0.043       53     6.0  cuneus
  582    448   1858  3.090 0.727     0.131     0.032        6     0.7  entorhinal
 3998   2749   8852  2.770 0.644     0.138     0.034       55     5.4  fusiform
 7812   5277  14073  2.397 0.475     0.132     0.033      100    10.6  inferiorparietal
 6002   4133  13543  2.737 0.693     0.125     0.029       83     6.8  inferiortemporal
 1374    894   2270  2.271 0.726     0.118     0.034       18     1.4  isthmuscingulate
 8773   5896  14512  2.202 0.551     0.152     0.048      143    15.9  lateraloccipital
 5102   3533  10287  2.582 0.580     0.140     0.043       81     8.8  lateralorbitofrontal
 4657   3201   7518  2.116 0.669     0.149     0.046       67     8.5  lingual
 2494   1808   5242  2.498 0.584     0.141     0.045       67     4.4  medialorbitofrontal
 6362   4415  14024  2.727 0.588     0.128     0.030       80     7.5  middletemporal
 1004    677   2224  2.827 0.815     0.114     0.024       10     0.9  parahippocampal
 2370   1467   3406  2.228 0.503     0.132     0.047       36     4.7  paracentral
 2645   1774   5162  2.709 0.534     0.135     0.042       40     4.7  parsopercularis
 1203    787   2286  2.462 0.618     0.129     0.034       14     1.7  parsorbitalis
 2472   1646   4476  2.458 0.515     0.128     0.032       29     3.0  parstriangularis
 2425   1630   2210  1.575 0.442     0.140     0.040       27     4.1  pericalcarine
 7244   4757  10404  2.007 0.591     0.120     0.032       79     9.4  postcentral
 2098   1355   3524  2.298 0.677     0.138     0.038       35     2.8  posteriorcingulate
 9443   6052  15586  2.398 0.578     0.131     0.046      117    18.4  precentral
 6458   4297  10947  2.365 0.571     0.125     0.031       75     7.8  precuneus
 1129    775   2359  2.835 0.577     0.131     0.036       19     1.4  rostralanteriorcingulate
 7444   5220  13587  2.335 0.536     0.146     0.039      110    12.4  rostralmiddlefrontal
16313  11163  32051  2.565 0.586     0.139     0.041      224    25.9  superiorfrontal
 6895   4536  10798  2.159 0.417     0.129     0.033       85     8.6  superiorparietal
 7402   5152  17368  2.913 0.675     0.120     0.030       78     9.1  superiortemporal
 6083   4186  11462  2.457 0.509     0.128     0.033       74     7.8  supramarginal
  560    332   1035  2.539 0.329     0.122     0.027        7     0.5  transversetemporal
 3297   2245   7053  2.955 0.759     0.121     0.037       49     5.7  insula
#-----------------------------------------
#@# WM/GM Contrast lh Wed Mar 27 17:58:21 CET 2019
/Users/elizavetalavrova/bert/scripts
\n pctsurfcon --s bert --lh-only \n
Log file is /Users/elizavetalavrova/bert/scripts/pctsurfcon.log
Wed Mar 27 17:58:22 CET 2019
setenv SUBJECTS_DIR /Users/elizavetalavrova
cd /Users/elizavetalavrova/bert/scripts
/Applications/freesurfer/bin/pctsurfcon
$Id: FreeSurferEnv.csh,v 1.89 2016/06/09 14:54:31 zkaufman Exp $
Darwin MacBook-Pro-Elizaveta.local 18.2.0 Darwin Kernel Version 18.2.0: Thu Dec 20 20:46:53 PST 2018; root:xnu-4903.241.1~1/RELEASE_X86_64 x86_64
FREESURFER_HOME /Applications/freesurfer
mri_vol2surf --mov /Users/elizavetalavrova/bert/mri/rawavg.mgz --hemi lh --noreshape --interp trilinear --projdist -1 --o /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9606/lh.wm.mgh --regheader bert --cortex
srcvol = /Users/elizavetalavrova/bert/mri/rawavg.mgz
srcreg unspecified
srcregold = 0
srcwarp unspecified
surf = white
hemi = lh
ProjDist = -1
reshape = 0
interp = trilinear
float2int = round
GetProjMax = 0
INFO: float2int code = 0
INFO: changing type to float
Done loading volume
Computing registration from header.
  Using /Users/elizavetalavrova/bert/mri/orig.mgz as target reference.
-------- original matrix -----------
 0.00000   1.00000   0.00000   0.00000;
-1.00000   0.00000   0.00000   0.00001;
 0.00000   0.00000   1.00000   0.00000;
 0.00000   0.00000   0.00000   1.00000;
-------- original matrix -----------
Loading label /Users/elizavetalavrova/bert/label/lh.cortex.label
Reading surface /Users/elizavetalavrova/bert/surf/lh.white
Done reading source surface
Mapping Source Volume onto Source Subject Surface
 1 -1 -1 -1
using old
Done mapping volume to surface
Number of source voxels hit = 73501
Masking with /Users/elizavetalavrova/bert/label/lh.cortex.label
Writing to /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9606/lh.wm.mgh
Dim: 151159 1 1
mri_vol2surf --mov /Users/elizavetalavrova/bert/mri/rawavg.mgz --hemi lh --noreshape --interp trilinear --o /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9606/lh.gm.mgh --projfrac 0.3 --regheader bert --cortex
srcvol = /Users/elizavetalavrova/bert/mri/rawavg.mgz
srcreg unspecified
srcregold = 0
srcwarp unspecified
surf = white
hemi = lh
ProjFrac = 0.3
thickness = thickness
reshape = 0
interp = trilinear
float2int = round
GetProjMax = 0
INFO: float2int code = 0
INFO: changing type to float
Done loading volume
Computing registration from header.
  Using /Users/elizavetalavrova/bert/mri/orig.mgz as target reference.
-------- original matrix -----------
 0.00000   1.00000   0.00000   0.00000;
-1.00000   0.00000   0.00000   0.00001;
 0.00000   0.00000   1.00000   0.00000;
 0.00000   0.00000   0.00000   1.00000;
-------- original matrix -----------
Loading label /Users/elizavetalavrova/bert/label/lh.cortex.label
Reading surface /Users/elizavetalavrova/bert/surf/lh.white
Done reading source surface
Reading thickness /Users/elizavetalavrova/bert/surf/lh.thickness
Done
Mapping Source Volume onto Source Subject Surface
 1 0.3 0.3 0.3
using old
Done mapping volume to surface
Number of source voxels hit = 89029
Masking with /Users/elizavetalavrova/bert/label/lh.cortex.label
Writing to /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9606/lh.gm.mgh
Dim: 151159 1 1
mri_concat /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9606/lh.wm.mgh /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9606/lh.gm.mgh --paired-diff-norm --mul 100 --o /Users/elizavetalavrova/bert/surf/lh.w-g.pct.mgh
ninputs = 2
Checking inputs
nframestot = 2
Allocing output
Done allocing
Combining pairs
nframes = 1
Multiplying by 100.000000
Writing to /Users/elizavetalavrova/bert/surf/lh.w-g.pct.mgh
mri_segstats --in /Users/elizavetalavrova/bert/surf/lh.w-g.pct.mgh --annot bert lh aparc --sum /Users/elizavetalavrova/bert/stats/lh.w-g.pct.stats --snr

$Id: mri_segstats.c,v 1.121 2016/05/31 17:27:11 greve Exp $
cwd 
cmdline mri_segstats --in /Users/elizavetalavrova/bert/surf/lh.w-g.pct.mgh --annot bert lh aparc --sum /Users/elizavetalavrova/bert/stats/lh.w-g.pct.stats --snr 
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64
user     elizavetalavrova
UseRobust  0
Constructing seg from annotation

Reading annotation /Users/elizavetalavrova/bert/label/lh.aparc.annot
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Seg base 1000
Loading /Users/elizavetalavrova/bert/surf/lh.w-g.pct.mgh
Vertex Area is 0.672056 mm^3
Generating list of segmentation ids
Found  36 segmentations
Computing statistics for each segmentation

Reporting on  35 segmentations
Using PrintSegStat
mri_segstats done
Cleaning up
#-----------------------------------------
#@# WM/GM Contrast rh Wed Mar 27 17:58:27 CET 2019
/Users/elizavetalavrova/bert/scripts
\n pctsurfcon --s bert --rh-only \n
Log file is /Users/elizavetalavrova/bert/scripts/pctsurfcon.log
Wed Mar 27 17:58:27 CET 2019
setenv SUBJECTS_DIR /Users/elizavetalavrova
cd /Users/elizavetalavrova/bert/scripts
/Applications/freesurfer/bin/pctsurfcon
$Id: FreeSurferEnv.csh,v 1.89 2016/06/09 14:54:31 zkaufman Exp $
Darwin MacBook-Pro-Elizaveta.local 18.2.0 Darwin Kernel Version 18.2.0: Thu Dec 20 20:46:53 PST 2018; root:xnu-4903.241.1~1/RELEASE_X86_64 x86_64
FREESURFER_HOME /Applications/freesurfer
mri_vol2surf --mov /Users/elizavetalavrova/bert/mri/rawavg.mgz --hemi rh --noreshape --interp trilinear --projdist -1 --o /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9678/rh.wm.mgh --regheader bert --cortex
srcvol = /Users/elizavetalavrova/bert/mri/rawavg.mgz
srcreg unspecified
srcregold = 0
srcwarp unspecified
surf = white
hemi = rh
ProjDist = -1
reshape = 0
interp = trilinear
float2int = round
GetProjMax = 0
INFO: float2int code = 0
INFO: changing type to float
Done loading volume
Computing registration from header.
  Using /Users/elizavetalavrova/bert/mri/orig.mgz as target reference.
-------- original matrix -----------
 0.00000   1.00000   0.00000   0.00000;
-1.00000   0.00000   0.00000   0.00001;
 0.00000   0.00000   1.00000   0.00000;
 0.00000   0.00000   0.00000   1.00000;
-------- original matrix -----------
Loading label /Users/elizavetalavrova/bert/label/rh.cortex.label
Reading surface /Users/elizavetalavrova/bert/surf/rh.white
Done reading source surface
Mapping Source Volume onto Source Subject Surface
 1 -1 -1 -1
using old
Done mapping volume to surface
Number of source voxels hit = 73632
Masking with /Users/elizavetalavrova/bert/label/rh.cortex.label
Writing to /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9678/rh.wm.mgh
Dim: 150852 1 1
mri_vol2surf --mov /Users/elizavetalavrova/bert/mri/rawavg.mgz --hemi rh --noreshape --interp trilinear --o /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9678/rh.gm.mgh --projfrac 0.3 --regheader bert --cortex
srcvol = /Users/elizavetalavrova/bert/mri/rawavg.mgz
srcreg unspecified
srcregold = 0
srcwarp unspecified
surf = white
hemi = rh
ProjFrac = 0.3
thickness = thickness
reshape = 0
interp = trilinear
float2int = round
GetProjMax = 0
INFO: float2int code = 0
INFO: changing type to float
Done loading volume
Computing registration from header.
  Using /Users/elizavetalavrova/bert/mri/orig.mgz as target reference.
-------- original matrix -----------
 0.00000   1.00000   0.00000   0.00000;
-1.00000   0.00000   0.00000   0.00001;
 0.00000   0.00000   1.00000   0.00000;
 0.00000   0.00000   0.00000   1.00000;
-------- original matrix -----------
Loading label /Users/elizavetalavrova/bert/label/rh.cortex.label
Reading surface /Users/elizavetalavrova/bert/surf/rh.white
Done reading source surface
Reading thickness /Users/elizavetalavrova/bert/surf/rh.thickness
Done
Mapping Source Volume onto Source Subject Surface
 1 0.3 0.3 0.3
using old
Done mapping volume to surface
Number of source voxels hit = 88936
Masking with /Users/elizavetalavrova/bert/label/rh.cortex.label
Writing to /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9678/rh.gm.mgh
Dim: 150852 1 1
mri_concat /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9678/rh.wm.mgh /Users/elizavetalavrova/bert/surf/tmp.pctsurfcon.9678/rh.gm.mgh --paired-diff-norm --mul 100 --o /Users/elizavetalavrova/bert/surf/rh.w-g.pct.mgh
ninputs = 2
Checking inputs
nframestot = 2
Allocing output
Done allocing
Combining pairs
nframes = 1
Multiplying by 100.000000
Writing to /Users/elizavetalavrova/bert/surf/rh.w-g.pct.mgh
mri_segstats --in /Users/elizavetalavrova/bert/surf/rh.w-g.pct.mgh --annot bert rh aparc --sum /Users/elizavetalavrova/bert/stats/rh.w-g.pct.stats --snr

$Id: mri_segstats.c,v 1.121 2016/05/31 17:27:11 greve Exp $
cwd 
cmdline mri_segstats --in /Users/elizavetalavrova/bert/surf/rh.w-g.pct.mgh --annot bert rh aparc --sum /Users/elizavetalavrova/bert/stats/rh.w-g.pct.stats --snr 
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64
user     elizavetalavrova
UseRobust  0
Constructing seg from annotation

Reading annotation /Users/elizavetalavrova/bert/label/rh.aparc.annot
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Seg base 2000
Loading /Users/elizavetalavrova/bert/surf/rh.w-g.pct.mgh
Vertex Area is 0.676798 mm^3
Generating list of segmentation ids
Found  36 segmentations
Computing statistics for each segmentation

Reporting on  35 segmentations
Using PrintSegStat
mri_segstats done
Cleaning up
#-----------------------------------------
#@# Relabel Hypointensities Wed Mar 27 17:58:33 CET 2019
/Users/elizavetalavrova/bert/mri
\n mri_relabel_hypointensities aseg.presurf.mgz ../surf aseg.presurf.hypos.mgz \n
reading input surface ../surf/lh.white...
relabeling lh hypointensities...
1448 voxels changed to hypointensity...
reading input surface ../surf/rh.white...
relabeling rh hypointensities...
1520 voxels changed to hypointensity...
3064 hypointense voxels neighboring cortex changed
#-----------------------------------------
#@# AParc-to-ASeg aparc Wed Mar 27 17:58:56 CET 2019
/Users/elizavetalavrova/bert
\n mri_aparc2aseg --s bert --volmask --aseg aseg.presurf.hypos --relabel mri/norm.mgz mri/transforms/talairach.m3z /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca mri/aseg.auto_noCCseg.label_intensities.txt \n
relabeling unlikely voxels interior to white matter surface:
	norm: mri/norm.mgz
	 XFORM: mri/transforms/talairach.m3z
	GCA: /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca
	label intensities: mri/aseg.auto_noCCseg.label_intensities.txt
SUBJECTS_DIR /Users/elizavetalavrova
subject bert
outvol /Users/elizavetalavrova/bert/mri/aparc+aseg.mgz
useribbon 0
baseoffset 0
RipUnknown 0

Reading lh white surface 
 /Users/elizavetalavrova/bert/surf/lh.white

Reading lh pial surface 
 /Users/elizavetalavrova/bert/surf/lh.pial

Loading lh annotations from /Users/elizavetalavrova/bert/label/lh.aparc.annot
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)

Reading rh white surface 
 /Users/elizavetalavrova/bert/surf/rh.white

Reading rh pial surface 
 /Users/elizavetalavrova/bert/surf/rh.pial

Loading rh annotations from /Users/elizavetalavrova/bert/label/rh.aparc.annot
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Have color table for lh white annotation
Have color table for rh white annotation
Loading ribbon segmentation from /Users/elizavetalavrova/bert/mri/ribbon.mgz

Building hash of lh white

Building hash of lh pial

Building hash of rh white

Building hash of rh pial

Loading aseg from /Users/elizavetalavrova/bert/mri/aseg.presurf.hypos.mgz
ASeg Vox2RAS: -----------
-1.00000   0.00000   0.00000   128.00000;
 0.00000   0.00000   1.00000  -128.00000;
 0.00000  -1.00000   0.00000   128.00000;
 0.00000   0.00000   0.00000   1.00000;
-------------------------

Labeling Slice
relabeling unlikely voxels in interior of white matter
setting orig areas to linear transform determinant scaled 6.59
reading 47 labels from mri/aseg.auto_noCCseg.label_intensities.txt
rescaling Left_Cerebral_White_Matter from 107 --> 108
rescaling Left_Cerebral_Cortex from 61 --> 57
rescaling Left_Lateral_Ventricle from 13 -->  4
rescaling Left_Inf_Lat_Vent from 34 --> 30
rescaling Left_Cerebellum_White_Matter from 86 --> 86
rescaling Left_Cerebellum_Cortex from 60 --> 50
rescaling Left_Thalamus from 94 --> 92
rescaling Left_Thalamus_Proper from 84 --> 93
rescaling Left_Caudate from 75 --> 74
rescaling Left_Putamen from 80 --> 78
rescaling Left_Pallidum from 98 --> 100
rescaling Third_Ventricle from 25 -->  6
rescaling Fourth_Ventricle from 22 -->  4
rescaling Brain_Stem from 81 --> 84
rescaling Left_Hippocampus from 57 --> 53
rescaling Left_Amygdala from 56 --> 57
rescaling CSF from 32 -->  8
rescaling Left_Accumbens_area from 62 --> 59
rescaling Left_VentralDC from 87 --> 89
rescaling Right_Cerebral_White_Matter from 105 --> 108
rescaling Right_Cerebral_Cortex from 58 --> 55
rescaling Right_Lateral_Ventricle from 13 -->  3
rescaling Right_Inf_Lat_Vent from 25 --> 21
rescaling Right_Cerebellum_White_Matter from 87 --> 82
rescaling Right_Cerebellum_Cortex from 59 --> 49
rescaling Right_Thalamus_Proper from 85 --> 90
rescaling Right_Caudate from 62 --> 71
rescaling Right_Putamen from 80 --> 78
rescaling Right_Pallidum from 97 --> 93
rescaling Right_Hippocampus from 53 --> 51
rescaling Right_Amygdala from 55 --> 62
rescaling Right_Accumbens_area from 65 --> 69
rescaling Right_VentralDC from 86 --> 94
rescaling Fifth_Ventricle from 40 -->  8
rescaling WM_hypointensities from 78 --> 81
rescaling non_WM_hypointensities from 40 --> 45
  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17  18  19 
 20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36  37  38  39 
 40  41  42  43  44  45  46  47  48  49  50  51  52  53  54  55  56  57  58  59 
 60  61  62  63  64  65  66  67  68  69  70  71  72  73  74  75  76  77  78  79 
 80  81  82  83  84  85  86  87  88  89  90  91  92  93  94  95  96  97  98  99 
100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 
120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 
140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 
160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 
180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 
200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 
220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 
240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 nctx = 517382
Used brute-force search on 0 voxels
relabeling unlikely voxels in interior of white matter
average std[0] = 7.3
pass 1: 135 changed.
pass 2: 3 changed.
pass 3: 0 changed.
nchanged = 0
Writing output aseg to /Users/elizavetalavrova/bert/mri/aparc+aseg.mgz
#-----------------------------------------
#@# AParc-to-ASeg a2009s Wed Mar 27 18:03:34 CET 2019
/Users/elizavetalavrova/bert
\n mri_aparc2aseg --s bert --volmask --aseg aseg.presurf.hypos --relabel mri/norm.mgz mri/transforms/talairach.m3z /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca mri/aseg.auto_noCCseg.label_intensities.txt --a2009s \n
relabeling unlikely voxels interior to white matter surface:
	norm: mri/norm.mgz
	 XFORM: mri/transforms/talairach.m3z
	GCA: /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca
	label intensities: mri/aseg.auto_noCCseg.label_intensities.txt
SUBJECTS_DIR /Users/elizavetalavrova
subject bert
outvol /Users/elizavetalavrova/bert/mri/aparc.a2009s+aseg.mgz
useribbon 0
baseoffset 10100
RipUnknown 0

Reading lh white surface 
 /Users/elizavetalavrova/bert/surf/lh.white

Reading lh pial surface 
 /Users/elizavetalavrova/bert/surf/lh.pial

Loading lh annotations from /Users/elizavetalavrova/bert/label/lh.aparc.a2009s.annot
reading colortable from annotation file...
colortable with 76 entries read (originally Simple_surface_labels2008.txt)

Reading rh white surface 
 /Users/elizavetalavrova/bert/surf/rh.white

Reading rh pial surface 
 /Users/elizavetalavrova/bert/surf/rh.pial

Loading rh annotations from /Users/elizavetalavrova/bert/label/rh.aparc.a2009s.annot
reading colortable from annotation file...
colortable with 76 entries read (originally Simple_surface_labels2008.txt)
Have color table for lh white annotation
Have color table for rh white annotation
Loading ribbon segmentation from /Users/elizavetalavrova/bert/mri/ribbon.mgz

Building hash of lh white

Building hash of lh pial

Building hash of rh white

Building hash of rh pial

Loading aseg from /Users/elizavetalavrova/bert/mri/aseg.presurf.hypos.mgz
ASeg Vox2RAS: -----------
-1.00000   0.00000   0.00000   128.00000;
 0.00000   0.00000   1.00000  -128.00000;
 0.00000  -1.00000   0.00000   128.00000;
 0.00000   0.00000   0.00000   1.00000;
-------------------------

Labeling Slice
relabeling unlikely voxels in interior of white matter
setting orig areas to linear transform determinant scaled 6.59
reading 47 labels from mri/aseg.auto_noCCseg.label_intensities.txt
rescaling Left_Cerebral_White_Matter from 107 --> 108
rescaling Left_Cerebral_Cortex from 61 --> 57
rescaling Left_Lateral_Ventricle from 13 -->  4
rescaling Left_Inf_Lat_Vent from 34 --> 30
rescaling Left_Cerebellum_White_Matter from 86 --> 86
rescaling Left_Cerebellum_Cortex from 60 --> 50
rescaling Left_Thalamus from 94 --> 92
rescaling Left_Thalamus_Proper from 84 --> 93
rescaling Left_Caudate from 75 --> 74
rescaling Left_Putamen from 80 --> 78
rescaling Left_Pallidum from 98 --> 100
rescaling Third_Ventricle from 25 -->  6
rescaling Fourth_Ventricle from 22 -->  4
rescaling Brain_Stem from 81 --> 84
rescaling Left_Hippocampus from 57 --> 53
rescaling Left_Amygdala from 56 --> 57
rescaling CSF from 32 -->  8
rescaling Left_Accumbens_area from 62 --> 59
rescaling Left_VentralDC from 87 --> 89
rescaling Right_Cerebral_White_Matter from 105 --> 108
rescaling Right_Cerebral_Cortex from 58 --> 55
rescaling Right_Lateral_Ventricle from 13 -->  3
rescaling Right_Inf_Lat_Vent from 25 --> 21
rescaling Right_Cerebellum_White_Matter from 87 --> 82
rescaling Right_Cerebellum_Cortex from 59 --> 49
rescaling Right_Thalamus_Proper from 85 --> 90
rescaling Right_Caudate from 62 --> 71
rescaling Right_Putamen from 80 --> 78
rescaling Right_Pallidum from 97 --> 93
rescaling Right_Hippocampus from 53 --> 51
rescaling Right_Amygdala from 55 --> 62
rescaling Right_Accumbens_area from 65 --> 69
rescaling Right_VentralDC from 86 --> 94
rescaling Fifth_Ventricle from 40 -->  8
rescaling WM_hypointensities from 78 --> 81
rescaling non_WM_hypointensities from 40 --> 45
  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17  18  19 
 20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36  37  38  39 
 40  41  42  43  44  45  46  47  48  49  50  51  52  53  54  55  56  57  58  59 
 60  61  62  63  64  65  66  67  68  69  70  71  72  73  74  75  76  77  78  79 
 80  81  82  83  84  85  86  87  88  89  90  91  92  93  94  95  96  97  98  99 
100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 
120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 
140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 
160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 
180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 
200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 
220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 
240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 nctx = 517406
Used brute-force search on 0 voxels
relabeling unlikely voxels in interior of white matter
average std[0] = 7.3
pass 1: 135 changed.
pass 2: 3 changed.
pass 3: 0 changed.
nchanged = 0
Writing output aseg to /Users/elizavetalavrova/bert/mri/aparc.a2009s+aseg.mgz
#-----------------------------------------
#@# AParc-to-ASeg DKTatlas Wed Mar 27 18:08:11 CET 2019
/Users/elizavetalavrova/bert
\n mri_aparc2aseg --s bert --volmask --aseg aseg.presurf.hypos --relabel mri/norm.mgz mri/transforms/talairach.m3z /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca mri/aseg.auto_noCCseg.label_intensities.txt --annot aparc.DKTatlas --o mri/aparc.DKTatlas+aseg.mgz \n
relabeling unlikely voxels interior to white matter surface:
	norm: mri/norm.mgz
	 XFORM: mri/transforms/talairach.m3z
	GCA: /Applications/freesurfer/average/RB_all_2016-05-10.vc700.gca
	label intensities: mri/aseg.auto_noCCseg.label_intensities.txt
SUBJECTS_DIR /Users/elizavetalavrova
subject bert
outvol mri/aparc.DKTatlas+aseg.mgz
useribbon 0
baseoffset 0
RipUnknown 0

Reading lh white surface 
 /Users/elizavetalavrova/bert/surf/lh.white

Reading lh pial surface 
 /Users/elizavetalavrova/bert/surf/lh.pial

Loading lh annotations from /Users/elizavetalavrova/bert/label/lh.aparc.DKTatlas.annot
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)

Reading rh white surface 
 /Users/elizavetalavrova/bert/surf/rh.white

Reading rh pial surface 
 /Users/elizavetalavrova/bert/surf/rh.pial

Loading rh annotations from /Users/elizavetalavrova/bert/label/rh.aparc.DKTatlas.annot
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Have color table for lh white annotation
Have color table for rh white annotation
Loading ribbon segmentation from /Users/elizavetalavrova/bert/mri/ribbon.mgz

Building hash of lh white

Building hash of lh pial

Building hash of rh white

Building hash of rh pial

Loading aseg from /Users/elizavetalavrova/bert/mri/aseg.presurf.hypos.mgz
ASeg Vox2RAS: -----------
-1.00000   0.00000   0.00000   128.00000;
 0.00000   0.00000   1.00000  -128.00000;
 0.00000  -1.00000   0.00000   128.00000;
 0.00000   0.00000   0.00000   1.00000;
-------------------------

Labeling Slice
relabeling unlikely voxels in interior of white matter
setting orig areas to linear transform determinant scaled 6.59
reading 47 labels from mri/aseg.auto_noCCseg.label_intensities.txt
rescaling Left_Cerebral_White_Matter from 107 --> 108
rescaling Left_Cerebral_Cortex from 61 --> 57
rescaling Left_Lateral_Ventricle from 13 -->  4
rescaling Left_Inf_Lat_Vent from 34 --> 30
rescaling Left_Cerebellum_White_Matter from 86 --> 86
rescaling Left_Cerebellum_Cortex from 60 --> 50
rescaling Left_Thalamus from 94 --> 92
rescaling Left_Thalamus_Proper from 84 --> 93
rescaling Left_Caudate from 75 --> 74
rescaling Left_Putamen from 80 --> 78
rescaling Left_Pallidum from 98 --> 100
rescaling Third_Ventricle from 25 -->  6
rescaling Fourth_Ventricle from 22 -->  4
rescaling Brain_Stem from 81 --> 84
rescaling Left_Hippocampus from 57 --> 53
rescaling Left_Amygdala from 56 --> 57
rescaling CSF from 32 -->  8
rescaling Left_Accumbens_area from 62 --> 59
rescaling Left_VentralDC from 87 --> 89
rescaling Right_Cerebral_White_Matter from 105 --> 108
rescaling Right_Cerebral_Cortex from 58 --> 55
rescaling Right_Lateral_Ventricle from 13 -->  3
rescaling Right_Inf_Lat_Vent from 25 --> 21
rescaling Right_Cerebellum_White_Matter from 87 --> 82
rescaling Right_Cerebellum_Cortex from 59 --> 49
rescaling Right_Thalamus_Proper from 85 --> 90
rescaling Right_Caudate from 62 --> 71
rescaling Right_Putamen from 80 --> 78
rescaling Right_Pallidum from 97 --> 93
rescaling Right_Hippocampus from 53 --> 51
rescaling Right_Amygdala from 55 --> 62
rescaling Right_Accumbens_area from 65 --> 69
rescaling Right_VentralDC from 86 --> 94
rescaling Fifth_Ventricle from 40 -->  8
rescaling WM_hypointensities from 78 --> 81
rescaling non_WM_hypointensities from 40 --> 45
  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17  18  19 
 20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36  37  38  39 
 40  41  42  43  44  45  46  47  48  49  50  51  52  53  54  55  56  57  58  59 
 60  61  62  63  64  65  66  67  68  69  70  71  72  73  74  75  76  77  78  79 
 80  81  82  83  84  85  86  87  88  89  90  91  92  93  94  95  96  97  98  99 
100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 
120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 
140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 
160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 
180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 
200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 
220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 
240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 nctx = 517406
Used brute-force search on 0 voxels
relabeling unlikely voxels in interior of white matter
average std[0] = 7.3
pass 1: 135 changed.
pass 2: 3 changed.
pass 3: 0 changed.
nchanged = 0
Writing output aseg to mri/aparc.DKTatlas+aseg.mgz
#-----------------------------------------
#@# APas-to-ASeg Wed Mar 27 18:12:44 CET 2019
/Users/elizavetalavrova/bert/mri
\n apas2aseg --i aparc+aseg.mgz --o aseg.mgz \n
Wed Mar 27 18:12:44 CET 2019

setenv SUBJECTS_DIR /Users/elizavetalavrova
cd /Users/elizavetalavrova/bert/mri
/Applications/freesurfer/bin/apas2aseg --i aparc+aseg.mgz --o aseg.mgz

freesurfer-Darwin-OSX-stable-pub-v6.0.0-2beb96c
$Id: FreeSurferEnv.csh,v 1.89 2016/06/09 14:54:31 zkaufman Exp $
Darwin MacBook-Pro-Elizaveta.local 18.2.0 Darwin Kernel Version 18.2.0: Thu Dec 20 20:46:53 PST 2018; root:xnu-4903.241.1~1/RELEASE_X86_64 x86_64
mri_binarize --i aparc+aseg.mgz --o aseg.mgz --replace 1000 3 --replace 2000 42 --replace 1001 3 --replace 2001 42 --replace 1002 3 --replace 2002 42 --replace 1003 3 --replace 2003 42 --replace 1004 3 --replace 2004 42 --replace 1005 3 --replace 2005 42 --replace 1006 3 --replace 2006 42 --replace 1007 3 --replace 2007 42 --replace 1008 3 --replace 2008 42 --replace 1009 3 --replace 2009 42 --replace 1010 3 --replace 2010 42 --replace 1011 3 --replace 2011 42 --replace 1012 3 --replace 2012 42 --replace 1013 3 --replace 2013 42 --replace 1014 3 --replace 2014 42 --replace 1015 3 --replace 2015 42 --replace 1016 3 --replace 2016 42 --replace 1017 3 --replace 2017 42 --replace 1018 3 --replace 2018 42 --replace 1019 3 --replace 2019 42 --replace 1020 3 --replace 2020 42 --replace 1021 3 --replace 2021 42 --replace 1022 3 --replace 2022 42 --replace 1023 3 --replace 2023 42 --replace 1024 3 --replace 2024 42 --replace 1025 3 --replace 2025 42 --replace 1026 3 --replace 2026 42 --replace 1027 3 --replace 2027 42 --replace 1028 3 --replace 2028 42 --replace 1029 3 --replace 2029 42 --replace 1030 3 --replace 2030 42 --replace 1031 3 --replace 2031 42 --replace 1032 3 --replace 2032 42 --replace 1033 3 --replace 2033 42 --replace 1034 3 --replace 2034 42 --replace 1035 3 --replace 2035 42

$Id: mri_binarize.c,v 1.43 2016/06/09 20:46:21 greve Exp $
cwd /Users/elizavetalavrova/bert/mri
cmdline mri_binarize.bin --i aparc+aseg.mgz --o aseg.mgz --replace 1000 3 --replace 2000 42 --replace 1001 3 --replace 2001 42 --replace 1002 3 --replace 2002 42 --replace 1003 3 --replace 2003 42 --replace 1004 3 --replace 2004 42 --replace 1005 3 --replace 2005 42 --replace 1006 3 --replace 2006 42 --replace 1007 3 --replace 2007 42 --replace 1008 3 --replace 2008 42 --replace 1009 3 --replace 2009 42 --replace 1010 3 --replace 2010 42 --replace 1011 3 --replace 2011 42 --replace 1012 3 --replace 2012 42 --replace 1013 3 --replace 2013 42 --replace 1014 3 --replace 2014 42 --replace 1015 3 --replace 2015 42 --replace 1016 3 --replace 2016 42 --replace 1017 3 --replace 2017 42 --replace 1018 3 --replace 2018 42 --replace 1019 3 --replace 2019 42 --replace 1020 3 --replace 2020 42 --replace 1021 3 --replace 2021 42 --replace 1022 3 --replace 2022 42 --replace 1023 3 --replace 2023 42 --replace 1024 3 --replace 2024 42 --replace 1025 3 --replace 2025 42 --replace 1026 3 --replace 2026 42 --replace 1027 3 --replace 2027 42 --replace 1028 3 --replace 2028 42 --replace 1029 3 --replace 2029 42 --replace 1030 3 --replace 2030 42 --replace 1031 3 --replace 2031 42 --replace 1032 3 --replace 2032 42 --replace 1033 3 --replace 2033 42 --replace 1034 3 --replace 2034 42 --replace 1035 3 --replace 2035 42 
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64
user     elizavetalavrova

input      aparc+aseg.mgz
frame      0
nErode3d   0
nErode2d   0
output     aseg.mgz
Binarizing based on threshold
min        -infinity
max        +infinity
binval        1
binvalnot     0
fstart = 0, fend = 0, nframes = 1
Replacing 72
 1:  1000    3
 2:  2000   42
 3:  1001    3
 4:  2001   42
 5:  1002    3
 6:  2002   42
 7:  1003    3
 8:  2003   42
 9:  1004    3
10:  2004   42
11:  1005    3
12:  2005   42
13:  1006    3
14:  2006   42
15:  1007    3
16:  2007   42
17:  1008    3
18:  2008   42
19:  1009    3
20:  2009   42
21:  1010    3
22:  2010   42
23:  1011    3
24:  2011   42
25:  1012    3
26:  2012   42
27:  1013    3
28:  2013   42
29:  1014    3
30:  2014   42
31:  1015    3
32:  2015   42
33:  1016    3
34:  2016   42
35:  1017    3
36:  2017   42
37:  1018    3
38:  2018   42
39:  1019    3
40:  2019   42
41:  1020    3
42:  2020   42
43:  1021    3
44:  2021   42
45:  1022    3
46:  2022   42
47:  1023    3
48:  2023   42
49:  1024    3
50:  2024   42
51:  1025    3
52:  2025   42
53:  1026    3
54:  2026   42
55:  1027    3
56:  2027   42
57:  1028    3
58:  2028   42
59:  1029    3
60:  2029   42
61:  1030    3
62:  2030   42
63:  1031    3
64:  2031   42
65:  1032    3
66:  2032   42
67:  1033    3
68:  2033   42
69:  1034    3
70:  2034   42
71:  1035    3
72:  2035   42
Found 0 values in range
Counting number of voxels in first frame
Found 0 voxels in final mask
Count: 0 0.000000 16777216 0.000000
mri_binarize done
 
Started at Wed Mar 27 18:12:44 CET 2019 
Ended   at Wed Mar 27 18:12:49 CET 2019
Apas2aseg-Run-Time-Sec 5
 
apas2aseg Done
#--------------------------------------------
#@# ASeg Stats Wed Mar 27 18:12:49 CET 2019
/Users/elizavetalavrova/bert
\n mri_segstats --seg mri/aseg.mgz --sum stats/aseg.stats --pv mri/norm.mgz --empty --brainmask mri/brainmask.mgz --brain-vol-from-seg --excludeid 0 --excl-ctxgmwm --supratent --subcortgray --in mri/norm.mgz --in-intensity-name norm --in-intensity-units MR --etiv --surf-wm-vol --surf-ctx-vol --totalgray --euler --ctab /Applications/freesurfer/ASegStatsLUT.txt --subject bert \n

$Id: mri_segstats.c,v 1.121 2016/05/31 17:27:11 greve Exp $
cwd 
cmdline mri_segstats --seg mri/aseg.mgz --sum stats/aseg.stats --pv mri/norm.mgz --empty --brainmask mri/brainmask.mgz --brain-vol-from-seg --excludeid 0 --excl-ctxgmwm --supratent --subcortgray --in mri/norm.mgz --in-intensity-name norm --in-intensity-units MR --etiv --surf-wm-vol --surf-ctx-vol --totalgray --euler --ctab /Applications/freesurfer/ASegStatsLUT.txt --subject bert 
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64
user     elizavetalavrova
UseRobust  0
atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
Computing euler number
orig.nofix lheno = -120, rheno = -126
orig.nofix lhholes =   61, rhholes = 64
Loading mri/aseg.mgz
Getting Brain Volume Statistics
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
Loading mri/norm.mgz
Loading mri/norm.mgz
Voxel Volume is 1 mm^3
Generating list of segmentation ids
Found  50 segmentations
Computing statistics for each segmentation

Reporting on  45 segmentations
Using PrintSegStat
mri_segstats done
#-----------------------------------------
#@# WMParc Wed Mar 27 18:15:53 CET 2019
/Users/elizavetalavrova/bert
\n mri_aparc2aseg --s bert --labelwm --hypo-as-wm --rip-unknown --volmask --o mri/wmparc.mgz --ctxseg aparc+aseg.mgz \n
SUBJECTS_DIR /Users/elizavetalavrova
subject bert
outvol mri/wmparc.mgz
useribbon 0
baseoffset 0
labeling wm
labeling hypo-intensities as wm
dmaxctx 5.000000
RipUnknown 1
CtxSeg /Users/elizavetalavrova/bert/mri/aparc+aseg.mgz

Reading lh white surface 
 /Users/elizavetalavrova/bert/surf/lh.white

Reading lh pial surface 
 /Users/elizavetalavrova/bert/surf/lh.pial

Loading lh annotations from /Users/elizavetalavrova/bert/label/lh.aparc.annot
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)

Reading rh white surface 
 /Users/elizavetalavrova/bert/surf/rh.white

Reading rh pial surface 
 /Users/elizavetalavrova/bert/surf/rh.pial

Loading rh annotations from /Users/elizavetalavrova/bert/label/rh.aparc.annot
reading colortable from annotation file...
colortable with 36 entries read (originally /autofs/space/tanha_002/users/greve/fsdev.build/average/colortable_desikan_killiany.txt)
Have color table for lh white annotation
Have color table for rh white annotation
Loading ribbon segmentation from /Users/elizavetalavrova/bert/mri/ribbon.mgz
Loading filled from /Users/elizavetalavrova/bert/mri/ribbon.mgz
Ripping vertices labeled as unkown
Ripped 8680 vertices from left hemi
Ripped 8235 vertices from right hemi

Building hash of lh white

Building hash of lh pial

Building hash of rh white

Building hash of rh pial

Loading aseg from /Users/elizavetalavrova/bert/mri/aseg.mgz
Loading Ctx Seg File /Users/elizavetalavrova/bert/mri/aparc+aseg.mgz
ASeg Vox2RAS: -----------
-1.00000   0.00000   0.00000   128.00000;
 0.00000   0.00000   1.00000  -128.00000;
 0.00000  -1.00000   0.00000   128.00000;
 0.00000   0.00000   0.00000   1.00000;
-------------------------

Labeling Slice
  0   1   2   3   4   5   6   7   8   9  10  11  12  13  14  15  16  17  18  19 
 20  21  22  23  24  25  26  27  28  29  30  31  32  33  34  35  36  37  38  39 
 40  41  42  43  44  45  46  47  48  49  50  51  52  53  54  55  56  57  58  59 
 60  61  62  63  64  65  66  67  68  69  70  71  72  73  74  75  76  77  78  79 
 80  81  82  83  84  85  86  87  88  89  90  91  92  93  94  95  96  97  98  99 
100 101 102 103 104 105 106 107 108 109 110 111 112 113 114 115 116 117 118 119 
120 121 122 123 124 125 126 127 128 129 130 131 132 133 134 135 136 137 138 139 
140 141 142 143 144 145 146 147 148 149 150 151 152 153 154 155 156 157 158 159 
160 161 162 163 164 165 166 167 168 169 170 171 172 173 174 175 176 177 178 179 
180 181 182 183 184 185 186 187 188 189 190 191 192 193 194 195 196 197 198 199 
200 201 202 203 204 205 206 207 208 209 210 211 212 213 214 215 216 217 218 219 
220 221 222 223 224 225 226 227 228 229 230 231 232 233 234 235 236 237 238 239 
240 241 242 243 244 245 246 247 248 249 250 251 252 253 254 255 nctx = 1032275
Used brute-force search on 1339 voxels
Fixing Parahip LH WM
  Found 11 clusters
     0 k 1481.000000
     1 k 1.000000
     2 k 1.000000
     3 k 1.000000
     4 k 2.000000
     5 k 3.000000
     6 k 24.000000
     7 k 2.000000
     8 k 1.000000
     9 k 3.000000
     10 k 1.000000
Fixing Parahip RH WM
  Found 8 clusters
     0 k 1.000000
     1 k 1.000000
     2 k 4.000000
     3 k 1.000000
     4 k 1.000000
     5 k 1639.000000
     6 k 2.000000
     7 k 21.000000
Writing output aseg to mri/wmparc.mgz
\n mri_segstats --seg mri/wmparc.mgz --sum stats/wmparc.stats --pv mri/norm.mgz --excludeid 0 --brainmask mri/brainmask.mgz --in mri/norm.mgz --in-intensity-name norm --in-intensity-units MR --subject bert --surf-wm-vol --ctab /Applications/freesurfer/WMParcStatsLUT.txt --etiv \n

$Id: mri_segstats.c,v 1.121 2016/05/31 17:27:11 greve Exp $
cwd 
cmdline mri_segstats --seg mri/wmparc.mgz --sum stats/wmparc.stats --pv mri/norm.mgz --excludeid 0 --brainmask mri/brainmask.mgz --in mri/norm.mgz --in-intensity-name norm --in-intensity-units MR --subject bert --surf-wm-vol --ctab /Applications/freesurfer/WMParcStatsLUT.txt --etiv 
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64
user     elizavetalavrova
UseRobust  0
atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
Loading mri/wmparc.mgz
Getting Brain Volume Statistics
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
Loading mri/norm.mgz
Loading mri/norm.mgz
Voxel Volume is 1 mm^3
Generating list of segmentation ids
Found 390 segmentations
Computing statistics for each segmentation

Reporting on  70 segmentations
Using PrintSegStat
mri_segstats done
/Users/elizavetalavrova/bert/label
INFO: fsaverage subject does not exist in SUBJECTS_DIR
INFO: Creating symlink to fsaverage subject...
\n cd /Users/elizavetalavrova; ln -s /Applications/freesurfer/subjects/fsaverage; cd - \n
#--------------------------------------------
#@# BA_exvivo Labels lh Wed Mar 27 18:26:17 CET 2019
\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA1_exvivo.label --trgsubject bert --trglabel ./lh.BA1_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA1_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA1_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 4129 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  4129 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 490
Checking for and removing duplicates
Writing label file ./lh.BA1_exvivo.label 4619
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA2_exvivo.label --trgsubject bert --trglabel ./lh.BA2_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA2_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA2_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 7909 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  7909 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 757
Checking for and removing duplicates
Writing label file ./lh.BA2_exvivo.label 8666
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA3a_exvivo.label --trgsubject bert --trglabel ./lh.BA3a_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA3a_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA3a_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 4077 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  4077 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 381
Checking for and removing duplicates
Writing label file ./lh.BA3a_exvivo.label 4458
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA3b_exvivo.label --trgsubject bert --trglabel ./lh.BA3b_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA3b_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA3b_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 5983 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  5983 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 604
Checking for and removing duplicates
Writing label file ./lh.BA3b_exvivo.label 6587
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA4a_exvivo.label --trgsubject bert --trglabel ./lh.BA4a_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA4a_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA4a_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 5784 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  5784 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 1053
Checking for and removing duplicates
Writing label file ./lh.BA4a_exvivo.label 6837
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA4p_exvivo.label --trgsubject bert --trglabel ./lh.BA4p_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA4p_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA4p_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 4070 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  4070 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 701
Checking for and removing duplicates
Writing label file ./lh.BA4p_exvivo.label 4771
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA6_exvivo.label --trgsubject bert --trglabel ./lh.BA6_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA6_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA6_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 13589 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  13589 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 2525
Checking for and removing duplicates
Writing label file ./lh.BA6_exvivo.label 16114
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA44_exvivo.label --trgsubject bert --trglabel ./lh.BA44_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA44_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA44_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 4181 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  4181 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 467
Checking for and removing duplicates
Writing label file ./lh.BA44_exvivo.label 4648
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA45_exvivo.label --trgsubject bert --trglabel ./lh.BA45_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA45_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA45_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 3422 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  3422 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 720
Checking for and removing duplicates
Writing label file ./lh.BA45_exvivo.label 4142
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.V1_exvivo.label --trgsubject bert --trglabel ./lh.V1_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.V1_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.V1_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 4641 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  4641 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 1931
Checking for and removing duplicates
Writing label file ./lh.V1_exvivo.label 6572
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.V2_exvivo.label --trgsubject bert --trglabel ./lh.V2_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.V2_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.V2_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 8114 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  8114 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 3794
Checking for and removing duplicates
Writing label file ./lh.V2_exvivo.label 11908
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.MT_exvivo.label --trgsubject bert --trglabel ./lh.MT_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.MT_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.MT_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 2018 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  2018 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 460
Checking for and removing duplicates
Writing label file ./lh.MT_exvivo.label 2478
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.entorhinal_exvivo.label --trgsubject bert --trglabel ./lh.entorhinal_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.entorhinal_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.entorhinal_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1290 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1290 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 110
Checking for and removing duplicates
Writing label file ./lh.entorhinal_exvivo.label 1400
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.perirhinal_exvivo.label --trgsubject bert --trglabel ./lh.perirhinal_exvivo.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.perirhinal_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.perirhinal_exvivo.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1199 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1199 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 110
Checking for and removing duplicates
Writing label file ./lh.perirhinal_exvivo.label 1309
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA1_exvivo.thresh.label --trgsubject bert --trglabel ./lh.BA1_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA1_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA1_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1014 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1014 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 131
Checking for and removing duplicates
Writing label file ./lh.BA1_exvivo.thresh.label 1145
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA2_exvivo.thresh.label --trgsubject bert --trglabel ./lh.BA2_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA2_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA2_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 2092 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  2092 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 285
Checking for and removing duplicates
Writing label file ./lh.BA2_exvivo.thresh.label 2377
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA3a_exvivo.thresh.label --trgsubject bert --trglabel ./lh.BA3a_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA3a_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA3a_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1504 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1504 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 96
Checking for and removing duplicates
Writing label file ./lh.BA3a_exvivo.thresh.label 1600
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA3b_exvivo.thresh.label --trgsubject bert --trglabel ./lh.BA3b_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA3b_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA3b_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1996 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1996 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 249
Checking for and removing duplicates
Writing label file ./lh.BA3b_exvivo.thresh.label 2245
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA4a_exvivo.thresh.label --trgsubject bert --trglabel ./lh.BA4a_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA4a_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA4a_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 2319 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  2319 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 530
Checking for and removing duplicates
Writing label file ./lh.BA4a_exvivo.thresh.label 2849
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA4p_exvivo.thresh.label --trgsubject bert --trglabel ./lh.BA4p_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA4p_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA4p_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1549 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1549 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 223
Checking for and removing duplicates
Writing label file ./lh.BA4p_exvivo.thresh.label 1772
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA6_exvivo.thresh.label --trgsubject bert --trglabel ./lh.BA6_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA6_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA6_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 7035 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  7035 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 1130
Checking for and removing duplicates
Writing label file ./lh.BA6_exvivo.thresh.label 8165
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA44_exvivo.thresh.label --trgsubject bert --trglabel ./lh.BA44_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA44_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA44_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1912 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1912 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 284
Checking for and removing duplicates
Writing label file ./lh.BA44_exvivo.thresh.label 2196
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.BA45_exvivo.thresh.label --trgsubject bert --trglabel ./lh.BA45_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.BA45_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.BA45_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1151 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1151 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 188
Checking for and removing duplicates
Writing label file ./lh.BA45_exvivo.thresh.label 1339
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.V1_exvivo.thresh.label --trgsubject bert --trglabel ./lh.V1_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.V1_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.V1_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 3405 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  3405 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 1395
Checking for and removing duplicates
Writing label file ./lh.V1_exvivo.thresh.label 4800
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.V2_exvivo.thresh.label --trgsubject bert --trglabel ./lh.V2_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.V2_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.V2_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 3334 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  3334 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 1792
Checking for and removing duplicates
Writing label file ./lh.V2_exvivo.thresh.label 5126
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.MT_exvivo.thresh.label --trgsubject bert --trglabel ./lh.MT_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.MT_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.MT_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 513 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  513 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 133
Checking for and removing duplicates
Writing label file ./lh.MT_exvivo.thresh.label 646
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.entorhinal_exvivo.thresh.label --trgsubject bert --trglabel ./lh.entorhinal_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.entorhinal_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.entorhinal_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 470 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  470 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 20
Checking for and removing duplicates
Writing label file ./lh.entorhinal_exvivo.thresh.label 490
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/lh.perirhinal_exvivo.thresh.label --trgsubject bert --trglabel ./lh.perirhinal_exvivo.thresh.label --hemi lh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/lh.perirhinal_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./lh.perirhinal_exvivo.thresh.label
regmethod = surface

srchemi = lh
trghemi = lh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 450 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/lh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/lh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  450 nlabel points
Performing mapping from target back to the source label 151159
Number of reverse mapping hits = 48
Checking for and removing duplicates
Writing label file ./lh.perirhinal_exvivo.thresh.label 498
mri_label2label: Done

\n mris_label2annot --s bert --hemi lh --ctab /Applications/freesurfer/average/colortable_BA.txt --l lh.BA1_exvivo.label --l lh.BA2_exvivo.label --l lh.BA3a_exvivo.label --l lh.BA3b_exvivo.label --l lh.BA4a_exvivo.label --l lh.BA4p_exvivo.label --l lh.BA6_exvivo.label --l lh.BA44_exvivo.label --l lh.BA45_exvivo.label --l lh.V1_exvivo.label --l lh.V2_exvivo.label --l lh.MT_exvivo.label --l lh.entorhinal_exvivo.label --l lh.perirhinal_exvivo.label --a BA_exvivo --maxstatwinner --noverbose \n
Reading ctab /Applications/freesurfer/average/colortable_BA.txt
Number of ctab entries 15

$Id: mris_label2annot.c,v 1.20 2016/01/07 23:28:11 greve Exp $
cwd /Users/elizavetalavrova/bert/label
cmdline mris_label2annot --s bert --hemi lh --ctab /Applications/freesurfer/average/colortable_BA.txt --l lh.BA1_exvivo.label --l lh.BA2_exvivo.label --l lh.BA3a_exvivo.label --l lh.BA3b_exvivo.label --l lh.BA4a_exvivo.label --l lh.BA4p_exvivo.label --l lh.BA6_exvivo.label --l lh.BA44_exvivo.label --l lh.BA45_exvivo.label --l lh.V1_exvivo.label --l lh.V2_exvivo.label --l lh.MT_exvivo.label --l lh.entorhinal_exvivo.label --l lh.perirhinal_exvivo.label --a BA_exvivo --maxstatwinner --noverbose 
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64
user     elizavetalavrova

subject bert
hemi    lh
SUBJECTS_DIR /Users/elizavetalavrova
ColorTable /Applications/freesurfer/average/colortable_BA.txt
AnnotName  BA_exvivo
nlables 14
LabelThresh 0 0.000000
Loading /Users/elizavetalavrova/bert/surf/lh.orig
 1 1530880 BA1_exvivo
 2 16749699 BA2_exvivo
 3 16711680 BA3a_exvivo
 4 3368703 BA3b_exvivo
 5 1376196 BA4a_exvivo
 6 13382655 BA4p_exvivo
 7 10036737 BA6_exvivo
 8 2490521 BA44_exvivo
 9 39283 BA45_exvivo
10 3993 V1_exvivo
11 8508928 V2_exvivo
12 10027163 MT_exvivo
13 16422433 perirhinal_exvivo
14 16392598 entorhinal_exvivo
Mapping unhit to unknown
Found 103528 unhit vertices
Writing annot to /Users/elizavetalavrova/bert/label/lh.BA_exvivo.annot
\n mris_label2annot --s bert --hemi lh --ctab /Applications/freesurfer/average/colortable_BA.txt --l lh.BA1_exvivo.thresh.label --l lh.BA2_exvivo.thresh.label --l lh.BA3a_exvivo.thresh.label --l lh.BA3b_exvivo.thresh.label --l lh.BA4a_exvivo.thresh.label --l lh.BA4p_exvivo.thresh.label --l lh.BA6_exvivo.thresh.label --l lh.BA44_exvivo.thresh.label --l lh.BA45_exvivo.thresh.label --l lh.V1_exvivo.thresh.label --l lh.V2_exvivo.thresh.label --l lh.MT_exvivo.thresh.label --l lh.entorhinal_exvivo.thresh.label --l lh.perirhinal_exvivo.thresh.label --a BA_exvivo.thresh --maxstatwinner --noverbose \n
Reading ctab /Applications/freesurfer/average/colortable_BA.txt
Number of ctab entries 15

$Id: mris_label2annot.c,v 1.20 2016/01/07 23:28:11 greve Exp $
cwd /Users/elizavetalavrova/bert/label
cmdline mris_label2annot --s bert --hemi lh --ctab /Applications/freesurfer/average/colortable_BA.txt --l lh.BA1_exvivo.thresh.label --l lh.BA2_exvivo.thresh.label --l lh.BA3a_exvivo.thresh.label --l lh.BA3b_exvivo.thresh.label --l lh.BA4a_exvivo.thresh.label --l lh.BA4p_exvivo.thresh.label --l lh.BA6_exvivo.thresh.label --l lh.BA44_exvivo.thresh.label --l lh.BA45_exvivo.thresh.label --l lh.V1_exvivo.thresh.label --l lh.V2_exvivo.thresh.label --l lh.MT_exvivo.thresh.label --l lh.entorhinal_exvivo.thresh.label --l lh.perirhinal_exvivo.thresh.label --a BA_exvivo.thresh --maxstatwinner --noverbose 
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64
user     elizavetalavrova

subject bert
hemi    lh
SUBJECTS_DIR /Users/elizavetalavrova
ColorTable /Applications/freesurfer/average/colortable_BA.txt
AnnotName  BA_exvivo.thresh
nlables 14
LabelThresh 0 0.000000
Loading /Users/elizavetalavrova/bert/surf/lh.orig
 1 1530880 BA1_exvivo
 2 16749699 BA2_exvivo
 3 16711680 BA3a_exvivo
 4 3368703 BA3b_exvivo
 5 1376196 BA4a_exvivo
 6 13382655 BA4p_exvivo
 7 10036737 BA6_exvivo
 8 2490521 BA44_exvivo
 9 39283 BA45_exvivo
10 3993 V1_exvivo
11 8508928 V2_exvivo
12 10027163 MT_exvivo
13 16422433 perirhinal_exvivo
14 16392598 entorhinal_exvivo
Mapping unhit to unknown
Found 122392 unhit vertices
Writing annot to /Users/elizavetalavrova/bert/label/lh.BA_exvivo.thresh.annot
\n mris_anatomical_stats -th3 -mgz -f ../stats/lh.BA_exvivo.stats -b -a ./lh.BA_exvivo.annot -c ./BA_exvivo.ctab bert lh white \n
computing statistics for each annotation in ./lh.BA_exvivo.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/lh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/lh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/lh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
Using TH3 vertex volume calc
Total face volume 263342
Total vertex volume 258917 (mask=0)
reading colortable from annotation file...
colortable with 15 entries read (originally /Applications/freesurfer/average/colortable_BA.txt)
Saving annotation colortable ./BA_exvivo.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 1277    775   2168  2.234 0.527     0.143     0.058       27     2.4  BA1_exvivo
 4369   2878   6840  2.217 0.482     0.117     0.027       43     4.7  BA2_exvivo
 1265    893   1253  1.801 0.391     0.140     0.036       12     1.9  BA3a_exvivo
 2803   1848   4040  1.985 0.607     0.127     0.036       34     4.0  BA3b_exvivo
 2258   1299   3234  2.273 0.592     0.132     0.056       38     4.9  BA4a_exvivo
 1796   1168   2489  2.305 0.519     0.130     0.042       15     3.7  BA4p_exvivo
11550   7636  22713  2.523 0.579     0.128     0.042      133    19.6  BA6_exvivo
 2522   1695   5111  2.567 0.519     0.124     0.030       28     3.1  BA44_exvivo
 2919   1969   5697  2.499 0.520     0.125     0.032       38     3.5  BA45_exvivo
 4092   2594   4492  1.695 0.465     0.147     0.051       63     8.1  V1_exvivo
 9387   6086  13072  1.994 0.486     0.148     0.046      146    16.4  V2_exvivo
 2130   1452   3632  2.399 0.439     0.146     0.035       30     3.0  MT_exvivo
  553    399   1733  3.303 0.775     0.128     0.043        7     1.2  perirhinal_exvivo
  710    523   1929  3.231 0.841     0.141     0.037        9     1.0  entorhinal_exvivo
\n mris_anatomical_stats -th3 -mgz -f ../stats/lh.BA_exvivo.thresh.stats -b -a ./lh.BA_exvivo.thresh.annot -c ./BA_exvivo.thresh.ctab bert lh white \n
computing statistics for each annotation in ./lh.BA_exvivo.thresh.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/lh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/lh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/lh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
Using TH3 vertex volume calc
Total face volume 263342
Total vertex volume 258917 (mask=0)
reading colortable from annotation file...
colortable with 15 entries read (originally /Applications/freesurfer/average/colortable_BA.txt)
Saving annotation colortable ./BA_exvivo.thresh.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
  828    476   1395  2.176 0.509     0.138     0.068       21     1.6  BA1_exvivo
 1861   1227   2952  2.236 0.503     0.117     0.029       19     2.1  BA2_exvivo
 1066    751    979  1.710 0.307     0.139     0.036       10     1.6  BA3a_exvivo
 1781   1166   2045  1.711 0.405     0.120     0.033       17     2.6  BA3b_exvivo
 2277   1302   3203  2.287 0.580     0.128     0.055       34     5.1  BA4a_exvivo
 1399    939   1865  2.200 0.475     0.133     0.041       13     2.8  BA4p_exvivo
 6373   4126  12080  2.473 0.578     0.129     0.049       81    12.5  BA6_exvivo
 1730   1140   3412  2.528 0.523     0.136     0.035       24     2.6  BA44_exvivo
 1093    729   2350  2.589 0.475     0.125     0.036       14     1.3  BA45_exvivo
 4300   2750   4772  1.701 0.466     0.148     0.051       67     8.6  V1_exvivo
 4827   3063   6230  1.885 0.434     0.154     0.050       82     9.4  V2_exvivo
  583    399   1108  2.517 0.439     0.159     0.036       11     0.9  MT_exvivo
  270    204    937  3.392 0.641     0.101     0.015        1     0.2  perirhinal_exvivo
  379    277   1013  3.269 0.818     0.139     0.035        5     0.5  entorhinal_exvivo
#--------------------------------------------
#@# BA_exvivo Labels rh Wed Mar 27 18:31:01 CET 2019
\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA1_exvivo.label --trgsubject bert --trglabel ./rh.BA1_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA1_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA1_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 3962 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  3962 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 379
Checking for and removing duplicates
Writing label file ./rh.BA1_exvivo.label 4341
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA2_exvivo.label --trgsubject bert --trglabel ./rh.BA2_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA2_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA2_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 6687 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  6687 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 445
Checking for and removing duplicates
Writing label file ./rh.BA2_exvivo.label 7132
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA3a_exvivo.label --trgsubject bert --trglabel ./rh.BA3a_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA3a_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA3a_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 3980 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  3980 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 261
Checking for and removing duplicates
Writing label file ./rh.BA3a_exvivo.label 4241
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA3b_exvivo.label --trgsubject bert --trglabel ./rh.BA3b_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA3b_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA3b_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 4522 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  4522 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 436
Checking for and removing duplicates
Writing label file ./rh.BA3b_exvivo.label 4958
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA4a_exvivo.label --trgsubject bert --trglabel ./rh.BA4a_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA4a_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA4a_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 5747 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  5747 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 929
Checking for and removing duplicates
Writing label file ./rh.BA4a_exvivo.label 6676
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA4p_exvivo.label --trgsubject bert --trglabel ./rh.BA4p_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA4p_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA4p_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 4473 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  4473 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 613
Checking for and removing duplicates
Writing label file ./rh.BA4p_exvivo.label 5086
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA6_exvivo.label --trgsubject bert --trglabel ./rh.BA6_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA6_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA6_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 12256 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  12256 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 2033
Checking for and removing duplicates
Writing label file ./rh.BA6_exvivo.label 14289
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA44_exvivo.label --trgsubject bert --trglabel ./rh.BA44_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA44_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA44_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 6912 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  6912 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 1555
Checking for and removing duplicates
Writing label file ./rh.BA44_exvivo.label 8467
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA45_exvivo.label --trgsubject bert --trglabel ./rh.BA45_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA45_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA45_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 5355 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  5355 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 1180
Checking for and removing duplicates
Writing label file ./rh.BA45_exvivo.label 6535
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.V1_exvivo.label --trgsubject bert --trglabel ./rh.V1_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.V1_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.V1_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 4727 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  4727 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 2018
Checking for and removing duplicates
Writing label file ./rh.V1_exvivo.label 6745
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.V2_exvivo.label --trgsubject bert --trglabel ./rh.V2_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.V2_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.V2_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 8016 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  8016 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 3577
Checking for and removing duplicates
Writing label file ./rh.V2_exvivo.label 11593
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.MT_exvivo.label --trgsubject bert --trglabel ./rh.MT_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.MT_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.MT_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1932 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1932 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 836
Checking for and removing duplicates
Writing label file ./rh.MT_exvivo.label 2768
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.entorhinal_exvivo.label --trgsubject bert --trglabel ./rh.entorhinal_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.entorhinal_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.entorhinal_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1038 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1038 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 127
Checking for and removing duplicates
Writing label file ./rh.entorhinal_exvivo.label 1165
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.perirhinal_exvivo.label --trgsubject bert --trglabel ./rh.perirhinal_exvivo.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.perirhinal_exvivo.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.perirhinal_exvivo.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 752 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  752 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 102
Checking for and removing duplicates
Writing label file ./rh.perirhinal_exvivo.label 854
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA1_exvivo.thresh.label --trgsubject bert --trglabel ./rh.BA1_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA1_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA1_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 876 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  876 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 137
Checking for and removing duplicates
Writing label file ./rh.BA1_exvivo.thresh.label 1013
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA2_exvivo.thresh.label --trgsubject bert --trglabel ./rh.BA2_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA2_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA2_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 2688 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  2688 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 133
Checking for and removing duplicates
Writing label file ./rh.BA2_exvivo.thresh.label 2821
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA3a_exvivo.thresh.label --trgsubject bert --trglabel ./rh.BA3a_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA3a_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA3a_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1698 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1698 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 83
Checking for and removing duplicates
Writing label file ./rh.BA3a_exvivo.thresh.label 1781
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA3b_exvivo.thresh.label --trgsubject bert --trglabel ./rh.BA3b_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA3b_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA3b_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 2183 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  2183 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 201
Checking for and removing duplicates
Writing label file ./rh.BA3b_exvivo.thresh.label 2384
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA4a_exvivo.thresh.label --trgsubject bert --trglabel ./rh.BA4a_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA4a_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA4a_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1388 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1388 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 154
Checking for and removing duplicates
Writing label file ./rh.BA4a_exvivo.thresh.label 1542
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA4p_exvivo.thresh.label --trgsubject bert --trglabel ./rh.BA4p_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA4p_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA4p_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1489 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1489 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 257
Checking for and removing duplicates
Writing label file ./rh.BA4p_exvivo.thresh.label 1746
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA6_exvivo.thresh.label --trgsubject bert --trglabel ./rh.BA6_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA6_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA6_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 6959 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  6959 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 1098
Checking for and removing duplicates
Writing label file ./rh.BA6_exvivo.thresh.label 8057
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA44_exvivo.thresh.label --trgsubject bert --trglabel ./rh.BA44_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA44_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA44_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1012 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1012 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 167
Checking for and removing duplicates
Writing label file ./rh.BA44_exvivo.thresh.label 1179
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.BA45_exvivo.thresh.label --trgsubject bert --trglabel ./rh.BA45_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.BA45_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.BA45_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 1178 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  1178 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 226
Checking for and removing duplicates
Writing label file ./rh.BA45_exvivo.thresh.label 1404
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.V1_exvivo.thresh.label --trgsubject bert --trglabel ./rh.V1_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.V1_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.V1_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 3232 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  3232 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 1333
Checking for and removing duplicates
Writing label file ./rh.V1_exvivo.thresh.label 4565
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.V2_exvivo.thresh.label --trgsubject bert --trglabel ./rh.V2_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.V2_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.V2_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 3437 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  3437 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 1710
Checking for and removing duplicates
Writing label file ./rh.V2_exvivo.thresh.label 5147
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.MT_exvivo.thresh.label --trgsubject bert --trglabel ./rh.MT_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.MT_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.MT_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 268 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  268 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 79
Checking for and removing duplicates
Writing label file ./rh.MT_exvivo.thresh.label 347
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.entorhinal_exvivo.thresh.label --trgsubject bert --trglabel ./rh.entorhinal_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.entorhinal_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.entorhinal_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 694 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  694 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 85
Checking for and removing duplicates
Writing label file ./rh.entorhinal_exvivo.thresh.label 779
mri_label2label: Done

\n mri_label2label --srcsubject fsaverage --srclabel /Users/elizavetalavrova/fsaverage/label/rh.perirhinal_exvivo.thresh.label --trgsubject bert --trglabel ./rh.perirhinal_exvivo.thresh.label --hemi rh --regmethod surface \n

srclabel = /Users/elizavetalavrova/fsaverage/label/rh.perirhinal_exvivo.thresh.label
srcsubject = fsaverage
trgsubject = bert
trglabel = ./rh.perirhinal_exvivo.thresh.label
regmethod = surface

srchemi = rh
trghemi = rh
trgsurface = white
srcsurfreg = sphere.reg
trgsurfreg = sphere.reg
usehash = 1
Use ProjAbs  = 0, 0
Use ProjFrac = 0, 0
DoPaint 0

SUBJECTS_DIR    /Users/elizavetalavrova
FREESURFER_HOME /Applications/freesurfer
Loading source label.
Found 291 points in source label.
Starting surface-based mapping
Reading source registration 
 /Users/elizavetalavrova/fsaverage/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Reading target surface 
 /Users/elizavetalavrova/bert/surf/rh.white
Reading target registration 
 /Users/elizavetalavrova/bert/surf/rh.sphere.reg
Rescaling ...  original radius = 100
Building target registration hash (res=16).
Building source registration hash (res=16).
INFO: found  291 nlabel points
Performing mapping from target back to the source label 150852
Number of reverse mapping hits = 54
Checking for and removing duplicates
Writing label file ./rh.perirhinal_exvivo.thresh.label 345
mri_label2label: Done

\n mris_label2annot --s bert --hemi rh --ctab /Applications/freesurfer/average/colortable_BA.txt --l rh.BA1_exvivo.label --l rh.BA2_exvivo.label --l rh.BA3a_exvivo.label --l rh.BA3b_exvivo.label --l rh.BA4a_exvivo.label --l rh.BA4p_exvivo.label --l rh.BA6_exvivo.label --l rh.BA44_exvivo.label --l rh.BA45_exvivo.label --l rh.V1_exvivo.label --l rh.V2_exvivo.label --l rh.MT_exvivo.label --l rh.entorhinal_exvivo.label --l rh.perirhinal_exvivo.label --a BA_exvivo --maxstatwinner --noverbose \n
Reading ctab /Applications/freesurfer/average/colortable_BA.txt
Number of ctab entries 15

$Id: mris_label2annot.c,v 1.20 2016/01/07 23:28:11 greve Exp $
cwd /Users/elizavetalavrova/bert/label
cmdline mris_label2annot --s bert --hemi rh --ctab /Applications/freesurfer/average/colortable_BA.txt --l rh.BA1_exvivo.label --l rh.BA2_exvivo.label --l rh.BA3a_exvivo.label --l rh.BA3b_exvivo.label --l rh.BA4a_exvivo.label --l rh.BA4p_exvivo.label --l rh.BA6_exvivo.label --l rh.BA44_exvivo.label --l rh.BA45_exvivo.label --l rh.V1_exvivo.label --l rh.V2_exvivo.label --l rh.MT_exvivo.label --l rh.entorhinal_exvivo.label --l rh.perirhinal_exvivo.label --a BA_exvivo --maxstatwinner --noverbose 
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64
user     elizavetalavrova

subject bert
hemi    rh
SUBJECTS_DIR /Users/elizavetalavrova
ColorTable /Applications/freesurfer/average/colortable_BA.txt
AnnotName  BA_exvivo
nlables 14
LabelThresh 0 0.000000
Loading /Users/elizavetalavrova/bert/surf/rh.orig
 1 1530880 BA1_exvivo
 2 16749699 BA2_exvivo
 3 16711680 BA3a_exvivo
 4 3368703 BA3b_exvivo
 5 1376196 BA4a_exvivo
 6 13382655 BA4p_exvivo
 7 10036737 BA6_exvivo
 8 2490521 BA44_exvivo
 9 39283 BA45_exvivo
10 3993 V1_exvivo
11 8508928 V2_exvivo
12 10027163 MT_exvivo
13 16422433 perirhinal_exvivo
14 16392598 entorhinal_exvivo
Mapping unhit to unknown
Found 103832 unhit vertices
Writing annot to /Users/elizavetalavrova/bert/label/rh.BA_exvivo.annot
\n mris_label2annot --s bert --hemi rh --ctab /Applications/freesurfer/average/colortable_BA.txt --l rh.BA1_exvivo.thresh.label --l rh.BA2_exvivo.thresh.label --l rh.BA3a_exvivo.thresh.label --l rh.BA3b_exvivo.thresh.label --l rh.BA4a_exvivo.thresh.label --l rh.BA4p_exvivo.thresh.label --l rh.BA6_exvivo.thresh.label --l rh.BA44_exvivo.thresh.label --l rh.BA45_exvivo.thresh.label --l rh.V1_exvivo.thresh.label --l rh.V2_exvivo.thresh.label --l rh.MT_exvivo.thresh.label --l rh.entorhinal_exvivo.thresh.label --l rh.perirhinal_exvivo.thresh.label --a BA_exvivo.thresh --maxstatwinner --noverbose \n
Reading ctab /Applications/freesurfer/average/colortable_BA.txt
Number of ctab entries 15

$Id: mris_label2annot.c,v 1.20 2016/01/07 23:28:11 greve Exp $
cwd /Users/elizavetalavrova/bert/label
cmdline mris_label2annot --s bert --hemi rh --ctab /Applications/freesurfer/average/colortable_BA.txt --l rh.BA1_exvivo.thresh.label --l rh.BA2_exvivo.thresh.label --l rh.BA3a_exvivo.thresh.label --l rh.BA3b_exvivo.thresh.label --l rh.BA4a_exvivo.thresh.label --l rh.BA4p_exvivo.thresh.label --l rh.BA6_exvivo.thresh.label --l rh.BA44_exvivo.thresh.label --l rh.BA45_exvivo.thresh.label --l rh.V1_exvivo.thresh.label --l rh.V2_exvivo.thresh.label --l rh.MT_exvivo.thresh.label --l rh.entorhinal_exvivo.thresh.label --l rh.perirhinal_exvivo.thresh.label --a BA_exvivo.thresh --maxstatwinner --noverbose 
sysname  Darwin
hostname MacBook-Pro-Elizaveta.local
machine  x86_64
user     elizavetalavrova

subject bert
hemi    rh
SUBJECTS_DIR /Users/elizavetalavrova
ColorTable /Applications/freesurfer/average/colortable_BA.txt
AnnotName  BA_exvivo.thresh
nlables 14
LabelThresh 0 0.000000
Loading /Users/elizavetalavrova/bert/surf/rh.orig
 1 1530880 BA1_exvivo
 2 16749699 BA2_exvivo
 3 16711680 BA3a_exvivo
 4 3368703 BA3b_exvivo
 5 1376196 BA4a_exvivo
 6 13382655 BA4p_exvivo
 7 10036737 BA6_exvivo
 8 2490521 BA44_exvivo
 9 39283 BA45_exvivo
10 3993 V1_exvivo
11 8508928 V2_exvivo
12 10027163 MT_exvivo
13 16422433 perirhinal_exvivo
14 16392598 entorhinal_exvivo
Mapping unhit to unknown
Found 124742 unhit vertices
Writing annot to /Users/elizavetalavrova/bert/label/rh.BA_exvivo.thresh.annot
\n mris_anatomical_stats -th3 -mgz -f ../stats/rh.BA_exvivo.stats -b -a ./rh.BA_exvivo.annot -c ./BA_exvivo.ctab bert rh white \n
computing statistics for each annotation in ./rh.BA_exvivo.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/rh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/rh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/rh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
Using TH3 vertex volume calc
Total face volume 266424
Total vertex volume 262392 (mask=0)
reading colortable from annotation file...
colortable with 15 entries read (originally /Applications/freesurfer/average/colortable_BA.txt)
Saving annotation colortable ./BA_exvivo.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
 1083    626   1916  2.178 0.575     0.145     0.051       22     2.1  BA1_exvivo
 3311   2234   4458  2.020 0.434     0.109     0.027       27     3.5  BA2_exvivo
 1186    797   1067  1.725 0.381     0.126     0.034        9     1.6  BA3a_exvivo
 2126   1420   2741  1.762 0.597     0.129     0.035       24     3.0  BA3b_exvivo
 1771   1014   2637  2.298 0.530     0.138     0.076       31     6.1  BA4a_exvivo
 1578    957   2006  2.259 0.491     0.127     0.051       19     3.6  BA4p_exvivo
 9697   6394  18178  2.493 0.596     0.131     0.043      114    16.6  BA6_exvivo
 4547   3064   8767  2.617 0.517     0.131     0.037       62     7.1  BA44_exvivo
 4751   3188   8931  2.482 0.548     0.130     0.033       56     6.4  BA45_exvivo
 4373   2929   5298  1.696 0.572     0.150     0.051       63     9.4  V1_exvivo
 8980   5999  13298  2.042 0.563     0.150     0.046      137    15.8  V2_exvivo
 2604   1792   4734  2.339 0.489     0.145     0.041       42     4.0  MT_exvivo
  598    453   2010  3.197 0.731     0.119     0.024        5     0.6  perirhinal_exvivo
  415    303   1016  2.847 0.620     0.124     0.028        4     0.5  entorhinal_exvivo
\n mris_anatomical_stats -th3 -mgz -f ../stats/rh.BA_exvivo.thresh.stats -b -a ./rh.BA_exvivo.thresh.annot -c ./BA_exvivo.thresh.ctab bert rh white \n
computing statistics for each annotation in ./rh.BA_exvivo.thresh.annot.
reading volume /Users/elizavetalavrova/bert/mri/wm.mgz...
reading input surface /Users/elizavetalavrova/bert/surf/rh.white...
reading input pial surface /Users/elizavetalavrova/bert/surf/rh.pial...
reading input white surface /Users/elizavetalavrova/bert/surf/rh.white...
INFO: using TH3 volume calc
INFO: assuming MGZ format for volumes.
Using TH3 vertex volume calc
Total face volume 266424
Total vertex volume 262392 (mask=0)
reading colortable from annotation file...
colortable with 15 entries read (originally /Applications/freesurfer/average/colortable_BA.txt)
Saving annotation colortable ./BA_exvivo.thresh.ctab

table columns are:
    number of vertices
    total surface area (mm^2)
    total gray matter volume (mm^3)
    average cortical thickness +- standard deviation (mm)
    integrated rectified mean curvature
    integrated rectified Gaussian curvature
    folding index
    intrinsic curvature index
    structure name

atlas_icv (eTIV) = 1631367 mm^3    (det: 1.194155 )
lhCtxGM: 259065.217 258138.000  diff=  927.2  pctdiff= 0.358
rhCtxGM: 261828.273 261029.000  diff=  799.3  pctdiff= 0.305
lhCtxWM: 256199.096 256428.000  diff= -228.9  pctdiff=-0.089
rhCtxWM: 259627.352 260482.000  diff= -854.6  pctdiff=-0.329
SubCortGMVol  63866.000
SupraTentVol  1115279.938 (1112347.000) diff=2932.938 pctdiff=0.263
SupraTentVolNotVent  1102968.938 (1100036.000) diff=2932.938 pctdiff=0.266
BrainSegVol  1248005.000 (1246238.000) diff=1767.000 pctdiff=0.142
BrainSegVolNotVent  1233232.000 (1233723.938) diff=-491.938 pctdiff=-0.040
BrainSegVolNotVent  1233232.000
CerebellumVol 133045.000
VentChorVol   12311.000
3rd4th5thCSF   2462.000
CSFVol   695.000, OptChiasmVol   151.000
MaskVol 1658944.000
  775    466   1242  1.970 0.555     0.146     0.053       14     1.5  BA1_exvivo
 1848   1249   2621  1.960 0.450     0.105     0.027       18     2.1  BA2_exvivo
 1068    713    897  1.722 0.368     0.129     0.036        9     1.5  BA3a_exvivo
 1715   1170   1870  1.599 0.409     0.120     0.030       15     2.1  BA3b_exvivo
  987    562   1483  2.278 0.569     0.142     0.094       20     4.0  BA4a_exvivo
 1353    835   1687  2.222 0.506     0.127     0.051       15     3.0  BA4p_exvivo
 6296   4097  11334  2.433 0.577     0.133     0.046       82    11.6  BA6_exvivo
  969    677   1949  2.568 0.454     0.142     0.040       16     1.3  BA44_exvivo
 1206    811   2711  2.789 0.464     0.147     0.042       19     1.9  BA45_exvivo
 4152   2776   4903  1.688 0.569     0.149     0.051       60     8.8  V1_exvivo
 4777   3255   6618  1.886 0.563     0.159     0.050       78     9.1  V2_exvivo
  324    227    611  2.356 0.421     0.143     0.044        5     0.5  MT_exvivo
  348    259   1161  3.250 0.733     0.101     0.016        2     0.2  perirhinal_exvivo
  292    215    649  2.926 0.618     0.146     0.032        4     0.4  entorhinal_exvivo

Started at Thu Mar 21 15:53:22 CET 2019 
Ended   at Wed Mar 27 18:35:40 CET 2019
#@#%# recon-all-run-time-hours 146.705
recon-all -s bert finished without error at Wed Mar 27 18:35:40 CET 2019
done
mbp-elizaveta:~ elizavetalavrova$  
