--[[

Loki - a serpent offense system for Achaea (Mudlet)

-------------------------------------------------------------------------------------------------------------------------
It's my hope this slimmed down, basic serpent offense system can encourage more involvement 
from non-combatants as a functional framework to expand upon and create thier own systems.

Shout out to Sylvi, Fen, Fendo, Janella, Siv, Agramon, Arcturus, Naytorlin, Balkin, Oblive, Gavai, Belaziel, Essie, 
and many many more for helping me along the way.

I'd also like to thank the third party code I made use of for this release, Mesmer by Isaiah 
and Austere's AK tracker (v8.6.5) (modified)

-------------------------------------------------------------------------------------------------------------------------
GETTING STARTED:

Install the latest release through the Package Manager: https://github.com/Hikagejuunin/Loki

Once installed, edit the script "Lokisettings" with your own variables in the "--SYSTEM VARS"
section.The system's functioning depends on you providing your updated variables (equipment, 
snaketype ...etc). You can change most of the "--SYSTEM DEFAULTS" if you want, but the 
defaults are generally fine.

* Make sure to enable serverside queueing 

** You will also want to add a custom prompt if ya got svof, otherwise see how Austere's AK
handles that for other curing systems:

from AK tracker's Osettings!:
----------------------------------------------------------------------------------------------------------------------

--*

--Svo Prompt--

--add ^y@ml_oprompt to your custom prompt

--*

Example custom prompts:
--Hika original
vconfig customprompt ^1@health^pinkhp^r@(diffhealth)^gray(^2@%health^g%^gray)^c|^2@mana^bmp^2^gray^b@diffmana^gray(^2@%mana^g%^gray)^c|^gray(@%endurance%^g^yellowen^gray)^c|^gray(@%willpower%^g^magentawp^gray)^c|^2^gold^DarkOrange@eqbal@affs^W-^c| ^r@target @promptstring @gametargethp ^y@ml_oprompt

--Hika new
vconfig customprompt ^SlateGrayH:^1@health^r@(diffhealth)^SlateGray(^azure@%health%^SlateGray) ^SlateGrayM:^2@mana^b@(diffmana)^SlateGray(^azure@%mana%^SlateGray) ^DarkSlateGray(^G@%endurance^SlateGrayE ^G@%willpower^SlateGrayW^DarkSlateGray) ^2^gold^DarkOrange@eqbal @affs^W -^SlateGray ^red@target ^SlateGray(^w@gametargethp^SlateGray) ^y@ml_oprompt

--Hika new with \n
vconfig customprompt \n^SlateGrayH:^1@health^r@(diffhealth)^SlateGray(^azure@%health%^SlateGray) ^SlateGrayM:^2@mana^b@(diffmana)^SlateGray(^azure@%mana%^SlateGray) ^DarkSlateGray(^G@%endurance^SlateGrayE ^G@%willpower^SlateGrayW^DarkSlateGray) ^2^gold^DarkOrange@eqbal @affs^W -^SlateGray ^red@target ^SlateGray(^w@gametargethp^SlateGray) ^y@ml_oprompt

and back to AK's WYS stuff

--WYS Prompt--

--type wshow display

--add @owysprompt into your prompt


I disabled the graphical AK stuff, if ya want it enable in Osettings! 
There you should also specify what dirk artefact you have, default is Thoth's


CORE COMMANDS:

ds<xx> - dstab alias             
  example: ds<ck> = dstab curare/kalmia
** 'ds' with no venoms specified will automatically select venoms from lockstack
** you can manipulate venom table loadouts with "vt <selection>"
  example: "vt w" = add weariness to lockstack 
    * currently only includes: "w" (weariness), "c" (clumsiness), "d" (darkshade), "wd" (weariness/darkshade), "cd" (clumsiness/darkshade),
                               "k" (kelp stack), "dg" (darkshade/ginseng), "pl" (partylock), "scy" (team combat), "scy2" (scytherus fork), "sleep" (for sleeplock)
    
    - this is something you could easily expand upon

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
   example: "cs drg" = [imp rec hyp] hypno; [wea/dark] vstack; [wea/rec] postlock
"cs" without an option will reset to defaults

--VSTACK SELECTION
"vt w"    - weariness 
"vt c"    - clumsiness
"vt d"    - darkshade
"vt wd"   - weariness/darkshade
"vt cd"   - weariness/darkshade
"vt k"    - kelp stack (ast/weariness/clums/sensitivity)
"vt dg"   - darkshade/ginseng stack
"vt pl"   - party lock (group combat)

--VSTACK MODIFIERS
"vt scy"  - scytherus (group combat) [mod]
"vt scy2" - scytherus2 (scytherus fork) [mod]
"vt sleep" - delphinium when they have hypersomnia [mod]
"vt b"    - clears all above venom selections, can be anything that is not one of the options, just like vt none clears postlock prefs

--POST LOCK STACK
"vt drg"  - dragon (weariness/recklessness)
"vt srp"  - serpent (weariness)
"vt kni"  - knight [monk, paladin, blademaster...etc] (weariness)
"vt alc"  - alchemist (stupidity)
"vt dru"  - druid (voyria, weariness)
"vt sha"  - shaman (selarnia)
"vt syl"  - sylvan (voyria)
"vt bar"  - bard (voyria)
"vt par"  - pariah (voyria)
"vt prt"  - priest (voyria)
"vt rwn"  - "runewarden" (voyria)
"vt pal"  - paladin (voyria, weariness)
"vt apo"  - apostate (voyria)
"vt occ"  - occultist (voyria)
"vt dsw"  - depthswalker (recklessness)
"vt aem"  - airelemental (voyria)
"vt none" - resets postlock to default 

other aliases:
mr - mesmer reset, will forceably reset opponents hypnosis status if things get buggy or you need to rehypno right away after a failed attempt
tr - target reset (will reset hypnosis if target not sealed)
aa - toggles autoassist
ps - pinshot
bk<venom> - backstab (ex: bkd = backstab delphinium)
cl - conjure lightwall
ms - push mesmer hypnosis
qh <option> - custom hypnosis, can also do [1-10] to set a custom seal time, then you can sugga <action1, action2, action3...etc> and progress hypnosis with the 'ms' alias (in situations such as theft)
sn <direction> - snipe +/- aim
sm - shoot meteor
pl - party leader (make target calls to party)
pc - listen to party aff calls
pa - announce affs to party
af - toggles autoflay
as - toggles autosnapper
nh - toggles hypnosis
sv - summon snake
svi - summon snake to inventory
sk - snake keepup 
st - snap target
qp<venom> - preps quiver with whatever venom you designate ex: curare = qpc
nr - no rebounding (set rebounding false on target)

--OTHER SETTINGS
"vt nt" - toggles if autosnap will wait to snap when tree is down 
]]--
