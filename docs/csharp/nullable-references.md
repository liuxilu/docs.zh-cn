---
title: 可为空引用类型
description: 本文概述了在 C# 8 中添加的可为空引用类型。 你将了解该功能如何为新项目和现有项目提供针对空引用异常的安全性。
ms.date: 02/19/2019
ms.openlocfilehash: 1eb4ccb5ec4397cb81aab37c13a31c41533238e9
ms.sourcegitcommit: 41c0637e894fbcd0713d46d6ef1866f08dc321a2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/01/2019
ms.locfileid: "57411542"
---
# <a name="nullable-reference-types"></a><span data-ttu-id="38c07-104">可为空引用类型</span><span class="sxs-lookup"><span data-stu-id="38c07-104">Nullable reference types</span></span>

<span data-ttu-id="38c07-105">C#8.0 引入了“可为空引用类型”和“不可为空引用类型”，使你能够对引用类型变量的属性作出重要声明：</span><span class="sxs-lookup"><span data-stu-id="38c07-105">C# 8.0 introduces **nullable reference types** and **non-nullable reference types** that enable you to make important statements about the properties for reference type variables:</span></span>

- <span data-ttu-id="38c07-106">引用不应为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-106">**A reference is not supposed to be null**.</span></span> <span data-ttu-id="38c07-107">当变量不应为 null 时，编译器会强制执行规则，以确保在不首先检查它们是否为 null 的情况下取消引用这些变量是安全的：</span><span class="sxs-lookup"><span data-stu-id="38c07-107">When variables aren't supposed to be null, the compiler enforces rules that ensure it is safe to dereference these variables without first checking that it isn't null:</span></span>
  - <span data-ttu-id="38c07-108">必须将变量初始化为非 null 值。</span><span class="sxs-lookup"><span data-stu-id="38c07-108">The variable must be initialized to a non-null value.</span></span>
  - <span data-ttu-id="38c07-109">变量永远不能赋值为 `null`。</span><span class="sxs-lookup"><span data-stu-id="38c07-109">The variable can never be assigned the value `null`.</span></span>
- <span data-ttu-id="38c07-110">引用可为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-110">**A reference may be null**.</span></span> <span data-ttu-id="38c07-111">当变量可以为 null 时，编译器会强制执行不同的规则以确保你已正确检查空引用：</span><span class="sxs-lookup"><span data-stu-id="38c07-111">When variables may be null, the compiler enforces different rules to ensure that you've correctly checked for a null reference:</span></span>
  - <span data-ttu-id="38c07-112">只有当编译器可以保证该值不为 null 时，才可以取消引用该变量。</span><span class="sxs-lookup"><span data-stu-id="38c07-112">The variable may only be dereferenced when the compiler can guarantee that the value isn't null.</span></span>
  - <span data-ttu-id="38c07-113">这些变量可以使用默认的 `null` 值进行初始化，也可以在其他代码中赋值为 `null`。</span><span class="sxs-lookup"><span data-stu-id="38c07-113">These variables may be initialized with the default `null` value and may be assigned the value `null` in other code.</span></span>

<span data-ttu-id="38c07-114">在 C# 的早期版本中，无法从变量声明中确定设计意图，与处理引用变量相比，这个新功能提供了显著的好处。</span><span class="sxs-lookup"><span data-stu-id="38c07-114">This new feature provides significant benefits over the handling of reference variables in earlier versions of C# where the design intent couldn't be determined from the variable declaration.</span></span> <span data-ttu-id="38c07-115">编译器不提供针对引用类型的空引用异常的安全性：</span><span class="sxs-lookup"><span data-stu-id="38c07-115">The compiler didn't provide safety against null reference exceptions for reference types:</span></span>

