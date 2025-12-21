
from https://ssb22.user.srcf.net/elec/lighting.html (also [mirrored on GitLab Pages](https://ssb22.gitlab.io/elec/lighting.html) just in case)

# Lighting notes

This is posted in the hope that it is useful but **without any warranty**. LED | CFL | Halogen | Pygmy | ESL | Task lighting | Spectrum issues

## LED room-light flicker

My notes on this were superseded by excellent discussions of flicker at [LEDBenchmark Australia](https://web.archive.org/web/20250112112424/http://ledbenchmark.com/faq/LED-Flicker-Measurement.html) (Internet Archive link as it went down in 2025) and [German consultant Peter Erwin](https://www.derlichtpeter.de/en/light-flicker/cfd/), and the IEEE took notice and published their recommendations in a 76-page standard: IEEE 1789-2015.

IEEE 1789 limits driver-circuitry’s flicker modulation fraction to Hz/1250 of frequencies above 90Hz and Hz/4000 of those below, with an additional 2½× reduction recommended (and plenty of studies are cited to show that we sufferers are *not just making this up*—stroboscopic “phantom array” effects are particularly irritating if you have a condition like nystagmus to aggravate your saccade movements and V5 blindsight to make you more sensitive to peripheral movement at photopic light levels, but sales personnel tend to confidently deny any LED products flicker because *they* don’t see it). Hopefully the existence of IEEE 1789 will now increase the number of off-the-shelf LED products with acceptably low flicker, but it’s still rarely discussed on packaging.

### B22, E27 etc LEDs
* In 2018 we bought a Morrison-branded R63 6W 450 Lumens ES “spot” and a large “GLS” 15W 1521 Lumens ES, to replace 2 bulbs in a 5-lamp screw-fixture ceiling in Dorset, and I was not able to see flicker or detect it with a phone camera held close to the light. But Morrison have since stopped selling these items.
* I was not able to see or detect flicker from a Morrison-branded A60-size 1521-lumen B22 11W 2700K “100W equivalent” bought in Dorset in 2022.
* I had only slight suspicion of negligible flicker from two ‘traditional A60 size’ B22 bulbs that fit restricted uplighters: a Philips CorePro 1521-lumen “13W=100W” stocked by RS (which was dimmed by the uplighter as most light hit the bottom), and an Osram/Ledvance dimmable 806-lumen “7W=60W” pearl LED-filament (EAN 4058075808249, expected to maintain 70% of its lumens during its rated service life) bought from Argos, in 2018. A third bulb however gave a little more flicker (but still not detectable on a phone camera)—it was an Integral-LED “12W=100W” 1521lm 300° 2700K dimmable filament GLS (and this is *not* A60 size even though it has the ‘classic’ shape: it’s an enlarged version so won’t fit in tight uplighters)—so you still have to be a bit careful.
* In 2016 we saw a non-flickering LED bulb in a DFS showroom (not for sale); I believe it was a Luceco LA22W10W81 (810-lumen 10W).
* We also noticed IKEA’s *lower*-lumen bulbs sometimes flicker less, but they’re not suitable when more light is required unless you have room for many of them. These are available in the UK but require adaptors if you have B22 sockets; IKEA usually sell them in their own table lamps. The interference added to Radio 3’s FM signal on a nearby portable suggests that the 4W 200lm “LED1206C4” (E14/SES) uses an improperly-shielded high-frequency modulator to evade visible flicker.
* And we found no flicker on some “Diall” bulbs from B&Q installed in a house: they were LP-A65-1S (9W 806lm, B22 and E27) and LP-A60-11S (6W B22). We also found no flicker on Diall’s E27 “reflector” (R63) bulbs bought in 2022 (470lm and 600lm “warm white”)—keep the receipt as ours had a 22% early-failure rate—but we *did* find flicker on a Diall 78mm R7S (for a patio light) and on Diall integrated downlights (see below), so *some* Diall models can flicker. (An unbranded 12W replacement R7S in 2025 did not flicker but lacked enough information for us to know where the private seller had obtained it.)
* We found no to negligible flicker on a set of 4 Anwio R63 E27 806lm WiFi (Tuya) “smart” bulbs bought in 2023 or their A60-size equivalents in 2024.

### Integrated LED fixtures
* We *did* get flicker from a Diall socketless 5W IP65 downlight bought in 2022, which was a let-down after their better B22 and E27 lamps. B&Q accepted a return.
* We found no noticeable flicker (including with a camera test) from a set of HCL-218A under-cabinet downlighters from Howdens. These are not intended as full-room lighting.
* We found no noticeable or camera-detected flicker from a Novostella 24W 2650-lumen “Tunable White LED Ceiling Light” (a larger circular flush fixture with infrared remote control—its codes can be input into third-party infrared devices like Tuya’s, although Tuya’s Alexa interface is on/off only when used via infrared).
* We initially found only 1 out of 18 bulbs were flickering in a set of dimmable 240V downlights, reportedly Luceco “F-Eco” 450lm IP65, but a second set of 8 of these *all* flickered. We think Luceco changed a driver component without changing the product name.

### LED tubes

In 2024 and 2025 in Dorset we bought V-Tac VT-151 and Philips “LED tubes” designed to replace 5-foot fluorescent strip lights without requiring removal of old-style magnetic ballasts (they were supplied with “LED starters”—straight-through connections with fuse—to replace the fluorescent starters), and we found no noticeable or camera-detected flicker from either. The Philips initially didn’t work at all and I think some Toolstation staff are reluctant to believe the product is genuinely faulty: I had one who implied I didn’t know the difference between magnetic and electronic ballasts, gave me a replacement anyway but put the returned tube back in stock for another customer, so keep your receipt!

### Other LED
* Peter Erwin’s [Der Lichtpeter test results](https://www.derlichtpeter.de/en/light-flicker/market-tests/) may be useful in Europe, although less so in the UK because not many products for the UK’s common B22 socket type are included. There *are* some [B22s on LEDBenchmark’s list](https://web.archive.org/web/20180802192827/http://ledbenchmark.com/list.php?fitt=6&voltage=2&order=17) (Internet Archive link as LEDBenchmark went down 2025; consider only lamps that came lower than the incandescent in their flicker measurements) but these lamps can still be **hard to find in UK shops** (LEDBenchmark mostly tests Australian shops), and you’ll want to check for an *exact match* on the rated wattage etc—bulbs sold under the same name by the same manufacturer can have wildly different flicker performances across their wattages (and **do not** assume any given company’s newer bulb will be better than its older counterpart—beware of “no but we have a newer version” sales: it **might not be the same thing**).
* A professional LED installation with a very good high-frequency driver (e.g. eldoLED, retailed in the UK by Phos of Hatfield) is usually flicker-free but expensive.

Many LED lamps are also subject to phosphor degradation over time.

### Battery and USB-powered LEDs

In 2025 an unbranded USB-chargeable wood-effect bird paperweight light (switchable between cool white, warm white or a mixture, with red charging light) whose circuit was marked with “CHX-E-126-D” defaulted to a brightness setting that wasn’t full and was using headache-inducing PWM synthesised by its unmarked 8-pin IC; however it was possible to change the brightness by holding down on the touch sensor (this was not documented) and there was no PWM at full brightness.

A columnar lamp of similar interface but without the battery (USB-powered only)—Shantou Youle Ming Electronic Technology Co No.3118—did not exhibit flicker at any brightness setting. However it had a constant red light when connected, and when we opened the device to occlude this, we were unable to reconnect the touch sensor to the diffuser so we had to use it bare-circuit.

A disc-shaped USB-chargeable no-button motion detection light whose circuit was marked CANYN 888 MZL-PIR V4 LT-16256 SN-2616 had no flicker. Separately, a 600-lumen “Solar Interaction Wall Lamp” model TK-888 exhibited no flicker in its full brightness mode but PWM’d in other modes.

## CFL phosphor leakage and degradation

21st-century versions of “energy saving” CFL bulbs (with high-frequency electronic ballasts) give reasonably good light but they have other issues, not least of which is decreased availability when more retailers prefer LED.

Due to concerns about UV leakage, CFLs should not be used at short distances (see task lighting).
* UV reduces with greater distance, lower wattage, full-enclosure lampshades, or “globe” bulbs (which cover the tube), but these strategies also reduce the brightness. It’s possible that “straight” CFLs leak less UV than “twisted” ones that stretch the phosphor more, but both types are susceptible. (If you have shades/fittings that block UV but are tight, you might want spirals for [more brightness in limited space](spiral.md).)

Additionally, all CFLs (like any phosphor-based device) gradually dim due to phosphor degradation.

Details:
* If you’re not sure how much your light has degraded, you could try using a light meter.
  * If a dedicated light-meter device is not available, you might get a reading from a mobile phone but *beware* any app that relies only on the phone’s camera is likely to be highly inaccurate (as in “could be wrong by a factor of 10”)—it’s better if the phone has a separate light-intensity sensor which can be read, e.g. by [GPS Status & Toolbox](https://ssb22.user.srcf.net/setup/android.html#gps).
  * In theory the lux value is the lumens divided by (4 × pi × the square of the distance in metres), but that only counts *direct* light—in a near-white room with good fixtures like uplighters, light reflected from the ceiling and walls can *triple* the illuminance of direct light, so an old 60W incandescent should give around 45 lux on the floor, 100W should give 90+ lux and 150W should give 150+ lux.
  * If you have an incandescent or halogen light with roughly known output, you can use this to calibrate your readings to the room’s reflection characteristics.
* Dim CFLs might not be a problem **if** good task lighting is also available, such as a good desk lamp.
* If bright light is important and task lighting is not available, then you could:
  1. Replace the bulb **before** the end of its life
     * CFL bulbs contain mercury (which also makes them unhealthy in an accident); LEDs contain no mercury but they are still electrical waste—reportedly some contain small amounts of lead and arsenic. Recycling facilities at large shops etc are now more common (I hope they don’t have hidden downsides); if you can’t get to one of these then the environmental cost of early replacement is greater.
     * Alternatively the dim bulb could be kept as an emergency spare, or moved to a location where brightness is less important (if one exists)
  2. Run **several** dim bulbs instead of one bright one (if you have the fittings)
     * This uses more power, which might or might not outweigh the cost and environmental impact of early replacement (depending on how often it saves a replacement); it also increases the UV.
  3. Choose a bulb with higher-quality phosphor that stays bright for longer (lumen maintenance)
     * You could pay a review database (Which, Choice, etc) for the results of their stress tests on currently-available bulbs
     * Some approval marks carry minimum requirements but these can be lenient (e.g. the American “Energy Star” specification v4.3 allowed the brightness to drop to 80% after 40% of the rated life, with 30% of the sample dropping below 75%, and said nothing about what happens after that time)
  4. Choose a bulb that is *too* bright to start with
     * Again this uses more power, see above
     * If you need to go beyond “100W equivalent”, it could mean expensive horticultural lights.

In areas with high humidity and/or short running times (e.g. small kitchens or bathrooms), CFL *electronics* can cut out early. If this happens often enough to make CFLs uneconomical and unenvironmental (because you “get through them” too quickly) then see below.

## Incandescents for humid rooms

If you experience CFLs cutting out very quickly in humid rooms, and you cannot control the humidity, you might be stuck with bulbs that do not include PCBs, which means either flickering non-rectified LEDs or hot power-hungry incandescents (switch off whenever possible).

(These notes assume the room does not have fluorescent tube fittings. If it does then you might have a problem: some high-frequency flicker-free electrical ballasts can take only 85% RH and only for 30-60 days/year; others are more tolerant, but many fittings try to be robust by using a magnetic ballast, which flickers at twice the mains frequency and might also flicker *at* the mains frequency if the tube’s electrodes are bad. You might at least be able to replace the starter with an electronic one for slightly nicer startups.)
* The EU’s 2009-2018 phase-out of incandescents concluded with most halogen bulbs being banned from production in September 2018, but you might have access to old stock.
  * A **B22 halogen** (e.g. 42W for “60W equivalent”) might be the best option for small kitchens that can’t take CFLs, but check if it really *is* equivalent to 60W (i.e. 700 to 900 lumens; calling a 600-lumen bulb “60W” is dubious, and 42W for that is category C).
  * While halogens don’t save nearly as much as CFLs, a halogen upgrade **should still pay for itself** in less than an older bulb’s lifetime, so anyone who has stockpiled older bulbs should be better off not using them and buying halogens.
  * Halogens could also be an option if a *lot* of light is needed and bulb size is limited, since a 100W “150W equivalent” halogen fits in an A60 B22 bulb; that brightness is still not readily available in a small LED/CFL bulb as of end-2018. If a room has two switches you could consider fitting a ‘normal brightness’ bulb on one and a ‘super-bright’ bulb on the other for occasional use.
* Refrigerator and oven bulbs were not banned
  * A **clear 15W “Pygmy” refrigerator bulb** can dimly light a small bathroom (if it’s B22), but don’t try this in a work area.
  * It might also be useful in small areas where a ceiling-level cupboard door collides with a pendant light due to inappropriate cable length.
  * Beware of 25W Pygmy bulbs: clear 15W is typically rated at 90 to 105 lumens, but clear 25W can come as low as 120 lumens (the extra brightness seems hardly worth the wattage); you might be able to get a 190-lumen one but these are not typical stock.

## ESL unsuitable for UK use?

ESL bulbs use an unfocused electron beam on phosphor. As of 2011 it’s difficult to find 240V ones, and they might turn out to be too heavy for the UK—a B22-to-E27 adapter won’t overcome the effective weight limit of a Bayonet socket. Also Vu1 haven’t yet explained how they’ve avoided X-rays in their unshielded bulbs (does their phosphor allow the use of lower-energy electrons?)

## Task lighting
* A fluorescent desk lamp can be positioned closer to the work than an incandescent (useful in conjuction with a [“Hedgehog” magnifier](hedgehog.md)).
* Some people put CFLs into old reading lamps (Anglepoise etc), but if the shade is not large enough to cover the CFL then it may glare (especially when positioned closely) and might also lead to UV exposure because CFL safety standards assume ceiling use. (UV is reduced if the desk lamp is placed further away or light is bounced off a wall, but this also reduces light levels.)
* A purpose-designed fluorescent fixture is better, but some of them have ballasts that become annoyingly noisy later (and are also inefficient).
* Flicker-free LED desk lamps with high-frequency drivers are available, but are expensive and tend to have lower lumen ratings than other types of lamp. If buying one then make sure it really *is* flicker-free—the product literature should claim a driving frequency of kHz or MHz (not just Hz).

## Spectrum issues

Certain brain disorders, such as Irlen’s syndrome (scotopic sensitivity, identifyable if high-contrast symbols on a printed page sometimes seem to move), and possibly some forms of autism, can result in sensitivity to certain wavelengths of light being overly prominent in the spectrum; the exact wavelengths depend on the individual and are typically addressed using customized eye or page filters, but lighting will obviously have an effect.

The spectral pattern (spectral power distribution) of non-incandescent lighting usually depends on the manufacturer’s phosphor chemistry and is likely to have “spikes” at frequencies corresponding with each chemical. Higher CRI “soft white” bulbs typically use more chemicals to reduce the prominence of particular spikes, but it’s hard to approach incandescent’s CRI=100 without using halogen. (It’s possible that phosphor-driven bulbs will irritate less if a “main” lamp is halogen and the others merely add “background” ambient light, but this again depends on the individual.)

Copyright and Trademarks:
All material © Silas S. Brown unless otherwise stated.
Anglepoise is a registered trademark of Anglepoise Holdings Limited.
Anwio is a trademark of Shanghai Denglian Trading Co., Ltd.
CorePro is a trademark of Philips Lighting Holding B.V.
DFS is a trademark of DFS Group Limited.
IEEE 1789 is a trademark of the IEEE.
Ledvance is a trademark of LEDVANCE GmbH.
Osram is a trademark of OSRAM GmbH.
Toolstation is a trademark of Toolstation Ltd.
Wi-Fi is a trademark of the Wi-Fi Alliance.
Any other [trademarks](https://ssb22.user.srcf.net/trademarks.html) I mentioned without realising are trademarks of their respective holders.
