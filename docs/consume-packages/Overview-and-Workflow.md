---
title: Genel bakış ve NuGet paketleri kullanma iş akışı
description: NuGet paketlerini bir projede işleminin diğer belirli bölümlerine bağlantılar ile kullanma işlemi bir genel bakış.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: 765b48b474aee17415f53491514bf6e9d50af010
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/26/2018
---
# <a name="package-consumption-workflow"></a><span data-ttu-id="ace47-103">Paket tüketimi iş akışı</span><span class="sxs-lookup"><span data-stu-id="ace47-103">Package consumption workflow</span></span>

<span data-ttu-id="ace47-104">Nuget.org ve kuruluşunuzun oluşturabilirsiniz özel paket galerileri arasında on binlerce uygulamaları ve Hizmetleri'kullanmak için çok yararlı paketleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ace47-104">Between nuget.org and private package galleries that your organization might establish, you can find tens of thousands of highly useful packages to use in your apps and services.</span></span> <span data-ttu-id="ace47-105">Ancak kaynak bağımsız olarak bir paket tüketen aynı genel iş akışını izler.</span><span class="sxs-lookup"><span data-stu-id="ace47-105">But regardless of the source, consuming a package follows the same general workflow.</span></span>

![Akış bir paket kaynağına giden, bir paket bulma, projede yükledikten sonra kullanarak bir ekleme deyimi ve paket API çağrıları](media/Overview-01-GeneralFlow.png)

<span data-ttu-id="ace47-107">\* _Visual Studio ve dotnet.ex' yalnızca. Nuget yükleme komut proje dosyalarını veya packages.config değiştirmez; Giriş el ile yönetilmesi gerekir._</span><span class="sxs-lookup"><span data-stu-id="ace47-107">\* _Visual Studio and dotnet.ex\` only. The nuget install command does not modify project files or packages.config; entries must be managed manually._</span></span>

<span data-ttu-id="ace47-108">Daha fazla ayrıntı için bkz: [bulma ve seçme paketleri](../consume-packages/finding-and-choosing-packages.md) ve [bir NuGet paketi yüklemek için farklı yollar](ways-to-install-a-package.md).</span><span class="sxs-lookup"><span data-stu-id="ace47-108">For further details, see [Finding and Choosing Packages](../consume-packages/finding-and-choosing-packages.md) and [Different ways to install a NuGet package](ways-to-install-a-package.md).</span></span>

