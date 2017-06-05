---
title: "Audit des &#233;v&#233;nements de s&#233;curit&#233; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "audit des événements de sécurité (WCF)"
ms.assetid: 5633f61c-a3c9-40dd-8070-1c373b66a716
caps.latest.revision: 27
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 27
---
# Audit des &#233;v&#233;nements de s&#233;curit&#233;
Les applications créées avec [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] peuvent enregistrer des événements de sécurité \(succès, échec, ou les deux\) à l'aide de la fonctionnalité d'audit.Les événements sont écrits dans le journal des événements système Windows et peuvent être examinés à l'aide de l'Observateur d'événements.  
  
 L'audit permet à un administrateur de détecter une attaque que s'est déjà produite ou qui est en cours.En outre, l'audit permet de déboguer des problèmes relatifs à la sécurité.Par exemple, si une erreur dans la configuration de la stratégie d'autorisation ou de vérification refuse accidentellement l'accès à un utilisateur autorisé, un développeur peut la détecter rapidement et en isoler la cause en examinant le journal des événements.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] la sécurité, consultez [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], consultez [Vue d'ensemble de la sécurité](../../../../docs/framework/wcf/feature-details/security-overview.md).[!INCLUDE[crabout](../../../../includes/crabout-md.md)] la programmation [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], consultez [Programmation WCF de base](../../../../docs/framework/wcf/basic-wcf-programming.md).  
  
## Niveau et comportement d'audit  
 Il existe deux niveaux d'audit de sécurité :  
  
-   Niveau d'autorisation de service, dans lequel un appelant est autorisé.  
  
