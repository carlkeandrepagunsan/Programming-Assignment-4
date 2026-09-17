# Programming-Assignment-4
**Carl Keandre L. Pagunsan | 2ECE-C** <br>
The repository contains the Programming Assignment 3 for the ECE2112 or Advanced Computer Programming and Algorithms Class. The objectives of the assignment are to:
1. filter tabular data using several categorical and numerical conditions;
2. construct focused DataFrames by selecting relevant features;
3. summarize the relationship between categorical features and a numerical variable; and
4. communicate a data comparison using clear and correctly labeled plots.
### PRELUDE
Before anything, pandas, matplotlib, and the required xlsx file were loaded into the notebook:
```python
import pandas as pd
import matplotlib.pyplot as plt
df = pd.read_excel('board2.xlsx')
```
Then, the ```Average``` column was added to the dataframe because it was required:
```python
df['Average'] = df[['GEAS', 'Electronics','Math','Communication']].mean(axis=1)
```
# A. Visayas Communication Dataframe
The task was to create a DataFrame called ```VisComm``` for students whose ```Hometown``` is Visayas, and Track is ```Communication```. Then, only the ```Name, Gender, Math, Electronics, Average``` columns were retained.
```python
VisComm = df.loc[(df['Hometown'] == 'Visayas') & (df['Track'] == 'Communication'), ['Name', 'Gender', 'Math', 'Electronics', 'Average']] .reset_index()
```
Then, the number of rows had to be displayed
```
VisComm.shape[0]
```
### Functions used:
```df.loc``` - slices the dataframe according to parameters given <br>
```df.shape[0]``` - shows the shape of the dataframe, with [0] used to only show the number of rows.

# B. Visayas Female Dataframe
Same as letter A, you have to create a DataFrame except in this instance the '''Gender''' has to be '''Female''' while retaining the '''Visayas''' Hometown. The columns of '''Name, Gender, GEAS, Electronics, Average''' columns.
```python
VisFemale = df.loc[(df['Hometown'] == 'Visayas') & (df['Gender'] == 'Female'), ['Name', 'Track', 'GEAS', 'Electronics', 'Average']].reset_index()
```
Then, only the rows of students in the ```VisFemale``` dataframe with an average greater than or equal to 60 had to be displayed:
```python
VisFemale.loc[VisFemale['Average'] >= 60]
```
### Functions used:
```df.loc``` - Same purpose as in A, to slice the dataframe according to the parameters. This was also used to find the rows in which the average is greater than 60.

# C. Category Average Visualization
For this problem, the mean of the average of each category had to be calculated and then plotted whilst adding statements under each graph.
First, the mean of the Average category for each of ```Track```, ```Gender```, and ```Hometown``` were found and put into their own variables:
```python
mean_track = df.groupby("Track")["Average"].mean().reset_index()
mean_gender = df.groupby("Gender")["Average"].mean().reset_index()
mean_hometown = df.groupby("Hometown")["Average"].mean().reset_index()
```
and then displayed.
Afterwards, the three bar graphs were plotted using matplotlib's plotting function:
```python
plt.figure(figsize=(15,5))

plt.subplot(1,3,1)
plt.bar(mean_track['Track'], mean_track['Average'], color = 'Green')
plt.title('Category Average')
plt.xlabel('Category')
plt.ylabel('Average')
plt.text (-0.6,-23,'The Category that had the highest sample mean was \nCommunication with a score of 67.975.')
plt.ylim(0,100)

plt.subplot(1,3,2)
plt.bar(mean_gender['Gender'], mean_gender['Average'], color = 'Brown')
plt.title('Gender Average')
plt.xlabel('Gender')
plt.text (-0.6,-23,'The Gender that had the highest sample mean was Male\nwith a score of 67.183.')
plt.ylim(0,100)

plt.subplot(1,3,3)
plt.bar(mean_hometown['Hometown'], mean_hometown['Average'], color = 'Blue')
plt.title('Hometown Average')
plt.xlabel('Hometown')
plt.text (-0.6,-23,'The Hometown that had the highest sample mean was Luzon\nwith a score of 68.083.')
plt.ylim(0,100)



plt.tight_layout()
plt.show()
```
This was then displayed.
### Functions used:
```df.groupby()``` - groups rows by a specific category that is set in the parameters. <br>
```.mean()``` - takes the mean of a column. <br>
```.reset_index()``` - resets the index of a sliced dataframe back to 0.<br>
```plt.figure()``` - creates a figure of a specific size set by the user.<br>
```plt.subplot()``` - creates a figure within the figure set before.<br>
```plt.bar()``` - creates a bar graph in the figure.<br>
```plt.title``` - sets the title of the graph.<br>
```plt.xlabel()``` - sets the name of the x axis in the graph.<br>
```plt.ylabel()``` - sets the name of the y axis in the graph.<br>
```plt.text()``` - adds text to the graph.<br>
```plt.ylim``` - sets the limit of the vertical axis of the graph.<br>
```plt.tight_layout()``` - automatically fixes the size of the graph.<br>
```plt.show()``` - shows the graph.<br>

## Version History
**September 17, 2026** - README File created.
