---
title: "vsscanf_s, vswscanf_s"
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
apiname: 
  - vswscanf_s
  - vsscanf_s
apilocation: 
  - msvcrt.dll
  - msvcr80.dll
  - msvcr90.dll
  - msvcr100.dll
  - msvcr100_clr0400.dll
  - msvcr110.dll
  - msvcr110_clr0400.dll
  - msvcr120.dll
  - msvcr120_clr0400.dll
  - ucrtbase.dll
apitype: DLLExport
ms.assetid: 7b732e68-c6f4-4579-8917-122f5a7876e1
caps.latest.revision: 4
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
# vsscanf_s, vswscanf_s
Reads formatted data from a string. These versions of [vsscanf, vswscanf](../VS_visualcpp/vsscanf--vswscanf.md) have security enhancements, as described in [Security Features in the CRT](../VS_visualcpp/Security-Features-in-the-CRT.md).  
  
## Syntax  
  
```  
int vsscanf_s(  
   const char *buffer,  
   const char *format,  
   va_list argptr  
);   
int vswscanf_s(  
   const wchar_t *buffer,  
   const wchar_t *format,  
   va_list arglist  
);   
```  
  
#### Parameters  
 `buffer`  
 Stored data  
  
 `format`  
 Format-control string. For more information, see [Format Specification Fields: scanf and wscanf Functions](../VS_visualcpp/Format-Specification-Fields--scanf-and-wscanf-Functions.md).  
  
 `arglist`  
 Variable argument list.  
  
## Return Value  
 Each of these functions returns the number of fields that are successfully converted and assigned; the return value does not include fields that were read but not assigned. A return value of 0 indicates that no fields were assigned. The return value is `EOF` for an error or if the end of the string is reached before the first conversion.  
  
 If `buffer` or `format` is a `NULL` pointer, the invalid parameter handler is invoked, as described in [Parameter Validation](../VS_visualcpp/Parameter-Validation.md). If execution is allowed to continue, these functions return -1 and set `errno` to `EINVAL`  
  
 For information about these and other error codes, see [errno, _doserrno, _sys_errlist, and _sys_nerr](../VS_visualcpp/errno--_doserrno--_sys_errlist--and-_sys_nerr.md).  
  
## Remarks  
 The `vsscanf_s` function reads data from `buffer` into the locations that are given by each argument in the `arglist` argument list. The arguments in the argument list specify pointers to variables that have a type that corresponds to a type specifier in `format`. Unlike the less secure version `vsscanf`, a buffer size parameter is required when you use the type field characters `c`, `C`, `s`, `S`, or string-control sets that are enclosed in `[]`. The buffer size in characters must be supplied as an additional parameter immediately after each buffer parameter that requires it.  
  
 The buffer size includes the terminating null. A width specification field may be used to ensure that the token that's read in will fit into the buffer. If no width specification field is used, and the token read in is too big to fit in the buffer, nothing is written to that buffer.  
  
 For more information, see [scanf_s, _scanf_s_l, wscanf_s, _wscanf_s_l](../VS_visualcpp/scanf_s--_scanf_s_l--wscanf_s--_wscanf_s_l.md) and [scanf Type Field Characters](../VS_visualcpp/scanf-Type-Field-Characters.md).  
  
> [!NOTE]
>  The size parameter is of type `unsigned`, not `size_t`.  
  
 The `format` argument controls the interpretation of the input fields and has the same form and function as the `format` argument for the `scanf_s` function. If copying occurs between strings that overlap, the behavior is undefined.  
  
 `vswscanf_s` is a wide-character version of `vsscanf_s`; the arguments to `vswscanf_s` are wide-character strings. `vsscanf_s` does not handle multibyte hexadecimal characters. `vswscanf_s` does not handle Unicode full-width hexadecimal or "compatibility zone" characters. Otherwise, `vswscanf_s` and `vsscanf_s` behave identically.  
  
### Generic-Text Routine Mappings  
  
|TCHAR.H routine|_UNICODE & _MBCS not defined|_MBCS defined|_UNICODE defined|  
|---------------------|------------------------------------|--------------------|-----------------------|  
|`_vstscanf_s`|`vsscanf_s`|`vsscanf_s`|`vswscanf_s`|  
  
## Requirements  
  
|Routine|Required header|  
|-------------|---------------------|  
|`vsscanf_s`|<stdio.h>|  
|`vswscanf_s`|<stdio.h> or <wchar.h>|  
  
 For additional compatibility information, see [Compatibility](../VS_visualcpp/Compatibility.md).  
  
## Example  
  
```  
// crt_vsscanf_s.c  
// compile with: /W3  
// This program uses vsscanf_s to read data items  
// from a string named tokenstring, then displays them.  
  
#include <stdio.h>  
#include <stdarg.h>  
#include <stdlib.h>  
  
int call_vsscanf_s(char *tokenstring, char *format, ...)  
{  
    int result;  
    va_list arglist;  
    va_start(arglist, format);  
    result = vsscanf_s(tokenstring, format, arglist);  
    va_end(arglist);  
    return result;  
}  
  
int main( void )  
{  
    char  tokenstring[] = "15 12 14...";  
    char  s[81];  
    char  c;  
    int   i;  
    float fp;  
  
    // Input various data from tokenstring:  
    // max 80 character string:  
    call_vsscanf_s(tokenstring, "%80s", s, _countof(s));  
    call_vsscanf_s(tokenstring, "%c", &c, sizeof(char));  
    call_vsscanf_s(tokenstring, "%d", &i);  
    call_vsscanf_s(tokenstring, "%f", &fp);  
  
    // Output the data read  
    printf("String    = %s\n", s);  
    printf("Character = %c\n", c);  
    printf("Integer:  = %d\n", i);  
    printf("Real:     = %f\n", fp);  
}  
```  
  
 **String    = 15**  
**Character = 1**  
**Integer:  = 15**  
**Real:     = 15.000000**   
## .NET Framework Equivalent  
 See `Parse` methods, such as [System::Double::Parse](https://msdn.microsoft.com/en-us/library/system.double.parse.aspx).  
  
## See Also  
 [Stream I/O](../VS_visualcpp/Stream-I-O.md)   
 [scanf, _scanf_l, wscanf, _wscanf_l](../VS_visualcpp/scanf--_scanf_l--wscanf--_wscanf_l.md)   
 [sscanf, _sscanf_l, swscanf, _swscanf_l](../VS_visualcpp/sscanf--_sscanf_l--swscanf--_swscanf_l.md)   
 [sscanf_s, _sscanf_s_l, swscanf_s, _swscanf_s_l](../VS_visualcpp/sscanf_s--_sscanf_s_l--swscanf_s--_swscanf_s_l.md)   
 [sprintf, _sprintf_l, swprintf, _swprintf_l, \__swprintf_l](../VS_visualcpp/sprintf--_sprintf_l--swprintf--_swprintf_l--__swprintf_l.md)   
 [vsscanf, vswscanf](../VS_visualcpp/vsscanf--vswscanf.md)