# Action Mailer

**Proposed Interface**

## USAGE

Action Mailer users directory conventions to map Mailer classes
to corresponding mailer views

````
import ActionMailer from 'action-mailer'

ActionMailer.configure(config => {
  config.mailers = __dirname+'/app/mailers'
  config.views   = __dirname+'/app/views'
})
````

````
bridges generate mailer user_payment
````

````
// in app/mailers/user_payment_mailer.js

class UserPaymentMailer extends ActionMailer.Base {
  get from() { return 'steven@anypay.io' }

  paymentReceivedEmail(payment, user) {

    this.payment = payment

    this.mail({
      to:user.email,
      subject: 'You received a payment of gold!'
    })
  }
}
````

The mailer will load its view from the corresponding views directory

````
app/views/user_payment_mailer/payment_received_email.html.ejs

<h1>Payment Received</h1>

<p>You received a payment of <%= payment.amount %> ounces gold!</p>
````

