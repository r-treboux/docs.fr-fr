---
title: '&lt;msmqIntegrationBinding&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- msmqIntegrationBinding Element
ms.assetid: edf277f3-e3bf-4ed8-9f55-83b5788430a7
caps.latest.revision: 
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload:
- dotnet
ms.openlocfilehash: 0715952077db755386a0381f68ccc6e33705a031
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="ltmsmqintegrationbindinggt"></a>&lt;msmqIntegrationBinding&gt;
Définit une liaison qui prend en charge la mise en file d’attente par routage des messages via MSMQ.  
  
 \<system.ServiceModel>  
\<bindings>  
msmqIntegrationBinding  
  
## <a name="syntax"></a>Syntaxe  
  
```xml  
<msmqIntegrationBinding>  
   <binding   
       closeTimeout="TimeSpan"   
       customDeadLetterQueue="Uri"  
       deadLetterQueue="Uri"  
       durable="Boolean"  
       exactlyOnce="Boolean"   
       maxReceivedMessageSize"Integer"  
       maxRetryCycles="Integer"   
       name="string"   
       openTimeout="TimeSpan"        receiveContextEnabled="Boolean"  
       receiveErrorHandling="Drop/Fault/Move/Reject"  
       receiveTimeout="TimeSpan"   
       receiveRetryCount="Integer"  
       retryCycleDelay="TimeSpan"    
       sendTimeout="TimeSpan"   
       serializationFormat="XML/Binary/ActiveX/ByteArray/Stream">  
       timeToLive="TimeSpan"    
       useMsmqTracing="Boolean  
       useSourceJournal="Boolean"  
   </binding>  
</msmqIntegrationBinding>   
```  
  
## <a name="attributes-and-elements"></a>Attributs et éléments  
 Les sections suivantes décrivent des attributs, des éléments enfants et des éléments parents.  
  
### <a name="attributes"></a>Attributs  
  
