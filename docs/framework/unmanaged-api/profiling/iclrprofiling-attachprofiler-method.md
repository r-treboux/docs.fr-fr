---
title: "ICLRProfiling::AttachProfiler, méthode"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: IClrProfiling.AttachProfiler Method
api_location: Mscorwks.dll
api_type: COM
f1_keywords: IClrProfiling::AttachProfiler
helpviewer_keywords:
- AttachProfiler method [.NET Framework profiling]
- IClrProfiling::AttachProfiler method [.NET Framework profiling]
ms.assetid: 535a6839-c443-405b-a6f4-e2af90725d5b
topic_type: apiref
caps.latest.revision: "15"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 1a0f1e41f7d59074f997a5812da61fdbcd692770
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/21/2017
---
# <a name="iclrprofilingattachprofiler-method"></a><span data-ttu-id="7b648-102">ICLRProfiling::AttachProfiler, méthode</span><span class="sxs-lookup"><span data-stu-id="7b648-102">ICLRProfiling::AttachProfiler Method</span></span>
<span data-ttu-id="7b648-103">Attache le profileur spécifié au processus spécifié.</span><span class="sxs-lookup"><span data-stu-id="7b648-103">Attaches the specified profiler to the specified process.</span></span>  
  
## <a name="syntax"></a><span data-ttu-id="7b648-104">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="7b648-104">Syntax</span></span>  
  
```  
HRESULT AttachProfiler(  
  [in] DWORD dwProfileeProcessID,  
  [in] DWORD dwMillisecondsMax,                     // optional  
  [in] const CLSID * pClsidProfiler,  
  [in] LPCWSTR wszProfilerPath,                     // optional  
  [in] size_is(cbClientData)] void * pvClientData,  // optional  
  [in] UINT cbClientData);                          // optional  
```  
  
