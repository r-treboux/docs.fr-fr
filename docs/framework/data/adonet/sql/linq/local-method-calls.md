---
title: "Appels de méthodes locaux"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: c34b5012-aee9-4994-9364-1d99d12b7463
caps.latest.revision: "2"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: d652072d5f2e0e0cfc74d627b573389864bca9dc
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2018
---
# <a name="local-method-calls"></a>Appels de méthodes locaux
Un appel de méthode local est un appel exécuté dans le modèle objet. Un appel de méthode distant est un appel que [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] traduit en SQL et est transmis au moteur de base de données pour l'exécution. Appels de méthode locaux sont nécessaires lorsque [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] ne peut pas traduire l’appel en SQL. Sinon, un <xref:System.InvalidOperationException> est levée.  
  
## <a name="example-1"></a>Exemple 1  
 Dans l'exemple suivant, une classe `Order` est mappée à la table Orders dans l'exemple de base de données Northwind. Une méthode d'instance locale a été ajoutée à la classe.  
  
 Dans Query1, le constructeur de la classe `Order` est exécuté localement. Dans Query2, si [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] a essayé de traduire `LocalInstanceMethod()` en SQL, la tentative échoue et une exception <xref:System.InvalidOperationException> est levée. Toutefois, comme [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fournit le support pour les appels de méthode locaux, Query2 ne lèvera pas d'exception.  
  
 [!code-csharp[DlinqLocalMethodCall#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqLocalMethodCall/cs/Program.cs#1)]
 [!code-vb[DlinqLocalMethodCall#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqLocalMethodCall/vb/Module1.vb#1)]  
  
 [!code-csharp[DlinqLocalMethodCall#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqLocalMethodCall/cs/northwind.cs#2)]
 [!code-vb[DlinqLocalMethodCall#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqLocalMethodCall/vb/northwind.vb#2)]  
  
## <a name="see-also"></a>Voir aussi  
 [Informations générales](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)
