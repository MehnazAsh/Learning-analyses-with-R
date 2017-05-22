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
  
ggpairs(data=litrecy_and_ageatmarriage,columns=c('Years','female_litrecy_rate','Age'),diag=list(continuous=wrap('barDiag',binwidth=5)))
  
ggplot(data=litrecy_and_ageatmarriage, aes(x=female_litrecy_rate,y=Age)) + 
geom_point(aes(color=Country,size=Years)) +
scale_y_continuous(breaks=seq(10,35,2)) +
scale_x_continuous(breaks=seq(0,100,5))+
xlab('%age of literate females aged 15 and above') +
ylab('Age at first marriage of females')   + geom_text(aes(label=Country)) +
geom_smooth(method='lm', formula=y~x)

with(litrecy_and_ageatmarriage,cor.test(female_litrecy_rate,Age))

Pearson's product-moment correlation

data:  female_litrecy_rate and Age
t = 5.2795, df = 51, p-value = 2.687e-06
alternative hypothesis: true correlation is not equal to 0
95 percent confidence interval:
 0.3862388 0.7450490
sample estimates:
     cor 
0.594471 
```
