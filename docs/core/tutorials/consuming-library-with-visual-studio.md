---
title: "Utilisation d’une bibliothèque de classes avec .NET Core dans Visual Studio 2017"
description: "Découvrez comment appeler les membres dans une bibliothèque de classes avec Visual Studio 2017."
author: BillWagner
ms.author: wiwagn
ms.date: 08/07/2017
ms.topic: article
ms.prod: .net-core
ms.translationtype: HT
ms.sourcegitcommit: 1b028e5880f9e57e87c16eabeb442e0a46a369da
ms.openlocfilehash: 38e6c7d8797285abc4eb2e87602cc0bbf46ba590
ms.contentlocale: fr-fr
ms.lasthandoff: 09/08/2017

---

# <a name="consuming-a-class-library-with-net-core-in-visual-studio-2017"></a><span data-ttu-id="62a64-103">Utilisation d’une bibliothèque de classes avec .NET Core dans Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="62a64-103">Consuming a class library with .NET Core in Visual Studio 2017</span></span>

<span data-ttu-id="62a64-104">Une fois que vous avez créé une bibliothèque de classes en suivant les étapes de [Création d’une bibliothèque de classes C# avec .NET Core dans Visual Studio 2017](./library-with-visual-studio.md) ou [Création d’une bibliothèque de classes Visual Basic avec .NET Core dans Visual Studio 2017](vb-library-with-visual-studio.md), que vous l’avez testée en suivant les instructions dans [Test d’une bibliothèque de classes avec .NET Core dans Visual Studio 2017](testing-library-with-visual-studio.md) et que vous avez créé une version Release de la bibliothèque, l’étape suivante consiste à la rendre accessible aux appelants.</span><span class="sxs-lookup"><span data-stu-id="62a64-104">Once you've created a class library by following the steps in [Building a C# class library with .NET Core in Visual Studio 2017](./library-with-visual-studio.md) or [Building a Visual Basic class library with .NET Core in Visual Studio 2017](vb-library-with-visual-studio.md), tested it in [Testing a class library with .NET Core in Visual Studio 2017](testing-library-with-visual-studio.md), and built a Release version of the library, the next step is to make it available to callers.</span></span> <span data-ttu-id="62a64-105">Pour cela, deux solutions s'offrent à vous :</span><span class="sxs-lookup"><span data-stu-id="62a64-105">You can do this in two ways:</span></span>

* <span data-ttu-id="62a64-106">Si la bibliothèque doit être utilisée par une seule solution (par exemple s’il s’agit d’un composant dans une seule application de grande taille), vous pouvez l’inclure en tant que projet dans votre solution.</span><span class="sxs-lookup"><span data-stu-id="62a64-106">If the library will be used by a single solution (for example, if it's a component in a single large application), you can include it as a project in your solution.</span></span>

* <span data-ttu-id="62a64-107">Si la bibliothèque est généralement accessible, vous pouvez la distribuer comme package NuGet.</span><span class="sxs-lookup"><span data-stu-id="62a64-107">If the library will be generally accessible, you can distribute it as a NuGet package.</span></span>

## <a name="including-a-library-as-a-project-in-a-solution"></a><span data-ttu-id="62a64-108">Inclusion d’une bibliothèque en tant que projet dans une solution</span><span class="sxs-lookup"><span data-stu-id="62a64-108">Including a library as a project in a solution</span></span>

<span data-ttu-id="62a64-109">Tout comme vous avez inclus des tests unitaires dans la même solution que votre bibliothèque de classes, vous pouvez inclure votre application dans le cadre de cette solution.</span><span class="sxs-lookup"><span data-stu-id="62a64-109">Just as you included unit tests in the same solution as your class library, you can include your application as part of that solution.</span></span> <span data-ttu-id="62a64-110">Par exemple, vous pouvez utiliser votre bibliothèque de classes dans une application console qui invite l’utilisateur à entrer une chaîne et indique si son premier caractère est une majuscule :</span><span class="sxs-lookup"><span data-stu-id="62a64-110">For example, you can use your class library in a console application that prompts the user to enter a string and reports whether its first character is uppercase:</span></span>

# <a name="ctabcsharp"></a>[<span data-ttu-id="62a64-111">C#</span><span class="sxs-lookup"><span data-stu-id="62a64-111">C#</span></span>](#tab/csharp)
1. <span data-ttu-id="62a64-112">Ouvrez la `ClassLibraryProjects` solution que vous avez créée dans la rubrique [Création d’une bibliothèque de classes C# avec .NET Core dans Visual Studio 2017](./library-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="62a64-112">Open the `ClassLibraryProjects` solution you created in the [Building a C# Class Library with .NET Core in Visual Studio 2017](./library-with-visual-studio.md) topic.</span></span> <span data-ttu-id="62a64-113">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur la solution **ClassLibraryProjects** et, dans le menu contextuel, sélectionnez **Ajouter** > **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="62a64-113">In **Solution Explorer**, right-click the **ClassLibraryProjects** solution and select **Add** > **New Project** from the context menu.</span></span>

1. <span data-ttu-id="62a64-114">Dans la boîte de dialogue **Ajouter un nouveau projet**, développez le nœud **Visual C#** et sélectionnez le nœud **.NET Core**, puis choisissez le modèle de projet **Application console (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="62a64-114">In the **Add New Project** dialog, expand the **Visual C#** node and select the **.NET Core** node followed by the **Console App (.NET Core)** project template.</span></span> <span data-ttu-id="62a64-115">Dans la zone de texte **Nom**, tapez « ShowCase », puis sélectionnez le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="62a64-115">In the **Name** text box, type "ShowCase", and select the **OK** button.</span></span>

   ![Boîte de dialogue Ajouter un nouveau projet](./media/consuming-library-with-visual-studio/addnewproject.png)

1. <span data-ttu-id="62a64-117">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet **ShowCase**, puis sélectionnez **Définir comme projet de démarrage** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="62a64-117">In **Solution Explorer**, right-click the **ShowCase** project and select **Set as StartUp Project** in the context menu.</span></span> 

   ![Menu contextuel de ShowCase](./media/consuming-library-with-visual-studio/setstartupproject.png)

1. <span data-ttu-id="62a64-119">Initialement, votre projet n’a pas accès à votre bibliothèque de classes.</span><span class="sxs-lookup"><span data-stu-id="62a64-119">Initially, your project doesn't have access to your class library.</span></span> <span data-ttu-id="62a64-120">Pour lui permettre d’appeler des méthodes dans votre bibliothèque de classes, vous créez une référence à la bibliothèque de classes.</span><span class="sxs-lookup"><span data-stu-id="62a64-120">To allow it to call methods in your class library, you create a reference to the class library.</span></span> <span data-ttu-id="62a64-121">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nœud **Dépendances** du projet `ShowCase` et sélectionnez **Ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="62a64-121">In **Solution Explorer**, right-click the `ShowCase` project's **Dependencies** node and select **Add Reference**.</span></span>

   ![Menu contextuel Dépendances de ShowCase](./media/consuming-library-with-visual-studio/addreference.png)

1. <span data-ttu-id="62a64-123">Dans la boîte de dialogue **Gestionnaire de références**, sélectionnez **StringLibrary**, votre projet de bibliothèque de classe, puis sélectionnez le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="62a64-123">In the **Reference Manager** dialog, select **StringLibrary**, your class library project, and select the **OK** button.</span></span>

   ![Gestionnaire de références](./media/consuming-library-with-visual-studio/referencemanager.png)

1. <span data-ttu-id="62a64-125">Dans la fenêtre de code pour le fichier *Program.cs*, remplacez tout le code par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="62a64-125">In the code window for the *Program.cs* file, replace all of the code with the following code:</span></span>

   <span data-ttu-id="62a64-126">[!CODE-csharp[UsingClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/showcase.cs)]</span><span class="sxs-lookup"><span data-stu-id="62a64-126">[!CODE-csharp[UsingClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/showcase.cs)]</span></span>

   <span data-ttu-id="62a64-127">Le code utilise la propriété [Console.WindowHeight](xref:System.Console.WindowHeight) pour déterminer le nombre de lignes de la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="62a64-127">The code uses the [Console.WindowHeight](xref:System.Console.WindowHeight) property to determine the number of rows in the console window.</span></span> <span data-ttu-id="62a64-128">Quand la propriété [Console.CursorTop](xref:System.Console.CursorTop) est supérieure ou égale au nombre total de lignes dans la fenêtre de console, le code efface la fenêtre de console et affiche un message à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="62a64-128">Whenever the [Console.CursorTop](xref:System.Console.CursorTop) property is greater than or equal to the number of rows in the console window, the code clears the console window and displays a message to the user.</span></span>

   <span data-ttu-id="62a64-129">Le programme invite l’utilisateur à entrer une chaîne.</span><span class="sxs-lookup"><span data-stu-id="62a64-129">The program prompts the user to enter a string.</span></span> <span data-ttu-id="62a64-130">Il indique si la chaîne commence par une majuscule.</span><span class="sxs-lookup"><span data-stu-id="62a64-130">It indicates whether the string starts with an uppercase character.</span></span> <span data-ttu-id="62a64-131">Si l’utilisateur appuie sur la touche Entrée sans entrer une chaîne, l’application se termine et la fenêtre de console se ferme.</span><span class="sxs-lookup"><span data-stu-id="62a64-131">If the user presses the Enter key without entering a string, the application terminates, and the console window closes.</span></span>

1. <span data-ttu-id="62a64-132">Si nécessaire, changez la barre d’outils pour compiler la version **Debug** du projet `ShowCase`.</span><span class="sxs-lookup"><span data-stu-id="62a64-132">If necessary, change the toolbar to compile the **Debug** release of the `ShowCase` project.</span></span> <span data-ttu-id="62a64-133">Compilez et exécutez le programme en sélectionnant la flèche verte sur le bouton **ShowCase**.</span><span class="sxs-lookup"><span data-stu-id="62a64-133">Compile and run the program by selecting the green arrow on the **ShowCase** button.</span></span>

   ![Image](./media/consuming-library-with-visual-studio/toolbar.png)
# <a name="visual-basictabvisual-basic"></a>[<span data-ttu-id="62a64-135">Visual Basic</span><span class="sxs-lookup"><span data-stu-id="62a64-135">Visual Basic</span></span>](#tab/visual-basic)
1. <span data-ttu-id="62a64-136">Ouvrez la solution `ClassLibraryProjects` que vous avez créée dans la rubrique [Création d’une bibliothèque de classes avec Visual Basic et .NET Core dans Visual Studio 2017](vb-library-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="62a64-136">Open the `ClassLibraryProjects` solution you created in the [Building a class Library with Visual Basic and .NET Core in Visual Studio 2017](vb-library-with-visual-studio.md) topic.</span></span> <span data-ttu-id="62a64-137">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur la solution **ClassLibraryProjects** et, dans le menu contextuel, sélectionnez **Ajouter** > **Nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="62a64-137">In **Solution Explorer**, right-click the **ClassLibraryProjects** solution and select **Add** > **New Project** from the context menu.</span></span>

1. <span data-ttu-id="62a64-138">Dans la boîte de dialogue **Ajouter un nouveau projet**, développez le nœud **Visual Basic** et sélectionnez le nœud **.NET Core**, puis choisissez le modèle de projet **Application console (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="62a64-138">In the **Add New Project** dialog, expand the **Visual Basic** node and select the **.NET Core** node followed by the **Console App (.NET Core)** project template.</span></span> <span data-ttu-id="62a64-139">Dans la zone de texte **Nom**, tapez « ShowCase », puis sélectionnez le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="62a64-139">In the **Name** text box, type "ShowCase", and select the **OK** button.</span></span>

   ![Boîte de dialogue Ajouter un nouveau projet](./media/consuming-library-with-visual-studio/vb-addnewproject.png)

1. <span data-ttu-id="62a64-141">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le projet **ShowCase**, puis sélectionnez **Définir comme projet de démarrage** dans le menu contextuel.</span><span class="sxs-lookup"><span data-stu-id="62a64-141">In **Solution Explorer**, right-click the **ShowCase** project and select **Set as StartUp Project** in the context menu.</span></span> 

   ![Menu contextuel de ShowCase](./media/consuming-library-with-visual-studio/setstartupproject.png)

1. <span data-ttu-id="62a64-143">Initialement, votre projet n’a pas accès à votre bibliothèque de classes.</span><span class="sxs-lookup"><span data-stu-id="62a64-143">Initially, your project doesn't have access to your class library.</span></span> <span data-ttu-id="62a64-144">Pour lui permettre d’appeler des méthodes dans votre bibliothèque de classes, vous créez une référence à la bibliothèque de classes.</span><span class="sxs-lookup"><span data-stu-id="62a64-144">To allow it to call methods in your class library, you create a reference to the class library.</span></span> <span data-ttu-id="62a64-145">Dans l’**Explorateur de solutions**, cliquez avec le bouton droit sur le nœud **Dépendances** du projet `ShowCase` et sélectionnez **Ajouter une référence**.</span><span class="sxs-lookup"><span data-stu-id="62a64-145">In **Solution Explorer**, right-click the `ShowCase` project's **Dependencies** node and select **Add Reference**.</span></span>

   ![Menu contextuel Dépendances de ShowCase](./media/consuming-library-with-visual-studio/addreference.png)

1. <span data-ttu-id="62a64-147">Dans la boîte de dialogue **Gestionnaire de références**, sélectionnez **StringLibrary**, votre projet de bibliothèque de classe, puis sélectionnez le bouton **OK**.</span><span class="sxs-lookup"><span data-stu-id="62a64-147">In the **Reference Manager** dialog, select **StringLibrary**, your class library project, and select the **OK** button.</span></span>

   ![Gestionnaire de références](./media/consuming-library-with-visual-studio/referencemanager.png)

1. <span data-ttu-id="62a64-149">Dans la fenêtre de code pour le fichier *Program.vb*, remplacez tout le code par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="62a64-149">In the code window for the *Program.vb* file, replace all of the code with the following code:</span></span>

    <span data-ttu-id="62a64-150">[!CODE-vb[UsingClassLib#1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/showcase.vb)]</span><span class="sxs-lookup"><span data-stu-id="62a64-150">[!CODE-vb[UsingClassLib#1](../../../samples/snippets/core/tutorials/vb-library-with-visual-studio/showcase.vb)]</span></span>

   <span data-ttu-id="62a64-151">Le code utilise la propriété [Console.WindowHeight](xref:System.Console.WindowHeight) pour déterminer le nombre de lignes de la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="62a64-151">The code uses the [Console.WindowHeight](xref:System.Console.WindowHeight) property to determine the number of rows in the console window.</span></span> <span data-ttu-id="62a64-152">Quand la propriété [Console.CursorTop](xref:System.Console.CursorTop) est supérieure ou égale au nombre total de lignes dans la fenêtre de console, le code efface la fenêtre de console et affiche un message à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="62a64-152">Whenever the [Console.CursorTop](xref:System.Console.CursorTop) property is greater than or equal to the number of rows in the console window, the code clears the console window and displays a message to the user.</span></span>

   <span data-ttu-id="62a64-153">Le programme invite l’utilisateur à entrer une chaîne.</span><span class="sxs-lookup"><span data-stu-id="62a64-153">The program prompts the user to enter a string.</span></span> <span data-ttu-id="62a64-154">Il indique si la chaîne commence par une majuscule.</span><span class="sxs-lookup"><span data-stu-id="62a64-154">It indicates whether the string starts with an uppercase character.</span></span> <span data-ttu-id="62a64-155">Si l’utilisateur appuie sur la touche Entrée sans entrer une chaîne, l’application se termine et la fenêtre de console se ferme.</span><span class="sxs-lookup"><span data-stu-id="62a64-155">If the user presses the Enter key without entering a string, the application terminates, and the console window closes.</span></span>

1. <span data-ttu-id="62a64-156">Si nécessaire, changez la barre d’outils pour compiler la version **Debug** du projet `ShowCase`.</span><span class="sxs-lookup"><span data-stu-id="62a64-156">If necessary, change the toolbar to compile the **Debug** release of the `ShowCase` project.</span></span> <span data-ttu-id="62a64-157">Compilez et exécutez le programme en sélectionnant la flèche verte sur le bouton **ShowCase**.</span><span class="sxs-lookup"><span data-stu-id="62a64-157">Compile and run the program by selecting the green arrow on the **ShowCase** button.</span></span>

   ![Image](./media/consuming-library-with-visual-studio/toolbar.png)
---

<span data-ttu-id="62a64-159">Vous pouvez déboguer et publier l’application qui utilise cette bibliothèque en suivant les étapes de [Débogage de votre application Hello World avec Visual Studio 2017](debugging-with-visual-studio.md) et de [Publication de votre application Hello World avec Visual Studio 2017](publishing-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="62a64-159">You can debug and publish the application that uses this library by following the steps in [Debugging your Hello World application with Visual Studio 2017](debugging-with-visual-studio.md) and [Publishing your Hello World Application with Visual Studio 2017](publishing-with-visual-studio.md).</span></span>

## <a name="distributing-the-library-in-a-nuget-package"></a><span data-ttu-id="62a64-160">Distribution de la bibliothèque dans un package NuGet</span><span class="sxs-lookup"><span data-stu-id="62a64-160">Distributing the library in a NuGet package</span></span>

<span data-ttu-id="62a64-161">Vous pouvez rendre votre bibliothèque de classes disponible à grande échelle en la publiant sous forme de package NuGet.</span><span class="sxs-lookup"><span data-stu-id="62a64-161">You can make your class library widely available by publishing it as a NuGet package.</span></span> <span data-ttu-id="62a64-162">Visual Studio ne prend pas en charge la création des packages NuGet.</span><span class="sxs-lookup"><span data-stu-id="62a64-162">Visual Studio does not support the creation of NuGet packages.</span></span> <span data-ttu-id="62a64-163">Pour en créer un, vous utilisez l’[`dotnet`utilitaire de ligne de commande](../../core/tools/dotnet.md) :</span><span class="sxs-lookup"><span data-stu-id="62a64-163">To create one, you use the [`dotnet` command line utility](../../core/tools/dotnet.md):</span></span>

1. <span data-ttu-id="62a64-164">Ouvrez une fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="62a64-164">Open a console window.</span></span> <span data-ttu-id="62a64-165">Par exemple, dans la zone de texte **Posez-moi une question** dans la barre des tâches Windows, entrez `Command Prompt` (ou `cmd` en abrégé) et ouvrez une fenêtre de console en sélectionnant l’application de poste de travail **Invite de commandes** ou en appuyant sur Entrée si elle est sélectionnée dans les résultats de la recherche.</span><span class="sxs-lookup"><span data-stu-id="62a64-165">For example in the **Ask me anything** text box in the Windows taskbar, enter `Command Prompt` (or `cmd` for short), and open a console window by either selecting the **Command Prompt** desktop app or pressing Enter if it's selected in the search results.</span></span>

1. <span data-ttu-id="62a64-166">Accédez au répertoire de votre projet de bibliothèque.</span><span class="sxs-lookup"><span data-stu-id="62a64-166">Navigate to your library's project directory.</span></span> <span data-ttu-id="62a64-167">Sauf si vous avez reconfiguré l’emplacement habituel du fichier, il se trouve dans le répertoire *Documents\Visual Studio 2017\Projects\ClassLibraryProjects\StringLibrary*.</span><span class="sxs-lookup"><span data-stu-id="62a64-167">Unless you've reconfigured the typical file location, it's in the *Documents\Visual Studio 2017\Projects\ClassLibraryProjects\StringLibrary* directory.</span></span> <span data-ttu-id="62a64-168">Le répertoire contient votre code source et un fichier projet, *StringLibrary.csproj*.</span><span class="sxs-lookup"><span data-stu-id="62a64-168">The directory contains your source code and a project file, *StringLibrary.csproj*.</span></span>

1. <span data-ttu-id="62a64-169">Émettez la commande `dotnet pack --no-build`.</span><span class="sxs-lookup"><span data-stu-id="62a64-169">Issue the command `dotnet pack --no-build`.</span></span> <span data-ttu-id="62a64-170">L’utilitaire `dotnet` génère un package avec une extension *.nupkg*.</span><span class="sxs-lookup"><span data-stu-id="62a64-170">The `dotnet` utility generates a package with a *.nupkg* extension.</span></span>

   > [!TIP]
   > <span data-ttu-id="62a64-171">Si le répertoire contenant *dotnet.exe* ne se trouve pas dans votre chemin, vous pouvez trouver son emplacement en entrant `where dotnet.exe` dans la fenêtre de console.</span><span class="sxs-lookup"><span data-stu-id="62a64-171">If the directory that contains *dotnet.exe* is not in your PATH, you can find its location by entering `where dotnet.exe` in the console window.</span></span>

<span data-ttu-id="62a64-172">Pour plus d’informations sur la création de packages NuGet, consultez [Création d’un Package NuGet avec les outils multiplateformes](../../core/deploying/creating-nuget-packages.md).</span><span class="sxs-lookup"><span data-stu-id="62a64-172">For more information on creating NuGet packages, see [How to Create a NuGet Package with Cross Platform Tools](../../core/deploying/creating-nuget-packages.md).</span></span>
