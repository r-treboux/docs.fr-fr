---
title: 210 - MessageThrottleExceeded
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 24ca08ea-c11c-4753-946e-98aa820f8711
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 299cc11dc4f6794b65761ad7da71bcf062c318db
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="210---messagethrottleexceeded"></a>210 - MessageThrottleExceeded
## <a name="properties"></a>Propriétés  
  
|||  
|-|-|  
|Id|210|  
|Mots clés|EndToEndMonitoring, HealthMonitoring, Dépannage, ServiceModel|  
|Niveau|Avertissement|  
|Canal|Microsoft-Windows-Application Server-Applications/Analyse|  
  
## <a name="description"></a>Description  
 Cet événement est émis lorsque l'un des trois accélérateurs de service principaux a été dépassé. Notez que cet événement est émis uniquement lors du premier dépassement de la limitation définie pour l'accélérateur. Par exemple, si la valeur de la limitation pour les appels simultanés est définie à 10, le onzième appel simultané produit un événement `MessageThrottleExceeded`. Le douzième appel ne provoque pas d'autre événement. En outre, l'activité qui tourne autour de la limitation ne provoque pas d'autre événement afin d'éviter un flux d'événements bruyant. Dans cet exemple, si deux appels sont effectués, cela correspond à 9 appels simultanés. Si par la suite, deux appels supplémentaires sont effectués, la valeur actuelle est à nouveau 11. Cela ne provoque aucun autre événement. Lorsque la valeur actuelle chute à 70 % de la limitation définie pour l'accélérateur, un événement différent est émis, indiquant que l'activité a ralenti. La prochaine activité qui dépasse la limitation provoque l'émission d'un autre événement `MessageThrottleExceeded`. Dans cet exemple, si la quantité d'appels simultanés descend à 7, puis remonte à 11, un autre événement `MessageThrottleExceeded` est émis.  
  
## <a name="message"></a>Message  
 La valeur '%1' de la limitation '%2' a été atteinte.  
  
## <a name="details"></a>Détails  
  
|Nom d'élément de données|Type d'élément de données|Description|  
|--------------------|--------------------|-----------------|  
|Nom de l'accélérateur|`xs:string`|Nom de l'accélérateur qui a été dépassé. `MaxConcurrentCalls`, `MaxConcurrentInstances` ou  `MaxConcurrentSessions`.|  
|Limitation|`xs:long`|Limitation configurée actuellement pour l'accélérateur.|  
|HostReference|`xs:string`|Pour les services hébergés par le Web, ce champ identifie de manière unique le service dans la hiérarchie Web. Son format est défini en tant que ' chemin d’accès virtuel de Site Web de nom d’Application &#124; Chemin d’accès virtuel de service &#124; ServiceName'. Exemple : ' Default Web Site/CalculatorApplication &#124;/CalculatorService.svc &#124; CalculatorService ».|  
|AppDomain|`xs:string`|Chaîne retournée par AppDomain.CurrentDomain.FriendlyName.|
