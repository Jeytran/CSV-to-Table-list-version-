# CSV-to-Table-list-version-
Python program takes a CSV file and produces a table with some computed data as the output. Program does this by making use of lists.

import math
import time

file_name = input("Enter a file name: ")
in_file = open(file_name)

#in_file = open("reducedweather.csv")

#reads the header, removes spaces and commas
heading = in_file.readline().strip().split(",")

#Overall list to contain all data
#amount of lists contained within columns is equal to number of columns in csv file
columns = []

#stores mean for each column in csv file
mean_temperature = []

#stores max for each column in csv file
max_temp = []

#stores min for each column in csv file
min_temp = []

#stores (data value - mean)^1/2 for each value in a column
#each column from csv file goes into its own respective list
squared_difference = []

#stores the standard deviation for each column 
standard_deviation = []


#appends empty list to the list columns
#the amount of lists it appends will be len(heading)
for i in heading:
    columns.append([])

#this will split each line of the data and make a list
# for each index of the created list, it will be appended to the
# list columns, in the appropriate index
for row in in_file:
    line = row.strip().split(",")
    for i in range(len(line)):
        columns[i].append(float(line[i]))


#calculates mean temp for each column and appends to mean_numbers
for i in range(len(columns)):
    added_temp = sum(columns[i])
    mean_value = added_temp / len(columns[i]) #divdes added temp by number of digits in list
    mean_temperature.append(mean_value)
    
#takes the max value of each list in columns, appends to max_temp
for i in range(len(columns)):
    max_value = max(columns[i])
    max_temp.append(max_value) 
#take mins value of each list in columns, appends to min_temp
    min_value = min(columns[i])
    min_temp.append(min_value)
    
    
#makes empty lists inside squared difference
#the numbers of lists it makes in equal to the amount of number of lists in columns
for i in range(len(columns)):
    squared_difference.append([])

#calculates the squared difference (data value - mean)^1/2 
#appends into the list squared_difference
for i in range(len(columns)):
    for j in range(len(columns[i])):
        s_d_value = math.pow((columns[i][j]- mean_temperature[i]), 2)
        squared_difference[i].append(s_d_value)
    
#calculates the standard deviation
for i in range(len(squared_difference)):
  #takes  sum of all the squared differences for each observation
    sum_sd = sum(squared_difference[i]) 
#divides sum_sd by numbers of observations in a column    
    sum_sd_divided = sum_sd/len(squared_difference[i])
#takes square root of sum_sd_divided    
    root_sum = math.pow(sum_sd_divided, (1 / 2))
    standard_deviation.append(root_sum)
    
#makes a table for the data, and formats it to 2 decimal points    
dash = "-" * 79
print("\n")
print("{:^15}|{:^15}|{:^15}|{:^15}|{:^15}" .format("Column Names", "Mean", "Std Deviation", "Highest Score", "Lowest Score"))
print(dash)  

#loops runs with 0, 1 to get wanted index of each list
for i in range(len(columns)):
    print("{:>15}|{:>15.2f}|{:>15.2f}|{:>15.2f}|{:>15.2f}" .format(heading[i], mean_temperature[i], standard_deviation[i], max_temp[i], min_temp[i]))
    print(dash)
print("\n")


print("\nProgrammed by Jenny Tran")
print("Date: " + time.ctime())
print("End of processing")

in_file.close()
