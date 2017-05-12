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
