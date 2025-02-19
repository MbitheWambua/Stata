
cd "C:\Users\pwambua\Desktop\AM\Mbili Pamoja\Abstract"
clear
//Importing merged data

u ACASI_CAPI_Merged
drop if subject ==10200608

********************************************************************************
*TABLE 1.1
//Generating Kisumu and Nairobi as variables
gen Kisumu=0
replace Kisumu=1 if site ==1
gen Nairobi=0
replace Nairobi=1 if site ==2

//Age
sum calcage, det 
poisson calcage i.site, irr vce(r)

replace site=0 if site==2
replace mode=0 if mode==2

//Eucation
ta MP003pbi7 
gen Educ=0 if MP003pbi7<=3
replace Educ=1 if MP003pbi7>=4
la def Educ 0 "Incomplete secondary education" 1 "Secondary education and higher"
la values Educ Educ
ta Educ  site,chi
ta Educ  site,col
poisson Educ i.site, irr vce(r)

//Gender
ta MP003pbi4
codebook MP003pbi4
replace MP003pbi4=3 if MP003pbi4==4
ta MP003pbi4  site,chi
ta MP003pbi4  site,col

poisson MP003pbi4 i.site, irr vce(r)

//Employed
replace MP003pbi20=1 if MP003pbi20>0
ta MP003pbi20  site,col
poisson MP003pbi20 i.site, irr vce(r)

//Worried on whether food would run out
ta MP003pbi25  site,col
poisson MP003pbi25 i.site, irr vce(r)

//Antibiotics use
ta MP003pbi26  site,col
poisson MP003pbi26 i.site, irr vce(r)

//Receptive sex
ta MP003shi1  site,col
poisson MP003shi1 i.site, irr vce(r)

//Vaginal or anal sex with cisgender 
replace MP003shi3=0 if MP003shi3==8 | MP003shi3==.
ta MP003shi3  site,col
poisson MP003shi3 i.site, irr vce(r)

//Current boyfriend/partner
replace MP003spm3=0 if MP003spm3==9
ta MP003spm3  site,col
poisson MP003spm3 i.site, irr vce(r)

//Any female sex partner past one week
gen FemalePartner=0
replace FemalePartner=1 if MP003spf1!=99
la def FemalePartner 1 "Yes" 0 "No"
la values FemalePartner FemalePartner
ta FemalePartner  site,col
poisson FemalePartner i.site, irr vce(r)

//Given money or gifts by partner at last sex
replace MP003ras4=0 if MP003ras4==9
ta MP003ras4 site,col
poisson MP003ras4 i.site, irr vce(r)

//Penile discharge
ta MP003ass2  site,col
poisson MP003ass2 i.site, irr vce(r)

//Anal discharge
ta MP003ass3  site,col
poisson MP003ass3 i.site, irr vce(r)

**Dysuria
ta MP003ass6  site,col
poisson MP003ass6 i.site, irr vce(r)

**Currently taking PrEP
replace MP003pku3=0 if MP003pku3==9
ta MP003pku3  site,col
poisson MP003pku3 i.site, irr vce(r)

**PLWHIV
replace MP003hts2=0 if MP003hts2==9
ta MP003hts2 site,col
poisson MP003hts2 i.site, irr vce(r)

********************************************************************************
*TABLE 1.2
**Generating ACASI and CAPI as variables
gen ACASI=0
replace ACASI=1 if mode==1
gen CAPI=0
replace CAPI=1 if mode==2

*Age
sum calcage, det 

signrank calcage =mode 

poisson calcage i.mode, irr vce(r)

**Eucation
ta Educ  mode,col
poisson Educ i.mode, irr vce(r)

**Gender
ta MP003pbi4  mode,col
poisson MP003pbi4 i.mode, irr vce(r)

//Employed
ta MP003pbi20  site,col
poisson MP003pbi20 i.site, irr vce(r)


**Worried on whether food would run out
ta MP003pbi25  mode,col
poisson MP003pbi25 i.mode, irr vce(r)

