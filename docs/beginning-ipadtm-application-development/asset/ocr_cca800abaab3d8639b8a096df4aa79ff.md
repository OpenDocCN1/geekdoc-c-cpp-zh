![](bbox=[0.1, 0.16, 0.52, 0.43])

FIGURE 18-20

3. Populate the MyAnnotation.h file as follows:

```
#import <Foundation/Foundation.h>
#import <MapKit/MapKit.h>

@interface MyAnnotation : NSObject <MKAnnotation> {

    CLLocationCoordinate2D coordinate;
    NSString *title;
    NSString *subTitle;
}

@property (nonatomic, readonly) CLLocationCoordinate2D coordinate;
@property (nonatomic, retain) NSString *title;
@property (nonatomic, retain) NSString *subTitle;

- (id)initWithCoordinate:(CLLocationCoordinate2D) c
                 title:(NSString *) t
               subTitle:(NSString *) st;

- (void) moveAnnotation: (CLLocationCoordinate2D) newCoordinate;
- (NSString *)subtitle;
- (NSString *)title;

@end
```

4. Populate the MyAnnotation.m file as follows:

```
#import "MyAnnotation.h"

@implementation MyAnnotation

@synthesize coordinate;
@synthesize title;
@synthesize subTitle;

- (NSString *)subtitle {
    return subTitle;
}
```