|Attribut|Description|  
|---------------|-----------------|  
|closeTimeout|<xref:System.TimeSpan> qui spécifie l'intervalle de temps prévu pour la réalisation d'une opération de fermeture. Cette valeur doit être supérieure ou égale à <xref:System.TimeSpan.Zero>. La valeur par défaut est 00:01:00.|  
|customDeadLetterQueue|URI contenant l'emplacement de la file d'attente de lettres mortes pour chaque application et dans laquelle sont placés les messages ayant expiré ou dont le transfert ou la remise a échoué.<br /><br /> La file d'attente de lettres mortes est une file d'attente du gestionnaire de files d'attente de l'application émettrice pour les messages ayant expiré et dont la remise a échoué.<br /><br /> L'URI spécifié par <xref:System.ServiceModel.MsmqBindingBase.CustomDeadLetterQueue%2A> doit utiliser le schéma net.msmq.|  
|deadLetterQueue|Valeur <xref:System.ServiceModel.MsmqBindingBase.DeadLetterQueue%2A> spécifiant le type de file d'attente de lettres mortes à utiliser (le cas échéant).<br /><br /> Une file d'attente de lettres mortes correspond à l'emplacement dans lequel sont transférés les messages dont la remise à l'application a échoué.<br /><br /> Pour les messages qui requièrent la garantie exactlyOnce (ceux pour lesquels l'attribut `exactlyOnce` a la valeur `true`), cet attribut a comme valeur par défaut la file d'attente de lettres mortes transactionnelle à l'échelle du système dans MSMQ.<br /><br /> Pour les messages qui ne requièrent pas de garanties, cet attribut a `null` comme valeur par défaut.|  
|fiable|Valeur booléenne qui indique si le message est fiable ou volatil dans la file d'attente. Un message durable survit à une panne du gestionnaire de files d'attente, alors qu'un message volatil n'y survit pas. Les messages volatils sont utiles lorsque les applications requièrent la latence plus faible et peuvent autoriser la perte occasionnelle de messages. Si l'attribut `exactlyOnce` a la valeur `true`, les messages doivent être fiables. La valeur par défaut est `true`.|  
|exactlyOnce|Valeur booléenne indiquant si chaque message est remis une seule fois. L'expéditeur est ensuite notifié des échecs de remise. Lorsque `durable` a pour valeur `false`, cet attribut est ignoré et les messages sont transférés sans garantie de remise. La valeur par défaut est `true`. Pour plus d'informations, consultez <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A>.|  
|maxReceivedMessageSize|Entier positif qui définit la taille maximale du message (en octets, en-têtes compris), qui est traité par cette liaison. L'expéditeur d'un message qui dépasse cette limite se verra notifier une erreur SOAP. Ce dernier abandonne le message et crée une entrée d'événement dans le journal de suivi. La valeur par défaut est 65536. Cette limite de taille des messages a pour but d'atténuer l'exposition aux attaques par déni de service (DoS).|  
|maxRetryCycles|Entier indiquant le nombre de cycles de tentatives utilisés par la fonctionnalité de détection de messages incohérents. Un message devient incohérent lorsque toutes les tentatives de remise de tous les cycles échouent. La valeur par défaut est 2. Pour plus d'informations, consultez <xref:System.ServiceModel.MsmqBindingBase.MaxRetryCycles%2A>.|  
|name|Chaîne qui contient le nom de configuration de la liaison. Cette valeur doit être unique car elle permet d'identifier la liaison. Depuis [!INCLUDE[netfx40_short](../../../../../includes/netfx40-short-md.md)], les liaisons et les comportements ne sont pas obligés d'avoir un nom. Pour plus d’informations sur la configuration par défaut et nommées liaisons et comportements, consultez [Configuration simplifiée](../../../../../docs/framework/wcf/simplified-configuration.md) et [simplifié la Configuration des Services WCF](../../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).|  
|openTimeout|<xref:System.TimeSpan> qui spécifie l'intervalle de temps prévu pour la réalisation d'une opération d'ouverture. Cette valeur doit être supérieure ou égale à <xref:System.TimeSpan.Zero>. La valeur par défaut est 00:01:00.|  
|receiveErrorHandling|Valeur <xref:System.ServiceModel.ReceiveErrorHandling> qui spécifie la façon dont sont gérés les messages incohérents et ne pouvant être distribués.|  
|receiveRetryCount|Entier indiquant le nombre maximal de nouvelles tentatives immédiates devant être effectuées par le gestionnaire de files d'attente si la transmission d'un message entre la file d'attente de l'application et l'application échoue.<br /><br /> Si le nombre maximal de tentatives de remise est atteint sans que l'application accède au message, ce dernier est envoyé à une file d'attente de nouvelles tentatives. La durée qui s'écoule avant que le message ne soit renvoyé à la file d'attente émettrice est contrôlée par `retryCycleDelay`. Si les cycles de nouvelles tentatives atteignent la valeur `maxRetryCycles`, soit le message est envoyé à la file d'attente de messages incohérents, soit un accusé de réception négatif est renvoyé à l'expéditeur.|  
|receiveTimeout|<xref:System.TimeSpan> qui spécifie l'intervalle de temps prévu pour la réalisation d'une opération de réception. Cette valeur doit être supérieure ou égale à <xref:System.TimeSpan.Zero>. La valeur par défaut est 00:10:00.|  
|receiveContextEnabled|Valeur booléenne qui spécifie si le contexte de réception pour le traitement des messages dans les files d'attente est activé. Lorsque cela est défini sur `true`, un service peut « aperçu » un message dans la file d’attente pour commencer à le traiter et, si une erreur se produit et une exception est levée, il reste dans la file d’attente. Services peuvent également « verrouiller » messages afin de nouvelle tentative de traitement à un moment ultérieur dans le temps. ReceiveContext fournit un mécanisme pour « achever » le message une fois traité, il peut être supprimée à partir de la file d’attente. Les messages sont n’est plus files d’attente de lecture et ré-écrits dans sur le réseau, et des messages individuels ne sont pas rebondissent entre les instances de service différent au cours du traitement.|  
|retryCycleDelay|Valeur TimeSpan qui spécifie l'intervalle entre les cycles de nouvelles tentatives de remise d'un message n'ayant pas pu être remis immédiatement. Cette valeur définit uniquement le délai d'attente minimum, car le temps d'attente réel peut être plus long. La valeur par défaut est 00:30:00. Pour plus d'informations, consultez <xref:System.ServiceModel.MsmqBindingBase.RetryCycleDelay%2A>.|  
|sendTimeout|<xref:System.TimeSpan> qui spécifie l'intervalle de temps prévu pour la réalisation d'une opération d'envoi. Cette valeur doit être supérieure ou égale à <xref:System.TimeSpan.Zero>. La valeur par défaut est 00:01:00.|  
|serializationFormat|Définit le format utilisé pour la sérialisation du corps du message. Cet attribut est de type <xref:System.ServiceModel.MsmqIntegration.MsmqMessageSerializationFormat>.|  
|timeToLive|Valeur TimeSpan qui spécifie la durée de validité des messages avant leur expiration et leur déplacement dans la file d'attente de lettres mortes. La valeur par défaut est 1.00:00:00.<br /><br /> Cet attribut est configuré de façon à garantir que les messages dépendants de l'heure n'expirent pas avant d'être traités par les applications de réception. Un message dans une file d'attente qui n'est pas consommé par l'application de réception dans l'intervalle de temps spécifié est considéré comme ayant expiré. Les messages ayant expiré sont envoyés dans une file d'attente spéciale appelée file d'attente de lettres mortes. L'emplacement de cette file d'attente est défini par l'attribut `DeadLetterQueue` ou par la valeur par défaut appropriée, en fonction des garanties utilisées.|  
|useMsmqTracing|Valeur booléenne indiquant si les messages traités par cette liaison doivent être suivis. La valeur par défaut est `false`. Lorsque le suivi est activé, des messages de rapport sont créés et envoyés à la file d'attente de rapports chaque fois que le message quitte ou atteint un ordinateur Message Queuing.|  
|useSourceJournal|Valeur booléenne qui spécifie si les copies de messages traitées par cette liaison doivent être stockées dans le journal source. La valeur par défaut est `false`.<br /><br /> Les applications en file d'attente souhaitant conserver une trace des messages qui ont quitté la file d'attente sortante de l'ordinateur peuvent copier les messages dans une file d'attente de journal. Une fois qu'un message quitte la file d'attente sortante et qu'un accusé de réception est envoyé par l'ordinateur de destination, une copie du message est conservée dans la file d'attente du journal système de l'ordinateur émetteur.|  
  
## <a name="serializationformat-attribute"></a>Attribut {serializationFormat}  
  
|Valeur|Description|  
|-----------|-----------------|  
|Xml|Format XML|  
|Binaire|Format binaire|  
|ActiveX|Format ActiveX|  
|ByteArray|Sérialise l'objet en un tableau d'octets.|  
|Flux de données|Corps mis en forme en tant que flux|  
  
### <a name="child-elements"></a>Éléments enfants  
  
|Élément|Description|  
|-------------|-----------------|  
|[\<security>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-msmqintegrationbinding.md)|Définit les paramètres de sécurité de la liaison. Cet élément est de type <xref:System.ServiceModel.Configuration.MsmqIntegrationSecurityElement>.|  
  
### <a name="parent-elements"></a>Éléments parents  
  
|Élément|Description|  
|-------------|-----------------|  
|[\<bindings>](../../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md)|Cet élément conserve une collection de liaisons standard et personnalisées.|  
  
## <a name="remarks"></a>Notes  
 Cet élément de liaison peut être utilisé pour permettre aux applications de Windows Communication Foundation (WCF) envoyer des messages à et recevoir des messages à partir des applications MSMQ existantes qui utilisent MSMQ des API natives COM ou les types définis dans le <xref:System.Messaging?displayProperty=nameWithType> espace de noms vous peut utiliser cet élément de configuration pour spécifier les façons de régler la file d’attente, les assurances de transfert, si les messages doivent être stockés de façon durable, et comment les messages doivent être protégés et authentifiés. Pour plus d’informations, consultez [Comment : échanger des Messages avec les points de terminaison WCF et les Applications Message Queuing](../../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md).  
  
## <a name="example"></a>Exemple  
  
```xml  
<configuration>  
<system.ServiceModel>  
    <bindings>  
       <msmqIntegrationBinding>  
           <binding   
                    closeTimeout="00:00:10"   
                    openTimeout="00:00:20"   
                    receiveTimeout="00:00:30"   
                    sendTimeout="00:00:40"   
                    deadLetterQueue="net.msmq://localhost/blah"   
                    durable="true"   
                    exactlyOnce="true"   
                    maxReceivedMessageSize="1000"   
                    maxImmediateRetries="11"   
                    maxRetryCycles="12"  
                    poisonMessageHandling="Disabled"   
                    rejectAfterLastRetry="false"   
                    retryCycleDelay="00:05:55"   
                    timeToLive="00:11:11"   
                    useSourceJournal="true"   
                    useMsmqTracing="true"   
                    serializationFormat="Binary">  
                    <security mode="None" />  
           </binding>  
       </msmqIntegrationBinding  
   </bindings>  
</system.ServiceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>Voir aussi  
 <xref:System.ServiceModel.Configuration.MsmqIntegrationBindingElement>  
 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>  
 <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBindingElement>  
 [\<binding>](../../../../../docs/framework/misc/binding.md)  
 [Liaisons](../../../../../docs/framework/wcf/bindings.md)  
 [Configuration des liaisons fournies par le système](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)  
 [Utilisation de liaisons pour configurer les Clients et les Services Windows Communication Foundation](http://msdn.microsoft.com/library/bd8b277b-932f-472f-a42a-b02bb5257dfb)  
 [Files d’attente dans WCF](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)
