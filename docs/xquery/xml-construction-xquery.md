---
title: XML 构造 (XQuery) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- white space [XQuery]
- computed constructor
- construct XML structures [XQuery]
- constructors [XQuery]
- prolog
- direct constructor [SQL Server]
- XML [SQL Server], construction
- XQuery, XML construction
ms.assetid: a6330b74-4e52-42a4-91ca-3f440b3223cf
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d5c63b6e2f128871740f816cf0772f44646e31f3
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024598"
---
# <a name="xml-construction-xquery"></a>XML 构造 (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  在 XQuery 中，你可以使用**直接**并**计算**构造函数来查询中构造 XML 结构。  
  
> [!NOTE]  
>  没有任何区别**直接**并**计算**构造函数。  
  
## <a name="using-direct-constructors"></a>使用直接构造函数  
 使用直接构造函数时，可以在构造 XML 时指定类似 XML 的语法。 下列示例说明了直接构造函数的 XML 构造。  
  
### <a name="constructing-elements"></a>构造元素  
 使用 XML 表示法时，可以构造元素。 下面的示例使用直接元素构造函数表达式，并创建\<ProductModel > 元素。 构造的元素有三个子元素。  
  
-   一个文本节点。  
  
-   两个元素节点，\<摘要 > 和\<功能 >。  
  
    -   \<摘要 > 元素有一个子文本节点的值为"Some description"。  
  
    -   \<功能 > 元素具有三个元素节点子级\<颜色 >，\<权重 >，和\<保证 >。 这些节点中，每个节点都有一个子文本节点，它们的值分别为 Red、25、2 years parts and labor。  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
<Features>  
  <Color>Red</Color>  
  <Weight>25</Weight>  
  <Warranty>2 years parts and labor</Warranty>  
</Features></ProductModel>')  
  
```  
  
 下面是生成的 XML：  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
  <Features>  
    <Color>Red</Color>  
    <Weight>25</Weight>  
    <Warranty>2 years parts and labor</Warranty>  
  </Features>  
</ProductModel>  
```  
  
 尽管从常量表达式构造元素（如本例所示）很有用，但是此 XQuery 语言功能的真正作用是构造能够从数据库动态提取数据的 XML。 可以使用大括号指定查询表达式。 在生成的 XML 中，表达式将由其值取代。 例如，下面的查询构造了一个 <`NewRoot`> 元素，该元素有一个子元素 <`e`>。 元素的值 <`e`> 通过指定在大括号 （"{...}"） 内的路径表达式计算。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
SELECT @x.query('<NewRoot><e> { /root } </e></NewRoot>');  
```  
  
 大括号充当上下文切换标记，并将查询从 XML 构造切换到查询计算。 在本例中，将对大括号中的 XQuery 路径表达式 `/root` 进行计算，并用结果替换该表达式。  
  
 下面是结果：  
  
```xml
<NewRoot>  
  <e>  
    <root>5</root>  
  </e>  
</NewRoot>  
```  
  
 下面的查询与上一个查询类似。 但是，大括号中的表达式指定**data （)** 函数来检索的原子值 <`root`> 元素并将其分配给构造的元素，<`e`>。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
                           <NewRoot>  
                             <e> { data(/root) } </e>  
                           </NewRoot>' ));  
SELECT @y;  
```  
  
 下面是结果：  
  
