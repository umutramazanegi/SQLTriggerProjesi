# SQLTriggerProjesi ⚙️ (SQL Server Trigger Demo Projesi)

Bu proje, **.NET Framework 4.7.2** üzerinde **C#** ile geliştirilmiş bir **Console uygulamasıdır**. Temel amacı, **SQL Server Triggerak için çok değerli. İşte bu `SQLTriggerProjesi` için detaylı bir GitHub README.md dosyası:

```markdown
# SQLTriggerProjesi 🚀

Bu proje, **.NET Framework 4.7.2** üzerinde **C#** ile geliştirilmiş bir **Console uygulamasıdır**. Temel amacı, **Microsoft SQL Server** veritabanında tanımlanmış **Trigger (Tetikleyici)** mekanizmalarının, **Entity Framework 6 (Database First)** aracılığıyla yapılan veri değişiklikleri (özellikle `INSERT` işlemleri) üzerindeki etkilerini canlı olarak göstermektir.

## 🚀 Genel Bakış

Uygulama, basit bir sipariş ve stok yönetim senaryosunu simüle eder. Ürünler (`TblProduct`), verilen siparişler (`TblOrder`), kasa bakiyesi (`TblCashRegister`) ve toplam işlem sayısı (`TblProcess`) gibi bilgileri içeren tablolarla çalışır. Konsol arayüzü üzerinden yeni bir sipariş oluşturulduğunda, SQL Server tarafında tanımlı olan Trigger'lar otomatik olarak devreye girer ve ilgili tablolarda (stok azaltma, kasa bakiyesini artırma, işlem sayacını artırma) gerekli güncellemeleri yapar.

Bu proje, özellikle veritabanı Trigger'larının uygulama katmanından bağımsız olarak nasıl çalıştığını ve Entity Framework gibi ORM'lerle yapılan işlemlerin bu Trigger'ları nasıl tetiklediğini anlamak için pratik bir örnektir.

## ✨ Özellikler ve Gösterilen Mekanizmalar

*   **Console Arayüzü:** Kullanıcıya basit bir menü sunarak veritabanı işlemlerini tetikleme imkanı sağlar:
    *   Ürünleri Listeleme
    *   Siparişleri Listeleme
    *   Kasa Bakiyesini Gösterme
    *   Yeni Ürün Satışı (Sipariş Oluşturma) - *Trigger'ların tetiklendiği ana nokta*
    *   İşlem Sayacını Gösterme
*   **Entity Framework 6 (Database First):** Var olan `SQLTriggerProjesiDB` veritabanı şemasından `.edmx` modeli oluşturulmuş ve veritabanı etkileşimleri bu model üzerinden (`SQLTriggerProjesiDBEntities`) sağlanmıştır.
*   **SQL Server Trigger Gösterimi:**
    *   **Stok Azaltma:** `TblOrder` tablosuna yeni bir kayıt eklendiğinde (`AFTER INSERT`), ilgili ürünün stoğu (`TblProduct.ProductStock`) otomatik olarak sipariş adedi kadar azalır.
    *   **Kasa Bakiyesini Artırma:** `TblOrder` tablosuna yeni bir kayıt eklendiğinde (`AFTER INSERT`), siparişin toplam tutarı (`TblOrder.TotalPrice`) otomatik olarak kasa bakiyesine (`TblCashRegister.Balance`) eklenir.
.  Satılan ürünün stoğunu düşürür (`TblProduct`).
2.  Kasa bakiyesini siparişin toplam tutarı kadar artırır (`TblCashRegister`).
3.  Genel işlem sayacını bir artırır (`TblProcess`).

Uygulama, bu işlemlerin sonucunu (güncel stok, kasa durumu, işlem sayısı) kullanıcıya göstererek Trigger'ların arka planda nasıl çalıştığını somutlaştırır.

## ✨ Gösterilen Temel Konseptler

*   **SQL Server Trigger'ları:**
    *   `AFTER INSERT` trigger kullanarak bir tabloya veri eklendikten sonra başka tabloları otomatik olarak güncelleme.
    *   `inserted` sanal tablosundan veri okuma.
    *   Basit stok düşme mantığı.
    *   Kasa toplamını güncelleme.
    *   İşlem sayacını artırma/azaltma (Örnek scriptlerde hem artırma hem azaltma trigger'ları mevcut).
*   **Entity Framework 6 (Database First):**
    *   Mevcut bir SQL Server veritabanından `.edmx` modeli oluşturma.
    *   `DbContext` ve Entity sınıfları üzerinden veritabanı işlemleri (`ToList()`, `FirstOrDefault()`, `Add()`, `SaveChanges()`).
    *   İlişkili veriye erişim (`item.TblProduct.ProductName`).
*   **.NET Console Uygulaması:**
    *   Basit menü sistemi.
    *   Kullanıcıdan veri alma (`Console.ReadLine()`).
    *   Veritabanından alınan verileri konsola yazdırma.

## 🛠️ Kullanılan Teknolojiler

*   **Programlama Dili:** C#
*   **Framework:** .NET Framework 4.7.2
*   **Uygulama Tipi:** Console Application
*   **Veri Erişimi:** Entity Framework 6 (Database First)
*   **Veritabanı:** Microsoft SQL Server
*   **Veritabanı Özelliği:** SQL Triggers

## 💾 Veritabanı Kurulumu (SQL Server)

Bu projenin çalışması için SQL Server'da ilgili veritabanının, tabloların ve **Trigger'ların** oluşturulması gerekmektedir.

1.  **Veritabanı Oluşturma:**
    *   SQL Server Management Studio (SSMS) veya başka bir araç kullanarak `SQLTriggerProjesiDB` adında yeni bir veritabanı oluşturun.
    *   *(Alternatif)*: Eğer veritabanı adı farklı olacaksa, `App.config` ve `.edmx` dosyalarındaki bağlantı bilgilerini güncellemeniz gerekir.

2.  **Tabloları Oluşturma:**
    *   `SQLTriggerProjesiDB` veritabanını seçin ve yeni bir sorgu (New Query) penceresi açın.
    *   Aşağıdaki SQL script'lerini çalıştırarak tabloları oluşturun:

    ```sql
    CREATE TABLE TblProduct (
        ProductId INT PRIMARY KEY IDENTITY(1,1),
        ProductName NVARCHAR(50),
        ProductPrice DECIMAL(18, **'larının nasıl çalıştığını ve Entity Framework (Database First) ile nasıl etkileşim kurabileceğini göstermektir. Basit bir sipariş ve stok yönetimi senaryosu üzerinden Trigger'ların otomatik etkileri sergilenmektedir.

## 🚀 Genel Bakış

Uygulama, Ürün (Product), Sipariş (Order), Kasa (CashRegister) ve İşlem Sayacı (Process) tablolarını içeren bir SQL Server veritabanı kullanır. Entity Framework 6 (Database First) yaklaşımıyla bu veritabanından model (`.edmx`) oluşturulmuştur. Projenin asıl odak noktası, `TblOrder` tablosuna yeni bir kayıt eklendiğinde veya silindiğinde (veya güncellendiğinde - trigger'lara bağlı olarak) otomatik olarak çalışan SQL Trigger'larıdır. Bu Trigger'lar, ürün stoğunu günceller, kasa bakiyesini ayarlar ve toplam işlem sayısını takip eder. Console uygulaması, bu işlemlerin yapılmasını sağlayan basit bir menü sunar.

## ✨ Öne Çıkan Konseptler

*   **SQL Server Trigger'ları:**
    *   `AFTER INSERT` Trigger'ı: Sipariş eklendiğinde stok düşürme ve kasa bakiyesini artırma.
    *   (Örnek olarak) `AFTER INSERT`/`AFTER DELETE` Trigger'ları: Sipariş eklendiğinde/silindiğinde işlem sayacını güncelleme.
*   **Entity Framework 6 (Database First):** Mevcut bir SQL Server veritabanından `.edmx` modeli oluşturma ve bu model üzerinden veri işlemleri (Listeleme, Ekleme) yapma.
*   **ADO.NET (Implicit):** Entity Framework arka planda ADO.NET kullanarak veritabanı ile iletişim kurar.
*   **Console Uygulaması:** Kullanıcıyla etkileşim için basit bir metin tabanlı menü sunar.

## 🛠️ Kullanılan Teknolojiler

*   **Programlama Dili:** C#
*   **Framework:** .NET Framework 4.7.2
*   **Uygulama Tipi:** Console Application
*   **Veri Erişimi:** Entity Framework 6 (Database First)
*   **Veritabanı:** Microsoft SQL Server
*   **Veritabanı Otomasyonu:** SQL Server Triggers

## 💾 Veritabanı Kurulumu (SQL Server)

Uygulamanın çalışması için bir SQL Server veritabanına ve ilgili tablolara **ve Trigger'lara** ihtiyaç vardır.

1.  **Veritabanı Oluşturma:**
    *   SQL Server Management Studio (SSMS) veya başka bir SQL Server aracı kullanarak `SQLTriggerProjesiDB` adında **yeni bir veritabanı** oluşturun.

2.  **Tabloları Oluşturma:**
    *   Oluşturduğunuz `SQLTriggerProjesiDB` veritabanını seçin ve yeni bir sorgu (New Query) penceresi açın.
    *   Aşağıdaki SQL script'ini çalıştırarak gerekli tabloları oluşturun:

    ```sql
    -- TblProduct Tablosu
    CREATE TABLE [dbo].[TblProduct](
        [ProductId] [int] IDENTITY(1,1) NOT NULL,
        [ProductName] [nvarchar](50) NULL,
        [ProductPrice] [decimal](18, 2) NULL,
        [ProductStock] [int] NULL,
        [ProductStatust] [bit] NULL, -- Not: Sütun adında 't' harfi fazla olabilir, C# modelinizle eşleştiğinden emin olun.
     CONSTRAINT [PK_TblProduct] PRIMARY KEY CLUSTERED ([ProductId] ASC)
    );
    GO

    -- TblOrder Tablosu
    CREATE TABLE [dbo].[TblOrder](
        [OrderId] [int] IDENTITY(1,1) NOT NULL,
        [Customer] [nvarchar](50) NULL,
        [ProductId] [int] NULL,
        [Quantity] [int] NULL,
        [UnitPrice] [decimal](18, 2) NULL,
        [TotalPrice] [decimal](18, 2) NULL,
     CONSTRAINT [PK_TblOrder] PRIMARY KEY CLUSTERED ([    *   **İşlem Sayacını Artırma/Azaltma:** `TblOrder` tablosuna kayıt eklendiğinde (`AFTER INSERT`) veya silindiğinde (`AFTER DELETE`), `TblProcess` tablosundaki sayaç otomatik olarak artar veya azalır.
*   **Doğrudan Veritabanı Etkileşimi:** Uygulama katmanında (C# kodu), sipariş ekleme işlemi sırasında stok düşürme, kasa güncelleme veya işlem sayacı artırma gibi *ekstra kodlar bulunmaz*. Bu işlemler tamamen SQL Server Trigger'ları tarafından halledilir.

## 🛠️ Kullanılan Teknolojiler

*   **Programlama Dili:** C#
*   **Framework:** .NET Framework 4.7.2
*   **Uygulama Tipi:** Console Application
*   **Veri Erişimi:** Entity Framework 6 (Database First)
*   **Veritabanı:** Microsoft SQL Server

## 💾 Veritabanı Kurulumu (SQL Server)

Bu projenin düzgün çalışabilmesi için SQL Server'da ilgili veritabanının, tabloların ve **Trigger'ların** oluşturulması gerekmektedir.

**1. SQL Server Kurulumu (Eğer kurulu değilse):**

*   Microsoft SQL Server'ın bir sürümünün (Express, Developer, Standard vb.) kurulu ve çalışır durumda olduğundan emin olun.

**2. Veritabanı Oluşturma:**

*   SQL Server Management Studio (SSMS) veya başka bir araç kullanarak sunucunuza bağlanın.
*   Aşağıdaki komutla `SQLTriggerProjesiDB` adında yeni bir veritabanı oluşturun:
    ```sql
    CREATE DATABASE SQLTriggerProjesiDB;
    GO

    USE SQLTriggerProjesiDB;
    GO
    ```

**3. Tabloları Oluşturma:**

*   Oluşturduğunuz `SQLTriggerProjesiDB` veritabanı üzerinde aşağıdaki SQL script'lerini çalıştırarak tabloları oluşturun:

    ```sql
    -- TblProduct Tablosu
    CREATE TABLE TblProduct (
        ProductId INT PRIMARY KEY IDENTITY(1,1),
        ProductName NVARCHAR(50),
        ProductPrice DECIMAL(18, 2),
        ProductStock INT,
        ProductStatust BIT -- Sütun adında yazım hatası olabilir, Statust yerine Status olmalı? Modelde Statust olarak geçmiş.
    );
    GO

    -- TblOrder Tablosu
    CREATE TABLE TblOrder (
        OrderId INT PRIMARY KEY IDENTITY(1,1),
        Customer NVARCHAR(50),
        ProductId INT FOREIGN KEY REFERENCES TblProduct(ProductId),
        Quantity INT,
        UnitPrice DECIMAL(18, 2),
        TotalPrice DECIMAL(18, 2)
    );
    GO

    -- TblCashRegister Tablosu (Başlangıç bakiyesi ile)
    CREATE TABLE TblCashRegister(
        CashRegisterId INT PRIMARY KEY IDENTITY(1,1),
        Balance DECIMAL(18,2)
    );
    INSERT INTO TblCashRegister (Balance) VALUES (0); -- Veya başlangıç değeri
    GO

    -- TblProcess Tablosu (Başlangıç işlem sayısı ile)
    CREATE TABLE TblProcess (
        ProcessId INT PRIMARY KEY IDENTITY(1,1),
        Process INT
    );
    INSERT INTO TblProcess (Process) VALUES (0); -- Başlangıç işlem sayısı
    GO
    ```

**4. Trigger'ları Oluşturma:**

*   **En Önemli Adım:** Aşağıdaki Trigger tanımlarını `SQLTriggerProjesiDB` veritabanı üzerinde çalıştırın. Bu Trigger'lar projenin ana konseptini oluşturur. (Bu kodlar proje içindeki `Items/TextFile1.txt` dosyasında da bulunabilir.)

    ```sql
    -- İşlem Sayacını Artıran Trigger
    CREATE TRIGGER IncreaseProcessCount
    ON TblOrder
    AFTER INSERT
    AS
    UPDATE TblProcess SET Process = Process + 1;
    GO

    -- İşlem Sayacını Azaltan Trigger (Sipariş silme durumunda)
    CREATE TRIGGER DecreaseProcessCount
    ON TblOrder
    AFTER DELETE
    AS
    UPDATE TblProcess SET Process = Process - 1;
    GO

    -- Ürün Stoğunu Azaltan Trigger
    CREATE TRIGGER DecraseProductStockCount
    ON TblOrder
    AFTER INSERT
    AS
    DECLARE @productQuantity INT
    DECLARE @productid INT
2),
        ProductStock INT,
        ProductStatust BIT -- Not: 'Status' yerine 'Statust' yazılmış görünüyor, dikkat!
    );
    GO

    CREATE TABLE TblOrder (
        OrderId INT PRIMARY KEY IDENTITY(1,1),
        Customer NVARCHAR(50),
        ProductId INT FOREIGN KEY REFERENCES TblProduct(ProductId),
        Quantity INT,
        UnitPrice DECIMAL(18, 2),
        TotalPrice DECIMAL(18, 2)
    );
    GO

    CREATE TABLE TblCashRegister (
        CashRegisterId INT PRIMARY KEY IDENTITY(1,1),
        Balance DECIMAL(18, 2)
    );
    GO

    CREATE TABLE TblProcess (
        ProcessId INT PRIMARY KEY IDENTITY(1,1),
        Process INT -- Sadece sayaç değerini tutacak.
    );
    GO

    -- Başlangıç Değerleri (Önemli!)
    -- Trigger'ların çalışması için bu tablolarda en az bir kayıt olmalı.
    INSERT INTO TblCashRegister (Balance) VALUES (0);
    INSERT INTO TblProcess (Process) VALUES (0);
    GO

    -- Örnek Ürün Ekleme (İsteğe Bağlı)
    -- INSERT INTO TblProduct (ProductName, ProductPrice, ProductStock, ProductStatust) VALUES ('Laptop', 15000.00, 50, 1);
    -- INSERT INTO TblProduct (ProductName, ProductPrice, ProductStock, ProductStatust) VALUES ('Klavye', 750.00, 100, 1);
    -- GO
    ```

3.  **Trigger'ları Oluşturma:**
    *   Yine `SQLTriggerProjesiDB` veritabanı üzerinde aşağıdaki Trigger script'lerini çalıştırın (Projedeki `Items/TextFile1.txt` dosyasından alınmıştır, yorumlar temizlenmiştir):

    ```sql
    -- Sipariş eklendiğinde işlem sayısını artıran trigger
    CREATE TRIGGER IncreaseProcessCount
    ON TblOrder
    AFTER INSERT
    AS
    UPDATE TblProcess SET Process += 1;
    GO

    -- Sipariş silindiğinde işlem sayısını azaltan trigger (Opsiyonel, isterseniz ekleyebilirsiniz)
    --CREATE TRIGGER DecreaseProcessCount
    --ON TblOrder
    --AFTER DELETE
    --AS
    --UPDATE TblProcess SET Process -= 1;
    --GO

    -- Sipariş eklendiğinde ilgili ürünün stoğunu azaltan trigger
    CREATE TRIGGER DecraseProductStockCount
    ON TblOrder
    AFTER INSERT
    AS
    DECLARE @productQuantity int
    DECLARE @productid int
    SELECT @productQuantity=Quantity, @productid=ProductId FROM inserted
    UPDATE TblProduct SET ProductStock -= @productQuantity WHERE ProductId=@productid;
    GO

    -- Sipariş eklendiğinde sipariş toplamını kasaya ekleyen trigger
    CREATE TRIGGER AddTotalPriceToCashRegisterBalance
    ON TblOrder
    AFTER INSERT
    AS
    DECLARE @totalPrice decimal(18,2)
    SELECT @totalPrice=TotalPrice FROM inserted
    UPDATE TblCashRegister SET Balance += @totalPrice;
    GO
    ```

## ⚙️ Uygulama Yapılandırması (Connection String)

Uygulamanın SQL Server veritabanına bağlanabilmesi için bağlantı dizesinin doğru ayarlanması gerekir.

*   `SQLTriggerProjesi` projesindeki `App.config` dosyasını açın.
*   `connectionStrings` bölümündeki `SQLTriggerProjesiDBEntities` adlı bağlantı dizesini bulun.
*   `provider connection string` içindeki `data source=UMUT\SQLEXPRESS` kısmını kendi SQL Server sunucu adınızla değiştirin (örn: `.` , `(localdb)\mssqllocaldb`, `YOUR_PC_NAME\SQLEXPRESS` vb.).
*   `initial catalog=SQLTriggerProjesiDB` kısmının, oluşturduğunuz veritabanı adıyla eşleştiğinden emin olun.
*   Eğer SQL Server'ınız Windows Authentication (`integrated security=True`) kullanmıyorsa, bağlantı dizesini SQL Server Authentication'a göre düzenleyin (`User ID=...;Password=...;`).

```xml
 <connectionStrings>
    <add name="SQLTriggerProjesiDBEntities"
         connectionString="metadata=res://*/Data.Model1.csdl|res://*/Data.Model1.ssdl|res://*/Data.Model1.msl;provider=System.Data.SqlClient;provider connection string="data source=YOUR_SERVER_NAME;initial catalog=SQLTriggerProjesiDB;integrated security=True;trustservercertificate=True;MultipleActiveResultSets=True;App=EntityFramework""
         providerName="System.Data.EntityClient" />
  </connectionStrings>
