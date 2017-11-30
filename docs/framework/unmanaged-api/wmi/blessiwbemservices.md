---
title: "BlessIWbemServices (fonction) (référence des API non managées)"
description: "La fonction BlessIWbemServices indique si les informations d’identification utilisateur autorisent l’accès à une classe IWbemServices."
ms.date: 11/06/2017
ms.prod: .net-framework
ms.technology: dotnet-clr
ms.topic: reference
api_name: BlessIWbemServices
api_location: WMINet_Utils.dll
api_type: DLLExport
f1_keywords: BlessIWbemServices
helpviewer_keywords: BlessIWbemServices function [.NET WMI and performance counters]
topic_type: Reference
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 67431d4272ac1da4d400a5552c61cf464680b502
ms.sourcegitcommit: a53799f81351ad9afb3007cd68846ce6aeeb10cb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/15/2017
---
# <a name="blessiwbemservices-function"></a><span data-ttu-id="13a5b-103">BlessIWbemServices (fonction)</span><span class="sxs-lookup"><span data-stu-id="13a5b-103">BlessIWbemServices function</span></span>
<span data-ttu-id="13a5b-104">Indique si les informations d’identification autorisent l’accès spécifié [IWbemServices](https://msdn.microsoft.com/library/aa392093(v=vs.85).aspx) classe.</span><span class="sxs-lookup"><span data-stu-id="13a5b-104">Indicates whether the user credentials permit access to the specified [IWbemServices](https://msdn.microsoft.com/library/aa392093(v=vs.85).aspx) class.</span></span>   
  
[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]
  
## <a name="syntax"></a><span data-ttu-id="13a5b-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="13a5b-105">Syntax</span></span>  
  
```  
HRESULT BlessIWbemServices (
   [in] IWbemServices* pIWbemServices,
   [in] BSTR strUser, 
   [in] BSTR strPassword, 
   [in] BSTR strAuthority, 
   [in] DWORD impLevel, 
   [in] DWORD authnLevel
);
```  

## <a name="parameters"></a><span data-ttu-id="13a5b-106">Paramètres</span><span class="sxs-lookup"><span data-stu-id="13a5b-106">Parameters</span></span>

`pIWbemServices`  
<span data-ttu-id="13a5b-107">[in] Un pointeur vers le [IWbemServices](https://msdn.microsoft.com/library/aa392093(v=vs.85).aspx) objet pour lequel les autorisations sont requises.</span><span class="sxs-lookup"><span data-stu-id="13a5b-107">[in] A pointer to the [IWbemServices](https://msdn.microsoft.com/library/aa392093(v=vs.85).aspx) object for which permissions are required.</span></span>

`strUser`  
<span data-ttu-id="13a5b-108">[in] Le nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="13a5b-108">[in] The user name.</span></span>

`strPassword`  
<span data-ttu-id="13a5b-109">[in] Le mot de passe associé `strUser`.</span><span class="sxs-lookup"><span data-stu-id="13a5b-109">[in] The password associated with `strUser`.</span></span>

<span data-ttu-id="13a5b-110">`strAuthority`[in] Le nom de domaine de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="13a5b-110">`strAuthority` [in] The domain name of the user.</span></span> <span data-ttu-id="13a5b-111">Consultez le [ConnectServerWmi](connectserverwmi.md) (fonction) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="13a5b-111">See the [ConnectServerWmi](connectserverwmi.md) function for more information.</span></span>

<span data-ttu-id="13a5b-112">`impLevel`[in] Le niveau d’emprunt d’identité.</span><span class="sxs-lookup"><span data-stu-id="13a5b-112">`impLevel` [in] The impersonation level.</span></span>

<span data-ttu-id="13a5b-113">`authnLevel`[in] Le niveau d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="13a5b-113">`authnLevel` [in] The authorization level.</span></span>

## <a name="return-value"></a><span data-ttu-id="13a5b-114">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="13a5b-114">Return value</span></span>

<span data-ttu-id="13a5b-115">Les valeurs suivantes est retournées par cette fonction sont définies dans le *WinError.h* fichier d’en-tête, ou vous pouvez les définir en tant que constantes dans votre code :</span><span class="sxs-lookup"><span data-stu-id="13a5b-115">The following values returned by this function are defined in the *WinError.h* header file, or you can define them as constants in your code:</span></span>

|<span data-ttu-id="13a5b-116">Constante</span><span class="sxs-lookup"><span data-stu-id="13a5b-116">Constant</span></span>  |<span data-ttu-id="13a5b-117">Valeur</span><span class="sxs-lookup"><span data-stu-id="13a5b-117">Value</span></span>  |<span data-ttu-id="13a5b-118">Description</span><span class="sxs-lookup"><span data-stu-id="13a5b-118">Description</span></span>  |
|---------|---------|---------|
| `E_INVALIDARG` | <span data-ttu-id="13a5b-119">0 x 80070057</span><span class="sxs-lookup"><span data-stu-id="13a5b-119">0x80070057</span></span> | <span data-ttu-id="13a5b-120">Un ou plusieurs arguments ne sont pas valide.</span><span class="sxs-lookup"><span data-stu-id="13a5b-120">One or more arguments are invalid.</span></span> |
| `E_POINTER` | <span data-ttu-id="13a5b-121">0 x 80004003</span><span class="sxs-lookup"><span data-stu-id="13a5b-121">0x80004003</span></span> | <span data-ttu-id="13a5b-122">`pIWbemServices` a la valeur `null`.</span><span class="sxs-lookup"><span data-stu-id="13a5b-122">`pIWbemServices` is `null`.</span></span> | 
| `E_FAIL` | <span data-ttu-id="13a5b-123">0x80000008</span><span class="sxs-lookup"><span data-stu-id="13a5b-123">0x80000008</span></span> | <span data-ttu-id="13a5b-124">Une erreur non spécifiée s’est produite.</span><span class="sxs-lookup"><span data-stu-id="13a5b-124">An unspecified error has occurred.</span></span> |
| `E_OUTOFMEMORY` | <span data-ttu-id="13a5b-125">0x80000002</span><span class="sxs-lookup"><span data-stu-id="13a5b-125">0x80000002</span></span> | <span data-ttu-id="13a5b-126">Mémoire disponible est insuffisante pour effectuer l’opération.</span><span class="sxs-lookup"><span data-stu-id="13a5b-126">Insufficient memory is available to perform the operation.</span></span> | 
| `S_OK` | <span data-ttu-id="13a5b-127">0</span><span class="sxs-lookup"><span data-stu-id="13a5b-127">0</span></span> | <span data-ttu-id="13a5b-128">L’appel de fonction a réussi.</span><span class="sxs-lookup"><span data-stu-id="13a5b-128">The function call was successful.</span></span> | 

## <a name="requirements"></a><span data-ttu-id="13a5b-129">Spécifications</span><span class="sxs-lookup"><span data-stu-id="13a5b-129">Requirements</span></span>  
 <span data-ttu-id="13a5b-130">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="13a5b-130">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="13a5b-131">**En-tête :** WMINet_Utils.idl</span><span class="sxs-lookup"><span data-stu-id="13a5b-131">**Header:** WMINet_Utils.idl</span></span>  
  
 <span data-ttu-id="13a5b-132">**Versions du .NET framework :**[!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span><span class="sxs-lookup"><span data-stu-id="13a5b-132">**.NET Framework Versions:** [!INCLUDE[net_current_v472plus](../../../../includes/net-current-v472plus.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="13a5b-133">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="13a5b-133">See also</span></span>  
[<span data-ttu-id="13a5b-134">WMI et les compteurs de Performance (référence des API non managées)</span><span class="sxs-lookup"><span data-stu-id="13a5b-134">WMI and Performance Counters (Unmanaged API Reference)</span></span>](index.md)