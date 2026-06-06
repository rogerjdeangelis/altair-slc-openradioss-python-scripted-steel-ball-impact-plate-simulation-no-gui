# altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui
Altair slc openradioss python scripted steel ball impact plate simulation no gui
    %let pgm=altair-slc-openradioss-python-scripted-steel-ball-plate-impact-simulation-no-gui;

    %stop_submission;

    Altair slc openradioss python scripted steel ball impact plate simulation no gui

    A complete self-contained reproducible example is presented that is entirely scripted, no
    GUI or mouse surfing requeried. The entire simulation is done without ALtair Radioss subscription..

    Openradioss simulation (if using win 11 media player, click on 1x and select the slowest playback)

    https://drive.google.com/file/d/1WPIAfCyEMrpQbkAldZMA9SITVYZ0AYSW/view?usp=sharing
    also downloadable from this repository, rubber_animation.mp4

    Too long to post here see github
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui

    SOURCE
    https://openradioss.atlassian.net/wiki/spaces/OPENRADIOSS/pages/67796993/Sol2SPH+Ball+-+Plate+Impact

    There are only two files you need to run this simulation. (in repo)
          Impact_0000.rad
          Impact_0001.rad

    5th   Frame https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/frame_0005.png
    15th  Frame https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/frame_0015.png
    25th  Frame https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/frame_0025.png
    35th  Frame https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/frame_0035.png
    45th  Frame https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/frame_0045.png

    Key csv tables (also slc tables)
                                       Bytes
      c:/rad/impactT01.csv            8,654 KB
      c:/rad/global_energy_data.csv      12 KB
      c:/rad/cell_data.csv           69,404 KB (not in repo - too large)

      CONTENTS

       1 Preparation
       2 Get github inputs
       3 Get animation & time history
       4 Time history table
       5 Many plots
          energy_evolution.png
          globalOverallForce.png
          timestephistory.png
          ElasticContactEnergy.png
          PlateZmom.png
          RotationEnergy.png
          StressComponentDistribution.png
          VonMisesStress.png
          xmomentumevolve.png
          ymomentumevolve.png
          zmomentumevolve.png
          ContactEnergy.png
          ContactForceEvolution.png
          DisplacementEvolution.png
          FrictionalContactEnergy.png
          HourGlassEnergy.png
       6 Animation to vtk file
       7 Vtk to vkthdf
       8 vkthdf to csv
       9 vkthdf slc tables
      10 vtkhdf plots
      11 Vtkhdf to mp4

                    Simulating the deformation of a plate when impacted by a solid ball
                                 Energies are within the plate

                             Plot of INTERNALENERGY*TIME.  Symbol used is 'i'
                             Plot of PLASTICWORK*TIME.     Symbol used is 'p'
                             Plot of INTERNALENERGY*TIME   Symbol used is 'i'


                                                    TIME
                   0.0000       0.0001       0.0002       0.0003       0.0004       0.0005
          Internal ---+------------+------------+------------+------------+------------+------- Kinetic
            Energy |                       |                                                  | Energy
                   | Plate Deformation Energies                                               |
            900000 +                       |              Internal Energy                     + 5020000
                   |                       |   iiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiii      |
                   | kk Ball Touches Plate |  ii  Kinetic Energy is converted to Internal     |
                   |  kk                   |ii,                                               |
                   |   kk                  ii                                                 |
            800000 +     k                 i                                                  + 5000000
                   |     kk Plate Deforms i|                                                  |
                   |      kk              i|                                                  |
                   |       kk            i |<-Maximum Plate Deformatiom before cracks?        |
                   |        k            i |                                                  |
            700000 +kinetic kk          i  |                                                  + 4900000
                   |energy-> kk         i  |                                                  |
                   |          k         i pp                                                  |
                   |          kk       i  pppppp           Plastic Work                       |
                   |           k       i pp|ppppppppppppppppppppppppppppppppppppppppppppp     | 4800000
            600000 +           kk     ii p |                                                  +
                   |            k     i pp |                                                  |
                   |             k    i p  |                                                  |
                   |             k   i  p  |                                                  |
                   |              k  i p   |                                                  |
            500000 +              k ii p   |<- 0.00015                                        + 4700000
                   |               ki pp   |                                                  |
                   |               ki p    |                                                  |
                   |               ik p    |<-Maximum Plate Deformatiom before cracks?        |
                   |               ikp     |                                                  |
            400000 +              iikp     |                                                  + 4600000
                   |              i pp     |                                                  |
                   |             ii pkk    |                                                  |
                   |             i pp k    |                                                  |
                   |             i p  kk   |                                                  |
            300000 +            i pp   k   |                                                  + 4500000
                   |            i p    k   |                                                  |
                   |           i pp     k  |                                                  |
                   |  Internal i p      kk |                                                  |
                   |          i pp       k |                                                  |
            200000 +          i p        kk|                                                  + 4400000
                   |         iipp         k|                                                  |
                   |  Energy i p           |k                                                 |
                   |        i pp           |kk                                                |
                   |       ii p            | kkk                                              |
            100000 +       i p             |   kkk                                            + 4300000
                   |      i pp             |    kk                                            |
                   |     iipp              |      kk                                          |
                   |    iipp Plastic Work  |        kk                                        |
                   |   iipp                |          kk  Kinetic Energy                      |
                 0 +  iip                  |            kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkk     + 4200000
                   |                       |                                                  |
                   ---+------------+------------+------------+------------+------------+-------
                   0.0000       0.0001       0.0002       0.0003       0.0004       0.0005
                                                           TIME

                             Ball Impact  Sress Distributions (PALTE)

                                X = _3DELEM_STRS_INTG_POINT111__0
                                Y = _3DELEM_STRS_INTG_POINT111__1
                                Z = _3DELEM_STRS_INTG_POINT111__2

                         Frequency              Frequency                Frequency

                     6000 12000 18000       6000 12000 18000         6000 12000 18000
                ------+-----+-----+--- ------+-----+-----+------------+-----+-----+-----
           -500 |                      |                        |                      | -500
           -475 |    STRESS X          |     STRESS Y           |     STRESS Z         | -475
           -450 |                      |                        |                      | -450
           -425 |*                     |                        |                      | -425
           -400 |*                     |                        |                      | -400
           -375 |*                     |                        |                      | -375
           -350 |**                    |                        |                      | -350
           -325 |**                    |                        |                      | -325
           -300 |**                    |                        |                      | -300
           -275 |**                    |                        |                      | -275
           -250 |**                    |*                       |                      | -250
           -225 |**                    |*                       |                      | -225
           -200 |**                    |*                       |*                     | -200
           -175 |**                    |**                      |*                     | -175
           -150 |**                    |***                     |**                    | -150
           -125 |**                    |***                     |**                    | -125
           -100 |**                    |****                    |***                   | -100
            -75 |**                    |******                  |*****                 |  -75
            -50 |*                     |*******                 |*******               |  -50
            -25 |**                    |*********               |**************        |  -25
              0 |***                   |**************          |******************    |    0
             25 |***                   |***********             |*************         |   25
             50 |***                   |********                |*******               |   50
             75 |***                   |******                  |****                  |   75
            100 |***                   |****                    |***                   |  100
            125 |***                   |***                     |**                    |  125
            150 |****                  |***                     |**                    |  150
            175 |****                  |**                      |*                     |  175
            200 |*****                 |*                       |*                     |  200
            225 |******                |*                       |*                     |  225
            250 |******                |*                       |                      |  250
            275 |*****                 |                        |                      |  275
            300 |***                   |                        |                      |  300
            325 |***                   |                        |                      |  325
            350 |**                    |                        |                      |  350
            375 |*                     |                        |                      |  375
            400 |*                     |                        |                      |  400
            425 |*                     |                        |                      |  425
            450 |*                     |                        |                      |  450
            475 |*                     |                        |                      |  475
            500 |*                     |                        |                      |  500
            525 |*                     |                        |                      |  525
            550 |                      |                        |                      |  550
            575 |                      |                        |                      |  575
            600 |                      |                        |                      |  600
                ------+-----+-----+----------+-----+-----+------------+-----+-----+-----
                     6000 12000 18000       6000 12000 18000         6000 12000 18000

                     Frequency              Frequency                Frequency

                                      D3ELEM_VON_MISES                        Cum.
            Midpoint                                                 Freq  Percent
                      |
                600   |*                                              106     0.12
                590   |***                                            206     0.36
                580   |***                                            261     0.66
                570   |****                                           295     1.00
                560   |*****                                          397     1.45
                550   |******                                         450     1.97
                540   |********                                       606     2.66
                530   |***********                                    820     3.61
                520   |****************                              1179     4.96
                510   |***********************                       1697     6.91
                500   |**************************                    1935     9.13
                490   |*************************                     1894    11.31
                480   |*****************************                 2211    13.84
                470   |*************************************         2797    17.06
                460   |*****************************************     3089    20.60
                450   |********************************************  3276    24.36
                440   |*************************************         2772    27.55
                430   |*********************************             2471    30.38
                420   |************************                      1822    32.48
                410   |**********************                        1680    34.40
                400   |************************                      1793    36.46
                390   |***************************                   2035    38.80
                380   |*****************************                 2178    41.30
                370   |*********************************             2451    44.12
                360   |*******************************               2355    46.82
                350   |**********************************            2547    49.74
                340   |*********************************             2503    52.62
                330   |*********************************             2455    55.44
                320   |********************************              2385    58.18
                310   |*******************************               2311    60.83
                300   |********************************              2377    63.56
                290   |*******************************               2351    66.26
                280   |********************************              2411    69.03
                270   |*********************************             2466    71.86
                260   |*******************************               2354    74.56
                250   |********************************              2410    77.33
                240   |******************************                2234    79.89
                230   |***************************                   2057    82.25
                220   |**************************                    1952    84.50
                210   |*************************                     1844    86.61
                200   |************************                      1815    88.70
                190   |************************                      1795    90.76
                180   |***********************                       1753    92.77
                170   |********************                          1468    94.46
                160   |***************                               1105    95.73
                150   |************                                   918    96.78
                140   |***********                                    799    97.70
                130   |*********                                      688    98.49
                120   |********                                       616    99.19
                110   |*******                                        490    99.76
                100   |***                                            212   100.00
                      |
                       --------+-------+-------+-------+-------+----
                              600     1200    1800    2400    3000

                                         Frequency




    Expected Behavior                                Your Distribution             Status

    sxx has widest range (impact direction)           -500 to +500 MPa            Correct
    syy has narrower range (lateral)                  -200 to +200 MPa            Correct
    szz has narrowest (through-thickness)             -100 to +200 MPa            Correct
    Zero stress peak present                                       Yes            Correct
    Asymmetric distribution(tension^-compression)                  Yes            Correct
    No extreme outliers                              Values within ±500 MPa       Correct



    PLOTS

    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/energy_evolution.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/globalOverallForce.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/timestephistory.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/ElasticContactEnergy.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/PlateZmom.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/StressComponentDistribution.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/VonMisesStress.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/xmomentumevolve.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/ymomentumevolve.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/zmomentumevolve.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/ContactEnergy.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/ContactForceEvolution.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/DisplacementEvolution.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/FrictionalContactEnergy.png
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/blob/main/HourGlassEnergy.png


    For macros see
      https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    Related Repos
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-rubber-ring-simulation-no-gui
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-bumper-beam-simulation-no-gui
    https://github.com/rogerjdeangelis/altair-slc-openradioss-python-script-for-cell-phone-drop-simulation-no-gui
    https://github.com/rogerjdeangelis/utl-altair-slc-enhanced-openradioss-tensile-strength-simulation-python-no-gui-no-mouse-surfing
    https://github.com/rogerjdeangelis/utl-altair-slc-python-script-to-run-openradioss-tensile-strength-simulation
    https://github.com/rogerjdeangelis/utl-altair-slc-post-processing-radioss-files-using-openradioss
    https://github.com/rogerjdeangelis/utl-personal-altair-slc-with-matlab-sympy-and-r-finite-element-cold-plate-heat-transfer

    /*
     _                                        _   _
    / |  _ __  _ __ ___ _ __   __ _ _ __ __ _| |_(_) ___  _ __
    | | | `_ \| `__/ _ \ `_ \ / _` | `__/ _` | __| |/ _ \| `_ \
    | | | |_) | | |  __/ |_) | (_| | | | (_| | |_| | (_) | | | |
    |_| | .__/|_|  \___| .__/ \__,_|_|  \__,_|\__|_|\___/|_| |_|
        |_|            |_|
    */

    libname workx "d:/wpswrkx";

    MOST OF THE INSTALLS ARE ONLY NEEDED FOR THE ANIMATION, YOU MAY NOT NEED STEPS III-V IF
    YOU ARE NOT INTERESTED DIN THE ANIMATION. INTEL API IS NEEDED FOR CUSTOMIZATION OF PENRADIOSS
    OR PARALLEL PROCESSING?
    There are many python tools you can easily add to the script below for graphics and summary tables.


    I INSTALL OPENRADIOSS
    ---------------------

     a  Go to https://github.com/OpenRadioss/OpenRadioss/releases
     b  Download openradioss_win64.zip
     c  Create directory c:/openradioss
     d  From the unzipped file copy all folders, see below, to c:/openradioss
        The result should look like

        c:/openradioss (should look like)

          <DIR>   exec
          <DIR>   extlib
          <DIR>   hm_cfg_files
          <DIR>   licenses
          <DIR>   openradioss_gui


    II  INSTALL INTEL OPENAPI TOOLKIT YOU NEED TO INSTALL VERSION 2 FROM THE ARCHIVES
    -----------------------------------------------------------------------------

     a  https://www.intel.com/content/www/us/en/developer/articles/tool/oneapi-archive.html
     b  It automaticall installs at C:/Program Files (x86)/Intel/oneapi


    III INSTALL VISUAL STUDIO
    -------------------------

     a  https://visualstudio.microsoft.com/vs/community/
     b  C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools


    IV  INSTALL FFMPEG
    ------------------

     a  https://www.gyan.dev/ffmpeg/builds/
     b  C:\Program Files\ffmpeg
     c  esential version
     d  unzip and save to c:/program files


    V   INSTALL PARAVIEW
    --------------------

     a  https://www.paraview.org/download/
     b  It will install at C:\Program Files\ParaView-6.1.0-Windows-Python3.12-msvc2017-AMD64


    VI  Download SLC macros and place in your autocall library for instance c:/wpsoto (also in this repo)
    -----------------------------------------------------------------------------------------------------
     a  https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories
     b  utlfkil
     d  slc_pvbegin  /*-- runs a virtual python ---*/
     e  slc_pvend
     f  slc_psbegin  /*--- runs powershell      ---*/
     g  slc_psend



    VII YOU NEED TO PUT THIS IN YOUR AUTOEXEC
    -----------------------------------------

      a libname workx "d:/wpswrkx";
      b or set in betewen each section below
        (many many sections. I suggest you put it in your autoexec ---*/


    /*---
     ____              _          _ _   _           _      _                   _
    |___ \   __ _  ___| |_   __ _(_) |_| |__  _   _| |__  (_)_ __  _ __  _   _| |_ ___
      __) | / _` |/ _ \ __| / _` | | __| `_ \| | | | `_ \ | | `_ \| `_ \| | | | __/ __|
     / __/ | (_| |  __/ |_ | (_| | | |_| | | | |_| | |_) || | | | | |_) | |_| | |_\__ \
    |_____| \__, |\___|\__| \__, |_|\__|_| |_|\__,_|_.__/ |_|_| |_| .__/ \__,_|\__|___/
            |___/           |___/                                 |_|

    You do not need to run this. You can manually  create d:/rad and download the rad files from this repp

    What powershell is doing ( you can do the following manually)

      1 deletes d:/rad directory if it exists
      2 recreate empty d:/rad
      3 copy files from github
        Impact_0000.rad
        Impact_0001.rad
    ---*/

    /*--- START HERE ---*/
    /*--- START HERE ---*/

    /*--- clear workx data ---*/
    libname workx sas7bdat "d:/wpswrkx";  /*--- put in autoexec                                                      ---*/
    libname wpdx wpd "d:/wpswrkx";        /*--- wpd datasets run faster than sas7bdats                               ---*/
                                          /*--- also wpd datasets work much better with sas procs that modify tables ---*/
    proc datasets lib=workx kill;
    run;

    proc datasets lib=wpdx kill;
    run;

    %slc_psbegin; /*--- call powershell ---*/
    cards4;
    # Deletes d:/rad and all subdirectories/files, recreates the folder, then
    # downloads the three OpenRadioss input files from your GitHub repository.

    $targetDir = "D:\rad"

    # 1. Remove the directory and everything inside it (forcefully, recursively)
    if (Test-Path $targetDir) {
        Write-Host "Removing existing directory: $targetDir" -ForegroundColor Yellow
        Remove-Item -Path $targetDir -Recurse -Force
    }


    # 2. Recreate the empty directory
    Write-Host "Creating fresh directory: $targetDir" -ForegroundColor Yellow
    New-Item -Path $targetDir -ItemType Directory -Force | Out-Null

    # 3. Define the source files (GitHub raw URLs) and their destination names
    $files = @(
        @{
            Source = "https://raw.githubusercontent.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/refs/heads/main/Impact_0000.rad"
            Dest   = "d:\rad\Impact_0000.rad"
        },
        @{
            Source = "https://raw.githubusercontent.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/refs/heads/main/Impact_0001.rad"
            Dest   = "d:\rad\Impact_0001.rad"
        }
    )

    # 4. Download each file using Invoke-WebRequest
    Write-Host "Downloading files to $targetDir ..." -ForegroundColor Yellow
    foreach ($file in $files) {
        try {
            Write-Host "  Downloading: $($file.Source)" -ForegroundColor Cyan
            Invoke-WebRequest -Uri $file.Source -OutFile $file.Dest
            Write-Host "    Saved to: $($file.Dest)" -ForegroundColor Green
        }
        catch {
            Write-Host "    ERROR: Failed to download $($file.Source)" -ForegroundColor Red
            Write-Host "    Exception: $($_.Exception.Message)" -ForegroundColor Red
        }
    }

    # 5. Optional: List the contents of D:\rad to verify
    Write-Host "`nContents of $targetDir :" -ForegroundColor Yellow
    Get-ChildItem -Path $targetDir | Format-Table Name, Length -AutoSize

    Write-Host "`nScript completed." -ForegroundColor Green
    ;;;;
    %slc_psend;


    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /*  Altair SLC                                                                                                            */
    /* Removing existing directory: D:\rad                                                                                    */
    /*                                                                                                                        */
    /* Creating fresh directory: D:\rad                                                                                       */
    /* Downloading files to D:\rad ...                                                                                        */
    /*                                                                                                                        */
    /*   Downloading: https://raw.githubusercontent.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel          */
    /*     -ball-impact-plate-simulation-no-gui/refs/heads/main/Impact_0000.rad                                               */
    /*     Saved to: d:\rad\Impact_0000.rad                                                                                   */
    /*                                                                                                                        */
    /*   Downloading: https://raw.githubusercontent.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel          */
    /*     -ball-impact-plate-simulation-no-gui/refs/heads/main/Impact_0001.rad                                               */
    /*     Saved to: d:\rad\Impact_0001.rad                                                                                   */
    /*                                                                                                                        */
    /* Contents of D:\rad :                                                                                                   */
    /*                                                                                                                        */
    /* Name            Length                                                                                                 */
    /* ----            ------                                                                                                 */
    /* Impact_0000.rad 432964                                                                                                 */
    /* Impact_0001.rad    646                                                                                                 */
    /*                                                                                                                        */
    /* Script completed.                                                                                                      */
    /*                                                                                                                        */
    /*------------------------------------------------------------------------------------------------------------------------*/
    /*                                                                                                                        */
    /* d:/rad/Impact_0001.rad                                                                                                 */
    /*                                                                                                                        */
    /*  #                                                                                                                     */
    /*  # Copyright (C) 2023 Altair Engineering Inc. ("Holder")                                                               */
    /*  # Model is licensed by Holder under CC BY-NC 4.0                                                                      */
    /*  # (https://creativecommons.org/licenses/by-nc/4.0/legalcode).                                                         */
    /*  #                                                                                                                     */
    /*  /ANIM/DT                                                                                                              */
    /*  #   TSTART     TFREQ                                                                                                  */
    /*  0.000000 0.000010                                                                                                     */
    /*  /ANIM/MASS                                                                                                            */
    /*  /DT                                                                                                                   */
    /*  0.67 0                                                                                                                */
    /*  /H3D/DT                                                                                                               */
    /*  #   TSTART     TFREQ                                                                                                  */
    /*  0.000000 0.000010                                                                                                     */
    /*  /PRINT/-1000/55                                                                                                       */
    /*  /RFILE                                                                                                                */
    /*  #   NCYCLE                                                                                                            */
    /*  1000000                                                                                                               */
    /*  /RUN/Impact/1                                                                                                         */
    /*                0.0005                                                                                                  */
    /*  /STOP                                                                                                                 */
    /*  # Emax Mmax Nmax NTH NANIM NERR_POSIT                                                                                 */
    /*  0 0 0 1 1 0                                                                                                           */
    /*  /TFILE/4                                                                                                              */
    /*  #            dT_HIS                                                                                                   */
    /*  0.000001                                                                                                              */
    /*  /TITLE                                                                                                                */
    /*  Impact                                                                                                                */
    /*  /ANIM/BRICK/TENS/STRESS/ALL                                                                                           */
    /*  /ANIM/BRICK/VONM                                                                                                      */
    /*  /ANIM/VECT/VEL                                                                                                        */
    /*  /ANIM/VECT/DISP                                                                                                       */
    /*  /ANIM/VECT/ACC                                                                                                        */
    /*  /ANIM/VECT/CONT                                                                                                       */
    /*  /ANIM/NODA/DMAS                                                                                                       */
    /*  /H3D/NODA/VEL                                                                                                         */
    /*                                                                                                                        */
    /*------------------------------------------------------------------------------------------------------------------------*/
    /*                                                                                                                        */
    /* d:/rad/Impact_0001.rad                                                                                                 */
    /*                                                                                                                        */
    /* #RADIOSS STARTER                                                                                                       */
    /* #                                                                                                                      */
    /* # Copyright (C) 2023 Altair Engineering Inc. ("Holder")                                                                */
    /* # Model is licensed by Holder under CC BY-NC 4.0                                                                       */
    /* # (https://creativecommons.org/licenses/by-nc/4.0/legalcode).                                                          */
    /* #---1----|----2----|----3----|----4----|----5----|----6----|----7----|----8----|----9----|---10----|                   */
    /* #                                                                                                                      */
    /* #-                                                                                                                     */
    /* #- DATE      Thu Nov  9 13:49:25 2023                                                                                  */
    /* #--------------------------------------------------------------------------------------------------|                   */
    /* #---1----|----2----|----3----|----4----|----5----|----6----|----7----|----8----|----9----|---10----|                   */
    /* /BEGIN                                                                                                                 */
    /* Impact                                                                                                                 */
    /*       2023         0                                                                                                   */
    /*                   Mg                  mm                   s                                                           */
    /*                   Mg                  mm                   s                                                           */
    /* #---1----|----2----|----3----|----4----|----5----|----6----|----7----|----8----|----9----|---10----|                   */
    /* #-  1. CONTROL CARDS:                                                                                                  */
    /* #---1----|----2----|----3----|----4----|----5----|----6----|----7----|----8----|----9----|---10----|                   */
    /* /TITLE                                                                                                                 */
    /*                                                                                                                        */
    /* #---1----|----2----|----3----|----4----|----5----|----6----|----7----|----8----|----9----|---10----|                   */
    /* #-  2. MATERIALS:                                                                                                      */
    /* #---1----|----2----|----3----|----4----|----5----|----6----|----7----|----8----|----9----|---10----|                   */
    /* /MAT/PLAS_JOHNS/1                                                                                                      */
    /* Alu                                                                                                                    */
    /* #              RHO_I                                                                                                   */
    /*               2.7E-9                   0                                                                               */
    /* #                  E                  Nu     Iflag                                                                     */
    /*                67000                  .3         1                                                                     */
    /* #              SIG_Y                 UTS                EUTS           EPS_p_max            SIG_max0                   */
    /*                  414                 483                 .13                   0                   0                   */
    /* #                  c           EPS_DOT_0       ICC   Fsmooth               F_cut               Chard                   */
    /*                    0                   0         0         0                   0                   0                   */
    /* #                  m              T_melt              rhoC_p                 T_r                                       */
    /*                    0                   0                   0                   0                                       */
    /* /FAIL/TENSSTRAIN/1                                                                                                     */
    /* #                Et1                 Et2  funct_ID                Eps1                Eps2    S-Flag                   */
    /*                   .5                 .51         0                   0                   0         0                   */
    /* #  Fail_Id                                                                                                             */
    /*          2                                                                                                             */
    /**************************************************************************************************************************/


    /*                   _     _
    (_)_ __  _ __  _   _| |_  | | ___   __ _
    | | `_ \| `_ \| | | | __| | |/ _ \ / _` |
    | | | | | |_) | |_| | |_  | | (_) | (_| |
    |_|_| |_| .__/ \__,_|\__| |_|\___/ \__, |
            |_|                        |___/
    */

    1                                          Altair SLC          12:37 Tuesday, June  2, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"

    NOTE: AUTOEXEC processing completed

    1         /*--- clear workx data ---*/
    2         libname workx sas7bdat "d:/wpswrkx";  /*--- put in autoexec                                                      ---*/
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    3         libname wpdx wpd "d:/wpswrkx";        /*--- wpd datasets run faster than sas7bdats                               ---*/
    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx


    Altair SLC

    The DATASETS Procedure

             Directory

    Libref           WORKX
    Engine           SAS7BDAT
    Physical Name    d:\wpswrkx
    4                                               /*--- also wpd datasets work much better with sas procs that modify tables ---*/
    5         proc datasets lib=workx kill;
    NOTE: No matching members in directory
    6         run;
    NOTE: Procedure datasets step took :
          real time : 0.015
          cpu time  : 0.000



    Altair SLC

    The DATASETS Procedure

             Directory

    Libref           WPDX
    Engine           WPD
    Physical Name    d:\wpswrkx
    7
    8         proc datasets lib=wpdx kill;
    NOTE: No matching members in directory
    9         run;
    10
    11        %slc_psbegin; /*--- call powershell ---*/
    NOTE: Procedure datasets step took :
          real time : 0.110
          cpu time  : 0.062


    12        cards4;

    NOTE: The file 'c:\temp\ps_pgm.ps1' is:
          Filename='c:\temp\ps_pgm.ps1',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=14:40:04 Mar 21 2026,
          Last Accessed=12:37:33 Jun 02 2026,
          Last Modified=12:37:33 Jun 02 2026,
          Lrecl=32767, Recfm=V

    NOTE: 47 records were written to file 'c:\temp\ps_pgm.ps1'
          The minimum record length was 80
          The maximum record length was 181
    NOTE: The data step took :
          real time : 0.000
          cpu time  : 0.000


    13        # Deletes d:/rad and all subdirectories/files, recreates the folder, then
    14        # downloads the three OpenRadioss input files from your GitHub repository.
    15
    16        $targetDir = "D:\rad"
    17
    18        # 1. Remove the directory and everything inside it (forcefully, recursively)
    19        if (Test-Path $targetDir) {
    20            Write-Host "Removing existing directory: $targetDir" -ForegroundColor Yellow
    21            Remove-Item -Path $targetDir -Recurse -Force
    22        }
    23
    24
    25        # 2. Recreate the empty directory
    26        Write-Host "Creating fresh directory: $targetDir" -ForegroundColor Yellow
    27        New-Item -Path $targetDir -ItemType Directory -Force | Out-Null
    28
    29        # 3. Define the source files (GitHub raw URLs) and their destination names
    30        $files = @(
    31            @{
    32                Source = "https://raw.githubusercontent.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/refs/heads/main/Impact_0000.rad"
    33                Dest   = "d:\rad\Impact_0000.rad"
    34            },
    35            @{
    36                Source = "https://raw.githubusercontent.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/refs/heads/main/Impact_0001.rad"
    37                Dest   = "d:\rad\Impact_0001.rad"
    38            }
    39        )
    40
    41        # 4. Download each file using Invoke-WebRequest
    42        Write-Host "Downloading files to $targetDir ..." -ForegroundColor Yellow
    43        foreach ($file in $files) {
    44            try {
    45                Write-Host "  Downloading: $($file.Source)" -ForegroundColor Cyan
    46                Invoke-WebRequest -Uri $file.Source -OutFile $file.Dest
    47                Write-Host "    Saved to: $($file.Dest)" -ForegroundColor Green
    48            }
    49            catch {
    50                Write-Host "    ERROR: Failed to download $($file.Source)" -ForegroundColor Red
    51                Write-Host "    Exception: $($_.Exception.Message)" -ForegroundColor Red
    52            }
    53        }
    54
    55        # 5. Optional: List the contents of D:\rad to verify
    56        Write-Host "`nContents of $targetDir :" -ForegroundColor Yellow
    57        Get-ChildItem -Path $targetDir | Format-Table Name, Length -AutoSize
    58
    59        Write-Host "`nScript completed." -ForegroundColor Green
    60        ;;;;
    61        %slc_psend;

    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=powershell.exe -executionpolicy bypass -file c:/temp/ps_pgm.ps1 >  c:/temp/ps_pgm.log,
          Lrecl=32756, Recfm=V

    NOTE: No records were written to file PRINT

    NOTE: No records were read from file rut
    Stderr output:
    Remove-Item : Cannot remove item D:\rad: The process cannot access the file 'D:\rad' because it is being used by
    another process.
    At C:\temp\ps_pgm.ps1:9 char:5
    +     Remove-Item -Path $targetDir -Recurse -Force
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : WriteError: (D:\rad:DirectoryInfo) [Remove-Item], IOException
        + FullyQualifiedErrorId : RemoveFileSystemItemIOError,Microsoft.PowerShell.Commands.RemoveItemCommand
    NOTE: The data step took :
          real time : 2.875
          cpu time  : 0.015



    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=powershell.exe -executionpolicy bypass -file c:/temp/ps_pgm.ps1 >  c:/temp/ps_pgm.log,
          Lrecl=32767, Recfm=V

    NOTE: No records were written to file PRINT

    NOTE: No records were read from file rut
    Stderr output:
    Remove-Item : Cannot remove item D:\rad: The process cannot access the file 'D:\rad' because it is being used by
    another process.
    At C:\temp\ps_pgm.ps1:9 char:5
    +     Remove-Item -Path $targetDir -Recurse -Force
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : WriteError: (D:\rad:DirectoryInfo) [Remove-Item], IOException
        + FullyQualifiedErrorId : RemoveFileSystemItemIOError,Microsoft.PowerShell.Commands.RemoveItemCommand
    NOTE: The data step took :
          real time : 3.353
          cpu time  : 0.015



    NOTE: The infile 'c:\temp\ps_pgm.log' is:
          Filename='c:\temp\ps_pgm.log',
          Owner Name=SLC\suzie,
          File size (bytes)=674,
          Create Time=10:30:46 Mar 22 2026,
          Last Accessed=12:37:39 Jun 02 2026,
          Last Modified=12:37:39 Jun 02 2026,
          Lrecl=32767, Recfm=V

    Removing existing directory: D:\rad
    Creating fresh directory: D:\rad
    Downloading files to D:\rad ...
      Downloading: https://raw.githubusercontent.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/refs/heads/main/Impact_0000.rad
        Saved to: d:\rad\Impact_0000.rad
      Downloading: https://raw.githubusercontent.com/rogerjdeangelis/altair-slc-openradioss-python-scripted-steel-ball-impact-plate-simulation-no-gui/refs/heads/main/Impact_0001.rad
        Saved to: d:\rad\Impact_0001.rad

    Contents of D:\rad :

    Name            Length
    ----            ------
    Impact_0000.rad 432964
    Impact_0001.rad    646



    Script completed.
    NOTE: 18 records were read from file 'c:\temp\ps_pgm.log'
          The minimum record length was 0
          The maximum record length was 177
    NOTE: 18 records were written to file PRINT

    NOTE: The data step took :
          real time : 0.013
          cpu time  : 0.000


    62
    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 6.622
          cpu time  : 0.281


    /*____             _                _                 _   _               ___    _   _                                _
    |___ /   __ _  ___| |_   __ _ _ __ (_)_ __ ___   __ _| |_(_) ___  _ __   ( _ )  | |_(_)_ __ ___   ___   ___  ___ _ __(_) ___  ___
      |_ \  / _` |/ _ \ __| / _` | `_ \| | `_ ` _ \ / _` | __| |/ _ \| `_ \  / _ \/\| __| | `_ ` _ \ / _ \ / __|/ _ \ `__| |/ _ \/ __|
     ___) || (_| |  __/ |_ | (_| | | | | | | | | | | (_| | |_| | (_) | | | || (_>  <| |_| | | | | | |  __/ \__ \  __/ |  | |  __/\__ \
    |____/  \__, |\___|\__| \__,_|_| |_|_|_| |_| |_|\__,_|\__|_|\___/|_| |_| \___/\/ \__|_|_| |_| |_|\___| |___/\___|_|  |_|\___||___/
            |___/
    */

    /*--- CREATE SIEMEN ANIMATION AND TIME HISTORY CSV FILE  ---*/

    options validvarname=v7;
    options set=PYTHONHOME "D:\py314";
    proc python;
    submit;
    import os
    import pandas as pd
    import subprocess
    from pathlib import Path

    # ============================================================================
    # CONFIGURATION
    # ============================================================================

    OPENRADIOSS_PATH = Path("C:/openradioss")
    STARTER_EXE = OPENRADIOSS_PATH / "exec" / "starter_win64.exe"
    ENGINE_EXE = OPENRADIOSS_PATH / "exec" / "engine_win64.exe"
    TH_TO_CSV_EXE = OPENRADIOSS_PATH / "exec" / "th_to_csv_win64.exe"

    MODEL_DIR = Path("D:/rad")
    STARTER_FILE = "Impact_0000.rad"
    ENGINE_FILE =  "Impact_0001.rad"

    # Time history file (output from simulation)
    TH_FILE = MODEL_DIR / "ImpactT01"
    # CSV output file
    CSV_FILE = MODEL_DIR / "results.csv"

    SETVARS_PATH = Path("C:/Program Files (x86)/Intel/oneAPI/setvars.bat")
    OMP_NUM_THREADS = "1"
    KMP_STACKSIZE = "400m"

    # ============================================================================
    # ENVIRONMENT SETUP
    # ============================================================================

    def setup_environment():
        env = os.environ.copy()
        env["OPENRADIOSS_PATH"] = str(OPENRADIOSS_PATH)
        env["RAD_CFG_PATH"] = str(OPENRADIOSS_PATH / "hm_cfg_files")
        env["RAD_H3D_PATH"] = str(OPENRADIOSS_PATH / "extlib" / "h3d" / "lib" / "win64")
        env["OMP_NUM_THREADS"] = OMP_NUM_THREADS
        env["KMP_STACKSIZE"] = KMP_STACKSIZE

        hm_reader = OPENRADIOSS_PATH / "extlib" / "hm_reader" / "win64"
        if hm_reader.exists():
            env["PATH"] = str(hm_reader) + ";" + env.get("PATH", "")

        # Add tools directory to PATH for th_to_csv
        tools_dir = OPENRADIOSS_PATH / "tools"
        if tools_dir.exists():
            env["PATH"] = str(tools_dir) + ";" + env.get("PATH", "")

        return env

    def run_cmd(cmd, cwd, env, log_file):
        """Run command and capture output to log file"""
        with open(log_file, 'w') as f:
            result = subprocess.run(cmd, shell=True, cwd=cwd, env=env,
                                    stdout=f, stderr=subprocess.STDOUT, text=True)
        return result.returncode

    def convert_th_to_csv(th_file, csv_file, env):
        """Convert time history binary file to CSV format"""
        if not th_file.exists():
            print(f"Warning: Time history file not found: {th_file}")
            return False

        if not TH_TO_CSV_EXE.exists():
            print(f"Warning: th_to_csv_win64.exe not found at {TH_TO_CSV_EXE}")
            return False

        print(f"Converting time history: {th_file.name} -> {csv_file.name}")

        # Run th_to_csv and redirect output to CSV file
        cmd = f'"{TH_TO_CSV_EXE}" "{th_file}"'

        try:
            with open(csv_file, 'w') as f:
                result = subprocess.run(cmd, shell=True, cwd=str(MODEL_DIR), env=env,
                                        stdout=f, stderr=subprocess.PIPE, text=True)

            if result.returncode == 0 and csv_file.exists() and csv_file.stat().st_size > 0:
                # Count lines to verify data
                with open(csv_file, 'r') as f:
                    line_count = sum(1 for _ in f)
                print(f"  [OK] Created {csv_file.name} ({line_count} lines, {csv_file.stat().st_size / 1024:.1f} KB)")

                # Show first few lines as preview
                with open(csv_file, 'r') as f:
                    header = f.readline().strip()
                    first_data = f.readline().strip() if line_count > 1 else ""
                print(f"  Header: {header[:100]}...")
                return True
            else:
                print(f"  [FAILED] Conversion failed (exit code {result.returncode})")
                if result.stderr:
                    print(f"    Error: {result.stderr[:200]}")
                return False
        except Exception as e:
            print(f"  [ERROR] {e}")
            return False

    # ============================================================================
    # MAIN EXECUTION
    # ============================================================================

    def main():
        print("=" * 60)
        print("OpenRadioss Rubber Seal Simulation")
        print("=" * 60)

        # Quick verification
        if not STARTER_EXE.exists() or not ENGINE_EXE.exists():
            print("ERROR: OpenRadioss executables not found")
            return 1

        env = setup_environment()
        setvars = f'call "{SETVARS_PATH}" intel64 vs2022 > nul 2>&1 && ' if SETVARS_PATH.exists() else ""

        # Run Starter
        print("\n[1/3] Running Starter...")
        starter_input = MODEL_DIR / STARTER_FILE
        rc = run_cmd(f'{setvars}"{STARTER_EXE}" -i "{starter_input}"',
                      str(MODEL_DIR), env, MODEL_DIR / "starter.log")
        if rc != 0:
            print(f"Starter failed (exit {rc}). Check starter.log")
            return rc

        # Run Engine
        print("[2/3] Running Engine...")
        engine_input = MODEL_DIR / ENGINE_FILE
        rc = run_cmd(f'{setvars}"{ENGINE_EXE}" -i "{engine_input}"',
                      str(MODEL_DIR), env, MODEL_DIR / "engine.log")
        if rc != 0:
            print(f"Engine failed (exit {rc}). Check engine.log")
            return rc

        # List animation files created
        anim_files = list(MODEL_DIR.glob("*.A0*")) + list(MODEL_DIR.glob("*.h3d"))
        if anim_files:
            print(f"\nAnimation files created ({len(anim_files)}):")
            for f in sorted(anim_files):
                size_kb = f.stat().st_size / 1024
                print(f"  {f.name} ({size_kb:.1f} KB)")
        else:
            print("\nWarning: No animation files found")

        # Convert time history to CSV
        print("\n[3/3] Converting time history to CSV...")
        convert_th_to_csv(TH_FILE, CSV_FILE, env)

        # Summary
        print("\n" + "=" * 60)
        print("SIMULATION COMPLETE")
        print("=" * 60)
        print(f"Results saved to: {MODEL_DIR}")
        print(f"  - Time history CSV: {CSV_FILE.name}")
        print(f"  - Starter log: starter.log")
        print(f"  - Engine log: engine.log")
        if anim_files:
            print(f"  - Animation files: {len(anim_files)} files")

        # Verify CSV was created
        if CSV_FILE.exists():
            print(f"\nCSV file size: {CSV_FILE.stat().st_size / 1024:.1f} KB")
            print("You can now open results.csv in Excel or Python for analysis.")

        print("\nDone.")
        return 0

    if __name__ == "__main__":
        exit(main());
    endsubmit;
    run;

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* Altair SLC                                                                                                             */
    /* The PYTHON Procedure                                                                                                   */
    /* =================================================                                                                      */
    /* OpenRadioss Rubber Seal Simulation                                                                                     */
    /* =================================================                                                                      */
    /*                                                                                                                        */
    /* [1/3] Running Starter...                                                                                               */
    /* [2/3] Running Engine...                                                                                                */
    /*                                                                                                                        */
    /* Animation files created (1):                                                                                           */
    /*   Impact.h3d (19781.5 KB)                                                                                              */
    /*                                                                                                                        */
    /* [3/3] Converting time history to CSV...                                                                                */
    /*                                                                                                                        */
    /* Converting time history: ImpactT01 -> results.csv                                                                      */
    /*   [OK] Created results.csv (6 lines, 0.1 KB)                                                                           */
    /*   Header: ...                                                                                                          */
    /*                                                                                                                        */
    /* =================================================                                                                      */
    /* SIMULATION COMPLETE                                                                                                    */
    /* =================================================                                                                      */
    /*                                                                                                                        */
    /* Results saved to: D:\rad                                                                                               */
    /*   - Time history CSV: results.csv                                                                                      */
    /*   - Starter log: starter.log                                                                                           */
    /*   - Engine log: engine.log                                                                                             */
    /*   - Animation files: 1 files                                                                                           */
    /*                                                                                                                        */
    /* CSV file size: 0.1 KB                                                                                                  */
    /* You can now open results.csv in Excel or Python for analysis.                                                          */
    /*                                                                                                                        */
    /* Done.                                                                                                                  */
    /*                                                                                                                        */
    /* -----------------------------------------------------------------------------------------------------------------------*/
    /*                                                                                                                        */
    /*  Volume in drive D is backup2tb                                                                                        */
    /*  Volume Serial Number is D839-A195                                                                                     */
    /*                                                                                                                        */
    /*  Directory of d:\rad                                                                                                   */
    /*                                                                                                                        */
    /*    Impact.h3d             20,256,240                                                                                   */
    /*    ImpactA001              2,280,189                                                                                   */
    /*    ImpactA002              2,280,189                                                                                   */
    /*    ImpactA003              2,280,189                                                                                   */
    /*                                                                                                                        */
    /*    ImpactA049              2,280,189                                                                                   */
    /*    ImpactA050              2,280,189                                                                                   */
    /*    ImpactA051              2,280,189                                                                                   */
    /*                                                                                                                        */
    /*    ImpactT01               2,673,304                                                                                   */
    /*    ImpactT01.csv           8,860,810                                                                                   */
    /*    results.csv                   120                                                                                   */
    /*                                                                                                                        */
    /*    Impact_0000.rad           432,964                                                                                   */
    /*    Impact_0001.rad               646                                                                                   */
    /*                                                                                                                        */
    /*    Impact_0000_0001.rst   33,753,892                                                                                   */
    /*    Impact_0001_0001.rst   33,754,656                                                                                   */
    /*                                                                                                                        */
    /*    Impact_0000.out            73,349                                                                                   */
    /*    Impact_0001.out           115,889                                                                                   */
    /*                                                                                                                        */
    /*    starter.log                 4,450                                                                                   */
    /*    engine.log                128,650                                                                                   */
    /*                                                                                                                        */
    /* -----------------------------------------------------------------------------------------------------------------------*/
    /*                                                                                                                        */
    /* D:/RAD/STARTER.LOG                                                                                                     */
    /*                                                                                                                        */
    /*    ************************************************************************                                            */
    /*    **                                                                    **                                            */
    /*    **                                                                    **                                            */
    /*    **                        OpenRadioss Starter                         **                                            */
    /*    **                                                                    **                                            */
    /*    **            Non-linear Finite Element Analysis Software             **                                            */
    /*    **                                                                    **                                            */
    /*    **                                                                    **                                            */
    /*    **                                                                    **                                            */
    /*    **                  Windows 64 bits, Intel compiler                   **                                            */
    /*    **                      Double Precision Version                      **                                            */
    /*    **                                                                    **                                            */
    /*    **                                                                    **                                            */
    /*    **                                                                    **                                            */
    /*    ************************************************************************                                            */
    /*    ** OpenRadioss Software                                               **                                            */
    /*    ** COPYRIGHT (C) 1986-2026 Altair Engineering, Inc.                   **                                            */
    /*    ** Licensed under GNU Affero General Public License.                  **                                            */
    /*    ** See License file.                                                  **                                            */
    /*    ************************************************************************                                            */
    /*                                                                                                                        */
    /*     .. UNITS SYSTEM                                                                                                    */
    /*     .. CONTROL VARIABLES                                                                                               */
    /*     .. STARTER RUNNING ON    1 THREAD                                                                                  */
    /*     .. MATERIALS                                                                                                       */
    /*     .. NODES                                                                                                           */
    /*     .. PROPERTIES                                                                                                      */
    /*                                                                                                                        */
    /*    WARNING ID :    138                                                                                                 */
    /*    ** WARNING IN PROPERTY DEFINITION                                                                                   */
    /*    DESCRIPTION :                                                                                                       */
    /*       -- PROPERTY ID: 3                                                                                                */
    /*       -- PROPERTY TITLE: SPH                                                                                           */
    /*       PARTICLE MASS MUST BE DEFINED UNLESS PARTICLES ARE BUILT FROM SOLIDS                                             */
    /*     .. 3D SOLID ELEMENTS                                                                                               */
    /*     .. 3D SHELL ELEMENTS                                                                                               */
    /*     .. SPH PARTICLES DEFINITION                                                                                        */
    /*     .. SUBSETS                                                                                                         */
    /*     .. ELEMENT GROUPS                                                                                                  */
    /*     .. PART GROUPS                                                                                                     */
    /*     .. SURFACES                                                                                                        */
    /*     .. LINES                                                                                                           */
    /*     .. NODE GROUP                                                                                                      */
    /*     .. BOUNDARY CONDITIONS                                                                                             */
    /*     .. INITIAL VELOCITIES                                                                                              */
    /*     .. DOMAIN DECOMPOSITION                                                                                            */
    /*     .. ELEMENT GROUPS                                                                                                  */
    /*     .. INTERFACES                                                                                                      */
    /*     .. INTERFACE BUFFER INITIALIZATION                                                                                 */
    /*     .. RIGID BODIES                                                                                                    */
    /*     .. RETURNS TO DOMAIN DECOMPOSITION FOR OPTIMIZATION                                                                */
    /*     .. DOMAIN DECOMPOSITION                                                                                            */
    /*     .. ELEMENT GROUPS                                                                                                  */
    /*     .. INTERFACES                                                                                                      */
    /*     .. INTERFACE BUFFER INITIALIZATION                                                                                 */
    /*     .. RIGID BODIES                                                                                                    */
    /*     .. ELEMENT BUFFER INITIALIZATION                                                                                   */
    /*     .. GEOMETRY PLOT FILE                                                                                              */
    /*     .. PARALLEL RESTART FILES GENERATION                                                                               */
    /*                                                                                                                        */
    /*    -------------------------------------------------------                                                             */
    /*                                                                                                                        */
    /*                       ** COMPUTE TIME INFORMATION **                                                                   */
    /*                                                                                                                        */
    /*     EXECUTION STARTED      :      2026/06/02  12:39:40                                                                 */
    /*     EXECUTION COMPLETED    :      2026/06/02  12:39:42                                                                 */
    /*                                                                                                                        */
    /*     ELAPSED TIME...........=          2.09 s                                                                           */
    /*                                   00:00:02                                                                             */
    /*                                                                                                                        */
    /*    -------------------------------------------------------                                                             */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*         TERMINATION WITH WARNING                                                                                       */
    /*         ------------------                                                                                             */
    /*                  0 ERROR(S)                                                                                            */
    /*                  7 WARNING(S)                                                                                          */
    /*                                                                                                                        */
    /*    PLEASE CHECK LISTING FILE FOR FURTHER DETAILS                                                                       */
    /*                                                                                                                        */
    /* -----------------------------------------------------------------------------------------------------------------------*/
    /*                                                                                                                        */
    /* D:/RAD/ENGINE.LOG                                                                                                    */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* ************************************************************************                                               */
    /* **                                                                    **                                               */
    /* **                                                                    **                                               */
    /* **                         OpenRadioss Engine                         **                                               */
    /* **                                                                    **                                               */
    /* **            Non-linear Finite Element Analysis Software             **                                               */
    /* **                                                                    **                                               */
    /* **                                                                    **                                               */
    /* **                                                                    **                                               */
    /* **                  Windows 64 bits, Intel compiler                   **                                               */
    /* **                      Double Precision Version                      **                                               */
    /* **                                                                    **                                               */
    /* **                                                                    **                                               */
    /* **                                                                    **                                               */
    /* ************************************************************************                                               */
    /* ** OpenRadioss Software                                               **                                               */
    /* ** COPYRIGHT (C) 1986-2026 Altair Engineering, Inc.                   **                                               */
    /* ** Licensed under GNU Affero General Public License.                  **                                               */
    /* ** See License file.                                                  **                                               */
    /* ************************************************************************                                               */
    /*                                                                                                                        */
    /*  ROOT: Impact  RESTART: 0001                                                                                           */
    /*  NUMBER OF HMPP PROCESSES     1                                                                                        */
    /*  02/06/2026                                                                                                            */
    /*   ** INFO ** SPH RE-SEARCH FOR NEIGHBOURS                                                                              */
    /*  NC=       0 T= 0.0000E+00 DT= 1.8380E-07 ERR=  0.0% DM/M= 0.0000E+00                                                  */
    /*      ANIMATION FILE: ImpactA001 WRITTEN                                                                                */
    /*      H3D FILE: Impact.h3d UPDATED:  FRAME=     1 , NC=       0 , TIME=   0.000                                         */
    /*   ** INFO ** SPH RE-SEARCH FOR NEIGHBOURS                                                                              */
    /*   ** INFO ** SPH RE-SEARCH FOR NEIGHBOURS                                                                              */
    /*   ** INFO ** SPH RE-SEARCH FOR NEIGHBOURS                                                                              */
    /*      ANIMATION FILE: ImpactA002 WRITTEN                                                                                */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /* CONTACT SORTING.............: .6203E+01     3.32 %                                                                     */
    /*  CONTACT FORCES..............: .7812E+00     0.42 %                                                                    */
    /*  ELEMENT FORCES..............: .1602E+02     8.58 %                                                                    */
    /*  KINEMATIC COND..............: .4562E+01     2.44 %                                                                    */
    /*  INTEGRATION.................: .1055E+02     5.65 %                                                                    */
    /*  ASSEMBLING..................: .1922E+01     1.03 %                                                                    */
    /*  OTHERS (including I/O)......: .1466E+03    78.55 %                                                                    */
    /*  TOTAL.......................: .1866E+03   100.00 %                                                                    */
    /*                                                                                                                        */
    /*                    ** MEMORY USAGE STATISTICS **                                                                       */
    /*                                                                                                                        */
    /*  TOTAL MEMORY USED .........................:      219 MB                                                              */
    /*  MAXIMUM MEMORY PER PROCESSOR...............:      219 MB                                                              */
    /*  MINIMUM MEMORY PER PROCESSOR...............:      219 MB                                                              */
    /*  AVERAGE MEMORY PER PROCESSOR...............:      219 MB                                                              */
    /*                                                                                                                        */
    /*                    ** DISK USAGE STATISTICS **                                                                         */
    /*                                                                                                                        */
    /*  TOTAL DISK SPACE USED .....................:        164 MB                                                            */
    /*  ANIMATION/H3D/TH/OUTP SIZE ................:        132 MB                                                            */
    /*  RESTART FILE SIZE .........................:         32 MB                                                            */
    /*                                                                                                                        */
    /*  ELAPSED TIME     =        188.11 s                                                                                    */
    /*                           0:03:08                                                                                      */
    /*                                                                                                                        */
    /*      NORMAL TERMINATION                                                                                                */
    /*      TOTAL NUMBER OF CYCLES  :    7619                                                                                 */
    /*                                                                                                                        */
    /* -----------------------------------------------------------------------------------------------------------------------*/
    /*                                                                                                                        */
    /*  D:/RAD/IMPACKT01.CSV                                                                                                  */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  The MEANS Procedure                                                                                                   */
    /*                              Summary statistics                                                                        */
    /*  Variable                 Label                                      N         Mean         Minimum         Maximum    */
    /*                                                                                                                        */
    /*  TIME                     Time                                     500 0.0002495326               0    0.0004990278    */
    /*  INTERNALENERGY           Internal Energy                          500 707995.81663               0        888201.4    */
    /*  KINETICENERGY            Kinetic Energy                           500  4267530.056         4066488         5023688    */
    /*  X_MOMENTUM               X Momentum                               500 0.1822888253    -0.001102821        0.349126    */
    /*  Y_MOMENTUM               Y Momentum                               500 0.3651750457    -0.000245739       0.5850916    */
    /*  Z_MOMENTUM               Z Momentum                               500 -92.67074848       -100.6157       -90.34196    */
    /*  MASS                     Mass                                     500  0.001038488     0.001038488     0.001038488    */
    /*  TIMESTEP                 Time Step                                500 6.7532112E-8      4.54308E-8     1.837958E-7    */
    /*  ROTATIONENERGY           Rotation Energy                          500 4347.5188561               0        6369.697    */
    /*  EXTERNALWORK             External Work                            500            0               0               0    */
    /*  SPRINGENERGY             Spring Energy                            500            0               0               0    */
    /*  CONTACTENERGY            Contact Energy                           500 43063.994031               0        61964.71    */
    /*  HOURGLASSENERGY          Hourglass Energy                         500 357.09532507               0        535.9865    */
    /*  ELASTICCONTACTENERGY     Elastic Contact Energy                   500 507.51642061               0        1927.893    */
    /*  FRICTIONALCONTACTENERGY  Frictional Contact Energy                500 42556.477397               0        61964.71    */
    /*  DAMPINGCONTACTENERGY     Damping Contact Energy                   500            0               0               0    */
    /*  PLASTICWORK              Plastic Work                             500 514735.94116               0        669617.9    */
    /*  ADDEDMASS                Added Mass                               500  -0.00003375     -0.00003375     -0.00003375    */
    /*  PERCENTAGEADDEDMASS      Percentage Added Mass                    500    -3.249918       -3.249918       -3.249918    */
    /*  INLETMASS                Inlet Mass                               500            0               0               0    */
    /*  OUTLETMASS               Outlet Mass                              500            0               0               0    */
    /*  INLETENERGY              Inlet Energy                             500            0               0               0    */
    /*  OUTLETENERGY             Outlet Energy                            500            0               0               0    */
    /*  PLATEIE                  Plate Internal Energy                    500 565898.51183               0        734858.1    */
    /*  PLATEKE                  Plate Kinetic Energy                     500 3970.3446287               0        16958.08    */
    /*  PLATEXMOM                Plate X Momentum                         500 -0.002671136     -0.04299465      0.03969102    */
    /*  PLATEYMOM                Plate Y Momentum                         500 -0.003565117     -0.06337282      0.06048155    */
    /*  PLATEZMOM                Plate Z Momentum                         500 -0.158396311      -0.7100757      0.09326532    */
    /*  PLATEMASS                Plate Mass                               500 0.0000331626      0.00003285      0.00003375    */
    /*  PLATEHE                  Plate Total Energy                       500            0               0               0    */
    /*  PLATEERODED              Plate Eroded                             500       32.636               0              50    */
    /*  PLATEHEAT                Plate Heat                               500            0               0               0    */
    /*  IMPACTORIE               Impactor Internal Energy                 500            0               0               0    */
    /*  IMPACTORKE               Impactor Kinetic Energy                  500            0               0               0    */
    /*  IMPACTORXMOM             Impactor X Momentum                      500            0               0               0    */
    /*  IMPACTORYMOM             Impactor Y Momentum                      500            0               0               0    */
    /*  IMPACTORZMOM             Impactor Z Momentum                      500            0               0               0    */
    /*  IMPACTORMASS             Impactor Mass                            500            0               0               0    */
    /*  IMPACTORHE               Impactor Total Energy                    500            0               0               0    */
    /*  IMPACTORERODED           Impactor Eroded                          500            0               0               0    */
    /*  IMPACTORHEAT             Impactor Heat                            500            0               0               0    */
    /*  TH_INTER1GROUP1VAR41     Time-History Inter 1 Group 1 Variable 41 500 0.1379095843               0        0.260351    */
    /*  TH_INTER1GROUP1VAR42     Time-History Inter 1 Group 1 Variable 42 500 0.0627015745     -0.06841327       0.1522743    */
    /*  TH_INTER1GROUP1VAR43     Time-History Inter 1 Group 1 Variable 43 500 -7.438980774        -9.30014               0    */
    /*  TH_INTER1GROUP1VAR44     Time-History Inter 1 Group 1 Variable 44 500 -0.327415273      -0.3992586               0    */
    /*  TH_INTER1GROUP1VAR45     Time-History Inter 1 Group 1 Variable 45 500 -0.436022161       -0.532333               0    */
    /*  TH_INTER1GROUP1VAR46     Time-History Inter 1 Group 1 Variable 46 500 -0.550418909      -0.8042181     0.007238572    */
    /*  TH_ELEM1883VAR47         Time-History Element 1883 Variable 47    500            1               1               1    */
    /*  TH_ELEM1883VAR48         Time-History Element 1883 Variable 48    500 126.07312804       -228.9241         372.497    */
    /*  TH_ELEM1883VAR49         Time-History Element 1883 Variable 49    500 226.12876628       -2.378552         395.032    */
    /*  TH_ELEM1883VAR50         Time-History Element 1883 Variable 50    500 95.952641055       -8.563899         206.379    */
    /*  TH_ELEM768VAR1319        Time-History Element 768 Variable 1319   500 74.454696506               0        98.99322    */
    /*  TH_ELEM768VAR1320        Time-History Element 768 Variable 1319   500 2.7056275E-9     2.685411E-9     2.719253E-9    */
    /*  TH_ELEM768VAR1321        Time-History Element 768 Variable 1319   500 0.1359897314               0       0.1775392    */
    /*  TH_ELEM768VAR1322        Time-History Element 768 Variable 1319   500          300             300             300    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*                                    _ _                 _
      ___  _ __   ___ _ __  _ __ __ _  __| (_) ___  ___ ___  | | ___   __ _
     / _ \| `_ \ / _ \ `_ \| `__/ _` |/ _` | |/ _ \/ __/ __| | |/ _ \ / _` |
    | (_) | |_) |  __/ | | | | | (_| | (_| | | (_) \__ \__ \ | | (_) | (_| |
     \___/| .__/ \___|_| |_|_|  \__,_|\__,_|_|\___/|___/___/ |_|\___/ \__, |
          |_|                                                         |___/
    */

    1                                          Altair SLC          12:39 Tuesday, June  2, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx

    NOTE: Library slchelp assigned as follows:
          Engine:        WPD
          Physical Name: C:\Progra~1\Altair\SLC\2026\sashelp


    LOG:  12:39:22
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.026
          cpu time  : 0.046


    NOTE: Format num2mis output
    NOTE: Format $chr2mis output
    NOTE: Procedure format step took :
          real time : 0.000
          cpu time  : 0.015


    NOTE: AUTOEXEC processing completed

    1          options validvarname=v7;
    2         options set=PYTHONHOME "D:\py314";
    3         proc python;
    4         submit;
    5         import os
    6         import pandas as pd
    7         import subprocess
    8         from pathlib import Path
    9
    10        # ============================================================================
    11        # CONFIGURATION
    12        # ============================================================================
    13
    14        OPENRADIOSS_PATH = Path("C:/openradioss")
    15        STARTER_EXE = OPENRADIOSS_PATH / "exec" / "starter_win64.exe"
    16        ENGINE_EXE = OPENRADIOSS_PATH / "exec" / "engine_win64.exe"
    17        TH_TO_CSV_EXE = OPENRADIOSS_PATH / "exec" / "th_to_csv_win64.exe"
    18
    19        MODEL_DIR = Path("D:/rad")
    20        STARTER_FILE = "Impact_0000.rad"
    21        ENGINE_FILE =  "Impact_0001.rad"
    22
    23        # Time history file (output from simulation)
    24        TH_FILE = MODEL_DIR / "ImpactT01"
    25        # CSV output file
    26        CSV_FILE = MODEL_DIR / "results.csv"
    27
    28        SETVARS_PATH = Path("C:/Program Files (x86)/Intel/oneAPI/setvars.bat")
    29        OMP_NUM_THREADS = "1"
    30        KMP_STACKSIZE = "400m"
    31
    32        # ============================================================================
    33        # ENVIRONMENT SETUP
    34        # ============================================================================
    35
    36        def setup_environment():
    37            env = os.environ.copy()
    38            env["OPENRADIOSS_PATH"] = str(OPENRADIOSS_PATH)
    39            env["RAD_CFG_PATH"] = str(OPENRADIOSS_PATH / "hm_cfg_files")
    40            env["RAD_H3D_PATH"] = str(OPENRADIOSS_PATH / "extlib" / "h3d" / "lib" / "win64")
    41            env["OMP_NUM_THREADS"] = OMP_NUM_THREADS
    42            env["KMP_STACKSIZE"] = KMP_STACKSIZE
    43
    44            hm_reader = OPENRADIOSS_PATH / "extlib" / "hm_reader" / "win64"
    45            if hm_reader.exists():
    46                env["PATH"] = str(hm_reader) + ";" + env.get("PATH", "")
    47
    48            # Add tools directory to PATH for th_to_csv
    49            tools_dir = OPENRADIOSS_PATH / "tools"
    50            if tools_dir.exists():
    51                env["PATH"] = str(tools_dir) + ";" + env.get("PATH", "")
    52
    53            return env
    54
    55        def run_cmd(cmd, cwd, env, log_file):
    56            """Run command and capture output to log file"""
    57            with open(log_file, 'w') as f:
    58                result = subprocess.run(cmd, shell=True, cwd=cwd, env=env,
    59                                        stdout=f, stderr=subprocess.STDOUT, text=True)
    60            return result.returncode
    61
    62        def convert_th_to_csv(th_file, csv_file, env):
    63            """Convert time history binary file to CSV format"""
    64            if not th_file.exists():
    65                print(f"Warning: Time history file not found: {th_file}")
    66                return False
    67
    68            if not TH_TO_CSV_EXE.exists():
    69                print(f"Warning: th_to_csv_win64.exe not found at {TH_TO_CSV_EXE}")
    70                return False
    71
    72            print(f"Converting time history: {th_file.name} -> {csv_file.name}")
    73
    74            # Run th_to_csv and redirect output to CSV file
    75            cmd = f'"{TH_TO_CSV_EXE}" "{th_file}"'
    76
    77            try:
    78                with open(csv_file, 'w') as f:
    79                    result = subprocess.run(cmd, shell=True, cwd=str(MODEL_DIR), env=env,
    80                                            stdout=f, stderr=subprocess.PIPE, text=True)
    81
    82                if result.returncode == 0 and csv_file.exists() and csv_file.stat().st_size > 0:
    83                    # Count lines to verify data
    84                    with open(csv_file, 'r') as f:
    85                        line_count = sum(1 for _ in f)
    86                    print(f"  [OK] Created {csv_file.name} ({line_count} lines, {csv_file.stat().st_size / 1024:.1f} KB)")
    87
    88                    # Show first few lines as preview
    89                    with open(csv_file, 'r') as f:
    90                        header = f.readline().strip()
    91                        first_data = f.readline().strip() if line_count > 1 else ""
    92                    print(f"  Header: {header[:100]}...")
    93                    return True
    94                else:
    95                    print(f"  [FAILED] Conversion failed (exit code {result.returncode})")
    96                    if result.stderr:
    97                        print(f"    Error: {result.stderr[:200]}")
    98                    return False
    99            except Exception as e:
    100               print(f"  [ERROR] {e}")
    101               return False
    102
    103       # ============================================================================
    104       # MAIN EXECUTION
    105       # ============================================================================
    106
    107       def main():
    108           print("=" * 60)
    109           print("OpenRadioss Rubber Seal Simulation")
    110           print("=" * 60)
    111
    112           # Quick verification
    113           if not STARTER_EXE.exists() or not ENGINE_EXE.exists():
    114               print("ERROR: OpenRadioss executables not found")
    115               return 1
    116
    117           env = setup_environment()
    118           setvars = f'call "{SETVARS_PATH}" intel64 vs2022 > nul 2>&1 && ' if SETVARS_PATH.exists() else ""
    119
    120           # Run Starter
    121           print("\n[1/3] Running Starter...")
    122           starter_input = MODEL_DIR / STARTER_FILE
    123           rc = run_cmd(f'{setvars}"{STARTER_EXE}" -i "{starter_input}"',
    124                         str(MODEL_DIR), env, MODEL_DIR / "starter.log")
    125           if rc != 0:
    126               print(f"Starter failed (exit {rc}). Check starter.log")
    127               return rc
    128
    129           # Run Engine
    130           print("[2/3] Running Engine...")
    131           engine_input = MODEL_DIR / ENGINE_FILE
    132           rc = run_cmd(f'{setvars}"{ENGINE_EXE}" -i "{engine_input}"',
    133                         str(MODEL_DIR), env, MODEL_DIR / "engine.log")
    134           if rc != 0:
    135               print(f"Engine failed (exit {rc}). Check engine.log")
    136               return rc
    137
    138           # List animation files created
    139           anim_files = list(MODEL_DIR.glob("*.A0*")) + list(MODEL_DIR.glob("*.h3d"))
    140           if anim_files:
    141               print(f"\nAnimation files created ({len(anim_files)}):")
    142               for f in sorted(anim_files):
    143                   size_kb = f.stat().st_size / 1024
    144                   print(f"  {f.name} ({size_kb:.1f} KB)")
    145           else:
    146               print("\nWarning: No animation files found")
    147
    148           # Convert time history to CSV
    149           print("\n[3/3] Converting time history to CSV...")
    150           convert_th_to_csv(TH_FILE, CSV_FILE, env)
    151
    152           # Summary
    153           print("\n" + "=" * 60)
    154           print("SIMULATION COMPLETE")
    155           print("=" * 60)
    156           print(f"Results saved to: {MODEL_DIR}")
    157           print(f"  - Time history CSV: {CSV_FILE.name}")
    158           print(f"  - Starter log: starter.log")
    159           print(f"  - Engine log: engine.log")
    160           if anim_files:
    161               print(f"  - Animation files: {len(anim_files)} files")
    162
    163           # Verify CSV was created
    164           if CSV_FILE.exists():
    165               print(f"\nCSV file size: {CSV_FILE.stat().st_size / 1024:.1f} KB")
    166               print("You can now open results.csv in Excel or Python for analysis.")
    167
    168           print("\nDone.")
    169           return 0
    170
    171       if __name__ == "__main__":
    172           exit(main());
    173       endsubmit;

    NOTE: Submitting statements to Python:


    174       run;
    NOTE: Procedure python step took :
          real time : 3:44.807
          cpu time  : 0:00.078


    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 3:45.012
          cpu time  : 0:00.250


    /*  _                      _          _     _     _                    _        _     _
    | || |     ___ _____   __ | |_ ___   | |__ (_)___| |_ ___  _ __ _   _ | |_ __ _| |__ | | ___
    | || |_   / __/ __\ \ / / | __/ _ \  | `_ \| / __| __/ _ \| `__| | | || __/ _` | `_ \| |/ _ \
    |__   _| | (__\__ \\ V /  | || (_) | | | | | \__ \ || (_) | |  | |_| || || (_| | |_) | |  __/
       |_|    \___|___/ \_/    \__\___/  |_| |_|_|___/\__\___/|_|   \__, | \__\__,_|_.__/|_|\___|
                                                                    |___/
    Contents
      1 fix problematic column headings and create slc table
      2 create slc table from csv

    FYI
      I could not get /TH.TITLE to work in the 0001.rad file, so some of the
      labels are less descriptive?

    */

    /*--- I COULD NOT GET THE SLC TO IMPUT A CSV WITH 1323 COLUMNS ---*/

    libname workx sas7bdat "d:/wpswrkx"; /*--- put in your autoexec file ---*/

    options set=PYTHONHOME "D:\py314";
    proc python;
    submit;
    import pandas as pd
    df = pd.read_csv("d:/rad/ImpactT01.csv")
    df.columns = df.columns.str.replace(r"\s+", "", regex=True)
    print(df);
    endsubmit;
    import python=df data=workx.df;
    run;

    data workx.time_hist;
    label
      TIME                      = "Time"
      INTERNALENERGY            = "Internal Energy"
      KINETICENERGY             = "Kinetic Energy"
      X_MOMENTUM                = "X Momentum"
      Y_MOMENTUM                = "Y Momentum"
      Z_MOMENTUM                = "Z Momentum"
      MASS                      = "Mass"
      TIMESTEP                  = "Time Step"
      ROTATIONENERGY            = "Rotation Energy"
      EXTERNALWORK              = "External Work"
      SPRINGENERGY              = "Spring Energy"
      CONTACTENERGY             = "Contact Energy"
      HOURGLASSENERGY           = "Hourglass Energy"
      ELASTICCONTACTENERGY      = "Elastic Contact Energy"
      FRICTIONALCONTACTENERGY   = "Frictional Contact Energy"
      DAMPINGCONTACTENERGY      = "Damping Contact Energy"
      PLASTICWORK               = "Plastic Work"
      ADDEDMASS                 = "Added Mass"
      PERCENTAGEADDEDMASS       = "Percentage Added Mass"
      INLETMASS                 = "Inlet Mass"
      OUTLETMASS                = "Outlet Mass"
      INLETENERGY               = "Inlet Energy"
      OUTLETENERGY              = "Outlet Energy"
      PLATEIE                   = "Plate Internal Energy"
      PLATEKE                   = "Plate Kinetic Energy"
      PLATEXMOM                 = "Plate X Momentum"
      PLATEYMOM                 = "Plate Y Momentum"
      PLATEZMOM                 = "Plate Z Momentum"
      PLATEMASS                 = "Plate Mass"
      PLATEHE                   = "Plate Total Energy"
      PLATEERODED               = "Plate Eroded"
      PLATEHEAT                 = "Plate Heat"
      IMPACTORIE                = "Impactor Internal Energy"
      IMPACTORKE                = "Impactor Kinetic Energy"
      IMPACTORXMOM              = "Impactor X Momentum"
      IMPACTORYMOM              = "Impactor Y Momentum"
      IMPACTORZMOM              = "Impactor Z Momentum"
      IMPACTORMASS              = "Impactor Mass"
      IMPACTORHE                = "Impactor Total Energy"
      IMPACTORERODED            = "Impactor Eroded"
      IMPACTORHEAT              = "Impactor Heat"

      TH_INTER1GROUP1VAR41      = "Time-History Inter 1 Group 1 Variable 41"
      TH_INTER1GROUP1VAR42      = "Time-History Inter 1 Group 1 Variable 42"
      TH_INTER1GROUP1VAR43      = "Time-History Inter 1 Group 1 Variable 43"
      TH_INTER1GROUP1VAR44      = "Time-History Inter 1 Group 1 Variable 44"
      TH_INTER1GROUP1VAR45      = "Time-History Inter 1 Group 1 Variable 45"
      TH_INTER1GROUP1VAR46      = "Time-History Inter 1 Group 1 Variable 46"

      TH_ELEM1883VAR47          = "Time-History Element 1883 Variable 47"
      TH_ELEM1883VAR48          = "Time-History Element 1883 Variable 48"
      TH_ELEM1883VAR49          = "Time-History Element 1883 Variable 49"
      TH_ELEM1883VAR50          = "Time-History Element 1883 Variable 50"

      /*--- ... repeat pattern for all TH_ELEM variables up to TH_ELEM768VAR1319 ...
                see complete_time,sas in this repo for all 1320 ariables
                last 4 variables below
       ---*/

      TH_ELEM768VAR1319     = "Time-History Element 768 Variable 1319"
      TH_ELEM768VAR1320     = "Time-History Element 768 Variable 1319"
      TH_ELEM768VAR1321     = "Time-History Element 768 Variable 1319"
      TH_ELEM768VAR1322     = "Time-History Element 768 Variable 1319"
     ;

     /*--- THE ~1300 DROPPED VARIABLES GIVE DETAIL CELL VALUES - YOU MAY WANT TO RESHAPE ---*/

     set workx.df(drop=TH_ELEM1883VAR51--TH_ELEM768VAR1318);
     run;

    options label;
    proc contents data=wpdx.time_hist position;
    run;

    proc means data=workx.time_hist n mean min max;
    run;



    /**************************************************************************************************************************/
    /* PYTHON                                                                                                                 */
    /* WORKX.TIME_HIST                                                                                                        */
    /*                                                                                                                        */
    /* [500 rows x 1323 columns]                                                                                              */
    /*                                                                                                                        */
    /* Altair SLC                                                                                                             */
    /*                                                                                                                        */
    /* The PYTHON Procedure                                                                                                   */
    /*                                                                                                                        */
    /*          time  INTERNALENERGY  ...  TH_ELEM768var1321  TH_ELEM768var1322                                               */
    /* 0    0.000000         0.00000  ...           0.000000              300.0                                               */
    /* 1    0.000001        58.61925  ...           0.000000              300.0                                               */
    /* 2    0.000002       512.75820  ...           0.000000              300.0                                               */
    /* 3    0.000003      1868.78800  ...           0.000000              300.0                                               */
    /* 4    0.000004      3624.49700  ...           0.000000              300.0                                               */
    /* ..        ...             ...  ...                ...                ...                                               */
    /* 495  0.000495    888097.90000  ...           0.177539              300.0                                               */
    /* 496  0.000496    888121.90000  ...           0.177539              300.0                                               */
    /* 497  0.000497    888110.90000  ...           0.177539              300.0                                               */
    /* 498  0.000498    888075.80000  ...           0.177539              300.0                                               */
    /* 499  0.000499    888143.10000  ...           0.177539              300.0                                               */
    /*                                                                                                                        */
    /*------------------------------------------------------------------------------------------------------------------------*/
    /* SLC                                                                                                                    */
    /* Altair SLC                                                                                                             */
    /*                                                                                                                        */
    /* Altair SLC                                                                                                             */
    /*                                                                                                                        */
    /* The CONTENTS Procedure                                                                                                 */
    /*                                                                                                                        */
    /* Data Set Name           TIME_HIST                                                                                      */
    /* Member Type             DATA                                                                                           */
    /* Engine                  WPD                                                                                            */
    /* Created                 02JUN2026:07:58:42                                                                             */
    /* Last Modified           02JUN2026:07:58:42                                                                             */
    /* Observations                   500                                                                                     */
    /* Variables               55                                                                                             */
    /* Indexes                 0                                                                                              */
    /* Observation Length      440                                                                                            */
    /* Deleted Observations             0                                                                                     */
    /* Data Set Type                                                                                                          */
    /* Label                                                                                                                  */
    /* Compressed              NO                                                                                             */
    /* Sorted                  NO                                                                                             */
    /* Data Representation     Little endian, IEEE Windows                                                                    */
    /* Encoding                wlatin1 Windows-1252 Western                                                                   */
    /*                                                                                                                        */
    /*                               List of Variables and Attributes in Creation Order                                       */
    /*                                                                                                                        */
    /* Number    Variable                   Type Len     Pos    Label                                                         */
    /* _________________________________________________________________________________________________                      */
    /*      1    TIME                       Num    8       0    Time                                                          */
    /*      2    INTERNALENERGY             Num    8       8    Internal Energy                                               */
    /*      3    KINETICENERGY              Num    8      16    Kinetic Energy                                                */
    /*      4    X_MOMENTUM                 Num    8      24    X Momentum                                                    */
    /*      5    Y_MOMENTUM                 Num    8      32    Y Momentum                                                    */
    /*      6    Z_MOMENTUM                 Num    8      40    Z Momentum                                                    */
    /*      7    MASS                       Num    8      48    Mass                                                          */
    /*      8    TIMESTEP                   Num    8      56    Time Step                                                     */
    /*      9    ROTATIONENERGY             Num    8      64    Rotation Energy                                               */
    /*     10    EXTERNALWORK               Num    8      72    External Work                                                 */
    /*     11    SPRINGENERGY               Num    8      80    Spring Energy                                                 */
    /*     12    CONTACTENERGY              Num    8      88    Contact Energy                                                */
    /*     13    HOURGLASSENERGY            Num    8      96    Hourglass Energy                                              */
    /*     14    ELASTICCONTACTENERGY       Num    8     104    Elastic Contact Energy                                        */
    /*     15    FRICTIONALCONTACTENERGY    Num    8     112    Frictional Contact Energy                                     */
    /*     16    DAMPINGCONTACTENERGY       Num    8     120    Damping Contact Energy                                        */
    /*     17    PLASTICWORK                Num    8     128    Plastic Work                                                  */
    /*     18    ADDEDMASS                  Num    8     136    Added Mass                                                    */
    /*     19    PERCENTAGEADDEDMASS        Num    8     144    Percentage Added Mass                                         */
    /*     20    INLETMASS                  Num    8     152    Inlet Mass                                                    */
    /*     21    OUTLETMASS                 Num    8     160    Outlet Mass                                                   */
    /*     22    INLETENERGY                Num    8     168    Inlet Energy                                                  */
    /*     23    OUTLETENERGY               Num    8     176    Outlet Energy                                                 */
    /*     24    PLATEIE                    Num    8     184    Plate Internal Energy                                         */
    /*     25    PLATEKE                    Num    8     192    Plate Kinetic Energy                                          */
    /*     26    PLATEXMOM                  Num    8     200    Plate X Momentum                                              */
    /*     27    PLATEYMOM                  Num    8     208    Plate Y Momentum                                              */
    /*     28    PLATEZMOM                  Num    8     216    Plate Z Momentum                                              */
    /*     29    PLATEMASS                  Num    8     224    Plate Mass                                                    */
    /*     30    PLATEHE                    Num    8     232    Plate Total Energy                                            */
    /*     31    PLATEERODED                Num    8     240    Plate Eroded                                                  */
    /*     32    PLATEHEAT                  Num    8     248    Plate Heat                                                    */
    /*     33    IMPACTORIE                 Num    8     256    Impactor Internal Energy                                      */
    /*     34    IMPACTORKE                 Num    8     264    Impactor Kinetic Energy                                       */
    /*     35    IMPACTORXMOM               Num    8     272    Impactor X Momentum                                           */
    /*     36    IMPACTORYMOM               Num    8     280    Impactor Y Momentum                                           */
    /*     37    IMPACTORZMOM               Num    8     288    Impactor Z Momentum                                           */
    /*     38    IMPACTORMASS               Num    8     296    Impactor Mass                                                 */
    /*     39    IMPACTORHE                 Num    8     304    Impactor Total Energy                                         */
    /*     40    IMPACTORERODED             Num    8     312    Impactor Eroded                                               */
    /*     41    IMPACTORHEAT               Num    8     320    Impactor Heat                                                 */
    /*                                                                                                                        */
    /*     42    TH_INTER1GROUP1VAR41       Num    8     328    Time-History Inter 1 Group 1 Variable 41                      */
    /*     43    TH_INTER1GROUP1VAR42       Num    8     336    Time-History Inter 1 Group 1 Variable 42                      */
    /*     44    TH_INTER1GROUP1VAR43       Num    8     344    Time-History Inter 1 Group 1 Variable 43                      */
    /*     45    TH_INTER1GROUP1VAR44       Num    8     352    Time-History Inter 1 Group 1 Variable 44                      */
    /*     46    TH_INTER1GROUP1VAR45       Num    8     360    Time-History Inter 1 Group 1 Variable 45                      */
    /*     47    TH_INTER1GROUP1VAR46       Num    8     368    Time-History Inter 1 Group 1 Variable 46                      */
    /*                                                                                                                        */
    /*     48    TH_ELEM1883VAR47           Num    8     376    Time-History Element 1883 Variable 47                         */
    /*     49    TH_ELEM1883VAR48           Num    8     384    Time-History Element 1883 Variable 48                         */
    /*     50    TH_ELEM1883VAR49           Num    8     392    Time-History Element 1883 Variable 49                         */
    /*     51    TH_ELEM1883VAR50           Num    8     400    Time-History Element 1883 Variable 50                         */
    /*           ...                                                                                                          */
    /*   1320    TH_ELEM768VAR1319          Num    8     408    Time-History Element 768 Variable 1319                        */
    /*   1321    TH_ELEM768VAR1320          Num    8     416    Time-History Element 768 Variable 1319                        */
    /*   1322    TH_ELEM768VAR1321          Num    8     424    Time-History Element 768 Variable 1319                        */
    /*   1323    TH_ELEM768VAR1322          Num    8     432    Time-History Element 768 Variable 1319                        */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  Altair SLC                                                                                                            */
    /*                                                                                                                        */
    /*  The MEANS Procedure                                                                                                   */
    /*                              Summary statistics                                                                        */
    /*  Variable                 Label                                      N         Mean         Minimum         Maximum    */
    /*                                                                                                                        */
    /*  TIME                     Time                                     500 0.0002495326               0    0.0004990278    */
    /*  INTERNALENERGY           Internal Energy                          500 707995.81663               0        888201.4    */
    /*  KINETICENERGY            Kinetic Energy                           500  4267530.056         4066488         5023688    */
    /*  X_MOMENTUM               X Momentum                               500 0.1822888253    -0.001102821        0.349126    */
    /*  Y_MOMENTUM               Y Momentum                               500 0.3651750457    -0.000245739       0.5850916    */
    /*  Z_MOMENTUM               Z Momentum                               500 -92.67074848       -100.6157       -90.34196    */
    /*  MASS                     Mass                                     500  0.001038488     0.001038488     0.001038488    */
    /*  TIMESTEP                 Time Step                                500 6.7532112E-8      4.54308E-8     1.837958E-7    */
    /*  ROTATIONENERGY           Rotation Energy                          500 4347.5188561               0        6369.697    */
    /*  EXTERNALWORK             External Work                            500            0               0               0    */
    /*  SPRINGENERGY             Spring Energy                            500            0               0               0    */
    /*  CONTACTENERGY            Contact Energy                           500 43063.994031               0        61964.71    */
    /*  HOURGLASSENERGY          Hourglass Energy                         500 357.09532507               0        535.9865    */
    /*  ELASTICCONTACTENERGY     Elastic Contact Energy                   500 507.51642061               0        1927.893    */
    /*  FRICTIONALCONTACTENERGY  Frictional Contact Energy                500 42556.477397               0        61964.71    */
    /*  DAMPINGCONTACTENERGY     Damping Contact Energy                   500            0               0               0    */
    /*  PLASTICWORK              Plastic Work                             500 514735.94116               0        669617.9    */
    /*  ADDEDMASS                Added Mass                               500  -0.00003375     -0.00003375     -0.00003375    */
    /*  PERCENTAGEADDEDMASS      Percentage Added Mass                    500    -3.249918       -3.249918       -3.249918    */
    /*  INLETMASS                Inlet Mass                               500            0               0               0    */
    /*  OUTLETMASS               Outlet Mass                              500            0               0               0    */
    /*  INLETENERGY              Inlet Energy                             500            0               0               0    */
    /*  OUTLETENERGY             Outlet Energy                            500            0               0               0    */
    /*  PLATEIE                  Plate Internal Energy                    500 565898.51183               0        734858.1    */
    /*  PLATEKE                  Plate Kinetic Energy                     500 3970.3446287               0        16958.08    */
    /*  PLATEXMOM                Plate X Momentum                         500 -0.002671136     -0.04299465      0.03969102    */
    /*  PLATEYMOM                Plate Y Momentum                         500 -0.003565117     -0.06337282      0.06048155    */
    /*  PLATEZMOM                Plate Z Momentum                         500 -0.158396311      -0.7100757      0.09326532    */
    /*  PLATEMASS                Plate Mass                               500 0.0000331626      0.00003285      0.00003375    */
    /*  PLATEHE                  Plate Total Energy                       500            0               0               0    */
    /*  PLATEERODED              Plate Eroded                             500       32.636               0              50    */
    /*  PLATEHEAT                Plate Heat                               500            0               0               0    */
    /*  IMPACTORIE               Impactor Internal Energy                 500            0               0               0    */
    /*  IMPACTORKE               Impactor Kinetic Energy                  500            0               0               0    */
    /*  IMPACTORXMOM             Impactor X Momentum                      500            0               0               0    */
    /*  IMPACTORYMOM             Impactor Y Momentum                      500            0               0               0    */
    /*  IMPACTORZMOM             Impactor Z Momentum                      500            0               0               0    */
    /*  IMPACTORMASS             Impactor Mass                            500            0               0               0    */
    /*  IMPACTORHE               Impactor Total Energy                    500            0               0               0    */
    /*  IMPACTORERODED           Impactor Eroded                          500            0               0               0    */
    /*  IMPACTORHEAT             Impactor Heat                            500            0               0               0    */
    /*  TH_INTER1GROUP1VAR41     Time-History Inter 1 Group 1 Variable 41 500 0.1379095843               0        0.260351    */
    /*  TH_INTER1GROUP1VAR42     Time-History Inter 1 Group 1 Variable 42 500 0.0627015745     -0.06841327       0.1522743    */
    /*  TH_INTER1GROUP1VAR43     Time-History Inter 1 Group 1 Variable 43 500 -7.438980774        -9.30014               0    */
    /*  TH_INTER1GROUP1VAR44     Time-History Inter 1 Group 1 Variable 44 500 -0.327415273      -0.3992586               0    */
    /*  TH_INTER1GROUP1VAR45     Time-History Inter 1 Group 1 Variable 45 500 -0.436022161       -0.532333               0    */
    /*  TH_INTER1GROUP1VAR46     Time-History Inter 1 Group 1 Variable 46 500 -0.550418909      -0.8042181     0.007238572    */
    /*  TH_ELEM1883VAR47         Time-History Element 1883 Variable 47    500            1               1               1    */
    /*  TH_ELEM1883VAR48         Time-History Element 1883 Variable 48    500 126.07312804       -228.9241         372.497    */
    /*  TH_ELEM1883VAR49         Time-History Element 1883 Variable 49    500 226.12876628       -2.378552         395.032    */
    /*  TH_ELEM1883VAR50         Time-History Element 1883 Variable 50    500 95.952641055       -8.563899         206.379    */
    /*  TH_ELEM768VAR1319        Time-History Element 768 Variable 1319   500 74.454696506               0        98.99322    */
    /*  TH_ELEM768VAR1320        Time-History Element 768 Variable 1319   500 2.7056275E-9     2.685411E-9     2.719253E-9    */
    /*  TH_ELEM768VAR1321        Time-History Element 768 Variable 1319   500 0.1359897314               0       0.1775392    */
    /*  TH_ELEM768VAR1322        Time-History Element 768 Variable 1319   500          300             300             300    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC          13:06 Tuesday, June  2, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx

    NOTE: Library slchelp assigned as follows:
          Engine:        WPD
          Physical Name: C:\Progra~1\Altair\SLC\2026\sashelp


    LOG:  13:06:31
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.031
          cpu time  : 0.031


    NOTE: Format num2mis output
    NOTE: Format $chr2mis output
    NOTE: Procedure format step took :
          real time : 0.015
          cpu time  : 0.000


    NOTE: AUTOEXEC processing completed

    1         libname workx sas7bdat "d:/wpswrkx"; /*--- put both of these in your autoexec file ---*/
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    2         libname wpdx wpd "d:/wpswrkx";  /*--- put both of these in your autoexec file ---*/
    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx

    3
    4         options set=PYTHONHOME "D:\py314";
    5         proc python;
    6         submit;
    7         import pandas as pd
    8         df = pd.read_csv("d:/rad/ImpactT01.csv")
    9         df.columns = df.columns.str.replace(r"\s+", "", regex=True)
    10        print(df);
    11        endsubmit;

    NOTE: Submitting statements to Python:


    12        import python=df data=wpdx.df;
    NOTE: Creating data set 'WPDX.df' from Python data frame 'df'
    NOTE: Data set "WPDX.df" has 500 observation(s) and 1323 variable(s)

    13        run;
    NOTE: Procedure python step took :
          real time : 1.877
          cpu time  : 0.078


    14
    15        data wpdx.time_hist;
    16        label
    17          TIME                      = "Time"
    18          INTERNALENERGY            = "Internal Energy"
    19          KINETICENERGY             = "Kinetic Energy"
    20          X_MOMENTUM                = "X Momentum"
    21          Y_MOMENTUM                = "Y Momentum"
    22          Z_MOMENTUM                = "Z Momentum"
    23          MASS                      = "Mass"
    24          TIMESTEP                  = "Time Step"
    25          ROTATIONENERGY            = "Rotation Energy"
    26          EXTERNALWORK              = "External Work"
    27          SPRINGENERGY              = "Spring Energy"
    28          CONTACTENERGY             = "Contact Energy"
    29          HOURGLASSENERGY           = "Hourglass Energy"
    30          ELASTICCONTACTENERGY      = "Elastic Contact Energy"
    31          FRICTIONALCONTACTENERGY   = "Frictional Contact Energy"
    32          DAMPINGCONTACTENERGY      = "Damping Contact Energy"
    33          PLASTICWORK               = "Plastic Work"
    34          ADDEDMASS                 = "Added Mass"
    35          PERCENTAGEADDEDMASS       = "Percentage Added Mass"
    36          INLETMASS                 = "Inlet Mass"
    37          OUTLETMASS                = "Outlet Mass"
    38          INLETENERGY               = "Inlet Energy"
    39          OUTLETENERGY              = "Outlet Energy"
    40          PLATEIE                   = "Plate Internal Energy"
    41          PLATEKE                   = "Plate Kinetic Energy"
    42          PLATEXMOM                 = "Plate X Momentum"
    43          PLATEYMOM                 = "Plate Y Momentum"
    44          PLATEZMOM                 = "Plate Z Momentum"
    45          PLATEMASS                 = "Plate Mass"
    46          PLATEHE                   = "Plate Total Energy"
    47          PLATEERODED               = "Plate Eroded"
    48          PLATEHEAT                 = "Plate Heat"
    49          IMPACTORIE                = "Impactor Internal Energy"
    50          IMPACTORKE                = "Impactor Kinetic Energy"
    51          IMPACTORXMOM              = "Impactor X Momentum"
    52          IMPACTORYMOM              = "Impactor Y Momentum"
    53          IMPACTORZMOM              = "Impactor Z Momentum"
    54          IMPACTORMASS              = "Impactor Mass"
    55          IMPACTORHE                = "Impactor Total Energy"
    56          IMPACTORERODED            = "Impactor Eroded"
    57          IMPACTORHEAT              = "Impactor Heat"
    58
    59          TH_INTER1GROUP1VAR41      = "Time-History Inter 1 Group 1 Variable 41"
    60          TH_INTER1GROUP1VAR42      = "Time-History Inter 1 Group 1 Variable 42"
    61          TH_INTER1GROUP1VAR43      = "Time-History Inter 1 Group 1 Variable 43"
    62          TH_INTER1GROUP1VAR44      = "Time-History Inter 1 Group 1 Variable 44"
    63          TH_INTER1GROUP1VAR45      = "Time-History Inter 1 Group 1 Variable 45"
    64          TH_INTER1GROUP1VAR46      = "Time-History Inter 1 Group 1 Variable 46"
    65
    66          TH_ELEM1883VAR47          = "Time-History Element 1883 Variable 47"
    67          TH_ELEM1883VAR48          = "Time-History Element 1883 Variable 48"
    68          TH_ELEM1883VAR49          = "Time-History Element 1883 Variable 49"
    69          TH_ELEM1883VAR50          = "Time-History Element 1883 Variable 50"
    70
    71          /*--- ... repeat pattern for all TH_ELEM variables up to TH_ELEM768VAR1319 ...
    72                    see complete_time,sas in this repo for all 1320 ariables
    73                    last 4 variables below
    74           ---*/
    75
    76          TH_ELEM768VAR1319     = "Time-History Element 768 Variable 1319"
    77          TH_ELEM768VAR1320     = "Time-History Element 768 Variable 1319"
    78          TH_ELEM768VAR1321     = "Time-History Element 768 Variable 1319"
    79          TH_ELEM768VAR1322     = "Time-History Element 768 Variable 1319"
    80         ;
    81
    82         /*--- THE ~1300 DROPPED VARIABLES GIVE DETAIL CELL VALUES - YOU MAY WANT TO RESHAPE ---*/
    83
    84         set wpdx.df(drop=TH_ELEM1883VAR51--TH_ELEM768VAR1318);
    85         run;

    NOTE: 500 observations were read from "WPDX.df"
    NOTE: Data set "WPDX.time_hist" has 500 observation(s) and 55 variable(s)
    NOTE: The data step took :
          real time : 0.079
          cpu time  : 0.015


    86
    87        options label;
    88        proc contents data=wpdx.time_hist position;
    89        run;
    NOTE: Procedure contents step took :
          real time : 0.031
          cpu time  : 0.015


    90
    91        proc means data=wpdx.time_hist n mean min max;
    92        run;
    NOTE: 500 observations were read from "WPDX.time_hist"
    NOTE: Procedure means step took :
          real time : 0.094
          cpu time  : 0.093


    93
    94
    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 2.329
          cpu time  : 0.343

    /*---
      ___                                       _       _
    | ___|  _ __ ___   __ _ _ __  _   _   _ __ | | ___ | |_ ___
    |___ \ | `_ ` _ \ / _` | `_ \| | | | | `_ \| |/ _ \| __/ __|
     ___) || | | | | | (_| | | | | |_| | | |_) | | (_) | |_\__ \
    |____/ |_| |_| |_|\__,_|_| |_|\__, | | .__/|_|\___/ \__|___/
                                  |___/  |_|
    ---*/

    %utlfkil(d:/rad/energy_evolution.png);

    ods listing close;
    ods graphics on / reset=all imagename="energy_evolution" outputfmt=png;
    ods printer file="d:/rad/energy_evolution.png" dpi=100;
    proc sgplot data=workx.time_hist;

        title "Internal Energy & Elastic Contact Energy";
        title2 "Internal vs Elastic Contact Energy";


        series x=time y=INTERNALENERGY /
               lineattrs=(color=blue thickness=2)
               name="Internal"
               legendlabel="Internal Energy";


        series x=time y=KINETICENERGY /
               lineattrs=(color=red thickness=2)
               y2axis
               name="Kinetic"
               legendlabel="Kinetic Energy";

        series x=time y=PLASTICWORK          /
               lineattrs=(color=green thickness=2 )
               name="PlasticWork"
               legendlabel="PasticWork";


        refline 0.000148 / axis=x label="Max Deformation"
                    lineattrs=(color=blue pattern=dash thickness=1.5);

        xaxis label="Time" grid;
        yaxis label="Internal & Plastic Work  " grid;
        y2axis label="Kinetic Energy";

    run;


    %utlfkil(d:/rad/ymomentumevolve.png);

    ods listing close;
    ods graphics on / reset=all imagename="ymomentumevolve" outputfmt=png;
    ods printer file="d:/rad/ymomentumevolve.png" dpi=100;

    proc sgplot data=workx.time_hist;
        title "Y-Momentum Evolution";
        title2 "Primary Direction Impulse";

        series x=time y=Y_MOMENTUM /
               lineattrs=(color=darkblue thickness=2)
               markerattrs=(color=darkblue symbol=circlefilled size=5);

         refline 0.000148 / axis=x label="Max Deformation"
                    lineattrs=(color=blue pattern=dash thickness=1.5);

        xaxis label="Time" grid;
        yaxis label="Y-Momentum" grid;
    run;

    ods printer close;
    ods _all_ close;
    ods listing;


    %utlfkil(d:/rad/zmomentumevolve.png);

    ods listing close;
    ods graphics on / reset=all imagename="xmomentumevolve" outputfmt=png;
    ods printer file="d:/rad/zmomentumevolve.png" dpi=100;

    proc sgplot data=workx.time_hist;
        title "Z-Momentum Evolution";
        title2 "Primary Direction Impulse";

        series x=time y=Z_MOMENTUM /
               lineattrs=(color=darkblue thickness=2)
               markerattrs=(color=darkblue symbol=circlefilled size=5);

        xaxis label="Time" grid;
        yaxis label="Z-Momentum" grid;

         refline 0.000148 / axis=x label="Max Deformation"
                    lineattrs=(color=blue pattern=dash thickness=1.5);
    run;

    ods printer close;
    ods _all_ close;
    ods listing;


    %utlfkil(d:/rad/xmomentumevolve.png);

    ods listing close;
    ods graphics on / reset=all imagename="xmomentumevolve" outputfmt=png;
    ods printer file="d:/rad/xmomentumevolve.png" dpi=100;

    proc sgplot data=workx.time_hist;
        title "X-Momentum Evolution";
        title2 "Primary Direction Impulse";

        series x=time y=X_MOMENTUM /
               lineattrs=(color=darkblue thickness=2)
               markerattrs=(color=darkblue symbol=circlefilled size=5);

        xaxis label="Time" grid;
        yaxis label="X-Momentum" grid;

         refline 0.000148 / axis=x label="Max Deformation"
                    lineattrs=(color=blue pattern=dash thickness=1.5);
    run;

    ods printer close;
    ods _all_ close;
    ods listing;


    %utlfkil(d:/rad/timestephistory.png);

    ods listing close;
    ods graphics on / reset=all imagename="timestephistory" outputfmt=png;
    ods printer file="d:/rad/timestephistory.png" dpi=100;

    /* Time step history with change detection */
    proc sgplot data=workx.time_hist;
        title "Time Step Evolution";
        title2 "Solver Adaptation to Simulation Complexity";

        /* Use scatter for better visibility of changes */
        scatter x=time y=TIMESTEP /
                markerattrs=(color=red symbol=circle size=6);

        /* Smooth line through the points */
        pbspline x=time y=TIMESTEP /
                 lineattrs=(color=blue thickness=1)
                 nomarkers;

         refline 0.000148 / axis=x label="Max Deformation"
                    lineattrs=(color=blue pattern=dash thickness=1.5);


        xaxis label="Time" grid;
        yaxis label="Time Step"
              type=log /* Log scale often helpful for time step */
              logbase=10
              logstyle=linear
              grid;

    run;quit;

    ods printer close;
    ods graphics off;
    ods listing;


    %macro plts(var);

        %*let var=xmomentumevolve;

        %utlfkil(d:/rad/&var..png);

        ods listing close;
        ods graphics on / reset=all imagename="&var" outputfmt=png;
        ods printer file="d:/rad/&var..png" dpi=100;

        proc sgplot data=workx.time_hist;
            title "X-&var";

            series x=time y=&var /
                   lineattrs=(color=darkblue thickness=2)
                   markerattrs=(color=darkblue symbol=circlefilled size=5);

            xaxis label="Time" grid;
            yaxis label="&var" grid;

        refline 0.000148 / axis=x label="Max Deformation"
                    lineattrs=(color=blue pattern=dash thickness=1.5);

        run;

        ods printer close;
        ods _all_ close;
        ods listing;

    %mend plts;

    %plts(PlateZmom);
    %plts(RotationEnergy);
    %plts(ContactEnergy);
    %plts(HourGlassEnergy);
    %plts(ElasticContactEnergy);
    %plts(FrictionalContactEnergy);

    /*                         _                    _               _
     ___  __ _ _ __ ___  _ __ | | ___    ___  _   _| |_ _ __  _   _| |_
    / __|/ _` | `_ ` _ \| `_ \| |/ _ \  / _ \| | | | __| `_ \| | | | __|
    \__ \ (_| | | | | | | |_) | |  __/ | (_) | |_| | |_| |_) | |_| | |_
    |___/\__,_|_| |_| |_| .__/|_|\___|  \___/ \__,_|\__| .__/ \__,_|\__|
                        |_|                            |_|
    */
                    Simulating The deformation of a plate when impacked by a sold ball
    /**************************************************************************************************************************/
    /*                             Energies are within the plate                                                              */
    /*                                                                                                                        */
    /*                        Plot of INTERNALENERGY*TIME.  Symbol used is 'i'                                                */
    /*                        Plot of PLASTICWORK*TIME.     Symbol used is 'p'                                                */
    /*                        Plot of INTERNALENERGY*TIME   Symbol used is 'i'                                                */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*                                               TIME                                                                     */
    /*              0.0000       0.0001       0.0002       0.0003       0.0004       0.0005                                   */
    /*     Internal ---+------------+------------+------------+------------+------------+------- Kinetic                      */
    /*       Energy |                       |                                                  | Energy                       */
    /*              | Plate Deformation Energies                                               |                              */
    /*       900000 +                       |              Internal Energy                     + 1020000                      */
    /*              |                       |   iiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiiii      |                              */
    /*              | kk Ball Touches Plate |  ii  Kinetic Energy is converted to Internal    |                               */
    /*              |  kk                   |ii,                                               |                              */
    /*              |   kk                  ii                                                 |                              */
    /*       800000 +     k                 i                                                  + 1000000                      */
    /*              |     kk Plate Deforms i|                                                  |                              */
    /*              |      kk              i|                                                  |                              */
    /*              |       kk            i |<-Maximum Plate Deformatiom before cracks?        |                              */
    /*              |        k            i |                                                  |                              */
    /*       700000 +kinetic kk          i  |                                                  +  980000                      */
     /*              |energy-> kk         i  |                                                  |                              */
    /*              |          k         i pp                                                  |                              */
    /*              |          kk       i  pppppp           Plastic Work                       |                              */
    /*              |           k       i pp|ppppppppppppppppppppppppppppppppppppppppppppp     |  960000                      */
    /*       600000 +           kk     ii p |                                                  +                              */
    /*              |            k     i pp |                                                  |                              */
    /*              |             k    i p  |                                                  |                              */
    /*              |             k   i  p  |                                                  |                              */
    /*              |              k  i p   |                                                  |                              */
    /*       500000 +              k ii p   |<- 0.00015                                       +  940000                       */
    /*              |               ki pp   |                                                  |                              */
    /*              |               ki p    |                                                  |                              */
    /*              |               ik p    |<-Maximum Plate Deformatiom before cracks?        |                              */
    /*              |               ikp     |                                                  |                              */
    /*       400000 +              iikp     |                                                  +  920000                      */
    /*              |              i pp     |                                                  |                              */
    /*              |             ii pkk    |                                                  |                              */
    /*              |             i pp k    |                                                  |                              */
    /*              |             i p  kk   |                                                  |                              */
    /*       300000 +            i pp   k   |                                                  +  900000                      */
    /*              |            i p    k   |                                                  |                              */
    /*              |           i pp     k  |                                                  |                              */
    /*              |  Internal i p      kk |                                                  |                              */
    /*              |          i pp       k |                                                  |                              */
    /*       200000 +          i p        kk|                                                  +  880000                      */
    /*              |         iipp         k|                                                  |                              */
    /*              |  Energy i p           |k                                                 |                              */
    /*              |        i pp           |kk                                                |                              */
    /*              |       ii p            | kkk                                              |                              */
    /*       100000 +       i p             |   kkk                                            +  860000                      */
    /*              |      i pp             |    kk                                            |                              */
    /*              |     iipp              |      kk                                          |                              */
    /*              |    iipp Plastic Work  |        kk                                        |                              */
    /*              |   iipp                |          kk  Kinetic Energy                      |                              */
    /*            0 +  iip                  |            kkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkkk     +  840000                      */
    /*              |                       |                                                  |                              */
    /*              ---+------------+------------+------------+------------+------------+-------                              */
    /*              0.0000       0.0001       0.0002       0.0003       0.0004       0.0005                                   */
    /*                                                      TIME                                                              */
    /**************************************************************************************************************************/

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC        12:54 Wednesday, June  3, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"

    NOTE: AUTOEXEC processing completed

    1         %utlfkil(d:/rad/energy_evolution.png);
    2
    3         ods listing close;
    4         ods graphics on / reset=all imagename="energy_evolution" outputfmt=png;
    5         ods printer file="d:/rad/energy_evolution.png" dpi=100;
    WARNING: ODS PRINTER is currently EXPERIMENTAL and is subject to change
    6         proc sgplot data=wpdx.time_hist;
    7
    8             title "Internal Energy & Elastic Contact Energy";
    9             title2 "Internal vs Elastic Contact Energy";
    10
    11
    12            series x=time y=INTERNALENERGY /
    13                   lineattrs=(color=blue thickness=2)
    14                   name="Internal"
    15                   legendlabel="Internal Energy";
    16
    17
    18            series x=time y=KINETICENERGY /
    19                   lineattrs=(color=red thickness=2)
    20                   y2axis
    21                   name="Kinetic"
    22                   legendlabel="Kinetic Energy";
    23
    24            series x=time y=PLASTICWORK          /
    25                   lineattrs=(color=green thickness=2 )
    26                   name="PlasticWork"
    27                   legendlabel="PasticWork";
    28
    29
    30            refline 0.000148 / axis=x label="Max Deformation"
    31                        lineattrs=(color=blue pattern=dash thickness=1.5);
    32
    33            xaxis label="Time" grid;
    34            yaxis label="Internal & Plastic Work  " grid;
    35            y2axis label="Kinetic Energy";
    36
    37        run;
    NOTE: Procedure sgplot step took :
          real time : 0.173
          cpu time  : 0.328


    38
    39
    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 0.525
          cpu time  : 0.515
    NOTE: Writing file d:\rad\energy_evolution.png


    /*__                    _                 _   _               _               _   _       __ _ _
     / /_    __ _ _ __ ___ (_)_ __ ___   __ _| |_(_) ___  _ __   | |_ ___  __   _| |_| | __  / _(_) | ___  ___
    | `_ \  / _` | `_ ` _ \| | `_ ` _ \ / _` | __| |/ _ \| `_ \  | __/ _ \ \ \ / / __| |/ / | |_| | |/ _ \/ __|
    | (_) || (_| | | | | | | | | | | | | (_| | |_| | (_) | | | | | || (_) | \ V /| |_|   <  |  _| | |  __/\__ \
     \___/  \__,_|_| |_| |_|_|_| |_| |_|\__,_|\__|_|\___/|_| |_|  \__\___/   \_/  \__|_|\_\ |_| |_|_|\___||___/
    */

    /*--- CONVERT ANIMATION FILES TO VTK ---*/

    options validvarname=v7;
    options set=PYTHONHOME "D:\py314";
    proc python;
    submit;
    import subprocess
    import os
    from pathlib import Path

    # Binary-safe conversion
    rad_dir = Path("D:/rad")
    converter = Path("C:/openradioss/exec/anim_to_vtk_win64.exe")

    # Find all ANIM files (no extension, contains pattern)
    anim_files = [f for f in rad_dir.iterdir()
                  if f.is_file() and "ImpactA" in f.name and f.suffix == ""]

    for anim_file in sorted(anim_files):
        output_file = anim_file.with_suffix(".vtk")
        print(f"Converting: {anim_file.name}")

        # Binary-safe: Use subprocess with stdout capture as bytes
        result = subprocess.run(
            [str(converter), str(anim_file)],
            capture_output=True,
            check=False
        )

        # Write binary output directly (no text conversion)
        with open(output_file, 'wb') as f:
            f.write(result.stdout)

        if result.returncode == 0 and output_file.stat().st_size > 0:
            # Verify VTK header
            with open(output_file, 'rb') as f:
                if f.read(5) == b'# vtk':
                    print(f"  [OK] Valid VTK file ({output_file.stat().st_size} bytes)")
                else:
                    print(f"  [WARNING] Invalid VTK header")
        else:
            print(f"  [FAILED] Return code: {result.returncode}")
    endsubmit;
    run;

    /**************************************************************************************************************************/
    /*| Altair SLC                                                                                                            */
    /*| The PYTHON Procedure                                                                                                  */
    /*|                                                                                                                       */
    /*| Converting: ImpactA001                                                                                                */
    /*|   [OK] Valid VTK file (2586124 bytes)                                                                                 */
    /*| Converting: ImpactA002                                                                                                */
    /*|   [OK] Valid VTK file (4322643 bytes)                                                                                 */
    /*| Converting: ImpactA003                                                                                                */
    /*|   [OK] Valid VTK file (4302538 bytes)                                                                                 */
    /*| ...                                                                                                                   */
    /*| Converting: ImpactA034                                                                                                */
    /*|   [OK] Valid VTK file (4215530 bytes)                                                                                 */
    /*| Converting: ImpactA035                                                                                                */
    /*|   [OK] Valid VTK file (4215571 bytes)                                                                                 */
    /*| Converting: ImpactA036                                                                                                */
    /*|                                                                                                                       */
    /*|   [OK] Valid VTK file (4226430 bytes)                                                                                 */
    /**************************************************************************************************************************/
    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC        09:28 Wednesday, June  3, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"

    NOTE: AUTOEXEC processing completed

    1
    2         options validvarname=v7;
    3         options set=PYTHONHOME "D:\py314";
    4         proc python;
    5         submit;
    6         import subprocess
    7         import os
    8         from pathlib import Path
    9
    10        # Binary-safe conversion
    11        rad_dir = Path("D:/rad")
    12        converter = Path("C:/openradioss/exec/anim_to_vtk_win64.exe")
    13
    14        # Find all ANIM files (no extension, contains pattern)
    15        anim_files = [f for f in rad_dir.iterdir()
    16                      if f.is_file() and "ImpactA" in f.name and f.suffix == ""]
    17
    18        for anim_file in sorted(anim_files):
    19            output_file = anim_file.with_suffix(".vtk")
    20            print(f"Converting: {anim_file.name}")
    21
    22            # Binary-safe: Use subprocess with stdout capture as bytes
    23            result = subprocess.run(
    24                [str(converter), str(anim_file)],
    25                capture_output=True,
    26                check=False
    27            )
    28
    29            # Write binary output directly (no text conversion)
    30            with open(output_file, 'wb') as f:
    31                f.write(result.stdout)
    32
    33            if result.returncode == 0 and output_file.stat().st_size > 0:
    34                # Verify VTK header
    35                with open(output_file, 'rb') as f:
    36                    if f.read(5) == b'# vtk':
    37                        print(f"  [OK] Valid VTK file ({output_file.stat().st_size} bytes)")
    38                    else:
    39                        print(f"  [WARNING] Invalid VTK header")
    40            else:
    41                print(f"  [FAILED] Return code: {result.returncode}")
    42        endsubmit;

    NOTE: Submitting statements to Python:

    43        run;
    NOTE: Procedure python step took :
          real time : 1:04.306
          cpu time  : 0:00.109

    44
    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 1:04.555
          cpu time  : 0:00.250


    /*____         _   _      _                _   _    _         _  __
    |___  | __   _| |_| | __ | |_ ___   __   _| |_| | _| |__   __| |/ _|
       / /  \ \ / / __| |/ / | __/ _ \  \ \ / / __| |/ / `_ \ / _` | |_
      / /    \ V /| |_|   <  | || (_) |  \ V /| |_|   <| | | | (_| |  _|
     /_/      \_/  \__|_|\_\  \__\___/    \_/  \__|_|\_\_| |_|\__,_|_|

    */

    %slc_pvpybegin;
    cards4;
    #!/usr/bin/env python
    """
    Convert a series of VTK files into a single, transient VTKHDF file.
    This script is designed to be run with ParaView's pvpython executable.
    """

    from paraview.simple import *
    import os
    import glob

    def convert_vtk_series_to_vtkhdf(file_pattern, output_file, compression_level=4):
        """
        Convert a series of VTK files into a single VTKHDF file.

        Args:
            file_pattern (str): Glob pattern matching your VTK files (e.g., "path/to/anim_*.vtk").
            output_file (str): Output filename (must end with .vtkhdf).
            compression_level (int): Compression level (0-9) for the HDF5 file.
                                     4 provides a good balance between size and speed.
        """
        # Get list of files sorted alphabetically
        vtk_files = sorted(glob.glob(file_pattern))

        if not vtk_files:
            print(f"ERROR: No files found matching pattern '{file_pattern}'")
            return

        print(f"Found {len(vtk_files)} VTK files to convert.")

        # Create a reader for the file series
        # Using LegacyVTKReader for .vtk files
        print("Loading file series...")
        reader = LegacyVTKReader(FileNames=vtk_files)

        # Save the data as a VTKHDF file
        print(f"Saving to {output_file}...")
        SaveData(
            output_file,
            proxy=reader,
            WriteAllTimeSteps=1,      # Save all time steps into one file
            CompressionLevel=compression_level
        )
        print("Conversion complete!")


    if __name__ == "__main__":
        # --- CONFIGURATION ---
        # Update these paths for your specific case
        INPUT_FILE_PATTERN = "D:/rad/Impact*.vtk"
        OUTPUT_FILE = "D:/rad/Impact.vtkhdf"

        convert_vtk_series_to_vtkhdf(INPUT_FILE_PATTERN, OUTPUT_FILE)
    ;;;;
    %slc_pvpyend;

    /**************************************************************************************************************************/
    /* Altair SLC                                                                                                             */
    /* Found 51 VTK files to convert.                                                                                         */
    /* Loading file series...                                                                                                 */
    /* Saving to D:/rad/Impact.vtkhdf...                                                                                      */
    /* Conversion complete!                                                                                                   */
    /**************************************************************************************************************************/

    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC        09:37 Wednesday, June  3, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"

    NOTE: AUTOEXEC processing completed

    1         %slc_pvpybegin;
    The file c:/temp/py_pgm.py does not exist
    2         cards4;

    NOTE: The file 'c:\temp\py_pgmx.py' is:
          Filename='c:\temp\py_pgmx.py',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=13:21:25 Jan 12 2026,
          Last Accessed=09:37:03 Jun 03 2026,
          Last Modified=09:37:03 Jun 03 2026,
          Lrecl=32767, Recfm=V

    NOTE: 52 records were written to file 'c:\temp\py_pgmx.py'
          The minimum record length was 80
          The maximum record length was 94
    NOTE: The data step took :
          real time : 0.016
          cpu time  : 0.015


    3         #!/usr/bin/env python
    4         """
    5         Convert a series of VTK files into a single, transient VTKHDF file.
    6         This script is designed to be run with ParaView's pvpython executable.
    7         """
    8
    9         from paraview.simple import *
    10        import os
    11        import glob
    12
    13        def convert_vtk_series_to_vtkhdf(file_pattern, output_file, compression_level=4):
    14            """
    15            Convert a series of VTK files into a single VTKHDF file.
    16
    17            Args:
    18                file_pattern (str): Glob pattern matching your VTK files (e.g., "path/to/anim_*.vtk").
    19                output_file (str): Output filename (must end with .vtkhdf).
    20                compression_level (int): Compression level (0-9) for the HDF5 file.
    21                                         4 provides a good balance between size and speed.
    22            """
    23            # Get list of files sorted alphabetically
    24            vtk_files = sorted(glob.glob(file_pattern))
    25
    26            if not vtk_files:
    27                print(f"ERROR: No files found matching pattern '{file_pattern}'")
    28                return
    29
    30            print(f"Found {len(vtk_files)} VTK files to convert.")
    31
    32            # Create a reader for the file series
    33            # Using LegacyVTKReader for .vtk files
    34            print("Loading file series...")
    35            reader = LegacyVTKReader(FileNames=vtk_files)
    36
    37            # Save the data as a VTKHDF file
    38            print(f"Saving to {output_file}...")
    39            SaveData(
    40                output_file,
    41                proxy=reader,
    42                WriteAllTimeSteps=1,      # Save all time steps into one file
    43                CompressionLevel=compression_level
    44            )
    45            print("Conversion complete!")
    46
    47
    48        if __name__ == "__main__":
    49            # --- CONFIGURATION ---
    50            # Update these paths for your specific case
    51            INPUT_FILE_PATTERN = "D:/rad/Impact*.vtk"
    52            OUTPUT_FILE = "D:/rad/Impact.vtkhdf"
    53
    54            convert_vtk_series_to_vtkhdf(INPUT_FILE_PATTERN, OUTPUT_FILE)
    55        ;;;;
    56        %slc_pvpyend;

    NOTE: The infile 'c:\temp\py_pgmx.py' is:
          Filename='c:\temp\py_pgmx.py',
          Owner Name=SLC\suzie,
          File size (bytes)=4281,
          Create Time=13:21:25 Jan 12 2026,
          Last Accessed=09:37:03 Jun 03 2026,
          Last Modified=09:37:03 Jun 03 2026,
          Lrecl=32767, Recfm=V

    NOTE: The file 'c:\temp\py_pgm.py' is:
          Filename='c:\temp\py_pgm.py',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=16:38:15 May 12 2026,
          Last Accessed=09:37:03 Jun 03 2026,
          Last Modified=09:37:03 Jun 03 2026,
          Lrecl=32767, Recfm=V

    #!/usr/bin/env python
    """
    Convert a series of VTK files into a single, transient VTKHDF file.
    This script is designed to be run with ParaView's pvpython executable.
    """

    from paraview.simple import *
    import os
    import glob

    def convert_vtk_series_to_vtkhdf(file_pattern, output_file, compression_level=4):
        """
        Convert a series of VTK files into a single VTKHDF file.

        Args:
            file_pattern (str): Glob pattern matching your VTK files (e.g., "path/to/anim_*.vtk").
            output_file (str): Output filename (must end with .vtkhdf).
            compression_level (int): Compression level (0-9) for the HDF5 file.
                                     4 provides a good balance between size and speed.
        """
        # Get list of files sorted alphabetically
        vtk_files = sorted(glob.glob(file_pattern))

        if not vtk_files:
            print(f"ERROR: No files found matching pattern '{file_pattern}'")
            return

        print(f"Found {len(vtk_files)} VTK files to convert.")

        # Create a reader for the file series
        # Using LegacyVTKReader for .vtk files
        print("Loading file series...")
        reader = LegacyVTKReader(FileNames=vtk_files)

        # Save the data as a VTKHDF file
        print(f"Saving to {output_file}...")
        SaveData(
            output_file,
            proxy=reader,
            WriteAllTimeSteps=1,      # Save all time steps into one file
            CompressionLevel=compression_level
        )
        print("Conversion complete!")


    if __name__ == "__main__":
        # --- CONFIGURATION ---
        # Update these paths for your specific case
        INPUT_FILE_PATTERN = "D:/rad/Impact*.vtk"
        OUTPUT_FILE = "D:/rad/Impact.vtkhdf"

        convert_vtk_series_to_vtkhdf(INPUT_FILE_PATTERN, OUTPUT_FILE)
    NOTE: 52 records were read from file 'c:\temp\py_pgmx.py'
          The minimum record length was 80
          The maximum record length was 94
    NOTE: 52 records were written to file 'c:\temp\py_pgm.py'
          The minimum record length was 80
          The maximum record length was 94
    NOTE: The data step took :
          real time : 0.015
          cpu time  : 0.015



    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=C:\Progra~1\ParaView-6.1.0-Windows-Python3.12-msvc2017-AMD64\bin\pvpython.exe c:/temp/py_pgm.py 2> c:/temp/py_pgm.log,
          Lrecl=32767, Recfm=V

    Found 51 VTK files to convert.
    Loading file series...
    Saving to D:/rad/Impact.vtkhdf...
    Conversion complete!
    NOTE: 4 records were written to file PRINT

    NOTE: 4 records were read from file rut
          The minimum record length was 20
          The maximum record length was 33
    NOTE: The data step took :
          real time : 39.329
          cpu time  : 0.062



    NOTE: The infile 'c:\temp\py_pgm.log' is:
          Filename='c:\temp\py_pgm.log',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=11:45:37 May 12 2026,
          Last Accessed=09:37:03 Jun 03 2026,
          Last Modified=09:37:03 Jun 03 2026,
          Lrecl=32767, Recfm=V

    NOTE: No records were read from file 'c:\temp\py_pgm.log'
    NOTE: The data step took :
          real time : 0.016
          cpu time  : 0.000


    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 39.969
          cpu time  : 0.312


    /*___         _   _       _  __   _
     ( _ ) __   _| |_| | ____| |/ _| | |_ ___     ___ _____   __
     / _ \ \ \ / / __| |/ / _` | |_  | __/ _ \   / __/ __\ \ / /
    | (_) | \ V /| |_|   < (_| |  _| | || (_) | | (__\__ \\ V /
     \___/   \_/  \__|_|\_\__,_|_|    \__\___/   \___|___/ \_/

    */

    /**************************************************************************************************************************/
    /* Create CSVs                                                                                                            */
    /*                                                                                                                        */
    /* d:/rad                                                                                                                 */
    /*   global_energy_data.csv                                                                                               */
    /*   cell_data.csv                                                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    %slc_pvpybegin;
    cards4;
    #!/usr/bin/env python
    """
    Extract ALL stress, strain, and energy data from VTKHDF.
    Run with: pvpython this_script.py
    """

    from paraview.simple import *
    from paraview import servermanager
    import csv
    import os

    # ------------------------------------------------------------
    # CONFIGURATION
    # ------------------------------------------------------------
    VTKHDF_FILE = "D:/rad/Impact.vtkhdf"
    OUTPUT_CSV = "D:/rad/Impact.csv"

    # ------------------------------------------------------------
    # LOAD THE DATA
    # ------------------------------------------------------------
    print(f"Loading file: {VTKHDF_FILE}")
    source = OpenDataFile(VTKHDF_FILE)
    source.UpdatePipeline()

    # ------------------------------------------------------------
    # CHECK WHAT DATA IS AVAILABLE
    # ------------------------------------------------------------
    print("\n--- Available Data Arrays ---")
    print(f"Point Data: {list(source.PointData.keys())}")
    print(f"Cell Data: {list(source.CellData.keys())}")

    # Get timesteps
    timesteps = source.TimestepValues
    print(f"\nNumber of timesteps: {len(timesteps)}")

    # ------------------------------------------------------------
    # CREATE AN INTEGRATE VARIABLES FILTER FOR GLOBAL TOTALS
    # ------------------------------------------------------------
    print("\nCalculating global integrated quantities...")
    integrate = IntegrateVariables(Input=source)

    # ------------------------------------------------------------
    # METHOD 1: Export global integrated data (energy totals)
    # ------------------------------------------------------------
    print("\nSaving global integrated data...")
    output_global = "D:/rad/global_energy_data.csv"
    SaveData(output_global, proxy=integrate, WriteTimeSteps=1, Precision=12)
    print(f"Global energy data saved to: {output_global}")

    # ------------------------------------------------------------
    # METHOD 2: Extract data for a specific point/region
    # ------------------------------------------------------------
    # If you want data for a specific point, use a threshold or clip filter
    # For example, to get data for the entire model, you can export cell data

    print("\nSaving cell data (if available)...")
    if len(source.CellData.keys()) > 0:
        output_cell = "D:/rad/cell_data.csv"
        SaveData(output_cell, proxy=source, WriteTimeSteps=1,
                 FieldAssociation='Cell Data', Precision=12)
        print(f"Cell data saved to: {output_cell}")

    # ------------------------------------------------------------
    # METHOD 3: Manual extraction of specific arrays
    # ------------------------------------------------------------
    print("\nExtracting specific arrays manually...")

    # Get a list of arrays you want to extract
    arrays_of_interest = ['GPS_SIGXX', 'GPS_SIGXY', 'GPS_SIGXZ', 'GPS_SIGYY',
                          'GPS_SIGZY', 'GPS_SIGZZ']

    # Check which arrays actually exist
    available_arrays = [arr for arr in arrays_of_interest if arr in source.PointData.keys()]

    if available_arrays:
        # Create a calculator to extract just these arrays
        calculator = Calculator(Input=source)
        calculator.ResultArrayName = 'Extracted_Data'
        calculator.Function = ' '.join(available_arrays)

        output_extracted = "D:/rad/extracted_stress_data.csv"
        SaveData(output_extracted, proxy=calculator, WriteTimeSteps=1, Precision=12)
        print(f"Extracted stress data saved to: {output_extracted}")
    else:
        print("No requested arrays found. Available arrays are:")
        print(f"  {list(source.PointData.keys())}")

    print("\n--- Summary ---")
    print(f"CSV files created in D:/rad/")
    print("  - global_energy_data.csv: Total internal/kinetic energy over time")
    print("  - cell_data.csv: Data for all cells (if available)")
    print("  - extracted_stress_data.csv: Specific stress components")

    # Verify files
    for f in ['global_energy_data.csv', 'cell_data.csv', 'extracted_stress_data.csv']:
        path = f"D:/rad/{f}"
        if os.path.exists(path) and os.path.getsize(path) > 0:
            size_kb = os.path.getsize(path) / 1024
            print(f"  âœ“ {f} ({size_kb:.2f} KB)")
        elif os.path.exists(path):
            print(f"   {f} (0 bytes - no data)")
        else:
            print(f"   {f} (not created)")
    ;;;;
    %slc_pvpyend;
    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /* Altair SLC                                                                                                             */
    /* Loading file: D:/rad/Impact.vtkhdf                                                                                     */
    /*                                                                                                                        */
    /* --- Available Data Arrays ---                                                                                          */
    /* Point Data: ['Acceleration', 'Contact_Forces', 'Displacement', 'Mass_Change', 'NODE_ID', 'Velocity']                   */
    /* Cell Data: ['3DELEM_Strs_Intg_Point111__', '3DELEM_Von_Mises', 'ELEMENT_ID', 'EROSION_STATUS', 'PART_ID',              */
    /*  'SPHELEM_Diameter', 'SPHELEM_Number_of_neighbours', 'SPHELEM_Strs_Intg_Point111__', 'SPHELEM_Von_Mises']              */
    /*                                                                                                                        */
    /* Number of timesteps: 51                                                                                                */
    /*                                                                                                                        */
    /* Calculating global integrated quantities...                                                                            */
    /*                                                                                                                        */
    /* Saving global integrated data...                                                                                       */
    /* Global energy data saved to: D:/rad/global_energy_data.csv                                                             */
    /*                                                                                                                        */
    /* Saving cell data (if available)...                                                                                     */
    /* Cell data saved to: D:/rad/cell_data.csv                                                                               */
    /*                                                                                                                        */
    /* Extracting specific arrays manually...                                                                                 */
    /* No requested arrays found. Available arrays are:                                                                       */
    /*   ['Acceleration', 'Contact_Forces', 'Displacement', 'Mass_Change', 'NODE_ID', 'Velocity']                             */
    /*                                                                                                                        */
    /* --- Summary ---                                                                                                        */
    /* CSV files created in D:/rad/                                                                                           */
    /*   - global_energy_data.csv: Total internal/kinetic energy over time                                                    */
    /*   - cell_data.csv: Data for all cells (if available)                                                                   */
    /*   - extracted_stress_data.csv: Specific stress components                                                              */
    /*   Ã¢Å“â€œ global_energy_data.csv (11.80 KB)                                                                            */
    /*   Ã¢Å“â€œ cell_data.csv (69403.20 KB)                                                                                  */
    /*    extracted_stress_data.csv (not created)                                                                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/


    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC         11:06 Thursday, June  4, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ï»¿ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx

    NOTE: Library slchelp assigned as follows:
          Engine:        WPD
          Physical Name: C:\Progra~1\Altair\SLC\2026\sashelp


    LOG:  11:06:30
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.031
          cpu time  : 0.015


    NOTE: Format num2mis output
    NOTE: Format $chr2mis output
    NOTE: Procedure format step took :
          real time : 0.016
          cpu time  : 0.000


    NOTE: AUTOEXEC processing completed

    1          %slc_pvpybegin;
    The file c:/temp/py_pgm.py does not exist
    2         cards4;

    NOTE: The file 'c:\temp\py_pgmx.py' is:
          Filename='c:\temp\py_pgmx.py',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=13:21:25 Jan 12 2026,
          Last Accessed=11:06:30 Jun 04 2026,
          Last Modified=11:06:30 Jun 04 2026,
          Lrecl=32767, Recfm=V

    NOTE: 103 records were written to file 'c:\temp\py_pgmx.py'
          The minimum record length was 80
          The maximum record length was 88
    NOTE: The data step took :
          real time : 0.000
          cpu time  : 0.000


    3         #!/usr/bin/env python
    4         """
    5         Extract ALL stress, strain, and energy data from VTKHDF.
    6         Run with: pvpython this_script.py
    7         """
    8
    9         from paraview.simple import *
    10        from paraview import servermanager
    11        import csv
    12        import os
    13
    14        # ------------------------------------------------------------
    15        # CONFIGURATION
    16        # ------------------------------------------------------------
    17        VTKHDF_FILE = "D:/rad/Impact.vtkhdf"
    18        OUTPUT_CSV = "D:/rad/Impact.csv"
    19
    20        # ------------------------------------------------------------
    21        # LOAD THE DATA
    22        # ------------------------------------------------------------
    23        print(f"Loading file: {VTKHDF_FILE}")
    24        source = OpenDataFile(VTKHDF_FILE)
    25        source.UpdatePipeline()
    26
    27        # ------------------------------------------------------------
    28        # CHECK WHAT DATA IS AVAILABLE
    29        # ------------------------------------------------------------
    30        print("\n--- Available Data Arrays ---")
    31        print(f"Point Data: {list(source.PointData.keys())}")
    32        print(f"Cell Data: {list(source.CellData.keys())}")
    33
    34        # Get timesteps
    35        timesteps = source.TimestepValues
    36        print(f"\nNumber of timesteps: {len(timesteps)}")
    37
    38        # ------------------------------------------------------------
    39        # CREATE AN INTEGRATE VARIABLES FILTER FOR GLOBAL TOTALS
    40        # ------------------------------------------------------------
    41        print("\nCalculating global integrated quantities...")
    42        integrate = IntegrateVariables(Input=source)
    43
    44        # ------------------------------------------------------------
    45        # METHOD 1: Export global integrated data (energy totals)
    46        # ------------------------------------------------------------
    47        print("\nSaving global integrated data...")
    48        output_global = "D:/rad/global_energy_data.csv"
    49        SaveData(output_global, proxy=integrate, WriteTimeSteps=1, Precision=12)
    50        print(f"Global energy data saved to: {output_global}")
    51
    52        # ------------------------------------------------------------
    53        # METHOD 2: Extract data for a specific point/region
    54        # ------------------------------------------------------------
    55        # If you want data for a specific point, use a threshold or clip filter
    56        # For example, to get data for the entire model, you can export cell data
    57
    58        print("\nSaving cell data (if available)...")
    59        if len(source.CellData.keys()) > 0:
    60            output_cell = "D:/rad/cell_data.csv"
    61            SaveData(output_cell, proxy=source, WriteTimeSteps=1,
    62                     FieldAssociation='Cell Data', Precision=12)
    63            print(f"Cell data saved to: {output_cell}")
    64
    65        # ------------------------------------------------------------
    66        # METHOD 3: Manual extraction of specific arrays
    67        # ------------------------------------------------------------
    68        print("\nExtracting specific arrays manually...")
    69
    70        # Get a list of arrays you want to extract
    71        arrays_of_interest = ['GPS_SIGXX', 'GPS_SIGXY', 'GPS_SIGXZ', 'GPS_SIGYY',
    72                              'GPS_SIGZY', 'GPS_SIGZZ']
    73
    74        # Check which arrays actually exist
    75        available_arrays = [arr for arr in arrays_of_interest if arr in source.PointData.keys()]
    76
    77        if available_arrays:
    78            # Create a calculator to extract just these arrays
    79            calculator = Calculator(Input=source)
    80            calculator.ResultArrayName = 'Extracted_Data'
    81            calculator.Function = ' '.join(available_arrays)
    82
    83            output_extracted = "D:/rad/extracted_stress_data.csv"
    84            SaveData(output_extracted, proxy=calculator, WriteTimeSteps=1, Precision=12)
    85            print(f"Extracted stress data saved to: {output_extracted}")
    86        else:
    87            print("No requested arrays found. Available arrays are:")
    88            print(f"  {list(source.PointData.keys())}")
    89
    90        print("\n--- Summary ---")
    91        print(f"CSV files created in D:/rad/")
    92        print("  - global_energy_data.csv: Total internal/kinetic energy over time")
    93        print("  - cell_data.csv: Data for all cells (if available)")
    94        print("  - extracted_stress_data.csv: Specific stress components")
    95
    96        # Verify files
    97        for f in ['global_energy_data.csv', 'cell_data.csv', 'extracted_stress_data.csv']:
    98            path = f"D:/rad/{f}"
    99            if os.path.exists(path) and os.path.getsize(path) > 0:
    100               size_kb = os.path.getsize(path) / 1024
    101               print(f"  Ã¢Å“â€œ {f} ({size_kb:.2f} KB)")
    102           elif os.path.exists(path):
    103               print(f"   {f} (0 bytes - no data)")
    104           else:
    105               print(f"   {f} (not created)")
    106       ;;;;
    107       %slc_pvpyend;

    NOTE: The infile 'c:\temp\py_pgmx.py' is:
          Filename='c:\temp\py_pgmx.py',
          Owner Name=SLC\suzie,
          File size (bytes)=8456,
          Create Time=13:21:25 Jan 12 2026,
          Last Accessed=11:06:30 Jun 04 2026,
          Last Modified=11:06:30 Jun 04 2026,
          Lrecl=32767, Recfm=V

    NOTE: The file 'c:\temp\py_pgm.py' is:
          Filename='c:\temp\py_pgm.py',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=16:38:15 May 12 2026,
          Last Accessed=11:06:30 Jun 04 2026,
          Last Modified=11:06:30 Jun 04 2026,
          Lrecl=32767, Recfm=V

    #!/usr/bin/env python
    """
    Extract ALL stress, strain, and energy data from VTKHDF.
    Run with: pvpython this_script.py
    """

    from paraview.simple import *
    from paraview import servermanager
    import csv
    import os

    # ------------------------------------------------------------
    # CONFIGURATION
    # ------------------------------------------------------------
    VTKHDF_FILE = "D:/rad/Impact.vtkhdf"
    OUTPUT_CSV = "D:/rad/Impact.csv"

    # ------------------------------------------------------------
    # LOAD THE DATA
    # ------------------------------------------------------------
    print(f"Loading file: {VTKHDF_FILE}")
    source = OpenDataFile(VTKHDF_FILE)
    source.UpdatePipeline()

    # ------------------------------------------------------------
    # CHECK WHAT DATA IS AVAILABLE
    # ------------------------------------------------------------
    print("\n--- Available Data Arrays ---")
    print(f"Point Data: {list(source.PointData.keys())}")
    print(f"Cell Data: {list(source.CellData.keys())}")

    # Get timesteps
    timesteps = source.TimestepValues
    print(f"\nNumber of timesteps: {len(timesteps)}")

    # ------------------------------------------------------------
    # CREATE AN INTEGRATE VARIABLES FILTER FOR GLOBAL TOTALS
    # ------------------------------------------------------------
    print("\nCalculating global integrated quantities...")
    integrate = IntegrateVariables(Input=source)

    # ------------------------------------------------------------
    # METHOD 1: Export global integrated data (energy totals)
    # ------------------------------------------------------------
    print("\nSaving global integrated data...")
    output_global = "D:/rad/global_energy_data.csv"
    SaveData(output_global, proxy=integrate, WriteTimeSteps=1, Precision=12)
    print(f"Global energy data saved to: {output_global}")

    # ------------------------------------------------------------
    # METHOD 2: Extract data for a specific point/region
    # ------------------------------------------------------------
    # If you want data for a specific point, use a threshold or clip filter
    # For example, to get data for the entire model, you can export cell data

    print("\nSaving cell data (if available)...")
    if len(source.CellData.keys()) > 0:
        output_cell = "D:/rad/cell_data.csv"
        SaveData(output_cell, proxy=source, WriteTimeSteps=1,
                 FieldAssociation='Cell Data', Precision=12)
        print(f"Cell data saved to: {output_cell}")

    # ------------------------------------------------------------
    # METHOD 3: Manual extraction of specific arrays
    # ------------------------------------------------------------
    print("\nExtracting specific arrays manually...")

    # Get a list of arrays you want to extract
    arrays_of_interest = ['GPS_SIGXX', 'GPS_SIGXY', 'GPS_SIGXZ', 'GPS_SIGYY',
                          'GPS_SIGZY', 'GPS_SIGZZ']

    # Check which arrays actually exist
    available_arrays = [arr for arr in arrays_of_interest if arr in source.PointData.keys()]

    if available_arrays:
        # Create a calculator to extract just these arrays
        calculator = Calculator(Input=source)
        calculator.ResultArrayName = 'Extracted_Data'
        calculator.Function = ' '.join(available_arrays)

        output_extracted = "D:/rad/extracted_stress_data.csv"
        SaveData(output_extracted, proxy=calculator, WriteTimeSteps=1, Precision=12)
        print(f"Extracted stress data saved to: {output_extracted}")
    else:
        print("No requested arrays found. Available arrays are:")
        print(f"  {list(source.PointData.keys())}")

    print("\n--- Summary ---")
    print(f"CSV files created in D:/rad/")
    print("  - global_energy_data.csv: Total internal/kinetic energy over time")
    print("  - cell_data.csv: Data for all cells (if available)")
    print("  - extracted_stress_data.csv: Specific stress components")

    # Verify files
    for f in ['global_energy_data.csv', 'cell_data.csv', 'extracted_stress_data.csv']:
        path = f"D:/rad/{f}"
        if os.path.exists(path) and os.path.getsize(path) > 0:
            size_kb = os.path.getsize(path) / 1024
            print(f"  Ã¢Å“â€œ {f} ({size_kb:.2f} KB)")
        elif os.path.exists(path):
            print(f"   {f} (0 bytes - no data)")
        else:
            print(f"   {f} (not created)")
    NOTE: 103 records were read from file 'c:\temp\py_pgmx.py'
          The minimum record length was 80
          The maximum record length was 88
    NOTE: 103 records were written to file 'c:\temp\py_pgm.py'
          The minimum record length was 80
          The maximum record length was 88
    NOTE: The data step took :
          real time : 0.015
          cpu time  : 0.000



    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=C:\Progra~1\ParaView-6.1.0-Windows-Python3.12-msvc2017-AMD64\bin\pvpython.exe c:/temp/py_pgm.py 2> c:/temp/py_pgm.log,
          Lrecl=32767, Recfm=V

    Loading file: D:/rad/Impact.vtkhdf

    --- Available Data Arrays ---
    Point Data: ['Acceleration', 'Contact_Forces', 'Displacement', 'Mass_Change', 'NODE_ID', 'Velocity']
    Cell Data: ['3DELEM_Strs_Intg_Point111__', '3DELEM_Von_Mises', 'ELEMENT_ID',
     'EROSION_STATUS', 'PART_ID', 'SPHELEM_Diameter', 'SPHELEM_Number_of_neighbours',
     'SPHELEM_Strs_Intg_Point111__', 'SPHELEM_Von_Mises']

    Number of timesteps: 51

    Calculating global integrated quantities...

    Saving global integrated data...
    Global energy data saved to: D:/rad/global_energy_data.csv

    Saving cell data (if available)...
    Cell data saved to: D:/rad/cell_data.csv

    Extracting specific arrays manually...
    No requested arrays found. Available arrays are:
      ['Acceleration', 'Contact_Forces', 'Displacement', 'Mass_Change', 'NODE_ID', 'Velocity']

    --- Summary ---
    CSV files created in D:/rad/
      - global_energy_data.csv: Total internal/kinetic energy over time
      - cell_data.csv: Data for all cells (if available)
      - extracted_stress_data.csv: Specific stress components
      Ã¢Å“â€œ global_energy_data.csv (11.79 KB)
      Ã¢Å“â€œ cell_data.csv (69403.20 KB)
       extracted_stress_data.csv (not created)
    NOTE: 28 records were written to file PRINT

    NOTE: 28 records were read from file rut
          The minimum record length was 0
          The maximum record length was 210
    NOTE: The data step took :
          real time : 37.019
          cpu time  : 0.031



    NOTE: The infile 'c:\temp\py_pgm.log' is:
          Filename='c:\temp\py_pgm.log',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=11:45:37 May 12 2026,
          Last Accessed=11:06:31 Jun 04 2026,
          Last Modified=11:06:31 Jun 04 2026,
          Lrecl=32767, Recfm=V

    NOTE: No records were read from file 'c:\temp\py_pgm.log'
    NOTE: The data step took :
          real time : 0.000
          cpu time  : 0.000


    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 37.604
          cpu time  : 0.171

    /*___          _   _    _         _  __       _       _        _     _
     / _ \  __   _| |_| | _| |__   __| |/ _|  ___| | ___ | |_ __ _| |__ | | ___  ___
    | (_) | \ \ / / __| |/ / `_ \ / _` | |_  / __| |/ __|| __/ _` | `_ \| |/ _ \/ __|
     \__, |  \ V /| |_|   <| | | | (_| |  _| \__ \ | (__ | || (_| | |_) | |  __/\__ \
       /_/    \_/  \__|_|\_\_| |_|\__,_|_|   |___/_|\___| \__\__,_|_.__/|_|\___||___/
    */

    /*--- GLOBAL ENERGY DATA ---*/

    proc delete data=workx.global_energy;
    run;quit;

    data workx.global_energy(drop=empty);
      infile "d:/rad/global_energy_data.csv" lrecl=32756 missover delimiter=',' firstobs=2;
      label
          Acceleration_0 = "Nodal acceleration - X component (mm/ms²)"
          Acceleration_1 = "Nodal acceleration - Y component (mm/ms²)"
          Acceleration_2 = "Nodal acceleration - Z component (mm/ms²)"
          Contact_Forces_0 = "Contact force - X component (N)"
          Contact_Forces_1 = "Contact force - Y component (N)"
          Contact_Forces_2 = "Contact force - Z component (N)"
          Displacement_0 = "Nodal displacement - X component (mm)"
          Displacement_1 = "Nodal displacement - Y component (mm)"
          Displacement_2 = "Nodal displacement - Z component (mm)"
          Mass_Change = "Mass change due to mass scaling or erosion (kg)"
          NODE_ID = "Node identification number"
          Velocity_0 = "Nodal velocity - X component (mm/ms)"
          Velocity_1 = "Nodal velocity - Y component (mm/ms)"
          Velocity_2 = "Nodal velocity - Z component (mm/ms)"
          Points_0 = "Node X-coordinate (mm)"
          Points_1 = "Node Y-coordinate (mm)"
          Points_2 = "Node Z-coordinate (mm)"
          Frame    = "Frame(png) within Simulation mp4"
        ;
      input
          Acceleration_0
          Acceleration_1
          Acceleration_2
          Contact_Forces_0
          Contact_Forces_1
          Contact_Forces_2
          Displacement_0
          Displacement_1
          Displacement_2
          Mass_Change
          NODE_ID
          Velocity_0
          Velocity_1
          Velocity_2
          Points_0
          Points_1
          Points_2
          empty best32.
          ;
          frame=_n_;
    run;quit;


    options label;
    proc means data=workx.global_energy;
    run;

    /**************************************************************************************************************************/
    /*  Altair SLC                                                                                                            */
    /* The MEANS Procedure                                                                                                    */
    /*                                                          Summary statistics                                            */
    /* Variable          Label                                               N            Mean        Minimum         Maximum */
    /*                                                                                                                        */
    /* Acceleration_0    Nodal acceleration - X component (mm/msÂ²)         51    1.6423247E12   -1.860349E13    2.8421743E13 */
    /* Acceleration_1    Nodal acceleration - Y component (mm/msÂ²)         51    -4.703281E11   -2.011633E13    1.1005244E13 */
    /* Acceleration_2    Nodal acceleration - Z component (mm/msÂ²)         51    -8.737283E11   -2.120307E13    2.9547447E13 */
    /* Contact_Forces_0  Contact force - X component (N)                    51     -755.891403   -28272.77662    38373.830475 */
    /* Contact_Forces_1  Contact force - Y component (N)                    51    -2556.506524   -28168.78792    34457.316653 */
    /* Contact_Forces_2  Contact force - Z component (N)                    51    -65227.84007   -246430.1623    3455.3775321 */
    /* Displacement_0    Nodal displacement - X component (mm)              51    1886.0927715   -666.7343785    13906.462097 */
    /* Displacement_1    Nodal displacement - Y component (mm)              51    -6799.311524   -30207.02848               0 */
    /* Displacement_2    Nodal displacement - Z component (mm)              51    -9914.924209   -33198.97559    49950.214378 */
    /* Mass_Change       Mass change due to mass scaling or erosion (kg)    51               0              0               0 */
    /* NODE_ID           Node identification number                         51    15438535.209   12679395.698    16429743.853 */
    /* Velocity_0        Nodal velocity - X component (mm/ms)               51    6382635.7462   -12310314.51    58083231.574 */
    /* Velocity_1        Nodal velocity - Y component (mm/ms)               51    -17858846.42   -71653266.43    8546842.3122 */
    /* Velocity_2        Nodal velocity - Z component (mm/ms)               51    -27397781.75   -252070679.9    146806639.92 */
    /* Points_0          Node X-coordinate (mm)                             51    0.2019964989   -0.031543292    1.4836882353 */
    /* Points_1          Node Y-coordinate (mm)                             51    -0.949785043   -4.561113834    2.619345E-15 */
    /* Points_2          Node Z-coordinate (mm)                             51    -0.732218237   -2.609353542    4.9924583435 */
    /**************************************************************************************************************************/

    /*--- CELL CSV CSV TO PANDA DATAFRAME AND SLC DATASET ---*/

    /*--- GLOBAL ENERGY DATA ---*/

    proc datasets lib=workx;
      delete df cell;
    run;

    options set=PYTHONHOME "D:\py314";
    proc python;
    submit;
    import pandas as pd
    df = pd.read_csv("d:/rad/cell_data.csv")
    df.columns = df.columns.str.replace(r"\s+", "", regex=True)
    print(df);
    endsubmit;
    import python=df data=workx.df;
    run;


    data workx.addLbl;

         /* SPH Stress Tensor Components (at integration point) */
         label
             _3DELEM_STRS_INTG_POINT111___0     = "3D Element - Strain exx at integration point (mm/mm)"
             _3DELEM_STRS_INTG_POINT111___1     = "3D Element - Strain eyy at integration point (mm/mm)"
             _3DELEM_STRS_INTG_POINT111___2     = "3D Element - Strain ezz at integration point (mm/mm)"
             _3DELEM_STRS_INTG_POINT111___3     = "3D Element - Shear strain exy at integration point (mm/mm)"
             _3DELEM_STRS_INTG_POINT111___4     = "3D Element - Shear strain eyz at integration point (mm/mm)"
             _3DELEM_STRS_INTG_POINT111___5     = "3D Element - Shear strain ezx at integration point (mm/mm)"
             _3DELEM_STRS_INTG_POINT111___6     = "3D Element - Strain component 6 at integration point (mm/mm)"
             _3DELEM_STRS_INTG_POINT111___7     = "3D Element - Strain component 7 at integration point (mm/mm)"
             _3DELEM_STRS_INTG_POINT111___8     = "3D Element - Strain component 8 at integration point (mm/mm)"

         ;
         /* 3D Element Von Mises Stress */
         label
              _3DELEM_VON_MISES                  = "3D Element - Von Mises equivalent stress (MPa)"
         ;

         /* Element identification and status */
         label
             ELEMENT_ID                         = "Element identification number"
             EROSION_STATUS                     = "Element erosion status (0=active, 1=eroded)"
             PART_ID                            = "Part identification number"
             CELLTYPE                           = "Element type (1=beam, 2=shell, 3=brick, 10=SPH)"
         ;
       set workx.df;

       drop
            SPHELEM_STRS_INTG_POINT111___0 - SPHELEM_STRS_INTG_POINT111___8;
    run;

    proc means data=workx.df(where=(_3DELEM_VON_MISES>100));
    run;


    /**************************************************************************************************************************/
    /*   The MEANS Procedure                                                                                                  */
    /*  Variable                        Label                                                                                 */
    /*  ------------------------------------------------------------------------------------------------                      */
    /*  _3DELEM_STRS_INTG_POINT111___0  3D Element - Strain exx at integration point (mm/mm)                                  */
    /*  _3DELEM_STRS_INTG_POINT111___1  3D Element - Strain eyy at integration point (mm/mm)                                  */
    /*  _3DELEM_STRS_INTG_POINT111___2  3D Element - Strain ezz at integration point (mm/mm)                                  */
    /*  _3DELEM_STRS_INTG_POINT111___3  3D Element - Shear strain exy at integration point (mm/mm)                            */
    /*  _3DELEM_STRS_INTG_POINT111___4  3D Element - Shear strain eyz at integration point (mm/mm)                            */
    /*  _3DELEM_STRS_INTG_POINT111___5  3D Element - Shear strain ezx at integration point (mm/mm)                            */
    /*  _3DELEM_STRS_INTG_POINT111___6  3D Element - Strain component 6 at integration point (mm/mm)                          */
    /*  _3DELEM_STRS_INTG_POINT111___7  3D Element - Strain component 7 at integration point (mm/mm)                          */
    /*  _3DELEM_STRS_INTG_POINT111___8  3D Element - Strain component 8 at integration point (mm/mm)                          */
    /*  _3DELEM_VON_MISES               3D Element - Von Mises equivalent stress (MPa)                                        */
    /*  ELEMENT_ID                      Element identification number                                                         */
    /*  EROSION_STATUS                  Element erosion status (0=active, 1=eroded)                                           */
    /*  PART_ID                         Part identification number                                                            */
    /*  CELLTYPE                        Element type (1=beam, 2=shell, 3=brick, 10=SPH)                                       */
    /*  SPHELEM_DIAMETER                SPHELEM_DIAMETER                                                                      */
    /*  SPHELEM_NUMBER_OF_NEIGHBOURS    SPHELEM_NUMBER_OF_NEIGHBOURS                                                          */
    /*  SPHELEM_VON_MISES               SPHELEM_VON_MISES                                                                     */
    /*  ------------------------------------------------------------------------------------------------                      */
    /*                                                                                                                        */
    /*                                                              Lower        Upper                                        */
    /*  Variable                             N     Mean   Min       Quartile     Quartile         Max                         */
    /*  ---------------------------------------------------------------------------------------------                         */
    /*  _3DELEM_STRS_INTG_POINT111___0  887451   6.9453 -819.554           0            0     978.068                         */
    /*  _3DELEM_STRS_INTG_POINT111___1  887451   0.0473 -409.614           0            0     426.925                         */
    /*  _3DELEM_STRS_INTG_POINT111___2  887451   0.0319 -344.225           0            0     365.938                         */
    /*  _3DELEM_STRS_INTG_POINT111___3  887451   0.0473 -409.614           0            0     426.925                         */
    /*  _3DELEM_STRS_INTG_POINT111___4  887451   7.0348     -102           0            0     910.294                         */
    /*  _3DELEM_STRS_INTG_POINT111___5  887451  -0.0070 -384.791           0            0     426.846                         */
    /*  _3DELEM_STRS_INTG_POINT111___6  887451   0.0319 -344.225           0            0     365.938                         */
    /*  _3DELEM_STRS_INTG_POINT111___7  887451  -0.0070 -384.791           0            0     426.846                         */
    /*  _3DELEM_STRS_INTG_POINT111___8  887451   1.7884     -101           0            0         101                         */
    /*  _3DELEM_VON_MISES               887451  35.6336        0           0            0     804.466                         */
    /*  ELEMENT_ID                      887451     6596        0     2044.00     10650.00    15000.00                         */
    /*  EROSION_STATUS                  887451   0.1210        0           0            0       1.000                         */
    /*  PART_ID                         887451  36.8847    1.000      5.0000     5.000000         213                         */
    /*  CELLTYPE                        887451   2.3360    1.000      1.0000     1.000000      12.000                         */
    /*  SPHELEM_DIAMETER                887451   0.8620        0      1.0000     1.000000       1.000                         */
    /*  SPHELEM_NUMBER_OF_NEIGHBOURS    887451  25.8139        0     23.0000    36.000000      44.000                         */
    /*  SPHELEM_VON_MISES               887451 302.3610        0    177.9120   429.256988         155                         */
    /**************************************************************************************************************************/


    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */


    /*  ___          _   _    _         _  __         _       _
    / |/ _ \  __   _| |_| | _| |__   __| |/ _|  _ __ | | ___ | |_ ___
    | | | | | \ \ / / __| |/ / `_ \ / _` | |_  | `_ \| |/ _ \| __/ __|
    | | |_| |  \ V /| |_|   <| | | | (_| |  _| | |_) | | (_) | |_\__ \
    |_|\___/    \_/  \__|_|\_\_| |_|\__,_|_|   | .__/|_|\___/ \__|___/
              _ _         _       _            |_|
      ___ ___| | |  _ __ | | ___ | |_ ___
     / __/ _ \ | | | `_ \| |/ _ \| __/ __|
    | (_|  __/ | | | |_) | | (_) | |_\__ \
     \___\___|_|_| | .__/|_|\___/ \__|___/
                   |_|
    */


    options ls=255 ps=255;
    proc means data=workx.addLbl;
     class part_id;
      var _3DELEM_VON_MISES;
    run;quit;

    The MEANS Procedure

           Analysis Variable : _3DELEM_VON_MISES 3D Element - Von Mises equivalent stress (MPa)

              Part
    identification
            number     N Obs         N            Mean         Std Dev         Minimum         Maximum
    --------------------------------------------------------------------------------------------------
                 1     95625     95625     330.6994294     144.1849508               0     804.4669800

                 2     13362     13362               0               0               0               0

                 5    765000    765000               0               0               0               0

              2138     13464     13464               0               0               0               0
    --------------------------------------------------------------------------------------------------



                       Ball Impact  Sress Distributions for

                          X = _3DELEM_STRS_INTG_POINT111__0
                          Y = _3DELEM_STRS_INTG_POINT111__1
                          Z = _3DELEM_STRS_INTG_POINT111__2

                   Frequency              Frequency                Frequency

               6000 12000 18000       6000 12000 18000         6000 12000 18000
          ------+-----+-----+--- ------+-----+-----+------------+-----+-----+-----
     -500 |                      |                        |                      | -500
     -475 |    STRESS X          |     STRESS Y           |     STRESS Z         | -475
     -450 |                      |                        |                      | -450
     -425 |*                     |                        |                      | -425
     -400 |*                     |                        |                      | -400
     -375 |*                     |                        |                      | -375
     -350 |**                    |                        |                      | -350
     -325 |**                    |                        |                      | -325
     -300 |**                    |                        |                      | -300
     -275 |**                    |                        |                      | -275
     -250 |**                    |*                       |                      | -250
     -225 |**                    |*                       |                      | -225
     -200 |**                    |*                       |*                     | -200
     -175 |**                    |**                      |*                     | -175
     -150 |**                    |***                     |**                    | -150
     -125 |**                    |***                     |**                    | -125
     -100 |**                    |****                    |***                   | -100
      -75 |**                    |******                  |*****                 |  -75
      -50 |*                     |*******                 |*******               |  -50
      -25 |**                    |*********               |**************        |  -25
        0 |***                   |**************          |******************    |    0
       25 |***                   |***********             |*************         |   25
       50 |***                   |********                |*******               |   50
       75 |***                   |******                  |****                  |   75
      100 |***                   |****                    |***                   |  100
      125 |***                   |***                     |**                    |  125
      150 |****                  |***                     |**                    |  150
      175 |****                  |**                      |*                     |  175
      200 |*****                 |*                       |*                     |  200
      225 |******                |*                       |*                     |  225
      250 |******                |*                       |                      |  250
      275 |*****                 |                        |                      |  275
      300 |***                   |                        |                      |  300
      325 |***                   |                        |                      |  325
      350 |**                    |                        |                      |  350
      375 |*                     |                        |                      |  375
      400 |*                     |                        |                      |  400
      425 |*                     |                        |                      |  425
      450 |*                     |                        |                      |  450
      475 |*                     |                        |                      |  475
      500 |*                     |                        |                      |  500
      525 |*                     |                        |                      |  525
      550 |                      |                        |                      |  550
      575 |                      |                        |                      |  575
      600 |                      |                        |                      |  600
          ------+-----+-----+----------+-----+-----+------------+-----+-----+-----
               6000 12000 18000       6000 12000 18000         6000 12000 18000

               Frequency              Frequency                Frequency


    Expected Behavior                                Your Distribution             Status

    sxx has widest range (impact direction)           -500 to +500 MPa            Correct
    syy has narrower range (lateral)                  -200 to +200 MPa            Correct
    szz has narrowest (through-thickness)             -100 to +200 MPa            Correct
    Zero stress peak present                                       Yes            Correct
    Asymmetric distribution(tension ^- compression)                Yes            Correct
    No extreme outliers                              Values within ±500 MPa       Correct



                                      D3ELEM_VON_MISES                        Cum.
            Midpoint                                                 Freq  Percent
                      |
                600   |*                                              106     0.12
                590   |***                                            206     0.36
                580   |***                                            261     0.66
                570   |****                                           295     1.00
                560   |*****                                          397     1.45
                550   |******                                         450     1.97
                540   |********                                       606     2.66
                530   |***********                                    820     3.61
                520   |****************                              1179     4.96
                510   |***********************                       1697     6.91
                500   |**************************                    1935     9.13
                490   |*************************                     1894    11.31
                480   |*****************************                 2211    13.84
                470   |*************************************         2797    17.06
                460   |*****************************************     3089    20.60
                450   |********************************************  3276    24.36
                440   |*************************************         2772    27.55
                430   |*********************************             2471    30.38
                420   |************************                      1822    32.48
                410   |**********************                        1680    34.40
                400   |************************                      1793    36.46
                390   |***************************                   2035    38.80
                380   |*****************************                 2178    41.30
                370   |*********************************             2451    44.12
                360   |*******************************               2355    46.82
                350   |**********************************            2547    49.74
                340   |*********************************             2503    52.62
                330   |*********************************             2455    55.44
                320   |********************************              2385    58.18
                310   |*******************************               2311    60.83
                300   |********************************              2377    63.56
                290   |*******************************               2351    66.26
                280   |********************************              2411    69.03
                270   |*********************************             2466    71.86
                260   |*******************************               2354    74.56
                250   |********************************              2410    77.33
                240   |******************************                2234    79.89
                230   |***************************                   2057    82.25
                220   |**************************                    1952    84.50
                210   |*************************                     1844    86.61
                200   |************************                      1815    88.70
                190   |************************                      1795    90.76
                180   |***********************                       1753    92.77
                170   |********************                          1468    94.46
                160   |***************                               1105    95.73
                150   |************                                   918    96.78
                140   |***********                                    799    97.70
                130   |*********                                      688    98.49
                120   |********                                       616    99.19
                110   |*******                                        490    99.76
                100   |***                                            212   100.00
                      |
                       --------+-------+-------+-------+-------+----
                              600     1200    1800    2400    3000

                                         Frequency


    PART_ID    Frequency     Percent     Frequency      Percent
    ------------------------------------------------------------
          1       95625       10.78         95625        10.78  PLATE
          2       13362        1.51        108987        12.28
          5      765000       86.20        873987        98.48
       2138       13464        1.52        887451       100.00

    CELLTYPE    Frequency     Percent     Frequency      Percent
    -------------------------------------------------------------
           1      765000       86.20        765000        86.20
           3       13464        1.52        778464        87.72
           9       13362        1.51        791826        89.22
          12       95625       10.78        887451       100.00  PLATE

                                                    Cumulative    Cumulative
    CELLTYPE    PART_ID    Frequency     Percent     Frequency      Percent
    ------------------------------------------------------------------------
           1          5      765000       86.20        765000        86.20
           3       2138       13464        1.52        778464        87.72
           9          2       13362        1.51        791826        89.22
          12          1       95625       10.78        887451       100.00  PLATE


    %utlfkil(d:/rad/VonMisesStress.png);

    ods listing close;
    ods graphics on / reset=all imagename="VonMisesStress" outputfmt=png;
    ods printer file="d:/rad/VonMisesStress.png" dpi=100;

    proc sgplot data=workx.addLbl(where=(100<=_3DELEM_VON_MISES<=600));
        histogram _3DELEM_VON_MISES / nbins=50;
        xaxis label="Von Mises Stress (MPa)" grid;
        yaxis label="Number of Elements" grid;
        title "Von Mises Stress Distribution in 3D Elements";
    run;

    ods printer close;
    ods graphics off;
    ods listing;



    %utlfkil(d:/rad/Stress-StrainRelationship.png);

    ods listing close;
    ods graphics on / reset=all imagename="StressComponents" outputfmt=png;
    ods printer file="d:/rad/StressStrainRelationship.png" dpi=100;

    %utlfkil(d:/rad/StrainComponentDistribution.png);

    ods listing close;
    ods graphics on / reset=all imagename="StrainComponentDistribution" outputfmt=png;
    ods printer file="d:/rad/StressComponentDistribution.png" dpi=100;

    proc sgplot data=workx.addLbl(where=(100<=_3DELEM_VON_MISES<=600));
        histogram _3DELEM_STRS_INTG_POINT111___0 / transparency=0.5 fillattrs=(color=blue) legendlabel="exx (stretch)";
        histogram _3DELEM_STRS_INTG_POINT111___1 / transparency=0.5 fillattrs=(color=green) legendlabel="eyy (lateral)";
        histogram _3DELEM_STRS_INTG_POINT111___2 / transparency=0.5 fillattrs=(color=red) legendlabel="ezz (thickness)";
        xaxis label="Strain (mm/mm)" grid;
        yaxis label="Number of Elements" grid;
        title "Stress Component Distribution";
    run;

    ods printer close;
    ods graphics off;
    ods listing;


    /*     _       _           _         _       _
      __ _| | ___ | |__   __ _| |  _ __ | | ___ | |_ ___
     / _` | |/ _ \| `_ \ / _` | | | `_ \| |/ _ \| __/ __|
    | (_| | | (_) | |_) | (_| | | | |_) | | (_) | |_\__ \
     \__, |_|\___/|_.__/ \__,_|_| | .__/|_|\___/ \__|___/
     |___/                        |_|
    */

    %utlfkil(d:/rad/ContactForceEvolution.png);

    ods listing close;
    ods graphics on / reset=all imagename="ContactForceEvolution" outputfmt=png;                            Acceleration_0
    ods printer file="d:/rad/ContactForceEvolution.png" dpi=100;                                            Acceleration_1
                                                                                                            Acceleration_2
    proc sgplot data=workx.global_energy;                                                                          Contact_Forces_0
        where FRAME is not missing;                                                                          Contact_Forces_1
        series x=FRAME y=CONTACT_FORCES_0 /                                                                  Contact_Forces_2
               lineattrs=(color=red thickness=2)                                                            Displacement_0
               legendlabel="Force X (N)";                                                                   Displacement_1
        series x=FRAME y=CONTACT_FORCES_1 /                                                                  Displacement_2
               lineattrs=(color=green thickness=2)                                                          Mass_Change
               legendlabel="Force Y (N)";                                                                   NODE_ID
        series x=FRAME y=CONTACT_FORCES_2 /                                                                  Velocity_0
               lineattrs=(color=blue thickness=2)                                                           Velocity_1
               legendlabel="Force Z (N)";                                                                   Velocity_2
        xaxis label="Frame #" grid;                                                                         Points_0
        yaxis label="Contact Force (N)" grid;                                                               Points_1
        title "Contact Force Evolution ";                                                                   Points_2
        refline 0 / axis=y lineattrs=(pattern=dash);                                                        empty best32.
    run;

    ods printer close;
    ods graphics off;
    ods listing;




    %utlfkil(d:/rad/DisplacementEvolution.png);

    ods listing close;
    ods graphics on / reset=all imagename="DisplacementEvolution" outputfmt=png;
    ods printer file="d:/rad/DisplacementEvolution.png" dpi=100;

    proc sgplot data=workx.global_energy;
        where FRAME is not missing;
        series x=FRAME y=Displacement_0 /
               lineattrs=(color=red thickness=2)
               legendlabel="Displacement X (N)";
        series x=FRAME y=Displacement_1 /
               lineattrs=(color=green thickness=2)
               legendlabel="Displacement Y (N)";
        series x=FRAME y=Displacement_2 /
               lineattrs=(color=blue thickness=2)
               legendlabel="Displacement Z (N)";
        xaxis label="Frame #" grid;
        yaxis label="Contact Force (N)" grid;
        title "Displacement Evolution ";
        title2 "Note the Late Rebound?";
        refline 0 / axis=y lineattrs=(pattern=dash);
    run;

    ods printer close;
    ods graphics off;
    ods listing;




    data workx.contact_analysis;
        set workx.global_energy;
        Force_Magnitude = sqrt(
            CONTACT_FORCES_0**2 +
            CONTACT_FORCES_1**2 +
            CONTACT_FORCES_2**2
        );
    run;

    %utlfkil(d:/rad/globalOverallForce.png);

    ods listing close;
    ods graphics on / reset=all imagename="globalOverallForce.png" outputfmt=png;
    ods printer file="d:/rad/globalOverallForce.png" dpi=100;

    proc sgplot data=workx.contact_analysis;
        where FRAME is not missing;
        series x=Frame y=Force_Magnitude /
               lineattrs=(color=purple thickness=3);
        xaxis label="Time (ms)" grid;
        yaxis label="Resultant Contact Force (N)" grid;
        title "Total Contact Force Magnitude";
        title2 "Peak indicates maximum Force";
        refline 15 / axis=x label="Max Deformation"
                    lineattrs=(color=blue pattern=dash thickness=1.5);
    run;

    ods printer close;
    ods graphics off;
    ods listing;


    /* _                      _                         _  _     __                             _   _       _  __
    / / |  ___ _ __ ___  __ _| |_ ___   _ __ ___  _ __ | || |   / _|_ __ ___  _ __ ___   __   _| |_| | ____| |/ _|
    | | | / __| `__/ _ \/ _` | __/ _ \ | `_ ` _ \| `_ \| || |_ | |_| `__/ _ \| `_ ` _ \  \ \ / / __| |/ / _` | |_
    | | || (__| | |  __/ (_| | ||  __/ | | | | | | |_) |__   _||  _| | | (_) | | | | | |  \ V /| |_|   < (_| |  _|
    |_|_| \___|_|  \___|\__,_|\__\___| |_| |_| |_| .__/   |_|  |_| |_|  \___/|_| |_| |_|   \_/  \__|_|\_\__,_|_|
                                                 |_|
    */

    %utlfkil(d:/rad/impact_animation.mp4);

    %slc_pvpybegin;
    cards4;
    #!/usr/bin/env python
    """
    Convert VTKHDF to MP4 with Sequential Color Map (viridis).
    Camera zoomed OUT to show entire model.
    Stress range focused on 100-400 MPa for better contrast.
    """

    from paraview.simple import *
    import os
    import subprocess

    # ============================================================
    # CRITICAL: Disable automatic camera reset
    # ============================================================
    paraview.simple._DisableFirstRenderCameraReset()

    # ============================================================
    # CONFIGURATION
    # ============================================================
    VTKHDF_FILE = "D:/rad/Impact.vtkhdf"
    OUTPUT_DIR = "D:/rad/frames"
    OUTPUT_VIDEO = "D:/rad/impact_animation.mp4"
    FRAME_RATE = 30

    IMAGE_WIDTH = 1080
    IMAGE_HEIGHT = 1920

    # Camera settings - ZOOMED OUT to show entire model
    CAMERA_POSITION = [0, -15, 8]
    CAMERA_FOCAL_POINT = [0, 0, 5]
    CAMERA_VIEW_UP = [0, 0, 1]
    USE_PARALLEL_PROJECTION = True
    PARALLEL_SCALE = 100.0

    # Color array for stress visualization
    COLOR_ARRAY = "3DELEM_Von_Mises"

    # ============================================================
    # COLOR MAP SETTINGS
    # ============================================================
    COLOR_MAP_PRESET = "viridis"  # Options: 'viridis', 'plasma', 'inferno', 'magma'

    # STRESS VISUALIZATION RANGE
    # Focus on stressed region (100-400 MPa) for better contrast
    STRESS_MIN = 100.0  # Minimum stress to show (MPa)
    STRESS_MAX = 800.0  # Maximum stress to show (MPa)

    # ============================================================
    # CREATE OUTPUT DIRECTORY
    # ============================================================
    os.makedirs(OUTPUT_DIR, exist_ok=True)

    print("=" * 60)
    print(f"VTKHDF to MP4 Converter - Color Map: {COLOR_MAP_PRESET}")
    print("=" * 60)
    print(f"Input file: {VTKHDF_FILE}")
    print(f"Output video: {OUTPUT_VIDEO}")
    print(f"Frame rate: {FRAME_RATE} fps")
    print(f"Parallel Scale (zoom): {PARALLEL_SCALE}")
    print(f"Stress visualization range: {STRESS_MIN} to {STRESS_MAX} MPa")

    # ============================================================
    # LOAD THE VTKHDF FILE
    # ============================================================
    if not os.path.exists(VTKHDF_FILE):
        print(f"ERROR: File not found: {VTKHDF_FILE}")
        exit(1)

    print("\nLoading VTKHDF file...")
    source = OpenDataFile(VTKHDF_FILE)
    source.UpdatePipeline()

    timesteps = source.TimestepValues
    num_frames = len(timesteps) if timesteps else 1
    print(f"Found {num_frames} time steps")

    print(f"Point Data: {list(source.PointData.keys())}")
    print(f"Cell Data: {list(source.CellData.keys())}")

    # ============================================================
    # STEP 1: CONVERT CELL DATA TO POINT DATA
    # ============================================================
    print(f"\nConverting cell data to point data...")
    cell_to_point = CellDatatoPointData(Input=source)
    cell_to_point.UpdatePipeline()
    print(f"Point Data after conversion: {list(cell_to_point.PointData.keys())}")

    # ============================================================
    # CREATE RENDER VIEW
    # ============================================================
    print("\nSetting up render view...")
    renderView = CreateView('RenderView')
    renderView.ViewSize = [IMAGE_WIDTH, IMAGE_HEIGHT]
    AssignViewToLayout(renderView)

    display = Show(cell_to_point, renderView)
    display.Representation = 'Surface'

    # ============================================================
    # APPLY SEQUENTIAL COLOR MAP WITH CUSTOM RANGE
    # ============================================================
    print(f"\nApplying '{COLOR_MAP_PRESET}' color map using '{COLOR_ARRAY}'...")

    if COLOR_ARRAY in cell_to_point.PointData.keys():
        display.ColorArrayName = ['POINTS', COLOR_ARRAY]
        display.SetScalarBarVisibility(renderView, True)

        # Get the color transfer function
        lut = GetColorTransferFunction(COLOR_ARRAY)

        # Get actual data range
        data_range = cell_to_point.PointData.GetArray(COLOR_ARRAY).GetRange()
        min_val = data_range[0]
        max_val = data_range[1]
        print(f"  Actual data range: {min_val:.2f} to {max_val:.2f} MPa")

        if max_val > min_val:
            # Apply the selected preset color map
            if COLOR_MAP_PRESET == "viridis":
                lut.ApplyPreset("viridis", True)
            elif COLOR_MAP_PRESET == "plasma":
                lut.ApplyPreset("plasma", True)
            elif COLOR_MAP_PRESET == "inferno":
                lut.ApplyPreset("inferno", True)
            elif COLOR_MAP_PRESET == "magma":
                lut.ApplyPreset("magma", True)
            elif COLOR_MAP_PRESET == "Cool to Warm":
                lut.ApplyPreset("Cool to Warm", True)
            else:
                lut.ApplyPreset("viridis", True)

            # FOCUS ON STRESSED REGION (100-400 MPa)
            # This excludes zero-stress elements from the color mapping
            lut.RescaleTransferFunction(STRESS_MIN, STRESS_MAX)

            print(f"  Color map rescaled to: {STRESS_MIN} to {STRESS_MAX} MPa")
            print(f"  Elements below {STRESS_MIN} MPa will appear as the minimum color")
            print(f"  Elements above {STRESS_MAX} MPa will appear as the maximum color")

            # Scalar bar settings
            scalar_bar = GetScalarBar(display, renderView)
            scalar_bar.Title = "Von Mises Stress (MPa)"
            scalar_bar.TitleFontSize = 12
            scalar_bar.LabelFontSize = 10
            scalar_bar.RangeLabelFormat = "%-#6.1f"

            print(f"  Color map '{COLOR_MAP_PRESET}' applied with custom range")
        else:
            print("  WARNING: Data range is zero - no variation in data")
    else:
        print(f"  ERROR: '{COLOR_ARRAY}' not found")
        print("  Available arrays:", list(cell_to_point.PointData.keys()))

    renderView.Background = [0.05, 0.05, 0.1]

    # ============================================================
    # SET UP CAMERA - ZOOMED OUT
    # ============================================================
    renderView.CameraPosition = CAMERA_POSITION
    renderView.CameraFocalPoint = CAMERA_FOCAL_POINT
    renderView.CameraViewUp = CAMERA_VIEW_UP

    if USE_PARALLEL_PROJECTION:
        renderView.CameraParallelProjection = 1
        renderView.CameraParallelScale = PARALLEL_SCALE
    else:
        renderView.CameraParallelProjection = 0

    # Force update
    renderView.UpdateVTKObjects()
    Render()
    renderView.ResetCamera()

    # ============================================================
    # CONFIGURE ANIMATION
    # ============================================================
    animationScene = GetAnimationScene()
    animationScene.NumberOfFrames = num_frames
    animationScene.StartTime = 0
    animationScene.EndTime = num_frames - 1
    animationScene.PlayMode = 'Sequence'

    # ============================================================
    # SAVE FRAMES
    # ============================================================
    print(f"\nSaving {num_frames} frames to {OUTPUT_DIR}...")

    for i in range(num_frames):
        animationScene.TimeKeeper.Time = i
        cell_to_point.UpdatePipeline(i)

        # Re-apply camera settings on each frame
        renderView.CameraPosition = CAMERA_POSITION
        renderView.CameraFocalPoint = CAMERA_FOCAL_POINT
        renderView.CameraViewUp = CAMERA_VIEW_UP
        renderView.CameraParallelScale = PARALLEL_SCALE

        Render()

        frame_file = os.path.join(OUTPUT_DIR, f"frame_{i+1:04d}.png")
        SaveScreenshot(frame_file, renderView, ImageResolution=[IMAGE_WIDTH, IMAGE_HEIGHT])

        if (i + 1) % 10 == 0 or (i + 1) == num_frames:
            print(f"  Saved frame {i+1}/{num_frames}")

    print(f"\nFrames saved to: {OUTPUT_DIR}")

    # ============================================================
    # CONVERT TO MP4
    # ============================================================
    print("\n" + "=" * 50)
    print("Converting PNG sequence to MP4...")
    print("=" * 50)

    ffmpeg_cmd = None
    ffmpeg_paths = ['ffmpeg', 'C:\\ffmpeg\\bin\\ffmpeg.exe', 'D:\\ffmpeg\\bin\\ffmpeg.exe']

    for path in ffmpeg_paths:
        try:
            subprocess.run([path, '-version'], capture_output=True, check=True)
            ffmpeg_cmd = path
            break
        except (subprocess.SubprocessError, FileNotFoundError):
            continue

    if ffmpeg_cmd:
        input_pattern = os.path.join(OUTPUT_DIR, "frame_%04d.png").replace('\\', '/')
        output_video = OUTPUT_VIDEO.replace('\\', '/')

        ffmpeg_command = [
            ffmpeg_cmd, '-framerate', str(FRAME_RATE),
            '-i', input_pattern,
            '-vf', 'pad=1920:1062:(ow-iw)/2:(oh-ih)/2',
            '-c:v', 'libx264',
            '-pix_fmt', 'yuv420p',
            '-crf', '18',
            '-y', output_video
        ]

        print(f"Running FFmpeg...")
        try:
            result = subprocess.run(ffmpeg_command, capture_output=True, text=True)
            if result.returncode == 0 and os.path.exists(OUTPUT_VIDEO):
                size_mb = os.path.getsize(OUTPUT_VIDEO) / (1024 * 1024)
                print(f"\nSUCCESS! MP4 created: {OUTPUT_VIDEO}")
                print(f"File size: {size_mb:.2f} MB")
            else:
                print(f"\nFFmpeg failed. Run this command manually:")
                print(f'ffmpeg -framerate {FRAME_RATE} -i "{OUTPUT_DIR}/frame_%04d.png" -vf "pad=1920:1062:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -pix_fmt yuv420p -crf 18 -y {OUTPUT_VIDEO}')
        except Exception as e:
            print(f"\nError: {e}")
            print(f'ffmpeg -framerate {FRAME_RATE} -i "{OUTPUT_DIR}/frame_%04d.png" -vf "pad=1920:1062:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -pix_fmt yuv420p -crf 18 -y {OUTPUT_VIDEO}')
    else:
        print("\nFFmpeg not found. Run this command manually:")
        print(f'ffmpeg -framerate {FRAME_RATE} -i "{OUTPUT_DIR}/frame_%04d.png" -vf "pad=1920:1062:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -pix_fmt yuv420p -crf 18 -y {OUTPUT_VIDEO}')

    print("\n" + "=" * 60)
    print("PROCESS COMPLETE")
    print("=" * 60)
    print(f"Animation saved to: {OUTPUT_VIDEO}")
    ;;;;
    %slc_pvpyend;


    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    /**************************************************************************************************************************/
    /* Altair SLC                                                                                                             */
    /* ============================================================                                                           */
    /* VTKHDF to MP4 Converter - Color Map: viridis                                                                           */
    /* ============================================================                                                           */
    /* Input file: D:/rad/Impact.vtkhdf                                                                                       */
    /* Output video: D:/rad/impact_animation.mp4                                                                              */
    /* Frame rate: 30 fps                                                                                                     */
    /* Parallel Scale (zoom): 100.0                                                                                           */
    /* Stress visualization range: 100.0 to 400.0 MPa                                                                         */
    /*                                                                                                                        */
    /* Loading VTKHDF file...                                                                                                 */
    /* Found 51 time steps                                                                                                    */
    /* Point Data: ['Acceleration', 'Contact_Forces', 'Displacement', 'Mass_                                                  */
    /* Cell Data: ['3DELEM_Strs_Intg_Point111__', '3DELEM_Von_Mises', 'ELEME                                                  */
    /*                                                                                                                        */
    /* Converting cell data to point data...                                                                                  */
    /* Point Data after conversion: ['Acceleration', 'Contact_Forces', 'Disp                                                  */
    /* hbours', 'SPHELEM_Strs_Intg_Point111__', 'SPHELEM_Von_Mises']                                                          */
    /*                                                                                                                        */
    /* Setting up render view...                                                                                              */
    /*                                                                                                                        */
    /* Applying 'viridis' color map using '3DELEM_Von_Mises'...                                                               */
    /*   Actual data range: 0.00 to 0.00 MPa                                                                                  */
    /*   WARNING: Data range is zero - no variation in data                                                                   */
    /*                                                                                                                        */
    /* Saving 51 frames to D:/rad/frames...                                                                                   */
    /*   Saved frame 10/51                                                                                                    */
    /*   Saved frame 20/51                                                                                                    */
    /*   Saved frame 30/51                                                                                                    */
    /*   Saved frame 40/51                                                                                                    */
    /*   Saved frame 50/51                                                                                                    */
    /*   Saved frame 51/51                                                                                                    */
    /*                                                                                                                        */
    /* Frames saved to: D:/rad/frames                                                                                         */
    /*                                                                                                                        */
    /* ==================================================                                                                     */
    /* Converting PNG sequence to MP4...                                                                                      */
    /* ==================================================                                                                     */
    /* Running FFmpeg...                                                                                                      */
    /*                                                                                                                        */
    /* SUCCESS! MP4 created: D:/rad/impact_animation.mp4                                                                      */
    /* File size: 0.12 MB                                                                                                     */
    /*                                                                                                                        */
    /* ============================================================                                                           */
    /* PROCESS COMPLETE                                                                                                       */
    /* ============================================================                                                           */
    /* Animation saved to: D:/rad/impact_animation.mp4                                                                        */
    /**************************************************************************************************************************/


    /*
    | | ___   __ _
    | |/ _ \ / _` |
    | | (_) | (_| |
    |_|\___/ \__, |
             |___/
    */

    1                                          Altair SLC         09:48 Saturday, June  6, 2026

    NOTE: Copyright 2002-2025 World Programming, an Altair Company
    NOTE: Altair SLC 2026 (05.26.01.00.000758)
          Licensed to Roger DeAngelis
    NOTE: This session is executing on the X64_WIN11PRO platform and is running in 64 bit mode

    NOTE: AUTOEXEC processing beginning; file is C:\wpsoto\autoexec.sas
    NOTE: AUTOEXEC source line
    1       +  ?ods _all_ close;
               ^
    ERROR: Expected a statement keyword : found "?"
    NOTE: Library workx assigned as follows:
          Engine:        SAS7BDAT
          Physical Name: d:\wpswrkx

    NOTE: Library wpdx assigned as follows:
          Engine:        WPD
          Physical Name: d:\wpswrkx

    NOTE: Library slchelp assigned as follows:
          Engine:        WPD
          Physical Name: C:\Progra~1\Altair\SLC\2026\sashelp


    LOG:  9:48:04
    NOTE: 1 record was written to file PRINT

    NOTE: The data step took :
          real time : 0.047
          cpu time  : 0.015


    NOTE: Format num2mis output
    NOTE: Format $chr2mis output
    NOTE: Procedure format step took :
          real time : 0.015
          cpu time  : 0.015


    NOTE: AUTOEXEC processing completed

    1          %utlfkil(d:/rad/impact_animation.mp4);
    2
    3         %slc_pvpybegin;
    The file c:/temp/py_pgm.py does not exist
    4         cards4;

    NOTE: The file 'c:\temp\py_pgmx.py' is:
          Filename='c:\temp\py_pgmx.py',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=13:21:25 Jan 12 2026,
          Last Accessed=09:48:04 Jun 06 2026,
          Last Modified=09:48:04 Jun 06 2026,
          Lrecl=32767, Recfm=V

    NOTE: 260 records were written to file 'c:\temp\py_pgmx.py'
          The minimum record length was 80
          The maximum record length was 181
    NOTE: The data step took :
          real time : 0.016
          cpu time  : 0.000


    5         #!/usr/bin/env python
    6         """
    7         Convert VTKHDF to MP4 with Sequential Color Map (viridis).
    8         Camera zoomed OUT to show entire model.
    9         Stress range focused on 100-400 MPa for better contrast.
    10        """
    11
    12        from paraview.simple import *
    13        import os
    14        import subprocess
    15
    16        # ============================================================
    17        # CRITICAL: Disable automatic camera reset
    18        # ============================================================
    19        paraview.simple._DisableFirstRenderCameraReset()
    20
    21        # ============================================================
    22        # CONFIGURATION
    23        # ============================================================
    24        VTKHDF_FILE = "D:/rad/Impact.vtkhdf"
    25        OUTPUT_DIR = "D:/rad/frames"
    26        OUTPUT_VIDEO = "D:/rad/impact_animation.mp4"
    27        FRAME_RATE = 30
    28
    29        IMAGE_WIDTH = 1080
    30        IMAGE_HEIGHT = 1920
    31
    32        # Camera settings - ZOOMED OUT to show entire model
    33        CAMERA_POSITION = [0, -15, 8]
    34        CAMERA_FOCAL_POINT = [0, 0, 5]
    35        CAMERA_VIEW_UP = [0, 0, 1]
    36        USE_PARALLEL_PROJECTION = True
    37        PARALLEL_SCALE = 100.0
    38
    39        # Color array for stress visualization
    40        COLOR_ARRAY = "3DELEM_Von_Mises"
    41
    42        # ============================================================
    43        # COLOR MAP SETTINGS
    44        # ============================================================
    45        COLOR_MAP_PRESET = "viridis"  # Options: 'viridis', 'plasma', 'inferno', 'magma'
    46
    47        # STRESS VISUALIZATION RANGE
    48        # Focus on stressed region (100-400 MPa) for better contrast
    49        STRESS_MIN = 100.0  # Minimum stress to show (MPa)
    50        STRESS_MAX = 800.0  # Maximum stress to show (MPa)
    51
    52        # ============================================================
    53        # CREATE OUTPUT DIRECTORY
    54        # ============================================================
    55        os.makedirs(OUTPUT_DIR, exist_ok=True)
    56
    57        print("=" * 60)
    58        print(f"VTKHDF to MP4 Converter - Color Map: {COLOR_MAP_PRESET}")
    59        print("=" * 60)
    60        print(f"Input file: {VTKHDF_FILE}")
    61        print(f"Output video: {OUTPUT_VIDEO}")
    62        print(f"Frame rate: {FRAME_RATE} fps")
    63        print(f"Parallel Scale (zoom): {PARALLEL_SCALE}")
    64        print(f"Stress visualization range: {STRESS_MIN} to {STRESS_MAX} MPa")
    65
    66        # ============================================================
    67        # LOAD THE VTKHDF FILE
    68        # ============================================================
    69        if not os.path.exists(VTKHDF_FILE):
    70            print(f"ERROR: File not found: {VTKHDF_FILE}")
    71            exit(1)
    72
    73        print("\nLoading VTKHDF file...")
    74        source = OpenDataFile(VTKHDF_FILE)
    75        source.UpdatePipeline()
    76
    77        timesteps = source.TimestepValues
    78        num_frames = len(timesteps) if timesteps else 1
    79        print(f"Found {num_frames} time steps")
    80
    81        print(f"Point Data: {list(source.PointData.keys())}")
    82        print(f"Cell Data: {list(source.CellData.keys())}")
    83
    84        # ============================================================
    85        # STEP 1: CONVERT CELL DATA TO POINT DATA
    86        # ============================================================
    87        print(f"\nConverting cell data to point data...")
    88        cell_to_point = CellDatatoPointData(Input=source)
    89        cell_to_point.UpdatePipeline()
    90        print(f"Point Data after conversion: {list(cell_to_point.PointData.keys())}")
    91
    92        # ============================================================
    93        # CREATE RENDER VIEW
    94        # ============================================================
    95        print("\nSetting up render view...")
    96        renderView = CreateView('RenderView')
    97        renderView.ViewSize = [IMAGE_WIDTH, IMAGE_HEIGHT]
    98        AssignViewToLayout(renderView)
    99
    100       display = Show(cell_to_point, renderView)
    101       display.Representation = 'Surface'
    102
    103       # ============================================================
    104       # APPLY SEQUENTIAL COLOR MAP WITH CUSTOM RANGE
    105       # ============================================================
    106       print(f"\nApplying '{COLOR_MAP_PRESET}' color map using '{COLOR_ARRAY}'...")
    107
    108       if COLOR_ARRAY in cell_to_point.PointData.keys():
    109           display.ColorArrayName = ['POINTS', COLOR_ARRAY]
    110           display.SetScalarBarVisibility(renderView, True)
    111
    112           # Get the color transfer function
    113           lut = GetColorTransferFunction(COLOR_ARRAY)
    114
    115           # Get actual data range
    116           data_range = cell_to_point.PointData.GetArray(COLOR_ARRAY).GetRange()
    117           min_val = data_range[0]
    118           max_val = data_range[1]
    119           print(f"  Actual data range: {min_val:.2f} to {max_val:.2f} MPa")
    120
    121           if max_val > min_val:
    122               # Apply the selected preset color map
    123               if COLOR_MAP_PRESET == "viridis":
    124                   lut.ApplyPreset("viridis", True)
    125               elif COLOR_MAP_PRESET == "plasma":
    126                   lut.ApplyPreset("plasma", True)
    127               elif COLOR_MAP_PRESET == "inferno":
    128                   lut.ApplyPreset("inferno", True)
    129               elif COLOR_MAP_PRESET == "magma":
    130                   lut.ApplyPreset("magma", True)
    131               elif COLOR_MAP_PRESET == "Cool to Warm":
    132                   lut.ApplyPreset("Cool to Warm", True)
    133               else:
    134                   lut.ApplyPreset("viridis", True)
    135
    136               # FOCUS ON STRESSED REGION (100-400 MPa)
    137               # This excludes zero-stress elements from the color mapping
    138               lut.RescaleTransferFunction(STRESS_MIN, STRESS_MAX)
    139
    140               print(f"  Color map rescaled to: {STRESS_MIN} to {STRESS_MAX} MPa")
    141               print(f"  Elements below {STRESS_MIN} MPa will appear as the minimum color")
    142               print(f"  Elements above {STRESS_MAX} MPa will appear as the maximum color")
    143
    144               # Scalar bar settings
    145               scalar_bar = GetScalarBar(display, renderView)
    146               scalar_bar.Title = "Von Mises Stress (MPa)"
    147               scalar_bar.TitleFontSize = 12
    148               scalar_bar.LabelFontSize = 10
    149               scalar_bar.RangeLabelFormat = "%-#6.1f"
    150
    151               print(f"  Color map '{COLOR_MAP_PRESET}' applied with custom range")
    152           else:
    153               print("  WARNING: Data range is zero - no variation in data")
    154       else:
    155           print(f"  ERROR: '{COLOR_ARRAY}' not found")
    156           print("  Available arrays:", list(cell_to_point.PointData.keys()))
    157
    158       renderView.Background = [0.05, 0.05, 0.1]
    159
    160       # ============================================================
    161       # SET UP CAMERA - ZOOMED OUT
    162       # ============================================================
    163       renderView.CameraPosition = CAMERA_POSITION
    164       renderView.CameraFocalPoint = CAMERA_FOCAL_POINT
    165       renderView.CameraViewUp = CAMERA_VIEW_UP
    166
    167       if USE_PARALLEL_PROJECTION:
    168           renderView.CameraParallelProjection = 1
    169           renderView.CameraParallelScale = PARALLEL_SCALE
    170       else:
    171           renderView.CameraParallelProjection = 0
    172
    173       # Force update
    174       renderView.UpdateVTKObjects()
    175       Render()
    176       renderView.ResetCamera()
    177
    178       # ============================================================
    179       # CONFIGURE ANIMATION
    180       # ============================================================
    181       animationScene = GetAnimationScene()
    182       animationScene.NumberOfFrames = num_frames
    183       animationScene.StartTime = 0
    184       animationScene.EndTime = num_frames - 1
    185       animationScene.PlayMode = 'Sequence'
    186
    187       # ============================================================
    188       # SAVE FRAMES
    189       # ============================================================
    190       print(f"\nSaving {num_frames} frames to {OUTPUT_DIR}...")
    191
    192       for i in range(num_frames):
    193           animationScene.TimeKeeper.Time = i
    194           cell_to_point.UpdatePipeline(i)
    195
    196           # Re-apply camera settings on each frame
    197           renderView.CameraPosition = CAMERA_POSITION
    198           renderView.CameraFocalPoint = CAMERA_FOCAL_POINT
    199           renderView.CameraViewUp = CAMERA_VIEW_UP
    200           renderView.CameraParallelScale = PARALLEL_SCALE
    201
    202           Render()
    203
    204           frame_file = os.path.join(OUTPUT_DIR, f"frame_{i+1:04d}.png")
    205           SaveScreenshot(frame_file, renderView, ImageResolution=[IMAGE_WIDTH, IMAGE_HEIGHT])
    206
    207           if (i + 1) % 10 == 0 or (i + 1) == num_frames:
    208               print(f"  Saved frame {i+1}/{num_frames}")
    209
    210       print(f"\nFrames saved to: {OUTPUT_DIR}")
    211
    212       # ============================================================
    213       # CONVERT TO MP4
    214       # ============================================================
    215       print("\n" + "=" * 50)
    216       print("Converting PNG sequence to MP4...")
    217       print("=" * 50)
    218
    219       ffmpeg_cmd = None
    220       ffmpeg_paths = ['ffmpeg', 'C:\\ffmpeg\\bin\\ffmpeg.exe', 'D:\\ffmpeg\\bin\\ffmpeg.exe']
    221
    222       for path in ffmpeg_paths:
    223           try:
    224               subprocess.run([path, '-version'], capture_output=True, check=True)
    225               ffmpeg_cmd = path
    226               break
    227           except (subprocess.SubprocessError, FileNotFoundError):
    228               continue
    229
    230       if ffmpeg_cmd:
    231           input_pattern = os.path.join(OUTPUT_DIR, "frame_%04d.png").replace('\\', '/')
    232           output_video = OUTPUT_VIDEO.replace('\\', '/')
    233
    234           ffmpeg_command = [
    235               ffmpeg_cmd, '-framerate', str(FRAME_RATE),
    236               '-i', input_pattern,
    237               '-vf', 'pad=1920:1062:(ow-iw)/2:(oh-ih)/2',
    238               '-c:v', 'libx264',
    239               '-pix_fmt', 'yuv420p',
    240               '-crf', '18',
    241               '-y', output_video
    242           ]
    243
    244           print(f"Running FFmpeg...")
    245           try:
    246               result = subprocess.run(ffmpeg_command, capture_output=True, text=True)
    247               if result.returncode == 0 and os.path.exists(OUTPUT_VIDEO):
    248                   size_mb = os.path.getsize(OUTPUT_VIDEO) / (1024 * 1024)
    249                   print(f"\nSUCCESS! MP4 created: {OUTPUT_VIDEO}")
    250                   print(f"File size: {size_mb:.2f} MB")
    251               else:
    252                   print(f"\nFFmpeg failed. Run this command manually:")
    253                   print(f'ffmpeg -framerate {FRAME_RATE} -i "{OUTPUT_DIR}/frame_%04d.png" -vf "pad=1920:1062:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -pix_fmt yuv420p -crf 18 -y {OUTPUT_VIDEO}')
    254           except Exception as e:
    255               print(f"\nError: {e}")
    256               print(f'ffmpeg -framerate {FRAME_RATE} -i "{OUTPUT_DIR}/frame_%04d.png" -vf "pad=1920:1062:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -pix_fmt yuv420p -crf 18 -y {OUTPUT_VIDEO}')
    257       else:
    258           print("\nFFmpeg not found. Run this command manually:")
    259           print(f'ffmpeg -framerate {FRAME_RATE} -i "{OUTPUT_DIR}/frame_%04d.png" -vf "pad=1920:1062:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -pix_fmt yuv420p -crf 18 -y {OUTPUT_VIDEO}')
    260
    261       print("\n" + "=" * 60)
    262       print("PROCESS COMPLETE")
    263       print("=" * 60)
    264       print(f"Animation saved to: {OUTPUT_VIDEO}")
    265       ;;;;
    266       %slc_pvpyend;

    NOTE: The infile 'c:\temp\py_pgmx.py' is:
          Filename='c:\temp\py_pgmx.py',
          Owner Name=SLC\suzie,
          File size (bytes)=21634,
          Create Time=13:21:25 Jan 12 2026,
          Last Accessed=09:48:04 Jun 06 2026,
          Last Modified=09:48:04 Jun 06 2026,
          Lrecl=32767, Recfm=V

    NOTE: The file 'c:\temp\py_pgm.py' is:
          Filename='c:\temp\py_pgm.py',
          Owner Name=SLC\suzie,
          File size (bytes)=0,
          Create Time=16:38:15 May 12 2026,
          Last Accessed=09:48:04 Jun 06 2026,
          Last Modified=09:48:04 Jun 06 2026,
          Lrecl=32767, Recfm=V

    #!/usr/bin/env python
    """
    Convert VTKHDF to MP4 with Sequential Color Map (viridis).
    Camera zoomed OUT to show entire model.
    Stress range focused on 100-400 MPa for better contrast.
    """

    from paraview.simple import *
    import os
    import subprocess

    # ============================================================
    # CRITICAL: Disable automatic camera reset
    # ============================================================
    paraview.simple._DisableFirstRenderCameraReset()

    # ============================================================
    # CONFIGURATION
    # ============================================================
    VTKHDF_FILE = "D:/rad/Impact.vtkhdf"
    OUTPUT_DIR = "D:/rad/frames"
    OUTPUT_VIDEO = "D:/rad/impact_animation.mp4"
    FRAME_RATE = 30

    IMAGE_WIDTH = 1080
    IMAGE_HEIGHT = 1920

    # Camera settings - ZOOMED OUT to show entire model
    CAMERA_POSITION = [0, -15, 8]
    CAMERA_FOCAL_POINT = [0, 0, 5]
    CAMERA_VIEW_UP = [0, 0, 1]
    USE_PARALLEL_PROJECTION = True
    PARALLEL_SCALE = 100.0

    # Color array for stress visualization
    COLOR_ARRAY = "3DELEM_Von_Mises"

    # ============================================================
    # COLOR MAP SETTINGS
    # ============================================================
    COLOR_MAP_PRESET = "viridis"  # Options: 'viridis', 'plasma', 'inferno', 'magma'

    # STRESS VISUALIZATION RANGE
    # Focus on stressed region (100-400 MPa) for better contrast
    STRESS_MIN = 100.0  # Minimum stress to show (MPa)
    STRESS_MAX = 800.0  # Maximum stress to show (MPa)

    # ============================================================
    # CREATE OUTPUT DIRECTORY
    # ============================================================
    os.makedirs(OUTPUT_DIR, exist_ok=True)

    print("=" * 60)
    print(f"VTKHDF to MP4 Converter - Color Map: {COLOR_MAP_PRESET}")
    print("=" * 60)
    print(f"Input file: {VTKHDF_FILE}")
    print(f"Output video: {OUTPUT_VIDEO}")
    print(f"Frame rate: {FRAME_RATE} fps")
    print(f"Parallel Scale (zoom): {PARALLEL_SCALE}")
    print(f"Stress visualization range: {STRESS_MIN} to {STRESS_MAX} MPa")

    # ============================================================
    # LOAD THE VTKHDF FILE
    # ============================================================
    if not os.path.exists(VTKHDF_FILE):
        print(f"ERROR: File not found: {VTKHDF_FILE}")
        exit(1)

    print("\nLoading VTKHDF file...")
    source = OpenDataFile(VTKHDF_FILE)
    source.UpdatePipeline()

    timesteps = source.TimestepValues
    num_frames = len(timesteps) if timesteps else 1
    print(f"Found {num_frames} time steps")

    print(f"Point Data: {list(source.PointData.keys())}")
    print(f"Cell Data: {list(source.CellData.keys())}")

    # ============================================================
    # STEP 1: CONVERT CELL DATA TO POINT DATA
    # ============================================================
    print(f"\nConverting cell data to point data...")
    cell_to_point = CellDatatoPointData(Input=source)
    cell_to_point.UpdatePipeline()
    print(f"Point Data after conversion: {list(cell_to_point.PointData.keys())}")

    # ============================================================
    # CREATE RENDER VIEW
    # ============================================================
    print("\nSetting up render view...")
    renderView = CreateView('RenderView')
    renderView.ViewSize = [IMAGE_WIDTH, IMAGE_HEIGHT]
    AssignViewToLayout(renderView)

    display = Show(cell_to_point, renderView)
    display.Representation = 'Surface'

    # ============================================================
    # APPLY SEQUENTIAL COLOR MAP WITH CUSTOM RANGE
    # ============================================================
    print(f"\nApplying '{COLOR_MAP_PRESET}' color map using '{COLOR_ARRAY}'...")

    if COLOR_ARRAY in cell_to_point.PointData.keys():
        display.ColorArrayName = ['POINTS', COLOR_ARRAY]
        display.SetScalarBarVisibility(renderView, True)

        # Get the color transfer function
        lut = GetColorTransferFunction(COLOR_ARRAY)

        # Get actual data range
        data_range = cell_to_point.PointData.GetArray(COLOR_ARRAY).GetRange()
        min_val = data_range[0]
        max_val = data_range[1]
        print(f"  Actual data range: {min_val:.2f} to {max_val:.2f} MPa")

        if max_val > min_val:
            # Apply the selected preset color map
            if COLOR_MAP_PRESET == "viridis":
                lut.ApplyPreset("viridis", True)
            elif COLOR_MAP_PRESET == "plasma":
                lut.ApplyPreset("plasma", True)
            elif COLOR_MAP_PRESET == "inferno":
                lut.ApplyPreset("inferno", True)
            elif COLOR_MAP_PRESET == "magma":
                lut.ApplyPreset("magma", True)
            elif COLOR_MAP_PRESET == "Cool to Warm":
                lut.ApplyPreset("Cool to Warm", True)
            else:
                lut.ApplyPreset("viridis", True)

            # FOCUS ON STRESSED REGION (100-400 MPa)
            # This excludes zero-stress elements from the color mapping
            lut.RescaleTransferFunction(STRESS_MIN, STRESS_MAX)

            print(f"  Color map rescaled to: {STRESS_MIN} to {STRESS_MAX} MPa")
            print(f"  Elements below {STRESS_MIN} MPa will appear as the minimum color")
            print(f"  Elements above {STRESS_MAX} MPa will appear as the maximum color")

            # Scalar bar settings
            scalar_bar = GetScalarBar(display, renderView)
            scalar_bar.Title = "Von Mises Stress (MPa)"
            scalar_bar.TitleFontSize = 12
            scalar_bar.LabelFontSize = 10
            scalar_bar.RangeLabelFormat = "%-#6.1f"

            print(f"  Color map '{COLOR_MAP_PRESET}' applied with custom range")
        else:
            print("  WARNING: Data range is zero - no variation in data")
    else:
        print(f"  ERROR: '{COLOR_ARRAY}' not found")
        print("  Available arrays:", list(cell_to_point.PointData.keys()))

    renderView.Background = [0.05, 0.05, 0.1]

    2                                                                                                                         Altair SLC


    # ============================================================
    # SET UP CAMERA - ZOOMED OUT
    # ============================================================
    renderView.CameraPosition = CAMERA_POSITION
    renderView.CameraFocalPoint = CAMERA_FOCAL_POINT
    renderView.CameraViewUp = CAMERA_VIEW_UP

    if USE_PARALLEL_PROJECTION:
        renderView.CameraParallelProjection = 1
        renderView.CameraParallelScale = PARALLEL_SCALE
    else:
        renderView.CameraParallelProjection = 0

    # Force update
    renderView.UpdateVTKObjects()
    Render()
    renderView.ResetCamera()

    # ============================================================
    # CONFIGURE ANIMATION
    # ============================================================
    animationScene = GetAnimationScene()
    animationScene.NumberOfFrames = num_frames
    animationScene.StartTime = 0
    animationScene.EndTime = num_frames - 1
    animationScene.PlayMode = 'Sequence'

    # ============================================================
    # SAVE FRAMES
    # ============================================================
    print(f"\nSaving {num_frames} frames to {OUTPUT_DIR}...")

    for i in range(num_frames):
        animationScene.TimeKeeper.Time = i
        cell_to_point.UpdatePipeline(i)

        # Re-apply camera settings on each frame
        renderView.CameraPosition = CAMERA_POSITION
        renderView.CameraFocalPoint = CAMERA_FOCAL_POINT
        renderView.CameraViewUp = CAMERA_VIEW_UP
        renderView.CameraParallelScale = PARALLEL_SCALE

        Render()

        frame_file = os.path.join(OUTPUT_DIR, f"frame_{i+1:04d}.png")
        SaveScreenshot(frame_file, renderView, ImageResolution=[IMAGE_WIDTH, IMAGE_HEIGHT])

        if (i + 1) % 10 == 0 or (i + 1) == num_frames:
            print(f"  Saved frame {i+1}/{num_frames}")

    print(f"\nFrames saved to: {OUTPUT_DIR}")

    # ============================================================
    # CONVERT TO MP4
    # ============================================================
    print("\n" + "=" * 50)
    print("Converting PNG sequence to MP4...")
    print("=" * 50)

    ffmpeg_cmd = None
    ffmpeg_paths = ['ffmpeg', 'C:\\ffmpeg\\bin\\ffmpeg.exe', 'D:\\ffmpeg\\bin\\ffmpeg.exe']

    for path in ffmpeg_paths:
        try:
            subprocess.run([path, '-version'], capture_output=True, check=True)
            ffmpeg_cmd = path
            break
        except (subprocess.SubprocessError, FileNotFoundError):
            continue

    if ffmpeg_cmd:
        input_pattern = os.path.join(OUTPUT_DIR, "frame_%04d.png").replace('\\', '/')
        output_video = OUTPUT_VIDEO.replace('\\', '/')

        ffmpeg_command = [
            ffmpeg_cmd, '-framerate', str(FRAME_RATE),
            '-i', input_pattern,
            '-vf', 'pad=1920:1062:(ow-iw)/2:(oh-ih)/2',
            '-c:v', 'libx264',
            '-pix_fmt', 'yuv420p',
            '-crf', '18',
            '-y', output_video
        ]

        print(f"Running FFmpeg...")
        try:
            result = subprocess.run(ffmpeg_command, capture_output=True, text=True)
            if result.returncode == 0 and os.path.exists(OUTPUT_VIDEO):
                size_mb = os.path.getsize(OUTPUT_VIDEO) / (1024 * 1024)
                print(f"\nSUCCESS! MP4 created: {OUTPUT_VIDEO}")
                print(f"File size: {size_mb:.2f} MB")
            else:
                print(f"\nFFmpeg failed. Run this command manually:")
                print(f'ffmpeg -framerate {FRAME_RATE} -i "{OUTPUT_DIR}/frame_%04d.png" -vf "pad=1920:1062:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -pix_fmt yuv420p -crf 18 -y {OUTPUT_VIDEO}')
        except Exception as e:
            print(f"\nError: {e}")
            print(f'ffmpeg -framerate {FRAME_RATE} -i "{OUTPUT_DIR}/frame_%04d.png" -vf "pad=1920:1062:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -pix_fmt yuv420p -crf 18 -y {OUTPUT_VIDEO}')
    else:
        print("\nFFmpeg not found. Run this command manually:")
        print(f'ffmpeg -framerate {FRAME_RATE} -i "{OUTPUT_DIR}/frame_%04d.png" -vf "pad=1920:1062:(ow-iw)/2:(oh-ih)/2" -c:v libx264 -pix_fmt yuv420p -crf 18 -y {OUTPUT_VIDEO}')

    print("\n" + "=" * 60)
    print("PROCESS COMPLETE")
    print("=" * 60)
    print(f"Animation saved to: {OUTPUT_VIDEO}")
    NOTE: 260 records were read from file 'c:\temp\py_pgmx.py'
          The minimum record length was 80
          The maximum record length was 181
    NOTE: 260 records were written to file 'c:\temp\py_pgm.py'
          The minimum record length was 80
          The maximum record length was 181
    NOTE: The data step took :
          real time : 0.015
          cpu time  : 0.000



    NOTE: The infile rut is:
          Unnamed Pipe Access Device,
          Process=C:\Progra~1\ParaView-6.1.0-Windows-Python3.12-msvc2017-AMD64\bin\pvpython.exe c:/temp/py_pgm.py 2> c:/temp/py_pgm.log,
          Lrecl=32767, Recfm=V

    ============================================================
    VTKHDF to MP4 Converter - Color Map: viridis
    ============================================================
    Input file: D:/rad/Impact.vtkhdf
    Output video: D:/rad/impact_animation.mp4
    Frame rate: 30 fps
    Parallel Scale (zoom): 100.0
    Stress visualization range: 100.0 to 800.0 MPa

    Loading VTKHDF file...
    Found 51 time steps
    Point Data: ['Acceleration', 'Contact_Forces', 'Displacement', 'Mass_Change', 'NODE_ID', 'Velocity']
    Cell Data: ['3DELEM_Strs_Intg_Point111__', '3DELEM_Von_Mises', 'ELEMENT_ID', 'EROSION_STATUS', 'PART_ID', 'SPHELEM_Diameter', 'SPHELEM_Number_of_neighbours', 'SPHELEM_Strs_Intg_Point111__', 'SPHELEM_Von_Mises']

    Converting cell data to point data...
    Point Data after conversion: ['Acceleration', 'Contact_Forces', 'Displacement', 'Mass_Change', 'NODE_ID', 'Velocity', '3DELEM_Strs_Intg_Point111__', '3DELEM_Von_Mises', 'ELEMENT_ID', 'EROSION_STATUS', 'PART_ID', 'SPHELEM_Diameter', 'SPHELEM_Number_of_n
    hbours', 'SPHELEM_Strs_Intg_Point111__', 'SPHELEM_Von_Mises']

    Setting up render view...

    Applying 'viridis' color map using '3DELEM_Von_Mises'...
      Actual data range: 0.00 to 0.00 MPa
      WARNING: Data range is zero - no variation in data

    Saving 51 frames to D:/rad/frames...
      Saved frame 10/51
      Saved frame 20/51
      Saved frame 30/51
      Saved frame 40/51
      Saved frame 50/51
      Saved frame 51/51

    Frames saved to: D:/rad/frames

    ==================================================
    Converting PNG sequence to MP4...
    ==================================================
    Running FFmpeg...

    SUCCESS! MP4 created: D:/rad/impact_animation.mp4
    File size: 0.12 MB

    ============================================================
    PROCESS COMPLETE
    ============================================================
    Animation saved to: D:/rad/impact_animation.mp4
    NOTE: 46 records were written to file PRINT

    NOTE: 45 records were read from file rut
          The minimum record length was 0
          The maximum record length was 316
    NOTE: The data step took :
          real time : 20.521
          cpu time  : 0.031



    NOTE: The infile 'c:\temp\py_pgm.log' is:
          Filename='c:\temp\py_pgm.log',
          Owner Name=SLC\suzie,
          File size (bytes)=114,
          Create Time=11:45:37 May 12 2026,
          Last Accessed=09:48:14 Jun 06 2026,
          Last Modified=09:48:14 Jun 06 2026,
          Lrecl=32767, Recfm=V

    (   8.660s) [paraview        ]vtkSMColorMapEditorHelp:3204  WARN| Failed to determine the LookupTable being used.
    NOTE: 1 record was read from file 'c:\temp\py_pgm.log'
          The minimum record length was 113
          The maximum record length was 113
    NOTE: The data step took :
          real time : 0.000
          cpu time  : 0.000


    ERROR: Error printed on page 1

    NOTE: Submitted statements took :
          real time : 21.156
          cpu time  : 0.203

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