#### <a name="parameters"></a><span data-ttu-id="7b648-105">Paramètres</span><span class="sxs-lookup"><span data-stu-id="7b648-105">Parameters</span></span>  
 `dwProfileeProcessID`  
 <span data-ttu-id="7b648-106">[in] ID du processus auquel le profileur doit être attaché.</span><span class="sxs-lookup"><span data-stu-id="7b648-106">[in] The process ID of the process to which the profiler should be attached.</span></span> <span data-ttu-id="7b648-107">Sur un ordinateur 64 bits, le nombre de bits du processus profilé doit correspondre au nombre de bits du processus déclencheur qui appelle `AttachProfiler`.</span><span class="sxs-lookup"><span data-stu-id="7b648-107">On a 64-bit machine, the profiled process's bitness must match the bitness of the trigger process that is calling `AttachProfiler`.</span></span> <span data-ttu-id="7b648-108">Si le compte d'utilisateur sous lequel `AttachProfiler` est appelé dispose de privilèges d'administrateur, le processus cible peut être n'importe quel processus sur le système.</span><span class="sxs-lookup"><span data-stu-id="7b648-108">If the user account under which `AttachProfiler` is called has administrative privileges, the target process may be any process on the system.</span></span> <span data-ttu-id="7b648-109">Sinon, le processus cible doit appartenir au même compte d'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7b648-109">Otherwise, the target process must be owned by the same user account.</span></span>  
  
 `dwMillisecondsMax`  
 <span data-ttu-id="7b648-110">[in] Durée d'attente, en millisecondes, pour qu'`AttachProfiler` se termine.</span><span class="sxs-lookup"><span data-stu-id="7b648-110">[in] The time duration, in milliseconds, for `AttachProfiler` to complete.</span></span> <span data-ttu-id="7b648-111">Le processus déclencheur doit passer un délai d'attente suffisant pour permettre au profileur spécifique de terminer son initialisation.</span><span class="sxs-lookup"><span data-stu-id="7b648-111">The trigger process should pass a timeout that is known to be sufficient for the particular profiler to complete its initialization.</span></span>  
  
 `pClsidProfiler`  
 <span data-ttu-id="7b648-112">[in] Pointeur vers le CLSID du profileur à charger.</span><span class="sxs-lookup"><span data-stu-id="7b648-112">[in] A pointer to the CLSID of the profiler to be loaded.</span></span> <span data-ttu-id="7b648-113">Le processus déclencheur peut réutiliser cette mémoire suite au retour d'`AttachProfiler`.</span><span class="sxs-lookup"><span data-stu-id="7b648-113">The trigger process can reuse this memory after `AttachProfiler` returns.</span></span>  
  
 `wszProfilerPath`  
 <span data-ttu-id="7b648-114">[in] Chemin d’accès complet au fichier DLL du profileur à charger.</span><span class="sxs-lookup"><span data-stu-id="7b648-114">[in] The full path to the profiler’s DLL file to be loaded.</span></span> <span data-ttu-id="7b648-115">Cette chaîne ne doit pas comporter plus de 260 caractères, y compris le terminateur null.</span><span class="sxs-lookup"><span data-stu-id="7b648-115">This string should contain no more than 260 characters, including the null terminator.</span></span> <span data-ttu-id="7b648-116">Si `wszProfilerPath` est null ou une chaîne vide, le Common Language Runtime (CLR) essaie de trouver l'emplacement du fichier DLL du profileur en recherchant le CLSID dans le Registre vers lequel `pClsidProfiler` pointe.</span><span class="sxs-lookup"><span data-stu-id="7b648-116">If `wszProfilerPath` is null or an empty string, the common language runtime (CLR) will try to find the location of the profiler’s DLL file by looking in the registry for the CLSID that `pClsidProfiler` points to.</span></span>  
  
 `pvClientData`  
 <span data-ttu-id="7b648-117">[in] Un pointeur vers les données à passer au profileur par la [ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md) (méthode).</span><span class="sxs-lookup"><span data-stu-id="7b648-117">[in] A pointer to data to be passed to the profiler by the [ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md) method.</span></span> <span data-ttu-id="7b648-118">Le processus déclencheur peut réutiliser cette mémoire suite au retour d'`AttachProfiler`.</span><span class="sxs-lookup"><span data-stu-id="7b648-118">The trigger process can reuse this memory after `AttachProfiler` returns.</span></span> <span data-ttu-id="7b648-119">Si `pvClientData` a la valeur null, `cbClientData` doit être égal à 0 (zéro).</span><span class="sxs-lookup"><span data-stu-id="7b648-119">If `pvClientData` is null, `cbClientData` must be 0 (zero).</span></span>  
  
 `cbClientData`  
 <span data-ttu-id="7b648-120">[in] Taille, en octets, des données vers lesquelles `pvClientData` pointe.</span><span class="sxs-lookup"><span data-stu-id="7b648-120">[in] The size, in bytes, of the data that `pvClientData` points to.</span></span>  
  
## <a name="return-value"></a><span data-ttu-id="7b648-121">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="7b648-121">Return Value</span></span>  
 <span data-ttu-id="7b648-122">Cette méthode retourne les HRESULT suivants.</span><span class="sxs-lookup"><span data-stu-id="7b648-122">This method returns the following HRESULTs.</span></span>  
  
