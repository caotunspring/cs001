# cs001

> 如何經濟有效節約人工維護代碼達到對給定數據庫查詢的功能


在官網的Blazor EF Core 不僅示範了 EF Core,還完整的以 Contact 連繫人做一個增刪改查的APP,其中查詢部份包括了篩選排序和分頁。
針對查詢的部份,按照原範例, 擴展做法, 可以快速在給定的 DbContext 和 Entity 自動化建立查詢頁面, 具有一致的風格和功能。

- 最多八個文字欄位的篩選
- 兩組所有顯示欄位的排序
- 每頁1-100筆可選的分頁

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





##REF
- [ASP.NET Core Blazor Server with Entity Framework Core (EFCore)](https://docs.microsoft.com/en-us/aspnet/core/blazor/blazor-server-ef-core?view=aspnetcore-5.0)
- [Sample app](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/blazor/common/samples/5.x/BlazorServerEFCoreSample)
- [Blazor lifecycle](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/lifecycle?view=aspnetcore-5.00)
- [Base Class](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/?view=aspnetcore-5.0)
- [DI|相依性插入|依赖关系注入](https://docs.microsoft.com/en-us/aspnet/core/blazor/fundamentals/dependency-injection?view=aspnetcore-5.0&pivots=webassembly)
