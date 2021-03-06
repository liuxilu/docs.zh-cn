---
title: COR_PRF_FUNCTION_ARGUMENT_INFO 结构
ms.date: 03/30/2017
api_name:
- COR_PRF_FUNCTION_ARGUMENT_INFO
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- COR_PRF_FUNCTION_ARGUMENT_INFO
helpviewer_keywords:
- COR_PRF_FUNCTION_ARGUMENT_INFO structure [.NET Framework profiling]
ms.assetid: 07cf3bab-e193-4991-8205-3f41cf2d67b3
topic_type:
- apiref
ms.openlocfilehash: c92ee580caed9f1fb87a31b676747769ad31a0e2
ms.sourcegitcommit: b11efd71c3d5ce3d9449c8d4345481b9f21392c6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76867242"
---
# <a name="cor_prf_function_argument_info-structure"></a>COR_PRF_FUNCTION_ARGUMENT_INFO 结构
按从左向右的顺序表示函数的参数。  
  
## <a name="syntax"></a>语法  
  
```cpp  
typedef struct _COR_PRF_FUNCTION_ARGUMENT_INFO {  
    ULONG numRanges;  
    ULONG totalArgumentSize;  
    COR_PRF_FUNCTION_ARGUMENT_RANGE ranges[1];  
} COR_PRF_FUNCTION_ARGUMENT_INFO;  
```  
  
## <a name="members"></a>Members  
  
|成员|描述|  
|------------|-----------------|  
|`numRanges`|参数块的数目。 也就是说，此值是 `ranges` 数组中[COR_PRF_FUNCTION_ARGUMENT_RANGE](cor-prf-function-argument-range-structure.md)结构的数目。|  
|`totalArgumentSize`|所有参数的总大小。 换言之，此值是自变量长度之和。|  
|`ranges`|`COR_PRF_FUNCTION_ARGUMENT_RANGE` 结构的数组，其中每个结构都表示一个函数参数块。|  
  
## <a name="remarks"></a>备注  
 函数可以包含多个参数。 这些参数可能不会连续存储在内存中。 在一个位置，您可能有一个包含三个自变量的块、另一个位置中的两个参数块，以及在不同位置中的一个自变量的最后一个块。 这些参数全部用于相同的函数;它们只是存储在不同的位置。  
  
 `COR_PRF_FUNCTION_ARGUMENT_INFO` 结构表示一个函数的所有自变量。 它使用数组引用函数参数的所有块。 因此，对于单个函数，有一个 `COR_PRF_FUNCTION_ARGUMENT_INFO` 结构，该结构引用多个 `COR_PRF_FUNCTION_ARGUMENT_RANGE` 结构，其中每个结构都指向一个或多个函数参数。  
  
 存储在寄存器中的参数会溢出到内存中以生成结构。  
  
## <a name="requirements"></a>需求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** Corprof.idl .idl  
  
 **库：** CorGuids.lib  
  
 **.NET Framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>另请参阅

- [分析结构](profiling-structures.md)