|<span data-ttu-id="7b648-123">HRESULT</span><span class="sxs-lookup"><span data-stu-id="7b648-123">HRESULT</span></span>|<span data-ttu-id="7b648-124">Description</span><span class="sxs-lookup"><span data-stu-id="7b648-124">Description</span></span>|  
|-------------|-----------------|  
|<span data-ttu-id="7b648-125">S_OK</span><span class="sxs-lookup"><span data-stu-id="7b648-125">S_OK</span></span>|<span data-ttu-id="7b648-126">Le profileur spécifié est correctement attaché au processus cible.</span><span class="sxs-lookup"><span data-stu-id="7b648-126">The specified profiler has successfully attached to the target process.</span></span>|  
|<span data-ttu-id="7b648-127">CORPROF_E_PROFILER_ALREADY_ACTIVE</span><span class="sxs-lookup"><span data-stu-id="7b648-127">CORPROF_E_PROFILER_ALREADY_ACTIVE</span></span>|<span data-ttu-id="7b648-128">Un profileur est déjà actif ou en cours d'attachement au processus cible.</span><span class="sxs-lookup"><span data-stu-id="7b648-128">There is already a profiler active or attaching to the target process.</span></span>|  
|<span data-ttu-id="7b648-129">CORPROF_E_PROFILER_NOT_ATTACHABLE</span><span class="sxs-lookup"><span data-stu-id="7b648-129">CORPROF_E_PROFILER_NOT_ATTACHABLE</span></span>|<span data-ttu-id="7b648-130">Le profileur spécifié ne prend pas en charge l'attachement.</span><span class="sxs-lookup"><span data-stu-id="7b648-130">The specified profiler does not support attachment.</span></span> <span data-ttu-id="7b648-131">Le processus déclencheur peut essayer d'attacher un profileur différent.</span><span class="sxs-lookup"><span data-stu-id="7b648-131">The trigger process may attempt to attach a different profiler.</span></span>|  
|<span data-ttu-id="7b648-132">CORPROF_E_PROFILEE_INCOMPATIBLE_WITH_TRIGGER</span><span class="sxs-lookup"><span data-stu-id="7b648-132">CORPROF_E_PROFILEE_INCOMPATIBLE_WITH_TRIGGER</span></span>|<span data-ttu-id="7b648-133">Impossible de demander un attachement de profileur, car la version du processus cible est incompatible avec le processus actuel qui appelle `AttachProfiler`.</span><span class="sxs-lookup"><span data-stu-id="7b648-133">Unable to request a profiler attachment, because the version of the target process is incompatible with the current process that is calling `AttachProfiler`.</span></span>|  
|<span data-ttu-id="7b648-134">HRESULT_FROM_WIN32(ERROR_ACCESS_DENIED)</span><span class="sxs-lookup"><span data-stu-id="7b648-134">HRESULT_FROM_WIN32(ERROR_ACCESS_DENIED)</span></span>|<span data-ttu-id="7b648-135">L'utilisateur du processus déclencheur n'a pas accès au processus cible.</span><span class="sxs-lookup"><span data-stu-id="7b648-135">The user of the trigger process does not have access to the target process.</span></span>|  
|<span data-ttu-id="7b648-136">HRESULT_FROM_WIN32(ERROR_PRIVILEGE_NOT_HELD)</span><span class="sxs-lookup"><span data-stu-id="7b648-136">HRESULT_FROM_WIN32(ERROR_PRIVILEGE_NOT_HELD)</span></span>|<span data-ttu-id="7b648-137">L'utilisateur du processus déclencheur ne dispose pas des privilèges nécessaires pour attacher un profileur au processus cible donné.</span><span class="sxs-lookup"><span data-stu-id="7b648-137">The user of the trigger process does not have the privileges necessary to attach a profiler to the given target process.</span></span> <span data-ttu-id="7b648-138">Le journal des événements de l'application peut contenir des d'informations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="7b648-138">The application event log may contain more information.</span></span>|  
|<span data-ttu-id="7b648-139">CORPROF_E_IPC_FAILED</span><span class="sxs-lookup"><span data-stu-id="7b648-139">CORPROF_E_IPC_FAILED</span></span>|<span data-ttu-id="7b648-140">Un échec s'est produit lors de la communication avec le processus cible.</span><span class="sxs-lookup"><span data-stu-id="7b648-140">A failure occurred when communicating with the target process.</span></span> <span data-ttu-id="7b648-141">Cela se produit généralement quand le processus cible s'arrête.</span><span class="sxs-lookup"><span data-stu-id="7b648-141">This commonly happens if the target process was shutting down.</span></span>|  
|<span data-ttu-id="7b648-142">HRESULT_FROM_WIN32(ERROR_FILE_NOT_FOUND)</span><span class="sxs-lookup"><span data-stu-id="7b648-142">HRESULT_FROM_WIN32(ERROR_FILE_NOT_FOUND)</span></span>|<span data-ttu-id="7b648-143">Le processus cible n'existe pas ou n'exécute pas un CLR prenant en charge l'attachement.</span><span class="sxs-lookup"><span data-stu-id="7b648-143">The target process does not exist or is not running a CLR that supports attachment.</span></span> <span data-ttu-id="7b648-144">Cela peut indiquer que le CLR a été déchargé depuis l'appel à la méthode d'énumération du runtime.</span><span class="sxs-lookup"><span data-stu-id="7b648-144">This may indicate that the CLR was unloaded since the call to the runtime enumeration method.</span></span>|  
|<span data-ttu-id="7b648-145">HRESULT_FROM_WIN32(ERROR_TIMEOUT)</span><span class="sxs-lookup"><span data-stu-id="7b648-145">HRESULT_FROM_WIN32(ERROR_TIMEOUT)</span></span>|<span data-ttu-id="7b648-146">Le délai d'attente a expiré avant le chargement du profileur.</span><span class="sxs-lookup"><span data-stu-id="7b648-146">The timeout expired without beginning to load the profiler.</span></span> <span data-ttu-id="7b648-147">Vous pouvez réessayer l'opération d'attachement.</span><span class="sxs-lookup"><span data-stu-id="7b648-147">You can retry the attach operation.</span></span> <span data-ttu-id="7b648-148">L'expiration d'un délai d'attente se produit quand un finaliseur du processus cible s'exécute plus longtemps que la valeur du délai d'attente.</span><span class="sxs-lookup"><span data-stu-id="7b648-148">Timeouts occur when a finalizer in the target process runs for a longer time than the timeout value.</span></span>|  
|<span data-ttu-id="7b648-149">E_INVALIDARG</span><span class="sxs-lookup"><span data-stu-id="7b648-149">E_INVALIDARG</span></span>|<span data-ttu-id="7b648-150">Un ou plusieurs paramètres ont des valeurs non valides.</span><span class="sxs-lookup"><span data-stu-id="7b648-150">One or more parameters have invalid values.</span></span>|  
|<span data-ttu-id="7b648-151">E_FAIL</span><span class="sxs-lookup"><span data-stu-id="7b648-151">E_FAIL</span></span>|<span data-ttu-id="7b648-152">Un autre échec non spécifié s'est produit.</span><span class="sxs-lookup"><span data-stu-id="7b648-152">Some other, unspecified failure occurred.</span></span>|  
|<span data-ttu-id="7b648-153">Autres codes d'erreur</span><span class="sxs-lookup"><span data-stu-id="7b648-153">Other error codes</span></span>|<span data-ttu-id="7b648-154">Si du profileur [ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md) méthode retourne un HRESULT qui indique un échec, `AttachProfiler` retourne ce même HRESULT.</span><span class="sxs-lookup"><span data-stu-id="7b648-154">If the profiler’s [ICorProfilerCallback3::InitializeForAttach](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback3-initializeforattach-method.md) method returns an HRESULT that indicates failure, `AttachProfiler` returns that same HRESULT.</span></span> <span data-ttu-id="7b648-155">Dans ce cas, E_NOTIMPL est converti en CORPROF_E_PROFILER_NOT_ATTACHABLE.</span><span class="sxs-lookup"><span data-stu-id="7b648-155">In this case, E_NOTIMPL is converted to CORPROF_E_PROFILER_NOT_ATTACHABLE.</span></span>|  
  
