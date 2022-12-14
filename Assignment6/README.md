# PSYCH 403 - Assignment 6 exercises: MPacificar

## Dialog box exercises
**Use the PsychoPy help page on guis to customize your "exp_info" dialog box: psychopy.gui**
1. Edit the dictionary "exp_info" so you have a variable called "session", with "1" preset as the session number.
2. Edit the "gender" variable in "exp_info" so the subject can write in whatever they want into an empty box, instead of the drop-down list
```
# dictionary setup for the dialog box gui:
exp_info = {'subject_nr':0, 'age':0, 'handedness':('right','left','ambi'), 'gender':'', 'session': 1}
print(exp_info)
```
**Using DlgFromDict:**
1. Customize my_dlg so that you have a title for your dialog box: "subject info".
```
my_dlg = gui.DlgFromDict(dictionary = exp_info, title = 'subject info')
```
2. Set the variable "session" as fixed. What happens?
```
my_dlg = gui.DlgFromDict(dictionary = exp_info, title = 'subject info', fixed = ['session'])
```
- **Answer: The session variable cannot be edited (non-editable) by the participant if it's set to fixed**

3. Set the order of the variables as session, subject_nr, age, gender, handedness.
```
my_dlg = gui.DlgFromDict(dictionary = exp_info, title = 'subject info', fixed = ['session'], order = ['session','subject_nr','age','gender','handedness'])
```
4. Once you have done all of the above, don't show "my_dlg" right away. Tell your experiment to print "All variables have been created! Now ready to show the dialog box!". Then, show the dialog box.
```
my_dlg = gui.DlgFromDict(dictionary = exp_info, title = 'subject info', fixed = ['session'], order = ['session','subject_nr','age','gender','handedness'], show = False)
print("All variables have been created! Now ready to show the dialog box!")
my_dlg.show()
```
Fill in the following pseudocode with the real code you have learned so far:
```
from psychopy import gui, core
from datetime import datetime
import os

#=====================
#COLLECT PARTICIPANT INFO
#=====================

#-create a dialogue box that will collect current participant number, age, gender, handedness
# dictionary setup for the dialog box gui:
# dictionary setup for the dialog box gui:
exp_info = {'subject_nr':0, 'age':0, 'handedness':('right','left','ambi'), 'gender':'', 'session': 1}
print(exp_info)

# participant info dialog box customization:
my_dlg = gui.DlgFromDict(dictionary = exp_info, title = 'subject info', fixed = ['session'], order = ['session','subject_nr','age','gender','handedness'], show = False)
print("All variables have been created! Now ready to show the dialog box!")
my_dlg.show() # show dialog box after printing variables have been created

# get date and time
date = datetime.now()
print(date)
exp_info['date'] = str(date.hour) + '-' + str(date.day) + '-' + str(date.month) + '-' + str(date.year)
print(exp_info['date'])

#-create a unique filename for the data
filename =  str(exp_info['subject_nr']) + '_' + exp_info['date'] + '.csv'
print(filename)

main_dir = os.getcwd() 
sub_dir = os.path.join(main_dir,'sub_info',filename)
```

## Monitor and window exercises