**Antibiotics use
ta MP003pbi26  mode,col
poisson MP003pbi26 i.mode, irr vce(r)

**Receptive sex
ta MP003shi1  mode,col
poisson MP003shi1 i.mode, irr vce(r)

**Vaginal or anal sex with cisgender 
ta MP003shi3  mode,col
poisson MP003shi3 i.mode, irr vce(r)

**Current boyfriend/partner
ta MP003spm3  mode,col
poisson MP003spm3 i.mode, irr vce(r)

**Any female sex partner past one week
ta FemalePartner  mode,col
poisson FemalePartner i.mode, irr vce(r)

**Given money or gifts by partner at last sex
ta MP003ras4 mode,col
poisson MP003ras4 i.mode, irr vce(r)

**Penile discharge
ta MP003ass2  mode,col
poisson MP003ass2 i.mode, irr vce(r)

**Anal discharge
ta MP003ass3  mode,col
poisson MP003ass3 i.mode, irr vce(r)

**Dysuria
ta MP003ass6  mode,col
poisson MP003ass6 i.mode, irr vce(r)

**Currently taking PrEP
replace MP003pku3=0 if MP003pku3==9
ta MP003pku3  mode,col
poisson MP003pku3 i.mode, irr vce(r)

**PLWHIV
replace MP003hts2=0 if MP003hts2==9
ta MP003hts2  mode,col
poisson MP003hts2 i.mode, irr vce(r)

********************************************************************************
*TABLE 1.3
clear
u ACASI_CAPI_Merged
keep if site==1
//Age
sum calcage, det 
signrank calcage =mode 
poisson calcage i.mode, irr vce(r)

**Eucation
ta MP003pbi7 
gen Educ=0 if MP003pbi7<=3
replace Educ=1 if MP003pbi7>=4
la def Educ 0 "Incomplete secondary education" 1 "Secondary education and higher"
la values Educ Educ
ta Educ  mode,exact
ta Educ  mode,col
poisson Educ i.mode, irr vce(r)

**Gender
ta MP003pbi4
codebook MP003pbi4
replace MP003pbi4=3 if MP003pbi4==4
ta MP003pbi4  mode,chi
ta MP003pbi4  mode,col
poisson MP003pbi4 i.mode, irr vce(r)

//Employed
replace MP003pbi20=1 if MP003pbi20>0
ta MP003pbi20  mode,col
ta MP003pbi20  mode,exact

poisson MP003pbi20 i.mode, irr vce(r)

**Worried on whether food would run out
ta MP003pbi25  mode,col
ta MP003pbi25  mode,exact
poisson MP003pbi25 i.mode, irr vce(r)

**Antibiotics use
ta MP003pbi26  mode,col
ta MP003pbi26  mode,exact
poisson MP003pbi26 i.mode, irr vce(r)

**Receptive sex
ta MP003shi1  mode,col
ta MP003shi1  mode,exact
poisson MP003shi1 i.mode, irr vce(r)

**Vaginal or anal sex with cisgender
ta MP003shi3  mode,exact 
ta MP003shi3  mode,col
poisson MP003shi3 i.mode, irr vce(r)

**Current boyfriend/partner
replace MP003spm3=0 if MP003spm3==9
ta MP003spm3  mode,col
ta MP003spm3  mode,exact
poisson MP003spm3 i.mode, irr vce(r)

**Any female sex partner past one week
gen FemalePartner=0
replace FemalePartner=1 if MP003spf1!=99
la def FemalePartner 1 "Yes" 0 "No"
la values FemalePartner FemalePartner
ta FemalePartner  mode,col
ta FemalePartner  mode,exact
poisson FemalePartner i.mode, irr vce(r)

**Given money or gifts by partner at last sex
replace MP003ras4=0 if MP003ras4==9
ta MP003ras4 mode,col
ta MP003ras4 mode,chi
poisson MP003ras4 i.mode, irr vce(r)

**Penile discharge
ta MP003ass2  mode,col
ta MP003ass2  mode,exact
poisson MP003ass2 i.mode, irr vce(r)

