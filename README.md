# UIGestureRecognizer-ObjectiveC
UIGestureRecognizer-ObjectiveC

# UIGestureRecognizer Subclasses

# Detecting taps with UITapGestureRecognizer

``` objective-c
//
//  ViewController.m
//  AlertViewControllerExample
//
//  Created by Carlos Santiago Cruz on 4/17/19.
//  Copyright © 2019 Carlos Santiago Cruz. All rights reserved.
//

#import "ViewController.h"

@interface ViewController () <UIGestureRecognizerDelegate>
{
    UIButton *button;
    UITapGestureRecognizer *doubleTapRecognizer;
    UIView *viewToTap;
}
@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];

    CGFloat widthButton = 60;
    CGFloat heightButton = 60;
    CGFloat abscissaCenteredButton = self.view.frame.size.width/2 - widthButton/2;
    CGFloat ordinateCenteredButton = self.view.frame.size.height/2 - heightButton/2;

    CGRect buttonFrame = CGRectMake(abscissaCenteredButton,
                                    ordinateCenteredButton,
                                    widthButton,
                                    heightButton);
    button = [[UIButton alloc] initWithFrame:buttonFrame];
    [button setTitle:@"button" forState:UIControlStateNormal];
    [button setBackgroundColor:[UIColor blackColor]];
    // target-action patter explicitly shown.
    [button addTarget:self action:@selector(buttonTapped) forControlEvents:UIControlEventTouchUpInside];
    [self.view addSubview:button];
    
    // Detecting taps with UITapGestureRecognizer on a view
    CGFloat widthViewToTap = 60;
    CGFloat heightViewToTap = 60;
    CGFloat abscissaCenteredViewToTap = self.view.frame.size.width/2 - widthViewToTap/2;
    CGFloat ordinateCenteredViewToTap = self.view.frame.size.height/2 - heightViewToTap/2 - 3*widthButton;
    viewToTap = [[UIView alloc] initWithFrame:CGRectMake(abscissaCenteredViewToTap,
                                                         ordinateCenteredViewToTap,
                                                         widthViewToTap,
                                                         heightViewToTap)];
    viewToTap.backgroundColor = [UIColor grayColor];
    [self.view addSubview:viewToTap];
    
    doubleTapRecognizer = [[UITapGestureRecognizer alloc] initWithTarget:self action:@selector(doubleTap:)];
    doubleTapRecognizer.numberOfTapsRequired = 2;
    doubleTapRecognizer.delegate = self;
    [viewToTap addGestureRecognizer:doubleTapRecognizer];
    
}
- (void)doubleTap:(UIGestureRecognizer *)gestureRecognizer
{
    NSLog(@"Recognized Double Tap");
}

- (void)buttonTapped
{
    UIAlertController *alert = [UIAlertController alertControllerWithTitle:@"This is my first alert, be nice"
                                                                   message:@"This is a simple alert"
                                                            preferredStyle:UIAlertControllerStyleAlert];
    
    UIAlertAction *oKButton = [UIAlertAction actionWithTitle:@"OK"
                                                       style:UIAlertActionStyleDefault
                                                     handler:nil];
    [alert addAction:oKButton];
    
    NSMutableAttributedString *attributedStringTitle = [[NSMutableAttributedString alloc]initWithString:@"This is my first alert, be nice"];
    [attributedStringTitle addAttribute:NSForegroundColorAttributeName
                                  value:[UIColor redColor]
                                  range:NSMakeRange(0,[attributedStringTitle length])];
    [attributedStringTitle addAttribute:NSFontAttributeName
                                  value:[UIFont fontWithName:@"HelveticaNeue-Light" size:20]
                                  range:NSMakeRange(0,[attributedStringTitle length])];
    [alert setValue:attributedStringTitle forKey:@"attributedTitle"];
    
    NSMutableAttributedString *attributedStringMessage = [[NSMutableAttributedString alloc]initWithString:@"This is a simple alert"];
    [attributedStringMessage addAttribute:NSForegroundColorAttributeName
                                  value:[UIColor blueColor]
                                  range:NSMakeRange(0,[attributedStringMessage length])];
    [attributedStringMessage addAttribute:NSFontAttributeName
                                  value:[UIFont fontWithName:@"HelveticaNeue-Light" size:20]
                                  range:NSMakeRange(0,[attributedStringMessage length])];
    [alert setValue:attributedStringMessage forKey:@"attributedMessage"];
    
    [self presentViewController:alert animated:YES completion:^{
        sleep(2);
        [self->button setBackgroundColor:[UIColor redColor]];
    }];
}
@end
```

``` console
2019-04-29 00:07:16.646996-0600 AlertViewControllerExample[26051:2321451] Recognized Double Tap
2019-04-29 00:07:17.309023-0600 AlertViewControllerExample[26051:2321451] Recognized Double Tap
2019-04-29 00:07:18.177142-0600 AlertViewControllerExample[26051:2321451] Recognized Double Tap
```

![Captura de Pantalla 2019-04-29 a la(s) 0 04 03](https://user-images.githubusercontent.com/24994818/56877304-461c7c80-6a0a-11e9-9b4a-0526d9a81893.png)