- <span data-ttu-id="38c07-116">引用可为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-116">**A reference can be null**.</span></span> <span data-ttu-id="38c07-117">将引用类型初始化为 null 或稍后将其指定为 null 时，编译器不会发出警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-117">No warnings are issued when a reference type is initialized to null, or later assigned to null.</span></span>
- <span data-ttu-id="38c07-118">假定引用不为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-118">**A reference is assumed to be not null**.</span></span> <span data-ttu-id="38c07-119">当引用类型被取消引用时，编译器不会发出任何警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-119">The compiler doesn't issue any warnings when reference types are dereferenced.</span></span> <span data-ttu-id="38c07-120">（使用可为空引用，只要取消引用可能为 null 的变量，编译器就会发出警告）。</span><span class="sxs-lookup"><span data-stu-id="38c07-120">(With nullable references,  the compiler issues warnings whenever you dereference a variable that may be null).</span></span>

<span data-ttu-id="38c07-121">通过添加可为空引用类型，你可以更清楚地声明你的意图。</span><span class="sxs-lookup"><span data-stu-id="38c07-121">With the addition of nullable reference types, you can declare your intent more clearly.</span></span> <span data-ttu-id="38c07-122">`null` 值是表示变量不引用值的正确方法。</span><span class="sxs-lookup"><span data-stu-id="38c07-122">The `null` value is the correct way to represent that a variable doesn't refer to a value.</span></span> <span data-ttu-id="38c07-123">请勿使用此功能从代码中删除所有 `null` 值。</span><span class="sxs-lookup"><span data-stu-id="38c07-123">Don't use this feature to remove all `null` values from your code.</span></span> <span data-ttu-id="38c07-124">相反，应该向编译器和其他读取代码的开发人员声明你的意图。</span><span class="sxs-lookup"><span data-stu-id="38c07-124">Rather, you should declare your intent to the compiler and other developers that read your code.</span></span> <span data-ttu-id="38c07-125">通过声明意图，编译器会在你编写与该意图不一致的代码时通知你。</span><span class="sxs-lookup"><span data-stu-id="38c07-125">By declaring your intent, the compiler informs you when you write code that is inconsistent with that intent.</span></span>

<span data-ttu-id="38c07-126">使用与[可为空值类型](programming-guide/nullable-types/index.md)相同的语法记录**可为空引用类型**：将 `?` 附加到变量的类型。</span><span class="sxs-lookup"><span data-stu-id="38c07-126">A **nullable reference type** is noted using the same syntax as [nullable value types](programming-guide/nullable-types/index.md): a `?` is appended to the type of the variable.</span></span> <span data-ttu-id="38c07-127">例如，以下变量声明表示可为空的字符串变量 `name`：</span><span class="sxs-lookup"><span data-stu-id="38c07-127">For example, the following variable declaration represents a nullable string variable, `name`:</span></span>

```csharp
string? name;
```

<span data-ttu-id="38c07-128">未将 `?` 附加到类型名称的任何变量都是“不可为空引用类型”。</span><span class="sxs-lookup"><span data-stu-id="38c07-128">Any variable where the `?` is not appended to the type name is a **non-nullable reference type**.</span></span> <span data-ttu-id="38c07-129">这包括启用此功能时现有代码中的所有引用类型变量。</span><span class="sxs-lookup"><span data-stu-id="38c07-129">That includes all reference type variables in existing code when you have enabled this feature.</span></span>

<span data-ttu-id="38c07-130">编译器使用静态分析来确定可为空引用是否为非 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-130">The compiler uses static analysis to determine if a nullable reference is known to be non-null.</span></span> <span data-ttu-id="38c07-131">如果你在一个可为空引用可能是 null 时对其取消引用，编译器将向你发出警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-131">The compiler warns you if you dereference a nullable reference when it may be null.</span></span> <span data-ttu-id="38c07-132">通过在变量名后面使用 null 包容运算符 (`!`) 即可覆盖此行为。</span><span class="sxs-lookup"><span data-stu-id="38c07-132">You can override this behavior by using the **null-forgiving operator** (`!`) following a variable name.</span></span> <span data-ttu-id="38c07-133">例如，若知道 `name` 变量不为 null 但编译器仍发出警告，则可以编写以下代码来覆盖编译器的分析：</span><span class="sxs-lookup"><span data-stu-id="38c07-133">For example, if you know the `name` variable isn't null but the compiler issues a warning, you can write the following code to override the compiler's analysis:</span></span>

```csharp
name!.Length;
```