**Anal discharge
ta MP003ass3  mode,col
ta MP003ass3  mode,exact
poisson MP003ass3 i.mode, irr vce(r)

**Dysuria
ta MP003ass6  mode,col
ta MP003ass6  mode,exact
poisson MP003ass6 i.mode, irr vce(r)

**Currently taking PrEP
replace MP003pku3=0 if MP003pku3==9
ta MP003pku3  mode,col
ta MP003pku3  mode,exact
poisson MP003pku3 i.mode, irr vce(r)

**PLWHIV
replace MP003hts2=0 if MP003hts2==9
ta MP003hts2  mode,col
ta MP003hts2  mode,exact
poisson MP003hts2 i.mode, irr vce(r)

********************************************************************************
*Urethral CT/NG/ Rectal

ta urethralctng mode ,col
ta rectalctng mode, col

ta urethralctng mode ,exact
ta rectalctng mode, exact

poisson urethralctng i.mode, irr vce(r)
poisson rectalctng i.mode, irr vce(r)

********************************************************************************
*PHQ9

foreach var in MP003phq1 MP003phq2 MP003phq93 MP003phq4 MP003phq5 MP003phq6 MP003phq7 MP003phq8 MP003phq9 {
    gen `var'_new = `var' - 1 if !missing(`var')
}

gen dep9m0 = (MP003phq2_new + MP003phq93_new + MP003phq4_new + MP003phq5_new + MP003phq6_new + MP003phq7_new + MP003phq8_new + MP003phq9_new)
label variable dep9m0 "PHQ-9 summary score for depression symptoms (range: 0-27)"

tab dep9m0, m

gen dep9catm0=dep9m0
recode dep9catm0 (0/4=0) (5/9=1) (10/14=2) (15/19=3) (20/27=4)

label variable dep9catm0 "PHQ-9 depression level-categorical"
label define dep9catr 0 "Minimal" 1 "Mild" 2 "Moderate" 3 "Moderately severe" 4 "Severe"
label values dep9catm0 dep9catr

gen phqdich=0 if dep9m0<5
replace phqdich=1 if dep9m0>=5&dep9m0~=.
label var phqdich "PHQ-9 dichotomized mild or more symptoms"
ta phqdich mode,col
ta phqdich mode,exact
poisson phqdich i.mode, irr vce(r)

********************************************************************************
**AUDIT
gen aud1r=MP003aud1
recode aud1r (8=.)
label variable aud1r "How often have a drink containing alcohol?"
label define audit1 0 "Never" 1 "Monthly or less" 2 "Two to four times a month-Monthly" 3 "Two to three times per week-Weekly" 4 "Four or more times a week-Daily/Almost daily"
label values aud1r audit1

********************************************************************************
//aud2-Typical-Typical quantity of drinking
//need to recode everything 
gen aud2r=HMP003aud2
recode aud2r (.=0) (1=0) (2=1) (3=2) (4=3) (5=4) (9=.)

label variable aud2r "How many drinks containing alcohol do you typically have when you drink?"
label define audit2 0 "Never/1-2 drinks" 1 "3-4 drinks" 2 "5-6 drinks" 3 "7-9 drinks" 4 "10+ drinks"
label values aud2r audit2

tab aud2r, m

********************************************************************************
//aud3-Frequency of heavy drinking
//need to recode .->0, replace the women who are No/0 for q146 to 0


gen aud3r=MP003aud3
recode aud3r (.=0) (9=.)

label variable aud3r "How often have 6+ drinks on one occasion-Heavy Drinking?"
label values aud3r audit1

tab aud3r, m

********************************************************************************
//aud4-Impaired control over drinking
//need to recode .-->0, replace the men who are No/0 for q146 to 0

gen aud4r=MP003aud4
recode aud4r (.=0) (9=.)
label variable aud4r "Not able to stop drinking when you start-Impaired control of drinking"
label values aud4r audit1

tab aud4r, m

