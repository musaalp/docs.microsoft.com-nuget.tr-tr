---
title: Yerelleştirilmiş bir NuGet paketi oluşturma
description: Oluşturmanın iki yolu ayrıntıları da tüm derlemelerin tek bir pakete dahil etme veya ayrı derlemeler yayımlama NuGet paketleri yerelleştirilmiş.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 017957a349f3c53822225f885e32b7068f1c1c34
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="creating-localized-nuget-packages"></a><span data-ttu-id="ffd1a-103">Yerelleştirilmiş NuGet paketleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ffd1a-103">Creating localized NuGet packages</span></span>

<span data-ttu-id="ffd1a-104">Bir kitaplık yerelleştirilmiş sürümlerini oluşturmanın iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="ffd1a-104">There are two ways to create localized versions of a library:</span></span>

1. <span data-ttu-id="ffd1a-105">Tüm yerelleştirilmiş kaynaklar derlemeleri tek bir paket içerir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-105">Include all localized resources assemblies in a single package.</span></span>
1. <span data-ttu-id="ffd1a-106">Ayrı yerelleştirilmiş uydu paketleri kuralları katı bir dizi izleyerek oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-106">Create separate localized satellite packages by following a strict set of conventions.</span></span>

<span data-ttu-id="ffd1a-107">Her iki yöntem aşağıdaki bölümlerde açıklandığı gibi avantajları ve dezavantajları, sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-107">Both methods have their advantages and disadvantages, as described in the following sections.</span></span>

## <a name="localized-resource-assemblies-in-a-single-package"></a><span data-ttu-id="ffd1a-108">Tek bir pakette yerelleştirilmiş kaynak derlemeler</span><span class="sxs-lookup"><span data-stu-id="ffd1a-108">Localized resource assemblies in a single package</span></span>

<span data-ttu-id="ffd1a-109">Yerelleştirilmiş kaynak grupları tek bir paket dahil olmak üzere genellikle en basit yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-109">Including localized resource assemblies in a single package is typically the simplest approach.</span></span> <span data-ttu-id="ffd1a-110">Bunu yapmak için klasörler oluşturmanız `lib` için desteklenen dil paketi varsayılandan (tr varsayılır-us).</span><span class="sxs-lookup"><span data-stu-id="ffd1a-110">To do this, create folders within `lib` for supported language other than the package default (assumed to be en-us).</span></span> <span data-ttu-id="ffd1a-111">Bu klasörlerde kaynak derlemeler ve yerelleştirilmiş IntelliSense XML dosyaları yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-111">In these folders you can place resource assemblies and localized IntelliSense XML files.</span></span>

<span data-ttu-id="ffd1a-112">Örneğin, aşağıdaki klasör yapısını destekler, Almanca (de), İtalyanca (,), Japonca (ja), Rusça (ru), Çince (Basitleştirilmiş) (zh-atanır) ve Çince (Geleneksel) (zh-Hant):</span><span class="sxs-lookup"><span data-stu-id="ffd1a-112">For example, the following folder structure supports, German (de), Italian (it), Japanese (ja), Russian (ru), Chinese (Simplified) (zh-Hans), and Chinese (Traditional) (zh-Hant):</span></span>

    lib
    └───net40
        │   Contoso.Utilities.dll
        │   Contoso.Utilities.xml
        │
        ├───de
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───it
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ja
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───ru
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        ├───zh-Hans
        │       Contoso.Utilities.resources.dll
        │       Contoso.Utilities.xml
        │
        └───zh-Hant
                Contoso.Utilities.resources.dll
                Contoso.Utilities.xml

<span data-ttu-id="ffd1a-113">Dilleri tüm altında listelendiğini görebilirsiniz `net40` hedef framework klasör.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-113">You can see that the languages are all listed underneath the `net40` target framework folder.</span></span> <span data-ttu-id="ffd1a-114">Kullanıcısıysanız [birden çok çerçeveyi destekleyen](../create-packages/supporting-multiple-target-frameworks.md), altında bir klasör sahip `lib` her değişken için.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-114">If you're [supporting multiple frameworks](../create-packages/supporting-multiple-target-frameworks.md), then you have a folder under `lib` for each variant.</span></span>

