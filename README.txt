--[[

-------------------------------------------------------------------------------------------------------------------------
 Loki 2.1.4 - Serpent Offense Framework for Achaea (Mudlet)
-------------------------------------------------------------------------------------------------------------------------

Loki is a lightweight, modular serpent offense system designed for the MUD Achaea. It's my hope this slimmed down, basic serpent offense system can encourage more involvement from non-combatants as a functional framework to expand upon and create their own systems.

-- Acknowledgements --

  🐍 Special thanks to:

     Sylvi, Fen, Fendo, Janella, Siv, Agramon, Arcturus, Naytorlin, Balkin, Oblive, Gavai, Sprucebruce, Belaziel, Essie, Anaria and many others for support and insight.

    Isaiah for the Mesmer system

    Austere for the AK Tracker (v8.6.4) – modified for Loki 2.1 integration

    Myrddin for lhelp UI

------------------- 
 GETTING STARTED:
-------------------

-- Installation --

💡 Note: requires Mudlet client (https://www.mudlet.org/download/)

Install via Mudlet's Package Manager:
    📦 GitHub Repository: https://github.com/Hikagejuunin/Loki

    Open the Lokisettings script and update the --SYSTEM VARS section with your personalized info:

        - Name, Equipment, Artefacts, Snaketype, Preferences ... etc

    💡 Note: The --SYSTEM DEFAULTS are fine for most users, but feel free to tweak as needed.

    ✅ Enable server-side queueing.

-- Prompt Configuration --

Using SVOF?

Add ^y@ml_oprompt to your vconfig customprompt. Sample formats:
Basic:

vconfig customprompt ^1@health@mana@eqbal@affs@target @promptstring @gametargethp ^y@ml_oprompt

Custom Examples:

--Hika original
vconfig customprompt ^1@health^pinkhp^r@(diffhealth)^gray(^2@%health^g%^gray)^c|^2@mana^bmp^2^gray^b@diffmana^gray(^2@%mana^g%^gray)^c|^gray(@%endurance%^g^yellowen^gray)^c|^gray(@%willpower%^g^magentawp^gray)^c|^2^gold^DarkOrange@eqbal@affs^W-^c| ^r@target @promptstring @gametargethp ^y@ml_oprompt

--Hika new
vconfig customprompt ^SlateGrayH:^1@health^r@(diffhealth)^SlateGray(^azure@%health%^SlateGray) ^SlateGrayM:^2@mana^b@(diffmana)^SlateGray(^azure@%mana%^SlateGray) ^DarkSlateGray(^G@%endurance^SlateGrayE ^G@%willpower^SlateGrayW^DarkSlateGray) ^2^gold^DarkOrange@eqbal @affs^W -^SlateGray ^red@target ^SlateGray(^w@gametargethp^SlateGray) ^y@ml_oprompt

--Hika new with \n
vconfig customprompt \n^SlateGrayH:^1@health^r@(diffhealth)^SlateGray(^azure@%health%^SlateGray) ^SlateGrayM:^2@mana^b@(diffmana)^SlateGray(^azure@%mana%^SlateGray) ^DarkSlateGray(^G@%endurance^SlateGrayE ^G@%willpower^SlateGrayW^DarkSlateGray) ^2^gold^DarkOrange@eqbal @affs^W -^SlateGray ^red@target ^SlateGray(^w@gametargethp^SlateGray) ^y@ml_oprompt

Using WYS?

Type wshow display

Add @owysprompt to your prompt string

--Hika current
wconfig prompt #red@paused@softpaused#DodgerBlue@retardation#yellow@phase#DarkGreen H:#hcolour@health#DarkGreen#SlateGray(@percenthealth%#SlateGray)#DarkGreen M:#mcolour@mana#DarkGreen#SlateGrey(@percentmana%#SlateGrey)#SlateGrey(E#DarkGreen@percentendurance#SlateGrey W#DarkGreen@percentwillpower#SlateGrey)@hiding@flying@slc@hikaaffs#SlateGray@hikamesmer@hikaauto - #red@target@npchp @owysprompt

💡 Note: Graphical AK features are disabled by default. You can re-enable them via Osettings.
💡 Note: in AK's Osettings script you should also specify what dirk artefact you have, default is Thoth's

-------------------
 CORE COMMANDS:
-------------------

ds<xx> - dstab alias             
  example: ds<ck> = dstab curare/kalmia
** 'ds' with no venoms specified will automatically select venoms from Lockstack script
** you can manipulate venom table loadouts with "vt <selection>"
  example: "vt w" = add weariness to lockstack 
    * currently only includes: "w" (weariness), "c" (clumsiness), "d" (darkshade), "wd" (weariness/darkshade), "cd" (clumsiness/darkshade),
                               "k" (kelp stack), "dg" (darkshade/ginseng), "pl" (partylock), "scy" (impulse fork), "scy2" (scytherus fork), "sleep" (for sleeplock)
    
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
   example: "cs rwn" = 
                       [VSTACK]: weariness added to stack...
                       [VSTACK]: post-lock set to runewarden (weariness, voyria)...
                       [MESMER]: hyp hpr con added to queue...

   example: "cs drg" = 
                       [VSTACK]: weariness added to stack...
                       [VSTACK]: post-lock set to dragon (weariness, recklessness)...
                       [MESMER]: hyp hpr rec added to queue...
             

💡 Note: "cs" without an option will reset to defaults

--VSTACK SELECTION
"vt w"    - weariness 
"vt c"    - clumsiness
"vt d"    - darkshade
"vt wd"   - weariness/darkshade
"vt wc"   - weariness/clumsiness
"vt cd"   - clumsiness/darkshade
"vt cw"   - clumsiness/weariness
"vt an"   - addiction/nausea
"vt na"   - nausea/addiction
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
imp <impulse aff> - custom impulse, ex: dea, epi, hal, con, mas ... etc
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
noose - hang your oppenent from the trees
exe - execute your oppoenent with your whip
bh - head your opponent with your sword
pvp - pvp mode, sets auto_assist on and shows combat settings
lok - display combat settings, does not turn on auto_assist

--OTHER SETTINGS
"vt nt" - toggles if autosnap will wait to snap when tree is down 

"lhelp" - will print a summary of system commands

Don’t be afraid to reach out if you have any questions!

🐍 Happy stabbing

]]--






