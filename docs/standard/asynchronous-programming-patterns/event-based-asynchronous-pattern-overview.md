---
title: "Event-based Asynchronous Pattern Overview | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Event-based Asynchronous Pattern"
  - "ProgressChangedEventArgs class"
  - "BackgroundWorker component"
  - "events [.NET Framework], asynchronous"
  - "Asynchronous Pattern"
  - "AsyncOperationManager class"
  - "threading [.NET Framework], asynchronous features"
  - "AsyncOperation class"
  - "AsyncCompletedEventArgs class"
ms.assetid: 792aa8da-918b-458e-b154-9836b97735f3
caps.latest.revision: 19
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# Event-based Asynchronous Pattern Overview
Les applications qui effectuent de nombreuses tâches simultanément tout en réagissant aux interventions de l'utilisateur nécessitent souvent une conception utilisant plusieurs threads.  L'espace de noms <xref:System.Threading> fournit tous les outils nécessaires à la création d'applications multithread de hautes performances, mais l'utilisation de ces outils suppose une connaissance approfondie de l'ingénierie logicielle multithread.  Pour les applications multithread relativement simples, le composant <xref:System.ComponentModel.BackgroundWorker> fournit une solution simple.  Pour les applications asynchrones plus sophistiquées, envisagez l'implémentation d'une classe obéissant au modèle asynchrone basé sur les événements.  
  
 Le modèle asynchrone basé sur les événements permet de profiter des avantages des applications multithread tout en masquant de nombreux problèmes complexes inhérents à la conception multithread.  L'utilisation d'une classe prenant en charge ce modèle peut vous permettre :  
  
-   d'effectuer, « en arrière\-plan », des tâches de longue durée, telles que des téléchargements et des opérations de base de données, sans interrompre votre application ;  
  
-   d'exécuter plusieurs opérations simultanément, en recevant des notifications quand chacune d'elles se termine ;  
  
-   d'attendre que les ressources soient disponibles sans arrêter \(« bloquer »\) votre application ;  
  
-   de communiquer avec les opérations asynchrones en attente à l'aide du modèle d'événements et de délégués connu.  Pour plus d'informations sur l'utilisation des gestionnaires d'événements et des délégués, voir [Événements](../../../docs/standard/events/index.md).  
  
 Une classe prenant en charge le modèle asynchrone basé sur les événements possède une ou plusieurs méthodes nommées *nom\_méthode*`Async`.  Ces méthodes peuvent refléter des versions synchrones qui exécutent la même opération sur le thread actuel.  La classe peut également posséder un événement *nom\_méthode*`Completed` et une méthode *nom\_méthode*`AsyncCancel` \(ou simplement `CancelAsync`\).  
  
 <xref:System.Windows.Forms.PictureBox> est un composant courant qui prend en charge le modèle asynchrone basé sur les événements.  Vous pouvez télécharger une image de façon synchrone en appelant sa méthode <xref:System.Windows.Forms.PictureBox.Load%2A>, mais si l'image est grande ou que la connexion réseau est lente, votre application s'arrête \(« se bloque »\) jusqu'à ce que l'opération de téléchargement soit terminée et que l'appel à <xref:System.Windows.Forms.PictureBox.Load%2A> soit retourné.  
  
 Si vous souhaitez que votre application continue de s'exécuter pendant le chargement de l'image, vous pouvez appeler la méthode <xref:System.Windows.Forms.PictureBox.LoadAsync%2A> et gérer l'événement <xref:System.Windows.Forms.PictureBox.LoadCompleted> tout comme vous le feriez pour tout autre événement.  Quand vous appelez la méthode <xref:System.Windows.Forms.PictureBox.LoadAsync%2A>, l'exécution de votre application se poursuit pendant que le téléchargement s'effectue sur un thread séparé \(« en arrière\-plan »\).  Votre gestionnaire d'événements est appelé quand l'opération de chargement d'image est terminée, et peut examiner le paramètre <xref:System.ComponentModel.AsyncCompletedEventArgs> pour déterminer si le téléchargement s'est déroulé correctement.  
  
 Le modèle asynchrone basé sur les événements nécessite qu'une opération asynchrone puisse être annulée ; le contrôle <xref:System.Windows.Forms.PictureBox> prend en charge cette exigence avec sa méthode <xref:System.Windows.Forms.PictureBox.CancelAsync%2A>.  L'appel de <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> soumet une demande d'arrêt du téléchargement en attente et, quand la tâche est annulée, l'événement <xref:System.Windows.Forms.PictureBox.LoadCompleted> est déclenché.  
  
