# GRSISort sort code cheat sheet

This document contains tips and tricks for developing sort codes using GRSISort (https://github.com/GRIFFINCollaboration/GRSISort).

## Loading calibration files

Event when sorting from a fragment tree, a calibration file is needed in order to get and use channel numbers, as well as get proper timestamp units.

### Code snippet

```
#include "TParserLibrary.h"
#include "TEnv.h"
#include "TChannel.h"

//load configuration, needed to access channel numbers, and to load the proper time stamp units

std::string grsi_path = getenv("GRSISYS"); // Finds the GRSISYS path to be used by other parts of the grsisort code
if (grsi_path.length() > 0) {
  grsi_path += "/";
}

// Read in grsirc in the GRSISYS directory to set user defined options on grsisort startup
grsi_path += ".grsirc";
gEnv->ReadFile(grsi_path.c_str(), kEnvChange);
TParserLibrary::Get()->Load();

char const * calfile;
calfile = argv[2]; 
printf("Reading calibration file: %s\n", calfile);
TChannel::ReadCalFile(calfile);
```

