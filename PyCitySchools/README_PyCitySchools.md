
# PyCity Schools Analysis

# Schools , Students 
    # OBSERVED TREND 1   
        Total 15 schools in the district with 94% passing rate in Reading.
        
    # OBSERVED TREND 2
        Bailey High School has the highest student count - 4976
        Holden High School has the lowest student count - 427
        
        Pena High School has the highest avg score in both Maths (83.8) , Reading(84.0).
        Huang High School has the lowest avg score in Maths.
        Rodriguez High School , Ford High School has the lowest avg score in Reading 74.4
        
        Huang High School has the highest per student budget : $655
        Wilson High School has the lowest per student budget : $578
        
    # OBSERVED TREND 3
        Top 5 schools by passing rate , with 100% passing rate. All of them are Charter schools.
            Cabrera High School	
            Griffin High School	 
            Holden High School	 
            Pena High School	
            Shelton High School


```python
import os
import json
import pandas as pd
import numpy as np
from IPython.core.interactiveshell import InteractiveShell
InteractiveShell.ast_node_interactivity = "all"
```


```python
file_schools = os.path.join('Resources', 'schools_complete.csv')
file_students = os.path.join('Resources', 'students_complete.csv')
schools_df = pd.read_csv(file_schools)
students_df = pd.read_csv(file_students)

students_df = students_df.rename(columns={"Student ID":"Student_ID",
                                          "name":"Student_Name",
                                          "gender":"Gender",
                                          "grade":"Grade",
                                          "school":"School_Name",
                                          "reading_score" :"Reading_Score",
                                          "math_score" :"Math_Score"
                                         })
schools_df = schools_df.rename(columns={"School ID":"School_ID",
                                        "name":"School_Name",
                                        "type":"School Type",
                                        "size":"Size",
                                        "budget":"Budget"
                                       })
schools_students_DF = pd.merge(schools_df, students_df, on=["School_Name"])
schools_students_DF["Math_Pass"]= np.where(schools_students_DF['Math_Score'] > 65, "Pass", "Fail")
schools_students_DF["Reading_Pass"]= np.where(schools_students_DF['Reading_Score'] > 65, "Pass", "Fail")

schools_students_DF = schools_students_DF[["Student_ID","Student_Name","Gender","Grade","Reading_Score","Reading_Pass"
                     ,"Math_Score","Math_Pass","School_ID","School_Name","School Type","Size","Budget"]]

schools_students_DF.head(10)

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student_ID</th>
      <th>Student_Name</th>
      <th>Gender</th>
      <th>Grade</th>
      <th>Reading_Score</th>
      <th>Reading_Pass</th>
      <th>Math_Score</th>
      <th>Math_Pass</th>
      <th>School_ID</th>
      <th>School_Name</th>
      <th>School Type</th>
      <th>Size</th>
      <th>Budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>Pass</td>
      <td>79</td>
      <td>Pass</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>Pass</td>
      <td>61</td>
      <td>Fail</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>Pass</td>
      <td>60</td>
      <td>Fail</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>Pass</td>
      <td>58</td>
      <td>Fail</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>Pass</td>
      <td>84</td>
      <td>Pass</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>Bryan Miranda</td>
      <td>M</td>
      <td>9th</td>
      <td>94</td>
      <td>Pass</td>
      <td>94</td>
      <td>Pass</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>Sheena Carter</td>
      <td>F</td>
      <td>11th</td>
      <td>82</td>
      <td>Pass</td>
      <td>80</td>
      <td>Pass</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>Nicole Baker</td>
      <td>F</td>
      <td>12th</td>
      <td>96</td>
      <td>Pass</td>
      <td>69</td>
      <td>Pass</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>Michael Roth</td>
      <td>M</td>
      <td>10th</td>
      <td>95</td>
      <td>Pass</td>
      <td>87</td>
      <td>Pass</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>Matthew Greene</td>
      <td>M</td>
      <td>10th</td>
      <td>96</td>
      <td>Pass</td>
      <td>84</td>
      <td>Pass</td>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
  </tbody>
</table>
</div>



# District Summary


```python
total_schools =  len(schools_students_DF["School_Name"].unique())
total_student =  schools_students_DF["Student_ID"].count()
total_budget = sum(schools_students_DF["Budget"].unique())
avg_math_score = schools_students_DF["Math_Score"].sum()/total_student
avg_reading_score = schools_students_DF["Reading_Score"].sum()/total_student
passing_math = schools_students_DF[schools_students_DF["Math_Pass"]=="Pass"].count()["Student_ID"] / total_student * 100
passing_reading = schools_students_DF[schools_students_DF["Reading_Pass"]=="Pass"].count()["Student_ID"] / total_student * 100
overall_passing_rate = (passing_math + passing_reading) / 2