<span data-ttu-id="ffd1a-115">Bu klasörler yerinde sonra tüm dosyalarda başvuru, `.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="ffd1a-115">With these folders in place, you then reference all the files in your `.nuspec`:</span></span>

```xml
<?xml version="1.0"?>
<package>
    <metadata>...
    </metadata>
    <files>
    <file src="lib\**" target="lib" />
    </files>
</package>
```

<span data-ttu-id="ffd1a-116">Bu yaklaşım kullanan bir örnek paket [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span><span class="sxs-lookup"><span data-stu-id="ffd1a-116">One example package that uses this approach is [Microsoft.Data.OData 5.4.0](http://nuget.org/packages/Microsoft.Data.OData/5.4.0).</span></span>

### <a name="advantages-and-disadvantages-localized-resource-assemblies"></a><span data-ttu-id="ffd1a-117">Olumlu ve olumsuz yönleri (yerelleştirilmiş kaynak derlemeler)</span><span class="sxs-lookup"><span data-stu-id="ffd1a-117">Advantages and disadvantages (localized resource assemblies)</span></span>

<span data-ttu-id="ffd1a-118">Tek bir paketteki tüm diller paketleme birkaç sakıncaları vardır:</span><span class="sxs-lookup"><span data-stu-id="ffd1a-118">Bundling all languages in a single package has a few disadvantages:</span></span>

1. <span data-ttu-id="ffd1a-119">**Meta veri paylaşılan**: bir NuGet paketi yalnızca tek bir içerebileceğinden `.nuspec` dosya, yalnızca tek bir dil için meta verileri sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-119">**Shared metadata**: Because a NuGet package can only contain a single `.nuspec` file, you can provide metadata for only a single language.</span></span> <span data-ttu-id="ffd1a-120">Diğer bir deyişle, NuGet yerelleştirilmiş meta verileri sunmaz.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-120">That is, NuGet does not present support localized metadata.</span></span>
1. <span data-ttu-id="ffd1a-121">**Paket boyutu**: desteklediğiniz dilleri sayısına bağlı olarak, kitaplık yükleme ve paket geri yükleme yavaşlatır oldukça büyük olabilir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-121">**Package size**: Depending on the number of languages you support, the library can become considerably large, which slows installing and restoring the package.</span></span>
1. <span data-ttu-id="ffd1a-122">**Eşzamanlı sürümleri**: tek bir pakete yerelleştirilmiş dosyaları paketleme gerektirir, paketteki tüm varlıklar eşzamanlı olarak, her yerelleştirme ayrı olarak yayımlamayı bölümlemeye yerine bırakmadan olduğunu.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-122">**Simultaneous releases**: Bundling localized files into a single package requires that you release all assets in that package simultaneously, rather than being able to release each localization separately.</span></span> <span data-ttu-id="ffd1a-123">Ayrıca, herhangi bir yerelleştirme için herhangi bir güncelleştirme tüm paketin yeni bir sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-123">Furthermore, any update to any one localization requires a new version of the entire package.</span></span>

<span data-ttu-id="ffd1a-124">Ancak, aynı zamanda birkaç faydası vardır:</span><span class="sxs-lookup"><span data-stu-id="ffd1a-124">However, it also has a few benefits:</span></span>

1. <span data-ttu-id="ffd1a-125">**Basitlik**: tüketicileri paketi Al desteklenen tüm dillerde her dil ayrıca yüklemek zorunda kalmadan yerine tek bir yükleme.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-125">**Simplicity**: Consumers of the package get all supported languages in a single install, rather than having to install each language separately.</span></span> <span data-ttu-id="ffd1a-126">Tek bir paket üzerinde nuget.org bulmak de kolaydır.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-126">A single package is also easier to find on nuget.org.</span></span>
1. <span data-ttu-id="ffd1a-127">**Sürümleri eşleşmiş**: tüm kaynak derlemeler birincil derlemeyle aynı paketteki olduğundan, bunlar tüm aynı sürüm numarasına paylaşır ve yanlışlıkla ayrılmış riski çalıştırmayın.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-127">**Coupled versions**: Because all of the resource assemblies are in the same package as the primary assembly, they all share the same version number and don't run a risk of getting erroneously decoupled.</span></span>

## <a name="localized-satellite-packages"></a><span data-ttu-id="ffd1a-128">Yerelleştirilmiş uydu paketleri</span><span class="sxs-lookup"><span data-stu-id="ffd1a-128">Localized satellite packages</span></span>

<span data-ttu-id="ffd1a-129">Benzer şekilde nasıl .NET Framework uydu derlemelerini destekler, bu yöntem yerelleştirilmiş kaynaklar ve IntelliSense XML dosyaları uydu paketlere ayırır.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-129">Similar to how .NET Framework supports satellite assemblies, this method separates localized resources and IntelliSense XML files into satellite packages.</span></span>

<span data-ttu-id="ffd1a-130">Bunun için birincil paketinizi adlandırma kuralı kullanır `{identifier}.{version}.nupkg` ve varsayılan dil (örneğin, en-US) için derleme içerir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-130">Do to this, your primary package uses the naming convention `{identifier}.{version}.nupkg` and contains the assembly for the default language (such as en-US).</span></span> <span data-ttu-id="ffd1a-131">Örneğin, `ContosoUtilities.1.0.0.nupkg` aşağıdaki yapısını içerir:</span><span class="sxs-lookup"><span data-stu-id="ffd1a-131">For example, `ContosoUtilities.1.0.0.nupkg` would contain the following structure:</span></span>

    lib
    └───net40
            ContosoUtilities.dll
            ContosoUtilities.xml

<span data-ttu-id="ffd1a-132">Ardından bir uydu derleme adlandırma kuralı kullanır `{identifier}.{language}.{version}.nupkg`, gibi `ContosoUtilities.de.1.0.0.nupkg`.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-132">A satellite assembly then uses the naming convention `{identifier}.{language}.{version}.nupkg`, such as `ContosoUtilities.de.1.0.0.nupkg`.</span></span> <span data-ttu-id="ffd1a-133">Tanımlayıcı **gerekir** birincil paketi tam olarak eşleşmesi.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-133">The identifier **must** exactly match that of the primary package.</span></span>

<span data-ttu-id="ffd1a-134">Bu ayrı bir paket olduğundan, kendi yoktur `.nuspec` yerelleştirilmiş meta verileri içeren dosya.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-134">Because this is a separate package, it has its own `.nuspec` file that contains localized metadata.</span></span> <span data-ttu-id="ffd1a-135">Dikkatli olmanızı, dilde `.nuspec` **gerekir** filename kullanılanla aynı.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-135">Be mindful that the language in the `.nuspec` **must** match the one used in the filename.</span></span>

<span data-ttu-id="ffd1a-136">Uydu derlemesi **gerekir** [] sürüm gösterimini kullanarak bir bağımlılık olarak birincil paketi tam bir sürümünü de bildirme (bkz [paket sürüm](../reference/package-versioning.md)).</span><span class="sxs-lookup"><span data-stu-id="ffd1a-136">The satellite assembly **must** also declare an exact version of the primary package as a dependency, using the [] version notation (see [Package versioning](../reference/package-versioning.md)).</span></span> <span data-ttu-id="ffd1a-137">Örneğin, `ContosoUtilities.de.1.0.0.nupkg` bir bağımlılık üzerindeki bildirilmelidir `ContosoUtilities.1.0.0.nupkg` kullanarak `[1.0.0]` gösterimi.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-137">For example, `ContosoUtilities.de.1.0.0.nupkg` must declare a dependency on `ContosoUtilities.1.0.0.nupkg` using the `[1.0.0]` notation.</span></span> <span data-ttu-id="ffd1a-138">Elbette, uydu paket birincil paketi farklı sürüm numarasından olabilir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-138">The satellite package can, of course, have a different version number than the primary package.</span></span>

<span data-ttu-id="ffd1a-139">Uydu paketin yapısı sonra kaynak assembly ve IntelliSense dosya ile eşleşen bir alt klasöre içermelidir `{language}` paketi dosya:</span><span class="sxs-lookup"><span data-stu-id="ffd1a-139">The satellite package's structure must then include the resource assembly and XML IntelliSense file in a subfolder that matches `{language}` in the package filename:</span></span>

    lib
    └───net40
        └───de
                ContosoUtilities.resources.dll
                ContosoUtilities.xml

<span data-ttu-id="ffd1a-140">**Not**: sürece gibi belirli subcultures `ja-JP` gerekliyse, her zaman daha yüksek düzey dil tanımlayıcısını gibi kullanmak `ja`.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-140">**Note**: unless specific subcultures such as `ja-JP` are necessary, always use the higher level language identifier, like `ja`.</span></span>

<span data-ttu-id="ffd1a-141">Bir uydu derlemede NuGet algılar **yalnızca** eşleşen klasöründeki dosyaları `{language}` dosya.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-141">In a satellite assembly, NuGet will recognize **only** those files in the folder that matches the `{language}` in the filename.</span></span> <span data-ttu-id="ffd1a-142">Diğerleri yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-142">All others are ignored.</span></span>

<span data-ttu-id="ffd1a-143">Tüm bu kuralları karşılandığında, NuGet paketi uydu paket olarak tanımak ve yerelleştirilmiş dosyaları birincil paket yüklemek `lib` klasörü, bunlar ilk olarak toplanmış olur.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-143">When all of these conventions are met, NuGet will recognize the package as a satellite package and install the localized files into the primary package's `lib` folder, as if they had been originally bundled.</span></span> <span data-ttu-id="ffd1a-144">Uydu paketi kaldırma dosyalarından aynı bu klasörden kaldırın.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-144">Uninstalling the satellite package will remove its files from that same folder.</span></span>

<span data-ttu-id="ffd1a-145">Desteklenen her dil için aynı şekilde ek uydu derlemelerini oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-145">You would create additional satellite assemblies in the same way for each supported language.</span></span> <span data-ttu-id="ffd1a-146">Örneğin, ASP.NET MVC paket kümesini inceleyin:</span><span class="sxs-lookup"><span data-stu-id="ffd1a-146">For an example, examine the set of ASP.NET MVC packages:</span></span>

- <span data-ttu-id="ffd1a-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (İngilizce birincil)</span><span class="sxs-lookup"><span data-stu-id="ffd1a-147">[Microsoft.AspNet.Mvc](http://nuget.org/packages/Microsoft.AspNet.Mvc) (English primary)</span></span>
- <span data-ttu-id="ffd1a-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (Almanca)</span><span class="sxs-lookup"><span data-stu-id="ffd1a-148">[Microsoft.AspNet.Mvc.de](http://nuget.org/packages/Microsoft.AspNet.Mvc.de) (German)</span></span>
- <span data-ttu-id="ffd1a-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japonca)</span><span class="sxs-lookup"><span data-stu-id="ffd1a-149">[Microsoft.AspNet.Mvc.ja](http://nuget.org/packages/Microsoft.AspNet.Mvc.ja) (Japanese)</span></span>
- <span data-ttu-id="ffd1a-150">[Microsoft.AspNet.Mvc.zh atanır](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Çince (Basitleştirilmiş))</span><span class="sxs-lookup"><span data-stu-id="ffd1a-150">[Microsoft.AspNet.Mvc.zh-Hans](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hans) (Chinese (Simplified))</span></span>
- <span data-ttu-id="ffd1a-151">[Microsoft.AspNet.Mvc.zh Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Çince (Geleneksel))</span><span class="sxs-lookup"><span data-stu-id="ffd1a-151">[Microsoft.AspNet.Mvc.zh-Hant](http://nuget.org/packages/Microsoft.AspNet.Mvc.zh-Hant) (Chinese (Traditional))</span></span>

### <a name="summary-of-required-conventions"></a><span data-ttu-id="ffd1a-152">Gerekli kuralları özeti</span><span class="sxs-lookup"><span data-stu-id="ffd1a-152">Summary of required conventions</span></span>

- <span data-ttu-id="ffd1a-153">Birincil paketi olarak adlandırılmalıdır `{identifier}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="ffd1a-153">Primary package must be named `{identifier}.{version}.nupkg`</span></span>
- <span data-ttu-id="ffd1a-154">Uydu paket olarak adlandırılmalıdır `{identifier}.{language}.{version}.nupkg`</span><span class="sxs-lookup"><span data-stu-id="ffd1a-154">A satellite package must be named `{identifier}.{language}.{version}.nupkg`</span></span>
- <span data-ttu-id="ffd1a-155">Uydu paketin `.nuspec` filename eşleşecek şekilde dili belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-155">A satellite package's `.nuspec` must specify its language to match the filename.</span></span>
- <span data-ttu-id="ffd1a-156">Bir uydu paketi bir bağımlılık [] noktalı gösterim kullanılarak birincil tam bir sürümünü bildirmelidir kendi `.nuspec` dosya.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-156">A satellite package must declare a dependency on an exact version of the primary using the [] notation in its `.nuspec` file.</span></span> <span data-ttu-id="ffd1a-157">Aralıkları desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-157">Ranges are not supported.</span></span>
- <span data-ttu-id="ffd1a-158">Uydu paket dosyalarında yerleştirmelisiniz `lib\[{framework}\]{language}` tam olarak eşleşen klasör `{language}` dosya.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-158">A satellite package must place files in the `lib\[{framework}\]{language}` folder that exactly matches `{language}` in the filename.</span></span>

