---
title: 图表故障排除（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 3a327ffa-3b69-40d6-8015-cc01cfae9161
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 10774fbba43f2aea9b2e3565169ed9a856c86ae9
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288225"
---
# <a name="troubleshoot-charts-report-builder-and-ssrs"></a>图表故障排除（报表生成器和 SSRS）
  对以下问题的解答可能在您使用图表时对您有所帮助。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="why-does-my-chart-count-not-sum-the-values-on-the-value-axis"></a>为什么我的图表对值轴上的值进行计数，而不是求和？  
 大多数图表类型都要求数值放置在通常作为 y 轴的值轴上，以便能够正确地绘制图表。 如果值字段的数据类型是 `String`，则图表将无法显示数值，即使这些字段中包含数字也是如此。 相反，该图表将显示包含该字段中值的行的总行数。 若要避免出现此情况，请确保用于值序列的字段是数字数据类型的，而不是包含格式化数字的字符串。  
  
## <a name="see-also"></a>请参阅  
 [图表（报表生成器和 SSRS）](charts-report-builder-and-ssrs.md)  
  
  