<span data-ttu-id="38c07-134">你可以在 GitHub 上的[可为空引用类型草稿](https://github.com/dotnet/csharplang/blob/master/proposals/csharp-8.0/nullable-reference-types-specification.md#the-null-forgiving-operator)规范提案中阅读有关此运算符的详细信息。</span><span class="sxs-lookup"><span data-stu-id="38c07-134">You can read details about this operator in the [draft nullable reference types](https://github.com/dotnet/csharplang/blob/master/proposals/csharp-8.0/nullable-reference-types-specification.md#the-null-forgiving-operator) specification proposal on GitHub.</span></span>

## <a name="nullability-of-types"></a><span data-ttu-id="38c07-135">类型为 Null 性</span><span class="sxs-lookup"><span data-stu-id="38c07-135">Nullability of types</span></span>

<span data-ttu-id="38c07-136">任何引用类型都可以具有四个“为 Null 性”中的一个，它描述了何时生成警告：</span><span class="sxs-lookup"><span data-stu-id="38c07-136">Any reference type can have one of four *nullabilities*, which describes when warnings are generated:</span></span>

- <span data-ttu-id="38c07-137">*不可为空*：无法将 null 分配给此类型的变量。</span><span class="sxs-lookup"><span data-stu-id="38c07-137">*Nonnullable*: Null can't be assigned to variables of this type.</span></span> <span data-ttu-id="38c07-138">在取消引用之前，无需对此类型的变量进行 null 检查。</span><span class="sxs-lookup"><span data-stu-id="38c07-138">Variables of this type don't need to be null-checked before dereferencing.</span></span>
- <span data-ttu-id="38c07-139">*可为空*：可将 null 分配给此类型的变量。</span><span class="sxs-lookup"><span data-stu-id="38c07-139">*Nullable*: Null can be assigned to variables of this type.</span></span> <span data-ttu-id="38c07-140">在不首先检查 `null` 的情况下取消引用此类型的变量时发出警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-140">Dereferencing variables of this type without first checking for `null` causes a warning.</span></span>
- <span data-ttu-id="38c07-141">*无视*：这是 C# 8 之前版本的状态。</span><span class="sxs-lookup"><span data-stu-id="38c07-141">*Oblivious*: This is the pre-C# 8 state.</span></span> <span data-ttu-id="38c07-142">可以取消引用或分配此类型的变量而不发出警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-142">Variables of this type can be dereferenced or assigned without warnings.</span></span>
- <span data-ttu-id="38c07-143">*未知*：这通常针对类型参数，约束不告知编译器类型是否必须是“可为空”或“不可为空”。</span><span class="sxs-lookup"><span data-stu-id="38c07-143">*Unknown*: This is generally for type parameters where constraints don't tell the compiler that the type must be *nullable* or *nonnullable*.</span></span>

<span data-ttu-id="38c07-144">变量声明中类型的为 Null 性由声明变量的“可为空上下文”控制。</span><span class="sxs-lookup"><span data-stu-id="38c07-144">The nullability of a type in a variable declaration is controlled by the *nullable context* in which the variable is declared.</span></span>

## <a name="nullable-contexts"></a><span data-ttu-id="38c07-145">可为空上下文</span><span class="sxs-lookup"><span data-stu-id="38c07-145">Nullable contexts</span></span>

<span data-ttu-id="38c07-146">可为空上下文可以对编译器如何解释引用类型变量进行精细控制。</span><span class="sxs-lookup"><span data-stu-id="38c07-146">Nullable contexts enable fine-grained control for how the compiler interprets reference type variables.</span></span> <span data-ttu-id="38c07-147">任何给定源代码行的“可为空注释上下文”为 `enabled` 或 `disabled`。</span><span class="sxs-lookup"><span data-stu-id="38c07-147">The **nullable annotation context** of any given source line is `enabled` or `disabled`.</span></span> <span data-ttu-id="38c07-148">你可以将 C# 8 之前的编译器视为在 `disabled` 可为空上下文中编译所有代码：任何引用类型都可以为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-148">You can think of the pre-C# 8 compiler as compiling all your code in a `disabled` nullable context: Any reference type may be null.</span></span> <span data-ttu-id="38c07-149">“可为空警告上下文”可以设置为`enabled`、`disabled` 或 `safeonly`。</span><span class="sxs-lookup"><span data-stu-id="38c07-149">The **nullable warnings context** may be set to `enabled`, `disabled`, or `safeonly`.</span></span> <span data-ttu-id="38c07-150">可为空警告上下文指定编译器使用其流分析生成的警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-150">The nullable warnings context specifies the warnings generated by the compiler using its flow analysis.</span></span>

<span data-ttu-id="38c07-151">可以使用 `csproj` 文件中的 `NullableContextOptions` 元素为项目设置可为空注释上下文和可为空警告上下文。</span><span class="sxs-lookup"><span data-stu-id="38c07-151">The nullable annotation context and nullable warning context can be set for a project using the `NullableContextOptions` element in your `csproj` file.</span></span> <span data-ttu-id="38c07-152">此元素配置编译器如何解释类型的为 Null 性以及生成哪些警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-152">This element configures how the compiler interprets the nullability of types and what warnings are generated.</span></span> <span data-ttu-id="38c07-153">有效设置如下：</span><span class="sxs-lookup"><span data-stu-id="38c07-153">Valid settings are:</span></span>

- <span data-ttu-id="38c07-154">`enable`：“启用”可为空注释上下文。</span><span class="sxs-lookup"><span data-stu-id="38c07-154">`enable`: The nullable annotation context is **enabled**.</span></span> <span data-ttu-id="38c07-155">“启用”可为空警告上下文。</span><span class="sxs-lookup"><span data-stu-id="38c07-155">The nullable warning context is **enabled**.</span></span>
  - <span data-ttu-id="38c07-156">引用类型的变量，例如 `string` 是“不可为空”。</span><span class="sxs-lookup"><span data-stu-id="38c07-156">Variables of a reference type, `string` for example, are non-nullable.</span></span>  <span data-ttu-id="38c07-157">启用所有为 Null 性警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-157">All nullability warnings are enabled.</span></span>
- <span data-ttu-id="38c07-158">`disable`：“禁用”可为空注释上下文。</span><span class="sxs-lookup"><span data-stu-id="38c07-158">`disable`: The nullable annotation context is **disabled**.</span></span> <span data-ttu-id="38c07-159">“禁用”可为空警告上下文。</span><span class="sxs-lookup"><span data-stu-id="38c07-159">The nullable warning context is **disabled**.</span></span>
  - <span data-ttu-id="38c07-160">引用类型的变量是“无视”，就像早期版本的 C# 一样。</span><span class="sxs-lookup"><span data-stu-id="38c07-160">Variables of a reference type are oblivious, just like earlier versions of C#.</span></span> <span data-ttu-id="38c07-161">禁用所有为 Null 性警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-161">All nullability warnings are disabled.</span></span>
- <span data-ttu-id="38c07-162">`safeonly`：“启用”可为空注释上下文。</span><span class="sxs-lookup"><span data-stu-id="38c07-162">`safeonly`: The nullable annotation context is **enabled**.</span></span> <span data-ttu-id="38c07-163">可为空警告上下文为 safeonly。</span><span class="sxs-lookup"><span data-stu-id="38c07-163">The nullable warning context is **safeonly**.</span></span>
  - <span data-ttu-id="38c07-164">引用类型的变量“不可为空”。</span><span class="sxs-lookup"><span data-stu-id="38c07-164">Variables of a reference type are nonnullable.</span></span> <span data-ttu-id="38c07-165">启用所有安全性为 Null 性警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-165">All safety nullability warnings are enabled.</span></span>
- <span data-ttu-id="38c07-166">`warnings`：“禁用”可为空注释上下文。</span><span class="sxs-lookup"><span data-stu-id="38c07-166">`warnings`: The nullable annotation context is **disabled**.</span></span> <span data-ttu-id="38c07-167">“启用”可为空警告上下文。</span><span class="sxs-lookup"><span data-stu-id="38c07-167">The nullable warning context is **enabled**.</span></span>
  - <span data-ttu-id="38c07-168">引用类型的变量是“无视”。</span><span class="sxs-lookup"><span data-stu-id="38c07-168">Variables of a reference type are oblivious.</span></span> <span data-ttu-id="38c07-169">启用所有为 Null 性警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-169">All nullability warnings are enabled.</span></span>
- <span data-ttu-id="38c07-170">`safeonlywarnings`：“禁用”可为空注释上下文。</span><span class="sxs-lookup"><span data-stu-id="38c07-170">`safeonlywarnings`: The nullable annotation context is **disabled**.</span></span> <span data-ttu-id="38c07-171">可为空警告上下文为 safeonly。</span><span class="sxs-lookup"><span data-stu-id="38c07-171">The nullable warning context is **safeonly**.</span></span>
  - <span data-ttu-id="38c07-172">引用类型的变量是“无视”。</span><span class="sxs-lookup"><span data-stu-id="38c07-172">Variables of a reference type are oblivious.</span></span> <span data-ttu-id="38c07-173">启用所有安全性为 Null 性警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-173">All safety nullability warnings are enabled.</span></span>

<span data-ttu-id="38c07-174">你还可以使用指令在项目的任何位置设置这些相同的上下文：</span><span class="sxs-lookup"><span data-stu-id="38c07-174">You can also use directives to set these same contexts anywhere in your project:</span></span>

- <span data-ttu-id="38c07-175">`#nullable enable`：将可为空注释上下文和可为空警告上下文设置为“已启用”。</span><span class="sxs-lookup"><span data-stu-id="38c07-175">`#nullable enable`: Sets the nullable annotation context and nullable warning context to **enabled**.</span></span>
- <span data-ttu-id="38c07-176">`#nullable disable`：将可为空注释上下文和可为空警告上下文设置为“已禁用”。</span><span class="sxs-lookup"><span data-stu-id="38c07-176">`#nullable disable`: Sets the nullable annotation context and nullable warning context to **disabled**.</span></span>
- <span data-ttu-id="38c07-177">`#nullable safeonly`：将可为空注释上下文设置为“已启用”，并将警告上下文设置为“safeonly”。</span><span class="sxs-lookup"><span data-stu-id="38c07-177">`#nullable safeonly`: Set the nullable annotation context to **enabled**, and the warning context to **safeonly**.</span></span>
- <span data-ttu-id="38c07-178">`#nullable restore`：将可为空注释上下文和可为空警告上下文还原到项目设置。</span><span class="sxs-lookup"><span data-stu-id="38c07-178">`#nullable restore`: Restores the nullable annotation context and nullable warning context to the project settings.</span></span>
- <span data-ttu-id="38c07-179">`#pragma warning disable nullable`：将可为空警告上下文设置为“已禁用”。</span><span class="sxs-lookup"><span data-stu-id="38c07-179">`#pragma warning disable nullable`: Set the nullable warning context to **disabled**.</span></span>
- <span data-ttu-id="38c07-180">`#pragma warning enable nullable`：将可为空警告上下文设置为“已启用”。</span><span class="sxs-lookup"><span data-stu-id="38c07-180">`#pragma warning enable nullable`: Set the nullable warning context to **enabled**.</span></span>
- <span data-ttu-id="38c07-181">`#pragma warning restore nullable`：将可为空警告上下文还原到项目设置。</span><span class="sxs-lookup"><span data-stu-id="38c07-181">`#pragma warning restore nullable`: Restores the nullable warning context to the project settings.</span></span>
- <span data-ttu-id="38c07-182">`#pragma warning safeonly nullable`：将可为空警告上下文设置为“safeonly”。</span><span class="sxs-lookup"><span data-stu-id="38c07-182">`#pragma warning safeonly nullable`: Sets the nullable warning context to **safeonly**.</span></span>

<span data-ttu-id="38c07-183">默认的可为空注释和警告上下文为 `disabled`。</span><span class="sxs-lookup"><span data-stu-id="38c07-183">The default nullable annotation and warning contexts are `disabled`.</span></span> <span data-ttu-id="38c07-184">该决定意味着无需更改现有代码即可进行编译，并且不会生成任何新警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-184">That decision means that your existing code compiles without changes and without generating any new warnings.</span></span>

<span data-ttu-id="38c07-185">`enabled` 和 `safeonly` 可为空警告上下文之间的差异在于警告是在可为空引用分配给不可为空引用时发出的。</span><span class="sxs-lookup"><span data-stu-id="38c07-185">The differences between the `enabled` and `safeonly` nullable warning contexts are warnings for assigning a nullable reference to a non-nullable reference.</span></span> <span data-ttu-id="38c07-186">以下分配在 `enabled` 警告上下文中生成警告，但不在 `safeonly` 警告上下文中生成警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-186">The following assignment generates a warning in an `enabled` warning context, but not a `safeonly` warning context.</span></span> <span data-ttu-id="38c07-187">但是，第二行（取消引用 `s`）将在 `safeonly` 上下文中生成警告：</span><span class="sxs-lookup"><span data-stu-id="38c07-187">However, the second line, where `s` is dereferenced, generates a warning in a `safeonly` context:</span></span>

```csharp
string s = null; // warning when nullable warning context is enabled.
var txt = s.ToString(); // warning when nullable warnings context is safeonly, or enabled.
```

### <a name="nullable-annotation-context"></a><span data-ttu-id="38c07-188">可为空注释上下文</span><span class="sxs-lookup"><span data-stu-id="38c07-188">Nullable annotation context</span></span>

<span data-ttu-id="38c07-189">编译器在已禁用的可为空注释上下文中使用以下规则：</span><span class="sxs-lookup"><span data-stu-id="38c07-189">The compiler uses the following rules in a disabled nullable annotation context:</span></span>

- <span data-ttu-id="38c07-190">不能在已禁用的上下文中声明可为空引用。</span><span class="sxs-lookup"><span data-stu-id="38c07-190">You can't declare nullable references in a disabled context.</span></span>
- <span data-ttu-id="38c07-191">可以将所有引用变量分配为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-191">All reference variables may be assigned to null.</span></span>
- <span data-ttu-id="38c07-192">取消引用引用类型的变量时不会生成警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-192">No warnings are generated when a variable of a reference type is dereferenced.</span></span>
- <span data-ttu-id="38c07-193">可能不会在禁用的上下文中使用 null 包容运算符。</span><span class="sxs-lookup"><span data-stu-id="38c07-193">The null-forgiving operator may not be used in a disabled context.</span></span>

<span data-ttu-id="38c07-194">该行为与以前版本的 C# 相同。</span><span class="sxs-lookup"><span data-stu-id="38c07-194">The behavior is the same as previous versions of C#.</span></span>

<span data-ttu-id="38c07-195">编译器在已启用的可为空注释上下文中使用以下规则：</span><span class="sxs-lookup"><span data-stu-id="38c07-195">The compiler uses the following rules in an enabled nullable annotation context:</span></span>

- <span data-ttu-id="38c07-196">引用类型的任何变量都是“不可为空引用”。</span><span class="sxs-lookup"><span data-stu-id="38c07-196">Any variable of a reference type is a **non-nullable reference**.</span></span>
- <span data-ttu-id="38c07-197">任何不可为空引用都可以安全地取消引用。</span><span class="sxs-lookup"><span data-stu-id="38c07-197">Any non-nullable reference may be dereferenced safely.</span></span>
- <span data-ttu-id="38c07-198">任何可为空引用类型（在变量声明中的类型之后由 `?` 标记）可为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-198">Any nullable reference type (noted by `?` after the type in the variable declaration) may be null.</span></span> <span data-ttu-id="38c07-199">静态分析确定在取消引用该值时是否已知该值不为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-199">Static analysis determines if the value is known to be non-null when it is dereferenced.</span></span> <span data-ttu-id="38c07-200">否则，编译器会发出警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-200">If not, the compiler warns you.</span></span>
- <span data-ttu-id="38c07-201">你可以使用 null 包容运算符声明可为空引用不为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-201">You can use the null-forgiving operator to declare that a nullable reference isn't null.</span></span>

<span data-ttu-id="38c07-202">在已启用的可为空注释上下文中，附加到引用类型的 `?` 字符声明“可为空引用类型”。</span><span class="sxs-lookup"><span data-stu-id="38c07-202">In an enabled nullable annotation context, the `?` character appended to a reference type declares a **nullable reference type**.</span></span> <span data-ttu-id="38c07-203">可将 null 包容运算符 (`!`) 附加到表达式以声明表达式不为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-203">The **null forgiveness operator** (`!`) may be appended to an expression to declare that the expression isn't null.</span></span>

## <a name="nullable-warning-context"></a><span data-ttu-id="38c07-204">可为空警告上下文</span><span class="sxs-lookup"><span data-stu-id="38c07-204">Nullable warning context</span></span>

<span data-ttu-id="38c07-205">可为空警告上下文与可为空注释上下文不同。</span><span class="sxs-lookup"><span data-stu-id="38c07-205">The nullable warning context is distinct from the nullable annotation context.</span></span> <span data-ttu-id="38c07-206">即使禁用新注释，也可以启用警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-206">Warnings can be enabled even when the new annotations are disabled.</span></span> <span data-ttu-id="38c07-207">编译器使用静态流分析来确定任何引用的“null 状态”。</span><span class="sxs-lookup"><span data-stu-id="38c07-207">The compiler uses static flow analysis to determine the **null state** of any reference.</span></span> <span data-ttu-id="38c07-208">当“可为空警告上下文”未被“禁用”时，null 状态为“非 null”或“可能为 null”。</span><span class="sxs-lookup"><span data-stu-id="38c07-208">The null state is either **not null** or **maybe null** when the *nullable warning context* isn't **disabled**.</span></span> <span data-ttu-id="38c07-209">如果在编译器确定引用“可能为 null”时取消引用该引用，编译器会向你发出警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-209">If you dereference a reference when the compiler has determined it's **maybe null**, the compiler warns you.</span></span> <span data-ttu-id="38c07-210">除非编译器可以确定以下两个条件之一，否则引用的状态为“可能为 null”：</span><span class="sxs-lookup"><span data-stu-id="38c07-210">The state of a reference is **maybe null** unless the compiler can determine one of two conditions:</span></span>

1. <span data-ttu-id="38c07-211">该变量已明确分配给非 null 值。</span><span class="sxs-lookup"><span data-stu-id="38c07-211">The variable has been definitely assigned to a non-null value.</span></span>
1. <span data-ttu-id="38c07-212">在取消引用之前，已检查变量或表达式是否为 null。</span><span class="sxs-lookup"><span data-stu-id="38c07-212">The variable or expression has been checked against null before de-referencing it.</span></span>

<span data-ttu-id="38c07-213">当可为空警告上下文为 `enabled` 或 `safeonly` 时，只要取消引用“可能为 null”状态的变量或表达式，编译器就会生成警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-213">The compiler generates warnings whenever you dereference a variable or expression in a **maybe null** state when the nullable warning context is `enabled` or `safeonly`.</span></span> <span data-ttu-id="38c07-214">此外，当可为空注释上下文为 `enabled` 且将“可能为 null”变量或表达式分配给不可为空引用类型时，将生成警告。</span><span class="sxs-lookup"><span data-stu-id="38c07-214">Furthermore, warnings are generated when a **maybe null** variable or expression is assigned to a nonnullable reference type when the nullable annotation context is `enabled`.</span></span>

## <a name="learn-more"></a><span data-ttu-id="38c07-215">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="38c07-215">Learn more</span></span>

- [<span data-ttu-id="38c07-216">可为空引用规范草案</span><span class="sxs-lookup"><span data-stu-id="38c07-216">Draft Nullable reference specification</span></span>](https://github.com/dotnet/csharplang/blob/master/proposals/csharp-8.0/nullable-reference-types-specification.md)
- [<span data-ttu-id="38c07-217">可为空引用教程简介</span><span class="sxs-lookup"><span data-stu-id="38c07-217">Intro to nullable references tutorial</span></span>](tutorials/nullable-reference-types.md)
- [<span data-ttu-id="38c07-218">将现有代码库迁移到可为空引用</span><span class="sxs-lookup"><span data-stu-id="38c07-218">Migrate an existing codebase to nullable references</span></span>](tutorials/upgrade-to-nullable-references.md)