### <a name="advantages-and-disadvantages-satellite-packages"></a><span data-ttu-id="ffd1a-159">Olumlu ve olumsuz yönleri (uydu paketleri)</span><span class="sxs-lookup"><span data-stu-id="ffd1a-159">Advantages and disadvantages (satellite packages)</span></span>

<span data-ttu-id="ffd1a-160">Uydu paketleri kullanma birkaç faydası vardır:</span><span class="sxs-lookup"><span data-stu-id="ffd1a-160">Using satellite packages has a few benefits:</span></span>

1. <span data-ttu-id="ffd1a-161">**Paket boyutu**: birincil paketinin genel ayak en aza indirilir ve tüketicilerin yalnızca bunlar kullanmak istediğiniz her bir dilin maliyetinden doğurur.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-161">**Package size**: The overall footprint of the primary package is minimized, and consumers only incur the costs of each language they want to use.</span></span>
1. <span data-ttu-id="ffd1a-162">**Ayrı meta veri**: Her uydu paket kendi sahip `.nuspec` dosyası ve bu nedenle yerelleştirilmiş metaverileri olduğundan.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-162">**Separate metadata**: Each satellite package has its own `.nuspec` file and thus its own localized metadata because.</span></span> <span data-ttu-id="ffd1a-163">Bu yerelleştirilmiş koşullarla nuget.org arayarak paketleri daha kolay bulmak bazı tüketiciler izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-163">This can allow some consumers to find packages more easily by searching nuget.org with localized terms.</span></span>
1. <span data-ttu-id="ffd1a-164">**Ayrılmış sürümleri**: uydu derlemelerini serbest bırakılabilir zamanla yerine tüm aynı anda yerelleştirme çabalarınız yayılan olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-164">**Decoupled releases**: Satellite assemblies can be released over time, rather than all at once, allowing you to spread out your localization efforts.</span></span>