********************************************************************************
//aud5-Increased salience of drinking
//need to recode .-->0, replace the women who are No/0 for q146 to 0
gen aud5r=MP003aud5
recode aud5r (.=0) (9=.)

label variable aud5r "Not do what is expected because of drinking-Salience of drinking"
label values aud5r audit1

tab aud5r, m

********************************************************************************
//aud6-Morning drinking
//need to recode .-->0, replace the women who are No/0 for q146 to 0
gen aud6r=MP003aud6
recode aud6r (.=0) (9=.)
label variable aud6r "Times needed a drink to get going in morning-Morning drinking"
label values aud6r audit1

tab aud6r, m

********************************************************************************
//aud7-Guilt after drinking
//need to recode .-->0, replace the women who are No/0 for q146 to 0

gen aud7r=FMP003aud7
recode aud7r (.=0) (9=.)
label variable aud7r "Times feeling guilt after drinking"
label values aud7r audit1

tab aud7r, m

********************************************************************************
//aud8-Blackouts
//need to recode .-->0, replace the women who are No/0 for q146 to 0

gen aud8r=aud8
recode aud8r (.=0) (9=.)
label variable aud8r "Unable to remember what happened because of drinking-Blackouts"
label values aud8r audit1

tab aud8r, m

********************************************************************************
//aud9-Alcohol-related injuries
//need to recode .-->0, replace the women who are No/0 for q146 to 0
//need to recode 1-->2, 2-->4
gen aud9r=MP003aud9
recode aud9r (.=0) (0=0) (1=2) (2=4) (9=.)
label variable aud9r "You/someone else been injured because of your drinking-Alcohol related injuries"
label define audit3 0 "No" 2 "Yes, but not in the last year" 4 "Yes, during the last year"
label values aud9r audit3

tab aud9r, m

********************************************************************************
//aud10-Others concerned about drinking
//need to recode .-->0, replace the women who are No/0 for q146 to 0
//need to recode 1-->2, 2-->4
gen aud10r=MP003aud10
recode aud10r (.=0) (0=0) (1=2) (2=4) (9=.)
label variable aud10r "Has anyone been concerned because of your drinking?"
label values aud10r audit3

tab aud10r, m

********************************************************************************
//raw sum total of AUDIT alcohol related questions

gen auditsum0 = (aud1r + aud2r + aud3r + aud4r + aud5r + aud6r + aud7r + aud8r + aud9r + aud10r)
label variable auditsum0 "Sum total of AUDIT questions (range: 0-40)"



********************************************************************************
//AUDIT cutpoints
//AUDIT cut-point 8--most sensitive
gen auditcut8m0=.
replace auditcut8m0 = 1 if auditsum0 >= 8 & auditsum0 != .
replace auditcut8m0 = 0 if auditsum0 <8

label variable auditcut8m0 "AUDIT score: >=8 vs <8"
label define auditcut8 1 "Hazardous/Harmful alcohol use" 0 "No harmful use"
replace auditcut8m0=0 if auditcut8m0==.
label values auditcut8m0 auditcut8

ta auditcut8m0 mode,col
ta auditcut8m0 mode,exact
poisson auditcut8m0 i.mode, irr vce(r)

********************************************************************************
*DAST
gen das4r=MP003das4
recode das4r(9=0)(8=.)
label variable das4r "Taken more than 1 drug at a time in past year?"
label values das4r yn

gen das5r=MP003das5
recode das5r(9=0)(8=.)
label variable das5r "Able to stop using drugs when want?"
label values das5r yn

gen das6r=MP003das6
recode das6r(9=0)(8=.)
label variable das6r "Blackouts or flashbacks?"
label values das6r yn

gen das7r=MP003das7
recode das7r(9=0)(8=.)
label variable das7r "Feel bad or guilty?"
label values das7r yn

gen das8r=MP003das8
recode das8r(9=0)(8=.)
label variable das8r "Complain about involvement in drugs?"
label values das8r yn

gen das9r=MP003das9
recode das9r(9=0)(8=.)
label variable das9r "Neglected family because of drugs?"
label values das9r yn

