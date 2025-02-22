---
title: "Pass parameters to a URL by using the ribbon (Developer Guide for Dynamics 365 Customer Engagement) | MicrosoftDocs"
description: "Learn about passing parameters to a URL by using the ribbon"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: pehecke

ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
applies_to: 
  - Dynamics 365 Customer Engagement (on-premises)
helpviewer_keywords: 
  - ribbon
ms.assetid: 27ae5df1-fbd3-404b-bf52-40bbd2773cf6
caps.latest.revision: 24
author: JimDaly
ms.author: jdaly
manager: amyla
search.audienceType: 
  - developer

---
# Pass parameters to a URL by using the ribbon

Ribbon actions are defined in the `<Actions>` element of a `<CommandDefinition>` element. There are several ways to pass contextual [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] information as query string parameters to a URL by using the ribbon.  
  
-   Use a `<Url>` element. Within the `Url` element, use the **PassParams** attribute.  
  
-   Use a `<Url>` element together with a `<CrmParameter>` element. When used from a `Url` element, the name attribute value must be set.  
  
-   Use a `<JavaScriptFunction>` element together with a `<CrmParameter>` element.  
  
## Use the PassParams attribute to set dynamic values  
 Passing parameters to the target URL by using the **PassParams** attribute provides information to the target application about the context of the record or the user. All the parameters are passed if the ribbon control is configured by using the **PassParams** attribute. The following table lists the parameters that are passed.  
  
|Parameter|Name|Description|  
|---------------|----------|-----------------|  
|`typename`|Entity Name|Name of the entity. For custom entities, this includes the customization prefix, for example, new_entityname.|  
|`type`|Entity Type Code|Integer that uniquely identifies the entity in the current organization. **Note:**  `Entity Type Code` values are determined by the order in which an entity is created in an organization. `Entity Type Codes` for custom entities are usually different in different organizations.|  
|`id`|Object GUID|Globally unique identifier (GUID) that represents a record.|  
|`orgname`|Organization Name|Unique name of the organization.|  
|`userlcid`|User Language Code|Language code identifier that is used by the current user.|  
|`orglcid`|Organization Language Code|Language code identifier that represents the base language for the organization.|  
  
[!INCLUDE[languagecode](../../includes/languagecode.md)]
  
> [!NOTE]
>  We recommend that you use the entity name instead of the entity type code because the entity type code may be different between [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] installations.  
  
### Example  
 The following sample shows the URL without parameters:  
  
```  
https://myserver/mypage.aspx  
```  
  
 The following sample shows the parameters included when the ribbon control is presented for the account entity, for an organization called ‘AdventureWorksCycle’, when the user’s language and the organization base language is English, and the GUID for the account record is DBD5DBFB-0666-DC11-A5D9-0003FF9CE217:  
  
```  
https://myserver/mypage.aspx?orgname=AdventureWorksCycle&userlcid=1033&orglcid=1033&type=1&typename=account&id=%7BDBD5DBFB-0666-DC11-A5D9-0003FF9CE217%7D  
```  
  
## Use a Querystring parameter in the URL  
 You can include a `querystring` parameter in the URL attribute. This can be very useful if you want to open a specific [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] record or view by using [Open forms, views, dialogs, and reports with a URL](../open-forms-views-dialogs-reports-url.md).  
  
> [!NOTE]
>  You will not be able to import the ribbon if the URL includes the ampersand (&) character that is used to separate multiple `querystring` parameters in the URL. This character makes the XML invalid. You must escape the ampersand character in the URL attribute value with "&amp;".  
  
## Reading passed parameters  
 Passed parameters are usually read in the target .aspx page by using the `HttpRequest.QueryString` property. [!INCLUDE[proc_more_information](../../includes/proc-more-information.md)] [HttpRequest.QueryString Property](https://msdn.microsoft.com/library/system.web.httprequest.querystring.aspx)  
  
> [!NOTE]
>  If the target of your URL is a Web resource, it can accept only the parameters identified in the topic [Passing Parameters to HTMLWeb Resources](../webpage-html-web-resources.md#BKMK_PassingParametersToWebResources). The only opportunity to pass custom values is by including them within the `data` parameter. Some special handling is required to include multiple values in a single parameter. [!INCLUDE[proc_more_information](../../includes/proc-more-information.md)] [Sample: Passing Multiple Values to a Web Page Web Resource Through the Data Parameter](../sample-pass-multiple-values-web-resource-through-data-parameter.md)  
  
### See also

 [Customize commands and the ribbon](customize-commands-ribbon.md)   
 [Open Forms And Views with a URL](../open-forms-views-dialogs-reports-url.md)    
 [Define Ribbon Tab Display Rules](define-ribbon-tab-display-rules.md)   
 [Sample: Export Ribbon Definitions](sample-export-ribbon-definitions.md)


[!INCLUDE[footer-include](../../../../includes/footer-banner.md)]