District_Summary_PD = pd.DataFrame({
    "Total Schools": [total_schools],
    "Total Students": [total_student],
    "Total Budget" : [total_budget],
    "Average Math Score": [avg_math_score],
    "Average Reading Score" : [avg_reading_score],
    "% Passing Math" : [passing_math],
    "% Passing Reading" : [passing_reading],
    "% Overall Passing Rate" : [overall_passing_rate]
})

District_Summary_PD = District_Summary_PD[[
    "Total Schools",
    "Total Students",
    "Total Budget",
    "Average Math Score",
    "Average Reading Score",
    "% Passing Math",
    "% Passing Reading",
    "% Overall Passing Rate"
]]

District_Summary_PD["Total Budget"] = District_Summary_PD["Total Budget"].map("${0:,.2f}".format)
District_Summary_PD["Total Students"] = District_Summary_PD["Total Students"].map("{0:,.0f}".format)
District_Summary_PD
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Schools</th>
      <th>Total Students</th>
      <th>Total Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>15</td>
      <td>39,170</td>
      <td>$24,649,428.00</td>
      <td>78.985371</td>
      <td>81.87784</td>
      <td>83.112076</td>
      <td>94.263467</td>
      <td>88.687771</td>
    </tr>
  </tbody>
</table>
</div>



# School Summary


```python
school_group = schools_students_DF.groupby("School_Name")
school_group_pass_math = schools_students_DF.loc[(schools_students_DF["Math_Pass"] == "Pass")]
school_group_pass_reading = schools_students_DF.loc[(schools_students_DF["Reading_Pass"] == "Pass")]

sg_school_type = school_group['School Type'].min()
sg_total_students = school_group['Student_ID'].count()
sg_total_budget = school_group['Budget'].min()
sg_student_budget = sg_total_budget / sg_total_students
sg_avg_math_score = school_group['Math_Score'].mean()
sg_avg_reading_score = school_group['Reading_Score'].mean()

sg_passing_math_df = school_group_pass_math.groupby("School_Name")["Student_ID"].count()/sg_total_students * 100
sg_passing_reading_df = school_group_pass_reading.groupby("School_Name")["Student_ID"].count()/sg_total_students * 100
sg_passing_overall_df = (sg_passing_math_df + sg_passing_reading_df) / 2




School_Summary = { 
    "School Type": sg_school_type,
    "Total Students": sg_total_students,
    "Total School Budget" : sg_total_budget,
    "Per Student Budget" : sg_student_budget,
    "Average Math Score": sg_avg_math_score,
    "Average Reading Score" : sg_avg_reading_score,
    "% Passing Math" : sg_passing_math_df,
    "% Passing Reading" : sg_passing_reading_df,
    "% Overall Passing Rate" : sg_passing_overall_df
}

School_Summary_DF = pd.DataFrame(School_Summary)

School_Summary_DF = School_Summary_DF[[ 
    "School Type",
    "Total Students",
    "Total School Budget" ,
    "Per Student Budget" ,
    "Average Math Score",
    "Average Reading Score" ,
    "% Passing Math" ,
    "% Passing Reading" ,
    "% Overall Passing Rate"
]]

School_Summary_DF["Total School Budget"] = School_Summary_DF["Total School Budget"].map("${0:,.2f}".format)
School_Summary_DF["Per Student Budget"] = School_Summary_DF["Per Student Budget"].map("${0:,.2f}".format)

School_Summary_DF




```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School_Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>District</td>
      <td>4976</td>
      <td>$3,124,928.00</td>
      <td>$628.00</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>75.602894</td>
      <td>91.901125</td>
      <td>83.752010</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356.00</td>
      <td>$582.00</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411.00</td>
      <td>$639.00</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>74.872838</td>
      <td>91.895558</td>
      <td>83.384198</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916.00</td>
      <td>$644.00</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>76.195692</td>
      <td>90.799562</td>
      <td>83.497627</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500.00</td>
      <td>$625.00</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020.00</td>
      <td>$652.00</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>75.469256</td>
      <td>91.456311</td>
      <td>83.462783</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087.00</td>
      <td>$581.00</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635.00</td>
      <td>$655.00</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>75.282825</td>
      <td>91.772369</td>
      <td>83.527597</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650.00</td>
      <td>$650.00</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>75.383323</td>
      <td>92.060491</td>
      <td>83.721907</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858.00</td>
      <td>$609.00</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363.00</td>
      <td>$637.00</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>75.543886</td>
      <td>91.522881</td>
      <td>83.533383</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>$1,056,600.00</td>
      <td>$600.00</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>Charter</td>
      <td>1635</td>
      <td>$1,043,130.00</td>
      <td>$638.00</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574.00</td>
      <td>$578.00</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>Charter</td>
      <td>1800</td>
      <td>$1,049,400.00</td>
      <td>$583.00</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
  </tbody>
