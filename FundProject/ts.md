​	[ts学习](https://juejin.im/post/5ee00fca51882536846781ee)

1. ts枚举的反向映射只支持数字枚举，字符串枚举不支持  [**链接**](https://juejin.im/post/5edd8ad8f265da76fc45362c#heading-8)

2. 字面量类型可严格控制输入的value

   ```typescript
   type CardinalDirection = 'North' | 'East' | 'South' | 'West';
   function move(distance: number, direction: CardinalDirection) {
     // ...
   }
   move(1, 'North'); // ok
   move(1, 'Nurth'); // Error
   ```

   

3. Omit

* 作用：基于**已经声明**的类型进行**属性剔除**获得**新类型**

* 语法

  ```typescript
  type User = {
  
  id: string;
  
  name: string;
  
  email: string;
  
  };
  
  type UserWithoutEmail = Omit<User, "email">;
  ```

4. 泛型约束

   * 使用场景：使用泛型虽然增加了扩展性，但是当我们需要使用到某些类型的特定特性（如字符串的length属性）时，就会需要泛型约束来完善这样的机制了

   * 用例：

     ```typescript
     interface Length {
       length: number;
     }
     
     function identity<T extends Length>(arg: T): T {
       console.log(arg.length); // 可以获取length属性
       return arg;
     }
     ```

   * tips:
     * 泛型约束可以有多个，通过逗号隔开，如**<T extends Length, Type2, Type3>**

5. 泛型参数默认类型

   * 用例 

     ```typescript
     interface A<T=string> {
       name: T;
     }
     
     const strA: A = { name: "Semlinker" };
     const numB: A<number> = { name: 101 };
     ```

   * TIPS:

     * 有默认类型的类型参数被认为是可选的。

     * 必选的类型参数不能在可选的类型参数后。

     * 如果类型参数有约束，类型参数的默认类型必须满足这个约束。

     * 当指定类型实参时，你只需要指定必选类型参数的类型实参。 未指定的类型参数会被解析为它们的默认类型。

     * 如果指定了默认类型，且类型推断无法选择一个候选类型，那么将使用默认类型作为推断结果。

     * 一个被现有类或接口合并的类或者接口的声明可以为现有类型参数引入默认类型。

     * 一个被现有类或接口合并的类或者接口的声明可以引入新的类型参数，只要它指定了默认类型。

6. 泛型工具类型：

   * `partial`

     * 作用：将某个类型里的属性全部变为可选项

     * 用例：

       ```typescript
       interface Todo {
         title: string;
         description: string;
       }
       
       function updateTodo(todo: Todo, fieldsToUpdate: Partial<Todo>) {
         return { ...todo, ...fieldsToUpdate };
       }
       ```

       上面代码中定义 `fieldsToUpdate` 的类型为 `Partial<Todo>`，即

       ```
       {
          title?: string | undefined;
          description?: string | undefined;
       }
       ```

       

