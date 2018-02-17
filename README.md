# De-duplication
df1<-read.csv("Deduplication Problem - Sample Dataset.csv",stringsAsFactors = F)
df1$date<-format(as.Date(df1$dob,format="%d/%m/%y"),"%d")
df1$month<-format(as.Date(df1$dob,format="%d/%m/%y"),"%m")
df1$year<-format(as.Date(df1$dob,format="%d/%m/%y"),"%y")
df1$gn<-ifelse(as.factor(df1$gn)=="F",1,0)
df1$dob<-NULL
df2<-df1[c(2,4,5,6)]
df3<-vector()
df4<-0

df3<-df1[26,]
for(i in 1:103)
  {if((df3$date==df1[i,]$date)&&(df3$month==df1[i,]$month)&&(df3$year==df1[i,]$year) )
    if(df3$gn==df1[i,]$gn)
      if((1-stringdist(df3$ln,df1[i,]$ln,method="jw"))>0.7 &&
         (1-stringdist(df3$fn,df1[i,]$fn,method="jw"))>0.7)
      {  print(df1[i,])
        
      }
}
            