> [!CAUTION]
>  Comme il est possible que le téléchargement se termine au moment où la demande <xref:System.Windows.Forms.PictureBox.CancelAsync%2A> est effectuée, <xref:System.ComponentModel.AsyncCompletedEventArgs.Cancelled%2A> peut ne pas refléter la demande d'annulation.  Il s'agit d'une *condition de concurrence* qui est un problème courant dans la programmation multithread.  Pour plus d'informations sur les problèmes relatifs à la programmation multithread, voir [Managed Threading Best Practices](../../../docs/standard/threading/managed-threading-best-practices.md).  
  
## Caractéristiques du modèle asynchrone basé sur les événements  
 Le modèle asynchrone basé sur les événements peut prendre plusieurs formes selon la complexité des opérations prises en charge par une classe particulière.  Les classes les plus simples peuvent avoir une seule méthode *nom\_méthode*`Async` et un événement *nom\_méthode*`Completed` correspondant.  Les classes plus complexes peuvent avoir plusieurs méthodes *nom\_méthode*`Async`, chacune avec un événement *nom\_méthode*`Completed` correspondant, ainsi que des versions synchrones de ces méthodes.  Les classes peuvent éventuellement prendre en charge l'annulation, le rapport de progression et les résultats incrémentiels pour chaque méthode asynchrone.  
  
 Une méthode asynchrone peut également prendre en charge plusieurs appels en attente \(plusieurs appels simultanés\), ce qui permet à votre code de l'appeler autant de fois que nécessaire avant de terminer d'autres opérations en attente.  La gestion correcte de cette situation peut nécessiter que votre application effectue le suivi de l'achèvement de chaque opération.  
  
### Exemples du modèle asynchrone basé sur les événements  
 Les composants <xref:System.Media.SoundPlayer> et <xref:System.Windows.Forms.PictureBox> représentent des implémentations simples du modèle asynchrone basé sur les événements.  Les composants <xref:System.Net.WebClient> et <xref:System.ComponentModel.BackgroundWorker> représentent des implémentations plus complexes de ce modèle.  
  
 Voici un exemple de déclaration de classe conforme au modèle :  
  
```vb  
Public Class AsyncExample  
    ' Synchronous methods.  
    Public Function Method1(ByVal param As String) As Integer   
    Public Sub Method2(ByVal param As Double)   
  
    ' Asynchronous methods.  
    Overloads Public Sub Method1Async(ByVal param As String)   
    Overloads Public Sub Method1Async(ByVal param As String, ByVal userState As Object)   
    Public Event Method1Completed As Method1CompletedEventHandler  
  
    Overloads Public Sub Method2Async(ByVal param As Double)   
    Overloads Public Sub Method2Async(ByVal param As Double, ByVal userState As Object)   
    Public Event Method2Completed As Method2CompletedEventHandler  
  
    Public Sub CancelAsync(ByVal userState As Object)   
  
    Public ReadOnly Property IsBusy () As Boolean  
  
    ' Class implementation not shown.  
End Class  
```  
  
```csharp  
public class AsyncExample  
{  
    // Synchronous methods.  
    public int Method1(string param);  
    public void Method2(double param);  
  
    // Asynchronous methods.  
    public void Method1Async(string param);  
    public void Method1Async(string param, object userState);  
    public event Method1CompletedEventHandler Method1Completed;  
  
    public void Method2Async(double param);  
    public void Method2Async(double param, object userState);  
    public event Method2CompletedEventHandler Method2Completed;  
  
    public void CancelAsync(object userState);  
  
    public bool IsBusy { get; }  
  
    // Class implementation not shown.  
}  
```  
  
 La classe `AsyncExample` fictive possède deux méthodes qui prennent en charge les appels synchrones et asynchrones.  Les surcharges synchrones se comportent comme tout appel de méthode et exécutent l'opération sur le thread appelant ; si l'opération est de longue durée, le délai de retour de l'appel peut être important.  Les surcharges asynchrones démarrent l'opération sur un autre thread, puis elles sont retournées immédiatement, permettant au thread appelant de continuer pendant l'exécution de l'opération « en arrière\-plan ».  
  
### Surcharges de méthode asynchrone  
 Il existe potentiellement deux surcharges pour les opérations asynchrones : l'appel unique et les appels multiples.  Ces deux surcharges se distinguent par leurs signatures de méthode : la surcharge d'appels multiples possède un paramètre supplémentaire appelé `userState`.  Elle permet à votre code d'appeler `Method1Async(string param, object userState)` plusieurs fois sans attendre que les opérations asynchrones en attente se terminent.  En revanche, si vous tentez d'appeler `Method1Async(string param)` avant qu'un appel antérieur soit terminé, la méthode lève une <xref:System.InvalidOperationException>.  
  
 Le paramètre `userState` pour les surcharges d'appels multiples vous permet de différencier les opérations asynchrones.  Vous fournissez une valeur unique \(par exemple, un GUID ou un code de hachage\) pour chaque appel à  `Method1Async(string param, object userState)`, et quand chaque opération est terminée, votre gestionnaire d'événements peut déterminer l'instance de l'opération qui a déclenché l'événement d'achèvement.  
  
