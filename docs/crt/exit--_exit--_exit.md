---
title: "exit, _Exit, _exit"
ms.custom: na
ms.date: "10/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: na
ms.suite: na
ms.technology: 
  - "devlang-cpp"
ms.tgt_pltfrm: na
ms.topic: "article"
apiname: 
  - "_exit"
  - "exit"
apilocation: 
  - "msvcrt.dll"
  - "msvcr80.dll"
  - "msvcr90.dll"
  - "msvcr100.dll"
  - "msvcr100_clr0400.dll"
  - "msvcr110.dll"
  - "msvcr110_clr0400.dll"
  - "msvcr120.dll"
  - "msvcr120_clr0400.dll"
  - "ucrtbase.dll"
  - "api-ms-win-crt-runtime-l1-1-0.dll"
apitype: "DLLExport"
f1_keywords: 
  - "Exit"
  - "_exit"
  - "process/exit"
  - "process/_Exit"
  - "stdlib/exit"
  - "stdlib/_Exit"
dev_langs: 
  - "C++"
  - "C"
helpviewer_keywords: 
  - "exit function"
  - "_exit function"
  - "processes, terminating"
  - "function calls, terminating"
  - "process termination, calling"
ms.assetid: b1501fa6-27c2-478c-9e93-cc4fd802a01f
caps.latest.revision: 17
ms.author: "corob"
manager: "ghogen"
translation.priority.ht: 
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
translation.priority.mt: 
  - "cs-cz"
  - "pl-pl"
  - "pt-br"
  - "tr-tr"
---
# exit, _Exit, _exit
Terminates the calling process. The `exit` function terminates it after cleanup; `_exit` and `_Exit` terminate it immediately.  
  
> [!NOTE]
>  Do not use this method to shut down a Universal Windows Platform (UWP) app or a [!INCLUDE[win8_appname_long](../build/includes/win8_appname_long_md.md)] app, except in testing or debugging scenarios. Programmatic or UI ways to close a [!INCLUDE[win8_appname_long](../build/includes/win8_appname_long_md.md)] app are not permitted. For more information about Windows 8 and 8.1 apps, see [App lifecycle](http://go.microsoft.com/fwlink/?LinkId=262853). For more information about Windows 10 apps, see [How-to guides for Windows 10 apps](http://go.microsoft.com/fwlink/p/?linkid=619133).  
  
## Syntax  
  
```  
void exit(   
   int const status   
);  
void _Exit(   
   int const status   
);  
void _exit(   
   int const status   
);  
```  
  
#### Parameters  
 `status`  
 Exit status code.  
  
## Remarks  
 The `exit`, `_Exit` and `_exit` functions terminate the calling process. The `exit` function calls destructors for thread-local objects, then calls—in last-in-first-out (LIFO) order—the functions that are registered by `atexit` and `_onexit`, and then flushes all file buffers before it terminates the process. The `_Exit` and `_exit` functions terminate the process without destroying thread-local objects or processing `atexit` or `_onexit` functions, and without flushing stream buffers.  
  
 Although the `exit`, `_Exit` and `_exit` calls do not return a value, the low-order byte of `status` is made available to the host environment or waiting calling process, if one exists, after the process exits. Typically, the caller sets the `status` value to 0 to indicate a normal exit, or to some other value to indicate an error. The `status` value is available to the operating-system batch command `ERRORLEVEL` and is represented by one of two constants: `EXIT_SUCCESS`, which represents a value of 0, or `EXIT_FAILURE`, which represents a value of 1.  
  
 The `exit`, `_Exit`, `_exit`, `quick_exit`, `_cexit`, and `_c_exit` functions behave as follows.  
  
|Function|Description|  
|--------------|-----------------|  
|`exit`|Performs complete C library termination procedures, terminates the process, and provides the supplied status code to the host environment.|  
|`_Exit`|Performs minimal C library termination procedures, terminates the process, and provides the supplied status code to the host environment.|  
|`_exit`|Performs minimal C library termination procedures, terminates the process, and provides the supplied status code to the host environment.|  
|`quick_exit`|Performs quick C library termination procedures, terminates the process, and provides the supplied status code to the host environment.|  
|`_cexit`|Performs complete C library termination procedures and returns to the caller. Does not terminate the process.|  
|`_c_exit`|Performs minimal C library termination procedures and returns to the caller. Does not terminate the process.|  
  
 When you call the `exit`,  `_Exit` or `_exit` function, the destructors for any temporary or automatic objects that exist at the time of the call are not called. An automatic object is defined in a function where the object is not declared to be static. A temporary object is an object that's created by the compiler. To destroy an automatic object before you call `exit`, `_Exit`, or `_exit`, explicitly call the destructor for the object, as follows:  
  
```  
myObject.myClass::~myClass();  
```  
  
 Do not use `DLL_PROCESS_ATTACH` to call `exit` from `DllMain`. If you want to exit the `DLLMain` function, return `FALSE` from `DLL_PROCESS_ATTACH`.  
  
## Requirements  
  
|Function|Required header|  
|--------------|---------------------|  
|`exit`, `_Exit`, `_exit`|\<process.h> or \<stdlib.h>|  
  
 For additional compatibility information, see [Compatibility](../crt/compatibility.md).  
  
## Example  
  
```  
// crt_exit.c  
// This program returns an exit code of 1. The  
// error code could be tested in a batch file.  
  
#include <stdlib.h>  
  
int main( void )  
{  
   exit( 1 );  
}  
```  
  
## .NET Framework Equivalent  
 [System::Diagnostics::Process::Kill](https://msdn.microsoft.com/en-us/library/system.diagnostics.process.kill.aspx)  
  
## See Also  
 [Process and Environment Control](../crt/process-and-environment-control.md)   
 [abort](../crt/abort.md)   
 [atexit](../crt/atexit.md)   
 [_cexit, _c_exit](../crt/_cexit--_c_exit.md)   
 [_exec, _wexec Functions](../crt/_exec--_wexec-functions.md)   
 [_onexit, _onexit_m](../crt/_onexit--_onexit_m.md)   
 [quick_exit](../crt/quick_exit1.md)   
 [_spawn, _wspawn Functions](../crt/_spawn--_wspawn-functions.md)   
 [system, _wsystem](../crt/system--_wsystem.md)