---
title: "NuGet 2.8.6 sürüm notları | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Bilinen sorunlar, hata düzeltmeleri, eklenen özellikleri ve dcr NuGet 2.8.6 dahil etmek için sürüm notları."
keywords: "Özellikler, dcr bilinen sorunlar, NuGet 2.8.6 sürüm notları, hata düzeltmeleri eklendi"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f33c1edd3ef703a8cd97b7bdd97c37e12426aafa
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-286-release-notes"></a>NuGet 2.8.6 sürüm notları

[NuGet 2.8.5 sürüm notları](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Sürüm Notları](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 yayımlanan 20 Temmuz 2015 bizim 2.8.5 için ikincil bir güncelleştirme olarak bazı VSIX hedeflenen düzeltmeler ve iyileştirmeler Windows 10 UWP geliştirme modeli desteğiyle teslim edilebilir paketleri destekler.

NuGet Paket Yöneticisi uzantısı'nın bu sürümü yalnızca Visual Studio 2013 için destek sağlar.

Bu sürümde, NuGet Paket Yöneticisi iletişim için eklenen destek vardı:

* Windows 10 uygulaması geliştirme desteklemek için UAP hedef Framework ad kullanıma sunuldu.
* NuGet Protokolü sürüm 3 uç noktaları
* Desteği [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) depo kaynakları protocolVersion özniteliği. Varsayılan değer "2".
* Gerekli Paket sürümü yerel önbellekte kullanılabilir değilse, uzak depoya geri dönmeden