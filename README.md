# Ipums_twins_study
A replication project completed during my Masters degree, attempting to duplicate Angrist &amp; Evans' 1997 Paper 'Children and Their Parents' Labor Supply'. 

* Generate unique code for every individual, based on pernum and serial

sort serial pernum
gen zeros = "000000000"
egen idlong = concat(zeros serial pernum)
gen person_id=substr(idlong,-9,.)
duplicates drop person_id, force


* Determine age and gender of all children born


*** Child 1

cap drop child_pernum1
gen child_pernum1 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 

cap drop gender1
gen gender1 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0

cap drop age1
gen age1 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0

forv i =-19(1) 20{
	display "`i'"
	replace child_pernum1 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 
	replace gender1 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 
	replace age1 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 

}



*** Child 2 

cap drop age2
gen age2 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & pernum[_n-20] > child_pernum1 

cap drop child_pernum2
gen child_pernum2 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & pernum[_n-20] > child_pernum1 & age[_n-20]<age1

cap drop gender2
gen gender2 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & pernum[_n-20] > child_pernum1 

forv i=-19(1) 20{
	display "`i'"
	replace child_pernum2 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & pernum[_n+`i'] > child_pernum1 
	
	replace gender2 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & pernum[_n+`i'] > child_pernum1 
	
	replace age2 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & pernum[_n+`i'] > child_pernum1 
}

*** Child 3

cap drop child_pernum3
gen child_pernum3 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2)

cap drop gender3
gen gender3 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2)

cap drop age3
gen age3 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2)

forv i=-19(1) 20{
	display "`i'"
	replace child_pernum3 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2)
	
	replace gender3 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2)
	
	replace age3 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2)
	
}

*** Child 4

cap drop child_pernum4
gen child_pernum4 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3)

cap drop gender4
gen gender4 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3)

cap drop age4
gen age4 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3)

forv i=-19(1) 20{
	display "`i'"
	replace child_pernum4 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3)
	
	replace gender4 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3)
	
	replace age4 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3)
	
}

*** Child 5

cap drop child_pernum5
gen child_pernum5 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4)

cap drop gender5
gen gender5 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4)
	
cap drop age5
gen age5 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4)

forv i=-19(1) 20{
	display "`i'"
	
	replace child_pernum5 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4)
	
	replace gender5 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4)
	
	replace age5 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4)
			
}


*** Child 6

cap drop child_pernum6
gen child_pernum6 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5)

cap drop gender6
gen gender6 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5)
	
cap drop age6
gen age6 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5)

forv i=-20(1) 20{
	display "`i'"
	
	replace child_pernum6 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5)

	replace gender6 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5)
				
	replace age6 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5)

}

*** Child 7

cap drop child_pernum7
gen child_pernum7 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6)

cap drop gender7
gen gender7 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6)
	
cap drop age7
gen age7 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6)

forv i=-20(1) 20{
	display "`i'"
	
	replace child_pernum7 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6)							
	
	replace gender7 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6)
	
	replace age7 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6)

}

*** Child 8

cap drop child_pernum8
gen child_pernum8 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7)

cap drop gender8
gen gender8 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7)
	
cap drop age8
gen age8 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7)
	
forv i=-20(1) 20{
	display "`i'"
	
	replace child_pernum8 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7)
	
	replace gender8 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7)
				
	replace age8 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7)							
}

*** Child 9

cap drop child_pernum9
gen child_pernum9 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8)

cap drop gender9
gen gender9 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8)
	
cap drop age9
gen age9 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8)

forv i=-20(1) 20{
	display "`i'"
	
	replace child_pernum9 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8)					
	
	replace gender9 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8)					
				
	replace age9 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8)					
}


*** Child 10

cap drop child_pernum10
gen child_pernum10 = pernum[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8, child_pernum9)					

cap drop gender10
gen gender10 = sex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8, child_pernum9)
	
