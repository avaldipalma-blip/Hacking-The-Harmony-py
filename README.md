# Hacking-The-Harmony-py
[Hacking the Harmony.py](https://github.com/user-attachments/files/34299914/Hacking.the.Harmony.py)
# Title: Hacking The Harmony 
# Author/composer: Ava Lily Di Palma

# Description: Layered 8-bit synth track that builds from pads to drums, vocals, bass and piano over 48 measures
# with the kick running one measure longer.

# Sounds: EarSketch sound library
from earsketch import *

setTempo(120)
#Main synth: our starting point where volume is loud enough for element to be salient 
Synth1 = EIGHT_BIT_ATARI_PAD_002
Synth2 = EIGHT_BIT_ATARI_PAD_003

for measure in range (1, 17, 2):
    if measure % 4 == 1:
        fitMedia(Synth1, 1, measure,measure+2)
    else:
        fitMedia(Synth2, 2, measure, measure +2)
    

# Main synth section 2: same alternating pattern as the first, but quieter on tracks 9 and 10
for measure in range(17, 29, 4):
     fitMedia(Synth1, 9, measure, measure + 2)
     fitMedia(Synth2, 10, measure + 2, measure + 4)

#Percussion section below
#kick drums enter at measure 5 and run until 50
fitMedia(MILKNSIZZ_BOSSA_CLUBA_KICK, 3, 5, 50)
# Hi-hat enters at measure 9 and runs until 37
fitMedia(MILKNSIZZ_NORTENA_HI_HAT, 4, 9, 37)

#claps
def addClaps(start, end, step, length):
    """Place a clap clip every `step` measures between start and end."""
    for measure in range(start, end, step):
        fitMedia(AK_UNDOG_CLAPS_SNAPS_4, 11, measure, measure + length)

# Each tuple holds the settings for one clap section: (start, end, step, length).
# The loop unpacks each tuple into those four variables and passes them to addClaps,
# so one function is reused five times.
clapSections = [(9, 21, 2, 1), (21, 25, 2, 2), (26, 37, 2, 1), (38, 44, 2, 2), (45, 48, 2, 1)]
for start, end, step, length in clapSections:
    addClaps(start, end, step, length)


#All of the vocals will be below here

#backing vocals
fitMedia(AK_UNDOG_OOHS_2, 5, 13, 29)
fitMedia(AK_UNDOG_OOHS_2, 5, 37, 41)

#Main vocals
fitMedia(AK_UNDOG_OOHS_1,6, 13, 21)
fitMedia(AK_UNDOG_OOHS_1,6, 25, 29)
fitMedia(AK_UNDOG_OOHS_1,6, 33, 37)

# Choir layer: sustained "oohs/ahhs" from measure 21 to the end to thicken the ending
fitMedia(AK_UNDOG_OOHS_AHHS_4,8, 21, 49)


# Bass and keys

# building it out with bass
fitMedia(AK_UNDOG_BASS_3,7, 17, 29)

# Electric piano enters at measure 29 for the final build
fitMedia(IRCA_BOMBA_SICA_ELEC_PIANO,12, 29, 49)


# Effects
# Mixing: GAIN is in dB. Positive values boost a track, negative values lower it. 
# Second synth section (tracks 9/10) is turned down by 17 dB so it sits behind the vocals
setEffect(9,VOLUME,GAIN,-17.0)
setEffect(10,VOLUME,GAIN,-17.0)
setEffect(6,VOLUME,GAIN,3)
setEffect(8,VOLUME,GAIN,2)
setEffect(4,VOLUME,GAIN,3)
setEffect(5,VOLUME,GAIN,3)
setEffect(11,VOLUME,GAIN,-8)
setEffect(7,VOLUME,GAIN,5)








