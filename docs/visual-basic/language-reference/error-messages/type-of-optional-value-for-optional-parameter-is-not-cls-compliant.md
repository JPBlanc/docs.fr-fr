---
title: "Type of optional value for optional parameter &lt;parametername&gt; is not CLS-compliant | Microsoft Docs"
ms.custom: ""
ms.date: "11/17/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "BC40042"
  - "vbc40042"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40042"
ms.assetid: 1d6eae29-4ad3-4434-bde4-a53b6051adf5
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
translationtype: Human Translation
---
# Type of optional value for optional parameter &lt;parametername&gt; is not CLS-compliant
Une procédure est marquée comme `<CLSCompliant(True)>`, mais déclare un paramètre [Optional](../../../visual-basic/language-reference/modifiers/optional.md) avec une valeur par défaut d'un type non conforme.  
  
 Pour qu'une procédure soit conforme [Indépendance du langage et composants indépendants du langage](../Topic/Language%20Independence%20and%20Language-Independent%20Components.md) \(CLS\), elle ne doit utiliser que des types conformes CLS.  Cette règle s'applique aux types des paramètres, au type de retour et aux types de toutes ses variables locales.  Cela s'applique également aux valeurs par défaut des paramètres optionnels.  
  
 Les types de données [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] suivants ne sont pas conformes CLS :  
  
-   [SByte Data Type](../../../visual-basic/language-reference/data-types/sbyte-data-type.md)  
  
-   [UInteger Data Type](../../../visual-basic/language-reference/data-types/uinteger-data-type.md)  
  
-   [ULong Data Type](../../../visual-basic/language-reference/data-types/ulong-data-type.md)  
  
-   [UShort Data Type](../../../visual-basic/language-reference/data-types/ushort-data-type.md)  
  
 Lorsque vous appliquez l'attribut <xref:System.CLSCompliantAttribute> à un élément de programmation, vous affectez au paramètre `isCompliant` de l'attribut la valeur `True` ou `False` pour indiquer la conformité ou la non\-conformité.  Il n'existe pas de valeur par défaut pour ce paramètre et vous devez fournir une valeur.  
  
 Si vous n'appliquez pas <xref:System.CLSCompliantAttribute> à un élément, il est considéré comme étant non conforme.  
  
 Par défaut, ce message est un avertissement.  Pour plus d'informations sur le masquage des avertissements ou le traitement des avertissements en tant qu'erreurs, consultez [Configuration d'avertissements en Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID d'erreur :** BC40042  
  
### Pour corriger cette erreur  
  
-   Si le paramètre optionnel doit avoir une valeur par défaut de ce type particulier, supprimez <xref:System.CLSCompliantAttribute>.  La procédure ne peut pas être conforme CLS.  
  
-   Si la procédure doit être conforme CLS, remplacez le type de cette valeur par défaut par le type conforme CLS le plus proche.  Par exemple, vous pouvez peut\-être utiliser `Integer` à la place d'`UInteger` si vous n'avez pas besoin de la plage de valeurs qui est supérieure à 2 147 483 647.  Si vous avez besoin de la plage étendue, vous pouvez remplacer `UInteger` par `Long`.  
  
-   Si vous utilisez des objets Automation ou COM, gardez à l'esprit que certains types ont des largeurs des données différentes de celles du [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  Par exemple, `int` correspond souvent à 16 bits dans d'autres environnements.  Si vous passez un argument de 16 bits à un tel composant, déclarez\-le comme type de données `Short` et non comme `Integer` dans votre code managé [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## Voir aussi  
 [\<PAVE OVER\> Writing CLS\-Compliant Code](http://msdn.microsoft.com/fr-fr/4c705105-69a2-4e5e-b24e-0633bc32c7f3)