## <a name="remarks"></a><span data-ttu-id="7b648-156">Remarques</span><span class="sxs-lookup"><span data-stu-id="7b648-156">Remarks</span></span>  
  
## <a name="memory-management"></a><span data-ttu-id="7b648-157">Gestion de la mémoire</span><span class="sxs-lookup"><span data-stu-id="7b648-157">Memory Management</span></span>  
 <span data-ttu-id="7b648-158">Conformément aux conventions COM, l'appelant d'`AttachProfiler` (par exemple, le code déclencheur créé par le développeur du profileur) est chargé de l'allocation et de la libération de la mémoire pour les données vers lesquelles le paramètre `pvClientData` pointe.</span><span class="sxs-lookup"><span data-stu-id="7b648-158">In keeping with COM conventions, the caller of `AttachProfiler` (for example, the trigger code authored by the profiler developer) is responsible for allocating and de-allocating the memory for the data that the `pvClientData` parameter points to.</span></span> <span data-ttu-id="7b648-159">Quand le CLR exécute l'appel `AttachProfiler`, il fait une copie de la mémoire vers laquelle `pvClientData` pointe et la transmet au processus cible.</span><span class="sxs-lookup"><span data-stu-id="7b648-159">When the CLR executes the `AttachProfiler` call, it makes a copy of the memory that `pvClientData` points to and transmits it to the target process.</span></span> <span data-ttu-id="7b648-160">Quand le CLR à l'intérieur du processus cible reçoit sa propre copie du bloc `pvClientData`, il passe le bloc au générateur de profils via la méthode `InitializeForAttach`, puis libère sa copie du bloc `pvClientData` du processus cible.</span><span class="sxs-lookup"><span data-stu-id="7b648-160">When the CLR inside the target process receives its own copy of the `pvClientData` block, it passes the block to the profiler through the `InitializeForAttach` method, and then deallocates its copy of the `pvClientData` block from the target process.</span></span>  
  