Look at the psychopy help page on "window" to help solve the exercises:
1. How does changing "units" affect how you define your window size?
- **Answer: Changing units does not affect how you define the window size, because it applies to the units of the stimuli being drawin in the window**
3. How does changing colorSpace affect how you define the color of your window? Can you define colors by name?
- **Answer: PsychoPy uses three color spaces which are RGB, DKL, and LMS. Changing colorSpace changes how you define the colour of the window. RGB and DKL follows this format: [#,#,#], where # can range -1:1; HSV format is [#,#,#], where # can range 0:1. Colors can also be defined using hex values or by name as listed on the web/X11 color names (e.g., "pink").**

Fill in the following pseudocode with the real code you have learned so far:
```
from psychopy import visual, monitors

#=====================
#CREATION OF WINDOW AND STIMULI
#=====================

#-define the monitor settings using psychopy functions
mon = monitors.Monitor('myMonitor', width=38.3, distance=60) 
mon.setSizePix([1920,1080])
mon.save()

#-define the window (size, color, units, fullscreen mode) using psychopy functions
win = visual.Window(monitor=mon, size = [1920, 1080], color=["black"], units='pix', fullscr=True)
```

## Stimulus exercises
Check the psychopy help page on "ImageStim" to help you solve these exercises:
1. Write a short script that shows different face images from the image directory at 400x400 pixels in size. What does this do to the images? How can you keep the proper image dimensions and still change the size?
- **Answer: specifying the size changes how big the stimulus (image) is showm on the screen. To keep proper image dimensions and still change size, specify the unit according to the image's dimension format (i.e., use units = 'pix' for images with dimensions specified in pixels).**
```
from psychopy import gui, core, visual, monitors, event
from datetime import datetime
import numpy as np
import os

#=====================
#CREATION OF WINDOW AND STIMULI
#=====================

#-define the monitor settings using psychopy functions
mon = monitors.Monitor('myMonitor', width=38.3, distance=60) 
mon.setSizePix([1920,1080])
mon.save()

#-define the window (size, color, units, fullscreen mode) using psychopy functions
win = visual.Window(monitor=mon, size = [1920, 1080], color=["black"], units='pix', fullscr=True)

# stim exercise 1
os.chdir('C:\Psycopy Images') #stuff you only have to define once at the top of your script
main_dir = os.getcwd() #stuff you only have to define once at the top of your script
image_dir = os.path.join(main_dir,'images') #stuff you only have to define once at the top of your script

# number of trials
nTrials = 10 

# face images stimuli
faceStims = ['face01.jpg', 'face02.jpg', 'face03.jpg', 'face04.jpg', 'face05.jpg', 'face06.jpg', 'face07.jpg', 'face08.jpg', 'face09.jpg', 'face10.jpg']

# stimuli properties
my_image = visual.ImageStim(win, units = 'pix', size = (400,400))

# randomize to show different face images
np.random.shuffle(faceStims)

for trial in range(nTrials):
    my_image.image = os.path.join(image_dir,faceStims[trial])
    my_image.draw()
    win.flip()
    event.waitKeys()
win.close()
```
2. Write a short script that makes one image appear at a time, each in a different quadrant of your screen (put the window in fullscreen mode). Think about how you can calculate window locations without using a trial-and-error method.
```
from psychopy import gui, core, visual, monitors, event
from datetime import datetime
import numpy as np
import os

# stim exercise 2

mon = monitors.Monitor('myMonitor', width=38.3, distance=60) 
mon.setSizePix([1920,1080])
mon.save()
# get screen size
screenSize = mon.getSizePix()
screenWidth = screenSize[0] # get screen width in pixel
screenHeight = screenSize[1] # get screen height in pixel

#-define the window (size, color, units, fullscreen mode) using psychopy functions
win = visual.Window(monitor=mon, size = [1920, 1080], color=["black"], units='pix', fullscr=True)

os.chdir('C:\Psycopy Images') #stuff you only have to define once at the top of your script
main_dir = os.getcwd() #stuff you only have to define once at the top of your script
image_dir = os.path.join(main_dir,'images') #stuff you only have to define once at the top of your script

# number of trials
nTrials = 10 

# face images stimuli
faceStims = ['face01.jpg', 'face02.jpg', 'face03.jpg', 'face04.jpg', 'face05.jpg', 'face06.jpg', 'face07.jpg', 'face08.jpg', 'face09.jpg', 'face10.jpg']

# stimuli properties
my_image = visual.ImageStim(win, units = 'pix', size = (400,400))
horizMult = [-1, 1, 1, -1, -1, 1, 1, -1, -1, 1] # list of all possible horizontal positions for 10 trials
vertMult = [1, 1, -1, -1, 1, 1, -1, -1, 1, 1] # list of all possible vertical positions for 10 trials
xCoord = []
yCoord = []
# get all possible horizontal positions in each quadrant per screen width
for i in horizMult:
    xCoord.append(i*(screenSize[0]/4)) 
print(xCoord)
# get all possible vertical positions in each quadrant per screen height
for i in vertMult:
    yCoord.append(i*(screenSize[1]/4))
print(yCoord)
# make a list of all X,Y coordinates for image presentation
imageCoords = list(zip(xCoord, yCoord))
print(imageCoords)

# randomize to show different face images
np.random.shuffle(faceStims)

# show face images stimuli
for trial in range(nTrials):
    my_image.image = os.path.join(image_dir,faceStims[trial])
    my_image.pos = imageCoords[trial] # go through imageCoords list for image position
    my_image.draw()
    win.flip()
    event.waitKeys()
win.close()
```
3. Create a fixation cross stimulus (hint:text stimulus).
```
from psychopy import gui, core, visual, monitors, event
from datetime import datetime
import numpy as np
import os

# stim exercise 3

mon = monitors.Monitor('myMonitor', width=38.3, distance=60) 
mon.setSizePix([1920,1080])
mon.save()
# get screen size
screenSize = mon.getSizePix()
screenWidth = screenSize[0] # get screen width in pixel
screenHeight = screenSize[1] # get screen height in pixel

#-define the window (size, color, units, fullscreen mode) using psychopy functions
win = visual.Window(monitor=mon, size = [1920, 1080], color=["black"], units='pix', fullscr=True)

os.chdir('C:\Psycopy Images') #stuff you only have to define once at the top of your script
main_dir = os.getcwd() #stuff you only have to define once at the top of your script
image_dir = os.path.join(main_dir,'images') #stuff you only have to define once at the top of your script

# number of trials
nTrials = 10 

# face images stimuli
faceStims = ['face01.jpg', 'face02.jpg', 'face03.jpg', 'face04.jpg', 'face05.jpg', 'face06.jpg', 'face07.jpg', 'face08.jpg', 'face09.jpg', 'face10.jpg']

# stimuli properties
fix_text = visual.TextStim(win, text = '+')
my_image = visual.ImageStim(win, units = 'pix', size = (400,400))
horizMult = [-1, 1, 1, -1, -1, 1, 1, -1, -1, 1] # list of all possible horizontal positions for 10 trials
vertMult = [1, 1, -1, -1, 1, 1, -1, -1, 1, 1] # list of all possible vertical positions for 10 trials
xCoord = []
yCoord = []
# get all possible horizontal positions in each quadrant per screen width
for i in horizMult:
    xCoord.append(i*(screenSize[0]/4)) 
print(xCoord)
# get all possible vertical positions in each quadrant per screen height
for i in vertMult:
    yCoord.append(i*(screenSize[1]/4))
print(yCoord)
# make a list of all X,Y coordinates for image presentation
imageCoords = list(zip(xCoord, yCoord))
print(imageCoords)

# randomize to show different face images
np.random.shuffle(faceStims)

for trial in range(nTrials):
    my_image.image = os.path.join(image_dir,faceStims[trial])
    my_image.pos = imageCoords[trial] # go through imageCoords list for image position
    my_image.draw()
    fix_text.draw()
    win.flip()
    event.waitKeys()
win.close()
```
Fill in the following pseudocode with the real code you have learned so far:

- **Note: some codes taken from other parts of the full experiment structure to be able to run the script**
```
from psychopy import gui, core, visual, monitors, event
from datetime import datetime
import numpy as np
import os

# path settings:
os.chdir('C:\Psycopy Images') #stuff you only have to define once at the top of your script
main_dir = os.getcwd() #stuff you only have to define once at the top of your script
image_dir = os.path.join(main_dir,'images') #stuff you only have to define once at the top of your script

# stimulus and trial settings:
nTrials = 10
nBlocks = 2

#=====================
#CREATION OF WINDOW AND STIMULI
#=====================
#-define the monitor settings using psychopy functions
mon = monitors.Monitor('myMonitor', width=38.3, distance=60) 
mon.setSizePix([1920,1080])
mon.save()
#-define the window (size, color, units, fullscreen mode) using psychopy functions
win = visual.Window(monitor=mon, size = [1920, 1080], color=["black"], units='pix', fullscr=True)
# get screen size
screenSize = mon.getSizePix()
screenWidth = screenSize[0] # get screen width in pixel
screenHeight = screenSize[1] # get screen height in pixel

#-define experiment start text using psychopy functions
start_msg = "Welcome to the experiment! Press any key to begin."
start_text = visual.TextStim(win, text = start_msg)
#-define block (start)/end text using psychopy functions
block_msg = "Press any key to continue to the next block."
end_trial_msg = "End of trial"
block_text = visual.TextStim(win, text = block_msg)
end_trial_text = visual.TextStim(win, text = end_trial_msg)

#-define stimuli using psychopy functions (images, fixation cross)
faceStims = ['face01.jpg', 'face02.jpg', 'face03.jpg', 'face04.jpg', 'face05.jpg', 
             'face06.jpg', 'face07.jpg', 'face08.jpg', 'face09.jpg', 'face10.jpg']
fix_text = visual.TextStim(win, text = '+')
my_image = visual.ImageStim(win, units = 'pix', size = (400,400))
horizMult = [-1, 1, 1, -1, -1, 1, 1, -1, -1, 1] # list of all possible horizontal positions for 10 trials
vertMult = [1, 1, -1, -1, 1, 1, -1, -1, 1, 1] # list of all possible vertical positions for 10 trials
xCoord = []
yCoord = []
# get all possible horizontal positions in each quadrant per screen width
for i in horizMult:
    xCoord.append(i*(screenSize[0]/4)) 
# get all possible vertical positions in each quadrant per screen height
for i in vertMult:
    yCoord.append(i*(screenSize[1]/4))
# make a list of all X,Y coordinates for image presentation
imageCoords = list(zip(xCoord, yCoord))

#=====================
#START EXPERIMENT
#=====================
#-present start message text
start_text.draw()
win.flip()
#-allow participant to begin experiment with button press
event.waitKeys()

#=====================
#BLOCK SEQUENCE
#=====================
#-for loop for nBlocks
for block in range(nBlocks):
    print('Welcome to block ' + str(block + 1))
    #-present block start message
    block_text.draw()
    win.flip()
    #-randomize order of trials here
    np.random.shuffle(faceStims)
    
    #=====================
    #TRIAL SEQUENCE
    #=====================    
    #-for loop for nTrials
    for trial in range(nTrials):
        print('Trial ' + str(trial + 1))
        #-set stimuli and stimulus properties for the current trial
        
        #=====================
        #START TRIAL
        #=====================  
        #-draw fixation
        fix_text.draw()
        #-flip window
        win.flip()
        #-wait time (stimulus duration)
        
        #-draw image
        my_image.image = os.path.join(image_dir,faceStims[trial])
        my_image.pos = imageCoords[trial] # go through imageCoords list for image position
        my_image.draw()
        #-flip window
        win.flip()
        #-wait time (stimulus duration)
        event.waitKeys() # participant to press button for next image to show?
        
        #-draw end trial text
        end_trial_text.draw()
        #-flip window
        win.flip()
        #-wait time (stimulus duration)
        
#======================
# END OF EXPERIMENT
#======================        
#-close window
win.close()
```
