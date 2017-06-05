---
title: "Proc&#233;dure&#160;: contr&#244;ler la quantit&#233; de donn&#233;es li&#233;es r&#233;cup&#233;r&#233;es | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: efdc203e-3da9-4477-815e-54f10c3d7c6c
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Proc&#233;dure&#160;: contr&#244;ler la quantit&#233; de donn&#233;es li&#233;es r&#233;cup&#233;r&#233;es
Utilisez la méthode <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> pour spécifier quelles données associées à votre cible principale doivent être récupérées simultanément.  Par exemple, si vous savez que vous aurez besoin d'informations relatives aux commandes des clients, vous pouvez utiliser <xref:System.Data.Linq.DataLoadOptions.LoadWith%2A> pour vous assurer que les informations relatives aux commandes sont récupérées en même temps que les informations relatives au client.  Cette approche permet de ne provoquer qu'un seul envoi à la base de données pour les deux ensembles d'informations.  
  
> [!NOTE]
>  Vous pouvez récupérer des données en rapport avec la cible principale de votre requête en récupérant un produit croisé sous forme d'une grande projection, par exemple en récupérant des commandes lorsque vous ciblez des clients.  Cependant, cette approche présente souvent des inconvénients.  Par exemple, les résultats sont uniquement des projections et non des entités qui peuvent être modifiées et être rendues persistantes par [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]. Et vous pouvez récupérer une grande quantité de données dont vous n'avez pas besoin.  
  
## Exemple  
 Dans l'exemple suivant, toutes les `Orders` de tous les `Customers` dont la ville est London sont récupérés une fois la requête exécutée.  En conséquence, le fait d'accéder par la suite à la propriété `Orders` sur un objet `Customer` ne déclenche pas de nouvelle requête de la base de données.  
  
 [!code-csharp[System.Data.Linq.DataLoadOptions#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.dataloadoptions/cs/program.cs#2)]
 [!code-vb[System.Data.Linq.DataLoadOptions#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.dataloadoptions/vb/module1.vb#2)]  
  
## Voir aussi  
 [Interrogation de la base de données](../../../../../../docs/framework/data/adonet/sql/linq/querying-the-database.md)