</table>
</div>



# Top Performing Schools (By Passing Rate)


```python
School_Summary_DF = School_Summary_DF.sort_values(by="% Overall Passing Rate", ascending=False)
School_Summary_DF.head(5)


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School_Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Cabrera High School</th>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356.00</td>
      <td>$582.00</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500.00</td>
      <td>$625.00</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087.00</td>
      <td>$581.00</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858.00</td>
      <td>$609.00</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>Charter</td>
      <td>1761</td>
      <td>$1,056,600.00</td>
      <td>$600.00</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>100.0</td>
      <td>100.0</td>
      <td>100.0</td>
    </tr>
  </tbody>
</table>
</div>



# Bottom Performing Schools(By passing Rate)


```python
School_Summary_DF = School_Summary_DF.sort_values(by="% Overall Passing Rate", ascending=True)
School_Summary_DF.head(5)

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School_Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Figueroa High School</th>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411.00</td>
      <td>$639.00</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>74.872838</td>
      <td>91.895558</td>
      <td>83.384198</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020.00</td>
      <td>$652.00</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>75.469256</td>
      <td>91.456311</td>
      <td>83.462783</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916.00</td>
      <td>$644.00</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>76.195692</td>
      <td>90.799562</td>
      <td>83.497627</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635.00</td>
      <td>$655.00</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>75.282825</td>
      <td>91.772369</td>
      <td>83.527597</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363.00</td>
      <td>$637.00</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>75.543886</td>
      <td>91.522881</td>
      <td>83.533383</td>
    </tr>
  </tbody>
</table>
</div>



   # Math Scores by Grade


```python
Grade_9th = schools_students_DF.loc[(schools_students_DF["Grade"] == "9th")]
Grade_10th = schools_students_DF.loc[(schools_students_DF["Grade"] == "10th")]
Grade_11th = schools_students_DF.loc[(schools_students_DF["Grade"] == "11th")]
Grade_12th = schools_students_DF.loc[(schools_students_DF["Grade"] == "12th")]

Grade_9th_group = Grade_9th.groupby("School_Name")
Grade_10th_group = Grade_10th.groupby("School_Name")
Grade_11th_group = Grade_11th.groupby("School_Name")
Grade_12th_group = Grade_12th.groupby("School_Name")

math_Avg_9th = Grade_9th_group["Math_Score"].mean()
math_Avg_10th = Grade_10th_group["Math_Score"].mean()
math_Avg_11th = Grade_11th_group["Math_Score"].mean()
math_Avg_12th = Grade_12th_group["Math_Score"].mean()

Math_Grade_Summary = { 
    "9th": math_Avg_9th,
    "10th": math_Avg_10th,
    "11th" : math_Avg_11th,
    "12th" : math_Avg_12th
}

Math_Grade_Summary_DF = pd.DataFrame(Math_Grade_Summary)

Math_Grade_Summary_DF = Math_Grade_Summary_DF[[ 
    "9th",
    "10th",
    "11th" ,
    "12th"
]]

Math_Grade_Summary_DF





```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>School_Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>



