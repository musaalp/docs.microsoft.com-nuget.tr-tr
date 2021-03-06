---
title: Genel bakış ve iş akışı, NuGet paketlerini kullanma
description: İşleminin diğer belirli bölümlerine bağlantılar içeren bir proje içinde NuGet paketlerini kullanma işlemine bir genel bakış.
author: karann-msft
ms.author: karann
ms.date: 03/22/2018
ms.topic: conceptual
ms.openlocfilehash: a5807a6895a76a7d6660d218b29e1d3a2802ca28
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545054"
---
# <a name="package-consumption-workflow"></a>Paket tüketim iş akışı

Nuget.org ve kuruluşunuzun oluşturabilirsiniz özel paket galeriler arasında on binlerce uygulama ve hizmetlerinizin kullanmak için çok yararlı paketleri bulabilirsiniz. Ancak kaynağı ne olursa olsun, bir paketi kullanan aynı genel iş akışını izler.

![Bir paket kaynağına giderek, bir paket bulma, bir projede yükleme ve ardından kullanarak bir ekleme akışı deyimi ve ' % s'paketi API çağrıları](media/Overview-01-GeneralFlow.png)

\* _Visual Studio ve dotnet.ex' yalnızca. Nuget yükleme komutu, proje dosyaları veya Packages.config dosyasının değiştirmez; Giriş el ile yönetilmesi gerekir._

Daha fazla ayrıntı için bkz. [bulma ve seçme paketleri](../consume-packages/finding-and-choosing-packages.md) ve [NuGet paketini yüklemek için farklı yollar](ways-to-install-a-package.md).

NuGet, ya da kaydı yüklü her paket kimliği ve sürüm numarasını hatırlar [ `packages.config` ](../reference/packages-config.md) ya da proje dosyası (kullanarak [PackageReference](../consume-packages/package-references-in-project-files.md)) proje türüne bağlı olarak ve NuGet sürümü. Bu Visual Studio yapılandırılabilir olsa NuGet ile 4.0 +, PackageReference tercih edilen, [Paket Yöneticisi kullanıcı Arabirimi seçenekleri](../tools/package-manager-ui.md). Herhangi bir durumda, projeniz için bağımlılıklar tam listesini görmek için herhangi bir zamanda uygun dosyasına bakabilirsiniz.

> [!Tip]
> Akıllıca lisans yazılımınızı, kullanmak istediğiniz her paket için her zaman denetleyin. Nuget.org bulduğunuz bir **lisans bilgilerini** her paketin açıklaması sayfasının sağ taraftaki bağlantı. Bir paketi lisans koşulları belirtmezse kullanarak doğrudan paket sahibiyle iletişime geçin **sahipleriyle temas** bağlantı paketi sayfasında. Microsoft hiçbir fikri mülkiyet, üçüncü taraf paketi sağlayıcılarından lisans değil ve üçüncü taraflarca sağlanan bilgileri sorumlu değildir.

Paketler yüklenirken, NuGet genellikle paket zaten önbelleğinden kullanılabilir olup olmadığını denetler. Üzerinde açıklandığı gibi bu önbellek komut satırından el ile temizleyebilirsiniz [genel paketleri ve önbellek klasörlerini yönetme](../consume-packages/managing-the-global-packages-and-cache-folders.md).

Ayrıca NuGet paket tarafından desteklenen hedef çerçeve proje ile uyumlu olduğundan emin olur. NuGet, paket uyumlu derlemeleri içermiyorsa, bir hata görüntüler. Bkz: [uyumsuz paket hatalarını çözme](dependency-resolution.md#resolving-incompatible-package-errors).

Proje kodunu bir kaynak havuzuna eklerken NuGet paketleri genellikle dahil değildir. Daha sonra bir depoyu kopyalamanın veya aksi takdirde derleme aracılarınızda Visual Studio Team Services gibi sistemleri dahil olmak üzere proje alma kullanıcıların bir derleme çalıştırılmadan önce gerekli paketleri geri yüklemeniz gerekir:

![Bir depoyu kopyalama ve bir geri yükleme komutunu kullanarak NuGet paketlerini geri akışı](media/Overview-02-RestoreFlow.png)

[Paket geri yükleme](../consume-packages/package-restore.md) proje dosyasında bilgileri kullanır veya `packages.config` tüm bağımlılıkları yeniden yüklemek için. Olduğunu işlem farklılıkları karmaşık açıklandığı unutmayın [bağımlılık çözümlemesi](../consume-packages/dependency-resolution.md). Genellikle paketleri otomatik olarak geri yükler ve çözüm düzeyinde komut gösterildiği sağlayan Visual Studio bağlamında zaten işiniz konsolu ile olduğunuz için Ayrıca, yukarıdaki diyagramda restore komutu için Paket Yöneticisi konsolu göstermez. .

Bazen bağımlılıkları da yeniden yükleyebilir bir projede zaten dahil edilmiştir paketleri yeniden yüklemek gereklidir. Bunu yapmak kolaydır `nuget reinstall` komut veya NuGet Paket Yöneticisi konsolu. Ayrıntılar için bkz [Reinstalling ve güncelleştirme paketleri](../consume-packages/reinstalling-and-updating-packages.md).

Son olarak, NuGet'ın davranışını tarafından yönlendirilen `Nuget.Config` dosyaları. Birden çok dosya belirli ayarları farklı düzeylerde merkezileştirmek için açıklandığı gibi kullanılabilir [NuGet davranışını yapılandırma](../consume-packages/configuring-nuget-behavior.md).

NuGet paketleri ile üretken, kodlamanın keyfini çıkarın!
