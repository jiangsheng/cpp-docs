---
title: "How to: Use Regular Expressions to Validate Data Formatting (C++-CLI)"
ms.custom: na
ms.date: 10/03/2016
ms.devlang: 
  - C++
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-cpp
ms.tgt_pltfrm: na
ms.topic: article
H1: How to: Use Regular Expressions to Validate Data Formatting (C++/CLI)
ms.assetid: 225775c3-3efc-4734-bde2-1fdf73e3d397
caps.latest.revision: 9
manager: ghogen
translation.priority.ht: 
  - cs-cz
  - de-de
  - es-es
  - fr-fr
  - it-it
  - ja-jp
  - ko-kr
  - pl-pl
  - pt-br
  - ru-ru
  - tr-tr
  - zh-cn
  - zh-tw
---
# How to: Use Regular Expressions to Validate Data Formatting (C++-CLI)
The following code example demonstrates the use of regular expressions to verify the formatting of a string. In the following code example, the string should contain a valid phone number. The following code example uses the string "\d{3}-\d{3}-\d{4}" to indicate that each field represents a valid phone number. The "d" in the string indicates a digit, and the argument after each "d" indicates the number of digits that must be present. In this case, the number is required to be separated by dashes.  
  
## Example  
  
```  
// regex_validate.cpp  
// compile with: /clr  
#using <System.dll>  
  
using namespace System;  
using namespace Text::RegularExpressions;  
  
int main()  
{  
   array<String^>^ number =   
   {  
      "123-456-7890",   
      "444-234-22450",   
      "690-203-6578",   
      "146-893-232",  
      "146-839-2322",  
      "4007-295-1111",   
      "407-295-1111",   
      "407-2-5555",   
   };  
  
   String^ regStr = "^\\d{3}-\\d{3}-\\d{4}$";  
  
   for ( int i = 0; i < number->Length; i++ )  
   {  
      Console::Write( "{0,14}", number[i] );  
  
      if ( Regex::IsMatch( number[i], regStr ) )  
         Console::WriteLine(" - valid");  
      else  
         Console::WriteLine(" - invalid");  
   }  
   return 0;  
}  
```  
  
## See Also  
 [.NET Framework Regular Expressions](../Topic/.NET%20Framework%20Regular%20Expressions.md)   
 [.NET Programming with C++/CLI (Visual C++)](../VS_visualcpp/.NET-Programming-with-C---CLI--Visual-C---.md)