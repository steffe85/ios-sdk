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

===========

# Mondido Payments Documentation

Our focus is to make it as smooth as possible for you to implement Mondido and start accepting payments, regardless of whether you are implementing from scratch or already have an existing payment service in place.

Read more
* https://doc.mondido.com/

## Supported Card Types
Default card types that you will have access to are VISA and Mastercard, but the other such as AMEX, JCB and Diners are on separate contracts. Contact support for more information about card types.

* https://doc.mondido.com/api#cardtypes

## Test Cards
To create test transactions you need to send in a test card number, and also a CVV code that can simulate different responses

* https://doc.mondido.com/api#testcards

## Error messages
We aim to send as many insightful and helpful error messages to you as possible, both in numeric, data and human readable.

* https://doc.mondido.com/api#errors

# Help

* FAQ (Swedish) - http://help.mondido.com/

# PCI DSS

Mondido is a certified payment provider compliant to Level 1 Payment Card Industry Data Security Standard (PCI DSS) version 3.1 to provide a secure transaction for merchants and their customers. PCI compliance for merchants is required for any business accepting cardholder data. Let Mondido capture this sensitive information using one of our Hosted Window or mondido.js solutions to avoid PCI compliance issues.

* Payment Card Industry Data Security Standard (PCI DSS) - https://www.pcicomplianceguide.org/pci-faqs-2/#5
* Payment security educational resources - https://www.pcisecuritystandards.org/pci_security/educational_resources
* Hosted Window - https://doc.mondido.com/hosted

# 3D-Secure

Mondido understands the need to incorporate best business practices in security. That's why we've made it easy for merchants to implement 3D Secure or “3 Domain Secure” as the industry standard identity check solution to minimize chargebacks from fraudulent credit cards, all included in our simple pricing. 3D-Secure refers to second authentication factor products such as Verified by Visa, MastercardⓇSecureCode™, American Express SafekeyⓇ, and JCB J/Secure™.

NOTE: While you can create your own payment experience, We strongly recommend using our Hosted Window or Mondido.js solution to save time in implementing 3D-Secure and client side encryption to your checkout procedure.

* Verified by Visa - http://www.visaeurope.com/making-payments/verified-by-visa/
* MastercardⓇSecureCode™ - https://www.mastercard.us/en-us/merchants/safety-security.html
* American Express SafekeyⓇ  - https://www.americanexpress.com/uk/content/safekey-information.html?linknav=uk-securitycentre-home-safekey-learn
* JCB J/Secure™ - http://www.global.jcb/en/

# SSL

Secure Socket Layer is required to securely transfer cardholder data and payment information to Mondido. It is recommended that you purchase a SSL certificate directly through a recognized certification authority such as TrustwaveⓇ, HTTPS.SE or purchase a custom SSL certificate through your current e-commerce solution.

* TrustwaveⓇ - https://ssl.trustwave.com/buy-ssl-certificate?___s=1
* HTTPS.SE - https://https.se/

# Follow us on
* GitHub - https://github.com/Mondido
* Facebook - https://www.facebook.com/mondidopayments
* Twitter https://twitter.com/mondidopay
* LinkedIn  - https://www.linkedin.com/company/mondido
* Instagram - https://www.instagram.com/mondidopay/

