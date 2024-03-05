import pandas as pd
# 讀取資料
data=pd.read_csv("googleplaystore.csv.csv")
print("資料數量",data.shape)  #shape(欄,列)
print("資料欄位",data.columns)   #也就是資料的欄位名稱
# 分析資料(評分),# 確認是否有數值較突出的值
condition=data["Rating"]<=5
data=data[condition]
print("平均數",data["Rating"].mean())
print("中位數",data["Rating"].median())
print("取得前一千個應用程式最大值",data["Rating"].nlargest(1000).mean())
# 分析安裝數量的各種統計數據
print(data["installs"])
# 資料[installs]為非數值資料
# 去除一些怪異值符號
data["Installs"]=pd.to_numeric(data["Installs"].str.replace(r"[,+]","",regex=True).replace("Free",""))

# 再次查看installs的資料,確定還有無異常值
condition=data["Installs"]>100000
print("安裝數量大於100000的應用程式有幾個",data[condition].shape[0])
# 手動輸入遊戲關鍵字可查詢總數量
keyword=input("請輸入關鍵字:")
condition=data["App"].str.contains(keyword,case=False)
print("包含關鍵字的應用程式數量",data[condition].shape[0])


