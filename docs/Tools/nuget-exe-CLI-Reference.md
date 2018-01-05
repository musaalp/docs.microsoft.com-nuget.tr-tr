---
title: "NuGet komut satırı arabirimi (CLI) başvurusu | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d777c424-0cf3-4bc0-8abd-7ca16c22192b
description: "CLI nuget.exe için komut satırı başvurusu dizini"
keywords: "nuget.exe başvurusu dizini, nuget.exe komut satırı arabirimi, nuget.exe CLI, nuget komutu"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3d1c3585d8bbf4c9bd9b50c8167e860594a42055
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-cli-reference"></a>NuGet CLI başvurusu

NuGet komut satırı arabirimi (CLI), `nuget.exe`, tam kapsamı yüklemek, oluşturmak, yayımlama ve proje dosyalarına herhangi bir değişiklik yapmadan paketlerini yönetmek için NuGet işlevselliği sağlar.

Herhangi bir komutu kullanmak için bir komut penceresi açın veya kabuk bash ardından Çalıştır `nuget` gibi ardından komut ve uygun seçenekleri `nuget help pack` (paketi komutunda yardımını görüntülemek için).

## <a name="installing-nugetexe"></a>Nuget.exe yükleme

[!INCLUDE[install-cli](../includes/install-cli.md)]

## <a name="availability"></a>Kullanılabilirlik

- Tüm komutlar Windows üzerinde kullanılabilir.
- Tüm komutları çalışmak [Mono üzerinde çalışan nuget.exe](../guides/install-nuget.md#mac-osx-and-linux) için belirtilen yerlerde dışındaki `pack`, `restore`, ve `update`.
- `pack`, `restore`, `delete`, `locals`, Ve `push` komutları Mac ve Linux üzerinden kullanılabilir de [dotnet CLI](dotnet-Commands.md). 

## <a name="commands-and-applicability"></a>Komutlar ve Uygulanabilirlik

Kullanılabilir komutlar ve paket oluşturma, paket tüketim ve/veya bir ana bilgisayara bir paket yayımlama için Uygulanabilirlik:

| Sık kullanılan komutlar | Geçerli rolleri | NuGet sürümü | Açıklama | 
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Oluşturma | 2.7+ | NuGet paket oluşturur bir `.nuspec` veya proje dosyası. Mono üzerinde çalışırken, bir proje dosyasından paket oluşturma desteklenmiyor. |
| [anında iletme](cli-ref-push.md) | Yayımlama | Tümü | Bir paket için paket kaynağı yayımlar. |
| [yapılandırma](cli-ref-config.md) | Tümü | Tümü | Alır veya NuGet yapılandırma değerlerini ayarlar. |
| [Yardım veya?](cli-ref-help.md) | Tümü | Tümü | Bilgi veya bir komutla ilgili Yardım yardımını görüntüler. |
| [Yerel öğeler](cli-ref-locals.md) | Tüketim | 3.3+ | Temizler çeşitli önbellekleri veya genel paketler klasörü paketleri listeler veya bu klasörleri tanımlar. |
| [geri yükleme](cli-ref-restore.md) | Tüketim | 2.7+ | Paket başvuru biçime tarafından başvurulan tüm paketler geri yükler. Mono üzerinde çalışırken, PackageReference biçimi kullanarak paketleri geri yüklenmesi desteklenmez. | 
| [setapikey](cli-ref-setapikey.md) | Yayımlama, tüketim | Tümü | Bu paket kaynağına erişimi için bir anahtar gerektirdiğinde verilen paket kaynağı için bir API anahtarı kaydeder. |
| [belirtimi](cli-ref-spec.md) | Oluşturma | Tümü | Oluşturan bir `.nuspec` dosya, bir Visual Studio Proje dosyası oluşturma belirteçleri kullanarak. |


| İkincil komutları | Geçerli rolleri | NuGet sürümü | Açıklama | 
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Yayımlama | 3.3+ | Bir paket hiyerarşik düzenini kullanarak bir HTTP olmayan paket kaynağı ekler. HTTP kaynakları için kullanmak *itme*. |
| [Sil](cli-ref-delete.md) | Yayımlama | Tümü | Bir paketi paket kaynağında unlists ya da kaldırır. |
| [Init](cli-ref-init.md) | Oluşturma | 3.3+ | Paketleri bir klasörden hiyerarşik düzenini kullanarak bir paket kaynağı ekler. |
| [Yükleme](cli-ref-install.md) | Tüketim | Tümü | Geçerli bir pakete bir yükler proje ancak projeleri değiştirmeyin veya dosyaları başvuru. |
| [Liste](cli-ref-list.md) | Tüketim, belki de yayımlama | Tümü | Belirli bir kaynaktan paketleri görüntüler. |
| [Yansıtma](cli-ref-mirror.md) | Yayımlama | 3.2 +'da kullanım dışıdır | Bir paketi ve bağımlılıklarını bir kaynaktan bir hedef havuz yansıtır. |
| [kaynakları](cli-ref-sources.md) | Tüketim, yayımlama | Tümü | Yapılandırma dosyalarında paket kaynaklarını yönetir. |
| [Güncelleştirme](cli-ref-update.md) | Tüketim | Tümü | Bir projenin paketler için en son sürümleri güncelleştirir. Mono üzerinde çalışırken desteklenmez. |

Farklı komutlar çeşitli kullanmak [ortam değişkenleri](cli-ref-environment-variables.md).

NuGet CLI komutları geçerli rolleri tarafından:

| Rol | Komutlar |
| --- | --- |
| Tüketim | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` | 
| Oluşturma | `config`, `help`, `init`, `pack`, `spec` |
| Yayımlama | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Örneğin, geliştiriciler paketleri, yalnızca kullanma ile ilgili yalnızca NuGet komutların bu alt anlamanız.

> [!Note]
> Komut seçenek adları büyük/küçük harfe duyarsızdır. Kullanım dışı bırakılmıştır seçenekleri bu başvurusunda gibi eklenmemiştir `NoPrompt` (değiştirilmiştir `NonInteractive`) ve `Verbose` (değiştirilmiştir `Verbosity`).