```xml
<NewRoot>  
  <e>5</e>  
</NewRoot>  
```  
  
 若要将大括号用作文本的一部分，而不是上下文切换标记，则可以将其转义为“}}”或“{{”，如下面的示例所示：  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('  
<NewRoot> Hello, I can use {{ and  }} as part of my text</NewRoot>'));  
SELECT @y;  
```  
  
 下面是结果：  
  
```xml
<NewRoot> Hello, I can use { and  } as part of my text</NewRoot>  
```  
  
 下面的查询是使用直接元素构造函数来构造元素的另一个示例。 此外，<`FirstLocation`> 元素的值是通过执行大括号中的表达式获取的。 该查询表达式返回 Production.ProductModel 表的 Instructions 列中的第一个生产车间的生产步骤。  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation>  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 下面是结果：  
  
```xml
<FirstLocation>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Insert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">  
      Attach <AWMI:tool>Trim Jig TJ-26</AWMI:tool> to the upper and lower right corners of the aluminum sheet.   
  </AWMI:step>  
   ...  
</FirstLocation>  
```  
  
#### <a name="element-content-in-xml-construction"></a>XML 构造中的元素内容  
 下面的示例说明了使用直接元素构造函数构造元素内容时表达式的行为。 在下面的示例中，直接元素构造函数指定了一个表达式。 对于此表达式，生成的 XML 中创建了一个文本节点。  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { for $i in /root[1]/step  
    return string($i)  
 }  
</result>');  
  
```  
  
 从表达式计算得到的原子值序列被添加到该文本节点，并在两个相邻的原子值之间添加一个空格，如结果所示。 构造的元素有一个子元素。 这是一个包含结果中所显示值的文本节点。  
  
```xml
<result>This is step 1 This is step 2 This is step 3</result>  
```  
  
 如果指定三个单独的表达式（而不是一个表达式）生成三个文本节点，则在生成的 XML 中，相邻的文本节点将通过串联合并为一个文本节点。  
  
```sql
declare @x xml;  
set @x='  
<root>  
  <step>This is step 1</step>  
  <step>This is step 2</step>  
  <step>This is step 3</step>  
</root>';  
select @x.query('  
<result>  
 { string(/root[1]/step[1]) }  
 { string(/root[1]/step[2]) }  
 { string(/root[1]/step[3]) }  
</result>');  
```  
  
 构造的元素节点有一个子元素节点。 这是一个包含结果中所显示值的文本节点。  
  
```xml
<result>This is step 1This is step 2This is step 3</result>  
```  
  
### <a name="constructing-attributes"></a>构造属性  
 使用直接元素构造函数来构造元素时，还可以使用类似 XML 的语法来指定元素的属性，如下面的示例所示：  
  
```sql
declare @x xml;  
set @x='';  
select @x.query('<ProductModel ProductModelID="111">;  
This is product model catalog description.  
<Summary>Some description</Summary>  
</ProductModel>')  
```  
  
 下面是生成的 XML：  
  
```xml
<ProductModel ProductModelID="111">  
  This is product model catalog description.  
  <Summary>Some description</Summary>  
</ProductModel>  
```  
  
 构造的元素 <`ProductModel`> 包含 ProductModelID 属性和下列子节点：  
  
-   文本节点 `This is product model catalog description.`  
  
-   元素节点 <`Summary`>。 此节点有一个子文本节点 `Some description`。  
  
 构造属性时，可以使用大括号中的表达式指定属性的值。 在本例中，表达式的结果返回为属性值。  
  
 在以下示例中， **data （)** 函数不是绝对必需的。 将表达式值分配到一个属性，因为**data （)** 隐式应用以检索指定的表达式的类型化的值。  
  
```sql
DECLARE @x xml;  
SET @x='<root>5</root>';  
DECLARE @y xml;  
SET @y = (SELECT @x.query('<NewRoot attr="{ data(/root) }" ></NewRoot>'));  
SELECT @y;  
```  
  
 下面是结果：  
  
```xml
<NewRoot attr="5" />  
```  
  
 下面是另一个示例，其中为 LocationID 和 SetupHrs 属性构造指定了表达式。 这些表达式将根据 Instruction 列中的 XML 进行计算。 表达式的类型化值将分配给这些属性。  
  
```sql
SELECT Instructions.query('  
    declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        <FirstLocation   
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7;  
```  
  
 下面是部分结果：  
  
```xml
<FirstLocation LocationID="10" SetupHours="0.5" >  
  <AWMI:step ...   
  </AWMI:step>  
  ...  
</FirstLocation>  
```  
  
#### <a name="implementation-limitations"></a>实现限制  
 限制如下：  
  
-   不支持多个属性表达式或混合（字符串和 XQuery 表达式）属性表达式。 例如，下面的查询中，您构造的 XML，其中 `Item` 是一个常量，值 `5` 是通过计算查询表达式获得的：  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
     由于混合了常量字符串和表达式 ({/x})，但不支持此类情况，因此下面的查询返回了一个错误：  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="Item {/x}"/>' )   
    ```  
  
     在这种情况下，您有以下几种选择：  
  
    -   通过串联两个原子值，组成属性值。 这些原子值被序列化为属性值，并且两个原子值之间有一个空格：  
  
        ```sql
        SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
        ```  
  
         下面是结果：  
  
        ```xml
        <a attr="Item 5" />  
        ```  
  
    -   使用[concat 函数](../xquery/functions-on-string-values-concat.md)地连接到生成的属性值的两个字符串参数：  
  
        ```sql
        SELECT @x.query( '<a attr="{concat(''Item'', /x[1])}"/>' )   
        ```  
  
         本例中，两个字符串值之间没有添加空格。 如果希望两个值之间有空格，必须显式提供空格。  
  
         下面是结果：  
  
        ```xml
        <a attr="Item5" />  
        ```  
  
-   不支持将多个表达式作为一个属性值。 例如，下面的查询将返回错误：  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    SELECT @x.query( '<a attr="{/x}{/x}"/>' )  
    ```  
  
-   不支持异类序列。 任何将异类序列指定为属性值的尝试都将返回一个错误，如下面的示例所示。 在本例中，由字符串“Item”和元素 <`x`> 组成的异类序列被指定为属性值：  
  
    ```sql
    DECLARE @x xml  
    SET @x ='<x>5</x>'  
    select @x.query( '<a attr="{''Item'', /x }" />')  
    ```  
  
     如果将应用**data （)** 函数，该查询有效，因为它检索的表达式，原子值`/x`，这与字符串串联。 下面是原子值的序列：  
  
    ```sql
    SELECT @x.query( '<a attr="{''Item'', data(/x)}"/>' )   
    ```  
  
     下面是结果：  
  
    ```xml
    <a attr="Item 5" />  
    ```  
  