# Reading Score by Grade


```python
reading_Avg_9th = Grade_9th_group["Reading_Score"].mean()
reading_Avg_10th = Grade_10th_group["Reading_Score"].mean()
reading_Avg_11th = Grade_11th_group["Reading_Score"].mean()
reading_Avg_12th = Grade_12th_group["Reading_Score"].mean()

Reading_Grade_Summary = { 
    "9th": math_Avg_9th,
    "10th": math_Avg_10th,
    "11th" : math_Avg_11th,
    "12th" : math_Avg_12th
}

Reading_Grade_Summary_DF = pd.DataFrame(Reading_Grade_Summary)

Reading_Grade_Summary_DF = Reading_Grade_Summary_DF[[ 
    "9th",
    "10th",
    "11th" ,
    "12th"
]]

Reading_Grade_Summary_DF



```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>9th</th>
      <th>10th</th>
      <th>11th</th>
      <th>12th</th>
    </tr>
    <tr>
      <th>School_Name</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Bailey High School</th>
      <td>77.083676</td>
      <td>76.996772</td>
      <td>77.515588</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>Cabrera High School</th>
      <td>83.094697</td>
      <td>83.154506</td>
      <td>82.765560</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>Figueroa High School</th>
      <td>76.403037</td>
      <td>76.539974</td>
      <td>76.884344</td>
      <td>77.151369</td>
    </tr>
    <tr>
      <th>Ford High School</th>
      <td>77.361345</td>
      <td>77.672316</td>
      <td>76.918058</td>
      <td>76.179963</td>
    </tr>
    <tr>
      <th>Griffin High School</th>
      <td>82.044010</td>
      <td>84.229064</td>
      <td>83.842105</td>
      <td>83.356164</td>
    </tr>
    <tr>
      <th>Hernandez High School</th>
      <td>77.438495</td>
      <td>77.337408</td>
      <td>77.136029</td>
      <td>77.186567</td>
    </tr>
    <tr>
      <th>Holden High School</th>
      <td>83.787402</td>
      <td>83.429825</td>
      <td>85.000000</td>
      <td>82.855422</td>
    </tr>
    <tr>
      <th>Huang High School</th>
      <td>77.027251</td>
      <td>75.908735</td>
      <td>76.446602</td>
      <td>77.225641</td>
    </tr>
    <tr>
      <th>Johnson High School</th>
      <td>77.187857</td>
      <td>76.691117</td>
      <td>77.491653</td>
      <td>76.863248</td>
    </tr>
    <tr>
      <th>Pena High School</th>
      <td>83.625455</td>
      <td>83.372000</td>
      <td>84.328125</td>
      <td>84.121547</td>
    </tr>
    <tr>
      <th>Rodriguez High School</th>
      <td>76.859966</td>
      <td>76.612500</td>
      <td>76.395626</td>
      <td>77.690748</td>
    </tr>
    <tr>
      <th>Shelton High School</th>
      <td>83.420755</td>
      <td>82.917411</td>
      <td>83.383495</td>
      <td>83.778976</td>
    </tr>
    <tr>
      <th>Thomas High School</th>
      <td>83.590022</td>
      <td>83.087886</td>
      <td>83.498795</td>
      <td>83.497041</td>
    </tr>
    <tr>
      <th>Wilson High School</th>
      <td>83.085578</td>
      <td>83.724422</td>
      <td>83.195326</td>
      <td>83.035794</td>
    </tr>
    <tr>
      <th>Wright High School</th>
      <td>83.264706</td>
      <td>84.010288</td>
      <td>83.836782</td>
      <td>83.644986</td>
    </tr>
  </tbody>
