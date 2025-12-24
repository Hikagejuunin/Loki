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
💡 Note: in-game you can bring up the Loki Help printout using 'lhelp' (as seen below):

                                      -------------
                                      | Loki Help |
                                      -------------
[+]--------------------------------------------------------------------------------------[+]
|     -=+Double Stab Commands+=-           |=======+ Auto & Manual Targetting Info +=======|
[+]--------------------------------------------------------------------------------------[+]
|     ds<xx> - dstab alias                                                                 |
|       example: dsck = dstab curare/kalmia                                                |
|  * 'ds' with no venoms specified will automatically select venoms from lockstack         |
|     * you can manipulate venom table loadouts with: vt <option>                          |
|          example: vt w = add weariness to lockstack                                      |
|          options: ven: w,c,d,wd,wc,cw,cd,an,na,k,dg,pl  mod: scy,scy2,sleep              |
[+]--------------------------------------------------------------------------------------[+]
|     -=+Manual Venom Selection+=-         |========+ Manual DSTAB Venom Selection +=======|
[+]--------------------------------------------------------------------------------------[+]
| a - aconite ------>(Stupidity)(E:Plumbum)     n - selarnia-->(Unbond)(A:Mending)         |
| c - curare ------->(Paralysis)(E:Magnesium)   o - voyria---->(R.I.P.)(SP:Immunity)       |
| d - delphinium --->(Sleep)(E:Kola)(Metawake)  p - prefarar-->(Sensitivity)(E:Aurum)      |
| e - eurypteria --->(Recklessness)(E:Argentum) q - epseth---->(Shriveled Legs)(A:Mending) |
| f - epteth ------->(Shrivel Arms)(A:Mending)  r - darkshade->(Sunlight Allergy)(E:Ferrum)|
| g - gecko -------->(Slickness)(S:Realgar)     s - slike----->(Anorexia)(A:Epidermal)     |
| i - digitalis ---->(Shyness)(E:Plumbum)       u - euphorbia->(Nausea)(E:Ferrum)          |
| k - kalmia ------->(Asthma)(E:Aurum)          v - vernalius->(Weariness)(E:Aurum)        |
| l - larkspur ----->(Dizziness)(E:Plumbum)     x - xentio---->(Clumsiness)(E:Aurum)       |
| m - monkshood ---->(Disfigure)(S:Realgar)     z - vardrax--->(Addiction)(E:Ferrum)       |
[+]--------------------------------------------------------------------------------------[+]
|     -=+Bite Commands+=-                  |=======+ Auto & Manual Targetting Info +=======|
[+]--------------------------------------------------------------------------------------[+]
|     bs<x> - bite alias                                                                   |
|       example: bso = bite voyria                                                         |
|  * 'bs' with no venoms specified will automatically select venoms from bitestack         |
[+]--------------------------------------------------------------------------------------[+]
|     -=+Manual Venom Selection+=-         |========+ Manual BITE Venom Selection +========|
[+]--------------------------------------------------------------------------------------[+]
| a - aconite ------>(Stupidity)(E:Plumbum)     n - notechis-->(Haemophilia)(E:Ferrum)     |
| c - camus -------->(Damage)(SP:Health)        o - voyria---->(R.I.P.)(SP:Immunity)       |
| d - delphinium --->(Sleep)(E:Kola)(Metawake)  p - prefarar-->(Sensitivity)(E:Aurum)      |
| e - eurypteria --->(Recklessness)(E:Argentum) q - epseth --->(Shriveled Legs)(A:Mending) |
| f - epteth ------->(Shrivel Arms)(A:Mending)  r - darkshade->(Sunlight Allergy)(E:Ferrum)|
| g - gecko -------->(Slickness)(S:Realgar)     s - scytherus->(Relapsing Affs)(E:Ferrum)  |
| i - digitalis ---->(Shyness)(E:Plumbum)       u - euphorbia->(Nausea)(E:Ferrum)          |
| k - kalmia ------->(Asthma)(E:Aurum)          v - vernalius->(Weariness)(E:Aurum)        |
| l - loki ----->(Fratricide)(E:Ferrum)         x - xentio---->(Clumsiness)(E:Aurum)       |
| m - nechamandra ---->(Shivering)(A:Caloric)   y - oculus---->(Sight)(E:Arsenic)          |
|                                               z - vardrax--->(Addiction)(E:Ferrum)       |
[+]--------------------------------------------------------------------------------------[+]
|        -=+Settings Aliases+=-               |=======+ Aliases for Loki Settings +========|
[+]--------------------------------------------------------------------------------------[+]
|     pvp - pvp mode - enables auto-assist, displays current combat settings               |
|     lok - loki display - displays current combat settings without enabling auto-assist   |
|     aa - auto-assist - toggles auto-assist, when on will queue stabs on target cures     |
|     tar - set target - sets your target, if you use your own make sure it updates AK/Loki|
|     cs <class> - class settings - default combat settings for a given class (ex: cs srp) |
|     vt <option> - venom table - venom selection and other lockstack settings             |
|     vt <class> - set class - will set target class for postlock, cs alias also does this |
|     vt nt - no tree - toggles if autosnap will consider tree downtime for snaps          |
|     qh <option> - queue hypnosis - pre-set hypno sets (ex: qh hyp - hyp hpr con)         |
|                   options: hyp,nau,add,con,dis,hpr,hpr2,overkill,sleep                   |
|                     you can also do [1-10] to set a custom seal time, then you can       |
|                     sugga <action1, action2, action3...etc> and progress hypnosis        |
|                     with the 'ms' alias (in situations such as theft)                    |
|     imp <aff> - impulse setting - sets default impulse (ex: imp rec - adds recklessness) |
|                   options: dea,rec,epi,hal,mas,con,ver,dem,stt,ago,cla,lon,stu,par,amn   |
|     tr - target reset - resets target afflictions and mesmer status if not sealed        |
|     mr - mesmer reset - resets mesmer status, useful if mesmer breaks                    |
|     nr - no rebounding - sets targets rebounding status to false for backstab purposes   |
|     af - auto-flay - toggles automatic handling of rebounding and shield flays           |
|     as - auto-snap - toggles automatic handling of snaps                                 |
|     nh - no hypnosis -toggles mesmer hypnosis on or off                                  |
|     sk - snake keepup -toggles automatic snake summoning                                 |
|     pl - party leader - toggles making target calls to party                             |
|     pc - party calls - toggles listening to party affliction calls                       |
|     pa - party affs - toggles announcing afflictions to party                            |
|     qp <venom> - quiver prep - will envenom your arrows with a venom (ex: qpc - curare)  |
|     chaseon|chaseoff - chase - toggles automatic goto target on farsee                   |
[+]--------------------------------------------------------------------------------------[+]
|        -=+Other Aliases+=-               |=======+ Commonly Used Aliases for Loki +======|
[+]--------------------------------------------------------------------------------------[+]
|     ms - mesmer suggest - manually progresses hypnosis, except for snap                  |
|     sn <direction> - snipe + direction - direction optional, will aim if provided        |
|     sm - shoot meteor                                                                    |
|     ps - pinshot - pinshots target if not already pinshot or shielding                   |
|     bk<venom> - backstab target - with specific venom (ex: bkd - backstabs delphinium)   |
|     cl - conjure lightwall                                                               |
|     sv - summon viper - summon your snake                                                |
|     svi - summon viper inventory - summon your snake to your inventory                   |
|     st - snap target                                                                     |
|     bh - behead - only disables auto-assist, will want to disable curing                 |
|     exe - execute - only disables auto-assist, will want to disable curing               |
|     noose - noose - will need noose in inventory, only disables auto-assist              |
|     lhelp - loki help - displays summary of system commands                              |
[+]--------------------------------------------------------------------------------------[+]

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







