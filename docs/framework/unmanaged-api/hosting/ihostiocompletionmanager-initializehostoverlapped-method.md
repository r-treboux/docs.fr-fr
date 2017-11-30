---
title: "IHostIoCompletionManager::InitializeHostOverlapped, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IHostIoCompletionManager.InitializeHostOverlapped
api_location: mscoree.dll
api_type: COM
f1_keywords: IHostIoCompletionManager::InitializeHostOverlapped
helpviewer_keywords:
- IHostIoCompletionManager::InitializeHostOverlapped method [.NET Framework hosting]
- InitializeHostOverlapped method [.NET Framework hosting]
ms.assetid: c35199bf-bc47-4901-b467-4e8a37644bbb
topic_type: apiref
caps.latest.revision: "9"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 26e8f9d963e6924a8c6abd73c3e025543c7d5b83
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="ihostiocompletionmanagerinitializehostoverlapped-method"></a><span data-ttu-id="da240-102">IHostIoCompletionManager::InitializeHostOverlapped, méthode</span><span class="sxs-lookup"><span data-stu-id="da240-102">IHostIoCompletionManager::InitializeHostOverlapped Method</span></span>
<span data-ttu-id="da240-103">Fournit à l’hôte avec la possibilité d’initialiser toutes données personnalisées à ajouter à un Win32 `OVERLAPPED` structure utilisée pour les demandes d’e/s asynchrones.</span><span class="sxs-lookup"><span data-stu-id="da240-103">Provides the host with an opportunity to initialize any custom data to append to a Win32 `OVERLAPPED` structure that is used for asynchronous I/O requests.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="da240-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="da240-104">Syntax</span></span>  
  
```  
HRESULT InitializeHostOverlapped (  
    [in] void* pvOverlapped  
);  
```  
  
#### <a name="parameters"></a><span data-ttu-id="da240-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="da240-105">Parameters</span></span>  
 `pvOverlapped`  
 <span data-ttu-id="da240-106">[in] Un pointeur vers Win32 `OVERLAPPED` structure pour être inclus dans la demande d’e/s.</span><span class="sxs-lookup"><span data-stu-id="da240-106">[in] A pointer to the Win32 `OVERLAPPED` structure to be included with the I/O request.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="da240-107">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="da240-107">Return Value</span></span>  
  
