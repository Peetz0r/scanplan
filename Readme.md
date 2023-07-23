This is a messy set of messy script that I never really intended to put in git until now.

It assumes your scanner is a Canon Canoscan 9000F mk2 (which is not available anymore). It's SANE driver name is hardcoded and there are a bunch of hardcoded sizes and offsets for it's 35mm film holder.

Also the script are a messh of shell and python. The shell scripts depend on fish for no good reason other than that it's my prefered shell and I copypasten them from interactive sessions. They should someday become posix sh scripts. Especially since they're mostly `scanimage` oneliners.

You should collect 16 bit tiff samples of unexposed bits of each type of film stock in a directory and run the `film-base-to-txt` script there. It'll create text files containing the average color of those.

Every album directory should contain a file `film-base` which should be a symlink to a txt file created by `film-base-to-txt`. This will be used to properly compensate for the film base when inverting, without relying on auto(mis)detecting said colors.

When scanning regular 35mm film, you should:
- create a new directory
- run `35mm-neg-scan` for strips of 4 frames , or `35mm-neg-scan-6p` for strips of 6 frames
- use the button on the scanner to scan the strips of this roll
- if the film stock isn't in your film base catalog, then you should
  - probably while scanning the 2nd "page", aka 3rd and 4th strip: open out1.tif in GIMP or similar
  - crop out an unexposed bit of the film, export that as a tiff file
  - run `film-base-to-txt`
  - you should also do this for BW film, and you should make variations for pushed/pulled/expired/etc film
- create a symlink named `film-base` to the film base txt file
- if it's BW film, also create an empty file called `bw` (lack of this file tells the scripts that it's color film)
- when the physical scanning is done, you should run `35mm-neg-scans-to-pos-strips`
- look at the `strip*.tiff` files with an image viewer
- then run `35mm-strip-to-frame`
- now look at `frame*.tiff` and see the mess you made

I'm still working on improving the (embarrassingly simple) code that cuts out the frames from the strips, and the color correction, and everything else really.

I have scanned around 60 rolls of film and most of it is usable, but a lot of them have issues woith cropping and/or colors. Also, those that are mis-cropped are also usually mis-exposure-corrected because the black film base should (but itn't) cropped away.

However, since I always keep the out*.tiff files from scanimage around, I can declare the "scanning" finished.

I have also scanned around 240 slides with the oneliners in `dias.txt` ('dia' is Dutch for 'slide') but since those used much simpler hardcoded cropping and didn't need any color correction (only basic exposure and gamma corrections) I regard those as a seperate (and finished) project. But I included my notes anyway.
