Rの基本的な使い方：作図編おかわり 191009 Ryosuke TAJIMA 
==============  
  
- [作図](#作図)  
- [さらに便利に使うために](#さらに便利に使うために)  
- [作図課題](#作図課題)  
  
# 作図
## 基本  
```R  
a<-c(1,3,5,6,12) #数字列
b<-c(2,7,3,16,11) #数字列
barplot(a) # 棒グラフ
plot(a,b) #散布図
plot(a,b, type="l") #線
plot(a,b, type="b") #点と線
plot(a,b, type="o") #点と線を重ねる
plot(a,b, col="red") #基本的な色はだいたいある．
plot(a,b, pch=0) #シンボルの形を変える
plot(a,b, pch=16) #16は便利
plot(a,b, cex=2) #サイズの変更
plot(a,b, type="o", col="red", pch=16, cex=2) #組み合わせられる
# 以下のように構造的に書くとヌケモレがなくなる
plot(a,b,
        type="o",
        col="red",
        pch=16,
        cex=2,
    )
```  

## 実際のデータで作成
```R  
d1<-read.table("Test1.txt", header=T)
sd5<-subset(d1,d1$Stage=="5week")  
sd8<-subset(d1,d1$Stage=="8week")  
plot(sd5$SDW,sd5$RDW, 
        xlim = c(0,1),  # x軸の境界
        ylim = c(0,0.5), # y軸の境界
        xlab = "ShootDW", # x軸ラベル
        ylab = "RootDW", # y軸ラベル
        col = "red",
        pch=16,
        cex=1.5,
    )
```  
## それなりの図
- 手書きに近い  
  
```R  
plot(sd5$SDW,sd5$RDW, 
        xlim = c(0,1),  # x軸の境界
        ylim = c(0,0.5), # y軸の境界
        xlab = "", # x軸ラベル
        ylab = "", # y軸ラベル
        col = "red",
        pch=16,
        cex=2,
        axes=F,
    )
axis(1, at=c(0,0.2,0.4,0.6,0.8,1.0), cex.axis=1.2, las=1, labels = T) # x軸目盛
axis(2, at=c(0,0.1,0.2,0.3,0.4,0.5), cex.axis=1.2, las=1, labels = T) # y軸目盛
mtext(1, text="ShootDW", adj=0.5, cex = 1.5, line = 2.5) # x軸ラベル
mtext(2, text="RootDW", adj=0.5, cex = 1.5, line = 2.5) #y軸ラベル
box("plot",lty=1,lwd=1) # 枠をつける
```  
  
## 図を重ねる
```R  
plot(sd5$SDW,sd5$RDW, 
        xlim = c(0,2.4),  # x軸の境界
        ylim = c(0,1.2), # y軸の境界
        xlab = "", # x軸ラベル
        ylab = "", # y軸ラベル
        col = "red",
        pch=16,
        cex=2,
        axes=F,
    )
par(new=TRUE) # デフォルトはFalseなので図は更新される
plot(sd8$SDW,sd8$RDW, 
        xlim = c(0,2.4),  # x軸の境界
        ylim = c(0,1.2), # y軸の境界
        xlab = "", # x軸ラベル
        ylab = "", # y軸ラベル
        col = "blue",
        pch=16,
        cex=2,
        axes=F,
    )
axis(1, at=c(0,0.6,1.2,1.8,2.4), cex.axis=1.2, las=1, labels = T) # X軸ラベル
axis(2, at=c(0,0.3,0.6,0.9,1.2), cex.axis=1.2, las=1, labels = T) # y軸ラベル
mtext(1, text="ShootDW", adj=0.5, cex = 1.5, line = 2.5)
mtext(2, text="RootDW", adj=0.5, cex = 1.5, line = 2.5)
box("plot",lty=1,lwd=1) # 枠をつける
```  

## 並べる

```R  
par(mfrow=c(1,2)) # c(行, 列)  
plot(sd5$SDW,sd5$RDW, 
        xlim = c(0,1.2),  # x軸の境界
        ylim = c(0,0.6), # y軸の境界
        xlab = "", # x軸ラベル
        ylab = "", # y軸ラベル
        col = "red",
        pch=16,
        cex=2,
        axes=F,
    )
axis(1, at=c(0,0.3,0.6,0.9,1.2), cex.axis=1.2, las=1, labels = T) # X軸ラベル
axis(2, at=c(0,0.2,0.4,0.6), cex.axis=1.2, las=1, labels = T) # y軸ラベル
mtext(1, text="ShootDW", adj=0.5, cex = 1.5, line = 2.5)
mtext(2, text="RootDW", adj=0.5, cex = 1.5, line = 2.5)
box("plot",lty=1,lwd=1) # 枠をつける


plot(sd8$SDW,sd8$RDW, 
        xlim = c(0,2.4),  # x軸の境界
        ylim = c(0,1.2), # y軸の境界
        xlab = "", # x軸ラベル
        ylab = "", # y軸ラベル
        col = "blue",
        pch=16,
        cex=2,
        axes=F,
    )
axis(1, at=c(0,0.6,1.2,1.8,2.4), cex.axis=1.2, las=1, labels = T) # X軸ラベル
axis(2, at=c(0,0.3,0.6,0.9,1.2), cex.axis=1.2, las=1, labels = T) # y軸ラベル
mtext(1, text="ShootDW", adj=0.5, cex = 1.5, line = 2.5)
mtext(2, text="RootDW", adj=0.5, cex = 1.5, line = 2.5)
box("plot",lty=1,lwd=1) # 枠をつける
```  

## 並べ方の工夫  
```R  
par(oma = c(2, 2, 2, 2)) # 下・左・上・右
par(mfrow=c(1,2)) # c(行, 列)  
par(mar = c(5, 5, 0, 0))  # 下・左・上・右
plot(sd5$SDW,sd5$RDW, 
        xlim = c(0,2.4),  # x軸の境界
        ylim = c(0,1.2), # y軸の境界
        xlab = "", # x軸ラベル
        ylab = "", # y軸ラベル
        col = "red",
        pch=16,
        cex=2,
        axes=F,
    )
axis(1, at=c(0,0.6,1.2,1.8,2.4), cex.axis=1.2, las=1, labels = T) # X軸ラベル
axis(2, at=c(0,0.3,0.6,0.9,1.2), cex.axis=1.2, las=1, labels = T) # y軸ラベル
# mtext(1, text="ShootDW", adj=0.5, cex = 1.5, line = 2.5)
mtext(2, text="RootDW", adj=0.5, cex = 1.5, line = 4)
box("plot",lty=1,lwd=1) # 枠をつける

par(mar = c(5, 0, 0, 5))  # 下・左・上・右
plot(sd8$SDW,sd8$RDW, 
        xlim = c(0,2.4),  # x軸の境界
        ylim = c(0,1.2), # y軸の境界
        xlab = "", # x軸ラベル
        ylab = "", # y軸ラベル
        col = "blue",
        pch=16,
        cex=2,
        axes=F,
    )
axis(1, at=c(0,0.6,1.2,1.8,2.4), cex.axis=1.2, las=1, labels = T) # X軸ラベル
# axis(2, at=c(0,0.3,0.6,0.9,1.2), cex.axis=1.2, las=1, labels = T) # y軸ラベル
# mtext(1, text="ShootDW", adj=0.5, cex = 1.5, line = 2.5)
# mtext(2, text="RootDW", adj=0.5, cex = 1.5, line = 2.5)
box("plot",lty=1,lwd=1) # 枠をつける
mtext("ShootDW",adj=0.5,side = 1, cex = 1.5, line = -1, outer=TRUE)

```  

## pdfで書き出す
###  基本

```R  
pdf("test.pdf", width=5, height=5)
a<-c(1,3,5,6,12)
b<-c(2,7,3,16,11)
plot(a,b,
        type="o",
        col="red",
        pch=16,
        cex=2,
    )
dev.off()
```  

###  実際
```R  
pdf("Fig.pdf", width=10, height=5)
par(oma = c(2, 2, 2, 2)) # 下・左・上・右

par(mfrow=c(1,2)) # c(行, 列)  
par(mar = c(5, 5, 0, 0))  # 下・左・上・右
plot(sd5$SDW,sd5$RDW, 
        xlim = c(0,2.4),  # x軸の境界
        ylim = c(0,1.2), # y軸の境界
        xlab = "", # x軸ラベル
        ylab = "", # y軸ラベル
        col = "red",
        pch=16,
        cex=2,
        axes=FALSE
    )
axis(1, at=c(0,0.6,1.2,1.8,2.4), cex.axis=1.2, las=1, labels = T) # X軸ラベル
axis(2, at=c(0,0.3,0.6,0.9,1.2), cex.axis=1.2, las=1, labels = T) # y軸ラベル
# mtext(1, text="ShootDW", adj=0.5, cex = 1.5, line = 2.5)
mtext(2, text="RootDW", adj=0.5, cex = 1.5, line = 4)
box("plot",lty=1,lwd=1) # 枠をつける

par(mar = c(5, 0, 0, 5))  # 下・左・上・右
plot(sd8$SDW,sd8$RDW, 
        xlim = c(0,2.4),  # x軸の境界
        ylim = c(0,1.2), # y軸の境界
        xlab = "", # x軸ラベル
        ylab = "", # y軸ラベル
        col = "blue",
        pch=16,
        cex=2,
        axes=FALSE
    )
axis(1, at=c(0,0.6,1.2,1.8,2.4), cex.axis=1.2, las=1, labels = T) # X軸ラベル
# axis(2, at=c(0,0.3,0.6,0.9,1.2), cex.axis=1.2, las=1, labels = T) # y軸ラベル
# mtext(1, text="ShootDW", adj=0.5, cex = 1.5, line = 2.5)
# mtext(2, text="RootDW", adj=0.5, cex = 1.5, line = 2.5)
box("plot",lty=1,lwd=1) # 枠をつける
mtext("ShootDW",adj=0.5,side = 1, cex = 1.5, line = -1, outer=TRUE)
dev.off()
```  

# さらに便利に使うために  
## コードはソースとして読むこともできる
- 細かな修正はこれを用いた方が便利  
```R  
source("Fig1.r")
```  

## 繰り返しや分岐の関数を利用する
### for  
```R  
d<-0
ld<-c()
for (i in 1:100) {
    d<-d+i
    ld<-c(ld,d)
}

```  

### forとifの組み合わせ  
```R  
ldo<-c()
lde<-c()
for (i in 1:100) {
    if (i%%2==0) {
        lde<-c(lde,i)
    } else {
        ldo<-c(ldo,i)
    }
}
```  

# 作図課題
  
- [Fig2](https://github.com/blukaniro/TrainingR191009/blob/master/Fig2.pdf)を作る
- [ソースコード](https://github.com/blukaniro/TrainingR191009/blob/master/Fig2.r)
- [for, ifを使わないソースコード](https://github.com/blukaniro/TrainingR191009/blob/master/Fig2long.r)



# おしまい．お疲れさまでした．