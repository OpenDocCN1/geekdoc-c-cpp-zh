
该问题的通用解决方案是*递归地*调用 raytrace()，终止递归的条件（即所谓的“基本情况”）是当光线遇到非反射或非透明表面时（或达到预先确定的最大深度时），或者光线没有与任何物体发生碰撞时。不幸的是，GLSL 不支持递归。因此，为了对上述效果进行任何合理的模拟，我们需要自己跟踪递归。

在缺乏原生递归支持的情况下，构建 raytrace() 的递归版本并非易事。我们的解决方案需要一个*栈*，为要压入栈的项定义一个结构，构建适当的*压入*和*弹出*操作，一个包含用于处理光线的主循环的*驱动程序*（使用栈操作），以及一个用于*处理*栈元素的函数（该元素包含单个光线的信息）。

程序 16.12 将这些展示为对之前程序 16.11 中元素的添加（和替换）。有一个名为 Stack_Element 的结构体，它定义了存储在栈中的项，以及用于 raytrace()（即驱动程序）、push()、pop() 和 process_stack_element() 的函数。栈本身存储为 Stack_Elements 的数组。在展示代码之后，将给出更详细的解释。

## 程序 16.12 – 递归光线生成

### 计算着色器

```cpp
...
struct Stack_Element
{
    int type;       // type of ray (1 = reflected, 2 = refracted. Shadow rays are never pushed on stack)
    int depth;      // depth of the recursive raytrace
    int phase;      // which of the five phases of a recursive call is currently being processed
    vec3 phong_color;      // holds the computed ADS color
    vec3 reflected_color;  // holds the reflected color
    vec3 refracted_color;  // holds the refracted color
    vec3 final_color;      // final mixture of all colors (plus texture) for this invocation
    Ray ray;               // the ray for this raytrace invocation
    Collision collision;   // the collision for this raytrace invocation. Starts with null_collision value.
};
const int RAY_TYPE_REFLECTION = 1;
const int RAY_TYPE_REFRACTION = 2;

// "NULL" values for structs are defined to make it easier to tell when a value hasn't been assigned
Ray null_ray = {vec3(0.0), vec3(0.0)};
Collision null_collision = {-1.0, vec3(0.0), vec3(0.0), false, -1, vec2(0.0, 0.0), -1};

Stack_Element null_stack_element = { 0, -1, 0, vec3(0), vec3(0), vec3(0), vec3(0), null_ray, null_collision };

const int stack_size = 100;
Stack_Element stack[stack_size];        // holds the "recursive" stack of raytrace invocations
const int max_depth = 6;                // max sequence of rays, which equals max recursion depth
int stack_pointer = -1;                 // Points to the top of the stack (-1 if empty)
Stack_Element popped_stack_element;     // Holds the last popped element from the stack

// The "push" function, which schedules a new raytrace by adding it to the top of the stack
void push(Ray r, int depth, int type)
{  if (stack_pointer >= stack_size-1)  return;     // if there is no more room on the stack, exit

   Stack_Element element;   // initialize those fields that we already know, and set others to zero or null
   element = null_stack_element;
   element.type = type;
   element.depth = depth;
   element.phase = 0;
   element.ray = r;

   stack_pointer++;
   stack[stack_pointer] = element;      // add this element to the stack
}

// The "pop" function, which removes a raytrace operation that has been completed
Stack_Element pop()
{  // removes and returns the top stack element
   Stack_Element top_stack_element = stack[stack_pointer];
   stack[stack_pointer] = null_stack_element;
   stack_pointer--;
   return top_stack_element;
}

// 5-phase processing of a ray: (1) collision, (2) lighting, (3) reflection, (4) refraction, (5) mixing
void process_stack_element(int index)
{  // if there is a popped_stack_element that was previously processed, it holds reflection/refraction
   // information for the current stack element. Store that info, then clear the popped element reference.

   if (popped_stack_element != null_stack_element)    // GLSL element-wise comparison of structs
   {  if (popped_stack_element.type == RAY_TYPE_REFLECTION)
         stack[index].reflected_color = popped_stack_element.final_color;
      else if (popped_stack_element.type == RAY_TYPE_REFRACTION)
         stack[index].refracted_color = popped_stack_element.final_color;
      popped_stack_element = null_stack_element;
   }
   Ray r = stack[index].ray;           // initialized by the initial call
   Collision c = stack[index].collision;  // starts null, gets set in phase 1

   switch (stack[index].phase)
   {  // ========== PHASE 1 - raytrace collision detection
case 1:
    c = get_closest_collision(r);                  // Cast ray into the scene, store collision result
    if (c.object_index != -1)                       // If the ray didn't hit anything, stop.
        stack[index].collision = c;                 // Otherwise, store the collision result
    break;
// ========== PHASE 2 – Phong ADS lighting computation
case 2:
    stack[index].phong_color = ads_phong_lighting(r, c);
    break;
// ========== PHASE 3 – generate a reflection ray
case 3:
    if (stack[index].depth < max_depth)             // stop if at max depth
    {   if ((c.object_index == 1) || (c.object_index == 2))  // only sphere and box are reflective
        {
            Ray reflected_ray;
            reflected_ray.start = c.p + c.n * 0.001;
            reflected_ray.dir = reflect(r.dir, c.n);
            // add a raytrace for that ray to the stack, and set its type to reflection
            push(reflected_ray, stack[index].depth+1, RAY_TYPE_REFLECTION);
        }
    }
    break;
// ========== PHASE 4 – generate a refraction ray
case 4:
    if (stack[index].depth < max_depth)             // stop if at max depth
    {   if (c.object_index == 1)                    // only the sphere is transparent
        {
            Ray refracted_ray;
            refracted_ray.start = c.p - c.n * 0.001;
            float refraction_ratio = 0.66667;
            if (c.inside) refraction_ratio = 1.5; // 1.0 / refraction_ratio, when ray exits the sphere
            refracted_ray.dir = refract(r.dir, c.n, refraction_ratio);
            // Add a raytrace for that ray to the stack
            push(refracted_ray, stack[index].depth+1, RAY_TYPE_REFRACTION);
        }
    }
    break;
// ========== PHASE 5 – mixing
case 5:
    if (c.object_index == 1)        // for the sphere, blend reflection, refraction, and lighting
    {
        stack[index].final_color = stack[index].phong_color *
            (0.3 * stack[index].reflected_color) + (2.0 * (stack[index].refracted_color));
    }
    if (c.object_index == 2)        // for the box, blend reflection, lighting, and texture
    {
        stack[index].final_color = stack[index].phong_color *
            ((0.5 * stack[index].reflected_color) + (1.0 * (texture(sampMarble, c.tc)).xyz));
    }
        if (c.object_index == 3) stack[index].final_color = stack[index].phong_color * rbox_color;
        if (c.object_index == 4) stack[index].final_color = stack[index].phong_color *
            (checkerboard(c.tc)).xyz;
        break;
// ============ when all five phases are complete, end the recursion
case 6:
    popped_stack_element = pop();
    return;
}
stack[index].phase++;
return;    // only process one phase per process_stack_element() invocation
}

// This is the "driver" function that sends out the first ray,
// and then processes secondary rays until all have completed
vec3 raytrace(Ray r)
{  push(r, 0, RAY_TYPE_REFLECTION);
    while (stack_pointer >= 0) {          // process the stack until it is empty
        int element_index = stack_pointer;     // peek at the topmost stack element
        process_stack_element(element_index);  // process next phase of the current stack element
    }
    return popped_stack_element.final_color;   // final color of the last-popped stack element
}
```

在程序 16.12 中，栈是一个由 Stack_Element 类型结构体组成的数组，因此一个 Stack_Element 实例包含处理任意给定光线所需的全部信息。执行栈压入和弹出的函数——push() 和 pop()——应该很直接。栈的大小必须谨慎选择；如果存在许多既反射又折射的物体，光线的数量可能会呈指数增长。然而，在实践中，许多光线在达到最大递归深度之前就因为与天空盒碰撞而终止。

光线追踪从 raytrace() 开始。尽管所有光线都需要设置其类型（反射或折射），但初始光线的类型并未被使用——我们任意地将其设置为反射。然后我们开始处理栈中的所有光线（通过反复调用 process_stack_element()），在此过程中，次级（以及后续）光线也可能被生成并添加到栈中。当一条光线的所有处理都完成后，其最终计算出的颜色便可供其“父”光线使用，而父光线又可以利用它来计算自己的颜色。

所有这些——光线追踪处理的核心内容——都在 process_stack_element() 中完成，它被组织为五个阶段的一系列操作。每个阶段基本上与本 chapter 早期程序中看到的步骤相同。其中一些
