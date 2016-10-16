---
title: "Iterating Over STL Collection By Using for each"
ms.custom: na
ms.date: 10/04/2016
ms.devlang: 
  - C++
ms.prod: visual-studio-dev14
ms.reviewer: na
ms.suite: na
ms.technology: 
  - devlang-cpp
ms.tgt_pltfrm: na
ms.topic: reference
ms.assetid: 9358ca29-b982-4a19-bbfd-bef50fe66c9a
caps.latest.revision: 12
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
# Iterating Over STL Collection By Using for each
The `for each` keyword can be used to iterate over a Standard C++ Library (STL) collection.  
  
## All Platforms  
 **Remarks**  
  
 An STL collection is also known as a *container*. For more information, see [STL Containers](../VS_visualcpp/STL-Containers.md).  
  
## Examples  
 **Example**  
  
 The following code example uses `for each` to iterate over a [<map\>](../VS_visualcpp/-map-.md).  
  
```  
// for_each_stl.cpp  
// compile with: /EHsc  
#include <map>  
#include <iostream>  
#include <string>  
using namespace std;  
  
int main() {  
   int retval  = 0;  
   map<string, int> months;  
  
   months["january"] = 31;  
   months["february"] = 28;  
   months["march"] = 31;  
   months["april"] = 30;  
   months["may"] = 31;  
   months["june"] = 30;  
   months["july"] = 31;  
   months["august"] = 31;  
   months["september"] = 30;  
   months["october"] = 31;  
   months["november"] = 30;  
   months["december"] = 31;  
  
   map<string, int> months_30;  
  
   for each( pair<string, int> c in months )  
      if ( c.second == 30 )  
         months_30[c.first] = c.second;  
  
   for each( pair<string, int> c in months_30 )  
      retval++;  
  
   cout << "Months with 30 days = " << retval << endl;  
}  
```  
  
 **Output**  
  
 **Months with 30 days = 4** **Example**  
  
 The following code example uses a const reference (`const&`) for an iteration variable with STL containers. You can use a reference (`&`) as an iteration variable on any collection of a type that can be declared as a *T*`&`.  
  
```  
// for_each_stl_2.cpp  
// compile with: /EHsc  
#include <vector>  
#include <iostream>  
using namespace std;  
  
int main() {  
   int retval = 0;  
  
   vector<int> col(3);  
   col[0] = 10;  
   col[1] = 20;  
   col[2] = 30;  
  
   for each( const int& c in col )  
      retval += c;  
  
   cout << "retval: " << retval << endl;  
}  
```  
  
 **Output**  
  
 **retval: 60**   
## Windows Runtime  
 **Remarks**  
  
 There are no platform-specific remarks about this feature.  
  
### Requirements  
 Compiler option: **/ZW**  
  
## Common Language Runtime  
 **Remarks**  
  
 There are no platform-specific remarks about this feature.  
  
### Requirements  
 Compiler option: **/clr**  
  
## See Also  
 [for each, in](../VS_visualcpp/for-each--in.md)   
 [Component Extensions for Runtime Platforms](../VS_visualcpp/Component-Extensions-for-Runtime-Platforms.md)