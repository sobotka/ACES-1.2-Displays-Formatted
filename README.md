# ACES-1.2 Colourimetric Displays Edition

## What Do I Need to Know to Use This in Blender?

This configuration has been modified slightly to provide additional data such as an XYZ role that the Sky and Wavelength shaders depend on to find the rendering space. Additionally, several Blender-specific roles have been added to set default color spaces for textures.

Despite this, due to limitations in Blender some aspects are NOT FIXABLE. These are as follows:

* Blackbody Node (including Principled Volume): Cycles' Blackbody shader does not support non-sRGB colors. It always generates sRGB/709 output colors, which will then be used by the rest of the shading system as though they were ACEScg colors. This results in oversaturation of colors other than 6500K. (Note that this shader also uses 6500K as a whitepoint, even if this is not the rendering space white point).

* Principled Hair: Melanin colors are hardcoded as sRGB/rec709. Results will be oversaturated.

* Wavelength Node: While this node functions correctly, due to the wider (AP1) rendering primaries used with ACES this shader produces visually different results than it does when using linear-sRGB as the rendering space. This is most commonly seen with low wavelengths (ex 400nm) producing less magenta under ACES than they do under linear-sRGB. THIS IS NOT A BUG OR A COLOR MANAGEMENT ERROR.

* Color Pickers - HSV: The HSV tab of Blender's color picker and the color-wheel widget will not function correctly when using ACES.

* Color Pickers - Color spaces: All RGB values entered in color pickers are in ACEScg space. Old scenes will not be modified automatically, previously entered sRGB/709 values will be used as is but treated as if they were ACEScg. They will need to be manually converted from linear-sRGB to ACEScg.

* Color Pickers - Hex codes: The hex code tab of Blender's color picker does not produce meaningful output under ACES and should be ignored.

* Material Preview Mode: The built-in background HDRIs are not properly converted to ACEScg before rendering, and will appear over saturated.

A note about float textures: Floating point textures (such as OpenEXR files) will be use the ACEScg input space by default. This is consistent with the normal ACES workflow and standard OCIO configuration. However, please bear in mind this is not the correct input space for most HDRI maps you will find on stock texture sites. Most of these files are prepared with Linear sRGB primaries instead of ACEScg. In order to handle this, the input space should be changed to "Utility - Linear - sRGB"

## What is This?

This is a directly generated repository of the as-official-as-possible ACES 1.2 configuration.

## Why Does This Exist?

The official OpenColorIO configurations for ACES is a huge slew of transforms, which are utterly confusing to use for a majority of normal people. They are this way because ACES has to work with existing applications, many of which are not entirely working properly with regards to OpenColorIO implementation. Therefore, the poor audience member is faced with ACES working versus not working because some applications have unresolved OpenColorIO issues.

## How is this Different?

This is the same transforms, at the same 65 edge cube depth, generated via the proper Python configuration, untouched. The difference is in a configuration detail provided in the Python generation script which breaks out all of the displays into sane and proper colourimetric silos. The TL;DR is that there's one nice sRGB output display, not a slew of transforms under one general `ACES` display class.

## Who is This For?

This is for anyone seeking to use the slightly more sane ACES 1.2 configuration in applications that support OpenColourIO better, and list Displays, Views, and Looks via the API. Some software has some crippling bugs that don't support whitespace for example. Take this, find the bugs, and try to get the software to get the fixes it needs.

## When Would This Version Be Default?

Good question. Follow the steps. Apply pressure to the software that isn't doing things properly.

To the ACES folks who are reading this, please do your part and support the sane breakdown as per OpenColourIO's design. Lead by example, and put pressure on the problematic software to do things the right way.

## How Was This Configuration Generated?

This configuration was generated using the Python scripts available in the offical and as-official-as-possible versions. The full configuration Python command line is as follows:

`aces_1.2/python/bin/create_aces_config -a aces-dev/transforms/ctl --lutResolution1d 4096 --lutResolution3d 65 -c aces_1.2 --createMultipleDisplays --dontBakeSecondaryLUTs`