|<span data-ttu-id="da240-108">HRESULT</span><span class="sxs-lookup"><span data-stu-id="da240-108">HRESULT</span></span>|<span data-ttu-id="da240-109">Description</span><span class="sxs-lookup"><span data-stu-id="da240-109">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="da240-110">S_OK</span><span class="sxs-lookup"><span data-stu-id="da240-110">S_OK</span></span>|<span data-ttu-id="da240-111">`InitializeHostOverlapped`retourné avec succès.</span><span class="sxs-lookup"><span data-stu-id="da240-111">`InitializeHostOverlapped` returned successfully.</span></span>|  
|<span data-ttu-id="da240-112">HOST_E_CLRNOTAVAILABLE</span><span class="sxs-lookup"><span data-stu-id="da240-112">HOST_E_CLRNOTAVAILABLE</span></span>|<span data-ttu-id="da240-113">Le common language runtime (CLR) n’a pas été chargé dans un processus ou le CLR est dans un état dans lequel il ne peut pas exécuter du code managé ou traiter l’appel avec succès.</span><span class="sxs-lookup"><span data-stu-id="da240-113">The common language runtime (CLR) has not been loaded into a process, or the CLR is in a state in which it cannot run managed code or process the call successfully.</span></span>|  
|<span data-ttu-id="da240-114">HOST_E_TIMEOUT</span><span class="sxs-lookup"><span data-stu-id="da240-114">HOST_E_TIMEOUT</span></span>|<span data-ttu-id="da240-115">L’appel a expiré.</span><span class="sxs-lookup"><span data-stu-id="da240-115">The call timed out.</span></span>|  
|<span data-ttu-id="da240-116">HOST_E_NOT_OWNER</span><span class="sxs-lookup"><span data-stu-id="da240-116">HOST_E_NOT_OWNER</span></span>|<span data-ttu-id="da240-117">L’appelant ne possède pas le verrou.</span><span class="sxs-lookup"><span data-stu-id="da240-117">The caller does not own the lock.</span></span>|  
|<span data-ttu-id="da240-118">HOST_E_ABANDONED</span><span class="sxs-lookup"><span data-stu-id="da240-118">HOST_E_ABANDONED</span></span>|<span data-ttu-id="da240-119">Un événement a été annulé alors qu’un thread bloqué ou une fibre l’attendait.</span><span class="sxs-lookup"><span data-stu-id="da240-119">An event was canceled while a blocked thread or fiber was waiting on it.</span></span>|  
|<span data-ttu-id="da240-120">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="da240-120">E_FAIL</span></span>|<span data-ttu-id="da240-121">Une défaillance grave et inconnue s’est produite.</span><span class="sxs-lookup"><span data-stu-id="da240-121">An unknown catastrophic failure occurred.</span></span> <span data-ttu-id="da240-122">Lorsqu’une méthode retourne E_FAIL, le CLR n’est plus utilisable dans le processus.</span><span class="sxs-lookup"><span data-stu-id="da240-122">When a method returns E_FAIL, the CLR is no longer usable within the process.</span></span> <span data-ttu-id="da240-123">Les appels suivants aux méthodes d’hébergement retournent HOST_E_CLRNOTAVAILABLE.</span><span class="sxs-lookup"><span data-stu-id="da240-123">Subsequent calls to hosting methods return HOST_E_CLRNOTAVAILABLE.</span></span>|  
|<span data-ttu-id="da240-124">E_OUTOFMEMORY</span><span class="sxs-lookup"><span data-stu-id="da240-124">E_OUTOFMEMORY</span></span>|<span data-ttu-id="da240-125">Mémoire était insuffisante pour allouer la ressource demandée.</span><span class="sxs-lookup"><span data-stu-id="da240-125">Not enough memory was available to allocate the requested resource.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="da240-126">Remarques</span><span class="sxs-lookup"><span data-stu-id="da240-126">Remarks</span></span>  
 <span data-ttu-id="da240-127">La plateforme Windows fonctions utilisent la `OVERLAPPED` structure pour stocker l’état pour les demandes d’e/s asynchrones.</span><span class="sxs-lookup"><span data-stu-id="da240-127">The Windows Platform functions use the `OVERLAPPED` structure to store state for asynchronous I/O requests.</span></span> <span data-ttu-id="da240-128">Le CLR appelle la `InitializeHostOverlapped` méthode pour permettre à l’hôte la possibilité d’ajouter des données personnalisées à un `OVERLAPPED` instance.</span><span class="sxs-lookup"><span data-stu-id="da240-128">The CLR calls the `InitializeHostOverlapped` method to give the host the opportunity to append custom data to an `OVERLAPPED` instance.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="da240-129">Pour parvenir au début de leur bloc de données personnalisées, les hôtes doivent définir le décalage à la taille de la `OVERLAPPED` structure (`sizeof(OVERLAPPED)`).</span><span class="sxs-lookup"><span data-stu-id="da240-129">To get to the beginning of their custom data block, hosts must set the offset to the size of the `OVERLAPPED` structure (`sizeof(OVERLAPPED)`).</span></span>  
  
 <span data-ttu-id="da240-130">Une valeur de retour E_OUTOFMEMORY indique que l’ordinateur hôte n’a pas pu initialiser ses données personnalisées.</span><span class="sxs-lookup"><span data-stu-id="da240-130">A return value of E_OUTOFMEMORY indicates that the host has failed to initialize its custom data.</span></span> <span data-ttu-id="da240-131">Dans ce cas, le CLR signale une erreur et fait échouer l’appel.</span><span class="sxs-lookup"><span data-stu-id="da240-131">In this case, the CLR reports an error and fails the call.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="da240-132">Spécifications</span><span class="sxs-lookup"><span data-stu-id="da240-132">Requirements</span></span>  
 <span data-ttu-id="da240-133">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="da240-133">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="da240-134">**En-tête :** MSCorEE.h</span><span class="sxs-lookup"><span data-stu-id="da240-134">**Header:** MSCorEE.h</span></span>  
  
 <span data-ttu-id="da240-135">**Bibliothèque :** inclus en tant que ressource dans MSCorEE.dll</span><span class="sxs-lookup"><span data-stu-id="da240-135">**Library:** Included as a resource in MSCorEE.dll</span></span>  
  
 <span data-ttu-id="da240-136">**Versions du .NET framework :**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="da240-136">**.NET Framework Versions:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="da240-137">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="da240-137">See Also</span></span>  
 [<span data-ttu-id="da240-138">ICLRIoCompletionManager (Interface)</span><span class="sxs-lookup"><span data-stu-id="da240-138">ICLRIoCompletionManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/iclriocompletionmanager-interface.md)  
 [<span data-ttu-id="da240-139">GetHostOverlappedSize (méthode)</span><span class="sxs-lookup"><span data-stu-id="da240-139">GetHostOverlappedSize Method</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-gethostoverlappedsize-method.md)  
 [<span data-ttu-id="da240-140">IHostIoCompletionManager (Interface)</span><span class="sxs-lookup"><span data-stu-id="da240-140">IHostIoCompletionManager Interface</span></span>](../../../../docs/framework/unmanaged-api/hosting/ihostiocompletionmanager-interface.md)