</table>
</div>



# Scores by School Spending


```python
ss_total_students = school_group['Student_ID'].count()
ss_total_math = school_group['Math_Score'].sum()
ss_total_reading = school_group['Reading_Score'].sum()
ss_pass_math = school_group_pass_math.groupby("School_Name")["Student_ID"].count()
ss_pass_reading = school_group_pass_reading.groupby("School_Name")["Student_ID"].count()
ss_total_budget = school_group['Budget'].min()
ss_student_budget = ss_total_budget / ss_total_students

School_score_Summary = { 
    "Total Students": ss_total_students,
    "Total Math Score" : ss_total_math,
    "Total Reading Score" : ss_total_reading,
    "Maths passed count": ss_pass_math,
    "Reading passed count" : ss_pass_reading,
    "Total Budget" : ss_total_budget,
    "Per Student Budget" : ss_student_budget
}

School_score_Summary_DF = pd.DataFrame(School_score_Summary)

bins = [0,585,615,645,675]
group_names = ['<$585', '$585-615', '$615-645', '$645-675']
School_score_Summary_DF["Spending Ranges (Per Student)"] =  pd.cut(School_score_Summary_DF["Per Student Budget"], bins, labels=group_names)

school_spend_group = School_score_Summary_DF.groupby("Spending Ranges (Per Student)")
 
spend_avg_math = school_spend_group["Total Math Score"].sum() / school_spend_group["Total Students"].sum()
spend_avg_reading = school_spend_group["Total Reading Score"].sum() / school_spend_group["Total Students"].sum()
spend_pass_math = (school_spend_group["Maths passed count"].sum() / school_spend_group["Total Students"].sum())*100
spend_pass_reading = (school_spend_group["Reading passed count"].sum() / school_spend_group["Total Students"].sum())*100
spend_overall = (spend_pass_math + spend_pass_reading) / 2

School_spend_Summary = { 
    "Average Math Score": spend_avg_math,
    "Average Reading Score" : spend_avg_reading,
    "% Passing Math" : spend_pass_math,
    "% Passing Reading": spend_pass_reading,
    "% Overall Passing Rate" : spend_overall 
}

School_spend_Summary_DF = pd.DataFrame(School_spend_Summary)

School_spend_Summary_DF = School_spend_Summary_DF[[
    "Average Math Score",
    "Average Reading Score",
    "% Passing Math",
    "% Passing Reading",
    "% Overall Passing Rate"
]]

School_spend_Summary_DF
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>Spending Ranges (Per Student)</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$585</th>
      <td>83.363065</td>
      <td>83.964039</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>$585-615</th>
      <td>83.529196</td>
      <td>83.838414</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>$615-645</th>
      <td>78.061635</td>
      <td>81.434088</td>
      <td>79.821006</td>
      <td>93.059777</td>
      <td>86.440392</td>
    </tr>
    <tr>
      <th>$645-675</th>
      <td>77.049297</td>
      <td>81.005604</td>
      <td>75.391862</td>
      <td>91.764801</td>
      <td>83.578332</td>
    </tr>
  </tbody>
</table>
</div>



# Scores By School Size


```python
sz_total_students = school_group['Student_ID'].count()
sz_total_math = school_group['Math_Score'].sum()
sz_total_reading = school_group['Reading_Score'].sum()
sz_pass_math = school_group_pass_math.groupby("School_Name")["Student_ID"].count()
sz_pass_reading = school_group_pass_reading.groupby("School_Name")["Student_ID"].count()
sz_total_budget = school_group['Budget'].min()
sz_student_budget = sz_total_budget / sz_total_students