gen das10r=MP003das10
recode das10r(9=0) (8=.)
label variable das10r "Engaged in illegal activities?"
label values das10r yn

gen das11r	= MP003das11
recode das11r(9=0) (8=.)
label variable das11r "Experienced withdrawal symptoms?"
label values das11r yn

gen das12r= MP003das12
recode das12r(9=0) (8=.)
label variable das12r "Experienced medical problems?"
label values das12r yn

gen dastsum10 = das4r + das5r + das6r + das7r + das8r + das9r + das10r + das11r + das12r 
label var dastsum10 "BL DAST summary score (range: 0-10)"

gen dastdich3_10=1 if dastsum10>=3&dastsum10<=10
replace dastdich3_10=0 if dastsum10<3
label var dastdich3 "DAST 10-item, dich >=3 (moderate)"
label define dastdich3 0 "<3" 1 ">=3"
label values dastdich3 dastdich3

ta dastdich3 mode,col
ta dastdich3 mode,exact
poisson calcage i.mode, irr vce(r)

********************************************************************************
**Multivariable model
// antibiotic use
poisson  MP003pbi26 mode Educ calcage  MP003pbi20 MP003hts2  , irr vce(r)  
// rai
poisson  MP003shi1 mode Educ calcage  MP003pbi20 MP003hts2  , irr vce(r) 
// vaginal sex with cisgender
poisson  MP003shi3 mode Educ calcage  MP003pbi20 MP003hts2  , irr vce(r) 
// female partner
poisson  FemalePartner mode Educ calcage  MP003pbi20 MP003hts2  , irr vce(r) 
// age
poisson  calcage mode Educ   MP003pbi20 MP003hts2  , irr vce(r)  
// employed
poisson  MP003pbi20 mode Educ calcage   MP003hts2  , irr vce(r) 
// given money or gifts
poisson  MP003ras4 mode Educ calcage  MP003pbi20 MP003hts2  , irr vce(r) 

// phq9
poisson  phqdich mode Educ calcage  MP003pbi20 MP003hts2  , irr vce(r)  
// audit
poisson  auditcut8m0 mode Educ calcage  MP003pbi20 MP003hts2  , irr vce(r) 
// dast
poisson  dastdich3 mode Educ calcage  MP003pbi20 MP003hts2  , irr vce(r) 

/*
*Coefficient plots
label variable mode "CAPI VS ACASI"
*antibiotic
quietly poisson  MP003pbi26 mode Educ calcage  MP003pbi20 MP003hts2 if site==1, irr vce(r)  
estimates store MP003pbi26
*Rai
quietly poisson  MP003shi1 mode Educ calcage  MP003pbi20 MP003hts2 if site==1, irr vce(r) 
estimates store MP003shi1
*vaginal sex with cisgender
quietly poisson  MP003shi3 mode Educ calcage  MP003pbi20 MP003hts2 if site==1 , irr vce(r) 
estimates store MP003shi3
// female partner
quietly poisson  FemalePartner mode Educ calcage  MP003pbi20 MP003hts2 if site==1 , irr vce(r) 
estimates store FemalePartner
// age
quietly poisson  calcage mode Educ   MP003pbi20 MP003hts2 if site==1 , irr vce(r)
estimates store calcage  
// employed
quietly poisson  MP003pbi20 mode Educ calcage   MP003hts2 if site==1 , irr vce(r)
estimates store MP003pbi20  
// given money or gifts
quietly poisson  MP003ras4 mode Educ calcage  MP003pbi20 MP003hts2 if site==1 , irr vce(r)    
estimates store MP003ras4 

coefplot (MP003shi1,label("Receptive anal sex")) (MP003pbi26,label("Antibiotic use past 30 days")) (MP003shi3,label("Sex with cis-female")) (FemalePartner,label("Any female sex partner past one week")) (calcage,label("Age in years")) (MP003pbi20,label("Employed")) , drop(_cons Educ calcage MP003pbi20 MP003hts2) xline(1) eform xtitle(PRR) xscale(log) ylabel(, angle(vertical)) */
