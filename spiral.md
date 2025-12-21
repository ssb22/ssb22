
from https://ssb22.user.srcf.net/elec/spiral.html (also [mirrored on GitLab Pages](https://ssb22.gitlab.io/elec/spiral.html) just in case)

Back to [lighting notes](lighting.md)

# Spiral CFLs in tight fixtures

This approach may be no longer needed now [flicker-dampened A19/A60 LED-filament bulbs](lighting.md) are available.

Many CFL bulbs sold in the UK are of the straight, “U-bend” type, whereas America has sold more of the spiral “twisted” type (some Americans think *all* CFLs are that shape).

The “straight” bulbs are said to last longer due to better heat dissipation, although the brightness still reduces during the lifetime. Straight bulbs may also leak less UV, because UV leaks tend to arise from phosphor imperfections in the tube’s bends, so the more curvature the more UV leakage (although “straight” bulbs do still have *some* curvature and leakage).

Spiral “twisted” CFL bulbs, however, are said to pack more light into a smaller size (specifically, a smaller height) than the “straight” CFL bulbs. If true, this can be useful in fixtures where bulb size is limited, and where the possible extra UV emissions will be absorbed by the fixture anyway (full-enclosure or uplighter)—since these fixtures reduce the brightness, being able to have more light to start with could be helpful.

## Light loss due to tube occlusion

A potential cause for concern: the spiral lamps might well pack more *tube* into a smaller height, but if too much of that tube is *hidden behind other sections of tube* then it won’t necessarily result in more *light* being delivered to the room. So how do we check the light-distribution efficiency of different tube packings?

Assuming that phosphor has a fixed brightness per unit area and we wish to maximise visible area, a naive approach would be to look at the bulb from a fixed distance and calculate the total visual angle occupied by phosphor, averaging this over different rotations of the bulb (or calculate the total visual angle *not* occupied by phosphor from the viewpoint of an imaginary microscopic observer fixed to the surface of a tube and looking away from it, and average this over different points on the tube), and use this as a comparison metric for different bulbs. But this does not account for the *fixture* , which may not treat all directions as equal. For example, a pendant uplighter with a screw at the bottom might absorb nearly all of the downward-pointing light (the light that hits the screw) while transmitting or reflecting the light coming off of the bulb in horizontal directions, whereas a globe enclosure might result in the downward part of the light becoming more important. So the visual angles from each observation point would at least have to be multiplied by a correction factor to account for the desirability of light going toward that particular observation point.

As an approximate check for the horizontal-light case, I held up a “straight” CFL against a black background and rotated it in front of a video camera (trying to rotate as steadily as I could by hand; it might have been better if I’d had lab equipment). I then converted the video into a series of .jpg files via `mplayer -vo jpeg` (you can also use `-ss` to set the starting second and `-endpos` to set the length), and sampled a column of pixels cutting across the bulb (which I was pointing “sideways”) using NetPBM:

`for N in *jpg; do jpegtopnm $N | pnmcut -left 300 -bottom 300 -width 1 -height 200 | ppmtopgm | pamthreshold | pnmtoplainpnm | grep 1$|wc -l;done > pixel-counts.csv`

and, after verifying with a spreadsheet’s chart tool that my chosen column and time bounds did indeed exhibit roughly the pattern I’d expected (there were 3 “U-bended” tubes connected to the base on 6 equidistant points of a circle, so I was expecting the opacity to have minima at 6 or 12 viewing positions and maxima in between), read off that:
* The lowest opacity was about 85% of the highest. This lowest opacity corresponded to rotational positions when two of the six half-tubes were completely occluded (apart from their common bend at the end) and another two of the half-tubes were each about one-third occluded, giving a total tube-occlusion figure of about 45%, so at highest opacity I’d expect the tube-occlusion to be 35%.
* The average (mean) opacity was about 92% of the maximum, so the average tube occlusion, and therefore average loss of light due to tube occlusion (averaging over all horizontal viewing angles), is about 40%.

In other words, this CFL is likely to distribute about 40% less light than it would if its half-tubes could somehow be stuck end-to-end into a strip and suspended in empty space. (A typical strip-light *fixture* , however, might lose 30% or more of the strip’s light anyway, so it wouldn’t be *very* much more efficient than an unshaded CFL. But leaving the CFL unshaded does risk some exposure to UV leakage from its curved parts, and a strip can easily “beat” the efficiency of a shaded CFL if you don’t mind installing strip lighting in the room. On the other hand CFLs do make it easier to change your mind about size without rewiring the ceiling.)

