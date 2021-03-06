## MongoDB介紹

Mongo的資料體結構是以 Key,Value組合的，儲存的方式與Json格式完全相同，另外多了很多的靈活性，也就每一筆文件的是欄位的型態是不一定的，欄位的存在性也是不一定的。如果你學過Relation DataBase一定會很困惑，因為MSSQL、MySQL教我們要先設定Table Schema後，明確定義Table的Column和其型態，有利於資料整理、資料存儲、並執行正規化的行為…等。

但在文本資料庫並沒有這樣子的限制，不過我認為雖然有這樣的彈性還是乖一點用Relation DataBase的設定概念來設計你的MongoDB資料庫。不然有一天一定天下大亂的。

### Monogo特色
1.MongoDB可以處理資料庫為 T級量 的資料庫，也就是處理大數據的資料庫。  

2.分散式的資料庫模式，可以把眾多資料庫串聯後處理大數的資料。  

### MongoDB的基本術語
```
Relation DataBase               MongoDB
--------------------------------------------------------------------------
資料庫(Database)                        DataBase(資料庫)
資料表(Table)                           Collection(集合)
資料(Record/Row)                        Document(資料)
欄位(Column)                            Field(欄位)
主索引(PK)                              _id
function                               function ( )
stored procedure                       mapreduce
--------------------------------------------------------------------------
```

資料結構：
Mongodb儲存資料的結構稱document，為一種JSON-like(field-value)組合的格式。
與一般關連式資料庫不同，Mongodb是一種無schema(綱要)的資料庫，它的結構是動態的。
如果你曾經使用Json來進行資料的操作，那對於這種field-value資料格式一定不陌生。

何謂field-value型式資料？ field-value型式資料就是一個欄位對應一個值的資料格式，




### MongoDB存儲資料格式
在MongoDB是以 Json 格式存儲資料的，也就是所謂的Document其內容如下  
id是索引(PK)，這一個欄位的值如果你沒有指定的話，系統會自動的生成；email這個欄位的值是一個Array型態可以儲存多筆子文件。  

```
{
     _id:"A001",
     name:"Canred",
     age:30,
     email:[
                   'canred.chen@gmail.com',
                   'canred.chen@ooo.com'
           ]
}
```
### MonogoDB 的須注意
1.使用64位版本或者理解32位版本的限制  

2.每個文件保持在16M以下  

3.如果必須要寫入確認，你可以使用安全寫入或getLastError  

4.設計結構模型並充分利用MongoDB的特色  [MongoDB 官方文檔](https://docs.mongodb.com/manual/data-modeling/)  

5.可以通過指定多個文件的multi為true來完成多文件修改  

```
db.people.update( {age: {$gt: 30}} , {$set: {past_it: true}}  , false, true)
```
同樣在官方的驅動中還有類似的選項—— ' multi '，也就是最後一個 true  

6.查詢是區分大小寫的，在犧牲速度的情況下可以利用正則表達式  

7.使用最新的穩定版本才能獲得最高的性能  

8.MongoDB不支持join：如果你想在多個Collection中檢索數據，那麼你必須做多次的查詢。  

如果你覺得你手動做的查詢太多了，你可以重設計你的數據模型來減少整體查詢的數量  

9.MongoDB的安全性可以通過使用防火牆和綁定正確的接口來保證，當然也可以開啟身份驗證。  

10.在Collection達到256G以前進行分片  

11.當用公網連接時，要注意和MongoDB的通信是未加密的  

12.MongoDB會消耗太多的磁盤空間 , epairDatabase與compact命令也會在一定程度上幫到  

[跳至首頁](https://donaldsher.github.io/LearningBlog/)
