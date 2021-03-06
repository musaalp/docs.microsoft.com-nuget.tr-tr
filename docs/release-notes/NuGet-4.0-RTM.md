---
title: NuGet 4.0 RC sürüm notları
description: Bilinen sorunlar, hata düzeltmeleri yapıldı, eklenen özellikler ve dcr NuGet 4.0 RTM için sürüm notları.
author: anangaur
ms.author: anangaur
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: c27d0aa2e5c9af9cb15d2f487b93e93aca666214
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547767"
---
# <a name="nuget-40-rtm-release-notes"></a>NuGet 4.0 RTM sürüm notları

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) NuGet 4.0 ile .NET Core için destek ekler, kalite düzeltmeleri bir sürü var ve performansı artırır. Bu sürüm ayrıca PackageReference için destek, MSBuild hedefleri, arka planda paket geri yükler ve daha fazla NuGet komutları gibi çeşitli iyileştirmeler getirir.

## <a name="known-issues"></a>Bilinen sorunlar

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>Çözümdeki başka bir projeye başvuruda bulunan birden çok projeniz olduğunda NuGet geri yükleme başarısız olabilir

#### <a name="issue"></a>Sorun

Bir çözümde aynı projeye farklı büyük/küçük harf kullanımı veya farklı göreli yollarla birden çok proje başvurusu yapılıyorsa, NuGet geri yükleme çalışmayabilir. [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>Geçici Çözüm

Büyük/küçük harf kullanımını veya göreli yolları düzelterek tüm proje başvurularında aynı olmalarını sağlayın.

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>Paket Yöneticisi Konsolu’nu kullanırken, 'Enter' tuşu çalışmayabilir

#### <a name="issue"></a>Sorun

Bazen Paket Yöneticisi Konsolu’nda Enter tuşu çalışmıyor. Bunu görürseniz, lütfen düzeltmeye yönelik ilerlemeye göz atın ve yeniden oluşturma adımlarınız hakkında yararlı olabilecek ek bilgileri paylaşın. [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>Geçici Çözüm

Visual Studio’yu yeniden başlatın ve çözümü açmadan önce PMC’yi açın. Alternatif olarak, silmeyi deneyin `project.lock.json` ve yeniden geri yüklemeyi.

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>.NET Core projelerinde, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda sınırsız geri yükleme döngüsüne girebilirsiniz

#### <a name="issue"></a>Sorun

Bazen, geçersiz imzalı bir bütünleştirilmiş kod içeren bir paket kullandığınızda veya paket sürümü 'DateTime' onaylayıcısıyla ayarlandığında, bu durum paket otomatik geri yüklemesinin sınırsız bir döngüde çalışmasına neden olur. [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>Geçici Çözüm

Şu anda bu sorunun geçici çözümü yoktur.

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>Görüntülenemiyor, eklenemiyor veya Nuget Paket Yöneticisi'ni kullanarak dotnetclıtools'u başlatamadı

#### <a name="issue"></a>Sorun

NuGet Paket Yöneticisi DotNetCLITools’u görüntülemez ve eklemeye/güncelleştirmeye izin vermez. [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>Geçici Çözüm

Proje dosyanızda DotNetCLIToolReferences el ile düzenlenmelidir.

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>Projeler için PackageId özelliğini ayarladığınızda NuGet geri yüklemesi başarısız olur

#### <a name="issue"></a>Sorun

.NET Core projeleri için, Visual Studio’da NuGet geri yükleme projelerin PackageId özelliğini kabul etmez. [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>Geçici Çözüm

Geri yükleme komutunu, komut satırını kullanarak çalıştırın.

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>Projenizde 'obj' klasörü olmadığında, paket geri yükleme başarısız olabilir

#### <a name="issue"></a>Sorun

'obj' klasörü silindiğinde Visual Studio PackageReferences’ı geri yükleyemez. [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>Geçici Çözüm

'obj' klasörünü el ile oluşturursanız, geri yükleme çalışacaktır.

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>Konsolda Update-Package kullanarak paketleri el ile güncelleştirme işlemi başarısız olabilir

#### <a name="issue"></a>Sorun

Konsolda ile Update-Package kullanımı, yeni dönüştürülmüş PackageReferences projeleri için tek bir kez çalışır. [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>Geçici Çözüm

Şu anda bu sorunun geçici çözümü yoktur.

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>Hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir

#### <a name="issue"></a>Sorun

Visual Studio’da hedef Framework sürümü için hedefin yeniden belirlenmesi eksik Intellisense’e yol açabilir. Bu durum, paket yöneticisi biçimi olarak PackageReferences kullandığınızda ortaya çıkar. [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>Geçici Çözüm

El ile geri yükleme yapın.

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>.NET461’i hedefleyen bir proje, .NETStandard’ı hedefleyen başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur

#### <a name="issue"></a>Sorun

.NET461’i hedefleyen PackageReference tabanlı bir proje, .NETStandard’ı hedefleyen PackageReference tabanlı başka bir projeye başvuruda bulunduğunda, msbuild /t:restore başarısız olur.  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>Geçici Çözüm

Şu anda bu sorunun geçici çözümü yoktur.

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>NuGet 4.0 RTM zaman çerçevesinde giderilen sorunlar

[NuGet 4.0 RC sürüm notları](../release-notes/nuget-4.0-RC.md) -NuGet 4.0 RC için düzeltilen tüm sorunlara listeler

### <a name="features"></a>Özellikler

- NuGet.Core.sln - dizelerini yerelleştirmek [#2041](https://github.com/NuGet/Home/issues/2041)

- LSL modunda - web uygulama projeleri yüklemek için Nuget zorlar [#4258](https://github.com/NuGet/Home/issues/4258)

- Blok sürüme AutoReferenced PackageReference destek "yüklü sdk" paketleri - kullanıcı Arabiriminde değişiklikleri [#4044](https://github.com/NuGet/Home/issues/4044)

- Doğru proje bağımlılıkları için (PackageRef) - PackageSpec.Version iletişim [#3902](https://github.com/NuGet/Home/issues/3902)

- Destek içine başvurularının kaldırılması için `.csproj` commandline(s) - gelen [#4101](https://github.com/NuGet/Home/issues/4101)

- PackageReference projeleri (normal ve xplat) ve basit çözüm yükü - geri yükleme desteği [#4003](https://github.com/NuGet/Home/issues/4003)

- Destek başvuruyu eklemek için `.csproj` commandline(s) - gelen [#3751](https://github.com/NuGet/Home/issues/3751)

- Basit çözüm yükü'için NuGet geri yükleme desteği `packages.config` veya `project.json`  -  [#3711](https://github.com/NuGet/Home/issues/3711)

- contentFiles destek üretilen nuget hedefleri dosyasında - [#3683](https://github.com/NuGet/Home/issues/3683)

- Nuget.exe doğrulama Mac üzerinde bir Mono CI'kurmak MSBuild - kullanarak [#3646](https://github.com/NuGet/Home/issues/3646)

- NuGet v2 NuGet.Core bağımlılıkları dışına - taşıma [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Hatalar

- Visual Studio'da NuGet geri yükleme - projelerin PackageId özelliğini kayıtlı [#4586](https://github.com/NuGet/Home/issues/4586)

- Paket, VSIX paketinde - eklerken NuGet ProjectSystemCache hata [#4545](https://github.com/NuGet/Home/issues/4545)

- Paketi, bir projede birden çok Tfm'ler ile-IncludeSource kullanılıyorsa, özel durum oluşturursa [#4536](https://github.com/NuGet/Home/issues/4536)

- VS 2017 RC3 kilitlenmeleri çözüm çapında Update'ten kullanarak paket Yönetimi - [#4474](https://github.com/NuGet/Home/issues/4474)

- Yeni yüklenen package - kaldıramazsınız [#4435](https://github.com/NuGet/Home/issues/4435)

- İçin PackageRef geçirirken hibrit çözümler garip geri yükleme davranışlarını - sahip [#4433](https://github.com/NuGet/Home/issues/4433)

- Yakında NuGet başlattıktan sonra oluşturma işlemi (yükleme, güncelleştirme, geri yükleme) neden olabilecek VS kilitlenmesine - [#4420](https://github.com/NuGet/Home/issues/4420)

- UI askıda - NuGet.SolutionRestoreManager.RestoreManagerPackage başlatma kilitlenme [#4371](https://github.com/NuGet/Home/issues/4371)

- Paket komut sürüm öğesi - yerine özniteliği olarak ekleyin [#4325](https://github.com/NuGet/Home/issues/4325)

- DotNet
  - geri yükleme foo.sln dotnetcore--SLN yapılandırmalarında (ancak, fark config) yinelenen projeleri geri yükleme grafikte - neden başarısız [#4316](https://github.com/NuGet/Home/issues/4316)

- İçerik paketleri yalnızca - [#3668](https://github.com/NuGet/Home/issues/3668)

- Paket biçimi Seçici seçeneği dışında - varsayılan olarak iyileştirilmiş [#4468](https://github.com/NuGet/Home/issues/4468)

- Perf: CreateUAP_CSharp_VS.01.1.Create proje Duration_TotalElapsedTime 3,153.570 ms (%149.1) tarafından gerileyen. Temel 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- Perf: ManagedLangs_CS_DDRIT.0300.Rebuild Çözüm 1,5 sn Duration_TotalElapsedTime gerileyen. Temel 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- Adaylığınızı başarısız çoklu TFM projelerinde - [#4419](https://github.com/NuGet/Home/issues/4419)

- Perf: WebForms_DDRIT.1200.Close çözüm VM_ImagesInMemory_Total_devenv 3.000 sayısı (%0,5) tarafından gerileyen. Temel 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- -netcoreapp1.1 hedeflenirken paketi uyarıları - vsfeedback [#4397](https://github.com/NuGet/Home/issues/4397)

- Bir NuGet paketi için boş ASP.NET Core web uygulaması - eklenmeye çalışılırken PathTooLongException [#4391](https://github.com/NuGet/Home/issues/4391)

- Paketi dotnet çok sık sık--çalışır.
  - Orada ile dotnetcore paketi başarısız olduğu döngüsel bağımlılığa yol hedef bağımlılık grafiği içeren hedef "Paketi" - [#4381](https://github.com/NuGet/Home/issues/4381)

- Paketi çalıştıran çok sık--oluşturmak NuGet paketi, tüm yapılandırmalar için - içermez [#4380](https://github.com/NuGet/Home/issues/4380)

- NullReferenceException eklenirken nuget ile C++ projesinde - packageref [#4378](https://github.com/NuGet/Home/issues/4378)

- Erişilebilirlik: İçin - package yüklemek için bir proje seçmek için onay kutusunu ekran okuyucusu kompozisyonu değil [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 tutularak başarısız - VS hata 365798 - VSO/VSTS akışlarına bağlanma [#4365](https://github.com/NuGet/Home/issues/4365)

- contentFiles alma yanlış bir konuma çıkış PackagePath "contentFiles" - olarak yol belirtiyorsa [#4348](https://github.com/NuGet/Home/issues/4348)

- Paketi hedef ekler VersionSuffix - PackageVersion özelliğiyle [#4324](https://github.com/NuGet/Home/issues/4324)

- Paket yolu - dotnet paketi işe yaramazsa belirtme [#4321](https://github.com/NuGet/Home/issues/4321)

- NuGet geri yükleme sırasında - yinelenen içe aktarmalarını ilgili uyarılar bir sürü çıkarır [#4304](https://github.com/NuGet/Home/issues/4304)

- "NuGet Paket Yöneticisi biçimi" iletişim koyu tema altında - bozuk görünüyor seçin [#4300](https://github.com/NuGet/Home/issues/4300)

- VS kilitlenme derleme geri yükleme - [#4298](https://github.com/NuGet/Home/issues/4298)

- Visual Studio kilitlenmeleri targetframeworks TFM eklerseniz kaydedin, sonra oluşturun. % saati - 10 [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget paketi, bir proje başarıyla - paketleme başarı iletisi çıkışı değil [#4294](https://github.com/NuGet/Home/issues/4294)

- PackTask System.IO.Compression 4.1 değil olması nedeniyle başarısız bulunamadı - [#4290](https://github.com/NuGet/Home/issues/4290)

- Paketi çalıştıran çok sık--PackTask sık sık başarısız dosya erişim çakışma - [#4289](https://github.com/NuGet/Home/issues/4289)

- NuGet geri yükleme sırasında arka plan - çıkış penceresi açılır [#4274](https://github.com/NuGet/Home/issues/4274)

- (Bu kilitlenmelerine neden olabilir) tehlikeli kodlama düzeni - ServiceProvider ortadan [#4268](https://github.com/NuGet/Home/issues/4268)

- Performans/UIHang - DownloadTimeoutStream okuma - geliştirmek [#4266](https://github.com/NuGet/Home/issues/4266)

- Visual Studio kilitleniyor NuGet geri yükleme işlemi bitmeden - bir projeyi kapatmak çalışırsanız [#4257](https://github.com/NuGet/Home/issues/4257)

- PackTask ve paketleme ile ilgili sorunları `.nuspec`  -  [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] Nuget paketleri (visual Studio'yu yeniden başlatmanız gerekir) - yeni proje çözümlenemiyor [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] "Sürüm" açılan menü kalmak için struggles eşitlenmiş ile seçilen nuGet paketini... - mevcut paket sürümleri gösteren [#4198](https://github.com/NuGet/Home/issues/4198)

- Nuget.Client kullanması gereken CPS JoinableTaskFactory CPS ile etkileşim kurulurken - kilitlenmeleri önlemek için [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 değil akışının paketi açılırken `.targets` - paketinden [#4171](https://github.com/NuGet/Home/issues/4171)

- DotNet
  - dotnetcore paketi başlığında desteklemiyor `.csproj`  -  [#4150](https://github.com/NuGet/Home/issues/4150)

- Install-Package sonuçları VS2017 RC - hata iletişim [#4127](https://github.com/NuGet/Home/issues/4127)

- Kullanıcı arabirimini nominate CPS güncelleştirme katılmaz gibi .net core projesi için bir paket güncelleştirme çalışmıyor için görünür. - [#4035](https://github.com/NuGet/Home/issues/4035)

- Çözümlenmemiş başvuru uyarı - geliştirmek [#3955](https://github.com/NuGet/Home/issues/3955)

- DotNet
  - dotnetcore paketi - ProjectReference kaybeder sürüm bilgisi - [#3953](https://github.com/NuGet/Home/issues/3953)

- UWP uygulaması oluşturma projesi oluşturun ve geçen toplam süre gerilemeleri - yeniden [#3873](https://github.com/NuGet/Home/issues/3873)

- Başarılı bir geri yükleme iletisi bile hatasından sonra geri yükleme sırasında görüntülenir. - [#3799](https://github.com/NuGet/Home/issues/3799)

- Nuget.CommandLine 3.4.4 nuget.org'da - yeniden yayımlama [#2931](https://github.com/NuGet/Home/issues/2931)

- Geçiş üzerinde olan projeler Değiştir `project.json` için `.csproj` ---geri yükleme başarısız - [#4297](https://github.com/NuGet/Home/issues/4297)

- Yeni oluşturulan xunit Test projesi üzerinde-geri yükleme başarısız [#4296](https://github.com/NuGet/Home/issues/4296)

- Core projeleri biraz bekleyin, UI açık-'kurmak kilitleme [#4269](https://github.com/NuGet/Home/issues/4269)

- Hedef dosya için derleme görevleri - düzeltme [#4267](https://github.com/NuGet/Home/issues/4267)

- Hata listesi, başvurulan - projeyi derleme çözümü sonra hata sahip [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057: "_GenerateRestoreGraphProjectEntry" hedef projesinde yok. - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback: tüm projeleri - seçtiğiniz çözüm için nuget Yöneticisi UI kilitleniyor [#4191](https://github.com/NuGet/Home/issues/4191)

- nuget.exe msbuildpath başarısız sonunda eğik çizgi - olduğunda [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback: NuGet geri yükleme vermek LinqToTwitter proje - birden çok proje başvurusu uyarılarını [#4156](https://github.com/NuGet/Home/issues/4156)

- Gelen paket `.csproj` minClientVersion öznitelik - içermez [#4135](https://github.com/NuGet/Home/issues/4135)

- NuGet.Build.Tasks.Pack.dll sevk ertelenmiş olarak imzalandığında VS2017'de (d15rel 26014.00)- [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback: 3.7.1 - CMake ile oluşturulan bir VS 2015 proje geri yükleme başarısız [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback: Derleme müdürün - daha ayrıntılı hata iletileri küçük geri yükleme hataları gizlememeniz [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] Hata oluştu Web sitesi projesi için NuGet paketlerini geri yüklerken: değer null olamaz. - [#4092](https://github.com/NuGet/Home/issues/4092)

- Geçiş oluşturur "içinde NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker - özel durum başvuru nesnesi" [#4067](https://github.com/NuGet/Home/issues/4067)

- DotNet
  - dotnetcore pack Araçları Paketi - derlendiği sürümlerle [#4063](https://github.com/NuGet/Home/issues/4063)

- Durum çubuğunda geri yüklemek için - saniye sürer, yeni arka plan geri yazar milisaniye [#4036](https://github.com/NuGet/Home/issues/4036)

- Üzerinde yazım yanlışı başarısız tüm proje başvuruları - çözümlenecek [#4018](https://github.com/NuGet/Home/issues/4018)

- Paket başvurusu senaryolarda - PCM iş akışlarını etkinleştirin [#4016](https://github.com/NuGet/Home/issues/4016)

- Yüklü paketleri Yöneticisi kullanıcı Arabirimi - paketinde bulunamıyor [#4015](https://github.com/NuGet/Home/issues/4015)

- DotNet
  - PackagePath boş - olduğunda dotnetcore paketi başarısız [#3993](https://github.com/NuGet/Home/issues/3993)

- Bir Çoklu kullanıcı senaryosu - görev başarısız olursa geri [#3897](https://github.com/NuGet/Home/issues/3897)

- NuGet paketi görevi kullanılarak sevk içerik türü değiştirilemiyor- [#3895](https://github.com/NuGet/Home/issues/3895)

- Varsayılan Copy ContentFiles için MsBuild /t:pack - yanlış [#3894](https://github.com/NuGet/Home/issues/3894)

- Çift paket geri yükleme günlüklerini geri yükleme paketleri iletisi - [#3785](https://github.com/NuGet/Home/issues/3785)

- Guardrails - Kaldır "çalışma zamanları" bölümünün geri yükleme yalnızca geçerli projeye - uygulanması [#3768](https://github.com/NuGet/Home/issues/3768)

- Paketi görevi koyar içerik dosyaları hem de ' içeriği /' ve ' contentFiles /'- [#3718](https://github.com/NuGet/Home/issues/3718)

- DotNet
  - dotnetcore pack3 fazladan etiketi bölme - [#3701](https://github.com/NuGet/Home/issues/3701)

- DotNet
  - dotnetcore paketi: Paket projeleriyle paketleme, yinelenen alma uyarısı - sonuçlarında başvuruyor [#3665](https://github.com/NuGet/Home/issues/3665)

- Geri yükleme VS içinde günlüğü değil her zaman göster - [#3633](https://github.com/NuGet/Home/issues/3633)

- nuget Yereller Yardım metni hala paketleri önbellek - belirtilen [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 PackageReferences TargetFrameworks ile tüm çiftler. - [#3504](https://github.com/NuGet/Home/issues/3504)

- Nuget seçer beklenmeyen MSBuild sürümü VS "15" Preview 4 geliştirme Komut İstemi - [#3408](https://github.com/NuGet/Home/issues/3408)

- Hedefleri/özellik dosyaları geri yükleme başarısız - out yazma [#3399](https://github.com/NuGet/Home/issues/3399)

- Komut İstemi'nde VS 15 - çalıştırırken, NuGet geri yükleme işlemi sırasında aynı compat dolgular MSBuild olarak dikkate değil [#3387](https://github.com/NuGet/Home/issues/3387)

- PackFromProjectWithDevelopmentDependencySet VS15 için - yeniden etkinleştirmeniz [#3272](https://github.com/NuGet/Home/issues/3272)

- Blend - NuGet sorunları [#4043](https://github.com/NuGet/Home/issues/4043)

- RC2'den - göndermeye CLI ve SDK depoları 4.0.0.2067 tümleştirin [#4029](https://github.com/NuGet/Home/issues/4029)

- Yeni çekirdek konsol uygulaması, çözümü Kapat, açık olan çözüm ve çözümü Kapat - oluşturduğunuzda VS askıda [#4008](https://github.com/NuGet/Home/issues/4008)

- Yanıt vermemeye açılış proje d15prerel.25916.01 karşı-ulaşmaktan [#3982](https://github.com/NuGet/Home/issues/3982)

- Belge/yardım iletisini - dotnet/nuget.exe Yereller düzeltme [#3919](https://github.com/NuGet/Home/issues/3919)

- Başında veya sonunda boşluk - sorunlarının PackTask İnceleme [#3906](https://github.com/NuGet/Home/issues/3906)

- DotNet
  - dotnetcore paketi obj değil bin - paket [#3880](https://github.com/NuGet/Home/issues/3880)

- DotNet
  - dotnetcore paketi ProjectReference sürüm 1.0.0 sürümüne - ayarlamak için her zaman görünür [#3874](https://github.com/NuGet/Home/issues/3874)

- DotNet
  - dotnetcore paketi proje başvuruları ile başarısız olur ve <TargetFramework>  -  [#3865](https://github.com/NuGet/Home/issues/3865)

- LockRecursionException ProjectSystemCache.TryGetProjectNameByShortName içinde- [#3861](https://github.com/NuGet/Home/issues/3861)

- MSBuild özelliklerinden - boşluğu Kırp [#3819](https://github.com/NuGet/Home/issues/3819)

- Proje yükünde - oluşturulan iki proje olayları birleştirecek [#3759](https://github.com/NuGet/Home/issues/3759)

- P2p kitaplıklarında `project.assets.json` dosyanız yanlış sürüm - [#3748](https://github.com/NuGet/Home/issues/3748)

- Kilitlenme akışı yanıt vermiyor ve kullanılamıyor paket - nedeniyle geri [#3672](https://github.com/NuGet/Home/issues/3672)

- nuget.exe üzerinde büyük bir miktarını, MSBuild hata çıktısı - askıda kalmasına [#3572](https://github.com/NuGet/Home/issues/3572)

- Derleme üzerinde geri yükleme için Blend ilk kez başarısız ikinci kez (VS senaryo sabit) - başarılı [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>Dcr

- VSIX v3 vsıx'e - v2 VSIX geçirme [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet yolunu almak için bir mekanizma olmalıdır - msbuild'de kilit dosyaya [#3351](https://github.com/NuGet/Home/issues/3351)

- Derleme varlıklar TFM uyumluluk denetimi ve varlıklar - dosyasına [#3296](https://github.com/NuGet/Home/issues/3296)

- Yeni bir ProjectCapability "Paketi" paketinde tanımlamak hedefleri paket etkinleştirmek için ilgili özellikleri - [#4146](https://github.com/NuGet/Home/issues/4146)

- Bir posta oluştururken hedef koşuluna "GeneratePackageOnBuild" MSBuild özelliği - Pack çalıştırma [#4145](https://github.com/NuGet/Home/issues/4145)

- NuGet özelliği RestoreProjectStyle belirli NuGet proje - oluşturulacağı [#4134](https://github.com/NuGet/Home/issues/4134)

- Projeye geçişli başvurular değiştirmek için - geri yükleme uyum [#4076](https://github.com/NuGet/Home/issues/4076)

- Hedef dosya - olmayan UWP projeleri için NuGet özellikleri eklemek [#4030](https://github.com/NuGet/Home/issues/4030)

- UWP TargetPlatformVersion desteği - [#3923](https://github.com/NuGet/Home/issues/3923)

- Proje başvuru meta verisi için NuGet proje sistemi - iletişim [#3922](https://github.com/NuGet/Home/issues/3922)

- Kullanıcı Arabirimi ekleyin paketleme modu için - [#3921](https://github.com/NuGet/Home/issues/3921)

- Eski `.csproj` NugetTargetMoniker ve proj/hedefleri - Ayarla RuntimeIdentifiers gereken [#3854](https://github.com/NuGet/Home/issues/3854)

- Install package-geri - otomatik çakışıyor [#3836](https://github.com/NuGet/Home/issues/3836)

- Bağlam menüsü QueryStatus olmayan durum VSPackage yüklendiğinde değil, - [#3835](https://github.com/NuGet/Home/issues/3835)

- Çözüm geri yükleme ve yapı geri hala iletişim kutuları - Göster [#3789](https://github.com/NuGet/Home/issues/3789)

- NuGet.Clients çözüm derlemesi - yalıtmak VSSDK sürümünde [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>GitHub sorunları RTM'de sabit bağlantılar
[Sorunlar listesinde 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[Sorunlar listesinde 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[Sorunlar listesinde 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[4 sorunları listeler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[5 sorunları listeler](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
