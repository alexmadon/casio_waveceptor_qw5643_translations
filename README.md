# casio waveceptor qw5643 translations

Translations to French and English of the Japanese user manual for Casio modules 5643 and 5575.

# Introduction


# TLTR: where is the translation?

The result of the translation to French is in the file

qw5643_french.html

# Technical details for extracting the images of the Japanase PDF file
## NOT WORKING well

pdf2svg big2tt.pdf big2ttout.svg
then select with inkspace

##  WORKING well

import PDF into inkscape, page 11
inkscape big2tt2.pdf
deep ungroup



https://www.reddit.com/r/Inkscape/comments/zas1pv/deep_ungroup/?onetap_auto=true


Open Inkscape.

Import the saved PDF document with all pages and internal (File | Import | All pages, Internal import, Replace PDF fonts by closed-named installed fonts, Embed Images, "OK")

Edit | Select All In All Layers.

Extensions | Arrange | Deep Ungroup ...

Deep Ungroup: Starting Depth 1, Stopping Depth (from top) 65535, Depth to Keep (from bottom): 0

Click Apply


with select tool, SHIFT + mouse drag to rectangle

copy

create new doc

paste into new doc

edit -> resize page to selection
file -> save


To resize an image in Inkscape, grab the Select Tool (keyboard shortcut: S) and click on the image to select it. Transformation handles should appear around the sides and corners. Click and drag one of those handles to resize your image. Hold the Control key to lock the aspect ratio.


## scripting

pdfseparate big2tt2.pdf pages_%02d.pdf

https://inkscape.org/forums/beyond/cli-pdf-import-combined-with-actions/

inkscape --pdf-poppler --pdf-page=1 --export-type=svg --export-text-to-path --export-area-drawing --export-filename tmp2.svg tmp.pdf

inkscape --pdf-poppler --pdf-page=1 --export-type=svg --export-text-to-path --export-area-drawing --export-filename pages_11.svg pages_11.pdf

clean japanese characters:

inkscape --pdf-page=1 --export-type=svg --export-area-drawing --export-filename pages_11.svg pages_11.pdf


```
for file in pages*pdf
do
echo doing $file
inkscape --pdf-page=1 --export-type=svg --export-area-drawing --export-filename $file.svg $file
done
```

inkscape -g --batch-process --actions="EditSelectAll;StrokeToPath;export-filename:tmp.svg;export-do;FileClose" tmp2.svg


# deep ungroup

https://stackoverflow.com/questions/68073876/inkscape-ungroup-everything-from-windows-command-line


```
python3 /usr/share/inkscape/extensions/ungroup_deep.py groups.svg > ungrouped.svg
```



```
for file in pages*svg
do
echo doing $file
python3 /usr/share/inkscape/extensions/ungroup_deep.py $file > ungrouped_$file
done

```

https://askubuntu.com/questions/686103/how-do-i-save-areas-of-an-inkscape-file-to-separate-svg-files
https://github.com/bcbnz/inkscape-pybounds/blob/master/bounds.py


use ESC to unselect

press MAJ drag left button mouse to select region
