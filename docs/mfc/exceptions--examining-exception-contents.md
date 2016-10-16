---
title: "Exceptions: Examining Exception Contents"
ms.custom: na
ms.date: "10/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: na
ms.suite: na
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: na
ms.topic: "article"
dev_langs: 
  - "C++"
helpviewer_keywords: 
  - "exception handling, MFC"
  - "try-catch exception handling, MFC function exceptions"
  - "catch blocks, MFC function exceptions"
  - "CException class, class exceptions"
  - "try-catch exception handling, exception contents"
  - "throwing exceptions, exception contents"
ms.assetid: dfda4782-b969-4f60-b867-cc204ea7f33a
caps.latest.revision: 8
ms.author: "mblome"
manager: "ghogen"
translation.priority.ht: 
  - "cs-cz"
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "pl-pl"
  - "pt-br"
  - "ru-ru"
  - "tr-tr"
  - "zh-cn"
  - "zh-tw"
---
# Exceptions: Examining Exception Contents
Although a **catch** block's argument can be of almost any data type, the MFC functions throw exceptions of types derived from the class `CException`. To catch an exception thrown by an MFC function, then, you write a **catch** block whose argument is a pointer to a `CException` object (or an object derived from `CException`, such as `CMemoryException`). Depending on the exact type of the exception, you can examine the data members of the exception object to gather information about the specific cause of the exception.  
  
 For example, the `CFileException` type has the `m_cause` data member, which contains an enumerated type that specifies the cause of the file exception. Some examples of the possible return values are **CFileException::fileNotFound** and **CFileException::readOnly**.  
  
 The following example shows how to examine the contents of a `CFileException`. Other exception types can be examined similarly.  
  
 [!code[NVC_MFCExceptions#13](../mfc/codesnippet/CPP/exceptions--examining-exception-contents_1.cpp)]  
  
 For more information, see [Exceptions: Freeing Objects in Exceptions](../mfc/exceptions--freeing-objects-in-exceptions.md) and [Exceptions: Catching and Deleting Exceptions](../mfc/exceptions--catching-and-deleting-exceptions.md).  
  
## See Also  
 [Exception Handling](../mfc/exception-handling-in-mfc.md)