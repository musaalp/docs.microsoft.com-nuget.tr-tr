---
title: Bir NuGet Paketi Yayımlama
description: Ayrıntılı yönergeler için NuGet paketi nuget.org veya özel akışları yayımlama ve nuget.org paket sahipliği yönetme.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 539ac9485e6062a0bdc3bb86dac0f028a2de7821
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/28/2018
---
# <a name="publishing-packages"></a><span data-ttu-id="ddd85-103">Paketleri yayımlama</span><span class="sxs-lookup"><span data-stu-id="ddd85-103">Publishing packages</span></span>

<span data-ttu-id="ddd85-104">Bir paketi oluşturup sahip sonra `.nukpg` ele dosya, diğer geliştiriciler için genel veya özel olarak kullanılabilmesi için basit bir işlemdir:</span><span class="sxs-lookup"><span data-stu-id="ddd85-104">Once you have created a package and have your `.nukpg` file in hand, it's a simple process to make it available to other developers, either publicly or privately:</span></span>

- <span data-ttu-id="ddd85-105">Ortak paketleri kullanılabilir hale getirilir tüm geliştiriciler için genel ile [nuget.org](https://www.nuget.org/packages/manage/upload) (NuGet 4.1.0+ gerektirir) Bu makalede anlatıldığı gibi.</span><span class="sxs-lookup"><span data-stu-id="ddd85-105">Public packages are made available to all developers globally through [nuget.org](https://www.nuget.org/packages/manage/upload) as described in this article (requires NuGet 4.1.0+).</span></span>
- <span data-ttu-id="ddd85-106">Özel paketler yalnızca bir ekip veya kuruluş, kullanılabilir ya da bir dosya paylaşımı, özel bir NuGet sunucu barındırarak [Visual Studio Team Services paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish), veya bir üçüncü taraf deposu myget, ProGet, Nexus gibi Depo ve Artifactory.</span><span class="sxs-lookup"><span data-stu-id="ddd85-106">Private packages are available to only a team or organization, by hosting them either a file share, a private NuGet server, [Visual Studio Team Services Package Management](https://www.visualstudio.com/docs/package/nuget/publish), or a third-party repository such as myget, ProGet, Nexus Repository, and Artifactory.</span></span> <span data-ttu-id="ddd85-107">Daha fazla bilgi için bkz: [barındırma paketleri genel bakış](../hosting-packages/overview.md).</span><span class="sxs-lookup"><span data-stu-id="ddd85-107">For additional details, see [Hosting Packages Overview](../hosting-packages/overview.md).</span></span>

<span data-ttu-id="ddd85-108">Bu makale nuget.org yayımlamayı kapsamaktadır; Visual Studio Team Services yayımlama için bkz: [paket Yönetimi](https://www.visualstudio.com/docs/package/nuget/publish).</span><span class="sxs-lookup"><span data-stu-id="ddd85-108">This article covers publishing to nuget.org; for publishing to Visual Studio Team Services, see [Package Management](https://www.visualstudio.com/docs/package/nuget/publish).</span></span>

## <a name="publish-to-nugetorg"></a><span data-ttu-id="ddd85-109">Nuget.org için yayımlama</span><span class="sxs-lookup"><span data-stu-id="ddd85-109">Publish to nuget.org</span></span>

<span data-ttu-id="ddd85-110">Nuget.org için hangi hesabın nuget.org ile kaydetmek için istenir, bir Microsoft hesabıyla oturum gerekir. Portal eski sürümleri kullanılarak oluşturulan bir nuget.org hesabıyla oturum.</span><span class="sxs-lookup"><span data-stu-id="ddd85-110">For nuget.org, you must sign in with a Microsoft account, with which you'll be asked to register the account with nuget.org. You can also sign in with a nuget.org account created using older versions of the portal.</span></span>

![NuGet oturum açma konumu](media/publish_NuGetSignIn.png)

<span data-ttu-id="ddd85-112">Ardından, ya da nuget.org web portalı üzerinden paketini karşıya yükleyin, yapabilirsiniz nuget.org için komut satırından itme (gerektirir `nuget.exe` 4.1.0+), ya da Visual Studio Team Services aracılığıyla CI/CD işleminin parçası olarak aşağıdaki bölümlerde açıklandığı gibi yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="ddd85-112">Next, you can either upload the package through the nuget.org web portal, push to nuget.org from the command line (requires `nuget.exe` 4.1.0+) , or publish as part of a CI/CD process through Visual Studio Team Services, as described in the following sections.</span></span>

### <a name="web-portal-use-the-upload-package-tab-on-nugetorg"></a><span data-ttu-id="ddd85-113">Web portalı: nuget.org üzerinde karşıya yükleme paketini sekmesini kullanın</span><span class="sxs-lookup"><span data-stu-id="ddd85-113">Web portal: use the Upload Package tab on nuget.org</span></span>

1. <span data-ttu-id="ddd85-114">Seçin **karşıya** üst menüsünde nuget.org ve paket konumuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="ddd85-114">Select **Upload** on the top menu of nuget.org and browse to the package location.</span></span>

    ![Nuget.org paketin karşıya yükle](media/publish_UploadYourPackage.PNG)

1. <span data-ttu-id="ddd85-116">nuget.org paket adı olup olmadığını bildirir.</span><span class="sxs-lookup"><span data-stu-id="ddd85-116">nuget.org tells you if the package name is available.</span></span> <span data-ttu-id="ddd85-117">Değil değiştirirseniz, projenizdeki paket tanımlayıcısı yeniden oluşturun ve karşıya yüklemeyi yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="ddd85-117">If it isn't, change the package identifier in your project, rebuild, and try the upload again.</span></span>

1. <span data-ttu-id="ddd85-118">Paket adı olup olmadığını nuget.org açılır bir **doğrula** bölüm içinde gözden geçirebileceğiniz paket bildirimi meta verileri.</span><span class="sxs-lookup"><span data-stu-id="ddd85-118">If the package name is available, nuget.org opens a **Verify** section in which you can review the metadata from the package manifest.</span></span> <span data-ttu-id="ddd85-119">Meta veri değişiklik yapmak için projenizin Düzenle (proje dosyası veya `.nuspec` dosyası) yeniden, paketi yeniden oluşturun ve yeniden yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ddd85-119">To change any of the metadata, edit your project (project file or `.nuspec` file), rebuild, recreate the package, and upload again.</span></span>

1. <span data-ttu-id="ddd85-120">Altında **alma belgelerine** Markdown yapıştırın, bir URL ile belgelerinizi noktasına veya bir belge dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ddd85-120">Under **Import Documentation** you can paste Markdown, point to your docs with a URL, or upload a documentation file.</span></span>

1. <span data-ttu-id="ddd85-121">Tüm bilgileri hazır olduğunda seçme **gönderme** düğmesi</span><span class="sxs-lookup"><span data-stu-id="ddd85-121">When all the information is ready, select the **Submit** button</span></span>

### <a name="command-line"></a><span data-ttu-id="ddd85-122">Komut satırı</span><span class="sxs-lookup"><span data-stu-id="ddd85-122">Command line</span></span>

<span data-ttu-id="ddd85-123">Anında iletme paketlere kullanmalısınız nuget.org için [nuget.exe v4.1.0 veya yukarıdaki](https://www.nuget.org/downloads), gerekli uygulayan [NuGet protokolleri](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="ddd85-123">To push packages to nuget.org you must use [nuget.exe v4.1.0 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span> <span data-ttu-id="ddd85-124">Ayrıca nuget.org üzerinde oluşturulan bir API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="ddd85-124">You also need an API key, which is created on nuget.org.</span></span>

#### <a name="create-api-keys"></a><span data-ttu-id="ddd85-125">API anahtarları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddd85-125">Create API keys</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

#### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="ddd85-126">DotNet nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="ddd85-126">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](../quickstart/includes/publish-dotnet.md)]

#### <a name="publish-with-nuget-push"></a><span data-ttu-id="ddd85-127">Nuget itme ile yayımlama</span><span class="sxs-lookup"><span data-stu-id="ddd85-127">Publish with nuget push</span></span>

1. <span data-ttu-id="ddd85-128">Bir komut isteminde aşağıdaki komutu çalıştırın komutu, değiştirme `<your_API_key>` nuget.org elde edilen anahtar ile:</span><span class="sxs-lookup"><span data-stu-id="ddd85-128">At a command prompt, run the following command, replacing `<your_API_key>` with the key obtained from nuget.org:</span></span>

    ```cli
    nuget setApiKey <your_API_key>
    ```

    <span data-ttu-id="ddd85-129">Bu komut, API anahtarınıza NuGet yapılandırmanızda depolar aynı bilgisayarda bu adımı yineleyin.</span><span class="sxs-lookup"><span data-stu-id="ddd85-129">This command stores your API key in your NuGet configuration so that you need repeat this step again on the same computer.</span></span>

1. <span data-ttu-id="ddd85-130">Paketinizi NuGet galerisinde aşağıdaki komutu kullanarak gönderin:</span><span class="sxs-lookup"><span data-stu-id="ddd85-130">Push your package to NuGet Gallery using the following command:</span></span>

    ```cli
    nuget push YourPackage.nupkg -Source https://api.nuget.org/v3/index.json
    ```

### <a name="package-validation-and-indexing"></a><span data-ttu-id="ddd85-131">Paket doğrulama ve dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="ddd85-131">Package validation and indexing</span></span>

<span data-ttu-id="ddd85-132">Nuget.org için gönderilen paketleri virüs denetimleri gibi birkaç doğrulamaları geçer.</span><span class="sxs-lookup"><span data-stu-id="ddd85-132">Packages pushed to nuget.org undergo several validations, such as virus checks.</span></span> <span data-ttu-id="ddd85-133">(Nuget.org tüm paketleri düzenli aralıklarla taranır.)</span><span class="sxs-lookup"><span data-stu-id="ddd85-133">(All packages on nuget.org are periodically scanned.)</span></span>

<span data-ttu-id="ddd85-134">biçimindeki telefon numarasıdır.</span><span class="sxs-lookup"><span data-stu-id="ddd85-134">.</span></span> <span data-ttu-id="ddd85-135">Paketin tüm doğrulama denetimlerini geçtiğinde, sıralanması ve arama sonuçlarında görüntülenmesini biraz sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ddd85-135">When the package has passed all validation checks, it might take a while for it to be indexed and appear in search results.</span></span> <span data-ttu-id="ddd85-136">Dizin oluşturma işlemi tamamlandıktan sonra paketi başarıyla yayımlandı onaylayan bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="ddd85-136">Once indexing is complete, you receive an email confirming that the package was successfully published.</span></span> <span data-ttu-id="ddd85-137">Paket doğrulama denetimi başarısız olursa, ilgili hatayı görüntülemek için Paket ayrıntılarını sayfa güncelleştirilir ve ayrıca hakkında bildiren bir e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="ddd85-137">If the package fails a validation check, the package details page will update to display the associated error and you also receive an email notifying you about it.</span></span>

<span data-ttu-id="ddd85-138">Paket doğrulama ve dizin oluşturma altında 15 dakika genellikle alır.</span><span class="sxs-lookup"><span data-stu-id="ddd85-138">Package validation and indexing usually takes under 15 minutes.</span></span> <span data-ttu-id="ddd85-139">Paket yayımlama beklenenden daha uzun sürüyorsa, ziyaret [status.nuget.org](https://status.nuget.org/) nuget.org tüm kesintileri yaşayan varsa denetlemek için.</span><span class="sxs-lookup"><span data-stu-id="ddd85-139">If the package publishing is taking longer than expected, visit [status.nuget.org](https://status.nuget.org/) to check if nuget.org is experiencing any interruptions.</span></span> <span data-ttu-id="ddd85-140">Tüm sistemler işletimsel ve paket bir saat içinde başarıyla yayımlanmadı, lütfen nuget.org oturum açın ve paket sayfasında kişi destek bağlantısı kullanarak bizimle bağlantı kurun.</span><span class="sxs-lookup"><span data-stu-id="ddd85-140">If all systems are operational and the package hasn't been successfully published within an hour, please login to nuget.org and contact us using the Contact Support link on the package page.</span></span>

<span data-ttu-id="ddd85-141">Bir paketin durumunu görmek için seçin **paketlerini yönetmek** hesap adınızı nuget.org üzerinde altında. Doğrulama tamamlandıktan sonra bir onay e-posta alırsınız.</span><span class="sxs-lookup"><span data-stu-id="ddd85-141">To see the status of a package, select **Manage packages** under your account name on nuget.org. You receive a confirmation email when validation is complete.</span></span>

<span data-ttu-id="ddd85-142">Dizine ve diğerleri, hangi sırada paket sayfanızda aşağıdaki iletiyi görürsünüz bulabileceğiniz bir yerde arama sonuçlarında görüntülenmesini paketinizi biraz sürebilir dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="ddd85-142">Note that it might take a while for your package to be indexed and appear in search results where others can find it, during which time you see the following message on your package page:</span></span>

![Bir paket henüz yayımlanmadı belirten iletisi](media/publish_NotYetIndexed.png)

### <a name="visual-studio-team-services-cicd"></a><span data-ttu-id="ddd85-144">Visual Studio Team Services (CI/CD)</span><span class="sxs-lookup"><span data-stu-id="ddd85-144">Visual Studio Team Services (CI/CD)</span></span>

<span data-ttu-id="ddd85-145">Paketleri nuget.org sürekli tümleştirme/dağıtım işleminin bir parçası Visual Studio Team Services kullanarak anında iletme, kullanmalısınız `nuget.exe` 4.1 veya yukarıdaki NuGet görevler.</span><span class="sxs-lookup"><span data-stu-id="ddd85-145">If you push packages to nuget.org using Visual Studio Team Services as part of your Continuous Integration/Deployment process, you must use `nuget.exe` 4.1 or above in the NuGet tasks.</span></span> <span data-ttu-id="ddd85-146">Ayrıntılar bulunabilir [yapı içinde son NuGet kullanarak](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blogu).</span><span class="sxs-lookup"><span data-stu-id="ddd85-146">Details can be found on [Using the latest NuGet in your build](https://blogs.msdn.microsoft.com/devops/2017/09/29/using-the-latest-nuget-in-your-build/) (Microsoft DevOps blog).</span></span>

## <a name="managing-package-owners-on-nugetorg"></a><span data-ttu-id="ddd85-147">Nuget.org üzerinde paket sahiplerini yönetme</span><span class="sxs-lookup"><span data-stu-id="ddd85-147">Managing package owners on nuget.org</span></span>

<span data-ttu-id="ddd85-148">Ancak her NuGet paketin `.nuspec` dosyası paketin yazarlar tanımlar, nuget.org galeri meta verilerin sahipliği tanımlamak için kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="ddd85-148">Although each NuGet package's `.nuspec` file defines the package's authors, the nuget.org gallery does not use that metadata to define ownership.</span></span> <span data-ttu-id="ddd85-149">Bunun yerine, nuget.org ilk sahipliği paketi yayımlar kişiye atar.</span><span class="sxs-lookup"><span data-stu-id="ddd85-149">Instead, nuget.org assigns initial ownership to the person who publishes the package.</span></span> <span data-ttu-id="ddd85-150">Bu paket nuget.org kullanıcı Arabirimi aracılığıyla karşıya oturum açan kullanıcının ya da, API anahtarı ile kullanıldı kullanıcılar olan `nuget SetApiKey` veya `nuget push`.</span><span class="sxs-lookup"><span data-stu-id="ddd85-150">This is either the logged-in user who uploaded the package through the nuget.org UI, or the users whose API key was used with `nuget SetApiKey` or `nuget push`.</span></span>

<span data-ttu-id="ddd85-151">Tüm paket sahipleri paket ekleme ve kaldırma diğer sahipleri ve güncelleştirmeleri yayımlama da dahil olmak üzere, tam izinlere sahip.</span><span class="sxs-lookup"><span data-stu-id="ddd85-151">All package owners have full permissions for the package, including adding and removing other owners, and publishing updates.</span></span>

<span data-ttu-id="ddd85-152">Bir paket sahipliğini değiştirmek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="ddd85-152">To change ownership of a package, do the following:</span></span>

1. <span data-ttu-id="ddd85-153">Nuget.org paketinin geçerli sahibi olan hesap ile oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ddd85-153">Sign in to nuget.org with the account that is the current owner of the package.</span></span>
1. <span data-ttu-id="ddd85-154">Hesap adınızı seçin, **paketlerini yönetmek**ve genişletin **yayımlanan paketleri**.</span><span class="sxs-lookup"><span data-stu-id="ddd85-154">Select your account name, select **Manage packages**, and expand **Published Packages**.</span></span>
1. <span data-ttu-id="ddd85-155">Yönetmek istediğiniz paketi seçin, sonra sağ tarafta seçin **sahiplerini yönetme**.</span><span class="sxs-lookup"><span data-stu-id="ddd85-155">Select on the package you want to manage, then on the right side select **Manage owners**.</span></span>

<span data-ttu-id="ddd85-156">Buradan, birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="ddd85-156">From here you have several options:</span></span>

1. <span data-ttu-id="ddd85-157">Altında listelenen sahip kaldırmak **geçerli sahipleri**.</span><span class="sxs-lookup"><span data-stu-id="ddd85-157">Remove any owner listed under **Current Owners**.</span></span>
1. <span data-ttu-id="ddd85-158">Bir sahip altında eklemek **eklemek sahibi** kullanıcı adı, bir ileti girme ve seçerek **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="ddd85-158">Add an owner under **Add Owner** by entering their user name, a message, and selecting **Add**.</span></span> <span data-ttu-id="ddd85-159">Bu eylem, yeni ikincil sahip bir onay bağlantısı ile bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="ddd85-159">This action sends an email to that new co-owner with a confirmation link.</span></span> <span data-ttu-id="ddd85-160">Onaylandıktan sonra o kişiyi eklemek ve sahipleri kaldırmak için tam izinleri vardır.</span><span class="sxs-lookup"><span data-stu-id="ddd85-160">Once confirmed, that person has full permissions to add and remove owners.</span></span> <span data-ttu-id="ddd85-161">(Onaylandı kadar **geçerli sahipleri** bu kişi için onay bekleyen bölümü gösterir.)</span><span class="sxs-lookup"><span data-stu-id="ddd85-161">(Until confirmed, the **Current Owners** section indicates pending approval for that person.)</span></span>
1. <span data-ttu-id="ddd85-162">(Olarak ne zaman sahipliği değişiklikleri veya bir paket yanlış hesabı altında yayımlanan) sahipliğini aktarma için yeni sahibin ekleyin ve sahipliği onaylanıp sonra bunlar, listeden kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ddd85-162">To transfer ownership (as when ownership changes or a package was published under the wrong account), add the new owner, and once they've confirmed ownership they can remove you from the list.</span></span>

<span data-ttu-id="ddd85-163">Bir şirket veya grup sahipliği atamak için uygun ekip üyelerine iletilen bir e-posta diğer adı kullanarak bir nuget.org hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ddd85-163">To assign ownership to a company or group, create a nuget.org account using an email alias that is forwarded to the appropriate team members.</span></span> <span data-ttu-id="ddd85-164">Örneğin, çeşitli Microsoft ASP.NET paketleri birlikte sahibi [microsoft](http://nuget.org/profiles/microsoft) ve [aspnet](http://nuget.org/profiles/aspnet) hesapları, hangi yalnızca gibi diğer adları.</span><span class="sxs-lookup"><span data-stu-id="ddd85-164">For example, various Microsoft ASP.NET packages are co-owned by the [microsoft](http://nuget.org/profiles/microsoft) and [aspnet](http://nuget.org/profiles/aspnet) accounts, which simply such aliases.</span></span>

### <a name="recovering-package-ownership"></a><span data-ttu-id="ddd85-165">Paket sahipliği kurtarma</span><span class="sxs-lookup"><span data-stu-id="ddd85-165">Recovering package ownership</span></span>

<span data-ttu-id="ddd85-166">Bazen, bir paket etkin bir sahip olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="ddd85-166">Occasionally, a package may not have an active owner.</span></span> <span data-ttu-id="ddd85-167">Örneğin, özgün sahibinin paket üreten şirket bıraktıysanız, nuget.org kimlik bilgileri kaybolur veya galerisinde önceki hataların bir paket ownerless sol.</span><span class="sxs-lookup"><span data-stu-id="ddd85-167">For example, the original owner may have left the company that produces the package, nuget.org credentials are lost, or earlier bugs in the gallery left a package ownerless.</span></span>

<span data-ttu-id="ddd85-168">Bir paketin gerçek sahibiyseniz ve sahipliği kazanmaya ihtiyacınız varsa kullanmak [kişi formu](https://www.nuget.org/policies/Contact) açıklayan NuGet takım durumunuza nuget.org üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ddd85-168">If you are the rightful owner of a package and need to regain ownership, use the [contact form](https://www.nuget.org/policies/Contact) on nuget.org to explain your situation to the NuGet team.</span></span> <span data-ttu-id="ddd85-169">Biz sonra varolan sahibi paketin proje URL'sini, Twitter, e-posta veya başka yöntemler aracılığıyla bulmaya çalışan dahil olmak üzere paketin, sahipliği doğrulamak için bir işlemi izleyin.</span><span class="sxs-lookup"><span data-stu-id="ddd85-169">We then follow a process to verify your ownership of the package, including trying to locate the existing owner through the package's Project URL, Twitter, email, or other means.</span></span> <span data-ttu-id="ddd85-170">Ancak tüm yöntemler başarısız olursa, sahibi olmak için yeni bir davet gönderebiliriz.</span><span class="sxs-lookup"><span data-stu-id="ddd85-170">But if all else fails, we can send you a new invite to become an owner.</span></span>