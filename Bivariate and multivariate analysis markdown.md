```r
#read data from the excel file
female_litrecy<-read_excel('indicatorSE_ADT_LITR_FE_ZS.xls.xlsx')
colnames(female_litrecy)[1]<-"Country"
gatheredfemalelitrecy <- female_litrecy %>% 
gather(Years,female_litrecy_rate,-Country,na.rm = TRUE,convert=TRUE)
ggplot(data=gatheredfemalelitrecy,aes(x=Years,y=female_litrecy_rate))   +
geom_point(alpha=1,position = position_jitter(h=0), color='orange') +
geom_line(stat='summary',fun.y=mean) +
scale_x_continuous(breaks=seq(1975,2011,5)) +
scale_y_continuous(breaks=seq(0,100,10)) +
geom_text(aes(label=Country),check_overlap=TRUE)+ stat_smooth(method='lm', formula = y~x)
  
# now read another file which contains data for age at the time of first marriage in females, to a data frame 
ageofmarrigeinexcel<-read_excel("indicator age of marriage.xlsx")
# name the first column
colnames(ageofmarrigeinexcel)[1]<-"Country"
gatheredAgeDatafromExcel <- ageofmarrigeinexcel %>% gather(Years,Age,-Country,na.rm = TRUE,convert=TRUE)
ggplot(data=gatheredAgeDatafromExcel,aes(x=Years,y=Age))   +
geom_point(alpha=1,position = position_jitter(h=0), color='orange') +
geom_line(stat='summary',fun.y=mean) +
scale_x_continuous(breaks=seq(1600,2005,50)) +
scale_y_continuous(breaks=seq(10,40,2)) +
geom_text(aes(label=Country),check_overlap=TRUE) + stat_smooth(method='lm',formula=y~x)
  
  
##Merge the two data frame
litrecy_and_ageatmarriage<-inner_join(gatheredfemalelitrecy,gatheredAgeDatafromExcel,by=c('Country','Years'))
  
litrecy_and_ageatmarriage_grouped_by_Country<-litrecy_and_ageatmarriage %>% 
group_by(Country) %>%  
arrange(Country) %>% 
filter(n()>=2)
  
ggpairs(data=litrecy_and_ageatmarriage,columns=c('Years','female_litrecy_rate','Age'),diag=list(continuous=wrap('barDiag',binwidth=5)))
  
ggplot(data=litrecy_and_ageatmarriage_grouped_by_Country, aes(x=female_litrecy_rate,y=Age)) + 
geom_point(aes(color=Country,size=Years)) +
scale_y_continuous(breaks=seq(10,35,2)) +
scale_x_continuous(breaks=seq(0,100,5))+
xlab('%age of literate females aged 15 and above') +
ylab('Age at first marriage of females')   + geom_text(aes(label=Country)) +
geom_smooth(method='lm', formula=y~x)

with(litrecy_and_ageatmarriage_grouped_by_Country,cor.test(female_litrecy_rate,Age))


R version 3.2.1 (2015-06-18) -- "World-Famous Astronaut"
Copyright (C) 2015 The R Foundation for Statistical Computing
Platform: x86_64-apple-darwin10.8.0 (64-bit)

R is free software and comes with ABSOLUTELY NO WARRANTY.
You are welcome to redistribute it under certain conditions.
Type 'license()' or 'licence()' for distribution details.

  Natural language support but running in an English locale

R is a collaborative project with many contributors.
Type 'contributors()' for more information and
'citation()' on how to cite R or R packages in publications.

Type 'demo()' for some demos, 'help()' for on-line help, or
'help.start()' for an HTML browser interface to help.
Type 'q()' to quit R.

> povertyproportion_GDPperperson_waterresouces<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
Error: could not find function "inner_join"
> library("tidyr", lib.loc="/Library/Frameworks/R.framework/Versions/3.2/Resources/library")
Warning message:
package ‘tidyr’ was built under R version 3.2.5 
> povertyproportion_GDPperperson_waterresouces<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
Error: could not find function "inner_join"
> library("plyr", lib.loc="/Library/Frameworks/R.framework/Versions/3.2/Resources/library")
Warning message:
package ‘plyr’ was built under R version 3.2.5 
> library("ggplot2", lib.loc="/Library/Frameworks/R.framework/Versions/3.2/Resources/library")
> library("GGally", lib.loc="/Library/Frameworks/R.framework/Versions/3.2/Resources/library")
Warning messages:
1: replacing previous import by ‘utils::capture.output’ when loading ‘GGally’ 
2: replacing previous import by ‘utils::head’ when loading ‘GGally’ 
3: replacing previous import by ‘utils::installed.packages’ when loading ‘GGally’ 
4: replacing previous import by ‘utils::str’ when loading ‘GGally’ 
> povertyproportion_GDPperperson_waterresouces<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
Error: could not find function "inner_join"
> povertyproportion_GDPperperson_waterresouces<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
Error: could not find function "inner_join"
> library("dplyr", lib.loc="/Library/Frameworks/R.framework/Versions/3.2/Resources/library")

Attaching package: ‘dplyr’

The following object is masked from ‘package:GGally’:

    nasa

The following objects are masked from ‘package:plyr’:

    arrange, count, desc, failwith, id, mutate, rename, summarise, summarize

The following objects are masked from ‘package:stats’:

    filter, lag

The following objects are masked from ‘package:base’:

    intersect, setdiff, setequal, union

Warning message:
package ‘dplyr’ was built under R version 3.2.5 
> povertyproportion_GDPperperson_waterresouces<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
Error in inner_join(povertyproportion_GDPperperson, prop_people_using_imp_waterresouces_grouped_by_Country,  : 
  object 'povertyproportion_GDPperperson' not found
> povertyproportion_GDPperperson_waterresouces<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
Error in inner_join(povertyproportion_GDPperperson, prop_people_using_imp_waterresouces_grouped_by_Country,  : 
  object 'povertyproportion_GDPperperson' not found
> povertyproportion_GDPperperson_waterresouces<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
Error in inner_join(povertyproportion_GDPperperson, prop_people_using_imp_waterresouces_grouped_by_Country,  : 
  object 'povertyproportion_GDPperperson' not found
> povertyproportion_GDPperperson<-inner_join(proportionofpoorpeople_grouped_by_Country,gatheredincomeperperson_grouped_by_Country, by=c('Country','Years'))
Error in inner_join(proportionofpoorpeople_grouped_by_Country, gatheredincomeperperson_grouped_by_Country,  : 
  object 'proportionofpoorpeople_grouped_by_Country' not found
> povertyproportion_literacyrate<-inner_join(proportionofpoorpeople_grouped_by_Country,gatheredadultliteracyrate_grouped_by_Country,by=c('Country','Years'))
Error in inner_join(proportionofpoorpeople_grouped_by_Country, gatheredadultliteracyrate_grouped_by_Country,  : 
  object 'proportionofpoorpeople_grouped_by_Country' not found
> proportionofpoorpeople
Error: object 'proportionofpoorpeople' not found
> peoplebelowpovertyline<-read_excel('Indicator_Poverty headcount ratio at $1.25 a day (PPP) (% of population).xlsx')
Error: could not find function "read_excel"
> colnames(peoplebelowpovertyline)[which(names(peoplebelowpovertyline) == "Poverty headcount ratio at $1.25 a day (PPP) (% of population)")] <- "Country"
Error in colnames(peoplebelowpovertyline)[which(names(peoplebelowpovertyline) ==  : 
  object 'peoplebelowpovertyline' not found
> 
> proportionofpoorpeople <- peoplebelowpovertyline %>% gather(Years,Povertyratio,-Country,na.rm = TRUE,convert=TRUE)
Error in eval(expr, envir, enclos) : 
  object 'peoplebelowpovertyline' not found
> peoplebelowpovertyline<-read_excel('Indicator_Poverty headcount ratio at $1.25 a day (PPP) (% of population).xlsx')
Error: could not find function "read_excel"
> library("readxl", lib.loc="/Library/Frameworks/R.framework/Versions/3.2/Resources/library")
Warning message:
package ‘readxl’ was built under R version 3.2.4 
> peoplebelowpovertyline<-read_excel('Indicator_Poverty headcount ratio at $1.25 a day (PPP) (% of population).xlsx')
Error: 'Indicator_Poverty headcount ratio at $1.25 a day (PPP) (% of population).xlsx' does not exist in current working directory ('/Users/apple').
> colnames(peoplebelowpovertyline)[which(names(peoplebelowpovertyline) == "Poverty headcount ratio at $1.25 a day (PPP) (% of population)")] <- "Country"
Error in colnames(peoplebelowpovertyline)[which(names(peoplebelowpovertyline) ==  : 
  object 'peoplebelowpovertyline' not found
> 
> proportionofpoorpeople <- peoplebelowpovertyline %>% gather(Years,Povertyratio,-Country,na.rm = TRUE,convert=TRUE)
Error in eval(expr, envir, enclos) : 
  object 'peoplebelowpovertyline' not found
> peoplebelowpovertyline<-read_excel('Indicator_Poverty headcount ratio at $1.25 a day (PPP) (% of population).xlsx')
Error: 'Indicator_Poverty headcount ratio at $1.25 a day (PPP) (% of population).xlsx' does not exist in current working directory ('/Users/apple').
> setwd("/Users/apple/Documents/R programs")
> peoplebelowpovertyline<-read_excel('Indicator_Poverty headcount ratio at $1.25 a day (PPP) (% of population).xlsx')
> colnames(peoplebelowpovertyline)[which(names(peoplebelowpovertyline) == "Poverty headcount ratio at $1.25 a day (PPP) (% of population)")] <- "Country"
> 
> proportionofpoorpeople <- peoplebelowpovertyline %>% gather(Years,Povertyratio,-Country,na.rm = TRUE,convert=TRUE)
> proportionofpoorpeople_grouped_by_Country<-proportionofpoorpeople %>% 
+   group_by(Country) %>%  
+   arrange(Country) %>% 
+   filter(n()>=7)
> adultliteracyrate<-read_excel('indicator SE_ADT_LITR_ZS.xls.xlsx')
> colnames(adultliteracyrate)[which(names(adultliteracyrate) == "Adult (15+) literacy rate (%). Total")] <- "Country"
> 
> gatheredadultliteracyrate <- adultliteracyrate %>% gather(Years,Literacyrate,-Country,na.rm = TRUE,convert=TRUE)
> gatheredadultliteracyrate_grouped_by_Country<-gatheredadultliteracyrate %>% 
+   group_by(Country) %>%  
+   arrange(Country) %>% 
+   filter(n()>=5)
> incomeperperson<-read_excel('GDPpercapitaconstant2000US.xlsx')
> colnames(incomeperperson)[which(names(incomeperperson) == "Income per person (fixed 2000 US$)")] <- "Country"
> 
> gatheredincomeperperson<- incomeperperson %>% gather(Years,GDPpercapita,-Country,na.rm = TRUE,convert=TRUE)
> gatheredincomeperperson_grouped_by_Country<-gatheredincomeperperson %>% 
+   group_by(Country) %>%  
+   arrange(Country) %>% 
+   filter(n()>=2)
> people_using_imp_waterresouces<-read_excel('indicator improved water source % total.xls.xlsx')
> colnames(people_using_imp_waterresouces)[which(names(people_using_imp_waterresouces) == "Proportion of the population using improved drinking water sources, total")] <- "Country"
> prop_people_using_imp_waterresouces<- people_using_imp_waterresouces %>% gather(Years,proportion_using_improved_water_resouces,-Country,na.rm = TRUE,convert=TRUE)
> prop_people_using_imp_waterresouces_grouped_by_Country<-prop_people_using_imp_waterresouces %>% 
+   group_by(Country) %>%  
+   arrange(Country) %>% 
+   filter(n()>=2)
> prop_people_using_imp_waterresouces_grouped_by_Country_sample<-prop_people_using_imp_waterresouces_grouped_by_Country[sample(1:nrow(prop_people_using_imp_waterresouces_grouped_by_Country),500),]
> HDI<-read_excel('Indicator_HDI.xlsx')
> 
> View(HDI)
> colnames(HDI)[which(names(HDI) == "HDI")] <- "Country"
> 
> HDI<- HDI %>% gather(Years,HDI,-Country,na.rm = TRUE,convert=TRUE)
> povertyproportion_literacyrate<-inner_join(proportionofpoorpeople_grouped_by_Country,gatheredadultliteracyrate_grouped_by_Country,by=c('Country','Years'))
>   View(povertyproportion_literacyrate)
> ##poverty and HDI
> povertyproportion_HDI<-inner_join(proportionofpoorpeople_grouped_by_Country,HDI_grouped_by_Country,by=c('Country','Years'))
Error in is.data.frame(y) : object 'HDI_grouped_by_Country' not found
>   View(povertyproportion_HDI)
Error in View : object 'povertyproportion_HDI' not found
> ##poverty and water resources
> povertyproportion_proportionofpeopleusingwaterresources<-inner_join(proportionofpoorpeople_grouped_by_Country,prop_people_using_imp_waterresouces_grouped_by_Country,by=c('Country','Years'))
> View(povertyproportion_proportionofpeopleusingwaterresources)
> ##poverty and  GDP per person
> povertyproportion_GDPperperson<-inner_join(proportionofpoorpeople_grouped_by_Country,gatheredincomeperperson_grouped_by_Country, by=c('Country','Years'))
> View(povertyproportion_GDPperperson)
> HDI_grouped_by_Country<-HDI %>% 
+   group_by(Country) %>%  
+   arrange(Country) %>% 
+   filter(n()>=5)
> povertyproportion_literacyrate<-inner_join(proportionofpoorpeople_grouped_by_Country,gatheredadultliteracyrate_grouped_by_Country,by=c('Country','Years'))
> povertyproportion_HDI<-inner_join(proportionofpoorpeople_grouped_by_Country,HDI_grouped_by_Country,by=c('Country','Years'))
> povertyproportion_proportionofpeopleusingwaterresources<-inner_join(proportionofpoorpeople_grouped_by_Country,prop_people_using_imp_waterresouces_grouped_by_Country,by=c('Country','Years'))
> povertyproportion_GDPperperson<-inner_join(proportionofpoorpeople_grouped_by_Country,gatheredincomeperperson_grouped_by_Country, by=c('Country','Years'))
> povertyproportion_GDPperperson_waterresouces<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
> povertyproportion_GDPperperson_waterresouces<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
> View(povertyproportion_GDPperperson)
> View(povertyproportion_HDI)
> View(povertyproportion_literacyrate)
> povertyproportion_GDPperperson_waterresouces_HDI<-inner_join(povertyproportion_GDPperperson_waterresouces,HDI_grouped_by_Country, by=c('Country','Years'))
> View(povertyproportion_GDPperperson_waterresouces_HDI)
> povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate<-inner_join(povertyproportion_GDPperperson_waterresouces_HDI,gatheredadultliteracyrate_grouped_by_Country,by=c('Country','Years'))
> View(povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate)
> ggpairs(data=povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate,columns=c('Povertyratio','GDPpercapita','HDI','Literacyrate'),diag=list(continuous=wrap('barDiag',binwidth=5)))
                                                                                                          
> ggpairs(data=povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate,columns=c('Povertyratio','GDPpercapita','HDI','Literacyrate','proportion_using_improved_water_resources'),diag=list(continuous=wrap('barDiag',binwidth=5)))
Error in fix_column_values(data, columns, columnLabels, "columns", "columnLabels") : 
  Columns in 'columns' not found in data: c('proportion_using_improved_water_resources'). Choices: c('Country', 'Years', 'Povertyratio', 'GDPpercapita', 'proportion_using_improved_water_resouces', 'HDI', 'Literacyrate')
> ggpairs(data=povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate,columns=c('Povertyratio','GDPpercapita','HDI','Literacyrate','proportion_using_improved_water_resources'),diag=list(continuous=wrap('barDiag',binwidth=5)))
Error in fix_column_values(data, columns, columnLabels, "columns", "columnLabels") : 
  Columns in 'columns' not found in data: c('proportion_using_improved_water_resources'). Choices: c('Country', 'Years', 'Povertyratio', 'GDPpercapita', 'proportion_using_improved_water_resouces', 'HDI', 'Literacyrate')
> ggpairs(data=povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate,columns=c('Povertyratio','GDPpercapita','HDI','Literacyrate','proportion_using_improved_water_resources'))
Error in fix_column_values(data, columns, columnLabels, "columns", "columnLabels") : 
  Columns in 'columns' not found in data: c('proportion_using_improved_water_resources'). Choices: c('Country', 'Years', 'Povertyratio', 'GDPpercapita', 'proportion_using_improved_water_resouces', 'HDI', 'Literacyrate')
> ggpairs(data=povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate,columns=c('Povertyratio','GDPpercapita','HDI','Literacyrate','proportion_using_improved_water_resouces'))
                                                                                                          
> povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate.lm<-lm(data=povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate,Povertyratio~GDPpercapita)
> summary(povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate.lm)

Call:
lm(formula = Povertyratio ~ GDPpercapita, data = povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate)

Residuals:
   Min     1Q Median     3Q    Max 
-7.573 -4.314 -1.793  0.162 40.824 

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)  14.4776333  1.9989794   7.243 6.55e-09 ***
GDPpercapita -0.0017417  0.0004203  -4.144 0.000161 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 8.161 on 42 degrees of freedom
Multiple R-squared:  0.2902,	Adjusted R-squared:  0.2734 
F-statistic: 17.18 on 1 and 42 DF,  p-value: 0.0001614

> m1<-update(povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate.lm ,~.+HDI)
> summary(m1)

Call:
lm(formula = Povertyratio ~ GDPpercapita + HDI, data = povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate)

Residuals:
    Min      1Q  Median      3Q     Max 
-9.4490 -4.0218 -0.0733  2.2877 26.1425 

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)   8.133e+01  1.125e+01   7.228 7.87e-09 ***
GDPpercapita  5.997e-04  4.991e-04   1.202    0.236    
HDI          -1.113e+02  1.858e+01  -5.993 4.42e-07 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 6.031 on 41 degrees of freedom
Multiple R-squared:  0.6217,	Adjusted R-squared:  0.6032 
F-statistic: 33.69 on 2 and 41 DF,  p-value: 2.219e-09

> m2<-update(m1,~.+Literacyrate)
> summary(m2)

Call:
lm(formula = Povertyratio ~ GDPpercapita + HDI + Literacyrate, 
    data = povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate)

Residuals:
    Min      1Q  Median      3Q     Max 
-9.2114 -2.2539  0.0815  2.4543 18.5604 

Coefficients:
               Estimate Std. Error t value Pr(>|t|)    
(Intercept)   8.191e+01  1.002e+01   8.174 4.60e-10 ***
GDPpercapita  1.142e-03  4.719e-04   2.421  0.02011 *  
HDI          -1.735e+02  2.457e+01  -7.061 1.54e-08 ***
Literacyrate  4.488e-01  1.312e-01   3.421  0.00145 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 5.37 on 40 degrees of freedom
Multiple R-squared:  0.7073,	Adjusted R-squared:  0.6854 
F-statistic: 32.22 on 3 and 40 DF,  p-value: 9.282e-11

> m3<-update(m2,~.+proportion_using_improved_water_resouces)
> summary(m3)

Call:
lm(formula = Povertyratio ~ GDPpercapita + HDI + Literacyrate + 
    proportion_using_improved_water_resouces, data = povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate)

Residuals:
    Min      1Q  Median      3Q     Max 
-8.6683 -3.1471  0.2042  2.3286 12.6012 

Coefficients:
                                           Estimate Std. Error t value Pr(>|t|)    
(Intercept)                               1.260e+02  1.581e+01   7.969 1.04e-09 ***
GDPpercapita                              1.640e-03  4.454e-04   3.683 0.000698 ***
HDI                                      -1.455e+02  2.341e+01  -6.214 2.61e-07 ***
Literacyrate                              2.998e-01  1.249e-01   2.401 0.021214 *  
proportion_using_improved_water_resouces -5.680e-01  1.681e-01  -3.378 0.001666 ** 
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 4.783 on 39 degrees of freedom
Multiple R-squared:  0.7736,	Adjusted R-squared:  0.7504 
F-statistic: 33.31 on 4 and 39 DF,  p-value: 4.239e-12

> prop_people_using_imp_waterresouces<- people_using_imp_waterresouces %>% gather(Years,proportion_using_improved_water_resources,-Country,na.rm = TRUE,convert=TRUE)
> m3<-update(m2,~.+proportion_using_improved_water_resources)
Error in eval(expr, envir, enclos) : 
  object 'proportion_using_improved_water_resources' not found
> people_using_imp_waterresources<-read_excel('indicator improved water source % total.xls.xlsx')
> colnames(people_using_imp_waterresources)[which(names(people_using_imp_waterresources) == "Proportion of the population using improved drinking water sources, total")] <- "Country"
> prop_people_using_imp_waterresources<- people_using_imp_waterresources %>% gather(Years,proportion_using_improved_water_resources,-Country,na.rm = TRUE,convert=TRUE)
> prop_people_using_imp_waterresources_grouped_by_Country_sample<-prop_people_using_imp_waterresources_grouped_by_Country[sample(1:nrow(prop_people_using_imp_waterresources_grouped_by_Country),500),]
Error: object 'prop_people_using_imp_waterresources_grouped_by_Country' not found
> prop_people_using_imp_waterresources_grouped_by_Country<-prop_people_using_imp_waterresources %>% 
+   group_by(Country) %>%  
+   arrange(Country) %>% 
+   filter(n()>=2)
> prop_people_using_imp_waterresources_grouped_by_Country_sample<-prop_people_using_imp_waterresources_grouped_by_Country[sample(1:nrow(prop_people_using_imp_waterresources_grouped_by_Country),500),]
> povertyproportion_proportionofpeopleusingwaterresources<-inner_join(proportionofpoorpeople_grouped_by_Country,prop_people_using_imp_waterresources_grouped_by_Country,by=c('Country','Years'))
> povertyproportion_GDPperperson_waterresources<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresouces_grouped_by_Country, by=c('Country','Years'))
> povertyproportion_GDPperperson_waterresources_HDI<-inner_join(povertyproportion_GDPperperson_waterresources,HDI_grouped_by_Country, by=c('Country','Years'))
> povertyproportion_GDPperperson_waterresources_HDI_Literacyrate<-inner_join(povertyproportion_GDPperperson_waterresources_HDI,gatheredadultliteracyrate_grouped_by_Country,by=c('Country','Years'))
> ggpairs(data=povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate,columns=c('Povertyratio','GDPpercapita','HDI','Literacyrate','proportion_using_improved_water_resources'))
Error in fix_column_values(data, columns, columnLabels, "columns", "columnLabels") : 
  Columns in 'columns' not found in data: c('proportion_using_improved_water_resources'). Choices: c('Country', 'Years', 'Povertyratio', 'GDPpercapita', 'proportion_using_improved_water_resouces', 'HDI', 'Literacyrate')
> View(povertyproportion_GDPperperson_waterresouces_HDI_Literacyrate)
> povertyproportion_GDPperperson_waterresources<-inner_join(povertyproportion_GDPperperson,prop_people_using_imp_waterresources_grouped_by_Country, by=c('Country','Years'))
> povertyproportion_GDPperperson_waterresources_HDI<-inner_join(povertyproportion_GDPperperson_waterresources,HDI_grouped_by_Country, by=c('Country','Years'))
> povertyproportion_GDPperperson_waterresources_HDI_Literacyrate<-inner_join(povertyproportion_GDPperperson_waterresources_HDI,gatheredadultliteracyrate_grouped_by_Country,by=c('Country','Years'))
> ggpairs(data=povertyproportion_GDPperperson_waterresources_HDI_Literacyrate,columns=c('Povertyratio','GDPpercapita','HDI','Literacyrate','proportion_using_improved_water_resources'))
                                                                                                          
> povertyproportion_GDPperperson_waterresources_HDI_Literacyrate.lm<-lm(data=povertyproportion_GDPperperson_waterresources_HDI_Literacyrate,Povertyratio~GDPpercapita)
> m1<-update(povertyproportion_GDPperperson_waterresources_HDI_Literacyrate.lm ,~.+HDI)
> m1<-update(povertyproportion_GDPperperson_waterresources_HDI_Literacyrate.lm ,~.+HDI)
> m3<-update(m2,~.+proportion_using_improved_water_resources)
Error in eval(expr, envir, enclos) : 
  object 'proportion_using_improved_water_resources' not found
> View(povertyproportion_GDPperperson_waterresources_HDI_Literacyrate)
> m1<-update(povertyproportion_GDPperperson_waterresources_HDI_Literacyrate.lm ,~.+HDI)
> m2<-update(m1,~.+Literacyrate)
> m3<-update(m2,~.+proportion_using_improved_water_resources)
> ggplot(data=HDI_grouped_by_Country, aes(x=Years,y=HDI)) + 
+   geom_point() +
+   scale_y_continuous(breaks=seq(.1,1,.2)) +
+   scale_x_continuous(breaks=seq(1980,2011,10))+
+   xlab('Years') +
+   ylab('Human development indicator')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources<=quantile(proportion_using_improved_water_resources,0.50)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=CouIndicator_HDI.xlsxntry),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
Error in eval(expr, envir, enclos) : 
  object 'CouIndicator_HDI.xlsxntry' not found
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources<=quantile(proportion_using_improved_water_resources,0.50)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> View(prop_people_using_imp_waterresources_grouped_by_Country_sample)
> prop_people_using_imp_waterresources_grouped_by_Country_sample<-prop_people_using_imp_waterresources_grouped_by_Country[sample(1:nrow(prop_people_using_imp_waterresources_grouped_by_Country),200),]
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources<=quantile(proportion_using_improved_water_resources,0.50)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> prop_people_using_imp_waterresources_grouped_by_Country_sample<-prop_people_using_imp_waterresources_grouped_by_Country[sample(1:nrow(prop_people_using_imp_waterresources_grouped_by_Country),300),]
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources<=quantile(proportion_using_improved_water_resources,0.50)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample, aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.30)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.40)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.80)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.90)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.99)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>quantile(proportion_using_improved_water_resources,0.99)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>quantile(proportion_using_improved_water_resources,0.30)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>quantile(proportion_using_improved_water_resources,0.10)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.10)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources<quantile(proportion_using_improved_water_resources,0.10)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> summary(prop_people_using_imp_waterresources_grouped_by_Country_sample)
   Country              Years      proportion_using_improved_water_resources
 Length:300         Min.   :1990   Min.   : 15.00                           
 Class :character   1st Qu.:1996   1st Qu.: 73.00                           
 Mode  :character   Median :2000   Median : 90.00                           
                    Mean   :2000   Mean   : 82.73                           
                    3rd Qu.:2005   3rd Qu.: 98.00                           
                    Max.   :2010   Max.   :100.00                           
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>quantile(proportion_using_improved_water_resources,0.25)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.25)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.75)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>quantile(proportion_using_improved_water_resources,0.15)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources<quantile(proportion_using_improved_water_resources,0.15)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>quantile(proportion_using_improved_water_resources,0.15)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>quantile(proportion_using_improved_water_resources,0.50)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>quantile(proportion_using_improved_water_resources,0.30)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country_sample %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.25)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.25)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country %>% filter(proportion_using_improved_water_resources>=quantile(proportion_using_improved_water_resources,0.25)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point() +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country %>% filter(proportion_using_improved_water_resources<=quantile(proportion_using_improved_water_resources,0.95)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point() +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country %>% filter(proportion_using_improved_water_resources<quantile(proportion_using_improved_water_resources,0.98)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point() +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country %>% filter(proportion_using_improved_water_resources<quantile(proportion_using_improved_water_resources,0.90)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point() +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country %>% filter(proportion_using_improved_water_resources<quantile(proportion_using_improved_water_resources,0.80)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point() +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country %>% filter(proportion_using_improved_water_resources<quantile(proportion_using_improved_water_resources,0.70)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point() +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> ggplot(data=prop_people_using_imp_waterresources_grouped_by_Country %>% filter(proportion_using_improved_water_resources<quantile(proportion_using_improved_water_resources,0.50)), aes(x=Years,y=proportion_using_improved_water_resources)) + 
+   geom_point() +
+   scale_y_continuous(breaks=seq(2,100,5)) +
+   scale_x_continuous(breaks=seq(1990,2010,5))+
+   xlab('Years') +
+   ylab('Proportion of people using improved water resources')  + 
+   geom_text(aes(label=Country),check_overlap = TRUE) +
+   geom_smooth(method='lm', formula=y~x)
> summary(p2)
Error in summary(p2) : object 'p2' not found
> p2<-lm(data=litrecy_and_ageatmarriage_grouped_by_Country,female_litrecy_rate~Age )
Error in is.data.frame(data) : 
  object 'litrecy_and_ageatmarriage_grouped_by_Country' not found
> female_litrecy<-read_excel('indicatorSE_ADT_LITR_FE_ZS.xls.xlsx')
> source('~/Documents/R programs/Female litrecy vs female age at first marriage.R', echo=TRUE)

> setwd("/Users/apple/Documents/R programs")

> getwd()
[1] "/Users/apple/Documents/R programs"

> library(readxl)

> ?gather()

> female_litrecy<-read_excel('indicatorSE_ADT_LITR_FE_ZS.xls.xlsx')

> colnames(female_litrecy)[1]<-"Country"

> gatheredfemalelitrecy <- female_litrecy %>% gather(Years,female_litrecy_rate,-Country,na.rm = TRUE,convert=TRUE)

> View(gatheredfemalelitrecy)

> head(gatheredfemalelitrecy)
# A tibble: 6 x 3
               Country Years female_litrecy_rate
                 <chr> <dbl>               <dbl>
1         Burkina Faso  1975            3.182766
2 Central African Rep.  1975            8.399576
3               Kuwait  1975           48.015214
4               Turkey  1975           45.098921
5 United Arab Emirates  1975           38.124870
6              Uruguay  1975           94.304522

> ageofmarrigeinexcel<-read_excel("indicator age of marriage.xlsx")

> ## name the first column
> colnames(ageofmarrigeinexcel)[1]<-"Country"

> gatheredAgeDatafromExcel <- ageofmarrigeinexcel %>% gather(Years,Age,-Country,na.rm = TRUE,convert=TRUE)

> litrecy_and_ageatmarriage<-inner_join(gatheredfemalelitrecy,gatheredAgeDatafromExcel,by=c('Country','Years'))

> test<-gatheredAgeDatafromExcel %>% filter(Country %in% 'Burkina Faso')

> View(test)

> View(litrecy_and_ageatmarriage_grouped_by_Country)
Error in View : object 'litrecy_and_ageatmarriage_grouped_by_Country' not found

> litrecy_and_ageatmarriage_grouped_by_Country<-litrecy_and_ageatmarriage %>% 
+   group_by(Country) %>%  
+   arrange(Country) %>% 
+   filter(n()>=2 .... [TRUNCATED] 

> #the following plot shows that as the literacy rate of female increases , 
> #their age at the first marriage started increasing too.There is clearl .... [TRUNCATED] 

> ggsave('scatterplot of female literacy rate and age at the time of first marriage.jpeg')
Saving 7.62 x 6.83 in image

> dev.off()
null device 
          1 

> ?stat_smooth()

> ?geom_text()

> ##please note that the parameters to geom_smooth or stat_smooth shoyld be generelised formula and 
> #not the name of variables
> 
> 
> 
> View(gath .... [TRUNCATED] 

> #now lets plot individual plots 
> summary(gatheredAgeDatafromExcel$Years)
   Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
   1616    1950    1971    1962    2005    2005 

> gatheredAgeDatafromExcelfiltered<-gatheredAgeDatafromExcel %>% group_by(Country) %>% arrange(Country) %>% filter(n()>=10)

> ageatthefirstmarriage<-ggplot(data=gatheredAgeDatafromExcelfiltered 
+           %>% filter(Years>=quantile(Years,.5)), aes(x=Years,y=Age,color=Coun .... [TRUNCATED] 

> with(gatheredAgeDatafromExcelfiltered,cor.test(female_litrecy_rate,Years))
Error in cor.test(female_litrecy_rate, Years) : 
  object 'female_litrecy_rate' not found
> colnames(female_litrecy)[1]<-"Country"
> gatheredfemalelitrecy <- female_litrecy %>% gather(Years,female_litrecy_rate,-Country,na.rm = TRUE,convert=TRUE)
> ageofmarrigeinexcel<-read_excel("indicator age of marriage.xlsx")
> ## name the first column
> colnames(ageofmarrigeinexcel)[1]<-"Country"
> gatheredAgeDatafromExcel <- ageofmarrigeinexcel %>% gather(Years,Age,-Country,na.rm = TRUE,convert=TRUE)
> litrecy_and_ageatmarriage<-inner_join(gatheredfemalelitrecy,gatheredAgeDatafromExcel,by=c('Country','Years'))
> litrecy_and_ageatmarriage_grouped_by_Country<-litrecy_and_ageatmarriage %>% 
+   group_by(Country) %>%  
+   arrange(Country) %>% 
+   filter(n()>=2)
> ggplot(data=litrecy_and_ageatmarriage_grouped_by_Country, aes(x=female_litrecy_rate,y=Age)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(10,35,2)) +
+   scale_x_continuous(breaks=seq(0,100,5))+
+ xlab('%age of literate females aged 15 and above') +
+   ylab('Age at first marriage of females')   + geom_text(aes(label=Country)) +
+   geom_smooth(method='lm', formula=y~x)
> litrecy_and_ageatmarriage_grouped_by_Country<-litrecy_and_ageatmarriage %>% 
+   group_by(Country) %>%  
+   arrange(Country)
> ggplot(data=litrecy_and_ageatmarriage_grouped_by_Country, aes(x=female_litrecy_rate,y=Age)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(10,35,2)) +
+   scale_x_continuous(breaks=seq(0,100,5))+
+ xlab('%age of literate females aged 15 and above') +
+   ylab('Age at first marriage of females')   + geom_text(aes(label=Country)) +
+   geom_smooth(method='lm', formula=y~x)
> gatheredAgeDatafromExcelfiltered<-gatheredAgeDatafromExcel %>% group_by(Country) %>% arrange(Country) %>% filter(n()>=10)
> ageatthefirstmarriage<-ggplot(data=gatheredAgeDatafromExcelfiltered 
+           %>% filter(Years>=quantile(Years,.5)), aes(x=Years,y=Age,color=Country)) +
+   scale_color_discrete(guide=FALSE) +
+   geom_point() + geom_line() + geom_smooth(method='lm', formula=y~x)
> ageatthefirstmarriage
> m2<-lm(data=litrecy_and_ageatmarriage_grouped_by_Country,female_litrecy_rate~Age)
> p2<-lm(data=litrecy_and_ageatmarriage_grouped_by_Country,female_litrecy_rate~Age )
> summary(p2)

Call:
lm(formula = female_litrecy_rate ~ Age, data = litrecy_and_ageatmarriage_grouped_by_Country)

Residuals:
    Min      1Q  Median      3Q     Max 
-47.545 -20.735  -3.359  21.140  52.330 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)   -79.49      26.11  -3.044  0.00368 ** 
Age             6.23       1.18   5.280 2.69e-06 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 23.85 on 51 degrees of freedom
Multiple R-squared:  0.3534,	Adjusted R-squared:  0.3407 
F-statistic: 27.87 on 1 and 51 DF,  p-value: 2.687e-06

> ggplot(data=litrecy_and_ageatmarriage_grouped_by_Country, aes(x=female_litrecy_rate,y=Age)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(10,35,2)) +
+   scale_x_continuous(breaks=seq(0,100,5))+
+ xlab('%age of literate females aged 15 and above') +
+   ylab('Age at first marriage of females')   + geom_text(aes(label=Country)) +
+   geom_smooth(method='lm', formula=y~x)
> litrecy_and_ageatmarriage_grouped_by_Country<-litrecy_and_ageatmarriage %>% 
+   group_by(Country) %>%  
+   arrange(Country) %>% 
+   filter(n()>=2)
> #the following plot
> ggplot(data=litrecy_and_ageatmarriage_grouped_by_Country, aes(x=female_litrecy_rate,y=Age)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(10,35,2)) +
+   scale_x_continuous(breaks=seq(0,100,5))+
+ xlab('%age of literate females aged 15 and above') +
+   ylab('Age at first marriage of females')   + geom_text(aes(label=Country)) +
+   geom_smooth(method='lm', formula=y~x)
> with(litrecy_and_ageatmarriage_grouped_by_Country,cor.test(female_litrecy_rate,Age))

	Pearson's product-moment correlation

data:  female_litrecy_rate and Age
t = 2.5427, df = 19, p-value = 0.01986
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.09224804 0.76841539
sample estimates:
      cor 
0.5038696 

> litrecy_and_ageatmarriage_grouped_by_Country<-litrecy_and_ageatmarriage %>% 
+   group_by(Country) %>%  
+   arrange(Country)
> ggplot(data=litrecy_and_ageatmarriage_grouped_by_Country, aes(x=female_litrecy_rate,y=Age)) + 
+   geom_point(aes(color=Country,size=Years)) +
+   scale_y_continuous(breaks=seq(10,35,2)) +
+   scale_x_continuous(breaks=seq(0,100,5))+
+ xlab('%age of literate females aged 15 and above') +
+   ylab('Age at first marriage of females')   + geom_text(aes(label=Country)) +
+   geom_smooth(method='lm', formula=y~x)
> m2<-lm(data=litrecy_and_ageatmarriage_grouped_by_Country,female_litrecy_rate~Age)
> p1<-lm(data=litrecy_and_ageatmarriage_grouped_by_Country,female_litrecy_rate~Years)
> summary(p1)

Call:
lm(formula = female_litrecy_rate ~ Age, data = litrecy_and_ageatmarriage_grouped_by_Country)

Residuals:
    Min      1Q  Median      3Q     Max 
-47.545 -20.735  -3.359  21.140  52.330 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)   -79.49      26.11  -3.044  0.00368 ** 
Age             6.23       1.18   5.280 2.69e-06 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 23.85 on 51 degrees of freedom
Multiple R-squared:  0.3534,	Adjusted R-squared:  0.3407 
F-statistic: 27.87 on 1 and 51 DF,  p-value: 2.687e-06

> with(litrecy_and_ageatmarriage_grouped_by_Country,cor.test(female_litrecy_rate,Age))

	Pearson's product-moment correlation

data:  female_litrecy_rate and Age
t = 5.2795, df = 51, p-value = 2.687e-06
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.3862388 0.7450490
sample estimates:
     cor 
0.594471 

p1<-lm(data=litrecy_and_ageatmarriage_grouped_by_Country,female_litrecy_rate~Age )
summary(p1)

Call:
lm(formula = female_litrecy_rate ~ Age, data = litrecy_and_ageatmarriage_grouped_by_Country)

Residuals:
    Min      1Q  Median      3Q     Max 
-47.545 -20.735  -3.359  21.140  52.330 

Coefficients:
            Estimate Std. Error t value Pr(>|t|)    
(Intercept)   -79.49      26.11  -3.044  0.00368 ** 
Age             6.23       1.18   5.280 2.69e-06 ***
---
Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

Residual standard error: 23.85 on 51 degrees of freedom
Multiple R-squared:  0.3534,	Adjusted R-squared:  0.3407 
F-statistic: 27.87 on 1 and 51 DF,  p-value: 2.687e-06
```
