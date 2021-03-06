---
title: NuGet kaldırma-Package PowerShell başvurusu
description: Visual Studio'da NuGet Paket Yöneticisi konsolunda paket kaldırma PowerShell komutunu referansı.
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551649"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a>Uninstall-Package (Visual Studio'da Paket Yöneticisi Konsolu)

*Bu konu içindeki komut açıklar [NuGet Paket Yöneticisi Konsolu](package-manager-console.md) Windows üzerinde Visual Studio'da. Genel PowerShell paket kaldırma komutu için bkz: [PowerShell PackageManagement başvuru](/powershell/module/packagemanagement/?view=powershell-6).*

Bir paket bağımlılıklarını isteğe bağlı olarak kaldırarak bir projeden kaldırır. Diğer paketleri bu pakete bağlıdır, komut sürece başarısız olur Force seçeneği belirtildi.

## <a name="syntax"></a>Sözdizimi

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

Diğer paketleri bu pakete bağlıdır, komut sürece başarısız olur Force seçeneği belirtildi.

## <a name="parameters"></a>Parametreler

| Parametre | Açıklama |
| --- | --- |
| Kimliği | (Gerekli) Kaldırmak için paket tanımlayıcısı. Kimliği anahtarın kendisinde, isteğe bağlıdır. |
| Sürüm | Kaldırmak için paket sürümünü şu anda yüklü sürümü için varsayılan olarak ayarlanıyor. |
| RemoveDependencies | Paket ve kullanılmayan bağımlılıkları kaldırın. Diğer bir deyişle, herhangi bir bağımlılık bağımlı başka bir paket varsa atlanır. |
| ProjectName | Projeden olduğu için varsayılan proje varsayılan olarak ayarlanıyor. Bu paketi kaldırın. |
| Zorla | Diğer paketleri bağımlı bile paketini kaldırılması için zorlar. |
| WhatIf | Kaldırma işlemini gerçekleştirmeden komutu çalıştırırken ne olacağını gösterir. |

Hiçbiri bu parametre ardışık düzen giriş veya joker karakterler kabul edin.

## <a name="common-parameters"></a>Ortak parametreleri

`Uninstall-Package` şunları desteklemektedir [ortak PowerShell parametrelerini](http://go.microsoft.com/fwlink/?LinkID=113216): hata ayıklama, hata eylemi, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, ayrıntılı, WarningAction ve WarningVariable.

## <a name="examples"></a>Örnekler

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
