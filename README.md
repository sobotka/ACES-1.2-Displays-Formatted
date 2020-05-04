# ACES-1.2 Colourimetric Displays Edition

## What is This?

This is a directly generated repository of the as-official-as-possible ACES 1.2 configuration. [The current state of the most official ACES 1.2 configuration is located via the Colour Science OpenColorIO configuration repository](https://github.com/colour-science/OpenColorIO-Configs/tree/feature/aces-1.2-config/aces_1.2).

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
