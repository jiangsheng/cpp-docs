---
title: "ML Nonfatal Error A2206 | Microsoft Docs"
ms.custom: ""
ms.date: "11/04/2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: ["cpp-tools"]
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: ["A2206"]
dev_langs: ["C++"]
helpviewer_keywords: ["A2206"]
ms.assetid: 711846d0-5a09-4353-8857-60588c25526a
caps.latest.revision: 6
author: "corob-msft"
ms.author: "corob"
manager: "ghogen"
---
# ML Nonfatal Error A2206
**missing operator in expression**  
  
 An expression cannot be evaluated because it is missing an operator. This error message may also be a side-effect of a preceding program error.  
  
 The following line will generate this error:  
  
```  
value1 = ( 1 + 2 ) 3  
  
```  
  
## See Also  
 [ML Error Messages](../../assembler/masm/ml-error-messages.md)