-   属性节点顺序是在序列化期间而非静态类型检查期间执行的。 例如，以下查询的失败是因它尝试在非属性节点后添加一个属性造成的。  
  
    ```sql
    select convert(xml, '').query('  
    element x { attribute att { "pass" }, element y { "Element text" }, attribute att2 { "fail" } }  
    ')  
    go  
    ```  
  
     上述查询将返回以下错误：  
  
    ```  
    XML well-formedness check: Attribute cannot appear outside of element declaration. Rewrite your XQuery so it returns well-formed XML.  
    ```  
  
### <a name="adding-namespaces"></a>添加命名空间  
 使用直接构造函数构造 XML 时，可以使用命名空间前缀限定构造的元素和属性名称。 可以通过下列方法将前缀绑定到命名空间：  
  
-   使用命名空间声明属性。  
  
-   使用 WITH XMLNAMESPACES 子句。  
  
-   在 XQuery prolog 中。  
  
#### <a name="using-a-namespace-declaration-attribute-to-add-namespaces"></a>使用命名空间声明属性添加命名空间  
 下面的示例在元素 <`a`> 的构造中使用命名空间声明属性来声明默认的命名空间。 子元素 <`b`> 的构造撤消了父元素中声明的默认命名空间声明。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <a xmlns="a">  
    <b xmlns=""/>  
  </a>' )   
```  
  
 下面是结果：  
  
```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
 可以将前缀指定给命名空间。 前缀是在元素 <`a`> 的构造中指定的。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b/>  
  </x:a>' )  