<span data-ttu-id="ace47-109">NuGet ya da kaydı yüklü her paket kimliği ve sürüm numarasını hatırlıyor [ `packages.config` ](../reference/packages-config.md) veya proje dosyası (kullanarak [PackageReference](../consume-packages/package-references-in-project-files.md)) proje türüne bağlı olarak ve NuGet sürümü.</span><span class="sxs-lookup"><span data-stu-id="ace47-109">NuGet remembers the identity and version number of each installed package, recording it in either [`packages.config`](../reference/packages-config.md) or the project file (using [PackageReference](../consume-packages/package-references-in-project-files.md)), depending on project type and your version of NuGet.</span></span> <span data-ttu-id="ace47-110">Bu Visual Studio yapılandırılabilir olsa da NuGet ile 4.0 +, PackageReference tercih edilen, [Paket Yöneticisi kullanıcı Arabirimi seçenekleri](../tools/package-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="ace47-110">With NuGet 4.0+, PackageReference is preferred, although this is configurable in Visual Studio through the [Package Manager UI options](../tools/package-manager-ui.md).</span></span> <span data-ttu-id="ace47-111">Herhangi bir durumda, bağımlılıkları projeniz için tam listesini görmek için herhangi bir zamanda uygun dosyasında da bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ace47-111">In any case, you can look in the appropriate file at any time to see the full list of dependencies for your project.</span></span>

> [!Tip]
> <span data-ttu-id="ace47-112">Lisans yazılımınızla kullanmayı düşündüğünüz her paket için her zaman kontrol akıllıca olur.</span><span class="sxs-lookup"><span data-stu-id="ace47-112">It's prudent to always check the license for each package you intend to use in your software.</span></span> <span data-ttu-id="ace47-113">Nuget.org üzerinde bulduğunuz bir **lisans bilgilerini** her paketin açıklaması sayfasının sağ tarafında bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ace47-113">On nuget.org, you find a **License Info** link on the right side of each package's description page.</span></span> <span data-ttu-id="ace47-114">Bir paketi Lisans Koşulları'nı belirtmiyorsa kullanarak doğrudan paketi sahibine başvurun **sahipleri başvurun** bağlantı paketi sayfasında.</span><span class="sxs-lookup"><span data-stu-id="ace47-114">If a package does not specify license terms, contact the package owner directly using the **Contact owners** link on the package page.</span></span> <span data-ttu-id="ace47-115">Microsoft hiçbir fikri mülkiyet, üçüncü taraf paket sağlayıcılardan lisans değildir ve üçüncü taraflar tarafından sağlanan bilgileri sorumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="ace47-115">Microsoft does not license any intellectual property to you from third party package providers and is not responsible for information provided by third parties.</span></span>

<span data-ttu-id="ace47-116">Paketler yüklenirken, NuGet genellikle paket zaten önbelleğinden kullanılabilir olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="ace47-116">When installing packages, NuGet typically checks if the package is already available from its cache.</span></span> <span data-ttu-id="ace47-117">Bu önbellek komut satırından açıklandığı gibi el ile temizleyebilirsiniz [genel paketleri ve önbellek klasör yönetimi](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ace47-117">You can manually clear this cache from the command line, as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="ace47-118">NuGet Ayrıca paket tarafından desteklenen bir hedef çerçeveyi projenizi ile uyumlu olduğundan emin olur.</span><span class="sxs-lookup"><span data-stu-id="ace47-118">NuGet also makes sure that the target frameworks supported by the package are compatible with your project.</span></span> <span data-ttu-id="ace47-119">NuGet paket uyumlu derlemeleri içermiyorsa, bir hata görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ace47-119">If the package does not contain compatible assemblies, NuGet displays an error.</span></span> <span data-ttu-id="ace47-120">Bkz: [uyumsuz paket hatalarını çözme](dependency-resolution.md#resolving-incompatible-package-errors).</span><span class="sxs-lookup"><span data-stu-id="ace47-120">See [Resolving incompatible package errors](dependency-resolution.md#resolving-incompatible-package-errors).</span></span>

<span data-ttu-id="ace47-121">Proje kodunu bir kaynak havuzuna eklerken NuGet paketleri genellikle eklemeyin.</span><span class="sxs-lookup"><span data-stu-id="ace47-121">When adding project code to a source repository, you typically don't include NuGet packages.</span></span> <span data-ttu-id="ace47-122">Kullanıcılar daha sonra depoyu kopyalayın veya aksi takdirde Visual Studio Team Services gibi sistemlerde derleme aracılarını dahil olmak üzere bu proje elde bir yapı çalıştırılmadan önce gerekli paketleri geri yüklemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="ace47-122">Those who later clone the repository or otherwise acquire the project, including build agents on systems like Visual Studio Team Services, must restore the necessary packages prior to running a build:</span></span>

![Bir depo kopyalama ve bir geri yükleme komutunu kullanarak NuGet paketleri geri akışı](media/Overview-02-RestoreFlow.png)

<span data-ttu-id="ace47-124">[Paket geri yükleme](../consume-packages/package-restore.md) proje dosyasındaki bilgileri kullanır veya `packages.config` tüm bağımlılıkları yeniden yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="ace47-124">[Package Restore](../consume-packages/package-restore.md) uses the information in the project file or `packages.config` to reinstall all dependencies.</span></span> <span data-ttu-id="ace47-125">Farklar olduğunu işleminde karmaşık açıklandığı gibi unutmayın [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="ace47-125">Note that there are differences in the process involved, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span> <span data-ttu-id="ace47-126">Genellikle paketleri otomatik olarak geri yükler ve çözüm düzeyi komutu gösterildiği gibi sağlayan Visual Studio bağlamında zaten olduğunuz konsoluyla olduğundan Ayrıca, yukarıdaki diyagramda restore komutu için Paket Yöneticisi konsolu göstermez .</span><span class="sxs-lookup"><span data-stu-id="ace47-126">Also, the diagram above does not show a restore command for the Package Manager Console because you're with the Console you're already in the context of Visual Studio, which typically restores packages automatically and provides the solution-level command as shown.</span></span>

<span data-ttu-id="ace47-127">Bazen bağımlılıkları da yeniden yükleyebilir bir projede zaten dahil edilen paketler yeniden yüklemek gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ace47-127">Occasionally it's necessary to reinstall packages that are already included in a project, which may also reinstall dependencies.</span></span> <span data-ttu-id="ace47-128">Bu kullanarak yapmak kolaydır `nuget reinstall` komut veya NuGet Paket Yöneticisi konsolu.</span><span class="sxs-lookup"><span data-stu-id="ace47-128">This is easy to do using the `nuget reinstall` command or the NuGet Package Manager Console.</span></span> <span data-ttu-id="ace47-129">Ayrıntılar için bkz [Reinstalling ve güncelleştirme paketleri](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ace47-129">For details, see [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

<span data-ttu-id="ace47-130">Son olarak, NuGet davranışı tarafından yönlendirilen `Nuget.Config` dosyaları.</span><span class="sxs-lookup"><span data-stu-id="ace47-130">Finally, NuGet's behavior is driven by `Nuget.Config` files.</span></span> <span data-ttu-id="ace47-131">Birden çok dosya farklı düzeylerde belirli ayarları merkezileştirmek için açıklandığı gibi kullanılabilir [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="ace47-131">Multiple files can be used to centralize certain settings at different levels, as explained in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="ace47-132">NuGet paketleri, üretken kodlama keyfini çıkarın!</span><span class="sxs-lookup"><span data-stu-id="ace47-132">Enjoy your productive coding with NuGet packages!</span></span>