-   Niveau de message, dans lequel [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vérifie la validité du message et authentifie l'appelant.  
  
 La vérification de l'échec ou de la réussite de ces deux niveaux d'audit est appelée *comportement de vérification*.  
  
## Emplacement du journal d'audit  
 Après avoir déterminé un niveau et un comportement d'audit, vous \(ou un administrateur\) pouvez spécifier l'emplacement du journal d'audit.Vous disposez pour cela de trois options : Default, Application et Security.Lorsque vous spécifiez Default, le journal réel dépend du système que vous utilisez et du fait que celui\-ci prend ou non en charge l'écriture dans le journal Security.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la section « Système d'exploitation » plus loin dans cette rubrique.  
  
 L'écriture dans le journal Security requiert le privilège `SeAuditPrivilege`.Par défaut, seuls les comptes Système local et Service réseau possèdent ce privilège.La gestion des fonctions du journal Security `read` et `delete` requièrent le privilège `SeSecurityPrivilege`.Par défaut, seuls les administrateurs possèdent ce privilège.  
  
 En revanche, les utilisateurs authentifiés peuvent lire et écrire dans le journal des applications.[!INCLUDE[wxp](../../../../includes/wxp-md.md)] écrit par défaut les événements d'audit dans le journal des applications.Le journal peut également contenir des informations personnelles accessibles à tous les utilisateurs authentifiés.  
  
## Suppression des échecs d'audit  
 Une autre option pendant l'audit permet de déterminer s'il faut supprimer les échecs d'audit.Par défaut, un échec d'audit n'affecte pas une application.Toutefois, si cela s'avère nécessaire, vous pouvez affecter `false` à l'option, ce qui provoque la levée d'une exception.  
  
## Programmation de l'audit  
 Vous pouvez spécifier le comportement d'audit par programme ou via la configuration.  
  
### Classes d'audit  
 Le tableau suivant décrit les classes et propriétés utilisées pour programmer le comportement d'audit.  
  
|Classe|Description|  
|------------|-----------------|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>|Permet de définir les options d'audit en tant que comportement de service.|  
|<xref:System.ServiceModel.AuditLogLocation>|Énumération permettant de spécifier le journal dans lequel écrire.Les valeurs possibles sont Default, Application et Security.Lorsque vous sélectionnez Default, le système d'exploitation détermine l'emplacement du journal réel.Consultez la section « Sélection du journal des événements Application ou Security » développée ultérieurement dans cette rubrique.|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.MessageAuthenticationAuditLevel%2A>|Spécifie les types d'événements d'authentification de message audités au niveau du message.Les options disponibles sont `None`, `Failure`, `Success` et `SuccessOrFailure`.|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.ServiceAuthorizationAuditLevel%2A>|Spécifie les types d'événements d'autorisation de service audités au niveau du service.Les options disponibles sont `None`, `Failure`, `Success` et `SuccessOrFailure`.|  
|<xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A>|Spécifie ce que devient demande du client en cas d'échec de l'audit.Par exemple, lorsque le service tente d'écrire dans le journal Security, mais n'a pas `SeAuditPrivilege`.La valeur par défaut `true` indique que les échecs sont ignorés et que la demande du client est traitée normalement.|  
  
 Pour obtenir un exemple de configuration d'une application pour enregistrer des événements d'audit, consultez [Comment : auditer des événements de sécurité](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md).  
  
### Configuration  
 Vous pouvez également utiliser la configuration pour spécifier le comportement d'audit en ajoutant [\<serviceSecurityAudit\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md) sous [\<comportements\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md).Vous devez ajouter l'élément sous [\<comportement\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md), tel qu'indiqué dans le code suivant.  
  
```  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <behavior>  
        <!— auditLogLocation="Application" or "Security" -—>  
        <serviceSecurityAudit  
                  auditLogLocation="Application"  
                  suppressAuditFailure="true"  
                  serviceAuthorizationAuditLevel="Failure"  
                  messageAuthenticationAuditLevel="SuccessOrFailure" />   
      </behavior>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
 Si l'audit est activé et que `auditLogLocation` n'est pas spécifié, le nom de journal par défaut est "Security" pour la plateforme qui prend en charge l'écriture dans le journal Security, sinon il s'agit de "Application".Seuls les systèmes d'exploitation [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] et [!INCLUDE[wv](../../../../includes/wv-md.md)] prennent en charge l'écriture dans le journal Security.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la section « Système d'exploitation » plus loin dans cette rubrique.  
  
## Considérations sur la sécurité  
 Si un utilisateur malveillant sait que l'audit est activé, cet intrus peut envoyer des messages non valides pour provoquer l'écriture d'entrées d'audit.Si le journal d'audit se remplit de cette manière, le système d'audit échoue.Pour minimiser ce problème, affectez à la propriété <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior.SuppressAuditFailure%2A> la valeur `true` et utilisez les propriétés de l'Observateur d'événements pour contrôler le comportement d'audit.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'article de support technique Microsoft concernant l'affichage et la gestion des journaux des événements à l'aide de l'Observateur d'événements dans Windows XP disponible dans [Procédure : afficher et gérer les journaux des événements dans l'Observateur d'événements dans Windows XP](http://go.microsoft.com/fwlink/?LinkId=89150) \(cette page peut être en anglais\).  
  
 Les événements d'audit écrits dans le journal Application sur [!INCLUDE[wxp](../../../../includes/wxp-md.md)] sont accessibles aux utilisateurs authentifiés.  
  
## Sélection du journal des événements Application ou Security  
 Les tableaux suivants fournissent des informations vous permettant d'identifier si vous devez procéder à l'enregistrement dans le journal des événements Application ou dans le journal des événements Security.  
  
#### Système d'exploitation  
  
|Système|Journal Application|Journal Security|  
|-------------|-------------------------|----------------------|  
|[!INCLUDE[wxpsp2](../../../../includes/wxpsp2-md.md)] ou version ultérieure|Pris en charge|Non pris en charge|  
|[!INCLUDE[ws2003sp1](../../../../includes/ws2003sp1-md.md)] et [!INCLUDE[wv](../../../../includes/wv-md.md)]|Pris en charge|Le contexte de thread doit posséder `SeAuditPrivilege`|  
  
#### Autres facteurs  
 Outre le système d'exploitation, le tableau suivant décrit les autres paramètres qui contrôlent l'activation de l'enregistrement.  
  
|Facteur|Journal Application|Journal Security|  
|-------------|-------------------------|----------------------|  
|Gestion de la stratégie d'audit|Non applicable.|Outre la configuration, le journal Security est également contrôlé par la stratégie de l'autorité de sécurité locale \(LSA\).La catégorie "Audit object access" doit également être activée.|  
|Expérience utilisateur par défaut|Tous les utilisateurs authentifiés pouvant écrire dans le journal Application, aucune étape d'autorisation supplémentaire n'est donc nécessaire pour les processus d'application.|Le processus d'application \(contexte\) doit avoir `SeAuditPrivilege`.|  
  
## Voir aussi  
 <xref:System.ServiceModel.Description.ServiceSecurityAuditBehavior>   
 <xref:System.ServiceModel.AuditLogLocation>   
 [Vue d'ensemble de la sécurité](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [Programmation WCF de base](../../../../docs/framework/wcf/basic-wcf-programming.md)   
 [Comment : auditer des événements de sécurité](../../../../docs/framework/wcf/feature-details/how-to-audit-wcf-security-events.md)   
 [\<serviceSecurityAudit\>](../../../../docs/framework/configure-apps/file-schema/wcf/servicesecurityaudit.md)   
 [\<comportements\>](../../../../docs/framework/configure-apps/file-schema/wcf/behaviors.md)   
 [Modèle de sécurité pour Windows Server AppFabric](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x409)