---
title: "Fonctions locales (Guide de programmation C#)"
ms.date: 2017-06-14
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- local functions [C#]
author: rpetrusha
ms.author: ronpet
ms.translationtype: HT
ms.sourcegitcommit: 4582cb0ee091526423cce3fc1d8243029f34f59c
ms.openlocfilehash: 069a6411e3d89fa1c2dba57f0b83badff1342763
ms.contentlocale: fr-fr
ms.lasthandoff: 08/16/2017

---
# <a name="local-functions-c-programming-guide"></a><span data-ttu-id="fa24b-102">Fonctions locales (Guide de programmation C#)</span><span class="sxs-lookup"><span data-stu-id="fa24b-102">Local functions (C# Programming Guide)</span></span>

<span data-ttu-id="fa24b-103">À compter de C# 7, C# prend en charge les *fonctions locales*.</span><span class="sxs-lookup"><span data-stu-id="fa24b-103">Starting with C# 7, C# supports *local functions*.</span></span> <span data-ttu-id="fa24b-104">Les fonctions locales sont des méthodes privées d’un type qui sont imbriqués dans un autre membre.</span><span class="sxs-lookup"><span data-stu-id="fa24b-104">Local functions are private methods of a type that are nested in another member.</span></span> <span data-ttu-id="fa24b-105">Elles ne peuvent être appelées qu’à partir de leur membre conteneur.</span><span class="sxs-lookup"><span data-stu-id="fa24b-105">They can only be called from their containing member.</span></span> <span data-ttu-id="fa24b-106">Les fonctions locales peuvent être déclarées et appelées dans et à partir des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fa24b-106">Local functions can be declared in and called from:</span></span>

- <span data-ttu-id="fa24b-107">Méthodes, tout particulièrement les méthodes iterator et async</span><span class="sxs-lookup"><span data-stu-id="fa24b-107">Methods, especially iterator methods and async methods</span></span>
- <span data-ttu-id="fa24b-108">Constructeurs</span><span class="sxs-lookup"><span data-stu-id="fa24b-108">Constructors</span></span>
- <span data-ttu-id="fa24b-109">Accesseurs de propriété</span><span class="sxs-lookup"><span data-stu-id="fa24b-109">Property accessors</span></span>
- <span data-ttu-id="fa24b-110">Accesseurs d’événement</span><span class="sxs-lookup"><span data-stu-id="fa24b-110">Event accessors</span></span>
- <span data-ttu-id="fa24b-111">Méthodes anonymes</span><span class="sxs-lookup"><span data-stu-id="fa24b-111">Anonymous methods</span></span>
- <span data-ttu-id="fa24b-112">Expressions lambda</span><span class="sxs-lookup"><span data-stu-id="fa24b-112">Lambda expressions</span></span>
- <span data-ttu-id="fa24b-113">Finaliseurs</span><span class="sxs-lookup"><span data-stu-id="fa24b-113">Finalizers</span></span>
- <span data-ttu-id="fa24b-114">Autres fonctions locales</span><span class="sxs-lookup"><span data-stu-id="fa24b-114">Other local functions</span></span>

<span data-ttu-id="fa24b-115">En revanche, les fonctions locales ne peuvent pas être déclarées à l’intérieur d’un membre expression-bodied.</span><span class="sxs-lookup"><span data-stu-id="fa24b-115">However, local functions can't be declared inside an expression-bodied member.</span></span>

> [!NOTE]
> <span data-ttu-id="fa24b-116">Dans certains cas, vous pouvez utiliser une expression lambda pour implémenter la fonctionnalité également prise en charge par une fonction locale.</span><span class="sxs-lookup"><span data-stu-id="fa24b-116">In some cases, you can use a lambda expression to implement functionality also supported by a local function.</span></span> <span data-ttu-id="fa24b-117">Pour obtenir une comparaison, consultez [Fonctions locales comparées aux expressions lambda](../../local-functions-vs-lambdas.md).</span><span class="sxs-lookup"><span data-stu-id="fa24b-117">For a comparison, see [Local functions compared to Lambda expressions](../../local-functions-vs-lambdas.md).</span></span>

<span data-ttu-id="fa24b-118">Les fonctions locales permettent de clarifier l’objectif de votre code.</span><span class="sxs-lookup"><span data-stu-id="fa24b-118">Local functions make the intent of your code clear.</span></span> <span data-ttu-id="fa24b-119">Quiconque lisant votre code peut voir que la méthode ne peut pas être appelée, sauf par la méthode conteneur.</span><span class="sxs-lookup"><span data-stu-id="fa24b-119">Anyone reading you code can see that the method is not callable except by the containing method.</span></span> <span data-ttu-id="fa24b-120">Pour les projets d’équipe, elles empêchent aussi à un autre développeur d’appeler par inadvertance la méthode directement à partir d’un autre emplacement dans la classe ou le struct.</span><span class="sxs-lookup"><span data-stu-id="fa24b-120">For team projects, they also make it impossible for another developer to mistakenly call the method directly from elsewhere in the class or stuct.</span></span>
 
## <a name="local-function-syntax"></a><span data-ttu-id="fa24b-121">Syntaxe des fonctions locales</span><span class="sxs-lookup"><span data-stu-id="fa24b-121">Local function syntax</span></span>

<span data-ttu-id="fa24b-122">Une fonction locale est définie en tant que méthode imbriquée à l’intérieur d’un membre conteneur.</span><span class="sxs-lookup"><span data-stu-id="fa24b-122">A local function is defined as a nested method inside a containing member.</span></span> <span data-ttu-id="fa24b-123">Sa définition présente la syntaxe suivante :</span><span class="sxs-lookup"><span data-stu-id="fa24b-123">Its definition has the following syntax:</span></span>

```txt
<modifiers: async | unsafe> <return-type> <method-name> <parameter-list>
```

<span data-ttu-id="fa24b-124">Les fonctions locales peuvent utiliser les modificateurs [async](../../language-reference/keywords/async.md) et [unsafe](../../language-reference/keywords/unsafe.md).</span><span class="sxs-lookup"><span data-stu-id="fa24b-124">Local functions can use the [async](../../language-reference/keywords/async.md) and [unsafe](../../language-reference/keywords/unsafe.md) modifiers.</span></span> 

<span data-ttu-id="fa24b-125">Notez que toutes les variables locales définies dans le membre conteneur, y compris ses paramètres de méthode, sont accessibles dans la fonction locale.</span><span class="sxs-lookup"><span data-stu-id="fa24b-125">Note that all local variables that are defined in the containing member, including its method parameters, are accessible in the local function.</span></span> 

<span data-ttu-id="fa24b-126">Contrairement à la définition d’une méthode, la définition d’une fonction locale ne peut pas inclure les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="fa24b-126">Unlike a method definition, a local function definition cannot include the following elements:</span></span>

- <span data-ttu-id="fa24b-127">Le modificateur d’accès de membre.</span><span class="sxs-lookup"><span data-stu-id="fa24b-127">The member access modifier.</span></span> <span data-ttu-id="fa24b-128">Comme toutes les fonctions locales sont privées, l’inclusion d’un modificateur d’accès, tel que le mot clé `private`, génère l’erreur de compilateur CS0106 : « Le modificateur « private » n’est pas valide pour cet élément ».</span><span class="sxs-lookup"><span data-stu-id="fa24b-128">Because all local functions are private, including an access modifier, such as the `private` keyword, generates compiler error CS0106, "The modifier 'private' is not valid for this item."</span></span>
 
- <span data-ttu-id="fa24b-129">Le mot clé [static](../../language-reference/keywords/static.md).</span><span class="sxs-lookup"><span data-stu-id="fa24b-129">The [static](../../language-reference/keywords/static.md) keyword.</span></span> <span data-ttu-id="fa24b-130">L’inclusion du mot clé `static` génère l’erreur de compilateur CS0106 : « Le modificateur « static » n’est pas valide pour cet élément ».</span><span class="sxs-lookup"><span data-stu-id="fa24b-130">Including the `static` keyword generates compiler error CS0106, "The modifier 'static' is not valid for this item."</span></span>

<span data-ttu-id="fa24b-131">Par ailleurs, les attributs ne peuvent pas être appliqués à la fonction locale ou à ses paramètres et paramètres de type.</span><span class="sxs-lookup"><span data-stu-id="fa24b-131">In addition, attributes can't be applied to the local function or to its parameters and type parameters.</span></span> 
 
<span data-ttu-id="fa24b-132">L’exemple suivant définit une fonction locale nommée `AppendPathSeparator` qui est privée pour une méthode nommée `GetText` :</span><span class="sxs-lookup"><span data-stu-id="fa24b-132">The following example defines a local function named `AppendPathSeparator` that is private to a method named `GetText`:</span></span>
   
<span data-ttu-id="fa24b-133">[!code-cs[LocalFunctionExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions1.cs)]</span><span class="sxs-lookup"><span data-stu-id="fa24b-133">[!code-cs[LocalFunctionExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions1.cs)]</span></span>  
   
## <a name="local-functions-and-exceptions"></a><span data-ttu-id="fa24b-134">Fonctions locales et exceptions</span><span class="sxs-lookup"><span data-stu-id="fa24b-134">Local functions and exceptions</span></span>

<span data-ttu-id="fa24b-135">L’une des caractéristiques intéressantes des fonctions locales est qu’elles permettent l’affichage immédiat des exceptions.</span><span class="sxs-lookup"><span data-stu-id="fa24b-135">One of the useful features of local functions is that they can allow exceptions to surface immediately.</span></span> <span data-ttu-id="fa24b-136">Pour les itérateurs de méthode, les exceptions apparaissent uniquement au moment où la séquence retournée est énumérée, et non à la récupération de l’itérateur.</span><span class="sxs-lookup"><span data-stu-id="fa24b-136">For method iterators, exceptions are surfaced only when the returned sequence is enumerated, and not when the iterator is retrieved.</span></span> <span data-ttu-id="fa24b-137">Pour les méthodes async, les exceptions levées dans une méthode async sont observées quand la tâche retournée est attendue.</span><span class="sxs-lookup"><span data-stu-id="fa24b-137">For async methods, any exceptions thrown in an async method are observed when the returned task is awaited.</span></span> 

<span data-ttu-id="fa24b-138">L’exemple suivant définit une méthode `OddSequence` qui énumère les nombres impairs dans une plage spécifiée.</span><span class="sxs-lookup"><span data-stu-id="fa24b-138">The following example defines an `OddSequence` method that enumerates odd numbers between a specified range.</span></span> <span data-ttu-id="fa24b-139">Sachant qu’elle passe à la méthode d’énumérateur `OddSequence` un nombre supérieur à 100, la méthode lève une exception <xref:System.ArgumentOutOfRangeException>.</span><span class="sxs-lookup"><span data-stu-id="fa24b-139">Because it passes a number greater than 100 to the `OddSequence` enumerator method, the method throws an <xref:System.ArgumentOutOfRangeException>.</span></span> <span data-ttu-id="fa24b-140">Comme le montre la sortie de l’exemple, l’exception apparaît uniquement au moment d’itérer les nombres, et non à la récupération de l’énumérateur.</span><span class="sxs-lookup"><span data-stu-id="fa24b-140">As the output from the example shows, the exception surfaces only when you iterate the numbers, and not when you retrieve the enumerator.</span></span>

<span data-ttu-id="fa24b-141">[!code-cs[LocalFunctionIterator1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator1.cs)]</span><span class="sxs-lookup"><span data-stu-id="fa24b-141">[!code-cs[LocalFunctionIterator1](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator1.cs)]</span></span> 

<span data-ttu-id="fa24b-142">Au lieu de cela, vous pouvez lever une exception au moment d’effectuer la validation et avant la récupération de l’itérateur en retournant l’itérateur à partir d’une fonction locale, comme dans l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="fa24b-142">Instead, you can throw an exception when performing validation and before retrieving the iterator by returning the iterator from a local function, as the following example shows.</span></span>

<span data-ttu-id="fa24b-143">[!code-cs[LocalFunctionIterator2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator2.cs)]</span><span class="sxs-lookup"><span data-stu-id="fa24b-143">[!code-cs[LocalFunctionIterator2](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-iterator2.cs)]</span></span>

<span data-ttu-id="fa24b-144">Les fonctions locales peuvent être utilisées de manière similaire pour gérer les exceptions en dehors de l’opération asynchrone.</span><span class="sxs-lookup"><span data-stu-id="fa24b-144">Local functions can be used in a similar way to handle exceptions outside of the asynchronous operation.</span></span> <span data-ttu-id="fa24b-145">D’ordinaire, les exceptions levées dans la méthode async nécessitent que vous examiniez les exceptions internes d’un <xref:System.AggregateException>.</span><span class="sxs-lookup"><span data-stu-id="fa24b-145">Ordinarily, exceptions thrown in async method require that you examine the inner exceptions of an <xref:System.AggregateException>.</span></span> <span data-ttu-id="fa24b-146">Les fonctions locales permettent à votre code d’échouer rapidement et à votre exception d’être à la fois levée et observée de manière synchrone.</span><span class="sxs-lookup"><span data-stu-id="fa24b-146">Local functions allow your code to fail fast and allow your exception to be both thrown and observed synchronously.</span></span>

<span data-ttu-id="fa24b-147">L’exemple suivant utilise une méthode asynchrone nommée `GetMultipleAsync` visant à marquer une pause pendant un nombre défini de secondes et retourner une valeur qui est un multiple aléatoire de ce nombre de secondes.</span><span class="sxs-lookup"><span data-stu-id="fa24b-147">The following example uses an asynchronous method named `GetMultipleAsync` to pause for a specified number of seconds and return a value that is a random multiple of that number of seconds.</span></span> <span data-ttu-id="fa24b-148">Le délai maximal est de 5 secondes ; une exception <xref:System.ArgumentOutOfRangeException> est obtenue si la valeur est supérieure à 5.</span><span class="sxs-lookup"><span data-stu-id="fa24b-148">The maximum delay is 5 seconds; an <xref:System.ArgumentOutOfRangeException> results if the value is greater than 5.</span></span> <span data-ttu-id="fa24b-149">Comme le montre l’exemple suivant, l’exception qui est levée quand une valeur de 6 est passée à la méthode `GetMultipleAsync` est encapsulée dans une exception <xref:System.AggregateException> après que la méthode `GetMultipleAsync` a démarré son exécution.</span><span class="sxs-lookup"><span data-stu-id="fa24b-149">As the following example shows, the exception that is thrown when a value of 6 is passed to the `GetMultipleAsync` method is wrapped in an <xref:System.AggregateException> after the `GetMultipleAsync` method begins execution.</span></span>

<span data-ttu-id="fa24b-150">[!code-cs[LocalFunctionAsync\`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async1.cs)]</span><span class="sxs-lookup"><span data-stu-id="fa24b-150">[!code-cs[LocalFunctionAsync\`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async1.cs)]</span></span> 

<span data-ttu-id="fa24b-151">Comme nous l’avons fait avec l’itérateur de méthode, nous pouvons refactoriser le code de cet exemple pour assurer la validation avant l’appel de la méthode asynchrone.</span><span class="sxs-lookup"><span data-stu-id="fa24b-151">As we did with the method iterator, we can refactor the code from this example to perform the validation before calling the asynchronous method.</span></span> <span data-ttu-id="fa24b-152">Comme le montre la sortie de l’exemple suivant, l’exception <xref:System.ArgumentOutOfRangeException> n’est pas encapsulée dans une exception <x:System.AggregateException>.</span><span class="sxs-lookup"><span data-stu-id="fa24b-152">As the output from the following example shows, the <xref:System.ArgumentOutOfRangeException> is not wrapped in a <x:System.AggregateException>.</span></span>

<span data-ttu-id="fa24b-153">[!code-cs[LocalFunctionAsync\`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async2.cs)]</span><span class="sxs-lookup"><span data-stu-id="fa24b-153">[!code-cs[LocalFunctionAsync\`](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/local-functions-async2.cs)]</span></span> 

## <a name="see-also"></a><span data-ttu-id="fa24b-154">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="fa24b-154">See also</span></span>
[<span data-ttu-id="fa24b-155">Méthodes</span><span class="sxs-lookup"><span data-stu-id="fa24b-155">Methods</span></span>](methods.md)