### Suivi des opérations en attente  
 Si vous utilisez les surcharges d'appels multiples, votre code doit conserver une trace des objets `userState` \(ID de tâche\) pour les tâches en attente.  Pour chaque appel à  `Method1Async(string param, object userState)`, vous générez normalement un nouvel objet `userState` unique et l'ajoutez à une collection.  Quand la tâche correspondant à cet objet `userState` déclenche l'événement d'achèvement, l'implémentation de votre méthode d'achèvement examine <xref:System.ComponentModel.AsyncCompletedEventArgs.UserState%2A?displayProperty=fullName> et le supprime de votre collection.  Utilisé de cette manière, le paramètre `userState` joue le rôle d'un ID de tâche.  
  
> [!NOTE]
>  Vous devez fournir une valeur unique pour `userState` dans vos appels aux surcharges d'appels multiples.  Les ID de tâche non uniques conduisent la classe asynchrone à lever une <xref:System.ArgumentException>.  
  
### Annulation des opérations en attente  
 Il est important de pouvoir annuler des opérations asynchrones à tout moment avant leur achèvement.  Les classes qui implémentent le modèle asynchrone basé sur les événements ont une méthode `CancelAsync` \(s'il existe une seule méthode asynchrone\) ou une méthode *nom\_méthode*`AsyncCancel` \(s'il existe plusieurs méthodes asynchrones\).  
  
 Les méthodes qui autorisent les appels multiples acceptent un paramètre `userState`, qui peut être utilisé pour assurer le suivi de la durée de vie de chaque tâche.  `CancelAsync` accepte un paramètre `userState` qui vous permet d'annuler des tâches en attente particulières.  
  
 Les méthodes qui prennent en charge une seule opération en attente à la fois, comme `Method1Async(string param)`, ne sont pas annulables.  
  
### Réception des mises à jour de progression et des résultats incrémentiels  
 Une classe obéissant au modèle asynchrone basé sur les événements peut éventuellement fournir un événement pour assurer le suivi de la progression et des résultats incrémentiels.  Celui\-ci est généralement appelé `ProgressChanged` ou *nom\_méthode*`ProgressChanged`, et son gestionnaire d'événements correspondant accepte un paramètre <xref:System.ComponentModel.ProgressChangedEventArgs>.  
  
 Le gestionnaire d'événements pour l'événement `ProgressChanged` peut examiner la propriété <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A?displayProperty=fullName> afin de déterminer le pourcentage d'exécution d'une tâche asynchrone.  Cette propriété est comprise entre 0 et 100 et peut être utilisée pour mettre à jour la propriété <xref:System.Windows.Forms.ProgressBar.Value%2A> d'une <xref:System.Windows.Forms.ProgressBar>.  Si plusieurs opérations asynchrones sont en attente, vous pouvez utiliser la propriété <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A?displayProperty=fullName> pour distinguer l'opération qui signale la progression.  
  
 Certaines classes peuvent signaler des résultats incrémentiels au fur et à mesure que les opérations asynchrones sont exécutées.  Ces résultats sont stockés dans une classe dérivant de <xref:System.ComponentModel.ProgressChangedEventArgs> et apparaissent sous forme de propriétés dans la classe dérivée.  Vous pouvez accéder à ces résultats dans le gestionnaire d'événements pour l'événement `ProgressChanged`, tout comme vous accéderiez à la propriété <xref:System.ComponentModel.ProgressChangedEventArgs.ProgressPercentage%2A>.  Si plusieurs opérations asynchrones sont en attente, vous pouvez utiliser la propriété <xref:System.ComponentModel.ProgressChangedEventArgs.UserState%2A> pour distinguer l'opération qui signale des résultats incrémentiels.  
  
## Voir aussi  
 <xref:System.ComponentModel.ProgressChangedEventArgs>   
 <xref:System.ComponentModel.BackgroundWorker>   
 <xref:System.ComponentModel.AsyncCompletedEventArgs>   
 [How to: Use Components That Support the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)   
 [Comment : exécuter une opération en arrière\-plan](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Comment : implémenter un formulaire qui utilise une opération d'arrière\-plan](../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [Multithreaded Programming with the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)   
 [Meilleures pratiques pour implémenter le modèle asynchrone basé sur des événements](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)   
 [Deciding When to Implement the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)