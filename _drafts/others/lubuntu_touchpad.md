http://superuser.com/questions/229839/reduce-laptop-touch-pad-sensitivity-in-ubuntu

This works for me in Ubuntu 10.10

To see what trackpad you've got and what it's called, try:

xinput list

My device is called "SynPS/2 Synaptics TouchPad"

There are 3 finger pressure settings: low, high & press. See what their current values are with something like:

xinput list-props "SynPS/2 Synaptics TouchPad" |grep -i finger

Change the values with something like:

xinput set-prop "SynPS/2 Synaptics TouchPad" "Synaptics Finger" 50 90 255

By increasing the second parameter, you require more finger pressure for the trackpad to respond. The first parameter controls release pressure, the third is to detect a button press (I think).