<span data-ttu-id="ffd1a-165">Ancak, uydu paketleri kendi kümesi dezavantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="ffd1a-165">However, satellite packages have their own set of disadvantages:</span></span>

1. <span data-ttu-id="ffd1a-166">**Dağınıklığı**: yerine tek bir paket, yığın arama sonuçlarını nuget.org ve Visual Studio projede başvuruları uzun bir listesi neden olabilecek birçok paketleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-166">**Clutter**: Instead of a single package, you have many packages that can lead to cluttered search results on nuget.org and a long list of references in a Visual Studio project.</span></span>
1. <span data-ttu-id="ffd1a-167">**Katı kuralları**.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-167">**Strict conventions**.</span></span> <span data-ttu-id="ffd1a-168">Uydu paketleri kurallarına tam olarak uymalıdır veya yerelleştirilmiş sürümleri düzgün çekilmesi olmaz.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-168">Satellite packages must follow the conventions exactly or the localized versions won't be picked up properly.</span></span>
1. <span data-ttu-id="ffd1a-169">**Sürüm oluşturma**: Her uydu paket bir tam sürüm bağımlılığı birincil paketi sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-169">**Versioning**: Each satellite package must have an exact version dependency on the primary package.</span></span> <span data-ttu-id="ffd1a-170">Kaynakları değişmedi olsa bile bu birincil paketi güncellemeden tüm uydu paketleri de güncelleştirme gerektirebileceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ffd1a-170">This means that updating the primary package may require updating all satellite packages as well, even if the resources didn't change.</span></span>