---
title: Requery 方法 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 433f5d279e638e3ccdf7ba3a7bb2590f80b04a6b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706915"
---
# <a name="requery-method"></a>Requery 方法
更新中的数据[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)通过重新执行的查询该对象所基于的对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>Parameters  
 *选项*  
 可选。 包含一个位掩码[ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md)并[CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md)值会影响此操作。  
  
> [!NOTE]
>  如果*选项*设置为**adAsyncExecute**，将以异步方式执行此操作和一个[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)它结束时，将发出事件。 **ExecuteOpenEnum**的值**adExecuteNoRecords**或**adExecuteStream**不能与**再次查询**。  
  
## <a name="remarks"></a>备注  
 使用**Requery**方法来刷新的全部内容**记录集**重新颁发原始命令和检索数据的第二次通过数据源的对象。 调用此方法相当于调用[关闭](../../../ado/reference/ado-api/close-method-ado.md)并[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)连续的方法。 如果正在编辑当前记录或添加新记录时，出现错误。  
  
 虽然**记录集**对象已打开，定义游标的特性的属性 ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md)， [LockType](../../../ado/reference/ado-api/locktype-property-ado.md)， [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md)依次类推) 是只读的。 因此，**再次查询**方法仅刷新当前光标。 若要更改任何游标属性并查看结果，必须使用[关闭](../../../ado/reference/ado-api/close-method-ado.md)方法，以便属性再次变为读/写。 然后可以更改该属性设置并调用[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法以重新打开游标。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [执行、 再次查询和清除方法示例 (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [执行、 再次查询和清除方法示例 (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [执行、 再次查询和清除方法示例 （VC + +）](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [CommandText 属性 (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
