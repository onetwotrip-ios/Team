# iOS Interview

### 0. Test
* Что такое isa?
* Чем отличается id от NSObject? 
* Чем отличается категория от экстеншена (расширения)?
* Какие виды контейнеров (массив, сет, словарь) есть в iOS? Каких нет? Чем они отличаются?
* Очереди в GCD. Из чего? Кто выполняет задачи? Какие виды очередей есть в GCD?
* Чем отличается release от autorelease? (*)
* Какие свойства отвечают за позиционирование UIView? Как они между собой связаны? (*)
* Как устроен механизм self-sizing'а у UIView? 

Приемлемый результат: 4/8

### 1. Snippets

- Что выведется в консоль в при выполнении метода -method объекта класса C?

```objc
@interface A : NSObject
- (void)someMethod;
@end

@implementation A
- (void)someMethod {
    NSLog(@"This is class A");
}
@end

@interface B : A
@end

@implementation B
- (void)someMethod {
    NSLog(@"This is class B");
}
@end

@interface C : NSObject
@end

@implementation C
- (void)method {
    A *a = [B new];
    [a someMethod];
}
```

- Все ли в порядке с этим кодом?

```objc
- (void)viewDidLoad
{
    UILabel *label = [UILabel new];
    label.text = @"Pending...";
    [self.view addSubview: label];
    
    dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
        label.text = @"Some text";
    });
}
```

- Что выведется в консоль?

```objc
__block int i = 0; 
dispatch_async(dispatch_get_main_queue(), ^{
    NSLog(@"A %d", ++i);
    dispatch_async(dispatch_get_main_queue(), ^{
        NSLog(@"B %d", ++i);
    });
    NSLog(@"C %d", ++i);
});
NSLog(@"D %d", ++i);
```

- Что будет выведено в консоль?

```objc

- (void) method
{
    int i = 0;
    void (^block)() = ^{
        ++i;
    };
    
    block();
    NSLog(@"%d", i);
}
```

### 2. Language Mechanisms
#### Objective C
- Runtime and Messaging (`isa`, `selector`, object structure)
- Categories and extensions (caveats, usecases)
- Blocks (nature, `__block`, memory caveats)

#### Swift
- `Enums`. What's different from `C`.
- `Optionals`. Mechanism and usecases.

### 3. Platform

- Memory Management (Paradigm, `MRC`, `ARC`)
- Layout (Auto, Manual. Storyboards, Xibs. `Constraint`, `AutoresizingMask`)

### 4. Architecture
- Patterns (SOLID, SOA, Modul Constuction Concepts (MVC, MVVM, VIPER))



#Interviewer cheatsheet
- Code sharing: [CodeShare](https://codeshare.io), [Kobra](https://kobra.io/)