```  
  
 下面是结果：  
  
```xml
<x:a xmlns:x="a">  
  <b />  
</x:a>  
```  
  
 您可以不声明 XML 构造中的默认命名空间，但是必须声明命名空间前缀。 由于必须声明元素 <`b`> 的构造中指定的前缀，下面的查询返回了一个错误。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
  <x:a xmlns:x="a">  
    <b xmlns:x=""/>  
  </x:a>' )  
```  
  
 新构造的命名空间可在查询中使用。 例如，下面的查询在构造元素 <`FirstLocation`> 时声明了一个命名空间，并在 LocationID 和 SetupHrs 属性值的表达式中指定了前缀。  
  
```sql
SELECT Instructions.query('  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 注意，用此方法创建新的命名空间前缀将覆盖此前缀以前存在的所有命名空间声明。 例如，查询 prolog 中的命名空间声明 `AWMI="https://someURI"` 被 <`FirstLocation`> 元素中的命名空间声明覆盖。  
  
```sql
SELECT Instructions.query('  
declare namespace AWMI="https://someURI";  
        <FirstLocation xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
         LocationID="{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
         SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
           { /AWMI:root/AWMI:Location[1]/AWMI:step }  
        </FirstLocation>   
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
#### <a name="using-a-prolog-to-add-namespaces"></a>使用 prolog 添加命名空间  
 下面的示例说明了如何将命名空间添加到构造的 XML 中。 查询 prolog 中已声明默认命名空间。  
  
```sql
declare @x xml  
set @x ='<x>5</x>'  
select @x.query( '  
           declare default element namespace "a";  
            <a><b xmlns=""/></a>' )  
```  
  
 注意，在元素 <`b`> 的构造中，已指定空字符串作为命名空间声明属性的值。 这将取消声明父级中所声明的默认命名空间。  
  

下面是结果：  

```xml
<a xmlns="a">  
  <b xmlns="" />  
</a>  
```  
  
### <a name="xml-construction-and-white-space-handling"></a>XML 构造和空格处理  
 XML 构造中的元素内容可以包含空格字符。 这些字符以下列方式进行处理：  
  
-   命名空间 Uri 中的空白字符被视为 XSD 类型**anyURI**。 下面是专门处理这些空格字符的方式：  
  
    -   修整开头和结尾处的所有空格字符。  
  
    -   将内部空格字符值折叠为一个空格。  
  
-   将属性内容中的换行符替换为空格。 所有其他空格字符保持不变。  
  
-   保留元素中的空格。  
  
 下面的示例说明了如何处理 XML 构造中的空格：  
  
```sql
-- line feed is repaced by space.  
declare @x xml  
set @x=''  
select @x.query('  
  
declare namespace myNS="   https://       
 abc/  
xyz  
  
";  
<test attr="    my   
test   attr   
value    " >  
  
<a>  
  
This     is  a  
  
test  
  
</a>  
</test>  
') as XML_Result  
  
```  
  
 下面是结果：  
  
```xml
-- result  
<test attr="<test attr="    my test   attr  value    "><a>  
  
This     is  a  
  
test  
  
</a></test>  
"><a>  
  
This     is  a  
  
test  
  
</a></test>  
```  
  
### <a name="other-direct-xml-constructors"></a>其他直接 XML 构造函数  
 用于处理指令和 XML 注释的构造函数使用的语法与相应的 XML 构造使用的语法相同。 同时还支持文本节点的计算构造函数，但主要在 XML DML 中使用，用于构造文本节点。  
  
 **请注意**使用显式文本节点构造函数的示例，请参阅中的特定示例[插入&#40;XML DML&#41;](../t-sql/xml/insert-xml-dml.md)。  
  
 在下面的查询中，构造的 XML 包括一个元素、两个属性、一个注释和一个处理指令。 注意，由于正在构造序列，因此要在 <`FirstLocation`> 前使用逗号。  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   <?myProcessingInstr abc="value" ?>,   
   <FirstLocation   
        WorkCtrID = "{ (/AWMI:root/AWMI:Location[1]/@LocationID)[1] }"  
        SetupHrs = "{ (/AWMI:root/AWMI:Location[1]/@SetupHours)[1] }" >  
       <!-- some comment -->  
       <?myPI some processing instructions ?>  
       { (/AWMI:root/AWMI:Location[1]/AWMI:step) }  
    </FirstLocation>   
') as Result   
FROM Production.ProductModel  
where ProductModelID=7;  
  
```  
  
 下面是部分结果：  
  
```xml
<?myProcessingInstr abc="value" ?>  
<FirstLocation WorkCtrID="10" SetupHrs="0.5">  
  <!-- some comment -->  
  <?myPI some processing instructions ?>  
  <AWMI:step xmlns:AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions">I  
  nsert <AWMI:material>aluminum sheet MS-2341</AWMI:material> into the <AWMI:tool>T-85A framing tool</AWMI:tool>.   
  </AWMI:step>  
    ...  
</FirstLocation>  
  
```  
  
## <a name="using-computed-constructors"></a>使用计算构造函数  
 . 本例中，指定了关键字来标识要构造的节点的类型。 仅支持下列关键字：  
  
-   element  
  
-   属性  
  
-   text  
  
 对于元素节点和属性节点，这些关键字后面跟有节点名称和生成该节点内容的表达式（括在大括号内）。 下面的示例中，构造了此 XML：  
  
```xml
<root>  
  <ProductModel PID="5">Some text <summary>Some Summary</summary></ProductModel>  
</root>  
```  
  
 下面是使用计算构造函数生成 XML 的查询：  
  
```sql
declare @x xml  
set @x=''  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { 5 },  
text{"Some text "},  
    element summary { "Some Summary" }  
 }  
               } ')  
  
