# carla-patches
Service pack for Carla plugin host

DESCRIPTION
-----------

[Carla plugin host](https://github.com/falkTX/Carla) is well known and quite useful software, especially if you not only musician, but also electronic or radio engineer. 

_However_, it contain a number of long lasting bugs, most of them are not likely to going to be solved (i am would be happy if it is wrong). So i try to solve some, as well as add some new scalable art.

I have carefully described each bit of what's changed or new: **please see CHANGELOG** and read below.

This patch suite is intended to be used with _current Carla git_ (17000e7 or 378d5db, which are v. 2.6.0-alpha1), _not with release set_. You must know how to patch and compile things.

I have tested it using 64-bit Archlinux; and only Lv2, Internal, Ladsp, and Sound kits, using JACK only, are tested (but that not means others will not work).

PATCH
-----

Please check CHANGELOG for commands and file list.

COMPILE
-------
With Qt5:	
    
    make clean && make
    
With Qt6:	

    make clean && make FRONTEND_TYPE=6

_Addendum: New key list_
----------------------

Hotkeys on mouse hover:
---
* _For floating point values_:
- * `0`...`9`: Set absolute value, like 0 to 90 percent of full scale.
- * `Home`, `End`: Same, 0 and 100%. _Note:_ `Home` currently interferes with _Canvas control hotkey_ (use `0` then).
* _For integer and boolean values_:
- * Keys are same.
- * - If full scale span < 10, sets exact value.
- * - If full scale span < 20, sets doubled value. Etc. So, on larger spans, it is mostly work as for floats, but with integer step.

`PgUp`, `PgDn`: Scroll value up and down. Change precision: coarse (`Shift`), normal, fine (`Ctrl`), extra fine (both `Ctrl` & `Shift`).

`Enter`: Edit value. If it is button, cycles it instead (button editing is possible using `E` or Context menu).

`E`: Edit value.

`D`, `R`: Default value (Reset).

`Space`: Cycles scalepoint values. If it is button, it will be cycled also, if no scalepoints for it. If it is special Wet or Vol knobs with special state **MUTE** or **THRU** (Bypass) enabled: cycle this state, restoring previous value on un-mute/un-bypass.

Left click:
---
Exactly same as `Space` on hover.

Middle click:
---
Set default value. If it is special Wet or Vol knobs with special state **MUTE** or **THRU** (Bypass) enabled: un-mute/un-bypass it, but unlike of click, previous value is lost and replaced by default value.

Double click:
---
Edits value, except special cases: with Wet or Vol knobs when Left click is used, and if it's button. _Note:_ Editing still possible for these using `Enter` (if not button), `E`, or Context menu.

Mouse scroll:
---
(As well as **DJ Jog device** wheel action, it's often just HID scroll wheel)<br>
* For floating point values: 
Continuous change. Precision control: same as with `PgUp`, `PgDn`.
* For integer and boolean values: 
Cycles all possible values, with step best suited for span. Precision control: Only `Shift` and `Ctrl` will work.

Scalepoints: <small>_(But, see [#1976](https://github.com/falkTX/Carla/issues/1976))_</small>
---
If exist for this control, they are used when values using keyboard and mouse _cycling_, but not when _direct set_ (drag and 0 to 100 percent set) which still allows to use intermediate values, if any.

Drag: 
---
As before/classic (Continuous change); added `Ctrl` to increase precision. But:
* If it is _scalepointed_ control, drag will either:
- * not work (due to click used already), or
- * work as usual with intermediate value set possibility. (Selected by tweak).
* If it is special Wet or Vol knobs and there is special state **MUTE** or **THRU** (Bypass) enabled and active: drag will un-mute/un-bypass it, but unlike of click, previous value is lost and replaced by drag result.





