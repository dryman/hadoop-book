Hadoop 以及大數據工程教學
======================

大數據近幾年成為顯學，坊間許多書籍鼓吹各種大數據的商機，以及各種運用大數據的成功故事。不過，實際上探討大數據技術的書籍相對較少，不是技術程度太淺，就是太過個案，難以做為個人學習教材之用。在台美大數據工程師（非資料科學家）的職缺非常多，但相關工程訓練在學校沒教，即使進業界，若非曾經待過資料團隊也無法學到相關技術與經驗。因此筆者發願要將自己在數據工程領域的所學，匯集成冊，替後進多增加一個自學資料工程的管道。期許能拋磚引玉，促進學習交流。

![big data](imgs/big-data2.jpg)


章節規劃
-------

坊間有很多大數據相關的書籍，不過往往把太多概念混在一起談。
本書對大數據工程的定義只有一個：**能撰寫及分析高言展性 (highly scalable) 程式的軟體工程**。
其他獨立的資料處理概念，諸如資料科學、資料視覺化、資料探勘、資料庫表單設計、資料彙集 (data ingestion) 等皆不屬於本書討論範圍。
事實上看到這些概念被隨意替換誤植，也是促使筆者開始寫這本書的動機之一；
因此開宗明義就要定義清楚大數據技術的範疇。

本書的章節會先專注在資料工程領域，以及此工程所需要的各種技術，從基本 (maven, eclipse) 到進階 (Hadoop API, deployment, performance tuning, etc.) 。 另外本書會用數種範例來介紹數據工程的眉眉角角，以及系統該如何規劃等等。
直到資料工程介紹完後，才會開始介紹處理大數據資料科學可用的演算法有哪些。
以大數據演算法如何設計為主體，去完成數種資料科學的任務。
傳統上的許多資料科學演算法都是 $O(N^2)$ ，但加入一些大數據演算法的巧思後，能達到 $O(N log(N))$ 或更佳的計算複雜度。
這是傳統資料科學較沒有討論的領域，但若沒有紮實的大數據工程訓練，
也難以將這類型演算法以高效能的方式實做。

由於筆者目前工作是以 Hadoop MapReduce framework 為主，
因此本書範例也會集中在使用這套 API ，而非目前最流行的 Spark。
若有心人願意補足 Spark 的範例，歡迎加入共同寫作！

<!-- * 大數據工程範疇分類及產業現況 -->
<!-- * 數據工程師的核心技能 -->
<!-- * 大數據系統hadoop生態系 -->
<!-- * 建立程式開發環境 -->
<!-- * 認識hadoop API -->
