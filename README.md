IOS SDK for Mondido Payments
=======

Version 1.3


The iOS SDK provides developers with a easy-to-use library to make payments in their iOS application. 
Open the included demo application and see how it works.

Example:
```
- (void)viewDidLoad
{
    [super viewDidLoad];

    //Find your settings here: https://admin.mondido.com/en/settings
    mondido = [[MondidoBase alloc] init];
    //mondido.template_id = @"1"; //to hard code the payment template
    [mondido.meta_data setObject:@"productName" forKey:@"metadata[products][1][name]"];
    [mondido.meta_data setObject:@"red" forKey:@"metadata[products][1][color]"];
    
    mondido.payUrl = @"https://pay.mondido.com/v1/form?lang=en";
    mondido.amount = @"1.00";
    mondido.currency = @"sek"; //must be in lower case
    mondido.merchant_id = @"233";
    mondido.secret = @"$2a$10$gU.z.9QNc8VSGYqcJSOhv."; // should not store secret in app.
    mondido.payment_ref = @"test1";
    mondido.customer_ref = @"customer1";
    mondido.mondido_hash = @"";
    mondido.success_url = @"https://mondido.com/success";
    mondido.error_url = @"https://mondido.com/fail";
    mondido.test = @"true";
    mondido.webhook = @"{\"trigger\":\"payment_success\",\"email\":\"youremail+ios@gmail.com\"}";
    mondido.payment_ref = mondido.randomOrderId; //just for testing. remove in production.
    mondido.mondido_hash = mondido.createHash; //should be loaded from backend
    paymentView = mondido.createWebView; //create one here instead of storyboard/xib
    [self.view addSubview:paymentView]; //add view to stage. default is streatched over the whole screen.
    
    [mondido makeHostedPayment:paymentView withCallback:^(PaymentStatus status) {
        if(status == SUCCESS){
            //success
        }else{
            //problems
        }
     }];
}
```
