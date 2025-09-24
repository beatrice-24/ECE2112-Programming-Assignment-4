# PROGRAMMING ASSIGNMENT 4

This repository contains my Jupyter Notebook submission for **ECE 2112: Advanced Computer Programming and Algorithms – Experiment 4**, covering one problem:
**ECE Board Exam Problem**, divided into **(i) data frames** and **(ii) visualization of data**.

> Source of problems: *EXPERIMENT 4 - Data Wrangling and Data Visualization.pdf*

---

## Project Structure

```
.
├─ board2.csv              # dataset containing student information (Track, Gender, Hometown, Average, etc.)
├─ 2ECEB_LUCAS_PA4.ipynb   # Jupyter notebook with solutions
└─ README.md     
```

---

# ECE BOARD EXAM

**ECE BOARD EXAM PROBLEM**: Using data wrangling and data visualization technique with storytelling, analyze the data and present different (i) data frames; and (ii) visuals using the dataset given.

1. Create the following data frames based on the format provided: <br>
   Example: Vis = [“Name”, “Gender”, “Track”, “Math<70”]; hometown is constant as **Visayas**

    Output:
    <div align="center">

    | Name | Gender | Track            | Math |
    |------|--------|------------------|------|
    | S4   | Male   | Instrumentation  | 65   |
    | S11  | Female | Communication    | 48   |
    | S22  | Female | Communication    | 64   |

    </div>
---

# 1a. INSTRU DATAFRAME

## Problem Description
Filename: Instru = [“Name”, “GEAS”, “Electronics >70”]; where track is constant as Instrumentation and hometown Luzon.

---

## Implementation and Explanation

### 1. Import Pandas
We import the `pandas` library, which provides tools for working with tabular data in Python through DataFrames.

```
import pandas as pd
```

### 2. Load the dataset
The dataset `board2.csv` is read into a DataFrame named `board2`. Displaying it shows the full table of student records. 

```
board2 = pd.read_csv('board2.csv')
board2            
```

### 3. Filter and create the DataFrame
We apply three conditions: Electronics grade > 70, Track = Instrumentation, and Hometown = Luzon. Only the columns `Name`, `GEAS`, and `Electronics` are selected for the new DataFrame `Instru`.

```
Instru = board2[                               
    (board2['Electronics'] > 70) &            
    (board2['Track'] == 'Instrumentation') &   
    (board2['Hometown'] == 'Luzon')           
][['Name', 'GEAS', 'Electronics']]            

Instru         
```

### **Sample Output:**  

```
   Name  GEAS  Electronics
0   S1    75       89
7   S8    64       81
29  S30   57       81
``` 

# 1b. MINDY DATAFRAME

## Problem Description
Filename: Mindy = [“Name”, “Track”, “Electronics”, “Average >=55”]; where hometown is constant as Mindanao and gender Female.

---

## Implementation and Explanation

### 1. Compute average grades
We calculate the average of the four subjects (`Math`, `Electronics`, `GEAS`, `Communication`) for each student. The result is stored in a new column `Average`.

```
board2['Average'] = board2[['Math', 'Electronics', 'GEAS', 'Communication']].mean(axis=1) 

board2
```

### 2. Filter and create the DataFrame
We filter students with Average ≥ 55, Hometown = Mindanao, and Gender = Female. Only the columns `Name`, `Track`, `Electronics`, and `Average` are included in the new DataFrame `Mindy`. 

```
Mindy = board2[
    (board2['Average'] >= 55) &                  
    (board2['Hometown'] == 'Mindanao') &        
    (board2['Gender'] == 'Female')            
][['Name', 'Track', 'Electronics', 'Average']]  

Mindy           
```

### **Sample Output:**  

```
   Name            Track          Electronics  Average
1   S2   Communication              75        67.25
2   S3   Instrumentation            71        72.75
14  S15  Microelectronics           41        59.00
16  S17  Microelectronics           79        70.50
19  S20  Communication              60        66.50
``` 

# 2. VISUALIZATIONS

## Problem Description
Create a visualization that shows how the different features contributes to average grade. Does chosen track in college, gender, or hometown contributes to a higher average score?

---

## Implementation and Explanation

### 1. Import Matplotlib
We import the `matplotlib.pyplot` module as `plt` to generate plots and graphs.

```
import matplotlib.pyplot as plt                
```

### 2. Average Grade by College Track
We group students by `Track`, calculate their mean `Average` grades, and plot the result as a bar chart in maroon.

- **X-axis (College Track):** Different academic tracks chosen by students.
- **Y-axis (Average Grade:** Mean grade of students within each track.
- **Title:** Clearly indicates we are comparing the college track against the average score.

```
track_avg = board2.groupby('Track')['Average'].mean()                          
plt.figure(figsize=(5,5))                                                      
plt.bar(track_avg.index, track_avg.values, color='Maroon')                      
plt.xlabel('College Track')                                                     
plt.ylabel('Average Grade')                                                      
plt.title('College Track vs Average Score')              
```

### 3. Average Grade by Gender
We group students by `Gender`, compute their mean 'Average' grades, and plot the result as a green bar chart. 

- **X-axis (Gender):** Male and female categories.
- **Y-axis (Average Grade:** Mean grade of students for each gender.
- **Title:** Highlights the comparison of gender with respect to the average score.

```
gender_avg = board2.groupby('Gender')['Average'].mean()                       
plt.figure(figsize=(5,5))                                                    
plt.bar(gender_avg.index, gender_avg.values, color='Green')                     
plt.xlabel('Gender')                                                             
plt.ylabel('Average Grade')                                                     
plt.title('Gender vs Average Score')                       
```

### 4. Average Grade by Hometown
We group students by `Hometown`, calculate the mean of their `Average` grade, and plot the result as a navy-colored bar chart.

- **X-axis (Hometown):** Regional categories (Luzon, Visayas, Mindanao)
- **Y-axis (Average Grade:** Mean grade of students from each region.
- **Title:** Shows the relationship between a student's hometown and their average score.
  
```
hometown_avg = board2.groupby('Hometown')['Average'].mean()                   
plt.figure(figsize=(5,5))                                                      
plt.bar(hometown_avg.index, hometown_avg.values, color='Navy')                  
plt.xlabel('Hometown')                                                          
plt.ylabel('Average Grade')                                                     
plt.title('Hometown vs Average Score')     
```

### **Sample Outputs (Visualizations)**  

- **College Track vs Average Score** – Bar chart comparing mean grades across different college tracks. 
- **Gender vs Average Score** – Bar chart comparing male and female average scores.  
- **Hometown vs Average Score** – Bar chart comparing Luzon, Visayas, and Mindanao average scores.  

---

**Author:** LUCAS, Beatrice Sophia

**Section:** 2ECE-B

**Course:** ECE 2112 (Advanced Computer Programming and Algorithms)  
