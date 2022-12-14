# PSYCH 403 - Assignment 3 exercises: MPacificar

## Variable operations exercises:
Create three variables: "sub_code", "subnr_int", and "subnr_str". The sub_code should be "sub". Assign the integer 2 to subnr_int, and assign the string "2" to subnr_str. 
```
sub_code = "sub"
subnr_int = 2
subnr_str = "2"

print(sub_code + subnr_int)
print(sub_code + subnr_str)
```
Question: Which form of subnr (int or str) can be added to sub_code to create the output "sub2"? Why don't both work?
- **Answer:**
Only subnr_str can be concatenated with sub_code. This is because they belong to the same type or class, namingly the string class, and Python only allow objects from the same classes to be compounded together.

Use operations to create the following outputs with your variables:
"sub 2"
"sub 222"
"sub2sub2sub2"
"subsubsub222"
```
sub_code = "sub"
subnr_int = 2
subnr_str = "2"

# "sub 2"
print(sub_code + " " + subnr_str)

# "sub 222"
print(sub_code + " " + (subnr_str)*3)

# "sub2sub2sub2"
print((sub_code + subnr_str)*3)

# "subsubsub222"
print((sub_code)*3 + (subnr_str)*3)

```

## List operations exercises:
Create a list of numbers [1,2,3] called "numlist". Multiply the list by 2.
```
numlist = [1,2,3]
numlist * 2
```
Create a numpy array of numbers [1,2,3] called "numarr". Multiply the array by 2.
```
numarr = np.array([1,2,3])
numarr * 2
```
```
print(numlist*2)
print(numarr*2)
```
Question: What is the difference between multiplying lists and multiplying arrays?
- **Answer:** 

- When you multiply a list, the list is repeated according to the number you've given for it to be multiplied by. (E.g., list [1,2,3] multiplied by 2 is [1,2,3,1,2,3], the list doubled in length and is repeated twice).

- When you multiply a numpy array, each integer in the array is multiplied according to the number you've given, but the length of the array stays the same. (E.g., [1,2,3] becomes [2,4,6] if it is multiplied by 2, but still contains 3 integers).

Create a list of strings ['do','re','mi','fa'] called "strlist". Use operations to create the following outputs with your variable:
['dodo','rere','mimi','fafa']
['do','re','mi','fa','do','re','mi','fa']
['do','do','re','re','mi','mi','fa','fa']
[['do','do'],['re','re'],['mi','mi'],['fa','fa']]
```
strlist = ['do', 're', 'mi', 'fa']

# ['dodo','rere','mimi','fafa']
print([strlist[0]*2] +
      [strlist[1]*2] +
      [strlist[2]*2] +
      [strlist[3]*2])

# ['do','re','mi','fa','do','re','mi','fa']
print(strlist*2)

# ['do','do','re','re','mi','mi','fa','fa']
print([strlist[0]] + [strlist[0]] + 
      [strlist[1]] + [strlist[1]] + 
      [strlist[2]] + [strlist[2]] + 
      [strlist[3]] + [strlist[3]])

# [['do','do'],['re','re'],['mi','mi'],['fa','fa']]
print([[strlist[0]*2],
      [strlist[1]*2],
      [strlist[2]*2],
      [strlist[3]*2]])
```

## Zipping exercises:
Create a script that outputs a counterbalanced list with every face paired with every house, repeated with each possible post-cue. Then, randomize the order of the list.
```
import numpy as np

# VARIABLES
# 1. faces / houses present 1st
face_1st = ['face1.png']*5 + ['face2.png']*5 + ['face3.png']*5 + ['face4.png']*5 + ['face5.png']*5
house_1st = ['house1.png']*5 + ['house2.png']*5 + ['house3.png']*5 + ['house4.png']*5 + ['house5.png']*5

# 2. faces / houses present 2nd
face_2nd = ['face1.png','face2.png','face3.png','face4.png','face5.png']*5
house_2nd = ['house1.png','house2.png','house3.png','house4.png','house5.png']*5

# 3. post-cues
postcues = ['cue1']*25 + ['cue2']*25

# TRIALS
# Face presented first, house second
imgs_order1 = list(zip(face_1st, house_2nd))*2

# Half of all the possible trials, face presented first
TrialHalf1 = list(zip(imgs_order1, postcues))

# House presented first, face second
imgs_order2 = list(zip(house_1st, face_2nd))*2

# Half of all the possible trials, house presented first
TrialHalf2 = list(zip(imgs_order2, postcues))

# All trials combined
Alltrials = TrialHalf1 + TrialHalf2

# Randomize list of trials
np.random.shuffle(Alltrials)
print(Alltrials)
```

## Indexing exercises:
Create a list of strings called "colors", containing the following colors in this order: red, orange, yellow, green, blue, purple
```
colors = ['red', 'orange', 'yellow', 'green', 'blue', 'purple']
```
Using indexing, print the penultimate color.
```
print(colors[-2])
```
Using indexing, print the 3rd and 4th characters of the penultimate color.
```
print(colors[-2][2] + colors[-2][3])
```
Using indexing, remove the color "purple" and add "indigo" and "violet" to the list instead.
```
colors.remove(colors[5])
colors.append('indigo')
colors.append('violet')
print(colors)
```

## Slicing exercises:
Create a list of numbers 0-100 called "list100".
```
list100 = list(range(0,101))
```
Using slicing, print the first 10 numbers in the list.
```
print(list100[:10])
```
Using slicing, print all the odd numbers in the list backwards.
```
print(list100[99::-2])
```
Using slicing, print the last four numbers in the list backwards.
```
print(list100[100:96:-1])
```
Question: Are the 40th-44th numbers in the list equal to integers 39-43? Show the Boolean operation you would use to determine the truth value.
```
print(list100[39:44] == list(range(39,44)))
```
- **Answer:** Yes, the 40th-44th numbers in the list is equal to integers 39-43. 
