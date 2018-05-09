---
title: NuGet packages.config dosyası başvurusu
description: Bazı proje türleri packages.config projesinde kullanılan NuGet paketleri listesini tutar.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 73234f79cb9eb30327c4e206a5bc51c5bc1c6f1d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="packagesconfig-reference"></a><span data-ttu-id="be1d3-103">Packages.config başvurusu</span><span class="sxs-lookup"><span data-stu-id="be1d3-103">packages.config reference</span></span>

<span data-ttu-id="be1d3-104">`packages.config` Dosyası, projenin başvurduğu paketlerin listesini korumak için bazı proje türleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="be1d3-104">The `packages.config` file is used in some project types to maintain the list of packages referenced by the project.</span></span> <span data-ttu-id="be1d3-105">Bu projenin bağımlılıkları kolayca geri yüklemek NuGet sağlar, bu tüm paketler olmadan yapı sunucu gibi başka bir makine aktarılmasını projesi.</span><span class="sxs-lookup"><span data-stu-id="be1d3-105">This allows NuGet to easily restore the project's dependencies when the project to be transported to a different machine, such as a build server, without all those packages.</span></span>

## <a name="schema"></a><span data-ttu-id="be1d3-106">Şema</span><span class="sxs-lookup"><span data-stu-id="be1d3-106">Schema</span></span>

<span data-ttu-id="be1d3-107">Şema basittir: olan tek bir standart XML üst bilgisini aşağıdaki `<packages>` bir veya daha fazla içeren düğümü `<package>` öğeleri, her başvurusu için bir.</span><span class="sxs-lookup"><span data-stu-id="be1d3-107">The schema is simple: following the standard XML header is a single `<packages>` node that contains one or more `<package>` elements, one for each reference.</span></span> <span data-ttu-id="be1d3-108">Her `<package>` öğesi aşağıdaki özniteliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="be1d3-108">Each `<package>` element can have the following attributes:</span></span>

