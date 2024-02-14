Ch 1
====
h,j,k,l

:q, :q!
:w, :wq

d to delete

i to enter Insert mode

Esc to return to Normal mode.


Ch 2
====
i, a

I - Insert at the start of the line.

A - Insert at the end of the line.

o and O to open lines below and above the cursor respectively.


Ch 3
====
w - Move forward to before the the beginning of the next word.

e - Move forward to the end of the current word.

b - Move backward to the beginning of the current word.

W,E,B - traverses WORDS separated-only-by whitespaces.

c to change the current selection. (== di or delete+insert)

v to enter Select mode. Type v again or Esc to return to Normal mode. Notice d returns you to Normal mode.

x to select whole line. Type x again to select the next.

; to collapse selection to single cursor. Deselect without having to move the cursor(s). 
Alt-; flips position.


Ch 4
====
u to undo. U to redo.

y to yank (copy) the selection. 

p to paste the yanked selection after the cursor.

P to paste before the cursor.

Alt-d / Alt-c to delete or change without copying the altered text in register.

Space + y / p to yank / paste on the system's clipboard.

/ to search forward in file.
Shift-/ (or ?) to search backwards.

n to go to the next search match.
N to go to the previous search match.


Ch 5
====
C (Shift-c) to duplicate cursor to the next suitable line.

Alt-Shift-c does the same above the cursor.

, to remove multi cursor.

s to select matches in the selection. (x selects the whole line, then s opens prompt. Type to find matches and Enter. c to change matches. , to remove second cursor.)