## <a name="requirements"></a><span data-ttu-id="7b648-161">Spécifications</span><span class="sxs-lookup"><span data-stu-id="7b648-161">Requirements</span></span>  
 <span data-ttu-id="7b648-162">**Plateformes :** consultez [requise](../../../../docs/framework/get-started/system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="7b648-162">**Platforms:** See [System Requirements](../../../../docs/framework/get-started/system-requirements.md).</span></span>  
  
 <span data-ttu-id="7b648-163">**En-tête :** CorProf.idl, CorProf.h</span><span class="sxs-lookup"><span data-stu-id="7b648-163">**Header:** CorProf.idl, CorProf.h</span></span>  
  
 <span data-ttu-id="7b648-164">**Bibliothèque :** CorGuids.lib</span><span class="sxs-lookup"><span data-stu-id="7b648-164">**Library:** CorGuids.lib</span></span>  
  
 <span data-ttu-id="7b648-165">**Versions du .NET framework :**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span><span class="sxs-lookup"><span data-stu-id="7b648-165">**.NET Framework Versions:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]</span></span>  
  
## <a name="see-also"></a><span data-ttu-id="7b648-166">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="7b648-166">See Also</span></span>  
 [<span data-ttu-id="7b648-167">Interface ICorProfilerCallback</span><span class="sxs-lookup"><span data-stu-id="7b648-167">ICorProfilerCallback Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-interface.md)  
 [<span data-ttu-id="7b648-168">ICorProfilerInfo3 (Interface)</span><span class="sxs-lookup"><span data-stu-id="7b648-168">ICorProfilerInfo3 Interface</span></span>](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo3-interface.md)  
 [<span data-ttu-id="7b648-169">Interfaces de profilage</span><span class="sxs-lookup"><span data-stu-id="7b648-169">Profiling Interfaces</span></span>](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)  
 [<span data-ttu-id="7b648-170">Profilage</span><span class="sxs-lookup"><span data-stu-id="7b648-170">Profiling</span></span>](../../../../docs/framework/unmanaged-api/profiling/index.md)