| <span data-ttu-id="be1d3-109">Öznitelik</span><span class="sxs-lookup"><span data-stu-id="be1d3-109">Attribute</span></span> | <span data-ttu-id="be1d3-110">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be1d3-110">Required</span></span> | <span data-ttu-id="be1d3-111">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be1d3-111">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="be1d3-112">kimlik</span><span class="sxs-lookup"><span data-stu-id="be1d3-112">id</span></span> | <span data-ttu-id="be1d3-113">Evet</span><span class="sxs-lookup"><span data-stu-id="be1d3-113">Yes</span></span> | <span data-ttu-id="be1d3-114">Newtonsoft.json veya Microsoft.AspNet.Mvc gibi paket tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="be1d3-114">The identifier of the package, such as Newtonsoft.json or Microsoft.AspNet.Mvc.</span></span> | 
| <span data-ttu-id="be1d3-115">sürüm</span><span class="sxs-lookup"><span data-stu-id="be1d3-115">version</span></span> | <span data-ttu-id="be1d3-116">Evet</span><span class="sxs-lookup"><span data-stu-id="be1d3-116">Yes</span></span> | <span data-ttu-id="be1d3-117">3.1.1 veya 4.2.5.11-beta gibi yüklemek için paket tam sürümü.</span><span class="sxs-lookup"><span data-stu-id="be1d3-117">The exact version of the package to install, such as 3.1.1 or 4.2.5.11-beta.</span></span> <span data-ttu-id="be1d3-118">Bir sürüm dizesi en az üç sayı olması gerekir; bir yayın öncesi soneki olarak dördüncü isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="be1d3-118">A version string must have at least three numbers; a fourth is optional, as is a pre-release suffix.</span></span> <span data-ttu-id="be1d3-119">Aralıkları izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="be1d3-119">Ranges are not allowed.</span></span> | 
| <span data-ttu-id="be1d3-120">targetFramework</span><span class="sxs-lookup"><span data-stu-id="be1d3-120">targetFramework</span></span> | <span data-ttu-id="be1d3-121">Hayır</span><span class="sxs-lookup"><span data-stu-id="be1d3-121">No</span></span> | <span data-ttu-id="be1d3-122">[Framework bilinen ad (TFM) hedef](target-frameworks.md) paket yüklerken uygulanacak.</span><span class="sxs-lookup"><span data-stu-id="be1d3-122">The [target framework moniker (TFM)](target-frameworks.md) to apply when installing the package.</span></span> <span data-ttu-id="be1d3-123">Bir paketi yüklendiğinde bu projenin hedef başlangıçta ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="be1d3-123">This is initially set to the project's target when a package is installed.</span></span> <span data-ttu-id="be1d3-124">Sonuç olarak, farklı `<package>` öğeleri farklı TFMs sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="be1d3-124">As a result, different `<package>` elements can have different TFMs.</span></span> <span data-ttu-id="be1d3-125">Örneğin, .NET 4.5.2 hedefleyen bir proje oluşturduğunuzda, yüklü olan paketleri o noktada net452 TFM kullanın.</span><span class="sxs-lookup"><span data-stu-id="be1d3-125">For example, if you create a project targeting .NET 4.5.2, packages installed at that point will use the TFM of net452.</span></span> <span data-ttu-id="be1d3-126">Varsa, daha sonra .NET 4.6 projeyi yeniden hedefleyin ve daha fazla paket ekleme olanlar net46 TFM kullanır.</span><span class="sxs-lookup"><span data-stu-id="be1d3-126">If you ;later retarget the project to .NET 4.6 and add more packages, those will use TFM of net46.</span></span> <span data-ttu-id="be1d3-127">Projenin hedef arasında bir uyuşmazlık ve `targetFramework` öznitelikleri uyarılar üretir, bu durumda etkilenen paketler yeniden yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be1d3-127">A mismatch between the project's target and `targetFramework` attributes will generate warnings, in which case you can reinstall the affected packages.</span></span> | 
| <span data-ttu-id="be1d3-128">allowedVersions</span><span class="sxs-lookup"><span data-stu-id="be1d3-128">allowedVersions</span></span> | <span data-ttu-id="be1d3-129">Hayır</span><span class="sxs-lookup"><span data-stu-id="be1d3-129">No</span></span> | <span data-ttu-id="be1d3-130">Paket güncelleştirme sırasında uygulanan bu paket için izin verilen sürüm aralığı (bkz [Constraining yükseltme sürümleri](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span><span class="sxs-lookup"><span data-stu-id="be1d3-130">A range of allowed versions for this package applied during package update (see [Constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="be1d3-131">Mevcut *değil* hangi paket yükleme sırasında yüklü etkilemez ya da geri yükleme işlemi.</span><span class="sxs-lookup"><span data-stu-id="be1d3-131">It does *not* affect what package is installed during an install or restore operation.</span></span> <span data-ttu-id="be1d3-132">Bkz: [paket sürüm](../reference/package-versioning.md#version-ranges-and-wildcards) sözdizimi için.</span><span class="sxs-lookup"><span data-stu-id="be1d3-132">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for syntax.</span></span> <span data-ttu-id="be1d3-133">PackageManager UI izin verilen aralığın dışında tüm sürümleri de devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="be1d3-133">The PackageManager UI also disables all versions outside the allowed range.</span></span> | 
| <span data-ttu-id="be1d3-134">DevelopmentDependency</span><span class="sxs-lookup"><span data-stu-id="be1d3-134">developmentDependency</span></span> | <span data-ttu-id="be1d3-135">Hayır</span><span class="sxs-lookup"><span data-stu-id="be1d3-135">No</span></span> | <span data-ttu-id="be1d3-136">Proje kendisini kullanma, bu ayar bir NuGet paketi oluşturur `true` için bir bağımlılık paket kaybı paketi oluşturulduğunda eklenmesini engeller.</span><span class="sxs-lookup"><span data-stu-id="be1d3-136">If the consuming project itself creates a NuGet package, setting this to `true` for a dependency prevents that package from being included when the consuming package is created.</span></span> <span data-ttu-id="be1d3-137">Varsayılan, `false` değeridir.</span><span class="sxs-lookup"><span data-stu-id="be1d3-137">The default is `false`.</span></span> | 

## <a name="examples"></a><span data-ttu-id="be1d3-138">Örnekler</span><span class="sxs-lookup"><span data-stu-id="be1d3-138">Examples</span></span>

<span data-ttu-id="be1d3-139">Aşağıdaki `packages.config` iki bağımlılıkları başvuruyor:</span><span class="sxs-lookup"><span data-stu-id="be1d3-139">The following `packages.config` refers to two dependencies:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

<span data-ttu-id="be1d3-140">Aşağıdaki `packages.config` dokuz paketlerine başvuruyor ancak `Microsoft.Net.Compilers` nedeniyle tüketim paket oluştururken dahil edilmez `developmentDependency` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="be1d3-140">The following `packages.config` refers to nine packages, but `Microsoft.Net.Compilers` will not be included when building the consuming package because of the `developmentDependency` attribute.</span></span> <span data-ttu-id="be1d3-141">Newtonsoft.Json referansı güncelleştirmeleri yalnızca 8.x ve 9.x sürümleri için de kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="be1d3-141">The reference to Newtonsoft.Json also restricts updates to 8.x and 9.x versions only.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```