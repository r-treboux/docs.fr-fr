---
title: "Importation de métadonnées personnalisées pour une extension WCF"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 78beb28f-408a-4c75-9c3c-caefe9595b1a
caps.latest.revision: "10"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 9208a73f6a35e4c05ab9be612491f3f7db792a5b
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="importing-custom-metadata-for-a-wcf-extension"></a>Importation de métadonnées personnalisées pour une extension WCF
Dans [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], l'importation de métadonnées est le processus de génération d'une représentation abstraite d'un service ou de ses composants à partir de ses métadonnées. Par exemple, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] peut importer des instances <xref:System.ServiceModel.Description.ServiceEndpoint>, des instances <xref:System.ServiceModel.Channels.Binding> ou des instances <xref:System.ServiceModel.Description.ContractDescription> à partir d'un document WSDL pour un service. Pour importer des métadonnées de service dans [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], utilisez une implémentation de la classe abstraite <xref:System.ServiceModel.Description.MetadataImporter?displayProperty=nameWithType>. Les types qui dérivent de la classe <xref:System.ServiceModel.Description.MetadataImporter> implémentent la prise en charge de l'importation des formats de métadonnées qui tirent parti de la logique d'importation WS-Policy dans [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Les métadonnées personnalisées sont composées d'éléments XML que les importateurs de métadonnées fournis par le système ne peuvent pas importer. En général, cela inclut des extensions WSDL personnalisées et des assertions de stratégie personnalisées.  
  
 Cette section décrit comment importer des extensions WSDL et des assertions de stratégie personnalisées. Elle ne traite pas du processus d'importation lui-même. Pour plus d’informations sur la façon d’utiliser les types d’exportent et importer des métadonnées que les métadonnées sont personnalisé ou système pris en charge, consultez [exportation et importation de métadonnées](../../../../docs/framework/wcf/feature-details/exporting-and-importing-metadata.md).  
  
## <a name="overview"></a>Vue d'ensemble  
 Le type <xref:System.ServiceModel.Description.WsdlImporter?displayProperty=nameWithType> est l'implémentation de la classe abstraite <xref:System.ServiceModel.Description.MetadataImporter> fournie avec [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Le type <xref:System.ServiceModel.Description.WsdlImporter> importe des métadonnées WSDL avec les stratégies attachées fournies dans un objet <xref:System.ServiceModel.Description.MetadataSet?displayProperty=nameWithType>. Les assertions de stratégie et les extensions WSDL que les importateurs par défaut ne reconnaissent pas sont passées aux stratégies personnalisées inscrites et aux importateurs WSDL à des fins d’importation. En général, les importateurs sont implémentés pour prendre en charge les éléments de liaison définis par l'utilisateur ou pour modifier le contrat importé.  
  
 Cette section décrit :  
  
1.  Comment implémenter et utiliser l'interface <xref:System.ServiceModel.Description.IWsdlImportExtension?displayProperty=nameWithType>, qui expose les données WSDL aux importateurs personnalisés avant la génération des descriptions et la génération du code. Vous pouvez utiliser cette interface pour examiner ou modifier les types de description et la compilation de code effectuée à l'aide d'un ensemble donné de métadonnées.  
  
2.  Comment implémenter et utiliser l'interface <xref:System.ServiceModel.Description.IPolicyImportExtension?displayProperty=nameWithType>, qui expose des assertions de stratégie aux importateurs avant la génération d'objets de description. Vous pouvez utiliser cette interface pour examiner ou modifier la liaison ou le contrat selon les stratégies téléchargées.  
  
 Pour plus d’informations sur l’exportation WSDL personnalisée et les assertions de stratégie, consultez [exportation des métadonnées personnalisées pour une Extension WCF](../../../../docs/framework/wcf/extending/exporting-custom-metadata-for-a-wcf-extension.md).  
  
## <a name="importing-custom-wsdl-extensions"></a>Importation d’extensions WSDL personnalisées  
 Pour ajouter la prise en charge de l'importation d'extensions WSDL, implémentez l'interface <xref:System.ServiceModel.Description.IWsdlImportExtension>, puis ajoutez votre implémentation à la propriété <xref:System.ServiceModel.Description.WsdlImporter.WsdlImportExtensions%2A>. Le <xref:System.ServiceModel.Description.WsdlImporter> peut également charger des implémentations de l'interface <xref:System.ServiceModel.Description.IWsdlImportExtension> inscrite dans votre fichier de configuration d'application. Notez que plusieurs importateurs WSDL sont inscrits par défaut et que l'ordre des importateurs WSDL inscrits est significatif.  
  
 Lorsque l'importateur WSDL personnalisé est chargé et utilisé par le <xref:System.ServiceModel.Description.WsdlImporter>, la méthode <xref:System.ServiceModel.Description.IWsdlImportExtension.BeforeImport%2A> est d'abord appelée afin de permettre la modification des métadonnées avant l'importation. Les contrats sont ensuite importés, après quoi la méthode <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportContract%2A> est appelée afin de permettre la modification des contrats importés à partir des métadonnées. Pour finir, la méthode <xref:System.ServiceModel.Description.IWsdlImportExtension.ImportEndpoint%2A> est appelée afin de permettre la modification des points de terminaison importés.  
  
 Pour plus d’informations, consultez [Comment : importer personnalisé WSDL](../../../../docs/framework/wcf/extending/how-to-import-custom-wsdl.md).  
  
### <a name="importing-custom-policy-assertions"></a>Importation d'assertions de stratégie personnalisées  
 Le <xref:System.ServiceModel.Description.WsdlImporter> type et la [ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) gérer automatiquement le traitement de divers types d’assertion de stratégie dans les expressions de stratégie jointes aux documents WSDL. Ces outils recueillent, normalisent et fusionnent les expressions de stratégie jointes aux liaisons WSDL et aux ports WSDL.  
  
 Pour ajouter la prise en charge de l'importation d'assertions de stratégie personnalisées, implémentez l'interface <xref:System.ServiceModel.Description.IPolicyImportExtension>, puis ajoutez votre implémentation à la propriété <xref:System.ServiceModel.Description.MetadataImporter.PolicyImportExtensions%2A>. Le <xref:System.ServiceModel.Description.MetadataImporter> peut également charger des implémentations de l'interface <xref:System.ServiceModel.Description.IPolicyImportExtension> inscrite dans votre fichier de configuration d'application. Notez que plusieurs importateurs de stratégies sont inscrits par défaut et que l'ordre des importateurs de stratégies inscrits est significatif.  
  
 Le système de métadonnées appelle à plusieurs reprises la méthode <xref:System.ServiceModel.Description.IPolicyImportExtension.ImportPolicy%2A?displayProperty=nameWithType> sur toutes les extensions d'importation de stratégie inscrites pour chaque combinaison d'alternatives de stratégie jointe aux objets de stratégie de message, d'opération et de point de terminaison. Lors de l’importation d’un port WSDL, les stratégies jointes au port et à la liaison WSDL correspondante sont fusionnées avant l’appel des extensions d’importation de stratégie. Les alternatives de stratégie sont rendues accessibles par le biais d'un <xref:System.ServiceModel.Description.PolicyConversionContext> en tant qu'objets <xref:System.ServiceModel.Description.PolicyAssertionCollection>. Chaque <xref:System.ServiceModel.Description.PolicyAssertionCollection> est une collection d'assertions de stratégie représentés par des objets <xref:System.Xml.XmlElement>.  
  
 Les propriétés <xref:System.ServiceModel.Description.PolicyConversionContext.Contract%2A> et <xref:System.ServiceModel.Description.PolicyConversionContext.BindingElements%2A> sur l'objet <xref:System.ServiceModel.Description.PolicyConversionContext> exposent les objets <xref:System.ServiceModel.Description.ContractDescription> et <xref:System.ServiceModel.Channels.BindingElement> importés à partir du WSDL. Les extensions d'importation de stratégie traitent les assertions de stratégie en recherchant les instances d'un type d'assertion de stratégie particulier, en apportant les modifications correspondantes aux objets <xref:System.ServiceModel.Description.ContractDescription> ou <xref:System.ServiceModel.Channels.BindingElement> et en supprimant ensuite les assertions de stratégie de l'instance <xref:System.ServiceModel.Description.PolicyAssertionCollection> correspondante.  
  
 L'attribut `wsp:Optional` et les expressions de stratégie imbriquées n'étant pas normalisés, les extensions d'importation de stratégie doivent gérer ces constructions de stratégie. De plus, les extensions d'importation de stratégie pouvant être appelées plusieurs fois avec les mêmes objets <xref:System.ServiceModel.Description.ContractDescription> et <xref:System.ServiceModel.Channels.BindingElement>, les extensions d'importation de stratégie doivent être fiables envers ce comportement.  
  
> [!IMPORTANT]
>  Des métadonnées non valides ou incorrectes peuvent être passées à l'importateur. Assurez-vous que les importateurs personnalisés sont fiables à toutes les formes de XML.  
  
## <a name="see-also"></a>Voir aussi  
 [Guide pratique pour importer un WSDL personnalisé](../../../../docs/framework/wcf/extending/how-to-import-custom-wsdl.md)  
 [Guide pratique pour importer des assertions de stratégie personnalisées](../../../../docs/framework/wcf/extending/how-to-import-custom-policy-assertions.md)  
 [Guide pratique pour écrire une extension pour le ServiceContractGenerator](../../../../docs/framework/wcf/extending/how-to-write-an-extension-for-the-servicecontractgenerator.md)