cap drop age10
gen age10 = age[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & !inlist(pernum[_n-20], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8, child_pernum9)

forv i=-20(1) 20{
	display "`i'"
	replace child_pernum10 = pernum[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8, child_pernum9)
	
	replace gender10 = sex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8, child_pernum9)
	
	replace age10 = age[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] !=0 & !inlist(pernum[_n+`i'], child_pernum1, child_pernum2, child_pernum3, child_pernum4, child_pernum5, child_pernum6, child_pernum7, child_pernum8, child_pernum9)
}


*** Generate variable for women aged 21-35 and 36-50 
gen women_2135 = 1 if sex == 2 & age >= 21 & age <= 35 
gen women_3650 = 1 if sex == 2 & age >= 36 & age <= 50 


*** Determine actual number of children born 
generate actual_chborn = chborn-1 if chborn > 0  
replace actual_chborn = 0 if actual_chborn ==.

save "Master_Code_Final.dta", replace


*** Rename pernum in preperation for transforming data to wide
rename child_pernum1 pernum1
rename child_pernum2 pernum2
rename child_pernum3 pernum3
rename child_pernum4 pernum4
rename child_pernum5 pernum5
rename child_pernum6 pernum6
rename child_pernum7 pernum7
rename child_pernum8 pernum8
rename child_pernum9 pernum9
rename child_pernum10 pernum10


*** Drop non-mothers
drop if age1 ==. & age2 ==. & age3 ==. & age4 ==. & age5 ==. & age6 ==. & age7 ==. & age8 ==. & age9 ==. & age10 ==. 


*** Drop variables which aren't relevant.
keep person_id pernum1 gender1 age1 pernum2 gender2 age2 pernum3 age3 gender3 pernum4 gender4 age4 pernum5 gender5 age5 pernum6 gender6 age6 pernum7 age7 gender7 pernum8 age8 gender8 pernum9 age9 gender9 pernum10 age10 gender10 

*** Reshape data so that every individual sits on a seperate row
reshape long age gender, i(person_id) j(pernum)

*** Drop if not a child
drop if gender ==.


*** Sort data by serial and age 
drop if age > 17
gsort person_id -age
cap drop age_rank
by person_id: egen age_rank = rank(-age) 


*** Generate age_rank to find eldest
keep person_id gender age age_rank 
egen age_rank2 = seq(), by(person_id)
cap drop age_rank
reshape wide gender age, i(person_id) j(age_rank2)


*** Drop unnecessary variables 
keep person_id gender1 age1 gender2 age2 age3 gender3 
 

save "Eldest.dta", replace
 
*** Merge with original dataset
merge 1:1 person_id using "/Users/ameliablamey/Documents/ECON Replication Project/Main Assignment/Master_Code_Final.dta"


*** Identify mothers whose eldest two children have been allocatd by state 
cap drop allocated_by_state_age
gen allocated_by_state_age = qage[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & age1==age[_n-20] | age2==age[_n-20]	& gender1==sex[_n-20] | gender2==sex[_n-20] 

cap drop allocated_by_state_sex
gen allocated_by_state_sex = qsex[_n-20] if serial==serial[_n-20] & pernum==momloc[_n-20] & momloc[_n-20] !=0 & age1==age[_n-20] | age2==age[_n-20]	& gender1==sex[_n-20] | gender2==sex[_n-20] 
	

forv i=-20(1) 20{
	display "`i'"
	replace allocated_by_state_age = qage[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] & age1==age[_n+`i'] | age2==age[_n+`i'] & gender1==sex[_n+`i'] | gender2==sex[_n+`i']
	
	replace allocated_by_state_sex = qsex[_n+`i'] if serial==serial[_n+`i'] & pernum==momloc[_n+`i'] & momloc[_n+`i'] & age1==age[_n+`i'] | age2==age[_n+`i'] & gender1==sex[_n+`i'] | gender2==sex[_n+`i']
	
}

*** Drop mothers if childrens' age or sex has been allocated by state
drop if allocated_by_state_age == 4
drop if allocated_by_state_sex == 4
 

//////////////////////////////// Table 1 //////////////////////////////////////////
 
 
* Women aged 21-35
mean actual_chborn if women_2135==1
sum actual_chborn if women_2135==1 & actual_chborn >1
sum workedyr if women_2135==1 & workedyr==3
tabulate women_2135 

* Women aged 36-50
mean actual_chborn if women_3650==1
sum actual_chborn if women_3650==1 & actual_chborn >1
sum workedyr if women_3650==1 & workedyr==3
tabulate women_3650

* Women aged 21-35 with 2 or more children
mean actual_chborn if women_2135==1 & actual_chborn >1
sum actual_chborn if women_2135==1 & actual_chborn >2
sum workedyr if women_2135==1 & workedyr==3 & actual_chborn >1
tabulate women_2135 if actual_chborn >1

* Married women aged 21-35 with 2 or more children
mean actual_chborn if women_2135==1 & actual_chborn >1 & (marst==1 | marst==2)
sum actual_chborn if women_2135==1 & actual_chborn >2 & (marst==1 | marst==2)
sum workedyr if women_2135==1 & workedyr==3 & actual_chborn >1 & (marst==1 | marst==2)
tabulate women_2135 if actual_chborn >1 & (marst==1 | marst==2)


//////////////////////////////// Table 2 //////////////////////////////////////////

* Women aged 21-35 with 2 or more children 
cap drop women_2135_2ormore
generate women_2135_2ormore = 0
replace women_2135_2ormore = 1 if women_2135==1 & actual_chborn > 1 & actual_chborn==nchild & eldch < 18 & age2 >=1 
tabulate women_2135_2ormore

mean actual_chborn if women_2135_2ormore == 1
sum women_2135_2ormore if women_2135_2ormore == 1 & actual_chborn > 2
sum women_2135_2ormore if women_2135_2ormore == 1 & gender1 == 1
sum women_2135_2ormore if women_2135_2ormore == 1 & gender2 == 1
sum women_2135_2ormore if women_2135_2ormore==1 & gender1 == 1 & gender2 == 1
sum women_2135_2ormore if women_2135_2ormore==1 & gender1 == 2 & gender2 == 2  
sum women_2135_2ormore if women_2135_2ormore==1 & gender1 == gender2 
sum women_2135_2ormore if women_2135_2ormore==1 & age2 == age3
summarize age if women_2135_2ormore==1 

* Age at first birth 
cap drop age1stborn
generate age1stborn=age-age1
summarize age1stborn if women_2135_2ormore == 1 

* Setting weeks worked, hours/week, labour income to zero, if worked for pay last year = 0
replace wkswork1 = 0 if workedyr != 3
replace uhrswork = 0 if workedyr != 3
replace incwage = 0 if workedyr != 3
replace ftotinc = 0 if workedyr != 3

* Wage adjusted for inflation
generate incwage_inflated = incwage*1.18
generate ftotinc_inflated = ftotinc*1.18

* Employment and earnings info for women
summarize workedyr if women_2135_2ormore==1 & workedyr == 3
summarize wkswork1 if women_2135_2ormore==1 
summarize uhrswork if women_2135_2ormore==1
summarize incwage_inflated if women_2135_2ormore==1 
summarize ftotinc_inflated if women_2135_2ormore==1 & workedyr==3


* Married women aged 21-35 with 2 or more children 

cap drop married_women_2ormore
gen married_women_2ormore = 0
replace married_women_2ormore = 1 if women_2135_2ormore==1 & (marst==1 | marst==2)
tabulate married_women_2ormore

summarize actual_chborn if married_women_2ormore
summarize actual_chborn if married_women_2ormore == 1 & actual_chborn > 2
summarize actual_chborn if married_women_2ormore == 1 & gender1 == 1
summarize actual_chborn if married_women_2ormore == 1 & gender2 == 1
summarize actual_chborn if married_women_2ormore == 1 & gender1 == 1 & gender2 == 1
summarize actual_chborn if married_women_2ormore == 1 & gender1 == 2 & gender2 == 2
summarize actual_chborn if married_women_2ormore == 1 & gender1 == gender2 
summarize actual_chborn if married_women_2ormore == 1 & age2 == age3

summarize age if married_women_2ormore == 1
summarize age1stborn if married_women_2ormore == 1
summarize workedyr if married_women_2ormore == 1 & workedyr==3
summarize wkswork1 if married_women_2ormore == 1
summarize uhrswork if married_women_2ormore == 1 
summarize incwage_inflated if married_women_2ormore == 1 
summarize ftotinc_inflated if married_women_2ormore == 1 & workedyr==3


* Husbands 
cap drop husband 
generate husband = 1 if (marst==1 | marst==2) & sex == 2 & sploc[_n+sploc-pernum] == pernum & serial[_n+sploc-pernum] == serial 

cap drop husband_sample
generate husband_sample = 1 if husband == 1 & married_women_2ormore == 1

generate husband_age = age[_n+sploc-pernum] if sex == 2 & sploc[_n+sploc-pernum] == pernum & serial[_n+sploc-pernum] == serial 

sum husband_age if husband_sample == 1
generate age1stbornhusband = husband_age - age1
sum age1stbornhusband if married_women_2ormore == 1 & (marst == 1 | marst == 2)

cap drop husband_workforpay
gen husband_workforpay = workedyr[_n+sploc-pernum] if sex == 2 & sploc[_n+sploc-pernum] == pernum & serial[_n+sploc-pernum] == serial 
sum husband_workforpay if husband_sample == 1 & workedyr == 3

gen husband_wkswork = wkswork1[_n+sploc-pernum] if sex == 2 & sploc[_n+sploc-pernum] == pernum & serial[_n+sploc-pernum] == serial 
sum husband_wkswork if husband_sample == 1 

gen husband_uhrswork = uhrswork[_n+sploc-pernum] if sex == 2 & sploc[_n+sploc-pernum] == pernum & serial[_n+sploc-pernum] == serial 
sum husband_uhrswork if husband_sample==1
 
gen husband_incwage = incwage[_n+sploc-pernum] if sex == 2 & sploc[_n+sploc-pernum] == pernum &serial[_n+sploc-pernum] == serial 
gen husband_incwage_adjusted = husband_incwage*1.18
sum husband_incwage_adjusted if husband_sample == 1 


//////////////////////////////// Table 3 //////////////////////////////////////////

* Women aged 21-35 with 1 or more children 
generate women_2135_1ormore = 0
replace women_2135_1ormore = 1 if women_2135==1 & actual_chborn >= 1 & actual_chborn==nchild & age2 >=1 & eldch < 18 

sum women_2135_1ormore if women_2135_1ormore == 1 & gender1 == 2
sum women_2135_1ormore if women_2135_1ormore == 1 & gender1 == 2 & age2 !=.
sum women_2135_1ormore if women_2135_1ormore == 1 & gender1 == 1
sum women_2135_1ormore if women_2135_1ormore == 1 & gender1 == 1 & age2 !=.
tabulate women_2135_1ormore


* Married women aged 21-35 with 1 or more children 
generate married_women_2135_1ormore = 0
replace married_women_2135_1ormore = 1 if women_2135==1 & actual_chborn >= 1 & actual_chborn==nchild & age2 >=1 & eldch < 18 & (marst==1 | marst==2)

sum married_women_2135_1ormore if married_women_2135_1ormore == 1 & gender1 == 2
sum married_women_2135_1ormore if married_women_2135_1ormore == 1 & gender1 == 2 & age2 !=.
sum married_women_2135_1ormore if married_women_2135_1ormore == 1 & gender1 == 1
sum married_women_2135_1ormore if married_women_2135_1ormore == 1 & gender1 == 1 & age2 !=.
tabulate women_2135_1ormore


* Women aged 21-35 with 2 or more children
sum women_2135_2ormore if women_2135_2ormore == 1 & gender1 != gender2
sum women_2135_2ormore if women_2135_2ormore == 1 & gender1 == 2 & gender2 == 2
sum women_2135_2ormore if women_2135_2ormore == 1 & gender1 == 1 & gender2 == 1
sum women_2135_2ormore if women_2135_2ormore == 1 & gender1 != gender2 
sum women_2135_2ormore if women_2135_2ormore == 1 & gender1 == gender2 
tabulate women_2135_2ormore


* Married women aged 21-35 with 2 or more children 
sum married_women_2ormore if married_women_2ormore == 1 & gender1 != gender2
sum married_women_2ormore if married_women_2ormore == 1 & gender1 == 2 & gender2 == 2
sum married_women_2ormore if married_women_2ormore == 1 & gender1 == 1 & gender2 == 1
sum married_women_2ormore if married_women_2ormore == 1 & gender1 != gender2 
sum married_women_2ormore if married_women_2ormore == 1 & gender1 == gender2 
tabulate married_women_2ormore

//////////////////////////////// Table 4 //////////////////////////////////////////


cap drop women_age
generate women_age = .
replace women_age = age if women_2135_2ormore ==1 

cap drop same_sex
generate same_sex = 0 if women_2135_2ormore == 1 
replace same_sex = 1 if gender1 == gender2 & women_2135_2ormore == 1 
tabulate same_sex

regress age same_sex 

cap drop age1stborn
generate age1stborn = . 
replace age1stborn = age-age1 if women_2135_2ormore == 1 

regress age1stborn same_sex

cap drop women_black
generate women_black = 0 if women_2135_2ormore == 1 
replace women_black = 1 if women_2135_2ormore == 1 & race == 2
summarize women_black

regress women_black same_sex 


cap drop women_white
generate women_white = 0 if women_2135_2ormore == 1  
replace women_white = 1 if women_2135_2ormore == 1 & race == 1
summarize women_white

regress women_white same_sex 


cap drop women_other
generate women_other = 0 if women_2135_2ormore == 1 
replace women_other = 1 if women_2135_2ormore == 1 & race != 1 & race != 2
summarize women_other

regress women_other same_sex 


cap drop women_hispanic
generate women_hispanic = 0 if women_2135_2ormore == 1 
replace women_hispanic = 1 if women_2135_2ormore == 1 & hispan != 0
summarize women_hispanic

regress women_hispanic same_sex 

reg educ same_sex 


//////////////////////////////// Table 5 //////////////////////////////////////////

ssc install ivreg2
ssc install ranktest 

help ivregress2
help ivregress

*** Mean difference

cap drop morethan2
generate morethan2 = 0 if women_2135_2ormore == 1
replace morethan2 = 1 women_2135_2ormore == 1 & actual_chborn > 2

reg morethan2 same_sex 
reg actual_chborn same_sex

cap drop workedforpay
generate workedforpay = 0 if women_2135_2ormore == 1
replace workedforpay = 1 if women_2135_2ormore == 1 & workedyr==3
reg workedforpay same_sex

cap drop weeks_worked
generate weeks_worked = 0 if women_2135_2ormore == 1
replace weeks_worked = wkswork1 if women_2135_2ormore == 1
reg weeks_worked same_sex

cap drop hours_week
generate hours_week = 0 if women_2135_2ormore == 1
replace hours_week = uhrswork if women_2135_2ormore == 1
reg hours_week same_sex

cap drop labour_income
generate labour_income = 0 if women_2135_2ormore == 1
replace labour_income = incwage_inflated if women_2135_2ormore == 1
reg labour_income same_sex

cap drop family_income
generate family_income = 0 if women_2135_2ormore == 1
replace family_income = ftotinc_inflated if women_2135_2ormore == 1
reg family_income same_sex

*** Wald Estimate

ivreg2 workedforpay (morethan2 = same_sex) if women_2135_2ormore == 1

ivreg2 weeks_worked (morethan2 = same_sex) if women_2135_2ormore == 1

ivreg2 uhrswork (morethan2 = same_sex) if women_2135_2ormore == 1

ivreg2 incwage_inflated (morethan2 = same_sex) if women_2135_2ormore == 1

ivreg2 ftotinc_inflated (morethan2 = same_sex) if women_2135_2ormore == 1


//////////////////////////////// Table 8 //////////////////////////////////////////

cap drop first_boy
generate first_boy = 0 if women_2135_2ormore == 1
replace first_boy = 1 if women_2135_2ormore == 1 & gender1 == 1
tabulate first_boy

generate second_boy = 0 if women_2135_2ormore == 1
replace second_boy = 1 if women_2135_2ormore == 1 & gender2 == 1
tabulate second_boy

ivreg2 workedforpay (morethan2 = same_sex) age age1stborn first_boy second_boy women_black women_other, ffirst robust

ivreg2 wkswork1 (morethan2 = same_sex) age age1stborn first_boy second_boy women_black women_hispanic, ffirst robust

ivreg2 uhrswork (morethan2 = same_sex) age age1stborn first_boy second_boy women_black women_hispanic, ffirst robust

ivreg2 incwage_inflated (morethan2 = same_sex) age age1stborn first_boy second_boy women_black women_hispanic, ffirst robust

ivreg2 ftotinc_inflated (morethan2 = same_sex) age age1stborn first_boy second_boy women_black women_hispanic, ffirst robust

