---
title: "Validation basée sur le code impératif"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae12537c-455e-42b1-82f4-cea4c46c023e
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 79e50c9cc756915ffc1a2f376d6b46469c85dbf5
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/22/2017
---
# <a name="imperative-code-based-validation"></a>Validation basée sur le code impératif
La validation basée sur le code impératif offre un moyen simple de valider une activité ainsi que les activités dérivées de <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> et <xref:System.Activities.NativeActivity>. Le code de validation est ajouté à l'activité qui détermine les erreurs ou avertissements de validation ajoutés à l'activité.  
  
## <a name="using-code-based-validation"></a>Utilisation de la validation basée sur le code  
 La validation basée sur le code est prise en charge par les activités dérivées de <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> et <xref:System.Activities.NativeActivity>. Le code de validation peut être placé dans la substitution <xref:System.Activities.CodeActivity.CacheMetadata%2A>, et les erreurs ou avertissements de validation peuvent être ajoutés à l'argument de métadonnées. Dans l’exemple suivant, issu de la [une Validation de base](../../../docs/framework/windows-workflow-foundation/samples/basic-validation.md) exemple, si le `Cost` est supérieure à la `Price`, une erreur de validation est ajoutée aux métadonnées.  
  
> [!NOTE]
>  Notez que `Cost` et `Price` ne sont pas des arguments de l'activité, mais sont des propriétés définies au moment du design. C'est pourquoi leurs valeurs peuvent être validées dans la substitution <xref:System.Activities.CodeActivity.CacheMetadata%2A>. La valeur des données diffusées via un argument ne peut pas être validée au moment du design, car les données ne sont diffusées qu'au moment de l'exécution, mais des arguments d'activité peuvent être validés pour vérifier qu'ils sont liés à l'aide de l'attribut `RequiredArgument` et des groupes surchargés. Cet exemple de code voit l'attribut `RequiredArgument` de l'argument `Description`, et s'il n'est pas lié, une erreur de validation est générée. Les arguments obligatoires sont traités dans [requis des Arguments et des groupes surchargés](../../../docs/framework/windows-workflow-foundation/required-arguments-and-overload-groups.md).  
  
```csharp  
public sealed class CreateProduct : CodeActivity  
{  
    public double Price { get; set; }  
    public double Cost { get; set; }  
  
    // [RequiredArgument] attribute will generate a validation error   
    // if the Description argument is not set.  
    [RequiredArgument]  
    public InArgument<string> Description { get; set; }  
  
    protected override void CacheMetadata(CodeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        // Determine when the activity has been configured in an invalid way.  
        if (this.Cost > this.Price)  
        {  
            // Add a validation error with a custom message.  
            metadata.AddValidationError("The Cost must be less than or equal to the Price.");  
        }  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // Not needed for the sample.  
    }  
}  
```  
  
 Par défaut, une erreur de validation est ajoutée aux métadonnées lorsque <xref:System.Activities.CodeActivityMetadata.AddValidationError%2A> est appelé. Pour ajouter un avertissement de validation, utilisez la surcharge <xref:System.Activities.CodeActivityMetadata.AddValidationError%2A> qui prend <xref:System.Activities.Validation.ValidationError> et spécifiez que <xref:System.Activities.Validation.ValidationError> représente un avertissement en définissant la propriété <xref:System.Activities.Validation.ValidationError.IsWarning%2A>.  
  
 La validation a lieu lorsque, dans le Concepteur de Workflow, un workflow est modifié et que l'ensemble des erreurs ou avertissements de validation sont affichés. La validation se produit également au moment de l'exécution lorsqu'un workflow est appelé et si des erreurs de validation se produisent, <xref:System.Activities.InvalidWorkflowException> est levée par la logique de validation par défaut. [!INCLUDE[crabout](../../../includes/crabout-md.md)]appel de la validation et l’accès à des avertissements de validation ou d’erreurs, consultez [appel de Validation d’activité](../../../docs/framework/windows-workflow-foundation/invoking-activity-validation.md).  
  
 Toutes les exceptions levées à partir de <xref:System.Activities.CodeActivity.CacheMetadata%2A> ne sont pas traitées comme des erreurs de validation. Ces exceptions ne seront pas détectées par l'appel à <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> et doivent être gérées par l'appelant.  
  
 La validation basée sur le code est utile pour valider l’activité qui contient le code, mais elle n’offre pas de visibilité pour les autres activités du workflow. Validation de contraintes déclaratives offre la possibilité de valider les relations entre une activité et d’autres activités dans le flux de travail et est décrite dans le [contraintes déclaratives](../../../docs/framework/windows-workflow-foundation/declarative-constraints.md) rubrique.