Loading a photograph of a “3-rung” spiral CFL into a drawing program and painting black the “back” halves of its tubes leads to 80% of the original picture’s tube pixels still showing, which corresponds to a 38% loss due to tube occlusion. Within the bounds of this experiment’s (in)accuracy, that’s more or less the same as the 40% losses of the straight CFL. It might increase to 45% if the spiral has more “rungs”.

## Fitting into a restrictive fixture

“Classic” tungsten light bulbs (and their halogen replacements) are around 110mm high and 60mm wide, and the most restrictive fixtures tend to allow not much more room than this.

Straight CFLs of height 115mm (including base and electronics; half-tube height 55mm) are only 11W and rated between 600 and 650 lumens. I don’t know if these ratings account for the 40% loss due to tube occlusion, but they tend not to account for the 20% drop in brightness that occurs during the bulb’s lifetime (mostly toward the beginning), so we could be looking at anything between 290 and 520 lumens when the bulb is not brand-new. By comparison, an old 60W (halogen 43W), to which the 11W CFL is supposed to be equivalent, should be between 700 and 800 lumens (depending whom you ask) whereas an old 40W is about 450 lumens.

Spiral CFLs of the same height are available at 20-23W and rated 1100+ lumens (880 after a 20% drop). They are wider than the “straight” CFLs, but should still be within the fixture’s allowed width.
* However, the 20W 1100lm “Pro-Elec” spiral we bought had very poor lumen maintenance: it dropped to about 400 lumens within 22 months.

**Beware** that not all 20-23W spiral CFLs are physically as short as the most compact ones—if in doubt, it might be necessary to measure, which is awkward if it’s online and dimensions are not supplied. Trying to judge from a photograph (using general guidelines like “the metal connector should take at least 1/5 of the total height” for A60) can lead to errors of 1cm+, and some sellers re-use photographs of other similar-looking bulbs without noting the size difference.

Replacing an 11W “straight” CFL with a 20-23W “twisted” one should increase the light output by a factor of about 1.7 (more when the bulb is new). 1100 lumens is “old 75W”, which should end up being a little brighter than “old 60W” after the 20% drop (assuming these lumen figures account for tube occlusion)—although the results could be worse if you happen to have chosen a model with poor lumen maintenance.

Spiral CFLs can usually be sourced online (even from the UK), but be sure to specify the B22 socket type if that is what you have, and beware the note about dimensions above.

You’d get even more light into the same space if you install a 100W B22 halogen (said to be equivalent to the old 150W), but that might sometimes be too much. If I’m installing bulbs in a room with several fixtures that are individually switchable, I try to make them *different* brightnesses so the user can choose depending on what they’re doing, but appropriately-shielded table lamps and task lighting can also help with this.

## UV reflection from the ceiling

A concern with open-topped uplighters in particular is the amount of UV reflected from ceiling paint, especially if more tube curvature (and hence more UV leakage) is visible from the ceiling to begin with. It’s hard to find good data on indoor paints, but Perkin Elmer reported 6-8% reflection at 300nm (UVB) from *outdoor* painted panels (any hue), and a company called Lumacept (which sells UV-reflective paint for hospital rooms where UV decontamination devices are likely to be used) rates standard indoor paint as reflecting 3-7% of UVC. An attenuation to 6-8% is equivalent to increasing the distance by a factor of 3.5 to 4 (intensity is quartered for every doubling of distance). ARPANSA’s March 2015 factsheet said no CFL reached the UV daily exposure limit in 8 hours at 25cm—their team confirmed to me they meant the limit of the entire 250-400nm spectrum (UVA/UVB/UVC), not the larger UVA-only limit—so if you were standing 30cm below an uplighter that hangs ~30cm from the ceiling, you should get less than 0.08% of this (i.e. <24mJ) per hour.

Copyright and Trademarks:
All material © Silas S. Brown unless otherwise stated.
Any [trademarks](https://ssb22.user.srcf.net/trademarks.html) I mentioned without realising are trademarks of their respective holders.
