# seaborn3
titanic data analysis
#importing all libraries
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
#load titanic dataset
titanic=sns.load_dataset("titanic")
#print first 5 rows of data
titanic.head()
>>>>>output
survived	pclass	sex	age	sibsp	parch	fare	embarked	class	who	adult_male	deck	embark_town	alive	alone
0	0	        3   	male	22.0	1	0	7.2500	S	Third	man	True	NaN	Southampton	no	False
1	1	        1	    female	38.0	1	0	71.2833	C	First	woman	False	C	Cherbourg	yes	False
2	1       	3	    female	26.0	0	0	7.9250	S	Third	woman	False	NaN	Southampton	yes	True
3	1       	1	    female	35.0	1	0	53.1000	S	First	woman	False	C	Southampton	yes	False
4	0	        3     	male	35.0	0	0	8.0500	S	Third	man	True	NaN	Southampton	no	True

#we wish to show that people who were not alone, they survived
print(titanic.groupby('alone')['survived'].mean())
>>>output
alone
False    0.505650
True     0.303538
above result shows that people who were alone, 50% people of them survived.where as 30% people were not alone survived

# we wish to seek the information that how many people by gender by percentage survived with respect to class in which they were travelling.
print(titanic.pivot_table('survived','sex','class'))  #using pandas library
>>>output
class      First    Second     Third
sex                                 
female  0.968085  0.921053  0.500000
male    0.368852  0.157407  0.135447
above result clearly shows that females in the first class survived the most.however female are good survivor than man in any class.

#now we wish to seprate them by age,so let's create an age variable
age=pd.cut(titanic['age'],[0,17,100])
print(titanic.pivot_table('survived',['sex',age],'class'))
class                First    Second     Third
sex    age                                    
female (0, 17]    0.875000  1.000000  0.542857
       (17, 100]  0.974026  0.903226  0.417910
male   (0, 17]    1.000000  0.818182  0.232558
       (17, 100]  0.371134  0.068182  0.133333
       from above result it is clearly visible that that male in the age group of 0-17 survived 100% in the first class.where as the male in the age group of 17-100 in the third class are worst survivor.