School_size_Summary = { 
    "Total Students": ss_total_students,
    "Total Math Score" : ss_total_math,
    "Total Reading Score" : ss_total_reading,
    "Maths passed count": ss_pass_math,
    "Reading passed count" : ss_pass_reading,
    "Total Budget" : ss_total_budget,
    "Per Student Budget" : ss_student_budget
}

School_size_Summary_DF = pd.DataFrame(School_size_Summary)

bins1 = [0,1000,2000,5000]
group_names1 = ['small(<1000)', 'Medium(1000-2000)', 'Large(2000-5000)']
School_size_Summary_DF["School Size"] =  pd.cut(School_size_Summary_DF["Total Students"], bins1, labels=group_names1)

school_size_group = School_size_Summary_DF.groupby("School Size")
 
size_avg_math = school_size_group["Total Math Score"].sum() / school_size_group["Total Students"].sum()
size_avg_reading = school_size_group["Total Reading Score"].sum() / school_size_group["Total Students"].sum()
size_pass_math = (school_size_group["Maths passed count"].sum() / school_size_group["Total Students"].sum())*100
size_pass_reading = (school_size_group["Reading passed count"].sum() / school_size_group["Total Students"].sum())*100
size_overall = (size_pass_math + size_pass_reading) / 2

School_size_Summary = { 
    "Average Math Score": size_avg_math,
    "Average Reading Score" : size_avg_reading,
    "% Passing Math" : size_pass_math,
    "% Passing Reading": size_pass_reading,
    "% Overall Passing Rate" : size_overall 
}

School_size_Summary_DF = pd.DataFrame(School_size_Summary)

School_size_Summary_DF = School_size_Summary_DF[[
    "Average Math Score",
    "Average Reading Score",
    "% Passing Math",
    "% Passing Reading",
    "% Overall Passing Rate"
]]

School_size_Summary_DF
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>small(&lt;1000)</th>
      <td>83.828654</td>
      <td>83.974082</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Medium(1000-2000)</th>
      <td>83.372682</td>
      <td>83.867989</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>Large(2000-5000)</th>
      <td>77.477597</td>
      <td>81.198674</td>
      <td>77.391572</td>
      <td>92.320312</td>
      <td>84.855942</td>
    </tr>
  </tbody>
</table>
</div>



# Scores By School Type


```python
school_type_group = schools_students_DF.groupby("School Type")
school_type_group_pass_math = schools_students_DF.loc[(schools_students_DF["Math_Pass"] == "Pass")]
school_type_group_pass_reading = schools_students_DF.loc[(schools_students_DF["Reading_Pass"] == "Pass")]


st_total_students = school_type_group['Student_ID'].count()
st_avg_math_score = school_type_group['Math_Score'].mean()
st_avg_reading_score = school_type_group['Reading_Score'].mean()

st_passing_math_df = school_type_group_pass_math.groupby("School Type")["Student_ID"].count()/st_total_students * 100
st_passing_reading_df = school_type_group_pass_reading.groupby("School Type")["Student_ID"].count()/st_total_students * 100
st_passing_overall_df = (st_passing_math_df + st_passing_reading_df) / 2

School_Type_Summary = { 
    "Average Math Score": st_avg_math_score,
    "Average Reading Score" : st_avg_reading_score,
    "% Passing Math" : st_passing_math_df,
    "% Passing Reading" : st_passing_reading_df,
    "% Overall Passing Rate" : st_passing_overall_df
}

School_Type_Summary_DF = pd.DataFrame(School_Type_Summary)

School_Type_Summary_DF = School_Type_Summary_DF[[ 
    "Average Math Score",
    "Average Reading Score" ,
    "% Passing Math" ,
    "% Passing Reading" ,
    "% Overall Passing Rate"
]]

School_Type_Summary_DF


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.406183</td>
      <td>83.902821</td>
      <td>100.000000</td>
      <td>100.000000</td>
      <td>100.000000</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.987026</td>
      <td>80.962485</td>
      <td>75.478203</td>
      <td>91.670374</td>
      <td>83.574288</td>
    </tr>
  </tbody>
</table>
</div>