```  
  
 生成节点内容的表达式可以指定一个查询表达式。  
  
```sql
declare @x xml  
set @x='<a attr="5"><b>some summary</b></a>'  
select @x.query('element root   
               {   
                  element ProductModel  
     {  
attribute PID { /a/@attr },  
text{"Some text "},  
    element summary { /a/b }  
 }  
               } ')  
```  
  
 注意，使用 XQuery 规范中定义的计算元素和属性构造函数可以计算节点名称。 在 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 中使用直接构造函数时，元素和属性等节点名称必须指定为常量文字。 这样，元素和属性的直接构造函数和计算构造函数之间才不会有差异。  
  
 在以下示例中，构造节点的内容均来自的 Instructions 列中存储的 XML 生产说明**xml** ProductModel 表中的数据类型。  
  
```sql
SELECT Instructions.query('  
  declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   element FirstLocation   
     {  
        attribute LocationID { (/AWMI:root/AWMI:Location[1]/@LocationID)[1] },  
        element   AllTheSteps { /AWMI:root/AWMI:Location[1]/AWMI:step }  
     }  
') as Result   
FROM  Production.ProductModel  
where ProductModelID=7  
```  
  
 下面是部分结果：  
  
```xml
<FirstLocation LocationID="10">  
  <AllTheSteps>  
    <AWMI:step> ... </AWMI:step>  
    <AWMI:step> ... </AWMI:step>  
    ...  
  </AllTheSteps>  
</FirstLocation>    
```  
  
## <a name="additional-implementation-limitations"></a>其他实现限制  
 计算属性构造函数不能用于声明新的命名空间。 此外，[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 不支持下列计算构造函数：  
  
-   计算文档节点构造函数  
  
-   计算处理指令构造函数  
  
-   计算注释构造函数  
  
## <a name="see-also"></a>请参阅  
 [XQuery 表达式](../xquery/xquery-expressions.md)  
  
  
