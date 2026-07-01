### **Please note!** 
I'm not fully 100% confident on all of these, so if you see something wrong don't be afraid to point it out, I won't bite :)

These are my notes from all of the parser notes I'm able to gleam from reading through [gml_object_obj_writer_draw_0](https://code.deltarune.wiki/ch5/gml_object_obj_writer_draw_0)
_(Notes/Corrections provided to me will be noted as well, markated by a <sup>[x]</sup> (a footnote containing who provided what info will be available at the bottom of the document) )_

---

## Single* Character Codes

### Newline
`&` or `\n`

Simply acts as a linebreak within a dialogue box


### Delay
`^`
 > PARAMETER: 0-9

Halts the typewriter effect for X loops, used to add a specific delay to text ouput<sup>[1]</sup>

### Wait/End
`/`
 > PARAMETER: `%`

Used to wait for player input. If `%` is appended, this will be the last message before exiting dialogue<sup>[2]</sup>


### Escape Character (?)
`grave` (how the hell do i put a ` in a codeblock)

This simply moves the character reader forward by one step, maybe acting like an escape character?


---
## Codes beginning in \\\

### Emotion Select
`\\E`
 > PARAMETER: Alphanumeric ( 0-9 = [0-9], A-Z = [10-25], a-z = [26-51] )

Display a portrait from the current face to the corrosponding frame index.<sup>[5]</sup>

### Face select
`\\F`
 > PARAMETER: Any valid single utf character

Sets global.fc to various values corrosponding to the character following F
ie: lowercase r sets global.fc to 15

### Smallface Select
`\\f`
 > PARAMETER: Any valid single utf character

This is used for smallfaces specifically<sup>[3]</sup>

### Unknown
`\\*`
 > PARAMETER: Unknown

This does some bullshit. I think it's related to controller glyphs or inserting a variable inline

### Set Typer
`\\T`
 > PARAMETER: Any valid single utf character

This sets the typer to various values based on which character comes after T,
for example, \\T0 sets the typer value to 5, resulting in the normal narrator speaker
Also includes built in checks for if you're in the darkworld/fighting or not to decide which
typer to choose

### Skipable Set
`\\s`
 > PARAMETER: 0 or 1

can be \\s0 or \\s1 to switch text from being skippable or not

### Color
`\\c`
 > PARAMETER:
```
R = c_red
B = c_blue
Y = c_yellow
G = c_line
W = c_white
X = c_black
P = c_purple
M = c_maroon
S = #FF80FF
V = #80FF80
Z = Rainbow?
a = #84F9FF
y = #FFF8A1
g = #AEFFBC
o = #FFAC87
s = #E2A8FC
p = rgb(255, 138, 144)
b = #86A7FF
0 = `mycolor` (this is not set in this script, it's likely set before creating this message depending on circumstance)
```
Sets the color of any text that comes after it, color is decided by the first letter of the color placed after \\c
```gml
global.msg[0] = stringsetloc('\\cR I'm Red Now!\\cW Now i'm White!\\cZ now I'm RAINBOW??', {string_id_value})
```
Also supports hex values in some? cases?


### Choice
`\\C`
 > PARAMETER: 1-4

Invokes a previously set up choice. The number dictates valid options

### Meta
`\\M`
 > PARAMETER: 0-9
 
Sets global.flag[20 other_text_command] to the corrosponding number. This is used to set the talk-sprite of an example NPC<sup>[4]</sup>

### Voiceclip Enable
`\\v`
 > PARAMETER: 0 or 1

sets voiceclip mode to 0 or 1

### Voiceclip Play (?)
`\\V`
 > PARAMETER: Unknown

I believe this invokes a flowery voice clip

### Sound
`\\S`
 > PARAMETER: 0-9

Plays a sound corrosponding to the number using global.writersnd[i]

### Inline sprite
`\\I`
 > PARAMETER: 0-9

Draws a sprite with a corrosponding number id between 0 and 9, likely used for flower icons

### Miniface select?
`\\m`
 > PARAMETER: Any valid single utf character

Does something related to minifaces, I think it toggles a miniface on a delay?

### Unkown
`\\O`
 > PARAMETER: Unknown

I'll be honest I'm not too sure. It something to the writer

## Credits / References

_(thank you to mc.intosh on the DELTAMODDERS discord for corrections!)_

_(thank you to egochka11 from the DELTAMODDERS discord for corrections!)_

### Specifics
** from mc.intosh: **
> "the delay character ^ requires a number after it
it determines how long the delay is" <sup>[1]</sup>

> "the wait/end character is the forward slash / not the backslash \" <sup>[2]</sup>

> "\f is for small faces" <sup>[3]</sup>

> "\M is for setting flag 20 which is used by for example npcs to determine what sprite they should have as youre speaking to them" <sup>[4]</sup>

** from egochka11 **
> "This math turns 0-9 into 0-9, A-Z into 10-25, a-z into 26-51. These numbers are then used as indices of the frames of the face sprites to display" <sup>[5]</sup>
