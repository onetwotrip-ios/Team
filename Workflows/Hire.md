# iOS Interview

### 0. Test
* 
*
*
*
*
*

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


- Какие есть проблемы с этим кодом?
```objc

@interface OTTPlayground : NSObject
@end

@implementation OTTPlayground

- (void) post
{
  dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0), ^{
    [[NSNotificationCenter defaultCenter] postNotificationName: @"someNotification" object: nil];
  });
}

- (void) subscribe
{
  dispatch_async(dispatch_get_main_queue(), ^{
    [[NSNotificationCenter defaultCenter] addObserver: self
                                             selector: @selector(someMethod)
                                                 name: @"someNotification"
                                               object: nil];
  });
}

- (void) someMethod
{
  NSLog(@"Hello world");
}

- (instancetype) init
{
  if (self = [super init])
  {
    [self subscribe];
    [self post];
  }
  return self;
}

@end
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