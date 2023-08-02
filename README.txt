# Loki
Loki - a serpent combat system for Achaea

** note: includes AK aff tracker by Austere and a Mesmer by Isaiah


To install:

1) Have Mudlet installed. You can get Mudlet here (https://www.mudlet.org/).

2) Install the Loki 1.0 package through Mudlets package manger 

3) Edit the script "Lokisettings" with your own variables in the "--SYSTEM VARS" section. 
   The system's functioning depends on you providing your updated variables (equipment, snaketype ...etc)
   You can change most of the "--SYSTEM DEFAULTS" if you want, but the defaults are fine.
4) Edit the script "Osettings"
      ** You will also want to add a custom prompt if ya got svof, otherwise see how Austere's AK handles that for other curing systems:
      *** Also I disabled the graphical AK stuff, if ya want it enable in Osettings! There you should also specify what dirk artefact you have, default is Thoth's

from AK tracker's Osettings!:
----------------------------------------------------------------------------------------------------------------------

--*

--Svo Prompt--

--add ^y@ml_oprompt to your custom prompt

--*


--WYS Prompt--

--type wshow display

--add @owysprompt into your prompt

-----------------------------------------------------------------------------------------------------------------------

EXAMPLE CUSTOM PROMPTS (SVO):

--Hika original
vconfig customprompt ^1@health^pinkhp^r@(diffhealth)^gray(^2@%health^g%^gray)^c|^2@mana^bmp^2^gray^b@diffmana^gray(^2@%mana^g%^gray)^c|^gray(@%endurance%^g^yellowen^gray)^c|^gray(@%willpower%^g^magentawp^gray)^c|^2^gold^DarkOrange@eqbal@affs^W-^c| ^r@target @promptstring @gametargethp ^y@ml_oprompt

--Hika new
vconfig customprompt ^SlateGrayH:^1@health^r@(diffhealth)^SlateGray(^azure@%health%^SlateGray) ^SlateGrayM:^2@mana^b@(diffmana)^SlateGray(^azure@%mana%^SlateGray) ^DarkSlateGray(^G@%endurance^SlateGrayE ^G@%willpower^SlateGrayW^DarkSlateGray) ^2^gold^DarkOrange@eqbal @affs^W -^SlateGray ^red@target ^SlateGray(^w@gametargethp^SlateGray) ^y@ml_oprompt

--Hika new with \n
vconfig customprompt \n^SlateGrayH:^1@health^r@(diffhealth)^SlateGray(^azure@%health%^SlateGray) ^SlateGrayM:^2@mana^b@(diffmana)^SlateGray(^azure@%mana%^SlateGray) ^DarkSlateGray(^G@%endurance^SlateGrayE ^G@%willpower^SlateGrayW^DarkSlateGray) ^2^gold^DarkOrange@eqbal @affs^W -^SlateGray ^red@target ^SlateGray(^w@gametargethp^SlateGray) ^y@ml_oprompt

GETTING STARTED:

CORE COMMANDS:

ds<xx> - dstab alias             
  example: ds<ck> = dstab curare/kalmia
** 'ds' with no venoms specified will automatically select venoms from lockstack
** you can manipulate venom table loadouts with "vt <selection>"
  example: "vt w" = add weariness to lockstack 
    * currently only includes "w" (weariness), "c" (clumsiness), "d" (darkshade), "k" (kelp stack) for pre-snap loadouts - this is something you could easily expand upon

manual dstab venom selections:

a = "aconite" 
c = "curare"  
d = "delphinium" 
e = "eurypteria" 
f = "epteth" 
g = "gecko" 
i = "digitalis" 
k = "kalmia" 
l = "larkspur" 
m = "monkshood" 
n = "selarnia" 
o = "voyria" 
p = "prefarar" 
q = "epseth" 
r = "darkshade"
s = "slike"
u = "euphorbia"
v = "vernalius"
x = "xentio"
z = "vardrax"

bs<x> - bite alias
** bs with no venoms specified will automatically select venoms from bitestack
  
manual bite venoms:

a = "aconite",
b = "oculus",
c = "camus",
d = "delphinium",
e = "eurypteria",
f = "epteth",
g = "gecko",
i = "digitalis",
k = "kalmia",
l = "loki",
m = "nechamandra",      -- useful after lock to freeze/disrupt
n = "notechis",         -- magi class blocker
o = "voyria",
p = "prefarar",
q = "epseth",
r = "darkshade",
s = "scytherus",
u = "euphorbia",
v = "vernalius",
x = "xentio",
y = "oculus",           -- use against trueblind opponents/those you aren't able to hypnotize
z = "vardrax",

--CUSTOM PVP SETTINGS
"cs <class> = will set several offensive variables for a specific class
   example: "cs kni" = [imp] hypno; [wea] vstack; [wea] postlock
   example: "cs drg" = [imp add hyp rec con] hypno; [wea/dark] vstack; [wea] postlock
"cs" without an option will reset to defaults

--VSTACK SELECTION
"vt w" - weariness 
"vt d" - darkshade
"vt c" - clumsiness
"vt k" - ast/weariness/clums/sensitivity
"vt b" - clears all above venom selections, can be anything that is not one of the options, just like vt none clears postlock prefs

--POST LOCK STACK
"vt drg" = dragon (weariness/recklessness)
"vt srp" = serpent (weariness)
"vt kni" = knight [monk, paladin, blademaster...etc] (weariness)
"vt alc" = alchemist (stupidity)
"vt dru" = druid (voyria, weariness)
"vt sha" = shaman (selarnia)
"vt syl" = sylvan (voyria)
"vt bar" = bard (voyria)
"vt par" = pariah (voyria)
"vt prt" = priest (voyria)
"vt rwn" = "runewarden" (voyria)
"vt pal" = paladin (voyria)
"vt apo" = apostate (voyria)
"vt occ" = occultist (voyria)
"vt dsw" = depthswalker (recklessness)
"vt aem" = airelemental (voyria)
"vt none" = resets postlock to default 

other aliases:
pvp = sets auto_assist true and shows you some info
aa = auto_assist toggle
ps = pinshot
cl = conjure lightwall
ms = push mesmer hypnosis
tr = target reset
mr = mesmer reset
qh <option> = custom hypnosis, can also do [1-10] to set a custom seal time, then you can sugga <action1, action2, action3...etc> and progress hypnosis with the 'ms' alias (in situations such as theft)
sn <direction> = snipe +- aim; can also just be 'sn' with no direction
sm = shoot meteor
pl = party leader (make target calls to party)
pc = listen to party aff calls
pa = announce affs to party
af = toggles autoflay
as = toggles autosnapper
nh = toggles hypnosis
st = snap target
bh = behead

--OTHER SETTINGS
"vt nt" = toggles if autosnap will wait to snap when tree is down
