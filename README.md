# cs001

在官網的Blazor EF Core 不僅示範了 EF Core,還完整的以 Contact 連繫人做一個增刪改查的APP,其中查詢部份包括了篩選排序和分頁。
針對查詢的部份,按照原範例, 擴展做法, 可以快速在給定的 DbContext 和 Entity 自動化建立查詢頁面, 具有一致的風格和功能。

- 最多八個文字欄位的篩選
- 兩組所有顯示欄位的排序
- 每頁1-100筆可選的分頁



##REF
- [ASP.NET Core Blazor Server with Entity Framework Core (EFCore)](https://docs.microsoft.com/en-us/aspnet/core/blazor/blazor-server-ef-core?view=aspnetcore-5.0)
- [Sample app](https://github.com/dotnet/AspNetCore.Docs/tree/master/aspnetcore/blazor/common/samples/5.x/BlazorServerEFCoreSample)
- [Blazor lifecycle](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/lifecycle?view=aspnetcore-5.00)
- [Base Class](https://docs.microsoft.com/en-us/aspnet/core/blazor/components/?view=aspnetcore-5.0)
