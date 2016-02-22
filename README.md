# 22.Febrero.16
require(foreign)
sdem215<- read.dbf("C:\\Users\\SALA-C31\\Downloads\\sdemt215\\SDEMT215.dbf")##Abriendo base en dbf
sdem215<-data.frame(sdem215)###Hacemos la base de datos data frame
str(sdem215)

###Recodificar y etiquetar 
####Ponderar casos
install.packages("questionr")
require(questionr)
c0<-table(sdem215$SEX)
c0
c1<-wtd.table(sdem215$SEX, weights = sdem215$FAC)
table(c1)

###Porcentajes
tabrama<-wtd.table(sdem215$SEX, weights = sdem215$FAC)
c1.1<-round((tabrama/margin.table(tabrama))*100, 2)
c1.1
install.packages("XLConnect")
require(XLConnect)
library(XLConnect)
write.csv(c1.1, file='C:/Users/SALA-C31/Documents/Tablac1.1.csv')

sdem215$SEX<-ordered(sdem215$SEX, levels=c(1,2),labels=c("HOMBRES","MUJERES"))
View(sdem215$SEX)

### Ejercicio clase. Etiqueten la variable NAC_MES
table(NAC_MES)
NAC_MES<-as.numeric(as.character(NAC_MES))
sdem215$NAC_MES<-ordered(sdem215$NAC_MES,levels=c("01","02","03","04","05","06",
        "07","08","09","10","11","12","99"), 
        labels=c("ENERO","FEBRERO","MARZO","ABRIL","MAYO","JUNIO","JULIO","AGOSTO",
        "SEPTIEMBRE","OCTUBRE","NOVIEMBRE","DICIEMBRE","NO ESPECIFICADO"))
View(sdem215$NAC_MES)
table(sdem215$NAC_MES)
