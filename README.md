# Caotun Spring 草屯春分

> 2020年年未冬天在草屯渡過,保持程序開發和跑步的兩者平衡,2021節氣春分開啟新的氣息,以此為記!

> 如何經濟有效, 節約人工維護代碼, 實現在 Blazor 數據庫查詢頁面可以透過參數調試完成。

也就是說, 開發分成兩段。
第一段是編程人員可以使用封裝好的 package 快速建立功能風格一致的查詢APP。
第二段是可以直接以 JSON 檔案使用參數來完成頁面內容的取捨設計。

官網的範例示範了在 Blazor 不同生命周期階段的代碼寫入。

我所做的封裝打包, 給編程人員便利使用, 不必分心去做和底層對接的事。

## 三個層次
- 所有獲得數據的方法全部封裝打包
- 編程人員可以看到獲得數據的過程
- 編程人員可以看到封裝的細節

在官網的Blazor EF Core 不僅示範了 EF Core,還完整的以 Contact 連繫人做一個增刪改查的APP,其中查詢部份包括了篩選排序和分頁。
針對查詢的部份,按照原範例, 擴展做法, 可以快速在給定的 DbContext 和 Entity 自動化建立查詢頁面, 具有一致的風格和功能。

- 最多八個文字欄位的篩選
- 兩組所有顯示欄位的排序
- 每頁1-100筆可選的分頁

## 三個例子
- CS00１ 官網範例, 單一一個 Contact
- CS002 貿易公司銷售和產品物料
- CS003 倉儲項目所使用的表單和視圖


## 參數調試
每頁的篩選排序都有各應對的JSON檔案可以進行參數調試, 包括
- 顯示的欄位, 順序, 欄位顯示名
- 特定的格式, 例如數字靠右具有千逗號等

## 封組
每頁共同通用的部份,寫在 Base Class,各頁繼承後, 專注在各自頁面即可


### HTML Markup 部份
以 Wrapper 包括三個元件, 分別是(1)篩選排序填入選擇(2)當頁的內容(3)分頁顯示

### CS 部份
- DI 獨用的 Adapter
- 指定要顯示的 Table/View 的 Entity
- 初值化
- 在適當的生命周期觸發數據更新


## AppCompBase
- 整個App 只要一個 Wrapper即可
- PageHelper 曾經放在Filters 裡,後來改放到和 Filter 同級別, 採用DI
- 根據學理和實做驗証, 每個 Blazor 頁面要用自己的 Adapter
  - 每一個Adapter 會各自實例出一個 Filters
    - 目前是在無參的 Constructor 實例化
    - 為了方便後續大量直接繼承, 不做有參的 Constructor, 也就不能使用 DI
  - 每頁的篩選排序分頁,操作起來就像是有記住在那裡
  - 混用或是不當實例化, 頁面操作會有兩個頁面糾纏不清或是永遠記不住之前狀態的缺失
- 必需要能訪問到 Data (DbContext) 和 Models (Entity Classes)
  - DbContext 的 Factory 是封裝在 base class 裡
  - Entity 是搭配 EF Core 及 Dynamic LINQ 使用
- Wrapper 等 components 以及 adapters 要先備好
  - Wrapper,IAdapter, PageHelper




##REF
- [ASP.NET Core Blazor Server with Entity Framework Core (EFCore)](https://docs.microsoft.com/en-us/aspnet/core/blazor/blazor-server-ef-core?view=aspnetcore-5.0)
- [Sample app](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/blazor/common/samples/5.x/BlazorServerEFCoreSample)
- [Blazor lifecycle](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/lifecycle?view=aspnetcore-5.00)
- [Base Class](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/?view=aspnetcore-5.0)
- [DI|相依性插入|依赖关系注入](https://docs.microsoft.com/en-us/aspnet/core/blazor/fundamentals/dependency-injection?view=aspnetcore-5.0&pivots=webassembly)
